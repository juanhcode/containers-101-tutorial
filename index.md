---
title: Inicio
layout: home
nav_order: 1
---

# 🐳 Contenedores 101

## Construye, ejecuta y despliega en AWS

> **Tutorial práctico paso a paso**
>
> Lleva una aplicación desde tu computador hasta AWS, siguiendo el viaje completo:
>
> `Código → Dockerfile → docker build → Docker Image → docker run → Amazon ECR → EC2 → App en la nube`

---

### ¿Qué vas a aprender?

| Parte | Tema |
|---|---|
| [Requisitos previos](requisitos) | Herramientas necesarias |
| [Parte 1 · Crear la app](parte-1-app) | App Node.js mínima |
| [Parte 2 · Dockerfile](parte-2-dockerfile) | La receta para construir la imagen |
| [Parte 3 · Construir la imagen](parte-3-build) | `docker build` y capas |
| [Parte 4 · Ejecutar el contenedor](parte-4-run) | `docker run`, puertos, volúmenes, ciclo de vida |
| [Parte 5 · Subir a Amazon ECR](parte-5-ecr) | Registry, tag, push |
| [Parte 6 · Ejecutar en EC2](parte-6-ec2) | La app corriendo en la nube |
| [Parte 7 · Introducción a EKS](parte-7-eks) | Orquestación con Kubernetes |
| [Limpieza](parte-8-limpieza) | Eliminar recursos para no generar costos |

---

### El viaje completo

```
Código fuente (server.js)
         ↓
    Dockerfile (la receta)
         ↓
    docker build -t mi-app .
         ↓
    Docker Image (mi-app:latest)
         ↓
    docker run -p 8080:3000 mi-app
         ↓
    Contenedor corriendo local ✓
         ↓
    docker tag + docker push → Amazon ECR
         ↓
    ┌────────── AWS ──────────┐
    │  EC2 + Docker           │
    │       — ó —             │
    │  Amazon EKS (Pods)      │
    └─────────────────────────┘
         ↓
    App corriendo en la nube 🚀
```

---

**Speakers:** Juan Manuel Hoyos C. · Pablo Nicolás Marín G.

**Evento:** Universidad ICESI · Cali, Colombia
