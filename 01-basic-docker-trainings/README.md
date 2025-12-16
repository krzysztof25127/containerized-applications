# 01-basic-docker-trainings

## 1. Zarządzanie obrazami i kontenerami w Dockerze

### Pulling an image

`docker images` sprawdza dostępne obrazy  
![Lista dostępnych obrazów Docker](images/1-running-containers/1.png "Lista dostępnych obrazów Docker")

`docker search ubuntu` wyszukuje obrazy Ubuntu w Docker Hub  
![Wyniki wyszukiwania obrazu Ubuntu](images/1-running-containers/2.png "Wyniki wyszukiwania obrazu Ubuntu")

`docker pull ubuntu:22.04` pobiera obraz Ubuntu 22.04  
![Pobieranie obrazu Ubuntu 22.04](images/1-running-containers/3.png "Pobieranie obrazu Ubuntu 22.04")

`docker pull ubuntu:22.10` pobiera obraz Ubuntu 22.10  
![Pobieranie obrazu Ubuntu 22.10](images/1-running-containers/4.png "Pobieranie obrazu Ubuntu 22.10")

`docker images` pokazuje aktualną listę obrazów  
![Lista obrazów po pobraniu](images/1-running-containers/5.png "Lista obrazów po pobraniu")

`docker rmi e322f4808315` usuwa konkretny obraz  
![Usuwanie wybranego obrazu](images/1-running-containers/6.png "Usuwanie wybranego obrazu")

`docker images` ponownie pokazuje listę obrazów  
![Lista obrazów po usunięciu](images/1-running-containers/7.png "Lista obrazów po usunięciu")

`docker rmi $(docker images -a -q)` usuwa wszystkie obrazy  
![Usuwanie wszystkich obrazów](images/1-running-containers/8.png "Usuwanie wszystkich obrazów")

### Running our container

`docker run ubuntu:22.04 /bin/echo 'Hello world!'` uruchamia kontener i wyświetla wiadomość  
![Uruchomienie kontenera z komunikatem Hello world](images/1-running-containers/9.png "Uruchomienie kontenera z komunikatem Hello world")

`docker ps` pokazuje działające kontenery  
![Lista działających kontenerów](images/1-running-containers/10.png "Lista działających kontenerów")

`docker ps -a` pokazuje wszystkie kontenery, w tym zatrzymane  
![Lista wszystkich kontenerów](images/1-running-containers/11.png "Lista wszystkich kontenerów")

`docker run ubuntu:22.04 /bin/bash` uruchamia interaktywny kontener  
![Interaktywny kontener Ubuntu](images/1-running-containers/12.png "Interaktywny kontener Ubuntu")

`docker run -it ubuntu:22.04 /bin/bash` uruchamia kontener w terminalu  
![Kontener w trybie interaktywnym](images/1-running-containers/14.png "Kontener w trybie interaktywnym")

`docker run -d ubuntu:22.04 /bin/bash/sleep 3600` uruchamia kontener w tle  
![Kontener działający w tle](images/1-running-containers/16.png "Kontener działający w tle")

`docker exec -it cd2 /bin/bash` wchodzi do działającego kontenera  
![Dostęp do terminala kontenera](images/1-running-containers/18.png "Dostęp do terminala kontenera")

`ps aux` w kontenerze wyświetla procesy  
![Lista procesów w kontenerze](images/1-running-containers/19.png "Lista procesów w kontenerze")

`exit` kończy sesję terminala kontenera, `docker ps` pokazuje jego stan  
![Stan kontenera po wyjściu](images/1-running-containers/20.png "Stan kontenera po wyjściu")

`docker stop cd29` zatrzymuje kontener  
![Zatrzymanie kontenera](images/1-running-containers/21.png "Zatrzymanie kontenera")

### Removing containers

`docker rm $(docker ps -a -q)` usuwa wszystkie kontenery  
![Usuwanie wszystkich kontenerów](images/1-running-containers/23.png "Usuwanie wszystkich kontenerów")

## 2. Zmiana obrazów

`docker run -it ubuntu:16.04 /bin/bash` i uruchomienie `ping google.com` oraz `apt-get update`  
![Uruchomienie kontenera Ubuntu 16.04 i sprawdzenie połączenia ping](images/2-changing-images/1.png "Uruchomienie kontenera Ubuntu 16.04 i sprawdzenie połączenia ping")

`apt-get install iputils-ping` aby zainstalować narzędzie ping  
![Instalacja narzędzia ping w kontenerze](images/2-changing-images/2.png "Instalacja narzędzia ping w kontenerze")

`ping google.com` - teraz działa poprawnie  
![Ping do Google działa](images/2-changing-images/3.png "Ping do Google działa")

`docker commit -a "Krzysztof G" -m "Added ping utility." c47 delner/ping` tworzy nowy obraz z kontenera  
![Tworzenie nowego obrazu z zainstalowanym pingiem](images/2-changing-images/4.png "Tworzenie nowego obrazu z zainstalowanym pingiem")

`docker images` pokazuje nowy obraz  
![Lista obrazów po utworzeniu nowego obrazu](images/2-changing-images/5.png "Lista obrazów po utworzeniu nowego obrazu")

`docker run -it --rm delner/ping /bin/bash` i `ping google.com` działa w nowym obrazie  
![Uruchomienie nowego obrazu i działający ping](images/2-changing-images/6.png "Uruchomienie nowego obrazu i działający ping")

