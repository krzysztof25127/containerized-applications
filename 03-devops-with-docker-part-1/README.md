# 03-devops-with-docker-part-1

## Section 1.

`docker container run hello-world` - uruchomienie prostego kontenera testowego, sprawdzenie instalacji Dockera  
![Uruchomienie kontenera hello-world](images/section1/1.png "Uruchomienie kontenera hello-world")

`docker container run -it ubuntu sh -c "apt update && apt install -y curl && curl https://www.google.com"` - uruchomienie Ubuntu, instalacja curl i sprawdzenie połączenia z Google  
![Uruchomienie kontenera Ubuntu i instalacja curl](images/section1/2.png "Uruchomienie kontenera Ubuntu i instalacja curl")

Wynik poprzedniego polecenia  
![Wyjście polecenia curl w kontenerze Ubuntu](images/section1/3.png "Wyjście polecenia curl w kontenerze Ubuntu")


## Section 2.

`docker run ubuntu` – uruchomienie kontenera Ubuntu w domyślnym trybie  
`docker run -t ubuntu` – uruchomienie z pseudo-terminalem  
`docker run -it ubuntu` – uruchomienie interaktywne z terminalem  
`docker run -d -it --name looper ubuntu sh -c "while true; do date; sleep 1; done"` – kontener w tle z pętlą wyświetlającą datę  
`docker logs -f looper` – podgląd logów kontenera looper  
![Uruchomienie kontenera Ubuntu w różnych trybach i podgląd logów](images/section2/1.png "Uruchomienie kontenera Ubuntu w różnych trybach i podgląd logów")

`docker attach looper` – podłączenie do działającego kontenera w drugim terminalu  
![Podłączenie do działającego kontenera looper](images/section2/2.png "Podłączenie do działającego kontenera looper")

`docker attach --no-stdin looper` – podłączenie do kontenera bez stdin  
![Podłączenie do kontenera looper bez stdin](images/section2/3.png "Podłączenie do kontenera looper bez stdin")

`docker exec looper ls -la` – wyświetlenie zawartości kontenera  
![Wyświetlenie zawartości kontenera looper](images/section2/4.png "Wyświetlenie zawartości kontenera looper")

`docker exec -it looper bash` – uruchomienie bash w kontenerze  
`docker kill looper` – zatrzymanie kontenera  
![Uruchomienie bash w kontenerze looper i zatrzymanie kontenera](images/section2/5.png "Uruchomienie bash w kontenerze looper i zatrzymanie kontenera")

`docker run -d --rm -i --name looper-it ubuntu sh -c "while true; do date; sleep 1; done"` – uruchomienie kontenera w tle z auto-usuwaniem  
`docker attach looper-it` – podłączenie do kontenera  
![Uruchomienie kontenera looper-it i podłączenie do niego](images/section2/6.png "Uruchomienie kontenera looper-it i podłączenie do niego")

## Exercise 1.3

`docker exec -it secret bash` – podłączenie do kontenera  
`tail -f ./text.log` – wyświetlenie sekretnej wiadomości  
![Wyświetlenie sekretnej wiadomości w kontenerze secret](images/section2/exercise_1.3.png "Wyświetlenie sekretnej wiadomości w kontenerze secret")

## Exercise 1.4

`sh -c 'while true; do echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website; done'` – skrypt do pobierania strony przez curl  
![Interaktywny skrypt do pobierania strony przez curl w kontenerze](images/section2/exercise_1.4.png "Interaktywny skrypt do pobierania strony przez curl w kontenerze")


## Section 3.

`docker search hello-world` – wyszukiwanie obrazu hello-world  
![Wyszukiwanie hello-world](images/section3/1.png "Wyszukiwanie hello-world")

`docker build . -t hello-docker` – budowanie obrazu hello-docker  
`docker run hello-docker` – uruchomienie obrazu  
![Budowanie i uruchomienie hello-docker](images/section3/3.png "Budowanie i uruchomienie hello-docker")

