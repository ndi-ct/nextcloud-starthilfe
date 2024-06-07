# Nextcloud-Starthilfe

![nextcloud](https://github.com/ndi-ct/nextcloud-starthilfe/assets/78471292/d4d48ac4-ee8e-434b-923c-0f2ff8991c51)

Dies ist ein GitHub-Repository zum Artikel "Nextcloud wetterfest machen", erschienen bei heise+ und im c't Magazin 14/2024. Es enthält eine vereinfachte docker-compose.yaml-Datei, die von der offiziellen compose.yaml-Datei des Nextcloud-AIO-Projekts abgeleitet ist sowie ein Caddyfile, eine Konfigurationsdatei für den Reverse-Proxy Caddy.

Diese Konfiguration ist dafür gedacht, Nextcloud AIO auf einem angemieteten Server mit öffentlichter IPv4-Adresse zu betreiben. c't hat das Setup auf einem Server mit Ubuntu Server 24.04 LTS getestet, aber es sollte auf jeder Linux-Distribution mit Docker funktionieren. Wer Nextcloud im Heimnetz betreiben möchte (und öffentlich erreichbar machen will) sei die Dokumentation des Nextcloud-AIO-Projekts empfohlen.

# Loslegen

Voraussetzung: Sie brauchen eine eigene Domain und müssen einen A-Record setzen, der auf die IP-Adresse Ihres Servers zeigt.

Wenn Sie mittels SSH auf dem Server eingeloggt sind, sollten Sie zunächst das System auf den neuesten Stand bringen:

```
sudo apt update && apt upgrade
```

Danach installieren Sie Docker, am besten aus den offiziellen Docker-Paketquellen:

```
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Klonen Sie anschließend dieses Repository und wechseln in das neue Verzeichnis:

```
git clone https://github.com/ndi-ct/nextcloud-starthilfe
cd nextcloud-starthilfe
```

Bearbeiten Sie mit einem Texteditor (z.B. `nano Caddyfile`) die Datei Caddyfile und ersetzen nextcloud.example.com durch Ihre eigene Domain.

Jetzt ist alles bereit, um den nextcloud-aio-mastercontainer zu starten:

```
sudo docker compose up -d
```

Das kann eine Weile dauern. Sie können mit dem Befehl `docker ps` schauen, ob der Container bereit ist. Sobald er den Status `healthy` anzeigt, sollten Sie im Browser über https://<IP-Adresse des Servers>:8080 die Weboberfläche des AIO-Containers aufrufen können. 

Sie können jetzt im Artikel fortfahren.




