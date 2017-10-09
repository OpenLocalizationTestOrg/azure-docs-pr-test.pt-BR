---
title: aaaConnect um dispositivo usando C em mbed | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em C em execução em um dispositivo mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="ccff2-103">Conecte-se a sua solução pré-configurada (mbed) de monitoramento remoto de toohello de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ccff2-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="ccff2-104">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="ccff2-104">Scenario overview</span></span>
<span data-ttu-id="ccff2-105">Nesse cenário, você cria um dispositivo que envia Olá toohello telemetria de monitoramento remoto a seguir [pré-configurado solução][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="ccff2-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="ccff2-106">Temperatura externa</span><span class="sxs-lookup"><span data-stu-id="ccff2-106">External temperature</span></span>
* <span data-ttu-id="ccff2-107">Temperatura interna</span><span class="sxs-lookup"><span data-stu-id="ccff2-107">Internal temperature</span></span>
* <span data-ttu-id="ccff2-108">Umidade</span><span class="sxs-lookup"><span data-stu-id="ccff2-108">Humidity</span></span>

<span data-ttu-id="ccff2-109">Para simplificar, código de saudação no dispositivo hello gera valores de exemplo, mas recomendamos exemplo hello tooextend conectar sensores real tooyour dispositivo e enviar telemetria real.</span><span class="sxs-lookup"><span data-stu-id="ccff2-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="ccff2-110">dispositivo Olá também é capaz de toorespond toomethods invocada a partir do painel de solução de saudação e desejado valores de propriedade definidos no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="ccff2-111">toocomplete neste tutorial, você precisa de uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccff2-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="ccff2-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ccff2-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ccff2-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="ccff2-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ccff2-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ccff2-114">Before you start</span></span>
<span data-ttu-id="ccff2-115">Antes de escrever qualquer código para o seu dispositivo, você precisa provisionar a solução pré-configurada de monitoramento remoto e provisionar um novo dispositivo personalizado nessa solução.</span><span class="sxs-lookup"><span data-stu-id="ccff2-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ccff2-116">Provisionar sua solução pré-configurada de monitoramento remoto</span><span class="sxs-lookup"><span data-stu-id="ccff2-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="ccff2-117">dispositivo Olá criado por você neste tutorial envia a instância de saudação tooan de dados [monitoramento remoto] [ lnk-remote-monitoring] pré-configurado de solução.</span><span class="sxs-lookup"><span data-stu-id="ccff2-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="ccff2-118">Se você já não tiver provisionado Olá solução pré-configurada em sua conta do Azure de monitoramento remoto, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccff2-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="ccff2-119">Em Olá <https://www.azureiotsuite.com/> , clique em  **+**  toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="ccff2-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="ccff2-120">Clique em **selecione** em Olá **monitoramento remoto** painel toocreate sua solução.</span><span class="sxs-lookup"><span data-stu-id="ccff2-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="ccff2-121">Em hello **criar monitoramento remoto solução** , insira um **nome da solução** de sua escolha, selecione Olá **região** você deseja toodeploy para e selecione saudação do Azure assinatura toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="ccff2-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="ccff2-122">Clique em **Criar solução**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="ccff2-123">Aguarde até que a saudação processo de provisionamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="ccff2-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="ccff2-124">soluções de Olá pré-configurado usam os serviços do Azure faturáveis.</span><span class="sxs-lookup"><span data-stu-id="ccff2-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="ccff2-125">Certifique-se de que tooremove Olá solução pré-configurada de sua assinatura, quando você tiver realizado tooavoid quaisquer encargos desnecessários.</span><span class="sxs-lookup"><span data-stu-id="ccff2-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="ccff2-126">Você pode remover completamente uma solução pré-configurada de sua assinatura visitando Olá <https://www.azureiotsuite.com/> página.</span><span class="sxs-lookup"><span data-stu-id="ccff2-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="ccff2-127">Quando concluir a saudação processo para Olá remota de solução de monitoramento de provisionamento, clique em **iniciar** tooopen painel de solução de saudação em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ccff2-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Painel da solução][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="ccff2-129">Configurar seu dispositivo no hello remota de solução de monitoramento</span><span class="sxs-lookup"><span data-stu-id="ccff2-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="ccff2-130">Se você já configurou um dispositivo em sua solução, poderá ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="ccff2-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="ccff2-131">Você precisa ter credenciais de dispositivo de saudação do tooknow quando você cria o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="ccff2-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="ccff2-132">Para uma solução de toohello pré-configurado de tooconnect do dispositivo, ele deve se identificar tooIoT Hub usando credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="ccff2-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="ccff2-133">Você pode recuperar credenciais do dispositivo de saudação do painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="ccff2-134">Você pode incluir credenciais do dispositivo Olá em seu aplicativo cliente posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ccff2-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ccff2-135">tooadd uma solução de monitoramento remoto do tooyour dispositivo, Olá completo a seguir as etapas no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="ccff2-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="ccff2-136">No hello canto inferior esquerdo do painel do hello, clique em **adicionar um dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Adicionar um dispositivo][1]
2. <span data-ttu-id="ccff2-138">Em Olá **dispositivo personalizado** do painel, clique em **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Adicionar um dispositivo personalizado][2]
3. <span data-ttu-id="ccff2-140">Escolha **Deixe-me definir minha própria ID de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ccff2-141">Insira uma ID de dispositivo como **meudispositivo**, clique em **verificar ID** tooverify esse nome não está em uso e, em seguida, clique em **criar** tooprovision dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Adicionar ID do dispositivo][3]
4. <span data-ttu-id="ccff2-143">Tornar um dispositivo de saudação de Observação credenciais (ID do dispositivo, nome de host de Hub IoT e chave do dispositivo).</span><span class="sxs-lookup"><span data-stu-id="ccff2-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="ccff2-144">Seu aplicativo cliente precisa de solução de monitoramento remoto toohello de tooconnect esses valores.</span><span class="sxs-lookup"><span data-stu-id="ccff2-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="ccff2-145">Em seguida, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-145">Then click **Done**.</span></span>
   
    ![Exibir credenciais do dispositivo][4]
