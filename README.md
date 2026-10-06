# 🐳 Contenedores 101 — Tutorial

Tutorial práctico de la charla **"Contenedores 101: construye, ejecuta y despliega en AWS"**.

Lleva una aplicación desde el código fuente hasta ejecutarse en AWS:

```
Código → Dockerfile → docker build → Docker Image → docker run
    → Amazon ECR → EC2 / EKS → App en la nube
```

## 🌐 Ver el sitio

El tutorial está publicado con **GitHub Pages**:

👉 **https://juanhcode.github.io/containers-101-tutorial/**

## Contenido

1. Requisitos previos
2. Crear la app (Node.js)
3. Crear el Dockerfile
4. Construir la imagen (`docker build`)
5. Ejecutar el contenedor (`docker run`)
6. Subir la imagen a Amazon ECR
7. Ejecutar el contenedor en EC2
8. Introducción a EKS
9. Limpieza de recursos

## Desarrollo local (opcional)

Este sitio usa Jekyll con el tema [just-the-docs](https://just-the-docs.com/):

```bash
bundle install
bundle exec jekyll serve
```

---

**Speakers:** Juan Manuel Hoyos C. · Pablo Nicolás Marín G.
**Evento:** Universidad ICESI · Cali, Colombia
