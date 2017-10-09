## <a name="create-an-iot-hub"></a><span data-ttu-id="fba6f-101">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="fba6f-101">Create an IoT hub</span></span>
<span data-ttu-id="fba6f-102">Crie um hub IoT para sua tooconnect de aplicativo do dispositivo simulado para.</span><span class="sxs-lookup"><span data-stu-id="fba6f-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="fba6f-103">Olá etapas a seguir mostram como toocomplete essa tarefa por usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fba6f-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="fba6f-104">Entrar toohello [portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="fba6f-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="fba6f-105">No hello Jumpbar, clique em **novo** > **Internet das coisas** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Barra de Navegação do portal do Azure][1]
1. <span data-ttu-id="fba6f-107">Em Olá **hub IoT** folha, escolha a configuração Olá para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fba6f-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Folha Hub IoT][2]
   
   1. <span data-ttu-id="fba6f-109">Em Olá **nome** , digite um nome para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fba6f-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="fba6f-110">Se hello **nome** é válido e disponível, uma marca de seleção verde é exibido no hello **nome** caixa.</span><span class="sxs-lookup"><span data-stu-id="fba6f-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="fba6f-111">Selecione um [tipo de preço e de dimensionamento][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="fba6f-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="fba6f-112">Este tutorial não requer uma camada específica.</span><span class="sxs-lookup"><span data-stu-id="fba6f-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="fba6f-113">Para este tutorial, use Olá F1 grátis.</span><span class="sxs-lookup"><span data-stu-id="fba6f-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="fba6f-114">Em **Grupo de recursos**, crie um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="fba6f-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="fba6f-115">Para obter mais informações, consulte [usando o recurso de grupos de toomanage os recursos do Azure][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="fba6f-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="fba6f-116">Em **local**, selecione Olá local toohost seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fba6f-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="fba6f-117">Para este tutorial, escolha o local mais próximo.</span><span class="sxs-lookup"><span data-stu-id="fba6f-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="fba6f-118">Quando você tiver escolhido as opções de configuração do hub IoT, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="fba6f-119">Pode levar alguns minutos para o Azure toocreate seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fba6f-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="fba6f-120">status de saudação toocheck, você pode monitorar o progresso de Olá Olá quadro inicial ou no painel de notificações de saudação.</span><span class="sxs-lookup"><span data-stu-id="fba6f-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Novo status do Hub IoT do Azure][3]
1. <span data-ttu-id="fba6f-122">Quando o hub IoT de saudação foi criado com êxito, clique em novo bloco Olá para o hub IoT na folha de Olá Olá tooopen portal do Azure para o hub IoT da nova hello.</span><span class="sxs-lookup"><span data-stu-id="fba6f-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="fba6f-123">Anote Olá **Hostname**e, em seguida, clique em **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Nova folha Hub IoT][4]
1. <span data-ttu-id="fba6f-125">Em Olá **políticas de acesso compartilhado** folha, clique em Olá **iothubowner** política e, em seguida, copiar e anote Olá cadeia de caracteres de conexão de IoT Hub Olá **iothubowner** folha.</span><span class="sxs-lookup"><span data-stu-id="fba6f-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="fba6f-126">Para obter mais informações, consulte [controle de acesso] [ lnk-access-control] em hello "Guia do desenvolvedor do IoT Hub."</span><span class="sxs-lookup"><span data-stu-id="fba6f-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![Folha Políticas de acesso compartilhado][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
