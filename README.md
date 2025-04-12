# TP K8S – Sitio estático en Minikube  
Computación en la Nube · 2025 · Lautaro Gelman

---

## ¿Qué es esto?

Proyecto para levantar mi página estática (fork de `static-website`) dentro de un clúster **Minikube**.  
El sitio va empaquetado en una imagen personalizada de **Nginx**, así evito problemas de rutas en Windows.

---

## Requisitos

* Docker Desktop (WSL 2)
* Minikube + kubectl
* Git

---

## Pasos rápidos

```bash
# 1. Clonar repos
git clone https://github.com/LautaroGelman/static-website.git web-content
git clone https://github.com/LautaroGelman/TrabajoPracticoK8S.git
cd TrabajoPracticoK8S

# 2. Construir la imagen con el sitio
cd docker-nginx
docker build -t nginx-con-mi-web .
minikube image load nginx-con-mi-web
cd ..

# 3. Levantar Minikube y aplicar manifiestos
minikube start
kubectl apply -f deployment/deployment-nginx.yaml
kubectl apply -f service/service-nginx.yaml

# 4. Probar en el navegador
minikube service nginx-service        # abre la URL
# o:
minikube service nginx-service --url  # muestra la URL


TrabajoPracticoK8S/
├── docker-nginx/
│   ├── Dockerfile
│   └── web-content/
├── deployment/
│   └── deployment-nginx.yaml
├── service/
│   └── service-nginx.yaml
├── pvc/              # ejemplo hostPath (opcional)
│   ├── pv-web.yaml
│   └── pvc-web.yaml
└── README.md
