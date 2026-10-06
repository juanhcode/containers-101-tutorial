---
title: "Parte 4 · Ejecutar el contenedor"
nav_order: 6
---

# Parte 4 · Ejecutar el contenedor

## 4.1 docker run

```bash
docker run -d -p 8080:3000 --name mi-contenedor mi-app
```

| Flag | Significado |
|---|---|
| `-d` | Corre en segundo plano (detached) |
| `-p 8080:3000` | Tu puerto 8080 → puerto 3000 del contenedor |
| `--name mi-contenedor` | Le pone nombre al contenedor |
| `mi-app` | La imagen que construiste |

Abre [http://localhost:8080](http://localhost:8080). ¡Tu app está corriendo dentro de un contenedor!

## 4.2 Comandos del día a día

```bash
# Ver qué está corriendo
docker ps

# Ver todos (incluidos los detenidos)
docker ps -a

# Ver los logs
docker logs mi-contenedor

# Seguir logs en tiempo real
docker logs -f mi-contenedor

# Detener
docker stop mi-contenedor

# Reiniciar
docker start mi-contenedor

# Eliminar (debe estar detenido)
docker rm mi-contenedor
```

## 4.3 Variables de entorno

Configura sin modificar la imagen:

```bash
docker run -d -p 8081:3000 -e APP_ENV=production mi-app
```

{: .note }
> La misma imagen sirve para dev, test y producción. Nunca hornees secretos dentro de la imagen.

## 4.4 Volúmenes (datos que persisten)

```bash
docker run -d -p 8082:3000 -v mis-datos:/app/data mi-app
```

{: .warning }
> **Los contenedores son efímeros.** Sin un volumen, todo lo que se escribe dentro del contenedor se pierde al eliminarlo.

## Ciclo de vida

```
created → running → stopped → removed
```

| Estado | Significado |
|---|---|
| `created` | Creado, aún no corre |
| `running` | En ejecución |
| `stopped` | Detenido, se puede reiniciar |
| `removed` | Eliminado por completo |

{: .highlight }
> ✅ **Checkpoint:** Sabes construir, ejecutar, inspeccionar y controlar contenedores.

---

[← Parte 3](parte-3-build){: .btn } [Siguiente: Parte 5 · Subir a Amazon ECR →](parte-5-ecr){: .btn .btn-primary }
