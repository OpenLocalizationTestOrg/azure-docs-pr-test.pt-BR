## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="92dab-101">Configurar dispositivo simulado do hello Node. js</span><span class="sxs-lookup"><span data-stu-id="92dab-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="92dab-102">No painel de monitoramento remoto de saudação, clique em **+ adicionar um dispositivo** e, em seguida, adicione um *personalizadas de dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="92dab-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="92dab-103">Anote Olá IoT Hub hostname, a id de dispositivo e a chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92dab-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="92dab-104">Você precisa-los posteriormente neste tutorial ao preparar o aplicativo de cliente de dispositivo de remote_monitoring.js hello.</span><span class="sxs-lookup"><span data-stu-id="92dab-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="92dab-105">Certifique-se de que o Node.js versão 0.12.x ou posterior esteja instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="92dab-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="92dab-106">Executar `node --version` em um prompt de comando ou em uma versão de saudação do shell toocheck.</span><span class="sxs-lookup"><span data-stu-id="92dab-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="92dab-107">Para obter informações sobre como usar um Gerenciador de pacote tooinstall Node. js no Linux, consulte [Node. js instalando por meio do Gerenciador de pacote][node-linux].</span><span class="sxs-lookup"><span data-stu-id="92dab-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="92dab-108">Quando você tiver instalado o Node. js, clonar a versão mais recente de saudação do hello [azure iot-sdk-nó] [ lnk-github-repo] máquina de desenvolvimento tooyour de repositório.</span><span class="sxs-lookup"><span data-stu-id="92dab-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="92dab-109">Sempre use Olá **mestre** ramificação para a versão mais recente Olá das bibliotecas de saudação e exemplos.</span><span class="sxs-lookup"><span data-stu-id="92dab-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="92dab-110">A cópia local da saudação de [azure iot-sdk-nó] [ lnk-github-repo] repositório, Olá cópia seguir dois arquivos de saudação exemplos/de dispositivo de nó tooan vazio pasta no computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="92dab-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="92dab-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="92dab-111">packages.json</span></span>
   * <span data-ttu-id="92dab-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="92dab-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="92dab-113">Abra o arquivo de remote_monitoring.js hello e procure Olá após a definição da variável:</span><span class="sxs-lookup"><span data-stu-id="92dab-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="92dab-114">Substitua a **[cadeia de conexão de dispositivo do Hub IoT]** pela cadeia de conexão do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="92dab-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="92dab-115">Use valores de saudação para o nome de host IoT Hub, id do dispositivo e a chave do dispositivo que você tenha um anotado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="92dab-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="92dab-116">Uma cadeia de caracteres de conexão do dispositivo tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="92dab-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="92dab-117">Se o nome de host do IoT Hub é **contoso** e a id do dispositivo é **meudispositivo**, sua cadeia de caracteres de conexão parece Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="92dab-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Salve o arquivo hello. <span data-ttu-id="92dab-119">Execute Olá comandos em um shell ou o prompt de comando na pasta Olá que contém os pacotes necessários do tooinstall Olá esses arquivos a seguir e, em seguida, execute o aplicativo de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="92dab-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="92dab-120">Observe a telemetria dinâmica em ação</span><span class="sxs-lookup"><span data-stu-id="92dab-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="92dab-121">painel Olá mostra a telemetria de temperatura e umidade Olá de dispositivos simuladas existentes de saudação:</span><span class="sxs-lookup"><span data-stu-id="92dab-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![Painel de padrão de saudação][image1]

<span data-ttu-id="92dab-123">Se você selecionar dispositivo simulado do Node. js Olá que você executou na seção anterior hello, consulte temperatura, umidade e telemetria temperatura externa:</span><span class="sxs-lookup"><span data-stu-id="92dab-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Adicionar painel de toohello temperatura externa][image2]

<span data-ttu-id="92dab-125">solução de monitoramento remoto Olá automaticamente detecta Olá adicionais temperatura externa telemetria tipo e o adiciona toohello gráfico no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="92dab-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png