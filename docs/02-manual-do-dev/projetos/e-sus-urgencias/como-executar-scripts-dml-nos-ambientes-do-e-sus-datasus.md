
# Como executar scripts DML nos ambientes do e-SUS (DataSUS)

#### **Garanta que você tenha os seguintes acessos:**

1. VPN FortiClient
2. Acesso ao Rancher: [https://console-prd.saude.gov.br/](https://console-prd.saude.gov.br/)

Em todo o processo você precisará **obrigatoriamente** estar com a VPN ligada. **Lembrando que, para ligar a VPN FortiClient, primeiro você terá que se desconectar da VPN Pritunl da empresa para evitar conflitos.**

#### **Passo a passo:**

**1.** Entre no **Rancher**, abra o **pod de backend** do ambiente que você deseja atualizar e clique nos três pontinhos → **Execute Shell**.

  
[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2026-01/scaled-1680-/PgginvfmbwMNKaLt-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2026-01/PgginvfmbwMNKaLt-image.png)

**OBS:** lembrando que o banco de dados do ambiente de desenvolvimento e homologação são os mesmos!

**2.** Verifique se o `psql` **(CLI do PostgreSQL)** está instalado no pod com o comando abaixo. Caso já esteja, pule para a etapa 5.

```
which psql
```

**3.** Se não houver o binário, verifique qual é o sistema operacional da imagem do pod antes de instalar o `psql` com o comando abaixo:

```
cat /etc/os-release
```

**4.** Muito provavelmente será informado de que é o **Alpine Linux**. Se for, execute o comando abaixo para instalar o `psql`:

```
apk add postgresql-client
```

Caso não seja **Alpine Linux**, instale o `psql` conforme o gerenciador de pacotes do sistema operacional do pod.

E para verificar se a instalação foi efetuada com sucesso, execute o comando "**psql --version**".

**5.** Com o binário do `psql` instalado, conecte-se ao banco via `psql` usando o comando abaixo.

```
PGPASSWORD=${DB_PASSWORD} psql -h ${DB_HOST} -p ${DB_PORT} -U ${DB_USER} -d ${DB_NAME}
```

Caso o comando falhe, verifique quais variáveis de ambiente (as importantes são aquelas **DB\_alguma-coisa** ou algo parecido) o pod possui usando o comando `export` e substitua as variáveis no comando de conexão.

**6.** Já dentro do banco de dados, execute os scripts que foram informados pela equipe de DB do DataSUS como sendo um script DML, provavelmente vai estar assim (o script DML seria o código comentado), ou então será o script todo, isso será informado por eles:

  
[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2026-01/scaled-1680-/4Gv3UQH77i4OpgSr-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2026-01/4Gv3UQH77i4OpgSr-image.png)

Execute esse script no banco de dados.

**7.** Estando tudo certo, pode sair do `psql` **(CLI do PostgreSQL)** com o comando "**\\q**", feche o shell do pod e deslogue do **Rancher**.  
Se der tudo certo, o processo foi finalizado com sucesso!