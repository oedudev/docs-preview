---
id: 28
title: "Instalando AWS CLI na máquina self-hosted do Github Actions"
updated_at: 2025-03-30T19:10:17.000000Z
---

# Instalando AWS CLI na máquina self-hosted do Github Actions

Atualmente as máquinas que estão rodando o Github Actions está na DigitalOcean e, para utilizar os comandos da AWS no workflow do Github Actions, é necessário instalar as dependências necessárias da AWS.

Para realizar isso será necessário entrar na máquina (via SSH ou pelo painel de controle da DigitalOcean) para, em seguida, rodar os seguintes comandos no terminal

```
apt-get install unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
unzip awscliv2.zip
./aws/install
rm -f aws
rm awscliv2.zip
```

E verifique se foi instalado corretamente com o comando

```
aws --version
```

Caso apareça algo como "aws-cli/2.22.6 Python/3.12.6 Linux/6.11.0-8-generic exe/x86\_64.ubuntu.24" a instalação foi realizada com sucesso.