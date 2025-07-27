# Immagine di base
FROM python:3.8-buster

# Maintainer
LABEL maintainer="axelred-rgb 'Axel Nyagom Nkouokam'"

# Fix per i repository Debian Buster archiviati
RUN sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
    sed -i 's|security.debian.org/debian-security|archive.debian.org/debian-security|g' /etc/apt/sources.list && \
    sed -i '/buster-updates/d' /etc/apt/sources.list

# Installiamo le dipendenze di sistema
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libldap2-dev \
    libsasl2-dev \
    && rm -rf /var/lib/apt/lists/*

# Directory di lavoro
WORKDIR /app

# Copia i file necessari
COPY requirements.txt .
COPY student_age.py .

# Creiamo la cartella /data e copiamo il file JSON lì
RUN mkdir -p /data
COPY student_age.json /data/student_age.json

# Installa le dipendenze Python
RUN pip install --no-cache-dir -r requirements.txt

# Espone la porta
EXPOSE 5000

# Comando di avvio
CMD [ "python3", "./student_age.py" ]
