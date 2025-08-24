# Usar nginx para servir archivos estáticos
FROM nginx:alpine

# Copiar el archivo HTML al directorio de nginx
COPY src/index.html /usr/share/nginx/html/

# Copiar configuración personalizada de nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exponer el puerto 80
EXPOSE 80

# Comando para ejecutar nginx
CMD ["nginx", "-g", "daemon off;"]