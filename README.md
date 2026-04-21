# Materiały na warsztaty Funduszu ZDOLNI w 2026 r.
## Zanim rozpoczniemy
1. Instalacja Ubuntu lub [WSL](https://apps.microsoft.com/detail/9PDXGNCFSCZV?hl=en-us&gl=PL&ocid=pdpshare).
2. Instalacja `screen`a:
```
   sudo apt-get update
   sudo apt-get upgrade
   sudo apt install screen
 ```
4. Instalacja `Docker`a:
```
  sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc podman-docker containerd runc | cut -f1)
  sudo apt update
  sudo apt install ca-certificates curl
  sudo install -m 0755 -d /etc/apt/keyrings
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
  sudo chmod a+r /etc/apt/keyrings/docker.asc
  
  # Add the repository to Apt sources:
  sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
  Types: deb
  URIs: https://download.docker.com/linux/ubuntu
  Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
  Components: stable
  Architectures: $(dpkg --print-architecture)
  Signed-By: /etc/apt/keyrings/docker.asc
  EOF
  
  sudo apt update
```
Możemy ją przetestować:
```
sudo docker run hello-world
```
5. Utworzenie środowiska:
   - Utworzenie katalogu (najlepiej w katalogu domowym WSL):
     ```
     mkdir rstudio
     ls -lah
     ```
   - rozpoczęcie sesji `screen`:
     ```
     screen -S rstudio
     ```
     zawsze można połączyć się z tą sesją za pomocą komend:
     ```
     screen -d rstudio
     screen -R rstudio
     ```
   - rozpoczęcie sesji Rstudio Docker. Należy ustawić swoje hasło do interfejsu:
     ```
     sudo docker run \
      -e PASSWORD='TwojeHas£o' \
      -e ROOT=TRUE \
      -v /home/sbaluszek/rstudio:/home/rstudio/projects \
      -p 8789:8787 \
      bioconductor/bioconductor_docker:RELEASE_3_21-r-4.5.2
     ```
   - W przeglądarce (`http://localhost:8789`) powinno być dostępne Rstudio. Nazwa użytkownika to domyślnie `rstudio`.
6. Instalacja pakietów - w *terminalu* należy wykonać komendę `Rscript install.R`
