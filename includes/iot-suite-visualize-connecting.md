## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="bc9cc-101">Exibir telemetria do dispositivo no painel</span><span class="sxs-lookup"><span data-stu-id="bc9cc-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="bc9cc-102">O painel da solução de monitoramento remoto permite que você exiba a telemetria que seus dispositivos enviam para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="bc9cc-103">Em seu navegador, retorne para o painel da solução de monitoramento remoto, clique em **Dispositivos** no painel esquerdo para navegar até a **Lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="bc9cc-104">Na **Lista de dispositivos**, você deve ver que o status de seu dispositivo agora é **Executando**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="bc9cc-105">Caso contrário, clique em **Habilitar Dispositivo** no painel de **Detalhes do Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Exibir status do dispositivo][18]
3. <span data-ttu-id="bc9cc-107">Clique em **Painel** para voltar ao painel, selecione seu dispositivo no menu suspenso **Dispositivo para Exibição** para exibir sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="bc9cc-108">A telemetria do aplicativo de exemplo é de 50 unidades de temperatura interna, 55 unidades de temperatura externa e 50 unidades de umidade.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Exibir telemetria de dispositivo][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="bc9cc-110">Invocar um método no seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="bc9cc-110">Invoke a method on your device</span></span>
<span data-ttu-id="bc9cc-111">O painel da solução de monitoramento remoto permite que você invoque métodos nos seus dispositivos através do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="bc9cc-112">Por exemplo, na solução de monitoramento remoto, você pode invocar um método para simular a reinicialização de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="bc9cc-113">No painel da solução de monitoramento remoto, clique em **Dispositivos** no painel esquerdo para navegar até a **Lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="bc9cc-114">Clique em **ID de dispositivo** para seu dispositivo na **Lista de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="bc9cc-115">No painel **Detalhes do dispositivo**, clique em **Métodos**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Métodos do dispositivo][13]
4. <span data-ttu-id="bc9cc-117">Na lista suspensa **Método**, selecione **InitiateFirmwareUpdate** e, em seguida, insira uma URL fictícia em **FWPACKAGEURI**.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="bc9cc-118">Clique em **Invocar Método** para chamar o método no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Invocar um método do dispositivo][14]
   

5. <span data-ttu-id="bc9cc-120">Você verá uma mensagem no console que está executando o código do dispositivo quando o dispositivo manipular o método.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="bc9cc-121">Os resultados do método serão adicionados ao histórico no portal da solução:</span><span class="sxs-lookup"><span data-stu-id="bc9cc-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Exibir o histórico do método][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="bc9cc-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc9cc-123">Next steps</span></span>
<span data-ttu-id="bc9cc-124">O artigo [Personalizando soluções pré-configuradas][lnk-customize] descreve algumas maneiras de estender este exemplo.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="bc9cc-125">Extensões possíveis incluem usar sensores reais e implementar comandos adicionais.</span><span class="sxs-lookup"><span data-stu-id="bc9cc-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="bc9cc-126">Você pode aprender mais sobre as [permissões no site azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="bc9cc-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