`docker ps` – lista działających kontenerów  
`docker cp ./additiona.txt adoring_kapitsa:/usr/src/app/` – kopiowanie pliku do kontenera  
`docker diff adoring_kapitsa` – sprawdzenie zmian w kontenerze  
![Kopiowanie pliku i sprawdzenie zmian](images/section3/4.png "Kopiowanie pliku i sprawdzenie zmian")

`docker run -it hello-docker sh` – uruchomienie shella w kontenerze  
![Interaktywny shell w kontenerze](images/section3/5.png "Interaktywny shell w kontenerze")

`docker commit adoring_kapitsa hello-docker-additional` – zapisanie zmian jako nowy obraz  
![Tworzenie nowego obrazu](images/section3/6.png "Tworzenie nowego obrazu")

`docker run hello-docker-additional ls` – sprawdzenie zawartości nowego obrazu  
![Lista plików w nowym obrazie](images/section3/7.png "Lista plików w nowym obrazie")

## Exercise 1.5

`docker image ls` – lista obrazów  
![Lista obrazów](images/section3/exercise_1.51.png "Lista obrazów")

`docker run -it --name ubuntu_test devopsdockeruh/simple-web-service:ubuntu` – uruchomienie Ubuntu testowego kontenera  
`docker exec -it ubuntu_test sh` – podłączenie do kontenera  
![Testowy kontener Ubuntu](images/section3/exercise_1.52.png "Testowy kontener Ubuntu")

`docker run -it --name alpine_test devopsdockeruh/simple-web-service:alpine` – uruchomienie Alpine testowego kontenera  
`docker exec -it alpine_test sh` `tail -f ./text.log` – podgląd logów  
![Testowy kontener Alpine i podgląd logów](images/section3/exercise_1.53.png "Testowy kontener Alpine i podgląd logów")

## Exercise 1.6

`docker run -it devopsdockeruh/pull_exercise` – uruchomienie ćwiczenia pull  
![Ćwiczenie pull](images/section3/exercise_1.6.png "Ćwiczenie pull")

## Exercise 1.7

Dockerfile użyty do ćwiczenia  
![Dockerfile ćwiczenia curler](images/section3/exercise_1.71.png "Dockerfile ćwiczenia curler")

`docker run -it curler` – uruchomienie skryptu i podanie strony  
![Uruchomienie curler](images/section3/exercise_1.72.png "Uruchomienie curler")

## Exercise 1.8

Dockerfile użyty do ćwiczenia  
![Dockerfile ćwiczenia web-server](images/section3/exercise_1.82.png "Dockerfile ćwiczenia web-server")

`docker build . -t web-server` – budowa obrazu web-server  
`docker run web-server` – uruchomienie kontenera  
![Uruchomienie web-server](images/section3/exercise_1.81.png "Uruchomienie web-server")

## Section 4.

Instalacja curl i Pythona w kontenerze – przygotowanie środowiska do pobierania plików  
![Instalacja curl i Pythona w kontenerze](images/section4/1.png "Instalacja curl i Pythona w kontenerze")

`docker run yt-dlp https://www.youtube.com/watch?v=XsqlHHTGQrw` – pobranie filmu z YouTube przy użyciu yt-dlp  
![Pobranie filmu z YouTube w kontenerze](images/section4/2.png "Pobranie filmu z YouTube w kontenerze")

`docker run yt-dlp` – uruchomienie kontenera po ponownym zbudowaniu z ENTRYPOINT i CMD z domyślnym argumentem  
![Uruchomienie yt-dlp po zmianach w Dockerfile](images/section4/3.png "Uruchomienie yt-dlp po zmianach w Dockerfile")

`docker cp "vigorous_elbakyan://mydir/Welcome to Kumpula campus! | University of Helsinki [DptFY_MszQs].mp4" .` – skopiowanie pobranego filmu z kontenera na komputer lokalny  
![Kopiowanie pobranego filmu z kontenera](images/section4/4.png "Kopiowanie pobranego filmu z kontenera")