5. <span data-ttu-id="ccff2-147">Selecione o dispositivo na lista de dispositivos de saudação no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="ccff2-148">Em seguida, no hello **detalhes do dispositivo** do painel, clique em **Ativar dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ccff2-149">status de saudação do seu dispositivo agora é **executando**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="ccff2-150">solução de monitoramento remoto Olá agora pode receber telemetria do seu dispositivo e chamar métodos no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="ccff2-151">Compilar e executar a solução de exemplo hello C</span><span class="sxs-lookup"><span data-stu-id="ccff2-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="ccff2-152">Olá, instruções a seguir descrevem as etapas de saudação para se conectar um [habilitado mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello de dispositivo remoto de solução de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="ccff2-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="ccff2-153">Conecte-se a rede de tooyour Olá mbed dispositivo e o computador desktop</span><span class="sxs-lookup"><span data-stu-id="ccff2-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="ccff2-154">Conecte Olá mbed dispositivo tooyour rede usando um cabo Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ccff2-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="ccff2-155">Esta etapa é necessária porque o aplicativo de exemplo hello requer acesso à internet.</span><span class="sxs-lookup"><span data-stu-id="ccff2-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="ccff2-156">Consulte [guia de Introdução ao mbed] [ lnk-mbed-getstarted] tooconnect mbed dispositivo tooyour área de trabalho do computador.</span><span class="sxs-lookup"><span data-stu-id="ccff2-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="ccff2-157">Se seu computador desktop que executam o Windows, consulte [configuração PC] [ lnk-mbed-pcconnect] tooconfigure dispositivo de mbed tooyour acesso à porta serial.</span><span class="sxs-lookup"><span data-stu-id="ccff2-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="ccff2-158">Criar um projeto de mbed e importar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="ccff2-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="ccff2-159">Siga estas etapas tooadd alguns projeto mbed de tooan de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ccff2-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="ccff2-160">Importar Olá projeto de starter de monitoramento remoto e, em seguida, alterar Olá toouse de projeto Olá protocolo MQTT em vez da saudação protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="ccff2-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="ccff2-161">No momento, você precisa toouse Olá MQTT protocolo toouse Olá dispositivo recursos de gerenciamento do IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccff2-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="ccff2-162">No navegador da web, vá toohello mbed.org [site do desenvolvedor](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="ccff2-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="ccff2-163">Se você ainda não fez, você verá um toocreate opção uma conta (é gratuito).</span><span class="sxs-lookup"><span data-stu-id="ccff2-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="ccff2-164">Caso contrário, faça logon com suas credenciais de conta.</span><span class="sxs-lookup"><span data-stu-id="ccff2-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="ccff2-165">Em seguida, clique em **compilador** no canto superior direito de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="ccff2-166">Essa ação coloca toohello *espaço de trabalho* interface.</span><span class="sxs-lookup"><span data-stu-id="ccff2-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="ccff2-167">Certifique-se de plataforma de hardware Olá você está usando aparece no canto superior direito de saudação da janela hello, ou clique em ícone Olá tooselect de canto superior direito da saudação sua plataforma de hardware.</span><span class="sxs-lookup"><span data-stu-id="ccff2-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="ccff2-168">Clique em **importação** no menu principal da saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="ccff2-169">Em seguida, clique em **clique aqui tooimport de URL**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Iniciar o espaço de trabalho de importação toombed][6]

1. <span data-ttu-id="ccff2-171">Na janela pop-up do hello, insira o link de saudação para Olá exemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ e clique em **importação**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Importar o espaço de trabalho do exemplo código toombed][7]

