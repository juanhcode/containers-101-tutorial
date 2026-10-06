---
title: "Parte 7 · Introducción a EKS"
nav_order: 9
---

# Parte 7 · ¿Y si necesitamos escalar? Introducción a EKS

Con un solo contenedor en una EC2 todo funciona. Pero cuando la app crece:

- ¿Quién reinicia un contenedor si se cae?
- ¿Quién reparte el tráfico entre varias réplicas?
- ¿Quién escala según la demanda?
- ¿Quién hace actualizaciones sin downtime?

Para eso existe **Kubernetes**, y en AWS se usa **Amazon EKS** (Elastic Kubernetes Service).

## Conceptos clave de Kubernetes

| Concepto | Qué es |
|---|---|
| **Cluster** | Conjunto de máquinas donde corren tus contenedores |
| **Node** | Una máquina del cluster (normalmente una EC2) |
| **Pod** | La unidad mínima: envuelve 1 o más contenedores |
| **Deployment** | Define el estado deseado (cuántas réplicas, qué imagen) |

## ¿Qué es Amazon EKS?

EKS es **Kubernetes administrado** por AWS:

- AWS gestiona el **control plane** (el cerebro de Kubernetes).
- Tus contenedores corren como **Pods** en **nodes** (EC2 o Fargate).
- **ECR proporciona las imágenes; EKS las ejecuta.**

```
Developer → docker build → Amazon ECR → Amazon EKS
                                            │
                                   ┌────────┴────────┐
                                   Cluster
                                   ├── Node → Pod → Container
                                   └── Node → Pod → Container
```

## Crear un cluster EKS (vista rápida)

{: .note }
> Esta sección es introductoria. Un setup completo de EKS va más allá de este tutorial.

La forma más simple es con [`eksctl`](https://eksctl.io/installation/):

```bash
eksctl create cluster \
  --name mi-cluster \
  --region <REGION> \
  --nodegroup-name workers \
  --node-type t3.small \
  --nodes 2
```

## Desplegar tu app en EKS

Crea `deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mi-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mi-app
  template:
    metadata:
      labels:
        app: mi-app
    spec:
      containers:
        - name: mi-app
          image: <ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/mi-app:v1
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: mi-app-service
spec:
  type: LoadBalancer
  selector:
    app: mi-app
  ports:
    - port: 80
      targetPort: 3000
```

```bash
# Configurar kubectl para tu cluster
aws eks update-kubeconfig --name mi-cluster --region <REGION>

# Desplegar
kubectl apply -f deployment.yaml

# Ver los pods
kubectl get pods

# Ver el servicio (URL del Load Balancer)
kubectl get svc mi-app-service
```

> EKS crea 3 réplicas de tu contenedor distribuidas en los nodes, con un Load Balancer delante.

{: .highlight }
> ✅ **Checkpoint:** Entiendes cómo Kubernetes orquesta muchos contenedores y cómo EKS lo administra en AWS.

---

[← Parte 6](parte-6-ec2){: .btn } [Siguiente: Limpieza →](parte-8-limpieza){: .btn .btn-primary }
