## <a name="view-hello-telemetry"></a><span data-ttu-id="4767e-101">Telemetria de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="4767e-101">View hello telemetry</span></span>

<span data-ttu-id="4767e-102">Olá framboesa Pi agora está enviando a solução de monitoramento remoto de toohello telemetria.</span><span class="sxs-lookup"><span data-stu-id="4767e-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="4767e-103">Você pode exibir a telemetria de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4767e-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="4767e-104">Você também pode enviar mensagens tooyour framboesa Pi no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4767e-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="4767e-105">Navegue toohello painel de solução.</span><span class="sxs-lookup"><span data-stu-id="4767e-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="4767e-106">Selecione o dispositivo em Olá **tooView dispositivo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="4767e-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="4767e-107">Telemetria de saudação do hello framboesa Pi exibe no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="4767e-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Telemetria de exibição de saudação framboesa Pi][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="4767e-109">Agir no dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="4767e-109">Act on hello device</span></span>

<span data-ttu-id="4767e-110">No painel de solução Olá, você pode chamar métodos em seu framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="4767e-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="4767e-111">Quando Olá framboesa Pi conecta-se a solução de monitoramento remoto toohello, ele envia informações sobre métodos de saudação oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="4767e-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="4767e-112">No painel de solução de saudação, clique em **dispositivos** toovisit Olá **dispositivos** página.</span><span class="sxs-lookup"><span data-stu-id="4767e-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="4767e-113">Selecione o Pi framboesa no hello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="4767e-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="4767e-114">Depois, escolha **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="4767e-114">Then choose **Methods**:</span></span>

    ![Listar dispositivos no painel][img-list-devices]

- <span data-ttu-id="4767e-116">Em Olá **invocar o método** escolha **LightBlink** em Olá **método** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="4767e-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="4767e-117">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="4767e-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="4767e-118">Olá LED conectado toohello que framboesa Pi pisca várias vezes.</span><span class="sxs-lookup"><span data-stu-id="4767e-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="4767e-119">aplicativo Olá Olá framboesa Pi envia um painel de solução de backup toohello confirmação:</span><span class="sxs-lookup"><span data-stu-id="4767e-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![Mostrar o histórico do método][img-method-history]

- <span data-ttu-id="4767e-121">Você pode alternar LED hello e desativar usando Olá **ChangeLightStatus** método com um **LightStatusValue** definido muito**1** para em ou **0** para off.</span><span class="sxs-lookup"><span data-stu-id="4767e-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="4767e-122">Se você deixar Olá remoto em execução em sua conta do Azure de solução de monitoramento, você será cobrado por tempo de saudação que é executado.</span><span class="sxs-lookup"><span data-stu-id="4767e-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="4767e-123">Para obter mais informações sobre como reduzir o consumo durante a saudação execuções de solução de monitoramento remoto, consulte [Configurando o Azure IoT Suite pré-configurado soluções para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="4767e-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="4767e-124">Exclua solução Olá pré-configurado de sua conta do Azure quando você tiver terminado de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="4767e-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md