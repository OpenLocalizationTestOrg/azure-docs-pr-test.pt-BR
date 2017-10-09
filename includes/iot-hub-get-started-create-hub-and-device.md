## <a name="create-an-iot-hub"></a><span data-ttu-id="868ce-101">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="868ce-101">Create an IoT hub</span></span>

1. <span data-ttu-id="868ce-102">Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **Internet das coisas** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="868ce-102">In hello [Azure portal](https://portal.azure.com/), click **New** > **Internet of Things** > **IoT Hub**.</span></span>

   ![Criar um hub IoT em Olá portal do Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. <span data-ttu-id="868ce-104">Em Olá **hub IoT** painel, digite Olá informações para o hub IoT a seguir:</span><span class="sxs-lookup"><span data-stu-id="868ce-104">In hello **IoT hub** pane, enter hello following information for your IoT hub:</span></span>

     <span data-ttu-id="868ce-105">**Nome**: Insira nome de saudação do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="868ce-105">**Name**: Enter hello name of your IoT hub.</span></span> <span data-ttu-id="868ce-106">Se o nome de saudação for válido, uma marca de seleção verde é exibida.</span><span class="sxs-lookup"><span data-stu-id="868ce-106">If hello name you enter is valid, a green check mark appears.</span></span>

     <span data-ttu-id="868ce-107">**Escala e preço**: selecione Olá **F1 - livre** camada.</span><span class="sxs-lookup"><span data-stu-id="868ce-107">**Pricing and scale tier**: Select hello **F1 - Free** tier.</span></span> <span data-ttu-id="868ce-108">Essa opção é suficiente para esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="868ce-108">This option is sufficient for this demo.</span></span> <span data-ttu-id="868ce-109">Para obter mais informações, consulte Olá [camada de preços e escala](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="868ce-109">For more information, see hello [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

     <span data-ttu-id="868ce-110">**Grupo de recursos**: criar um hub IoT de saudação do recurso grupo toohost ou use uma existente.</span><span class="sxs-lookup"><span data-stu-id="868ce-110">**Resource group**: Create a resource group toohost hello IoT hub or use an existing one.</span></span> <span data-ttu-id="868ce-111">Para obter mais informações, consulte [grupos de recurso de uso toomanage seus recursos do Azure](../articles/azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="868ce-111">For more information, see [Use resource groups toomanage your Azure resources](../articles/azure-resource-manager/resource-group-portal.md).</span></span>

     <span data-ttu-id="868ce-112">**Local**: selecione Olá tooyou mais próximo do local em que o hub IoT de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="868ce-112">**Location**: Select hello closest location tooyou where hello IoT hub is created.</span></span>

     <span data-ttu-id="868ce-113">**PIN toodashboard**: Selecione esta opção para o hub de IoT tooyour fácil acesso do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="868ce-113">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Insira informações toocreate seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. <span data-ttu-id="868ce-115">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="868ce-115">Click **Create**.</span></span> <span data-ttu-id="868ce-116">O hub IoT levaria toocreate de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="868ce-116">Your IoT hub might take a few minutes toocreate.</span></span> <span data-ttu-id="868ce-117">Você pode ver o progresso na Olá **notificações** painel.</span><span class="sxs-lookup"><span data-stu-id="868ce-117">You can see progress in hello **Notifications** pane.</span></span>

   ![Ver as notificações de andamento para o hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. <span data-ttu-id="868ce-119">Depois que o hub IoT é criado, clique no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="868ce-119">After your IoT hub is created, click it on hello dashboard.</span></span> <span data-ttu-id="868ce-120">Anote Olá **Hostname**e, em seguida, clique em **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="868ce-120">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>

   ![Obter nome de host de saudação do seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. <span data-ttu-id="868ce-122">Em Olá **políticas de acesso compartilhado** painel, clique em Olá **iothubowner** política e, em seguida, copiar e anotado da saudação **cadeia de caracteres de Conexão** do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="868ce-122">In hello **Shared access policies** pane, click hello **iothubowner** policy, and then copy and make a note of hello **Connection string** of your IoT hub.</span></span> <span data-ttu-id="868ce-123">Para obter mais informações, consulte [tooIoT de acesso de controle Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span><span class="sxs-lookup"><span data-stu-id="868ce-123">For more information, see [Control access tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).</span></span>

> [!NOTE] 
<span data-ttu-id="868ce-124">Você não precisará dessa cadeia de conexão iothubowner para este tutorial de configuração.</span><span class="sxs-lookup"><span data-stu-id="868ce-124">You will not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="868ce-125">No entanto, você pode precisar dele para alguns tutoriais Olá sobre diferentes cenários de IoT depois de concluir esta instalação.</span><span class="sxs-lookup"><span data-stu-id="868ce-125">However, you may need it for some of hello tutorials on different IoT scenarios after you complete this set-up.</span></span>

   ![Obter sua cadeia de conexão do Hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a><span data-ttu-id="868ce-127">Registrar um dispositivo no hub IoT de saudação do seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="868ce-127">Register a device in hello IoT hub for your device</span></span>

1. <span data-ttu-id="868ce-128">Em Olá [portal do Azure](https://portal.azure.com/), abra seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="868ce-128">In hello [Azure portal](https://portal.azure.com/), open your IoT hub.</span></span>

2. <span data-ttu-id="868ce-129">Clique em **Gerenciador de Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="868ce-129">Click **Device Explorer**.</span></span>
3. <span data-ttu-id="868ce-130">No painel de saudação do Gerenciador de dispositivos, clique em **adicionar** tooadd um hub do dispositivo tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="868ce-130">In hello Device Explorer pane, click **Add** tooadd a device tooyour IoT hub.</span></span> <span data-ttu-id="868ce-131">Em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="868ce-131">Then do hello following:</span></span>

   <span data-ttu-id="868ce-132">**ID do dispositivo**: insira a ID de saudação do novo dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="868ce-132">**Device ID**: Enter hello ID of hello new device.</span></span> <span data-ttu-id="868ce-133">As IDs de Dispositivo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="868ce-133">Device IDs are case sensitive.</span></span>

   <span data-ttu-id="868ce-134">**Tipo de Autenticação**: selecione a **Chave Simétrica**.</span><span class="sxs-lookup"><span data-stu-id="868ce-134">**Authentication Type**: Select **Symmetric Key**.</span></span>

   <span data-ttu-id="868ce-135">**Gerar Chaves Automaticamente**: marque essa caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="868ce-135">**Auto Generate Keys**: Select this check box.</span></span>

   <span data-ttu-id="868ce-136">**Conecte-se o dispositivo tooIoT Hub**: clique em **habilitar**.</span><span class="sxs-lookup"><span data-stu-id="868ce-136">**Connect device tooIoT Hub**: Click **Enable**.</span></span>

   ![Adicionar um dispositivo no hello Gerenciador de dispositivo de seu hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. <span data-ttu-id="868ce-138">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="868ce-138">Click **Save**.</span></span>
5. <span data-ttu-id="868ce-139">Após a criação de dispositivo hello, abrir o dispositivo de saudação em hello **dispositivo Explorer** painel.</span><span class="sxs-lookup"><span data-stu-id="868ce-139">After hello device is created, open hello device in hello **Device Explorer** pane.</span></span>
6. <span data-ttu-id="868ce-140">Anote a chave primária Olá de cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="868ce-140">Make a note of hello primary key of hello connection string.</span></span>

   ![Obter cadeia de caracteres de conexão de dispositivo Olá](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