1. <span data-ttu-id="ccff2-173">Você pode ver na janela de compilador mbed Olá que importar este projeto também importa várias bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="ccff2-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="ccff2-174">Alguns são fornecidas e mantidas pela equipe do Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), enquanto outros são bibliotecas de terceiros disponíveis no catálogo do hello mbed bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="ccff2-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Exibir projeto mbed][8]

1. <span data-ttu-id="ccff2-176">Em hello **espaço de trabalho do programa**, atalho Olá **hub IOT\_amqp\_transporte** biblioteca, clique em **excluir**e, em seguida, clique em **Okey** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ccff2-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="ccff2-177">Em hello **espaço de trabalho do programa**, atalho Olá **azure\_amqp\_c** biblioteca, clique em **excluir**e, em seguida, clique em **Okey**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ccff2-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="ccff2-178">Saudação do botão direito do mouse **remote_monitoring** projeto no hello **espaço de trabalho do programa**, selecione **biblioteca de importação**, em seguida, selecione **From URL**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Iniciar o espaço de trabalho de toombed de importação de biblioteca][6]

1. <span data-ttu-id="ccff2-180">Na janela pop-up do hello, insira o link de saudação para Olá MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_de transporte / clique **importação**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Importar o espaço de trabalho biblioteca toombed][12]

1. <span data-ttu-id="ccff2-182">Olá repetição etapa tooadd Olá MQTT biblioteca anterior de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="ccff2-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="ccff2-183">Seu espaço de trabalho agora Olá seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="ccff2-183">Your workspace now looks like hello following:</span></span>

    ![Exibir espaço de trabalho mbed][13]

1. <span data-ttu-id="ccff2-185">Abra Olá remoto\_monitoring\remote_monitoring.c arquivo e substituir Olá existente `#include` instruções com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccff2-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="ccff2-186">Excluir Olá todos os restantes código Olá remoto\_monitoring\remote\_monitoring.c arquivo.</span><span class="sxs-lookup"><span data-stu-id="ccff2-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="ccff2-187">Compilar e executar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="ccff2-187">Build and run hello sample</span></span>

<span data-ttu-id="ccff2-188">Adicionar saudação do código tooinvoke **remoto\_monitoramento\_executar** de função e, em seguida, compilar e executar o aplicativo de dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="ccff2-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="ccff2-189">Adicionar um **principal** função com o código a seguir no final de saudação do hello remoto\_saudação do monitoring.c arquivo tooinvoke **remoto\_monitoramento\_executar** função:</span><span class="sxs-lookup"><span data-stu-id="ccff2-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="ccff2-190">Clique em **compilar** toobuild programa de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="ccff2-191">Com segurança, você pode ignorar os avisos mas se a compilação hello gera erros, corrija-os antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="ccff2-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="ccff2-192">Se compilação Olá for bem-sucedida, o site de compilador mbed hello gera um arquivo. bin com nome de saudação do seu projeto e baixa máquina local tooyour.</span><span class="sxs-lookup"><span data-stu-id="ccff2-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="ccff2-193">Copie o dispositivo de toohello de arquivo hello. bin.</span><span class="sxs-lookup"><span data-stu-id="ccff2-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="ccff2-194">Salvar o dispositivo de toohello de arquivo hello. bin faz Olá dispositivo toorestart e executa programa hello contido no arquivo. bin de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccff2-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="ccff2-195">Você pode reiniciar manualmente o programa hello a qualquer momento, pressionando o botão de redefinição de saudação no dispositivo de mbed hello.</span><span class="sxs-lookup"><span data-stu-id="ccff2-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="ccff2-196">Conecte o dispositivo de toohello usando um aplicativo de cliente SSH, como PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ccff2-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="ccff2-197">Você pode determinar a porta serial hello, que o dispositivo usa verificando o Gerenciador de dispositivos do Windows.</span><span class="sxs-lookup"><span data-stu-id="ccff2-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="ccff2-198">Em PuTTY, clique em Olá **Serial** tipo de conexão.</span><span class="sxs-lookup"><span data-stu-id="ccff2-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="ccff2-199">Olá dispositivo normalmente se conecta a 9600 baud, insira assim 9600 em Olá **velocidade** caixa.</span><span class="sxs-lookup"><span data-stu-id="ccff2-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="ccff2-200">Em seguida, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="ccff2-200">Then click **Open**.</span></span>

1. <span data-ttu-id="ccff2-201">programa Hello inicia a execução.</span><span class="sxs-lookup"><span data-stu-id="ccff2-201">hello program starts executing.</span></span> <span data-ttu-id="ccff2-202">Você pode ter tooreset placa de saudação (pressione CTRL + Break ou botão de redefinição da placa de saudação pressione) se o programa de saudação não for iniciado automaticamente quando você se conectar.</span><span class="sxs-lookup"><span data-stu-id="ccff2-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
