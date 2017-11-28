## <a name="view-the-telemetry"></a><span data-ttu-id="c1a7d-101">Exibir a Telemetria</span><span class="sxs-lookup"><span data-stu-id="c1a7d-101">View the telemetry</span></span>

<span data-ttu-id="c1a7d-102">O Raspberry Pi agora está enviando a telemetria para a solução de monitoramento remota.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="c1a7d-103">Você pode exibir a telemetria no painel de solução.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="c1a7d-104">Você também pode enviar mensagens para o Raspberry Pi a partir do painel da solução.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="c1a7d-105">Navegue para o painel da solução.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="c1a7d-106">Selecione o dispositivo na lista suspensa **Dispositivo para exibição**.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="c1a7d-107">A telemetria do Raspberry Pi é exibida no painel.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Exibir a telemetria do Raspberry Pi][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="c1a7d-109">Atuar no dispositivo</span><span class="sxs-lookup"><span data-stu-id="c1a7d-109">Act on the device</span></span>

<span data-ttu-id="c1a7d-110">No painel de solução, você pode invocar métodos em seu Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="c1a7d-111">Quando o Raspberry Pi se conecta a solução de monitoramento remota, ele envia informações sobre os métodos que ele suporta.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="c1a7d-112">No painel de solução, clique em **Dispositivos** para visitar a página **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="c1a7d-113">Selecione seu Raspberry Pi na **Lista de Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="c1a7d-114">Depois, escolha **Métodos**:</span><span class="sxs-lookup"><span data-stu-id="c1a7d-114">Then choose **Methods**:</span></span>

    ![Listar dispositivos no painel][img-list-devices]

- <span data-ttu-id="c1a7d-116">Na página **Invocar Método** escolha **LightBlink** na lista suspensa **Método**.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="c1a7d-117">Escolha **InvokeMethod**.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="c1a7d-118">O simulator imprime uma mensagem no console do Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="c1a7d-119">O aplicativo no Raspberry Pi envia uma confirmação de volta para o painel da solução:</span><span class="sxs-lookup"><span data-stu-id="c1a7d-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![Mostrar o histórico do método][img-method-history]

- <span data-ttu-id="c1a7d-121">Você pode ligar e desligar o LED usando o método **ChangeLightStatus** com **LightStatusValue** definido como **1** para ligar ou **0** para desligar.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="c1a7d-122">Se você deixar a solução de monitoramento remoto em execução em sua conta do Azure, você receberá uma cobrança pelo tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="c1a7d-123">Para saber mais sobre como reduzir o consumo durante a execução da solução de monitoramento remoto, confira [Configuração de soluções pré-configuradas do Azure IoT Suite para fins de demonstração][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="c1a7d-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="c1a7d-124">Exclua a solução pré-configurada de sua conta do Azure quando terminar de usá-la.</span><span class="sxs-lookup"><span data-stu-id="c1a7d-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md