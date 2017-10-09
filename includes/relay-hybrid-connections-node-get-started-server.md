### <a name="create-a-nodejs-application"></a><span data-ttu-id="52cbb-101">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="52cbb-101">Create a Node.js application</span></span>

<span data-ttu-id="52cbb-102">Crie um novo arquivo JavaScript chamado `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="52cbb-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="52cbb-103">Adicionar pacote de NPM de retransmissão Olá</span><span class="sxs-lookup"><span data-stu-id="52cbb-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="52cbb-104">Execute `npm install hyco-ws` em um prompt de comando do Node na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="52cbb-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="52cbb-105">Escrever um código tooreceive mensagens</span><span class="sxs-lookup"><span data-stu-id="52cbb-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="52cbb-106">Adicionar Olá após constante toohello superior de saudação `listener.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="52cbb-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="52cbb-107">Adicionar Olá toohello constantes a seguir `listener.js` detalhes de conexão híbrida Olá no arquivo.</span><span class="sxs-lookup"><span data-stu-id="52cbb-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="52cbb-108">Substitua espaços reservados de saudação entre colchetes com valores hello obtido quando você criou a conexão do hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="52cbb-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="52cbb-109">`const ns`-Olá namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="52cbb-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="52cbb-110">Ser nome de namespace totalmente qualificado do hello toouse se; Por exemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="52cbb-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="52cbb-111">`const path`-nome hello de conexão do hello híbrida.</span><span class="sxs-lookup"><span data-stu-id="52cbb-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="52cbb-112">`const keyrule`-nome de saudação da chave SAS de saudação.</span><span class="sxs-lookup"><span data-stu-id="52cbb-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="52cbb-113">`const key`-Olá valor de chave de SAS.</span><span class="sxs-lookup"><span data-stu-id="52cbb-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="52cbb-114">Adicionar Olá toohello de código a seguir `listener.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="52cbb-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="52cbb-115">Veja como o arquivo listener.js deve se parecer:</span><span class="sxs-lookup"><span data-stu-id="52cbb-115">Here is what your listener.js file should look like:</span></span>
   
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

