---
title: "Parte 1 · Crear la app"
nav_order: 3
---

# Parte 1 · Crear la aplicación

Vamos a crear una app web mínima con Node.js. Lo más simple posible para enfocarnos en el flujo de contenedores, no en la app.

## 1.1 Crear el proyecto

```bash
mkdir mi-app && cd mi-app
npm init -y
```

## 1.2 Crear el servidor

Crea un archivo `server.js`:

```javascript
// server.js
const http = require('http');

const PORT = 3000;

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({
    message: '¡Hola desde un contenedor Docker! 🐳',
    hostname: require('os').hostname(),
    timestamp: new Date().toISOString(),
  }));
});

server.listen(PORT, () => {
  console.log(`Servidor corriendo en http://localhost:${PORT}`);
});
```

## 1.3 Verificar que funciona

```bash
node server.js
```

Abre [http://localhost:3000](http://localhost:3000) en tu navegador. Deberías ver el JSON con el mensaje.

Detén el servidor con `Ctrl + C`.

{: .highlight }
> ✅ **Checkpoint:** Tienes una app que funciona en tu máquina.

---

[← Requisitos](requisitos){: .btn } [Siguiente: Parte 2 · Dockerfile →](parte-2-dockerfile){: .btn .btn-primary }
