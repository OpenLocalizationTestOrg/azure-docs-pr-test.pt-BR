## <a name="view-the-solution-dashboard"></a><span data-ttu-id="05359-101">Exibir o painel de solução</span><span class="sxs-lookup"><span data-stu-id="05359-101">View the solution dashboard</span></span>

<span data-ttu-id="05359-102">O painel de solução permite que você gerencie a solução implantada.</span><span class="sxs-lookup"><span data-stu-id="05359-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="05359-103">Por exemplo, você pode exibir telemetria, adicionar dispositivos e invocar métodos.</span><span class="sxs-lookup"><span data-stu-id="05359-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="05359-104">Quando o provisionamento for concluído e o bloco da solução pré-configurada indicar **Pronto**, escolha **Iniciar** para abrir o portal de solução de monitoramento remoto em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="05359-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar a solução pré-configurada][img-launch-solution]

1. <span data-ttu-id="05359-106">Por padrão, o portal de solução mostra o *painel*.</span><span class="sxs-lookup"><span data-stu-id="05359-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="05359-107">Navegue para outras áreas do portal de solução usando o menu ao lado esquerdo da página.</span><span class="sxs-lookup"><span data-stu-id="05359-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Painel de solução pré-configurada de monitoramento remoto][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="05359-109">Adicionar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="05359-109">Add a device</span></span>

<span data-ttu-id="05359-110">Para um dispositivo conectar-se à solução pré-configurada, ele deve identificar-se no Hub IoT usando credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="05359-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="05359-111">Você pode recuperar as credenciais do dispositivo no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="05359-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="05359-112">Você pode incluir as credenciais do dispositivo em seu aplicativo cliente posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="05359-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="05359-113">Para adicionar um dispositivo à sua solução de monitoramento remoto, realize as etapas a seguir no painel da solução:</span><span class="sxs-lookup"><span data-stu-id="05359-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="05359-114">No canto inferior esquerdo do painel, clique em **Adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="05359-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![Adicionar um dispositivo][1]

1. <span data-ttu-id="05359-116">No painel **Dispositivo Personalizado**, clique em **Adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="05359-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![Adicionar um dispositivo personalizado][2]

1. <span data-ttu-id="05359-118">Escolha **Deixe-me definir minha própria ID de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="05359-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="05359-119">Insira uma ID do Dispositivo como **device01**, clique em **Verificar ID** para verificar se você já não usou o nome na sua solução, em seguida, clique em **Criar** para provisionar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="05359-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![Adicionar ID do dispositivo][3]

1. <span data-ttu-id="05359-121">Anote as credenciais do dispositivo (**ID do dispositivo**, **Nome do host do Hub IoT** e **Chave do Dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="05359-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="05359-122">Seu aplicativo cliente no Intel NUC precisa desses valores para se conectar à solução de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="05359-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="05359-123">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="05359-123">Then click **Done**.</span></span>

    ![Exibir credenciais do dispositivo][4]

1. <span data-ttu-id="05359-125">Selecione seu dispositivo na lista de dispositivos do painel da solução.</span><span class="sxs-lookup"><span data-stu-id="05359-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="05359-126">Em seguida, no painel **Detalhes do Dispositivo**, clique em **Habilitar Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="05359-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="05359-127">O status do seu dispositivo agora é **Executando**.</span><span class="sxs-lookup"><span data-stu-id="05359-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="05359-128">Agora a solução de monitoramento remoto poderá receber telemetria do seu dispositivo e invocar métodos nele.</span><span class="sxs-lookup"><span data-stu-id="05359-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png