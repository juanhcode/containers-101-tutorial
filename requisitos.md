---
title: Requisitos previos
nav_order: 2
---

# Requisitos previos

Antes de empezar, asegúrate de tener instalado:

| Herramienta | Instalación |
|---|---|
| **Docker Desktop** | [docs.docker.com/get-docker](https://docs.docker.com/get-docker/) |
| **AWS CLI v2** | [docs.aws.amazon.com/cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |
| **Node.js** (solo para crear la app de ejemplo) | [nodejs.org](https://nodejs.org/) |
| **Una cuenta de AWS** | [aws.amazon.com/free](https://aws.amazon.com/free/) |

Verifica que todo funcione:

```bash
docker --version
aws --version
node --version
```

Configura tus credenciales de AWS si no lo has hecho:

```bash
aws configure
# AWS Access Key ID: <TU_ACCESS_KEY>
# AWS Secret Access Key: <TU_SECRET_KEY>
# Default region: <REGION>       (ej. us-east-1)
# Default output format: json
```

---

[Siguiente: Parte 1 · Crear la app →](parte-1-app){: .btn .btn-primary }
