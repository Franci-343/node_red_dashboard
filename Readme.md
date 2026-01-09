# Dashboard del Clima - Node-RED

Sistema completo de dashboard del clima con autenticación, tema oscuro/claro, y actualización en tiempo real usando Node-RED, Bootstrap 5 y WebSocket.

**Credenciales de acceso:**
- Email: `admin@weather.com`
- Password: `admin123`

## Estructura del Proyecto

```
node_red_dashboard/
├── flows/
│   └── weather-dashboard-flow.json  # Flow de Node-RED para clima
├── view/
│   ├── login.html                   # Login con animaciones de cubos
│   ├── create_account.html          # Registro de usuarios
│   ├── forgot_password.html         # Recuperación de contraseña
│   └── weather.html                 # Dashboard alternativo sin login
├── index.html                        # Dashboard principal (requiere login)
├── controller/                       # Carpeta para controladores (vacía)
├── model/                           # Carpeta para modelos (vacía)
└── database/                        # Carpeta para base de datos (vacía)
```
 Rápida

### 1. Obtener API Key de OpenWeatherMap

1. Regístrate en [OpenWeatherMap](https://openweathermap.org/api)
2. Obtén tu API Key gratuita (Free Tier)
3. Copia tu API key para usarla en el siguiente paso

### 2. Configurar e Importar el Flow en Node-RED

1. **Edita el archivo del flow:**
   - Abre `flows/weather-dashboard-flow.json`
   - Busca `TU_API_KEY` 
   - Reemplázalo con tu API key real de OpenWeatherMap
   - Guarda el archivo

2. **Inicia Node-RED:**
   ```powershell
   node-red
   ```

3. **Importa el flow:**
   - Abre Node-RED en tu navegador: `http://localhost:1880`
   - Ve a Menú (☰) → Import → Clipboard
   - Copia y pega el contenido completo de `flows/weather-dashboard-flow.json`
   - Haz clic en "Import"
   - **Haz clic en "Deploy"** (botón rojo superior derecho)

4. **Verifica que funcione:**
   - Abre la pestaña Debug en Node-RED (sidebar derecha)
   - Deberías ver datos del clima cada 10 segundos
8. Haz clic en "Deploy"

**Opción 1: Con autenticación (recomendado)**
1. Abre directamente `index.html` en tu navegador
2. Serás redirigido automáticamente a `view/login.html`
3. Ingresa las credenciales:
   - Email: `admin@weather.com`
   - Password: `admin123`
4. Serás redirigido al dashboard principal

**Opción 2: Sin autenticación (alternativa)**
Abre `view/weather.html` directamente en tu navegador

**Nota:** Si tienes problemas de CORS, usa un servidor local:

```powershell
# Opción A: Servidor HTTP con Python
python -m http.server 8000
# Luego abre: http://localhost:8000/index.html

# OpSistema de Autenticación
- ✅ Login con validación de credenciales
- ✅ Página de registro (UI completa)
- ✅ Recuperación de contraseña (UI completa)
- ✅ Protección de sesión con localStorage
- ✅ Cierre de sesión seguro

### Diseño y UI
- ✅ **Tema claro/oscuro** con persistencia
- ✅ **Animaciones de fondo** con cubos 3D animados
- ✅ Diseño responsive con Bootstrap 5.3.0
- ✅ Paleta de colores consistente en todas las páginas
- ✅ Iconos de Bootstrap Icons 1.11.1
- ✅ Efectos glassmorphism en tarjetas

### Flow de Node-RED
- ✅ **Actualización automática cada 10 segundos**
- ✅ Consulta a OpenWeatherMap API
- ✅ Formateo de datos (temperatura, viento, humedad, etc.)
- ✅ Publicación por WebSocket en `/ws/weather`
- ✅ Debug para monitorear datos en tiempo real
- ✅ Ciudad configurada: **La Paz, Bolivia**

### Dashboard del Clima
- ✅ Conexión WebSocket en tiempo real
- ✅ Reconexión automática si se pierde la conexión
- ✅ Indicador de estado de conexión
-dita `flows/weather-dashboard-flow.json` y busca el nodo "OpenWeatherMap API", luego cambia el parámetro `q=`:

**Ciudades de Bolivia:**
```
q=La Paz,BO          # Por defecto
q=Cochabamba,BO
q=Santa Cruz,BO
q=Sucre,BO
q=Oruro,BO
```

**Otras ciudades:**
```
q=Buenos Aires,AR
q=Lima,PE
q=Santiago,CL
q=Madrid,ES
```

Formato completo del URL:
```
https://api.openweathermap.org/data/2.5/weather?q=CIUDAD,CODIGO_PAIS&appid=TU_API_KEY&units=metric&lang=es
```

### Cambiar intervalo de actualización

En `flows/weather-dashboard-flow.json`, busca el nodo "Actualizar cada 10min" y cambia el valor `"repeat"`:

```json
"repeat": "10",    // 10 segundos (actual)
"repeat": "60",    // 1 minuto
1. Verifica que Node-RED esté ejecutándose: `http://localhost:1880`
2. Verifica que el flow esté desplegado (botón "Deploy" en rojo)
3. Abre la consola del navegador (F12) y busca mensajes de error
4. Revisa que el estado muestre "🟢 Conectado"

### No se obtienen datos del clima (muestra "Desconocida")
1. Verifica tu API Key de OpenWeatherMap en el archivo JSON
2. Revisa el Debug en Node-RED (sidebar derecha) para ver errores
3. Verifica tu conexión a Internet
4. Prueba la API directamente en el navegador:
   ```
   https://api.openweathermap.org/data/2.5/weather?q=La Paz,BO&appid=TU_API_KEY&units=metric&lang=es
   ```

### API Key inválida
- Espera 5-10 minutos después de registrarte (activación de la key)
- Verifica que copiaste la key completa sin espacios
- Revisa que reemplazaste `TU_API_KEY` en el JSON

### La página queda en "Cargando..."
1. Abre la consola del navegador (F12)
2. Revisa los logs con emojis (🚀, 📡, ✅, ❌)
3. Verifica que Node-RED esté enviando datos cada 10 segundos
4. Fuerza una actualización en Node-RED haciendo clic en el nodo inject

### El tema no persiste
- Verifica que tu navegador permita localStorage
- Prueba en modo normal (no incógnito)

## Tecnologías Utilizadas

- **Node-RED** - Flujo de datos y WebSocket
- **Bootstrap 5.3.0** - Framework CSS
- **Bootstrap Icons 1.11.1** - Iconografía
- **OpenWeatherMap API** - Datos meteorológicos
- **HTML5 Canvas** - Animaciones de fondo
- **WebSocket** - Comunicación en tiempo real
- **localStorage** - Persistencia de sesión y tema

## Roadmap / Mejoras Futuras

- [ ] Autenticación con base de datos real
- [ ] Pronóstico extendido de 5-7 días
- [ ] Gráficas históricas de temperatura
- [ ] Múltiples ciudades simultáneas
- [ ] Alertas meteorológicas
- [ ] PWA (Progressive Web App)
- [ ] Notificaciones push
- [ ] Exportar datos a CSV/JSON

## Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Haz fork del proyecto
2. Crea una rama para tu feature (`git checkout -b feature/NuevaCaracteristica`)
3. Commit tus cambios (`git commit -m 'Añade nueva característica'`)
4. Push a la rama (`git push origin feature/NuevaCaracteristica`)
5. Abre un Pull Request

## Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.

## Autor

Desarrollado con ❤️ para aprender Node-RED y WebSocket

---

⭐ Si este proyecto te fue útil, considera darle una estrella en GitHub

Cambia los valores a tus credenciales preferidas.

### Modificar colores del tema

Los colores están definidos en los archivos CSS de cada página:

**Tema claro:**
- Fondo: `#f8f9fa`
- Cards: `#ffffff`
- Acentos: `#2d78ff`

**Tema oscuro:**
- Fondo: `#0f1724`
- Cards: `#0b1220`
- Acentos: `#78c8ff Personalización

### Cambiar la ciudad

En el flow, edita el nodo "OpenWeatherMap API" y cambia el parámetro `q=`:

```
https://api.openweathermap.org/data/2.5/weather?q=Barcelona&appid=TU_API_KEY&units=metric&lang=es
```

### Cambiar intervalo de actualización

En el flow, edita el nodo "Actualizar cada 10min" y cambia el campo `repeat` (en segundos):
- 300 = 5 minutos
- 600 = 10 minutos (por defecto)
- 1800 = 30 minutos

### Modificar el puerto de WebSocket

Si Node-RED está en otro puerto, edita `view/weather.html` línea con `WS_URL`:

```javascript
const WS_URL = 'ws://tu-servidor:1880/ws/weather';
```

## Solución de Problemas

### No se conecta el WebSocket
- Verifica que Node-RED esté ejecutándose
- Verifica que el flow esté desplegado (botón "Deploy")
- Revisa la consola del navegador (F12)

### No se obtienen datos del clima
- Verifica tu API Key de OpenWeatherMap
- Revisa el Debug en Node-RED (sidebar derecha)
- Verifica tu conexión a Internet

### API Key inválida
- Espera unos minutos después de registrarte (activación de la key)
- Verifica que copiaste la key completa


