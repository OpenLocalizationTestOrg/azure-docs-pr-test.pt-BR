## <a name="create-a-device-identity"></a><span data-ttu-id="175bb-101">Criar uma identidade do dispositivo</span><span class="sxs-lookup"><span data-stu-id="175bb-101">Create a device identity</span></span>

<span data-ttu-id="175bb-102">Nesta seção, você use Olá [portal do Azure] [ lnk-azure-portal] toocreate uma identidade de dispositivo no registro de identidade Olá em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="175bb-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="175bb-103">Um dispositivo não pode se conectar a tooIoT hub, a menos que ele tenha uma entrada no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="175bb-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="175bb-104">Para obter mais informações, consulte a seção de "Registro de identidade" de saudação do hello [guia do desenvolvedor de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="175bb-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="175bb-105">Olá **dispositivo Explorer** Olá o portal ajuda a você gerar uma identificação de dispositivo exclusivo e uma chave que seu dispositivo possa usar tooidentify em si, quando ele se conecta tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="175bb-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="175bb-106">As IDs de Dispositivo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="175bb-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="175bb-107">Verifique se você está conectado no toohello [portal do Azure][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="175bb-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="175bb-108">No hello Jumpbar, clique em **todos os recursos** e encontrar seu recurso de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="175bb-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Navegue tooyour Iot hub][img-find-iothub]

1. <span data-ttu-id="175bb-110">Quando o recurso de hub IoT é aberto, clique em Olá **dispositivo Explorer** ferramenta e, em seguida, clique em **adicionar** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="175bb-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="175bb-111">Forneça nome Olá para o novo dispositivo, como **myDeviceId**e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="175bb-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![Criar identidade do dispositivo no portal][img-create-device]

   <span data-ttu-id="175bb-113">Isso cria uma nova identidade do dispositivo para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="175bb-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="175bb-114">Em Olá **dispositivo Explorer**da lista de dispositivos, clique em dispositivo Olá recém-criado e anote Olá **cadeia de caracteres de Conexão---chave primária**.</span><span class="sxs-lookup"><span data-stu-id="175bb-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![Cadeia de conexão de dispositivo][img-connection-string]

> [!NOTE]
> <span data-ttu-id="175bb-116">Olá registro de identidade de IoT Hub armazena apenas o hub IoT toohello de proteger o acesso do dispositivo identidades tooenable.</span><span class="sxs-lookup"><span data-stu-id="175bb-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="175bb-117">Ele armazena toouse IDs e chaves de dispositivo como credenciais de segurança e um sinalizador habilitado/desabilitado que você pode usar o acesso de toodisable para um dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="175bb-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="175bb-118">Se seu aplicativo precisa toostore outros metadados específicos do dispositivo, ele deve usar um repositório específico do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="175bb-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="175bb-119">Para saber mais, confira [Guia de Desenvolvedor do Hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="175bb-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