`docker run curler-v2 helsinki.fi` – ulepszony skrypt curler po zmianach w Dockerfile  
![Uruchomienie ulepszonego curlera](images/section4/5.png "Uruchomienie ulepszonego curlera")

Zmieniony Dockerfile użyty do ulepszenia curlera  
![Dockerfile ulepszonego curlera](images/section4/6.png "Dockerfile ulepszonego curlera")

## Section 5.

`docker run -v "%cd%:/mydir" yt-dlp https://www.youtube.com/watch?v=DptFY_MszQs` – pobranie filmu z YouTube i zapisanie go bezpośrednio na komputerze lokalnym dzięki bind mount  
![Pobranie filmu z YouTube i zapis na komputerze lokalnym](images/section5/1.png "Pobranie filmu z YouTube i zapis na komputerze lokalnym")

## Exercise 1.9

`docker run -d --name simplelogs devopsdockeruh/simple-web-service` – uruchomienie kontenera loggera w tle  
`docker cp simplelogs:/usr/src/app/text.log ./text.log` – skopiowanie wygenerowanych logów z kontenera na komputer lokalny  
![Skopiowanie logów z kontenera simplelogs na komputer lokalny](images/section5/exercise_1.9.png "Skopiowanie logów z kontenera simplelogs na komputer lokalny")

## Exercise 1.10

`docker run -p 8080:8080 simple-web-server` – uruchomienie kontenera web-server i udostępnienie go na porcie 8080, aby sprawdzić działanie w przeglądarce  
![Uruchomienie kontenera simple-web-server i sprawdzenie działania w przeglądarce](images/section5/exercise_1.10.png "Uruchomienie kontenera simple-web-server i sprawdzenie działania w przeglądarce")

## Section 6.

`docker run -p 3000:3000 rails-project` – uruchomienie aplikacji Rails i udostępnienie jej na porcie 3000  
![Uruchomienie projektu Rails i udostępnienie portu 3000](images/section6/1.png "Uruchomienie projektu Rails i udostępnienie portu 3000")

## Exercise 1.11

`docker run -p 8080:8080 spring-project` – uruchomienie projektu Spring i sprawdzenie działania w przeglądarce  
![Uruchomienie projektu Spring na porcie 8080](images/section6/exercise_1.11.png "Uruchomienie projektu Spring na porcie 8080")

## Exercise 1.12

`docker run -p 5000:5000 example-frontend` – uruchomienie projektu frontendowego i sprawdzenie działania w przeglądarce  
![Uruchomienie projektu frontendowego na porcie 5000](images/section6/exercise_1.12.png "Uruchomienie projektu frontendowego na porcie 5000")

## Exercise 1.13

`docker run -p 8080:8080 example-backend` – uruchomienie backendu i sprawdzenie odpowiedzi pod endpointem /ping  
![Uruchomienie backendu i test pod endpointem /ping](images/section6/exercise_1.13.png "Uruchomienie backendu i test pod endpointem /ping")

## Exercise 1.14

`docker build -t example-frontend --build-arg REACT_APP_BACKEND_URL=http://host.docker.internal:8080 .` – budowa obrazu frontendowego z konfiguracją połączenia do backendu  

`docker run -d -p 5000:5000 --name frontend example-frontend` – uruchomienie frontendu w tle  

`docker build -t example-backend .` – budowa obrazu backendu  

`docker run -d -p 8080:8080 --name backend example-backend` – uruchomienie backendu w tle  

Wynik działania
![Frontend komunikuje się z backendem po kliknięciu przycisku](images/section6/exercise_1.14.png "Frontend komunikuje się z backendem po kliknięciu przycisku")

Dockerfile dla backendu  
![Dockerfile backendu](images/section6/exercise_1.14_dockerfile_backend.png "Dockerfile backendu")

Dockerfile dla frontendu  
![Dockerfile frontendu](images/section6/exercise_1.14_dockerfile_frontend.png "Dockerfile frontendu")


