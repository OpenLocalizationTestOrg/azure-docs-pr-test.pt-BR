### <a name="create-a-nodejs-application"></a><span data-ttu-id="917ca-101">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="917ca-101">Create a Node.js application</span></span>

<span data-ttu-id="917ca-102">Crie um novo arquivo JavaScript chamado `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="917ca-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="917ca-103">Adicionar pacote de NPM de retransmissão Olá</span><span class="sxs-lookup"><span data-stu-id="917ca-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="917ca-104">Execute `npm install hyco-ws` em um prompt de comando do Node na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="917ca-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="917ca-105">Escrever um código toosend mensagens</span><span class="sxs-lookup"><span data-stu-id="917ca-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="917ca-106">Adicione o seguinte Olá `constants` toohello superior de saudação `sender.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="917ca-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="917ca-107">Adicionar Olá toohello constantes a seguir `sender.js` detalhes de conexão híbrida Olá no arquivo.</span><span class="sxs-lookup"><span data-stu-id="917ca-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="917ca-108">Substitua espaços reservados de saudação entre colchetes com valores hello obtido quando você criou a conexão do hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="917ca-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="917ca-109">`const ns`-Olá namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="917ca-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="917ca-110">Ser nome de namespace totalmente qualificado do hello toouse se; Por exemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="917ca-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="917ca-111">`const path`-nome hello de conexão do hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="917ca-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="917ca-112">`const keyrule`-nome de saudação da chave SAS de saudação.</span><span class="sxs-lookup"><span data-stu-id="917ca-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="917ca-113">`const key`-Olá valor de chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="917ca-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="917ca-114">Adicionar Olá toohello de código a seguir `sender.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="917ca-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="917ca-115">Veja como o arquivo sender.js deve se parecer:</span><span class="sxs-lookup"><span data-stu-id="917ca-115">Here is what your sender.js file should look like:</span></span>
   
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

