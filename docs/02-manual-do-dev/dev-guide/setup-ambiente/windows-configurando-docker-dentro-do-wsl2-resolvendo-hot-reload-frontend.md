
# [Windows] Configurando Docker dentro do WSL2 / Resolvendo hot reload frontend

#### 1 - Procure por Ubuntu na Microsoft Store para baixar o WSL2 com uma imagem do Ubuntu

[![1.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/ubxFlVq4q7y797Qe-1.png)

#### 2 - Digite Ubuntu na barra de pesquisa e abra o terminal do WSL

#### 3 - Dentro do WSL instale o docker engine seguindo o guia abaixo, intalando usando o repositorio apt

[https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository](#bkmrk--12 "https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository")

[![3.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-2.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/LpwvtHw2cHRGb3jY-3.png)

#### 4 - Após isso siga as intruções de pós instalação para evitar futuros erros de permissões do Docker.

[https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)

[![4.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-3.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/3BR42i1KDzFvPckI-4.png)

#### 5 - Dentro do ambiente WSL, clone o repositório do dip.

[![5.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-4.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/h6J0hg7NkaxcnjmH-5.png)

#### 6 - Para autenticação, no username digite seu email. Em password, gere um token de acesso pessoal dentro do Github(imagem abaixo).

[![6.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-5.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/ZG4rNMDXX930t8Xc-6.png)

#### 7 - No diretório do repositorio rode o comando "`code ."` que na primeira vez, automaticamente instala o VScode Server for Linux.

[![7.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-6.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/pMAHkzvSTn3QORHy-7.png)

#### 8 - O VScode irá abrir na pasta do repositório, a tag em azul na parte inferior escrito WSL : Ubuntu indica que o VScode está rodando uma instancia dentro do WSL.

Ao abrir o terminal integrado irá abrir o terminal do Ubuntu no WSL.

[![8.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-7.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/NKjH1RWHweyLGR8R-8.png)

#### 9 - Para o gerenciamento do Docker de forma mais visual pode ser feita utilizando a extensão do Docker no Vscode.

[![9.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-8.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/MiepvnCrNv82P82P-9.png)

#### 10 - Ou utilizando o Docker Desktop, indo em : Settings &gt; Resources &gt; WSL integration &gt; e habilite todas as opções de integrações com distros adicionais. 

Após habilitar, reinicie o Docker Desktop.

[![10.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-9.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/Drs82l5xDOkCdrFg-10.png)

#### 11 - No terminal do WSL, no diretorio do repositorio, rode o comando : `docker compose up --build -d` .

( Se houver algum erro de permissão nessa parte, verifique se o guia de pós-instalação do Docker Engine foi seguido corretamente).

[![11.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-10.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/3M5fLQWH2hG6DhUe-11.png)

#### 12 - É possivel gerenciar os Conteiners rodando dentro do WSL, pela extensão do VScode. 

[![12.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-11.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/aGGhamGtbKttwmPw-12.png)

### \[ADICIONAL BANCO DE DADOS MONGO\]

##### 1 - Para gerenciar o banco de dados MongoDB, baixe a ferramenta MongoDB Compass.

[https://www.mongodb.com/try/download/compass](https://www.mongodb.com/try/download/compass)

##### 2 - Crie uma nova Conexão , e em Autenticação, insira o Username e Password definidos no arquivo docker-compose.yaml

[![13.png](/docs-preview/img/windows-configurando-docker-dentro-do-wsl2-resolvendo-hot-reload-frontend-12.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/scaled-1680-/1wXviQZzWgFgCLoG-13.png)