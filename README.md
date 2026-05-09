# Control Frigorífico Pro

Sistema de monitoreo en tiempo real para cámaras frigoríficas, desarrollado como una Single-Page Application (SPA) con HTML, CSS y JavaScript vanilla.

## Características

- 📡 **Monitoreo en tiempo real** vía Firebase Realtime Database
- 🌡️ **Visualización de temperatura** de cámara y ambiente
- 💧 **Seguimiento de humedad**
- ⚡ **Estado del compresor y descongelado** con indicadores visuales
- 📊 **Gráficos interactivos** con zoom y medición de intervalos (plan Premium)
- 📋 **Tabla de historial** con selección de puntos en el gráfico
- ⚙️ **Panel de configuración** por equipo (setpoint, diferencial, parámetros de descongelado)
- 🔒 **Modelo Freemium**: últimos 50 registros gratis; historial completo con plan Premium

## Estructura del proyecto

```
camara/
└── index.html   # Aplicación completa (HTML + CSS + JS en un solo archivo)
```

## Tecnologías utilizadas

| Tecnología | Versión | Uso |
|---|---|---|
| Firebase JS SDK | 8.10.1 | Base de datos en tiempo real |
| Google Charts | latest | Gráficos de temperatura |
| Bootstrap | 5.3.0 | Estilos y componentes UI |

## Configuración

Antes de usar la aplicación, reemplazá la URL de la base de datos en `index.html`:

```javascript
const firebaseConfig = {
  databaseURL: "https://TU-PROYECTO-default-rtdb.firebaseio.com",
};
```

## Estructura esperada en Firebase

```
/
├── logs/
│   └── {idEquipo}/
│       └── {registro}/
│           ├── timestamp    (número, epoch ms)
│           ├── t_camara     (número, °C)
│           ├── t_ambiente   (número, °C)
│           ├── humedad      (número, %)
│           ├── puerta       ("ABIERTA" | "CERRADA")
│           ├── mensaje      (string, opcional)
│           ├── compresor    (0 | 1)
│           └── defrost      (0 | 1)
└── configuracion/
    └── {idEquipo}/
        ├── plan             ("basico" | "premium")
        └── parametros/
            ├── setpoint          (número, °C)
            ├── diferencial       (número, °C)
            ├── defrost_habilitado (boolean)
            ├── tipo_defrost      ("resistencia" | "gas")
            ├── int_defrost       (número, horas)
            └── dur_defrost       (número, minutos)
```

## Uso

1. Abrí `index.html` directamente en el navegador o publicalo en GitHub Pages / cualquier hosting estático.
2. La aplicación se conecta a Firebase y carga automáticamente los equipos registrados bajo `/logs`.
3. Cada equipo muestra su panel con temperatura en tiempo real, gráfico histórico y tabla de registros.
4. Usá los botones de rango (1h, 12hs, 24hs, 7d, Todo) o los campos de fecha para filtrar el historial.
5. Activá "📏 Medir" en el gráfico para medir intervalos de tiempo arrastrando el mouse.

## Planes

- **Básico (gratis):** muestra los últimos 50 registros en tiempo real; el gráfico e historial completo están bloqueados.
- **Premium:** acceso completo al historial, gráficos con zoom y exportación.

Para activar Premium, hacer clic en el botón "🚀 ACTIVAR PREMIUM" dentro de la aplicación.
