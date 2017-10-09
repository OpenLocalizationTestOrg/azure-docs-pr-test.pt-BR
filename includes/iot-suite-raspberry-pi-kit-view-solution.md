## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="63b9e-101">Painel de solução de saudação de View</span><span class="sxs-lookup"><span data-stu-id="63b9e-101">View hello solution dashboard</span></span>

<span data-ttu-id="63b9e-102">Painel de solução de saudação permite toomanage solução de saudação implantada.</span><span class="sxs-lookup"><span data-stu-id="63b9e-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="63b9e-103">Por exemplo, você pode exibir telemetria, adicionar dispositivos e invocar métodos.</span><span class="sxs-lookup"><span data-stu-id="63b9e-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="63b9e-104">Quando Olá provisionamento for concluído e lado a lado para sua solução pré-configurada Olá indica **pronto**, escolha **iniciar** tooopen seu portal de solução de monitoramento remoto em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="63b9e-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar a solução de saudação pré-configurado][img-launch-solution]

1. <span data-ttu-id="63b9e-106">Por padrão, o portal de solução Olá mostra Olá *painel*.</span><span class="sxs-lookup"><span data-stu-id="63b9e-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="63b9e-107">Você pode navegar tooother áreas do portal de solução hello usando o menu de saudação no lado esquerdo de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="63b9e-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Painel de solução pré-configurada de monitoramento remoto][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="63b9e-109">Adicionar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="63b9e-109">Add a device</span></span>

<span data-ttu-id="63b9e-110">Para uma solução de toohello pré-configurado de tooconnect do dispositivo, ele deve se identificar tooIoT Hub usando credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="63b9e-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="63b9e-111">Você pode recuperar credenciais do dispositivo de saudação do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="63b9e-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="63b9e-112">Você pode incluir credenciais do dispositivo Olá em seu aplicativo cliente posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="63b9e-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="63b9e-113">Se você ainda não o fez, adicione uma solução de monitoramento remoto do tooyour personalizada no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="63b9e-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="63b9e-114">Olá completo seguindo as etapas no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="63b9e-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="63b9e-115">No hello canto inferior esquerdo do painel do hello, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![Adicionar um dispositivo][1]

1. <span data-ttu-id="63b9e-117">Em Olá **dispositivo personalizado** do painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![Adicionar um dispositivo personalizado][2]

1. <span data-ttu-id="63b9e-119">Escolha **Deixe-me definir minha própria ID de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="63b9e-120">Insira uma ID de dispositivo como **rasppi**, clique em **verificar ID** tooverify você ainda não tiver usado o nome da saudação em sua solução e, em seguida, clique em **criar** tooprovision dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="63b9e-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![Adicionar ID do dispositivo][3]

1. <span data-ttu-id="63b9e-122">Tornar um dispositivo de saudação Observação credenciais (**ID do dispositivo**, **IoT Hub Hostname**, e **chave dispositivo**).</span><span class="sxs-lookup"><span data-stu-id="63b9e-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="63b9e-123">O aplicativo cliente em Olá framboesa Pi precisa toohello de tooconnect esses valores remotas de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="63b9e-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="63b9e-124">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-124">Then click **Done**.</span></span>

    ![Exibir credenciais do dispositivo][4]

1. <span data-ttu-id="63b9e-126">Selecione o dispositivo na lista de dispositivos de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="63b9e-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="63b9e-127">Em seguida, no hello **detalhes do dispositivo** do painel, clique em **Ativar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="63b9e-128">status de saudação do seu dispositivo agora é **executando**.</span><span class="sxs-lookup"><span data-stu-id="63b9e-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="63b9e-129">solução de monitoramento remoto Olá agora pode receber telemetria do seu dispositivo e chamar métodos no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="63b9e-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png