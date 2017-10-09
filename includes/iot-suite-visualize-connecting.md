## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="7e789-101">Telemetria de dispositivo de exibição no painel de saudação</span><span class="sxs-lookup"><span data-stu-id="7e789-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="7e789-102">Painel de saudação em Olá habilita solução telemetria Olá tooview seus dispositivos enviam tooIoT Hub de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="7e789-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="7e789-103">No navegador, toohello retorno remoto solução painel de monitoramento, clique em **dispositivos** em Olá painel esquerdo toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="7e789-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="7e789-104">Em Olá **lista de dispositivos**, você verá que o status de saudação do dispositivo é **executando**.</span><span class="sxs-lookup"><span data-stu-id="7e789-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="7e789-105">Se não estiver, clique em **Ativar dispositivo** em Olá **detalhes do dispositivo** painel.</span><span class="sxs-lookup"><span data-stu-id="7e789-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Exibir status do dispositivo][18]
3. <span data-ttu-id="7e789-107">Clique em **painel** tooreturn toohello painel, selecione seu dispositivo no hello **tooView dispositivo** suspensa tooview sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="7e789-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="7e789-108">Telemetria de saudação do aplicativo de exemplo hello é 50 unidades de temperatura interna, 55 unidades de temperatura externa e 50 unidades para umidade.</span><span class="sxs-lookup"><span data-stu-id="7e789-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Exibir telemetria de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="7e789-110">Invocar um método no seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="7e789-110">Invoke a method on your device</span></span>
<span data-ttu-id="7e789-111">painel Olá na solução de monitoramento remoto Olá permite tooinvoke métodos em seus dispositivos por meio de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7e789-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="7e789-112">Por exemplo, no hello solução de monitoramento remoto, você pode invocar toosimulate um método que a reinicialização de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e789-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="7e789-113">Olá remoto monitoramento solução painel, clique em **dispositivos** em Olá painel esquerdo toonavigate toohello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="7e789-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="7e789-114">Clique em **ID do dispositivo** para seu dispositivo no hello **lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="7e789-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="7e789-115">Em Olá **detalhes do dispositivo** do painel, clique em **métodos**.</span><span class="sxs-lookup"><span data-stu-id="7e789-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Métodos do dispositivo][13]
4. <span data-ttu-id="7e789-117">Em Olá **método** lista suspensa, selecione **InitiateFirmwareUpdate**e, em seguida, em **FWPACKAGEURI** insira uma URL fictícia.</span><span class="sxs-lookup"><span data-stu-id="7e789-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="7e789-118">Clique em **invocar o método** toocall método hello dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="7e789-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Invocar um método do dispositivo][14]
   

5. <span data-ttu-id="7e789-120">Você verá uma mensagem no console de saudação executar o código do dispositivo quando o dispositivo Olá manipula método hello.</span><span class="sxs-lookup"><span data-stu-id="7e789-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="7e789-121">resultados de saudação do método hello são adicionados toohello histórico no portal de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="7e789-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Exibir o histórico do método][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="7e789-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e789-123">Next steps</span></span>
<span data-ttu-id="7e789-124">artigo Olá [soluções pré-configuradas de personalização] [ lnk-customize] descreve algumas maneiras que você pode estender esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="7e789-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="7e789-125">Extensões possíveis incluem usar sensores reais e implementar comandos adicionais.</span><span class="sxs-lookup"><span data-stu-id="7e789-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="7e789-126">Você pode aprender mais sobre Olá [permissões no site do hello azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="7e789-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
