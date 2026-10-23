# Docker

### Externi odkazy

[Docker - FAQ](http://prakhar.me/docker-curriculum/)  

### Konfigurace

`%%export DOCKER_HOST=ssh://user@server%%` ... docker příkaz se bude vykonavat vzdáleně na zadaném serveru  
.docker/config.json ... konfigurace docker clienta  
docker info ... ukáže informace o Dockeru: verze, ipadresy, certifikáty atd  
docker system info ... to samé jako docker info  
docker system df ... informace o místu na disku, co docker zabírá  
docker system events ... sledování událostí v reálném čase  
### Nástroje

[portainer](http://portainer.io) ... grafická administrace Dockeru, Swarmu, Kubernetes, Nomad  
buildah ... nastroj na buildování a odesílání Docker obrazů  
kaniko ... jako buildah - nastroj na buildování a odesíláni Docker obrazů  

### Sluzba docker

systemctl start docker.io  
rm -rf /var/lib/docker/aufs ... v pripade problemu se startem je toto oprava  

### Obrazy

docker search centos ... hleda CentOS obrazy na [hub.docker.com/_/centos/](https://hub.docker.com/_/centos/)  
docker pull centos:7 ... stahne Centos obraz z [hub.docker.com/_/centos/](https://hub.docker.com/_/centos/)  
docker pull [jdeathe/centos-ssh](https://hub.docker.com/r/jdeathe/centos-ssh/) ... Centos 7 + ssh  
docker images ... seznam obrazu  
docker image rm b46fb5eafd46 ... smaže obraz b46fb5eafd46  
docker history centos:7 ... historie obrazu (kdy se dely jake upravy)  
docker inspect centos:7 ... podrobne informace o obrazu, jako treba obsah Docker souboru  
docker tag b46fb5eafd46 server:port/image:3.3.0 ... přidá tag, repozitář server:port/image, verze 3.3.0  
### Kontejnery

docker [run](https://docs.docker.com/engine/reference/run/) -i -t -p 80:80 d4350798c2ee /bin/bash ... spusti kontejner s prikazem bash  
docker %%--%%mount type=bind,source=/mnt/docker1,target=/data,readonly %%--%%name "kontejner_s_diskem" kontejner1 ... vytvori novy kontejner z obrazu kontejner1, pojmenuje ho a namountuje disk  
docker run -mount source=myvol2,target=/app kontejner ... vytvori kontejner s namountovanym volume  
docker run -v myvol,/app kontejner ... to same  
docker run --rm -it --cap-add=SYS_ADMIN debian:jessie ... spusti docker se SYS_ADMIN pravama (moznost mountovat file systemy a jine)  
docker run --user root --name mujkonterjner -p 8000:8000 nginx ... spustí konterner pod rootem, nastaví jméno kontejneru a publikaci portů  
[docker ps -a](https://docs.docker.com/engine/reference/commandline/ps/) ... vylistuje kontejnery  
docker ps -a -q -f ancestor=image1 ... vylistuje jen kontejnery vznikle z obrazu image1, zobrazi jen ID (lze kombinovat s docker rm atd)  
docker start 3a09b2588478 ... spusti kontejner  
docker stop 3a09b2588478 ... ukonci konterner  
docker rm -f 3a09b2588478 ... smaze kontejner, i pokud jede  
docker attach 3a09b2588478 ... pripoji se ke kontejneru  
docker exec -i 3a09b2588478 /bin/bash ... spusti interaktivne na kontejneru bash  
docker commit 3a09b2588478 ubuntu:14.04 ... ulozi kontejner jako novy image  
docker container ls -a ... seznam vsech kontejneru, vcetne stopnutych  
docker logs --since=-2h 3a09b2588478 ... vypis konzole kontejneru za poslední 2 hodiny  

### volumes - disky

docker volume create my-vol ... vytvori novy volume  
docker volume inspect my-vol ... ukaze informace o volume  
docker volume ls ... vylistuje jednotky  
docker volume rm my-vol ... smaze volume  
docker volume  inspect my-vol ... informace o jednotce  
### config - konfigurační soubory pro kontejnery

docker config ls ... seznam uložených konfigurací  
docker config inspect aaa ... ukáže konkrétní konfiguraci  

### network

docker network ls ... seznam síťových služeb  
docker network inspect ingress ... konfigurace síťové služby  
### Export/import

docker import /tmp/konterner.tgz ... naimportuje kontejner ze souboru  
docker import  --message "konterner s debug parametrem" --change "ENV DEBUG 1" http://tomas.lipensky.cz/kontejner.tgz ... import z URL, komentar a zmena v kontejneru  
tar -c . | docker import - importovanykontys ... import z aktualniho adresare  
docker export kontejner1 > kontejner1.tar ... export konterneru do souboru  
docker export --output="kontejner2.tar" kontejner2 ... export do souboru  

### Docker Swarm

Docker swarm umožnuje propojit a administrovat Docker na více nodech  
docker node ls ... seznam nodů  
docker node ps <node> ... seznam kontejnerů na serveru <node>  
docker node ps $(docker node ls -q) ... seznam kontejnerů na všech serverech (nodech) na swarmu  
docker node ps $(docker node ls -q) --filter desired-state=Running | uniq ... jak předchozí, ukáže jen jedoucí kontejnery  
docker service ls ... seznam kontejnrů jedoucích v celém swarmu  
docker swarm ca ... certifikát swarmu  
docker swarm join ... připojení nodu do Swarmu  
docker swarm leave ... odpojení od swarmu  

### Dockerfile

Soubor z ktereho se builduji dalsi images
   

```
FROM local/c7-systemd
RUN yum -y install httpd; yum clean all; systemctl enable httpd.service
EXPOSE 80
CMD ["/usr/sbin/init"]
```


docker build %%--%%rm -t local/c7-systemd-httpd ... vytvori z obrazu jiny obraz, provede prikazy z Dockerfile  

### Docker pod Windows

(Get-Item "HKLM:SOFTWARE\Microsoft\Windows NT\CurrentVersion").GetValue('ReleaseID') ... napr 1709  
docker search microsoft/ ... seznam dosupnych obrazu z microsoftu  
docker image pull microsoft/nanoserver :1709 ... stazeni obrazu pro tento system  
docker image pull microsoft/powershell ... stahne posledni verzi obrazu, nemusi podporovat tuto verzi WIndows  
docker run -it -u Administrator microsoft/powershell cmd ... spusti obraz pod administratorem (nelze spustit primo powershell)  

SFTP kontejner - ukazka:

```
FROM microsoft/powershell:nanoserver-1803
SHELL ["pwsh.exe", "-command"]
ENV ProgramFiles="C:\Program Files"
RUN mkdir /tmp
RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; Invoke-WebRequest -uri  https://github.com/PowerShell/Win32-OpenSSH/releases/download/v7.9.0.0p1-Beta/OpenSSH-Win64.zip -outFile /tmp/OpenSSH-Win64.zip;
RUN Expand-Archive -Path /tmp/OpenSSH-Win64.zip -DestinationPath /;
RUN mkdir C:/Programdata/ssh; mkdir /payment-la
COPY sshd_config /Programdata/ssh/sshd_config
RUN cd OpenSSH-Win64; & ./ssh-keygen.exe -A;
#RUN net user tomas tomas123 /ADD
CMD ["C:\\OpenSSH-Win64\\sshd.exe", "-d", "-f", "C:\\Programdata\\ssh\\sshd_config"]
```
