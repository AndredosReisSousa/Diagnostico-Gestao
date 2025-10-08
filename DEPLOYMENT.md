# Deployment Guide

Este projeto é composto apenas pelo arquivo estático `public/index.html`. Você pode publicá-lo em um link privado utilizando serviços de hospedagem gratuitos com proteção por senha ou controle de acesso.

## Opção 1 – Netlify com senha
1. Crie uma conta no [Netlify](https://www.netlify.com/).
2. No painel, clique em **Add new site → Deploy manually**.
3. Arraste o arquivo `public/index.html` (ou compacte a pasta `public/` em um `.zip`) para a área de upload.
4. Após o deploy, acesse **Site settings → Build & deploy → Post processing → Password-protect your site** e defina uma senha. O link ficará privado para quem possuir a senha.

### Gerando rapidamente um link privado com a CLI
Caso prefira fazer tudo pela linha de comando, instale a [Netlify CLI](https://docs.netlify.com/cli/get-started/) com `npm i -g netlify-cli`
e execute na raiz do projeto:

```bash
netlify deploy --dir=public --message "Diagnóstico de Gestão" --password "SUA-SENHA-SECRETA"
```

O comando gera uma URL temporária (`Draft URL`) protegida pela senha informada. Compartilhe apenas com as pessoas que realizarão os testes.
Quando quiser publicar definitivamente, use `netlify deploy --prod --dir=public` e mantenha a proteção por senha configurada no painel.

## Opção 2 – Vercel com proteção por cabeçalho
1. Crie uma conta no [Vercel](https://vercel.com/).
2. Instale a CLI: `npm i -g vercel`.
3. Na pasta do projeto, execute `vercel deploy --prebuilt` e selecione **Private** quando solicitado.
4. Adicione a proteção por cabeçalho criando um arquivo `vercel.json` com:
   ```json
   {
     "headers": [
       {
         "source": "/(.*)",
         "headers": [
           {
             "key": "x-vercel-protection-bypass",
             "value": "<senha-gerada>"
           }
         ]
       }
     ]
   }
   ```
   Em seguida, gere a senha com `vercel protection bypass create` e compartilhe apenas com os usuários autorizados.

## Google Apps Script
Garanta que o `SCRIPT_URL` no HTML esteja publicado como **Web App** com acesso para "Qualquer pessoa com o link" ou conforme a política de acesso desejada. Caso exija autenticação, informe as credenciais necessárias aos usuários de teste.

## Testes locais
Para testar localmente antes da publicação, você pode executar um servidor HTTP simples:
```bash
python3 -m http.server --directory public 8080
```
O questionário ficará disponível em `http://localhost:8080/`.

