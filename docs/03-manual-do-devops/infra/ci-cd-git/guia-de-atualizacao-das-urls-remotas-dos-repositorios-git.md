---
id: 39
title: "Guia de Atualização das URLs Remotas dos Repositórios Git"
updated_at: 2025-05-29T19:53:32.000000Z
---

# Guia de Atualização das URLs Remotas dos Repositórios Git

Este guia foi criado para ajudar o time a executar os scripts desenvolvidos para alterar as URLs remotas dos repositórios Git nos projetos locais, migrando para a da nova organização.

### **1. Baixando os Scripts**

Baixe o script correspondente ao seu sistema operacional:

- [**Windows**](https://ajuda.digitalsys.com.br/attachments/2)
- [**Linux/Mac**](https://ajuda.digitalsys.com.br/attachments/1)

Coloque o script na pasta onde estão localizados todos e apenas os projetos internos da empresa. Caso essa pasta não exista, crie uma nova ou pule para a seção de [execução manual](https://ajuda.digitalsys.com.br/books/infra/page/guia-de-atualizacao-das-urls-remotas-dos-repositorios-git#bkmrk-3.-alterando-o-remot).

**Exemplo de estrutura:**

```
projetos-digitalsys/
 ├──  statis/
 ├──  hsoares/
 ├──  ...
 └──  rename_remote_urls.exe
```

---

### **2. Executando o Script**

##### Windows

- Navegue até a pasta onde o arquivo `rename_remote_urls.exe` está localizado.
- Dê um duplo clique no executável ou execute-o pelo terminal:   
    `./rename_remote_urls.exe`
- O script buscará e atualizará automaticamente as URLs remotas de todos os repositórios da organização.

##### Linux/Mac

- Navegue até o diretório onde o script `rename_remote_urls.sh` está localizado.
- Dê permissão de execução ao arquivo:   
    `chmod +x rename_remote_urls.sh`
- Execute o script:   
    `./rename_remote_urls.sh`
- O script buscará e atualizará automaticamente as URLs remotas de todos os repositórios.

Você pode verificar se funcionou entrando em algum repositório e rodando o comando `git remote -v`, se tiver funcionado, a URL de saída deve conter a tag da nova org '`digitalsys-tecnologia`'. Caso ainda conste a tag antiga '`DigitalsysTecnologia`', tente novamente ou prossiga para a [alteração manual](https://ajuda.digitalsys.com.br/books/infra/page/guia-de-atualizacao-das-urls-remotas-dos-repositorios-git#bkmrk-3.-alterando-o-remot).

### **3. Alterando o Remote Manualmente no Git**

Caso os scripts não funcionem, você pode alterar o remote manualmente pela pasta de cada repositório:

- Navegue até o diretório do repositório local
- Verifique as URLs remotas existentes:  
    `git remote -v` (saída esperada: `origin https://github.com/DigitalsysTecnologia/nome-do-repo.git`)
- Altere a URL do remote "origin":  
    `git remote set-url origin https://github.com/digitalsys-tecnologia/nome-do-repo.git`
- Confirme a alteração:  
    `git remote -v` (saída esperada: `origin https://github.com/digitalsys-tecnologia/nome-do-repo.git`)

### **4. Possíveis Problemas**

##### Problema: "Execution Policy" no Windows

- **Mensagem:** "A execução de scripts foi desabilitada neste sistema."
- **Solução:** Execute o seguinte comando no PowerShell como Administrador:   
    `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser`

##### Problema: "Permissão Negada" no Linux/Mac

- **Mensagem:** "Permission Denied"
- **Solução:** Conceda permissão de execução ao arquivo do script:   
    `chmod +x rename_remote_urls.sh`

### **5. Conclusão**

Com este guia, o time deve conseguir executar os scripts para atualização das URLs remotas com facilidade. Em caso de dúvidas, consulte a seção de problemas ou entre em contato com o Victor ou com o Eduardo.

### **6. Problemas com token**

Em caso de problemas com os conteineres Docker, revisar a inserção de seu token de verificação de identidade. Neste cenário, acesse a url `https://github.com/settings/tokens` , crie um token (pode ser de sua preferência, classic ou fine-grained) e coloque em suas permissões "read:packages". Em seguida, salve o token, e no terminal de sua aplicação rode o seguinte comando: 

`echo SEU_TOKEN | docker login ghcr.io -u SEU_USERNAME --password-stdin`  
Espera-se que seja exibida no terminal a mensagem "Login succeeded.". Após isso, rode o comando de build do docker novamente.