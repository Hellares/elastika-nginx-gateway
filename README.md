# Elastika Nginx Gateway

🚀 API Gateway centralizado para los microservicios de Elastika.

## Features

- **Proxy reverso** para múltiples microservicios
- **Rate limiting** automático  
- **Headers de seguridad** 
- **Archivos estáticos** súper rápidos
- **Health checks** para todos los servicios
- **SSL ready**

## Arquitectura

```
Internet (Port 80) → Nginx Gateway → Microservicios
├── /files/* → Images Service ✅
├── /api/auth/* → Auth Service (ready)
├── /api/files/* → Files Service (ready)
└── /api/users/* → Users Service (ready)
```

## Deploy

```bash
git clone git@github.com:Hellares/elastika-nginx-gateway.git
cd elastika-nginx-gateway
docker-compose up -d
```

## Health Checks

```bash
curl http://your-server/health
curl http://your-server/health/images
curl http://your-server/files-list
```

## Configuración

- **Puerto**: 80 (HTTP), 443 (HTTPS ready)
- **Red Docker**: elastika-network
- **Logs**: ./logs/
- **SSL**: ./ssl/

## Servicios configurados

- ✅ **Images Service**: Upload, download, quota
- 🔄 **Auth Service**: Ready para configurar
- 🔄 **Files Service**: Ready para configurar
- 🔄 **Users Service**: Ready para configurar

## URLs de ejemplo

```bash
# Health checks
curl http://your-server/health
curl http://your-server/health/images

# Images service
curl http://your-server/files-list
curl http://your-server/files/tenant/image.jpg

# Upload (requiere auth)
curl -X POST -H "Authorization: Bearer your-token" \
  -F "file=@image.jpg" \
  "http://your-server/upload?path=tenant"
```

## Estructura del proyecto

```
elastika-nginx-gateway/
├── docker-compose.yml     # Configuración del contenedor
├── nginx/
│   ├── nginx.conf        # Configuración principal
│   └── conf.d/
│       └── services.conf # Configuración de servicios
├── logs/                 # Logs de Nginx
├── ssl/                  # Certificados SSL
└── README.md            # Esta documentación
```
