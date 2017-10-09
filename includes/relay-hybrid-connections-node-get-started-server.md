### <a name="create-a-nodejs-application"></a>Criar um aplicativo do Node.js

Crie um novo arquivo JavaScript chamado `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Adicionar pacote de NPM de retransmissão Olá

Execute `npm install hyco-ws` em um prompt de comando do Node na pasta do projeto.

### <a name="write-some-code-tooreceive-messages"></a>Escrever um código tooreceive mensagens

1. Adicionar Olá após constante toohello superior de saudação `listener.js` arquivo.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Adicionar Olá toohello constantes a seguir `listener.js` detalhes de conexão híbrida Olá no arquivo. Substitua espaços reservados de saudação entre colchetes com valores hello obtido quando você criou a conexão do hello híbrida.
   
   1. `const ns`-Olá namespace de retransmissão. Ser nome de namespace totalmente qualificado do hello toouse se; Por exemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome hello de conexão do hello híbrida.
   3. `const keyrule`-nome de saudação da chave SAS de saudação.
   4. `const key`-Olá valor de chave de SAS.

3. Adicionar Olá toohello de código a seguir `listener.js` arquivo:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Veja como o arquivo listener.js deve se parecer:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

