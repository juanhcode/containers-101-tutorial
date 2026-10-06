---
title: "Parte 2 · Dockerfile"
nav_order: 4
---

# Parte 2 · Crear el Dockerfile

El Dockerfile es la **receta** que le dice a Docker cómo construir la imagen de tu app.

## 2.1 Crear el Dockerfile

Crea un archivo llamado `Dockerfile` (sin extensión) en la raíz de `mi-app/`:

```dockerfile
# 1. Imagen base: Node.js sobre Alpine Linux (liviana)
FROM node:20-alpine

# 2. Directorio de trabajo dentro del contenedor
WORKDIR /app

# 3. Copiar primero las dependencias (aprovecha la caché de Docker)
COPY package.json .

# 4. Instalar dependencias
RUN npm install --production

# 5. Copiar el resto del código
COPY . .

# 6. Documentar el puerto que usa la app
EXPOSE 3000

# 7. Comando que se ejecuta al iniciar el contenedor
CMD ["node", "server.js"]
```

## Las instrucciones esenciales

| Instrucción | Qué hace |
|---|---|
| `FROM` | Imagen base de partida |
| `WORKDIR` | Directorio de trabajo dentro del contenedor |
| `COPY` | Copia archivos a la imagen |
| `RUN` | Ejecuta comandos durante la construcción |
| `EXPOSE` | Documenta el puerto que usa la app |
| `CMD` | Comando que corre al iniciar el contenedor |

## 2.2 Crear el .dockerignore

Crea un archivo `.dockerignore`:

```
node_modules
.git
*.log
.env
.DS_Store
```

{: .note }
> **¿Por qué?** Imágenes más livianas, builds más rápidos, y evitas filtrar archivos sensibles.

{: .highlight }
> ✅ **Checkpoint:** Tienes el código + Dockerfile + .dockerignore listos.

---

[← Parte 1](parte-1-app){: .btn } [Siguiente: Parte 3 · Construir la imagen →](parte-3-build){: .btn .btn-primary }
