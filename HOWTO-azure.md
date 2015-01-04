# Microsoft Azure HowTo

[Azure Commandline Tool for Mac and Linux](http://azure.microsoft.com/de-de/documentation/articles/command-line-tools/)

## Install azure-cli

```bash
npm install -g azure
azure account download
```

## Import Azure Account information

```bash
cd ~/Downloads
azure account import Kostenlose\ Testversion-12-26-2014-credentials.publishsettings
azure account list
```

## Create SSH Key

```bash
mkdir cert
cd cert
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout azurePrivateKey.key -out azureCert.pem
chmod 600 azurePrivateKey.key
openssl x509 -outform der -in azureCert.pem -out azureCert.cer
cd ..
```

## Create Ubuntu VM

```bash
azure vm create drone-ss b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_1-LTS-amd64-server-20141125-en-us-30GB drone --location "West Europe" -z ExtraSmall -e -P -t cert/azureCert.pem
ssh-keygen -R drone-ss.cloudapp.net
```

## Login to VM

```bash
ssh -i cert/azurePrivateKey.key drone@drone-ss.cloudapp.net
```

## Other commands

```bash
azure vm location list
azure vm image list | grep 14_04
azure vm endpoint list drone-ss
azure vm endpoint create drone-ss 80 8080
azure vm endpoint delete drone-ss tcp-80-8080
```
