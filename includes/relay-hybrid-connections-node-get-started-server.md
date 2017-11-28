### <a name="create-a-nodejs-application"></a><span data-ttu-id="9cb4a-101">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="9cb4a-101">Create a Node.js application</span></span>

<span data-ttu-id="9cb4a-102">Crie um novo arquivo JavaScript chamado `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="9cb4a-103">Adicionar o pacote NPM de retransmissão</span><span class="sxs-lookup"><span data-stu-id="9cb4a-103">Add the Relay NPM package</span></span>

<span data-ttu-id="9cb4a-104">Execute `npm install hyco-ws` em um prompt de comando do Node na pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="9cb4a-105">Escrever código para receber mensagens</span><span class="sxs-lookup"><span data-stu-id="9cb4a-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="9cb4a-106">Adicione a seguinte constante ao início do arquivo `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="9cb4a-107">Adicione as seguintes constantes ao arquivo `listener.js` para obter os detalhes de conexão híbrida.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="9cb4a-108">Substitua os espaços reservados entre colchetes pelos valores obtidos quando você criou a conexão híbrida.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="9cb4a-109">`const ns` - o namespace de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="9cb4a-110">Use o nome totalmente qualificado do namespace, por exemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="9cb4a-111">`const path` - o nome da conexão híbrida.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="9cb4a-112">`const keyrule` - o nome da chave SAS.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="9cb4a-113">`const key` - o valor da chave SAS.</span><span class="sxs-lookup"><span data-stu-id="9cb4a-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="9cb4a-114">Adicione o seguinte código ao arquivo `listener.js`:</span><span class="sxs-lookup"><span data-stu-id="9cb4a-114">Add the following code to the `listener.js` file:</span></span>
   
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
    <span data-ttu-id="9cb4a-115">Veja como o arquivo listener.js deve se parecer:</span><span class="sxs-lookup"><span data-stu-id="9cb4a-115">Here is what your listener.js file should look like:</span></span>
   
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

