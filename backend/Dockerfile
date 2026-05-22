# 1. Usamos una versión más moderna de Python (menos vulnerabilidades heredadas)
FROM python:3.12-slim

# 2. Le decimos a Python que no genere archivos basura y nos muestre los errores
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# 3. [NUEVO] Parche de seguridad: Actualizamos el sistema Linux interno
RUN apt-get update && apt-get upgrade -y && rm -rf /var/lib/apt/lists/*

# 4. Creamos una carpeta llamada /app adentro del contenedor
WORKDIR /app

# 5. Copiamos nuestra lista de compras adentro del contenedor
COPY requirements.txt /app/

# 6. Instalamos Django y el conector de la base de datos
RUN pip install --no-cache-dir -r requirements.txt

# 7. Copiamos todo nuestro código adentro del contenedor
COPY . /app/