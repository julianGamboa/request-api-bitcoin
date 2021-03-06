#  Requisição em uma API de Criptomoedas
___
___

### Objetivos
 * Fazer uma requisição de uma API de Bitcoins.
 * Manipular os valores da API.
 * Exibir os dados em uma página web
 
### Requisitos
 * VS Code.
 * extensão do chrome [Moesif Orign & CORS Changer](https://chrome.google.com/webstore/detail/moesif-origin-cors-change/digfbfaphojjndkpccljibejjbppifbc/related?hl=pt-BR&authuser=1)
 
 * Conta de desenvolvedor na CoinMarketCap.
 * 
 1 - Acesse: [http://pro.coinmarketcap.com/account](http://pro.coinmarketcap.com/account/)
 
 2 - Clique em: GET an a API Key now.
 
 3 - Copie a key.
 
 ___

### HTML.
###### Esqueleto

~~~html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CoinMarketCap</title>
</head>
<body>
    <script type="text/javascript"></script>
</body>
</html>
~~~

 
### FETCH
###### Método do js que permite a execução dos verbos da RestAPI.

 * Método que consegue fazer as requisições.
 * Sempre dentro da tag ... <script> </script>. ...
 * É importante tratar os erros.
 	* "responde.ok" = 200
 	* "response.error" = 400, 404...
 
* A API será exibida pelo "console.log(api)"

~~~javascript
    <script type="text/javascript">
    // My api key
        var apikey = {
            key: 'SUA API KEY VEM AQUI :)'
        }
    // GET Fetch Requisition - URI que fará a nossa requisição
    fetch('https://pro.coinmarketcap.com/v1/cryptocurrency/map?CMC_PRO_API_KEY=' +
    apikey.key)
    .then((response) => { // tratamento de erro
        if(!response.ok) throw new Error('Erro ao executar a requisição, status ' + response.status);
    })
    .then((api) => { // Aqui acontece a requisição
        console.log(api); // A resposta da requisição vem por aqui
    })
    .catch((error) => { // Exibição da mensagem de possível erro
        console.log(error.message);
    });

    </script>
~~~

* Ative a extensão.
* Abra o index.html e nas ferramentas do desenvolvedor, deverá ser possível visualizar a lista de dados das moedas.
* Adicione o link do bootstrap no css.

...
<meta name="viewport" content="width=device-width, initial-scale=1.0">

~~~html
    <!-- css -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
~~~

* Envie as informações da APi para o html

~~~javascript
 .then((api) => {
        console.log(api);

        var texto  = "";
        //GEt 10 coins and symbols
        for (let i = 0; i < 10; i++)
        {
             //Show API information
             texto = texto + `

            <div class="media">
                <img src="coin.jpg" class="align-self-center mr-3" alt="coin" width="100" height="60">
                <div class="media-body">
                    <h5 class="mt-2">${api.data[i].name}</h5>
                    <p>${api.data[i].symbol}</p>
                    <p>${api.data[i].first_historical_data}</p>
                </div>
            </div>

            `;  

        //Envia os dados para dentro do HTML    
        document.getElementById("coins").innerHTML = texto;

        }   
    })
~~~

___

### src

* [index.html](https://github.com/aluiziomonteiro/request-api-bitcoin/blob/master/index.html)

* [style.css](https://github.com/aluiziomonteiro/request-api-bitcoin/blob/master/css/style.css)

* [script.js](https://github.com/aluiziomonteiro/request-api-bitcoin/blob/master/js/script.js)

* [coin.jpeg](https://github.com/aluiziomonteiro/request-api-bitcoin/blob/master/img/coin.jpeg)
