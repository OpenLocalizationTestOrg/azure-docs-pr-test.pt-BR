> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1a8e-101">C em Windows</span><span class="sxs-lookup"><span data-stu-id="f1a8e-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="f1a8e-102">C em Linux</span><span class="sxs-lookup"><span data-stu-id="f1a8e-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="f1a8e-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="f1a8e-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="f1a8e-104">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="f1a8e-104">Scenario overview</span></span>
<span data-ttu-id="f1a8e-105">Nesse cenário, você cria um dispositivo que envia Olá toohello telemetria de monitoramento remoto a seguir [pré-configurado solução][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="f1a8e-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="f1a8e-106">Temperatura externa</span><span class="sxs-lookup"><span data-stu-id="f1a8e-106">External temperature</span></span>
* <span data-ttu-id="f1a8e-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="f1a8e-107">Internal temperature</span></span>
* <span data-ttu-id="f1a8e-108">Umidade</span><span class="sxs-lookup"><span data-stu-id="f1a8e-108">Humidity</span></span>

<span data-ttu-id="f1a8e-109">Para simplificar, código de saudação no dispositivo hello gera valores de exemplo, mas recomendamos exemplo hello tooextend conectar sensores real tooyour dispositivo e enviar telemetria real.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="f1a8e-110">dispositivo Olá também é capaz de toorespond toomethods invocada a partir do painel de solução de saudação e desejado valores de propriedade definidos no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="f1a8e-111">toocomplete neste tutorial, você precisa de uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="f1a8e-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f1a8e-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="f1a8e-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f1a8e-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f1a8e-114">Before you start</span></span>
<span data-ttu-id="f1a8e-115">Antes de escrever qualquer código para o seu dispositivo, você precisa provisionar a solução pré-configurada de monitoramento remoto e provisionar um novo dispositivo personalizado nessa solução.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f1a8e-116">Provisionar sua solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="f1a8e-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="f1a8e-117">dispositivo Olá criado por você neste tutorial envia a instância de saudação tooan de dados [monitoramento remoto] [ lnk-remote-monitoring] pré-configurado de solução.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="f1a8e-118">Se você já não tiver provisionado Olá solução pré-configurada em sua conta do Azure de monitoramento remoto, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1a8e-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="f1a8e-119">Em Olá <https://www.azureiotsuite.com/> , clique em  **+**  toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="f1a8e-120">Clique em **selecione** em Olá **monitoramento remoto** painel toocreate sua solução.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="f1a8e-121">Em hello **criar monitoramento remoto solução** , insira um **nome da solução** de sua escolha, selecione Olá **região** você deseja toodeploy para e selecione saudação do Azure assinatura toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="f1a8e-122">Clique em **Criar solução**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="f1a8e-123">Aguarde até que a saudação processo de provisionamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="f1a8e-124">soluções de Olá pré-configurado usam os serviços do Azure faturáveis.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="f1a8e-125">Certifique-se de que tooremove Olá solução pré-configurada de sua assinatura, quando você tiver realizado tooavoid quaisquer encargos desnecessários.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="f1a8e-126">Você pode remover completamente uma solução pré-configurada de sua assinatura visitando Olá <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="f1a8e-127">Quando concluir a saudação processo para Olá remota de solução de monitoramento de provisionamento, clique em **iniciar** tooopen painel de solução de saudação em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Painel da solução][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="f1a8e-129">Configurar seu dispositivo no hello remota de solução de monitoramento</span><span class="sxs-lookup"><span data-stu-id="f1a8e-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="f1a8e-130">Se você já configurou um dispositivo em sua solução, poderá ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="f1a8e-131">Você precisa ter credenciais de dispositivo de saudação do tooknow quando você cria o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="f1a8e-132">Para uma solução de toohello pré-configurado de tooconnect do dispositivo, ele deve se identificar tooIoT Hub usando credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="f1a8e-133">Você pode recuperar credenciais do dispositivo de saudação do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="f1a8e-134">Você pode incluir credenciais do dispositivo Olá em seu aplicativo cliente posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="f1a8e-135">tooadd uma solução de monitoramento remoto do tooyour dispositivo, Olá completo a seguir as etapas no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="f1a8e-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="f1a8e-136">No hello canto inferior esquerdo do painel do hello, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Adicionar um dispositivo][1]
2. <span data-ttu-id="f1a8e-138">Em Olá **dispositivo personalizado** do painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Adicionar um dispositivo personalizado][2]
3. <span data-ttu-id="f1a8e-140">Escolha **Deixe-me definir minha própria ID de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="f1a8e-141">Insira uma ID de dispositivo como **meudispositivo**, clique em **verificar ID** tooverify esse nome não está em uso e, em seguida, clique em **criar** tooprovision dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Adicionar ID do dispositivo][3]
4. <span data-ttu-id="f1a8e-143">Tornar um dispositivo de saudação de Observação credenciais (ID do dispositivo, nome de host de Hub IoT e chave do dispositivo).</span><span class="sxs-lookup"><span data-stu-id="f1a8e-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="f1a8e-144">Seu aplicativo cliente precisa de solução de monitoramento remoto toohello de tooconnect esses valores.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="f1a8e-145">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-145">Then click **Done**.</span></span>
   
    ![Exibir credenciais do dispositivo][4]
5. <span data-ttu-id="f1a8e-147">Selecione o dispositivo na lista de dispositivos de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="f1a8e-148">Em seguida, no hello **detalhes do dispositivo** do painel, clique em **Ativar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="f1a8e-149">status de saudação do seu dispositivo agora é **executando**.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="f1a8e-150">solução de monitoramento remoto Olá agora pode receber telemetria do seu dispositivo e chamar métodos no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1a8e-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/