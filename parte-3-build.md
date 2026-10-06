---
title: "Parte 3 · Construir la imagen"
nav_order: 5
---

# Parte 3 · Construir la imagen

## 3.1 docker build

```bash
docker build -t mi-app .
```

| Parte | Significado |
|---|---|
| `docker build` | Ejecuta la construcción |
| `-t mi-app` | Le da un nombre (tag) a la imagen |
| `.` | Usa el Dockerfile del directorio actual |

Docker ejecuta cada instrucción del Dockerfile, crea una **capa** por cada paso, y empaqueta todo en una imagen.

## 3.2 Verificar que la imagen existe

```bash
docker images
```

```
REPOSITORY   TAG       IMAGE ID       SIZE
mi-app       latest    abc123def456   142MB
```

## Capas (layers)

Cada instrucción del Dockerfile crea una **capa** apilada y cacheable. Por eso copiamos `package.json` e instalamos dependencias **antes** de copiar todo el código: si tu código cambia pero las dependencias no, Docker reutiliza esa capa y el build es mucho más rápido.

{: .highlight }
> ✅ **Checkpoint:** Tienes una Docker Image lista para ejecutar.

---

[← Parte 2](parte-2-dockerfile){: .btn } [Siguiente: Parte 4 · Ejecutar el contenedor →](parte-4-run){: .btn .btn-primary }
