# 🐳 QR Code Generator - Docker

Generador de códigos QR containerizado con Docker, listo para producción.

## 🚀 Inicio Rápido

### Opción 1: Docker Compose (Recomendado)

```bash
# Clonar o crear la estructura del proyecto
mkdir qr-generator-app
cd qr-generator-app

# Copiar todos los archivos proporcionados
# (Dockerfile, docker-compose.yml, package.json, etc.)

# Construir y ejecutar
docker-compose up --build -d
```

### Opción 2: Docker Manual

```bash
# Construir la imagen
docker build -t qr-generator .

# Ejecutar el contenedor
docker run -d -p 3000:80 --name qr-app qr-generator
```

## 📁 Estructura del Proyecto

```
qr-generator-app/
├── Dockerfile                 # Configuración del contenedor
├── docker-compose.yml         # Orquestación con Docker Compose
├── package.json              # Dependencias del proyecto
├── vite.config.js            # Configuración de Vite
├── nginx.conf                # Configuración del servidor web
├── .dockerignore             # Archivos ignorados por Docker
├── index.html                # HTML principal
├── src/
│   ├── main.jsx              # Punto de entrada de React
│   ├── index.css             # Estilos base con Tailwind
│   └── QRCodeGenerator.jsx   # Componente principal
└── README.md                 # Esta documentación
```

## 🔧 Configuración

### Variables de Entorno

Puedes personalizar la aplicación con estas variables:

```bash
# En docker-compose.yml o al ejecutar docker run
NODE_ENV=production
PORT=80
```

### Puerto

Por defecto, la aplicación estará disponible en:
- **Local**: http://localhost:3000
- **Docker**: http://localhost:3000 (mapeado al puerto 80 del contenedor)

## 📦 Características del Contenedor

- **Multi-stage build**: Optimización del tamaño de imagen
- **Nginx**: Servidor web de producción
- **Compresión gzip**: Para mejor rendimiento
- **Headers de seguridad**: Configuración segura por defecto
- **Cache de assets**: Optimización de recursos estáticos
- **SPA support**: Configurado para Single Page Applications

## 🛠️ Comandos Útiles

### Desarrollo

```bash
# Ver logs del contenedor
docker-compose logs -f qr-generator

# Acceder al contenedor
docker-compose exec qr-generator sh

# Reiniciar el servicio
docker-compose restart qr-generator
```

### Producción

```bash
# Parar todos los servicios
docker-compose down

# Actualizar y reconstruir
docker-compose up --build -d

# Limpiar imágenes no utilizadas
docker image prune -f
```

### Monitoreo

```bash
# Ver estado de contenedores
docker-compose ps

# Ver uso de recursos
docker stats qr-code-generator

# Ver información de la imagen
docker image inspect qr-generator
```

## 🌐 Acceso a la Aplicación

Una vez que el contenedor esté ejecutándose:

1. **Navegador**: Abre http://localhost:3000
2. **Genera códigos QR**: Para URLs, texto o información de contacto
3. **Descarga**: Los códigos QR en formato PNG
4. **Copia**: Los datos del código QR al portapapeles

## 🔒 Seguridad

El contenedor incluye configuraciones de seguridad:

- Headers de seguridad HTTP
- Configuración CSP (Content Security Policy)
- Usuario no-root en el contenedor
- Imagen base Alpine (minimalista y segura)

## 🐛 Solución de Problemas

### Puerto ya en uso
```bash
# Cambiar el puerto en docker-compose.yml
ports:
  - "8080:80"  # Usar puerto 8080 en lugar de 3000
```

### Problemas de construcción
```bash
# Limpiar cache de Docker
docker builder prune -f

# Reconstruir sin cache
docker-compose build --no-cache
```

### Logs de errores
```bash
# Ver logs detallados
docker-compose logs --tail=50 qr-generator
```

## 🚀 Despliegue en Producción

### Con reverse proxy (Nginx/Traefik)

El `docker-compose.yml` incluye labels para Traefik. Para otros proxies:

```nginx
# Configuración de Nginx como reverse proxy
server {
    listen 80;
    server_name tu-dominio.com;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Escalabilidad

```bash
# Ejecutar múltiples instancias
docker-compose up --scale qr-generator=3 -d
```

## 📊 Métricas y Rendimiento

La aplicación está optimizada para:

- **Tiempo de carga**: < 2 segundos
- **Tamaño de imagen**: ~ 50MB (con multi-stage build)
- **Memoria RAM**: ~ 20MB por contenedor
- **CPU**: Mínimo requerimiento

## 🤝 Contribuir

1. Fork del proyecto
2. Crear rama de feature (`git checkout -b feature/nueva-caracteristica`)
3. Commit de cambios (`git commit -am 'Agregar nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Crear Pull Request

## 📄 Licencia

Este proyecto está bajo la licencia MIT - ver el archivo LICENSE para más detalles.

---

¿Problemas? ¿Sugerencias? ¡Abre un issue o contribuye al proyecto! 🎉