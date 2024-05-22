## Langage de Programmation Go et TinyGo
### Introduction
Go est un langage de programmation développé chez Google depuis 2007. Go est également un
langage de programmation open source conçu pour permettre de réaliser des programmes simples,
rapides et fiables.
TinyGo, officiellement parrainé par Google, est une implémentation du langage Go pour les
microcontrôleurs. En utilisant un compilateur basé sur LLVM, TinyGo peut générer un fichier
binaire suffisamment compact pour être contenu dans un microcontrôleur, y compris les
microcontrôleurs 8 bits AVR avec très peu de mémoire.

### Installation et configuration de Go et TinyGo sur Linux Ubuntu
#### Installation et configuration de Go
Téléchargez et installez Go rapidement en suivant les étapes décrites ici.
> 1. Téléchargez
Cliquez sur le lien ci-dessous pour télécharger le programme d'installation de Go. Télécharger Go pour
Linux https://go.dev/dl/go1.19.3.linux-amd64.tar.gz go1.19.3.linux-amd64.tar.gz (142 Mo)

> 2. Installez
Extrayez l'archive que vous venez de télécharger dans /usr/local, en créant une nouvelle arborescence Go
dans /usr/local/go :
```
$ tar -C /usr/local -xzf go1.19.3.linux-amd64.tar.gz
Vous devrez peut-être exécuter la commande en tant que root ou via sudo).
Ajouter /usr/local/go/bin à la variable d'environnement PATH.
Vous pouvez le faire en ajoutant la ligne suivante à votre $HOME/.profile ou /etc/profile (pour une
installation à l'échelle du système) :
exporter PATH=$PATH:/usr/local/go/bin
Remarque : Les modifications apportées à un fichier de profil peuvent ne s'appliquer qu'à la prochaine
connexion à votre ordinateur. Pour appliquer les modifications immédiatement, exécuter simplement les
commandes shell directement ou exécuter-les à partir du profil à l'aide d'une commande telle que source
$HOME/.profile.
Vérifiez que vous avez installé Go en ouvrant une invite de commande et en saisissant la commande
suivante :
mamadou@dugny:~$ go version
go version go1.19.2 linux/amd64
mamadou@dugny:~$ go env
GO111MODULE=""
GOARCH="amd64"
GOBIN=""
GOCACHE="/users/mamadou/.cache/go-build"
GOENV="/users/mamadou/.config/go/env"
GOEXE=""
```
