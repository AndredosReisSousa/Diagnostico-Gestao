# Teste do envio ao Google Sheets

Foi solicitado testar o código responsável por enviar as respostas do questionário ao Google Sheets. No repositório analisado, contudo, não existe nenhuma implementação de aplicação (ex.: arquivos React, Node.js ou scripts de integração) além de dois arquivos JSON localizados em `public/`.

Passos executados:

1. Verificação da árvore de arquivos do repositório e do conteúdo do arquivo `diagnostico-maturidade.zip`, constatando que o pacote contém apenas os JSON mencionados.
2. Pesquisa por arquivos `package.json`, `.js` ou `.ts` que pudessem indicar um código executável responsável pela integração com o Google Sheets — nenhum foi encontrado.

Atualização: após a disponibilização da página `public/index.html`, foi realizada uma chamada HTTP direta para o Apps Script informado no código:

```
curl -s -D - -H 'Content-Type: application/json' -d '{"nomeEmpresa":"Empresa Teste","emailContato":"teste@example.com","scores":{"alinhamento":3.2,"governanca":4.1,"metodologia":2.8,"ferramentas":3.7,"competencias":4.5},"strengths":"Governança; Competências e Comportamento","weaknesses":"Metodologia"}' https://script.google.com/a/macros/f5gestao.com/s/AKfycbztNR2YoThkcmjXzPMQbNh2uFtNh6gcJsJmnsvCgpFyKn2Er_VbK2qcgZIbj39Sa2Ie/exec
```

O Apps Script respondeu com `HTTP/1.1 403 Forbidden`, indicando que a URL exige autenticação ou permissões adicionais antes de aceitar requisições vindas da aplicação. Enquanto a publicação do Apps Script não for ajustada para permitir acesso anônimo ou a origem for incluída na lista de permissões, o front-end não conseguirá confirmar o envio das respostas ao Google Sheets.
