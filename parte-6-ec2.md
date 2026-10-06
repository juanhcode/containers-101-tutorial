---
title: "Parte 6 · Ejecutar en EC2"
nav_order: 8
---

# Parte 6 · Ejecutar el contenedor en EC2

La imagen está en ECR. Ahora vamos a ejecutarla en un servidor de AWS.

## 6.1 Lanzar una instancia EC2

Desde la **AWS Management Console** → **EC2** → **Launch Instance**:

| Configuración | Valor |
|---|---|
| **Nombre** | `mi-app-server` |
| **AMI** | Amazon Linux 2023 |
| **Tipo** | `t3.micro` (capa gratuita) |
| **Par de claves** | Crea uno nuevo o selecciona existente |
| **Security Group** | SSH (22) desde tu IP + TCP personalizado (8080) desde `0.0.0.0/0` |
| **IAM Instance Profile** | Rol con política `AmazonEC2ContainerRegistryReadOnly` |

{: .warning }
> El **IAM Role** es clave. Sin él la EC2 no tiene permiso para descargar imágenes de ECR.

## 6.2 Conectarse a la EC2

```bash
ssh -i <TU_LLAVE>.pem ec2-user@<IP_PUBLICA_EC2>
```

## 6.3 Instalar Docker en la EC2

```bash
# Instalar
sudo yum update -y
sudo yum install -y docker

# Iniciar el servicio
sudo systemctl start docker
sudo systemctl enable docker

# Permitir usar docker sin sudo
sudo usermod -aG docker ec2-user
newgrp docker

# Verificar
docker --version
```

## 6.4 Autenticarse contra ECR desde la EC2

```bash
aws ecr get-login-password --region <REGION> \
  | docker login --username AWS --password-stdin \
    <ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com
```

{: .note }
> Si la EC2 tiene un IAM Role con permisos de ECR, este comando funciona sin configurar claves.

## 6.5 Descargar y ejecutar

```bash
# Pull: descargar la imagen desde ECR
docker pull \
  <ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/mi-app:v1

# Run: ejecutar el contenedor
docker run -d -p 8080:3000 \
  <ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/mi-app:v1
```

## 6.6 Verificar

Desde tu navegador, abre:

```
http://<IP_PUBLICA_EC2>:8080
```

```json
{
  "message": "¡Hola desde un contenedor Docker! 🐳",
  "hostname": "a1b2c3d4e5f6",
  "timestamp": "2026-10-06T..."
}
```

🎉 **¡Tu app está corriendo en un contenedor en AWS!**

## Security Groups

El **Security Group** actúa como firewall de la instancia. Solo el tráfico por los puertos que configures llega al contenedor.

```
Usuario → Security Group (puerto 8080 ✓) → EC2 → Docker → Container:3000
```

{: .highlight }
> ✅ **Checkpoint:** Tu app corre en un contenedor en EC2, servida desde AWS.

---

[← Parte 5](parte-5-ecr){: .btn } [Siguiente: Parte 7 · Introducción a EKS →](parte-7-eks){: .btn .btn-primary }
