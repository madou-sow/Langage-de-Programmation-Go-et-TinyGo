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
GOEXPERIMENT=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOINSECURE=""
GOMODCACHE="/users/mamadou/go/pkg/mod"
GONOPROXY=""
GONOSUMDB=""
GOOS="linux"
GOPATH="/users/mamadou/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/local/go"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/usr/local/go/pkg/tool/linux_amd64"
GOVCS=""
GOVERSION="go1.19.2"
GCCGO="gccgo"
GOAMD64="v1"
AR="ar"
CC="gcc"
CXX="g++"
CGO_ENABLED="1"
GOMOD="/dev/null"
GOWORK=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -Wl,--no-gc-sections -fmessage-length=0 -
fdebug-prefix-map=/tmp/go-build3759803811=/tmp/go-build -gno-record-gcc-
switches
```
**Ceci est une liste partielle des commandes de l'outil Go**

| Commande | Description |
|---------:|-------------|
| go build | compile les packages et les dépendances |
| go env | affiche les informations sur l'environnement Go | 
| go get | ajoute les dépendances aux des modules courants et installe les |
| go install | compile et installe les packages et les dépendances |
| go list | liste les packages et les modules |
| go run | compile et exécute un programme Go |
| go version | affiche la version Go |

### Installation et configuration de TinyGo
Go doit déjà être installé sur votre machine pour pouvoir installer TinyGo. Nous recommandons Go
v1.18 ou supérieur.
Si vous utiliser Ubuntu ou un autre Linux basé sur Debian, téléchargez le fichier DEB depuis
Github et installez-le à l'aide des commandes suivantes :
> wget https://github.com/tinygo-org/tinygo/releases/download/v0.26.0/tinygo_0.26.0_amd64.deb

> dpkg -i tinygo_0.26.0_amd64.deb
