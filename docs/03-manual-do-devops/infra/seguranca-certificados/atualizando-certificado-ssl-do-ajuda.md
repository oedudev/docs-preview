---
id: 59
title: "Atualizando Certificado SSL do Ajuda"
updated_at: 2025-05-12T03:23:45.000000Z
---

# Atualizando Certificado SSL do Ajuda

# Renovação de Certificado SSL para Bookstack

Este documento explica o processo de renovação do certificado SSL para a instância Bookstack hospedada em `ajuda.digitalsys.com.br` e como o sistema de renovação automática foi configurado.

## Informações do Certificado

- **Domínio**: ajuda.digitalsys.com.br
- **Tipo de Chave**: ECDSA
- **Caminho do Certificado**: /etc/letsencrypt/live/ajuda.digitalsys.com.br/fullchain.pem
- **Caminho da Chave Privada**: /etc/letsencrypt/live/ajuda.digitalsys.com.br/privkey.pem
- **Data de Expiração**: 10 de agosto de 2025 (renovado em 12 de maio de 2025)

## Renovação Manual do Certificado

Se for necessário renovar o certificado manualmente, você pode executar o seguinte comando:

```bash
certbot renew --force-renewal
```

Este comando tentará renovar todos os certificados gerenciados pelo Certbot que estão próximos da expiração.

Para renovar um certificado específico:

```bash
certbot renew --cert-name ajuda.digitalsys.com.br
```

Após a renovação, o Apache será recarregado automaticamente para aplicar o novo certificado.

## Sistema de Renovação Automática

Foram configurados dois mecanismos redundantes para garantir a renovação automática do certificado:

### 1. Script Personalizado de Renovação

Foi criado um script personalizado em `/usr/local/bin/renew-ssl.sh` que:
- Tenta renovar o certificado
- Recarrega o Apache após a renovação bem-sucedida
- Registra o resultado em um arquivo de log

**Código do Script**:

```bash
#!/bin/bash
# SSL certificate renewal script
certbot renew --quiet
if [ $? -eq 0 ]; then
  systemctl reload apache2
  echo "Certificate renewal completed successfully on $(date)" >> /var/log/ssl-renewal.log
else
  echo "Certificate renewal failed on $(date)" >> /var/log/ssl-renewal.log
fi
```

### 2. Configuração do Cronjob

Um cronjob foi configurado para executar o script de renovação diariamente às 2h da manhã:

```
0 2 * * * /usr/local/bin/renew-ssl.sh
```

**Explicação do Cronjob**:
- `0` - Minuto (0 = no início da hora)
- `2` - Hora (2 = 2h da manhã)
- `* * *` - Executar todos os dias, todos os meses, todos os dias da semana
- `/usr/local/bin/renew-ssl.sh` - Caminho para o script a ser executado

### 3. Timer do Systemd

Além do cronjob, o sistema também utiliza o timer do systemd para o Certbot, que é executado duas vezes ao dia:

```
certbot.timer - Run certbot twice daily
```

Este timer é instalado automaticamente pelo pacote Certbot e fornece uma camada adicional de redundância.

## Verificação do Status do Certificado

Para verificar o status atual do certificado:

```bash
certbot certificates
```

Este comando mostrará todos os certificados gerenciados pelo Certbot, incluindo suas datas de expiração.

## Verificação dos Logs de Renovação

Os logs de renovação do certificado podem ser encontrados em:

1. Log do Certbot:
```bash
cat /var/log/letsencrypt/letsencrypt.log
```

2. Log do script personalizado:
```bash
cat /var/log/ssl-renewal.log
```

## Solução de Problemas

Se o certificado não for renovado automaticamente:

1. Verifique se o script de renovação tem permissões de execução:
```bash
ls -la /usr/local/bin/renew-ssl.sh
```

2. Verifique se o cronjob está configurado corretamente:
```bash
crontab -l
```

3. Verifique o status do timer do systemd:
```bash
systemctl status certbot.timer
```

4. Tente executar o script manualmente para identificar possíveis erros:
```bash
/usr/local/bin/renew-ssl.sh
```

5. Verifique os logs para identificar erros específicos.

## Contato para Suporte

Em caso de problemas com a renovação do certificado, entre em contato com a equipe de infraestrutura através do canal #infra no Slack.