## 3. Budowanie obrazów

Dockerfile użyty do tworzenia obrazu  
![Zawartość Dockerfile](images/3-building-images/1.png "Zawartość Dockerfile")

`docker build -t "delner/ping"` - budowanie obrazu  
![Budowanie obrazu delner/ping](images/3-building-images/2.png "Budowanie obrazu delner/ping")

`docker images` - sprawdzenie dostępnych obrazów  
![Lista dostępnych obrazów po buildzie](images/3-building-images/3.png "Lista dostępnych obrazów po buildzie")

Dockerfile (kolejny przykład / wersja)  
![Inny przykład Dockerfile](images/3-building-images/4.png "Inny przykład Dockerfile")

Dockerfile (jeszcze jeden przykład)  
![Jeszcze jeden Dockerfile](images/3-building-images/5.png "Jeszcze jeden Dockerfile")

`docker run -it delner/ping` - uruchomienie kontenera z nowym obrazem  
![Uruchomienie kontenera z obrazem delner/ping](images/3-building-images/6.png "Uruchomienie kontenera z obrazem delner/ping")

## 4. Udostępnianie obrazów

`docker push kg25127/ping:1.0` - wypchnięcie obrazu do Docker Hub  
![Wypchnięcie obrazu ping do Docker Hub](images/4-sharing-images/1.png "Wypchnięcie obrazu ping do Docker Hub")

Widoczne zpushowane repozytorium na Docker Hub  
![Widok repozytorium z pushniętym obrazem](images/4-sharing-images/2.png "Widok repozytorium z pushniętym obrazem")

## 5. Wolumeny

`docker run --rm -d --name apache -p 80:80 httpd:2.4` i `curl localhost` - uruchomienie kontenera Apache i sprawdzenie serwera  
![Uruchomienie kontenera Apache i sprawdzenie lokalnego serwera](images/5-volumes/1.png "Uruchomienie kontenera Apache i sprawdzenie lokalnego serwera")

`notepad .\index.html` i `docker cp index.html apache:/usr/local/apache2/htdocs/` oraz `curl localhost` - kopiowanie pliku do kontenera i weryfikacja  
![Kopiowanie index.html do kontenera Apache i test z curl](images/5-volumes/2.png "Kopiowanie index.html do kontenera Apache i test z curl")

`docker stop apache` i ponowne uruchomienie kontenera `docker run --rm -d --name apache -p 80:80 httpd:2.4` oraz `curl localhost` - sprawdzenie zmian  
![Ponowne uruchomienie kontenera Apache i test po restarcie](images/5-volumes/3.png "Ponowne uruchomienie kontenera Apache i test po restarcie")

`docker volume ls`, `docker volume create`, `docker volume rm` - tworzenie i usuwanie wolumenów, m.in. `httpd_htdocs`  
![Tworzenie i zarządzanie wolumenami Docker](images/5-volumes/4.png "Tworzenie i zarządzanie wolumenami Docker")

## 6. Sieci

`docker network ls` - lista dostępnych sieci Docker  
![Lista sieci Docker](images/6-networking/1.png "Lista sieci Docker")

`docker network inspect bridge` - szczegóły sieci bridge  
![Szczegóły domyślnej sieci bridge](images/6-networking/2.png "Szczegóły domyślnej sieci bridge")

`docker run --rm -d --name dummy kg25127/ping:1.0` - uruchomienie kontenera dummy  
![Uruchomienie kontenera dummy](images/6-networking/3.png "Uruchomienie kontenera dummy")

`docker run --rm -d -e PING_TARGET=172.17.0.2 --name pinger kg25127/ping:1.0`, `docker ps`, `docker logs pinger` - test połączenia z konkretnym adresem IP  
![Test połączenia kontenera pinger do innego kontenera po IP](images/6-networking/5.png "Test połączenia kontenera pinger do innego kontenera po IP")

`docker run --rm -d -e PING_TARGET=dummy --name pinger kg25127/ping:1.0`, `docker ps` - test połączenia do kontenera po nazwie  
![Test połączenia kontenera pinger do kontenera dummy po nazwie](images/6-networking/6.png "Test połączenia kontenera pinger do kontenera dummy po nazwie")

`docker network create skynet` i `docker network ls` - tworzenie nowej sieci i sprawdzenie listy  
![Tworzenie sieci skynet i lista sieci](images/6-networking/7.png "Tworzenie sieci skynet i lista sieci")

`docker network inspect skynet` - sprawdzenie szczegółów nowo utworzonej sieci  
![Szczegóły sieci skynet](images/6-networking/8.png "Szczegóły sieci skynet")

`docker network rm skynet` i `docker network ls` - usunięcie sieci skynet  
![Usunięcie sieci skynet i lista sieci](images/6-networking/9.png "Usunięcie sieci skynet i lista sieci")

`docker network create skynet` i `docker run --rm -d --network skynet --name dummy kg25127/ping:1.0` - uruchomienie kontenera w nowej sieci  
![Uruchomienie kontenera dummy w sieci skynet](images/6-networking/10.png "Uruchomienie kontenera dummy w sieci skynet")

`docker run --rm -d --network skynet -e PING_TARGET=dummy --name pinger kg25127/ping:1.0`, `docker logs pinger` - test połączenia w nowej sieci  
![Test połączenia kontenera pinger do dummy w sieci skynet](images/6-networking/11.png "Test połączenia kontenera pinger do dummy w sieci skynet")


