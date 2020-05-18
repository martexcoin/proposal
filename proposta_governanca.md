O Governance é usado para preparar projetos de todos tipos, seja para o crescimento da moeda ou externo, tal projeto é decidido através dos Masternodes que votam e decidem o futuro desse projeto.

Custo: 5 MXT
Criando novo projeto no Blockchain da MarteXcoin

Antes é necessário gerar o JSON do projeto com suas informações, a estrutura é essa:

```
{
"end_epoch":TIMESTAMP UTC/DATA MÁXIMA DO PROJETO (numerico),
"name":"nome do projeto em minusculo (ate 20 caracteres)" (string),
"payment_address":"ENDEREÇO DA CARTEIRA" (string),
"payment_amount":QTD DE MXT A SER ARRECADADO (numerico),
"start_epoch":TIMESTAMP UTC/DATA ATUAL OU DO PRÓXIMO SUPERBLOCK (numerico),
"type":1,
"url":"SITE/DOCUMENTO DO PROJETO" (string)
}
``` 
Exemplo:
```
{
"end_epoch":1590796800,
"name":"projeto-a",
"payment_address":"mxtuiizTB3onHewHucPHTGH3sTVRFZ5Hzw",
"payment_amount":1,
"start_epoch":1589548894,
"type":1,
"url":"https://martexcoin.org"
}
```

Para converter a data em timestamp use este site aqui https://www.unixtimestamp.com/index.php

15/05/2020 10:21:34 => 1589548894
29/05/2020 21:00:00 => 1590796800

Se estiver usando linux abra o terminal e digite este comando: ```date -d 'MM/DD/AAAA HH:MM:SS' +"%s"```

```$ date -d '05/15/2020 10:21:34' +"%s"```

Após gerar esse JSON acima, é preciso codifica-lo de ASCII para HEX (pode ser usado este site aqui http://string-functions.com/string-hex.aspx), no json acima acima ficaria:
```7b0d0a22656e645f65706f6368223a313539303739363830302c0d0a226e616d65223a2270726f6a65746f2d61222c0d0a227061796d656e745f61646472657373223a226d78747569697a5442336f6e48657748756350485447483373545652465a35487a77222c0d0a227061796d656e745f616d6f756e74223a312c0d0a2273746172745f65706f6368223a313538393534383839342c0d0a2274797065223a312c0d0a2275726c223a2268747470733a2f2f6d6172746578636f696e2e6f7267220d0a7d```

Agora dentro da carteira, execute o seguinte comando:
```gobject prepare 0 1 {TIMESTAMP ATUAL / UTC} {HASH JSON}```

```gobject prepare 0 1 1589548894  7b0d0a22656e645f65706f6368223a313539303739363830302c0d0a226e616d65223a2270726f6a65746f2d61222c0d0a227061796d656e745f61646472657373223a226d78747569697a5442336f6e48657748756350485447483373545652465a35487a77222c0d0a227061796d656e745f616d6f756e74223a312c0d0a2273746172745f65706f6368223a313538393534383839342c0d0a2274797065223a312c0d0a2275726c223a2268747470733a2f2f6d6172746578636f696e2e6f7267220d0a7d```

O retorno do comando acima sera esse:
```
733fa62ebe94bde9674bce5b372c4b0d4f7f0da44a4e4b16401e330f43d95215
```
Espere 6 confirmações do collateral payment(retorno do comando gobject prepare).

Após executar o comando gobject prepare, receberá um hash. Com o mesmo hash acima, execute:
```gobject submit 0 1 {TIMESTAMP ATUAL / UTC} {HASH JSON} {HASH RECEBIDO}```

```gobject submit 0 1 1589548894 7b0d0a22656e645f65706f6368223a313539303739363830302c0d0a226e616d65223a2270726f6a65746f2d61222c0d0a227061796d656e745f61646472657373223a226d78747569697a5442336f6e48657748756350485447483373545652465a35487a77222c0d0a227061796d656e745f616d6f756e74223a312c0d0a2273746172745f65706f6368223a313538393534383839342c0d0a2274797065223a312c0d0a2275726c223a2268747470733a2f2f6d6172746578636f696e2e6f7267220d0a7d 733fa62ebe94bde9674bce5b372c4b0d4f7f0da44a4e4b16401e330f43d95215```

Pronto, projeto criado, basta publica-lo e esperar as votações dos Masternodes, sendo que é necessário minimo de 10% dos Masternodes ATIVOS em rede.


Depois que for aprovado, o próximo Budget na data prevista irá retirar 10% dos blocos para o projeto, e será pago no Próximo Superbloco.
Sendo que a recompensa do bloco ficará 45% Masternodes, 45% Mineradores e 10% Budget. Apenas se o projeto for aprovado.


Votando através do Masternode

Vá no Console(se for a grafica-QT) e digite:

```gobject list```

Pegue o HASH do projeto, anterior ao DataHex.

Votar SIM:

```gobject vote-many {HASH} funding yes```

Votar Não:

```gobject vote-many {HASH} funding no```

Votar Nulo:

```gobject vote-many {HASH} funding abstain```


FAQ
1) Quem paga?
 Budget de 10 % de todos os blocos gerados

2) Qual o amount máximo?
 Não há máximo, mas é importante ser realista e apresentar o valor necessário para o projeto.

3) Quem pode votar?
 Apenas Masternodes, mas não confunda com centralização, pois um projeto depende do Budget, esse Budget é retirado do bloco, então cada masternode deixará de receber 5% para o projeto aprovado.

4) Mineradores e Pools votam?
 Não, pois não há uma prova de que um minerador não é um usuário comum, os Masternodes fornecem uma estrutura e provam sua existência através de 5000 MXT.
