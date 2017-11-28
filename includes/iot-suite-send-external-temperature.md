## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="01dce-101">Configurar o dispositivo Node.js simulado</span><span class="sxs-lookup"><span data-stu-id="01dce-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="01dce-102">No painel de monitoramento remoto, clique em **+ Adicionar um dispositivo** e adicione um *dispositivo personalizado*.</span><span class="sxs-lookup"><span data-stu-id="01dce-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="01dce-103">Anote o nome de host do Hub IoT, id do dispositivo e chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="01dce-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="01dce-104">Você precisará deles mais tarde neste tutorial ao preparar o aplicativo cliente de dispositivo remote_monitoring.js.</span><span class="sxs-lookup"><span data-stu-id="01dce-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="01dce-105">Certifique-se de que o Node.js versão 0.12.x ou posterior esteja instalado no computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="01dce-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="01dce-106">Execute `node --version` em um prompt de comando ou em um shell para verificar a versão.</span><span class="sxs-lookup"><span data-stu-id="01dce-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="01dce-107">Para obter informações sobre como usar um gerenciador de pacotes para instalar o Node.js no Linux, confira [Instalação do Node.js por meio do gerenciador de pacotes][node-linux].</span><span class="sxs-lookup"><span data-stu-id="01dce-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="01dce-108">Após a instalação do Node.js, clone a versão mais recente do repositório [azure-iot-sdks][lnk-github-repo] em seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="01dce-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="01dce-109">Sempre use a ramificação **mestre** para a versão mais recente das bibliotecas e exemplos.</span><span class="sxs-lookup"><span data-stu-id="01dce-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="01dce-110">Em sua cópia local do repositório [azure-iot-sdks][lnk-github-repo], copie os dois arquivos a seguir da pasta node/device/samples em uma pasta vazia em seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="01dce-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="01dce-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="01dce-111">packages.json</span></span>
   * <span data-ttu-id="01dce-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="01dce-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="01dce-113">Abra o arquivo remote_monitoring.js e procure a seguinte definição de variável:</span><span class="sxs-lookup"><span data-stu-id="01dce-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="01dce-114">Substitua a **[cadeia de conexão de dispositivo do Hub IoT]** pela cadeia de conexão do seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="01dce-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="01dce-115">Use os valores de seu nome de host do Hub IoT, ID do dispositivo e chave de dispositivo que você anotou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="01dce-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="01dce-116">Uma cadeia de conexão do dispositivo tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="01dce-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="01dce-117">Se o nome de host do Hub IoT for **contoso** e a ID de dispositivo for **mydevice**, a cadeia de conexão se parecerá com este código:</span><span class="sxs-lookup"><span data-stu-id="01dce-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Salve o arquivo. <span data-ttu-id="01dce-119">Execute os seguintes comandos em um shell ou prompt de comando na pasta que contém os arquivos para instalar os pacotes necessários e, em seguida, execute o aplicativo de exemplo:</span><span class="sxs-lookup"><span data-stu-id="01dce-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="01dce-120">Observe a telemetria dinâmica em ação</span><span class="sxs-lookup"><span data-stu-id="01dce-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="01dce-121">O painel mostra a telemetria de temperatura e umidade dos dispositivos existentes simulados:</span><span class="sxs-lookup"><span data-stu-id="01dce-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![O painel padrão][image1]

<span data-ttu-id="01dce-123">Se você selecionar dispositivo simulado Node.js executado na seção anterior, verá a telemetria de temperatura, umidade e temperatura externa:</span><span class="sxs-lookup"><span data-stu-id="01dce-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Adicionar temperatura externa ao painel][image2]

<span data-ttu-id="01dce-125">A solução de monitoramento remoto detecta automaticamente o tipo de telemetria adicional de temperatura externa e o adiciona ao gráfico no painel.</span><span class="sxs-lookup"><span data-stu-id="01dce-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png