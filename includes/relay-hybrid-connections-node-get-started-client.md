### <a name="create-a-nodejs-application"></a>Criar um aplicativo do Node.js

Crie um novo arquivo JavaScript chamado `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Adicionar pacote de NPM de retransmissão Olá

Execute `npm install hyco-ws` em um prompt de comando do Node na pasta do projeto.

### <a name="write-some-code-toosend-messages"></a>Escrever um código toosend mensagens

1. Adicione o seguinte Olá `constants` toohello superior de saudação `sender.js` arquivo.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Adicionar Olá toohello constantes a seguir `sender.js` detalhes de conexão híbrida Olá no arquivo. Substitua espaços reservados de saudação entre colchetes com valores hello obtido quando você criou a conexão do hello híbrida.
   
   1. `const ns`-Olá namespace de retransmissão. Ser nome de namespace totalmente qualificado do hello toouse se; Por exemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome hello de conexão do hello híbrida.
   3. `const keyrule`-nome de saudação da chave SAS de saudação.
   4. `const key`-Olá valor de chave de SAS.

3. Adicionar Olá toohello de código a seguir `sender.js` arquivo:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Veja como o arquivo sender.js deve se parecer:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

