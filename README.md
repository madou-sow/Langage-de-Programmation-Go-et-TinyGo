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

#### Installation et configuration de TinyGo
Go doit déjà être installé sur votre machine pour pouvoir installer TinyGo. Nous recommandons Go
v1.18 ou supérieur.
Si vous utiliser Ubuntu ou un autre Linux basé sur Debian, téléchargez le fichier DEB depuis
Github et installez-le à l'aide des commandes suivantes :
```
 wget https://github.com/tinygo-org/tinygo/releases/download/v0.26.0/tinygo_0.26.0_amd64.deb
 dpkg -i tinygo_0.26.0_amd64.deb
```
Ajouter le chemin vers l’exécutable de TinyGo dans votre variable d’environnement PATH :
```
export PATH=$PATH:/usr/local/bin
```
Tester si l’installation s’est parfaitement déroulée en exécutant la commande qui devrait afficher le
numéro de version de TinyGo :
```
$ tinygo version
tinygo version 0.26.0 linux/amd64 (using go version go1.19.2 and LLVM version 14.0.0)
```
Pour compiler et téléverser des programmes TinyGo dans un microcontrôleur AVR comme celui de
l’Arduino Uno, vous devez encore installer des outils supplémentaires :
```
apt-get install gcc-avr avr-libc avrdude
```

### Un premier programme en langage tinygo faisant clignoter la carte ESP-WROOM-32D
Vous devez installer la chaîne d'outils Espressif pour Linux pour utiliser TinyGo avec l'ESP32 :
```
https://docs.espressif.com/projects/esp-idf/en/release-v3.0/get-started/linux-
setup.html#standard-setup-of-toolchain-for-linux
```
De plus, vous devez installer l'outil de flash esptool :
```
https://github.com/espressif/esptool#easy-installation
```
Vous devriez maintenant pouvoir flasher votre carte comme suit :
```
Branchez votre carte ESP32 sur le port USB de votre ordinateur.
```
Construisez et flashez votre code TinyGo à l'aide de la commande flash tinygo. Cette commande
devrait faire clignoter l'ESP32 avec l'exemple blinky :
```
tinygo flash -target=esp32-mini32 -port=/dev/ttyUSB0 examples/blinky
```
**EXEMPLE 1 : blinky.go**
```
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ cat blinky.go
package main
import (
"machine"
"time"
)
func main() {
// Utilisation de la LED intégrée en surface de la carte, broche D13
var led machine.Pin = machine.Pin(13)
// Configuration de la broche en sortie
led.Configure(machine.PinConfig{Mode: machine.PinOutput})
for {
led.High() // sortie au niveau logique haut, LED allumée
time.Sleep(time.Millisecond * 500) // temporisation 500 millisecondes
led.Low() // sortie au niveau logique bas, LED éteinte
time.Sleep(time.Millisecond * 500) // temporisation 500 millisecondes
}
}
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ go mod init blinky
go: creating new go.mod: module blinky
go: to add module requirements and sums:
go mod tidy
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ ls -l
total 8
-rw-rw-r-- 1 mamadou mamadou 595 Oct 13 09:28 blinky.go
-rw-rw-r-- 1 mamadou mamadou 23 Oct 13 09:56 go.mod
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ cat go.mod
module blinky
go 1.19
```
**EXEMPLE 2 : blinkblue.go**
Il existe un exemple fourni avec le package TinyGo que vous avez configuré à l'étape précédente,
vous pouvez le trouver dans le répertoire TinyGo/examples. Voici un code qui fonctionne avec la
majorité de la carte de développement ESP32 l’on peut rencontrer des problèmes avec le numéro
des broches ou le numéro "Pin"
```
package main
import (
"machine"
"time"
)
func main() {
      // On board LED is connected to GPIO 2
      led := machine.Pin(2)
      // Configure PIN as output
      led.Configure(machine.PinConfig{Mode: machine.PinOutput})
      // Infinite main loop
      for {
           // Turn LED off
           led.Low()
           // Wait for 1 second
           time.Sleep(time.Millisecond * 1000)
           // Turn LED on
           led.High()
           // Wait for 1 second
           time.Sleep(time.Millisecond * 1000)
      }
}
```
Et maintenant .... flashons le code sur l'ESP32. Si tout se passe comme prévu, la LED de votre
ESP32 commencera à clignoter dans quelques secondes à peine !

