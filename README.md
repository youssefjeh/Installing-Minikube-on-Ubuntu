
# Installing Minikube on Ubuntu


## Installing Docker on Ubuntu


met à jour la liste des paquets sur le système, en s'assurant que les dernières versions des paquets sont utilisées.
```bash
sudo apt update
```
 installe les paquets nécessaires pour installer Docker, y compris les certificats CA, curl (pour télécharger des fichiers), gnupg (pour télécharger en toute sécurité des paquets) et lsb-release (pour identifier la version d'Ubuntu utilisée).
```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```
télécharge la clé GPG de Docker et l'importe dans le trousseau de clés système pour la vérification des paquets.
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
ajoute le dépôt Docker à la liste des sources de paquets du système, permettant au système de télécharger et d'installer les paquets Docker
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
met à jour à nouveau la liste des paquets, cette fois-ci en incluant le dépôt Docker.
```bash
sudo apt-get update
```
installe le moteur Docker, l'interface en ligne de commande et containerd.io (runtime de conteneur de bas niveau de Docker)
```bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
```
Ajoute l'utilisateur actuel au groupe docker, ce qui permet à cet utilisateur d'exécuter des commandes Docker sans utiliser sudo.
```bash
sudo usermod -aG docker $USER
```
recharge les groupes de l'utilisateur actuel pour que les modifications de la commande précédente prennent effet.
```bash
newgrp docker
```

## Installing Minikube on Ubuntu

installe les paquets nécessaires pour télécharger et installer Minikube, y compris curl, wget et apt-transport-https.
```bash
sudo apt install -y curl wget apt-transport-https
```
télécharge la dernière version de l'exécutable Minikube pour Linux (architecture amd64)
```bash
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
copie l'exécutable téléchargé dans le répertoire /usr/local/bin, qui est dans le PATH système, permettant au système de trouver et d'exécuter la commande minikube.
```bash
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
```
rend l'exécutable minikube exécutable.
```bash
sudo chmod +x /usr/local/bin/minikube
```
télécharge la dernière version de l'exécutable kubectl pour Linux (architecture amd64)
```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt` /bin/linux/amd64/kubectl
```
rend l'exécutable kubectl exécutable
```bash
chmod +x kubectl
```
déplace l'exécutable kubectl dans le répertoire /usr/local/bin, permettant au système de trouver et d'exécuter la commande kubectl
```bash
sudo mv kubectl /usr/local/bin/
```
démarre Minikube en utilisant le pilote Docker.
```bash
minikube start --driver=docker
```



