# Unity-WebSocket with Node.js

## Overview
**Unity-WebSocket** permite comunicación bidireccional en tiempo real entre una aplicación desarrollada en Unity y un servidor externo implementado con Node.js, utilizando WebSockets como protocolo principal.

## Propósito
Establecer una comunicación en tiempo real entre Unity y un backend externo, permitiendo enviar y recibir datos de manera eficiente usando WebSockets.

## Componentes Principales
- `server.js`: Servidor WebSocket basado en Node.js.
- `WebSocketManager.cs`: Script en Unity que gestiona conexión, envío y recepción de mensajes.
- `WebSocketClient.cs`: Componente auxiliar para encapsular la lógica de comunicación.
- **UI**: InputFields y botones en Unity que permiten enviar mensajes y conectarse al servidor.

## Arquitectura
- Unity como cliente WebSocket.
- Servidor WebSocket Node.js escuchando en un puerto determinado.
- Comunicación directa cliente-servidor usando el protocolo WebSocket.
- Para despliegue en navegador se utiliza WebGL + GitHub Pages (solo como hosting del cliente).

![image](https://github.com/user-attachments/assets/1bbd2800-867d-4027-a792-84b097a28996)

## Comandos Disponibles (en servidor)
- `connection`: Se activa cuando un cliente se conecta.
- `message`: Recibe y procesa mensajes entrantes.
- `close`: Se activa al cerrar la conexión.

## Parámetros Configurables
| Parámetro       | Tipo     | Descripción                                 |
|-----------------|----------|---------------------------------------------|
| `serverUrl`     | `string` | Dirección del servidor WebSocket (ej. ws://localhost:8080) |
| `InputField`    | UI       | Entrada de texto para mensajes              |
| `Button`        | UI       | Botones para conectar/enviar                |

## Proceso de Configuración
1. Instalar Node.js y el paquete `ws`:  
```bash
   npm install ws
```
## Crear `server.js`:

```js
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', ws => {
  console.log('Cliente conectado');
  ws.on('message', message => {
    console.log('Mensaje recibido:', message);
    ws.send(`Echo: ${message}`);
  });
});
```
## En Unity:
- Crear WebSocketManager.cs y WebSocketClient.cs.
- Usar Application.ExternalCall o SendMessage si se interactúa con JS.
- Vincular los scripts a UI (botones e inputs).

## Subida a WebGL y configuración de base de datos en la nube

- Después de exportar el proyecto Unity como WebGL, se suben los archivos a un hosting web.
- En este caso, se utilizó **awardspace.com** para alojar una base de datos en la nube.
- Desde Awardspace se pueden gestionar archivos PHP que se conectan correctamente a la base de datos.
- Esto permite que el frontend WebGL haga llamadas a los scripts PHP para interactuar con la base de datos remota.

## Desplegar en GitHub Pages (si se usa WebGL como frontend):
Exportar desde Unity como WebGL.

Subir la carpeta /Build a GitHub Pages.

## Características
- Comunicación en tiempo real con Node.js mediante WebSocket.
- Fácil integración con UI de Unity.
- Estructura modular y extensible.
- Compatible con despliegue web usando GitHub Pages (solo como hosting).
