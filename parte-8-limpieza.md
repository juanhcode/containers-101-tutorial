---
title: "Limpieza"
nav_order: 10
---

# Limpieza

{: .warning }
> ⚠️ Para evitar costos inesperados, elimina los recursos que creaste.

## EC2

```bash
# Desde la consola de AWS: termina la instancia
# O con CLI:
aws ec2 terminate-instances --instance-ids <INSTANCE_ID>
```

## ECR

```bash
# Eliminar las imágenes del repositorio
aws ecr batch-delete-image \
  --repository-name mi-app \
  --image-ids imageTag=v1

# Eliminar el repositorio
aws ecr delete-repository \
  --repository-name mi-app \
  --region <REGION>
```

## EKS (si lo creaste)

```bash
kubectl delete -f deployment.yaml
eksctl delete cluster --name mi-cluster --region <REGION>
```

## Docker local

```bash
docker stop mi-contenedor
docker rm mi-contenedor
docker rmi mi-app
```

---

## 🎉 ¡Felicidades!

Completaste el viaje completo:

```
Código → Dockerfile → build → Image → run → Container
    → ECR → EC2 → App corriendo en AWS 🚀
```

Ahora te toca **construir, ejecutar y desplegar** tus propias aplicaciones.

---

## Recursos

- [Docker Docs](https://docs.docker.com/)
- [Dockerfile reference](https://docs.docker.com/reference/dockerfile/)
- [Amazon ECR User Guide](https://docs.aws.amazon.com/AmazonECR/latest/userguide/)
- [Amazon EC2 Getting Started](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/)
- [Amazon EKS User Guide](https://docs.aws.amazon.com/eks/latest/userguide/)
- [eksctl - Getting Started](https://eksctl.io/)
- [Kubernetes Docs](https://kubernetes.io/docs/home/)

---

[← Parte 7](parte-7-eks){: .btn }
