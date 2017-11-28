---
title: "web de matriz Virtual aaaStorSimple administração da interface do usuário | Microsoft Docs"
description: "Descreve como as tarefas de administração do tooperform básicas de dispositivos por meio da interface da web hello matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="5410d-103">Use Olá Web UI tooadminister sua matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="5410d-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![fluxo do processo de instalação](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="5410d-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5410d-105">Overview</span></span>
<span data-ttu-id="5410d-106">tutoriais de saudação neste artigo se aplicam a versão disponibilidade geral (GA) de março de 2016 em execução toohello Microsoft Azure StorSimple Virtual Array (também conhecido como Olá StorSimple no dispositivo virtual local).</span><span class="sxs-lookup"><span data-stu-id="5410d-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="5410d-107">Este artigo descreve alguns dos fluxos de trabalho complexos hello e tarefas de gerenciamento que podem ser executadas em Olá matriz Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5410d-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="5410d-108">Você pode gerenciar Olá StorSimple matriz Virtual usando o serviço de Gerenciador de StorSimple Olá da interface do usuário (chamado tooas Olá IU do portal) e Olá interface da web local para o dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5410d-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="5410d-109">Este artigo enfoca tarefas Olá que você pode executar usando a interface da web hello.</span><span class="sxs-lookup"><span data-stu-id="5410d-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="5410d-110">Este artigo inclui Olá tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="5410d-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="5410d-111">Obter chave de criptografia de dados de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="5410d-112">Solucionar problemas de erros de instalação de interface do usuário da Web</span><span class="sxs-lookup"><span data-stu-id="5410d-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="5410d-113">Gerar um pacote de log</span><span class="sxs-lookup"><span data-stu-id="5410d-113">Generate a log package</span></span>
* <span data-ttu-id="5410d-114">Desligar ou reiniciar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="5410d-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="5410d-115">Obter chave de criptografia de dados de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-115">Get hello service data encryption key</span></span>
<span data-ttu-id="5410d-116">Uma chave de criptografia de dados de serviço é gerada quando você registra o dispositivo primeiro Olá serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="5410d-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="5410d-117">Essa chave é necessária com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="5410d-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="5410d-118">Se você esquecer sua chave de criptografia de dados de serviço e precisa tooretrieve, executar Olá seguintes etapas na interface de dispositivo de saudação da web local Olá registrado com o serviço.</span><span class="sxs-lookup"><span data-stu-id="5410d-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="5410d-119">chave de criptografia de dados de serviço do tooget Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="5410d-120">Conecte-se a interface da web local toohello.</span><span class="sxs-lookup"><span data-stu-id="5410d-120">Connect toohello local web UI.</span></span> <span data-ttu-id="5410d-121">Vá muito**configuração** > **as configurações de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="5410d-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="5410d-122">Final Olá Olá página, clique em **chave de criptografia de dados de serviço Get**.</span><span class="sxs-lookup"><span data-stu-id="5410d-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="5410d-123">Uma chave será exibida.</span><span class="sxs-lookup"><span data-stu-id="5410d-123">A key will appear.</span></span> <span data-ttu-id="5410d-124">Copie e salve essa chave.</span><span class="sxs-lookup"><span data-stu-id="5410d-124">Copy and save this key.</span></span>
   
    ![obter chave de criptografia de dados do serviço 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="5410d-126">Solucionar problemas de erros de instalação de interface do usuário da Web</span><span class="sxs-lookup"><span data-stu-id="5410d-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="5410d-127">Em alguns casos quando você configura o dispositivo Olá Web local de saudação da interface do usuário, você pode executar em erros.</span><span class="sxs-lookup"><span data-stu-id="5410d-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="5410d-128">toodiagnose e solucionar esses erros, você pode executar testes de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5410d-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="5410d-129">testes de diagnóstico toorun Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="5410d-130">Olá interface da web local, vá muito**solução de problemas** > **testes de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5410d-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![executar dignóstico 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="5410d-132">Final Olá Olá página, clique em **executar testes de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5410d-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="5410d-133">Isso irá iniciar testes toodiagnose possíveis problemas com sua rede, dispositivo, proxy da web, hora ou as configurações de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5410d-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="5410d-134">Você será notificado de que o dispositivo hello está executando testes.</span><span class="sxs-lookup"><span data-stu-id="5410d-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="5410d-135">Após a conclusão dos testes de hello, Olá resultados serão exibidos.</span><span class="sxs-lookup"><span data-stu-id="5410d-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="5410d-136">Olá, exemplo a seguir mostra os resultados de saudação de testes de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5410d-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="5410d-137">Observe que configurações de proxy da web hello não foram configuradas neste dispositivo e, portanto, o teste de proxy da web hello não foi executado.</span><span class="sxs-lookup"><span data-stu-id="5410d-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="5410d-138">Olá a todos os outros testes para configurações de rede, servidor DNS, e as configurações de tempo foram bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="5410d-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![executar dignóstico 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="5410d-140">Gerar um pacote de log</span><span class="sxs-lookup"><span data-stu-id="5410d-140">Generate a log package</span></span>
<span data-ttu-id="5410d-141">Um pacote de log é composto de todos os logs de saudação relevantes que podem ajudar a Microsoft Support na solução de problemas no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5410d-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="5410d-142">Nesta versão, um pacote de log pode ser gerado por meio da interface do usuário da web local hello.</span><span class="sxs-lookup"><span data-stu-id="5410d-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="5410d-143">pacote de log toogenerate Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="5410d-144">Olá interface da web local, vá muito**solução de problemas** > **logs do sistema**.</span><span class="sxs-lookup"><span data-stu-id="5410d-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![gerar pacote de log 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="5410d-146">Final Olá Olá página, clique em **criar pacote de log**.</span><span class="sxs-lookup"><span data-stu-id="5410d-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="5410d-147">Um pacote de saudação logs de sistema será criado.</span><span class="sxs-lookup"><span data-stu-id="5410d-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="5410d-148">Isso levará alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5410d-148">This will take a couple of minutes.</span></span>
   
    ![gerar pacote de log 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="5410d-150">Você será notificado depois de pacote de saudação é criado com êxito e Olá página será atualizada quando o pacote de saudação foi criado de data e hora de saudação do tooindicate.</span><span class="sxs-lookup"><span data-stu-id="5410d-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![gerar pacote de log 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="5410d-152">Clique em **Baixar pacote de log**.</span><span class="sxs-lookup"><span data-stu-id="5410d-152">Click **Download log package**.</span></span> <span data-ttu-id="5410d-153">Um pacote compactado será baixado em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="5410d-153">A zipped package will be downloaded on your system.</span></span>
   
    ![gerar pacote de log 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="5410d-155">Você pode descompactar pacote de log baixados Olá e exibir arquivos de log do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5410d-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="5410d-156">Desligue e reinicie seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="5410d-156">Shut down and restart your device</span></span>
<span data-ttu-id="5410d-157">Você pode desligar ou reiniciar seu dispositivo virtual usando a interface da web local hello.</span><span class="sxs-lookup"><span data-stu-id="5410d-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="5410d-158">É recomendável que, antes de reiniciar, levar volumes hello ou compartilhamentos offline no host Olá Olá, em seguida, o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5410d-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="5410d-159">Isso minimizará a possibilidade de dados corrompidos.</span><span class="sxs-lookup"><span data-stu-id="5410d-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="5410d-160">tooshut seu dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="5410d-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="5410d-161">Olá interface da web local, vá muito**manutenção** > **as configurações de energia**.</span><span class="sxs-lookup"><span data-stu-id="5410d-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="5410d-162">Final Olá Olá página, clique em **desligamento**.</span><span class="sxs-lookup"><span data-stu-id="5410d-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![desligamento de dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="5410d-164">Um aviso será exibido informando que um desligamento do dispositivo Olá interromperá qualquer e/s que estava em andamento, resultando em um tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="5410d-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="5410d-165">Clique o ícone de verificação Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-165">Click hello check icon</span></span> ![ícone de verificação](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="5410d-167">.</span><span class="sxs-lookup"><span data-stu-id="5410d-167">.</span></span>
   
    ![aviso de desligamento de dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="5410d-169">Você será notificado que desligamento Olá foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="5410d-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![o desligamento de dispositivo foi iniciado](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="5410d-171">dispositivo Olá será encerrado agora.</span><span class="sxs-lookup"><span data-stu-id="5410d-171">hello device will now shut down.</span></span> <span data-ttu-id="5410d-172">Se você quiser toostart seu dispositivo, você precisará toodo que, por meio de Olá Gerenciador Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="5410d-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="5410d-173">toorestart seu dispositivo virtual</span><span class="sxs-lookup"><span data-stu-id="5410d-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="5410d-174">Olá interface da web local, vá muito**manutenção** > **as configurações de energia**.</span><span class="sxs-lookup"><span data-stu-id="5410d-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="5410d-175">Final Olá Olá página, clique em **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="5410d-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![reinicialização do dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="5410d-177">Um aviso será exibido informando que reiniciar o dispositivo Olá interromperá qualquer IOs que estavam em andamento, resultando em um tempo de inatividade.</span><span class="sxs-lookup"><span data-stu-id="5410d-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="5410d-178">Clique o ícone de verificação Olá</span><span class="sxs-lookup"><span data-stu-id="5410d-178">Click hello check icon</span></span> ![ícone de verificação](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="5410d-180">.</span><span class="sxs-lookup"><span data-stu-id="5410d-180">.</span></span>
   
    ![aviso de reinicialização](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="5410d-182">Você será notificado de que a reinicialização Olá foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="5410d-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![reinicialização iniciada](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="5410d-184">Enquanto Olá reinicialização está em andamento, você perderá Olá conexão toohello da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="5410d-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="5410d-185">Você pode monitorar Olá reinicialização atualizando Olá UI periodicamente.</span><span class="sxs-lookup"><span data-stu-id="5410d-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="5410d-186">Como alternativa, você pode monitorar o status de reinicialização do dispositivo Olá por meio de saudação Gerenciador Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="5410d-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5410d-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5410d-187">Next steps</span></span>
<span data-ttu-id="5410d-188">Saiba como muito[use Olá toomanage do serviço StorSimple Manager seu dispositivo](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5410d-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

