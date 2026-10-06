---
title: "Parte 5 · Subir a Amazon ECR"
nav_order: 7
---

# Parte 5 · Subir la imagen a Amazon ECR

Tu imagen solo existe en tu computador. Vamos a llevarla a **Amazon Elastic Container Registry (ECR)**, el registry privado de AWS.

## 5.1 Definir variables

Cambia estos valores por los tuyos:

```bash
export AWS_ACCOUNT_ID=<ACCOUNT_ID>      # ej. 123456789012
export AWS_REGION=<REGION>              # ej. us-east-1
export REPO_NAME=mi-app
export IMAGE_TAG=v1
```

## 5.2 Crear el repositorio en ECR

```bash
aws ecr create-repository \
  --repository-name $REPO_NAME \
  --region $AWS_REGION
```

> Crea un repositorio vacío en ECR. Obtienes una URL tipo:
> `<ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/mi-app`

## 5.3 Autenticarse contra ECR

```bash
aws ecr get-login-password --region $AWS_REGION \
  | docker login --username AWS --password-stdin \
    $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com
```

Deberías ver: **Login Succeeded**.

{: .note }
> ECR es privado: sin este paso Docker no tiene permiso para subir imágenes.

## 5.4 Taggear la imagen para ECR

Docker necesita saber a dónde enviarla:

```bash
docker tag mi-app:latest \
  $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$REPO_NAME:$IMAGE_TAG
```

Verifica:

```bash
docker images | grep $REPO_NAME
```

## 5.5 Subir la imagen (push)

```bash
docker push \
  $AWS_ACCOUNT_ID.dkr.ecr.$AWS_REGION.amazonaws.com/$REPO_NAME:$IMAGE_TAG
```

> Docker sube cada capa de la imagen al repositorio. Solo sube las capas que no existan allá.

## 5.6 Verificar en ECR

```bash
aws ecr list-images \
  --repository-name $REPO_NAME \
  --region $AWS_REGION
```

Deberías ver tu imagen con el tag `v1`.

## ¿Qué pasó?

```
ANTES                              DESPUÉS
───────────                        ───────────
Tu máquina                         Tu máquina
└── Docker Image (mi-app)          └── Docker Image (mi-app)
                                       │
                                   AWS │
                                       └── ECR: mi-app:v1  ✓
```

{: .highlight }
> ✅ **Checkpoint:** Tu imagen está en AWS. Cualquier servicio con permisos puede descargarla.

---

[← Parte 4](parte-4-run){: .btn } [Siguiente: Parte 6 · Ejecutar en EC2 →](parte-6-ec2){: .btn .btn-primary }