**tinygo flash -target esp32 -port /dev/ttyUSB0 blinkblue.go**
```
esptool.py v4.5.dev0
Serial port /dev/ttyUSB0
Connecting.....
Chip is ESP32-D0WD (revision v1.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme
None
Crystal is 40MHz
MAC: ac:0b:fb:26:ff:58
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Flash will be erased from 0x00001000 to 0x00001fff...
Warning: Image file at 0x1000 is protected with a hash checksum, so not
changing the flash mode setting. Use the --flash_mode=keep option instead of --
flash_mode=dout in order to remove this warning, or use the --dont-append-
digest option for the elf2image command in order to generate an image file
without a hash checksum
Compressed 3232 bytes to 2426...
Wrote 3232 bytes (2426 compressed) at 0x00001000 in 0.3 seconds (effective 92.1
kbit/s)...
Hash of data verified.
Leaving...
Hard resetting via RTS pin...
```
Préparez votre carte ESP-WROOM-32D en la connectant sur le port USB. Un nouveau port devrait
apparaître avec la commande :
```
$ ls -l /dev/tty*
```
En général, il s’agit du port /dev/ttyUSB0. Avant de téléverser le programme dans la carte, il vous
faudra probablement modifier les droits d’accès au port USB (message Error opening serial port...).
La raison est que le propriétaire du fichier /dev/ttyUSB0 fait partie du groupe dialout :
```
crw-rw---- 1 root dialout 166, 0 févr. 26 10:49 /dev/ttyUSB0
```
Il faut donc ajouter l’utilisateur à ce groupe :
```
$ sudo usermod -a -G dialout mamadou
```
où est le nom utilisateur. Il faudra vous déconnecter et vous reconnecter pour que cela prenne effet.
Pour compiler et téléverser le programme, exécuter la commande :
```
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ ls -l
total 12
-rw-rw-r-- 1 mamadou mamadou 596 nov. 15 13:08 blinky.go
-rw-rw-r-- 1 mamadou mamadou 23 oct. 13 09:56 go.mod
-rw-r--r-- 1 mamadou mamadou 158 nov. 15 14:16 readme.txt
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ cd /usr/local/lib/tinygo/targets
mamadou@port-lipn12:/usr/local/lib/tinygo/targets$ ls -l esp32*
-rw-r--r-- 1 root root
61 sept. 29 15:28 esp32c3-12f.json
-rw-r--r-- 1 root root 577 sept. 29 15:28 esp32c3.json
-rw-r--r-- 1 root root 9686 sept. 29 15:28 esp32c3.ld
-rw-r--r-- 1 root root
66 sept. 29 15:28 esp32-coreboard-v2.json
-rw-r--r-- 1 root root 862 sept. 29 15:28 esp32.json
-rw-r--r-- 1 root root 5953 sept. 29 15:28 esp32.ld
-rw-r--r-- 1 root root
40 sept. 29 15:28 esp32-mini32.json
$ tinygo flash -target esp32 -port /dev/ttyUSB0 blinky
esptool.py v4.5.dev0
Serial port /dev/ttyUSB0
Connecting.....
Chip is ESP32-D0WD (revision v1.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding
Scheme None
Crystal is 40MHz
MAC: ac:0b:fb:26:ff:58
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Flash will be erased from 0x00001000 to 0x00001fff...
Warning: Image file at 0x1000 is protected with a hash checksum, so not
changing the flash mode setting. Use the --flash_mode=keep option instead
of --flash_mode=dout in order to remove this warning, or use the --dont-
append-digest option for the elf2image command in order to generate an
image file without a hash checksum
Compressed 3232 bytes to 2436...
Wrote 3232 bytes (2436 compressed) at 0x00001000 in 0.3 seconds (effective
92.3 kbit/s)...
Hash of data verified.
Leaving...
Hard resetting via RTS pin...
```
Ici, la cible est esp32-mini32.
```
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ tinygo flash -target esp32-mini32 -port /dev/ttyUSB0 blinky
esptool.py v4.5.dev0
Serial port /dev/ttyUSB0
Connecting....
Chip is ESP32-D0WD (revision v1.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding
Scheme None
Crystal is 40MHz
MAC: ac:0b:fb:26:ff:58
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Flash will be erased from 0x00001000 to 0x00001fff...
Warning: Image file at 0x1000 is protected with a hash checksum, so not
changing the flash mode setting. Use the --flash_mode=keep option instead
of --flash_mode=dout in order to remove this warning, or use the --dont-
append-digest option for the elf2image command in order to generate an
image file without a hash checksum
Compressed 3232 bytes to 2436...
Wrote 3232 bytes (2436 compressed) at 0x00001000 in 0.3 seconds (effective
101.6 kbit/s)...
Hash of data verified.
Leaving...
Hard resetting via RTS pin...
```
Ici, la cible est esp32-coreboard-v2 .
```
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/blinky-
arduino$ tinygo flash -target esp32-coreboard-v2 -port /dev/ttyUSB0 blinky
esptool.py v4.5.dev0
Serial port /dev/ttyUSB0
Connecting....
Chip is ESP32-D0WD (revision v1.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme
None
Crystal is 40MHz
MAC: ac:0b:fb:26:ff:58
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Flash will be erased from 0x00001000 to 0x00001fff...
Warning: Image file at 0x1000 is protected with a hash checksum, so not
changing the flash mode setting. Use the --flash_mode=keep option instead of --
flash_mode=dout in order to remove this warning, or use the --dont-append-
digest option for the elf2image command in order to generate an image file
without a hash checksum
Compressed 3232 bytes to 2436...
Wrote 3232 bytes (2436 compressed) at 0x00001000 in 0.3 seconds (effective
101.6 kbit/s)...
Hash of data verified.
Leaving...
Hard resetting via RTS pin...
```

```
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/hello$ cat
hello.go
package main
import "fmt"
func main() {
fmt.Println("Hello world !")
}
mamadou@port-lipn12:~/big-data/cerin10102022/apprentissage/tinygo/hello$ tinygo
flash -target esp32 -port /dev/ttyUSB0 hello
esptool.py v4.5.dev0
Serial port /dev/ttyUSB0
Connecting.......
Chip is ESP32-D0WD (revision v1.0)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme
None
Crystal is 40MHz
MAC: ac:0b:fb:26:ff:58
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Flash will be erased from 0x00001000 to 0x0000bfff...
Warning: Image file at 0x1000 is protected with a hash checksum, so not
changing the flash mode setting. Use the --flash_mode=keep option instead of --
flash_mode=dout in order to remove this warning, or use the --dont-append-
digest option for the elf2image command in order to generate an image file
without a hash checksum
Compressed 41408 bytes to 32602...
Wrote 41408 bytes (32602 compressed) at 0x00001000 in 3.4 seconds (effective
98.2 kbit/s)...
Hash of data verified.
Leaving...
Hard resetting via RTS pin...
```
