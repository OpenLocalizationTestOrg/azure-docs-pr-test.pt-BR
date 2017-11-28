---
title: dispositivo de tootroubleshoot StorSimple 8000 ferramenta aaaDiagnostics | Microsoft Docs
description: "Descreve os modos do dispositivo StorSimple hello e explica como toouse do Windows PowerShell para StorSimple toochange Olá modo de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="91061-103">Use Olá ferramenta de diagnóstico do StorSimple tootroubleshoot 8000 series problemas do dispositivo</span><span class="sxs-lookup"><span data-stu-id="91061-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="91061-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91061-104">Overview</span></span>

<span data-ttu-id="91061-105">Olá, ferramenta de diagnóstico de StorSimple diagnostica toosystem relacionados problemas, desempenho, rede e integridade dos componentes de hardware para um dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="91061-106">ferramenta de diagnóstico de saudação pode ser usada em vários cenários.</span><span class="sxs-lookup"><span data-stu-id="91061-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="91061-107">Esses cenários incluem a carga de trabalho de planejamento, implantação de um dispositivo StorSimple, avaliar o ambiente de rede de saudação e determinação do desempenho de saudação de um dispositivo operacional.</span><span class="sxs-lookup"><span data-stu-id="91061-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="91061-108">Este artigo fornece uma visão geral da ferramenta de diagnóstico de saudação e descreve como a ferramenta Olá pode ser usada com um dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="91061-109">ferramenta de diagnóstico de saudação é usado principalmente para dispositivos de locais de série StorSimple 8000 (8100 e 8600).</span><span class="sxs-lookup"><span data-stu-id="91061-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="91061-110">Execute a ferramenta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="91061-110">Run diagnostics tool</span></span>

<span data-ttu-id="91061-111">Essa ferramenta pode ser executada por meio da interface do Windows PowerShell de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="91061-112">Há duas maneiras tooaccess Olá interface local do seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="91061-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="91061-113">[Console serial do dispositivo usar PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="91061-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="91061-114">[Acessar remotamente a ferramenta Olá por meio de saudação do Windows PowerShell para StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="91061-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="91061-115">Neste artigo, vamos supor que você está conectado toohello console serial do dispositivo por meio do PuTTY.</span><span class="sxs-lookup"><span data-stu-id="91061-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="91061-116">ferramenta de diagnóstico de saudação toorun</span><span class="sxs-lookup"><span data-stu-id="91061-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="91061-117">Depois que você se conectou a interface do Windows PowerShell toohello do dispositivo hello, execute Olá etapas toorun Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="91061-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="91061-118">Faça logon no console serial do dispositivo toohello, seguindo as etapas de saudação em [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="91061-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="91061-119">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="91061-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="91061-120">Se o parâmetro de escopo de saudação não for especificado, o cmdlet de Olá executa todos os testes de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="91061-121">Esses testes incluem a integridade de componentes de hardware, sistema, rede e desempenho.</span><span class="sxs-lookup"><span data-stu-id="91061-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="91061-122">toorun apenas um teste específico, especifique o parâmetro de escopo de hello.</span><span class="sxs-lookup"><span data-stu-id="91061-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="91061-123">Por exemplo, toorun somente Olá teste de rede, tipo</span><span class="sxs-lookup"><span data-stu-id="91061-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="91061-124">Selecione e copie a saída de hello da saudação PuTTY janela em um arquivo de texto para análise posterior.</span><span class="sxs-lookup"><span data-stu-id="91061-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="91061-125">Ferramenta de diagnóstico cenários toouse Olá</span><span class="sxs-lookup"><span data-stu-id="91061-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="91061-126">Use Olá diagnóstico ferramenta tootroubleshoot Olá rede, o desempenho, o sistema e o hardware integridade do sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="91061-127">Aqui estão alguns cenários possíveis:</span><span class="sxs-lookup"><span data-stu-id="91061-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="91061-128">**Dispositivo offline** - Seu dispositivo da série StorSimple 8000 dispositivo está offline.</span><span class="sxs-lookup"><span data-stu-id="91061-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="91061-129">No entanto, na interface do Windows PowerShell hello, parece que ambos os controladores Olá estão em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="91061-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="91061-130">Você pode usar essa ferramenta toothen determinar o estado da rede hello.</span><span class="sxs-lookup"><span data-stu-id="91061-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="91061-131">Não use esse desempenho de tooassess de ferramenta e as configurações de rede em um dispositivo antes de registro hello (ou configurar por meio do Assistente de instalação).</span><span class="sxs-lookup"><span data-stu-id="91061-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="91061-132">Um IP válido é atribuído toohello dispositivo durante o registro e o Assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="91061-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="91061-133">Você pode executar este cmdlet em um dispositivo que não está registrado para verificar a integridade do hardware e do sistema.</span><span class="sxs-lookup"><span data-stu-id="91061-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="91061-134">Use o parâmetro de escopo hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="91061-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="91061-135">**Problemas de dispositivo persistente** -você estiver tendo problemas de dispositivo que parecem toopersist.</span><span class="sxs-lookup"><span data-stu-id="91061-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="91061-136">Por exemplo, ocorre um erro ao fazer o registro.</span><span class="sxs-lookup"><span data-stu-id="91061-136">For instance, registration is failing.</span></span> <span data-ttu-id="91061-137">Você pode também ter problemas dispositivo depois que o dispositivo hello está operacional e registrado com êxito por um tempo.</span><span class="sxs-lookup"><span data-stu-id="91061-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="91061-138">Nesse caso, use essa ferramenta para uma solução de problemas preliminar antes de fazer uma solicitação de serviço o Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="91061-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="91061-139">É recomendável que você execute essa saída Olá ferramenta e a captura dessa ferramenta.</span><span class="sxs-lookup"><span data-stu-id="91061-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="91061-140">Em seguida, você pode fornecer essa saída tooSupport tooexpedite de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="91061-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="91061-141">Se houver qualquer falha de um componente ou cluster de hardware, você deve fazer uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="91061-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="91061-142">**Baixo desempenho do dispositivo** - O dispositivo StorSimple está muito lento.</span><span class="sxs-lookup"><span data-stu-id="91061-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="91061-143">Nesse caso, execute este cmdlet com tooperformance de conjunto de parâmetros de escopo.</span><span class="sxs-lookup"><span data-stu-id="91061-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="91061-144">Analise a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="91061-144">Analyze hello output.</span></span> <span data-ttu-id="91061-145">Você obtém nuvem Olá latências de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="91061-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="91061-146">Olá Use relatado latências como destino viável máximo, leve em alguma sobrecarga de processamento de dados interno do hello e implantar cargas de trabalho Olá no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="91061-147">Para obter mais informações, vá muito[usar Olá rede teste tootroubleshoot dispositivo desempenho](#network-test).</span><span class="sxs-lookup"><span data-stu-id="91061-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="91061-148">Saídas de exemplo e teste de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="91061-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="91061-149">Teste de hardware</span><span class="sxs-lookup"><span data-stu-id="91061-149">Hardware test</span></span>

<span data-ttu-id="91061-150">Esse teste determina o status de Olá Olá componentes de hardware, firmware USM de Olá e firmware de disco Olá em execução no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="91061-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="91061-151">componentes de hardware de saudação relatados são os componentes desse teste Olá com falha ou não estão presentes no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="91061-152">versões de firmware Olá USM firmware e do disco são relatadas para Olá controlador 0, o controlador 1 e componentes compartilhados no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="91061-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="91061-153">Para obter uma lista completa dos componentes de hardware, vá para:</span><span class="sxs-lookup"><span data-stu-id="91061-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="91061-154">Componentes no compartimento principal</span><span class="sxs-lookup"><span data-stu-id="91061-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="91061-155">Componentes no compartimento EBOD</span><span class="sxs-lookup"><span data-stu-id="91061-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="91061-156">Se os componentes com falha, relatórios de teste de hardware Olá [de log em uma solicitação de serviço com o Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="91061-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="91061-157">Exemplo de saída de uma execução de teste de hardware em um dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="91061-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="91061-158">Aqui está um exemplo de saída de um dispositivo StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="91061-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="91061-159">Olá compartimento EBOD não está presente no dispositivo de modelo 8100 hello.</span><span class="sxs-lookup"><span data-stu-id="91061-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="91061-160">Portanto, os componentes do controlador EBOD Olá não são relatados.</span><span class="sxs-lookup"><span data-stu-id="91061-160">Hence, hello EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="91061-161">Teste do sistema</span><span class="sxs-lookup"><span data-stu-id="91061-161">System test</span></span>

<span data-ttu-id="91061-162">Esse teste relata informações do sistema hello, Olá atualizações disponíveis, informações de saudação do cluster e informações de serviço Olá para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="91061-163">informações do sistema Olá incluem modelo hello, número de série do dispositivo, fuso horário, status do controlador e versão do hello detalhadas do software em execução no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="91061-164">Olá toounderstand vários parâmetros do sistema relatados como saída de hello, ir muito[interpretar as informações do sistema](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="91061-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="91061-165">relatórios de disponibilidade de atualização de saudação se modos de saudação normais e de manutenção estão disponíveis e seus nomes de pacote associado.</span><span class="sxs-lookup"><span data-stu-id="91061-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="91061-166">Se `RegularUpdates` e `MaintenanceModeUpdates` são `false`, isso indica que as atualizações de saudação não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="91061-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="91061-167">Seu dispositivo está atualizado.</span><span class="sxs-lookup"><span data-stu-id="91061-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="91061-168">informações de cluster Olá contém informações de saudação em vários componentes lógicos de todos os grupos de cluster HCS hello e seus respectivos status.</span><span class="sxs-lookup"><span data-stu-id="91061-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="91061-169">Se você vir um grupo de cluster offline nesta seção do relatório hello, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="91061-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="91061-170">informações do serviço de saudação incluem nomes de saudação e status de todos os hello HCS e serviços de CiS em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="91061-171">Essas informações são úteis para Olá Microsoft Support na solução de problema de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="91061-172">Exemplo de saída de uma execução de teste do sistema em um dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="91061-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="91061-173">Aqui está um exemplo de saída do teste de sistema Olá executado em um dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="91061-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="91061-174">Teste de rede</span><span class="sxs-lookup"><span data-stu-id="91061-174">Network test</span></span>

<span data-ttu-id="91061-175">Esse teste valida Olá status de interfaces de rede Olá, portas, DNS e NTP conectividade do servidor, SSL certificado, as credenciais de conta de armazenamento, servidores de Update toohello conectividade e conectividade de proxy da web em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="91061-176">Exemplo de saída do teste de rede quando somente DATA0 está habilitado</span><span class="sxs-lookup"><span data-stu-id="91061-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="91061-177">Aqui está um exemplo de saída do dispositivo 8100 hello.</span><span class="sxs-lookup"><span data-stu-id="91061-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="91061-178">Você pode ver na saída de hello que:</span><span class="sxs-lookup"><span data-stu-id="91061-178">You can see in hello output that:</span></span>
* <span data-ttu-id="91061-179">Somente as interfaces de rede DATA 0 e DATA 1 estão ativadas e configuradas.</span><span class="sxs-lookup"><span data-stu-id="91061-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="91061-180">2 a 5 de dados não estão habilitados no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="91061-181">configuração do servidor DNS Olá é válida e dispositivo Olá pode se conectar por meio do servidor DNS hello.</span><span class="sxs-lookup"><span data-stu-id="91061-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="91061-182">Olá conectividade com o servidor NTP também é bom.</span><span class="sxs-lookup"><span data-stu-id="91061-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="91061-183">As portas 80 e 443 estão abertas.</span><span class="sxs-lookup"><span data-stu-id="91061-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="91061-184">No entanto, a porta 9354 está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="91061-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="91061-185">Com base em Olá [requisitos de rede do sistema](storsimple-system-requirements.md), você precisa tooopen essa porta para comunicação do barramento de serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="91061-186">Olá SSL é válido.</span><span class="sxs-lookup"><span data-stu-id="91061-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="91061-187">dispositivo Olá pode se conectar a conta de armazenamento toohello: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="91061-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="91061-188">servidores de tooUpdate conectividade Olá é válido.</span><span class="sxs-lookup"><span data-stu-id="91061-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="91061-189">proxy da web de saudação não está configurado neste dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="91061-190">Exemplo de saída do teste de rede quando somente DATA0 e DATA1 estão habilitados</span><span class="sxs-lookup"><span data-stu-id="91061-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="91061-191">Teste de desempenho</span><span class="sxs-lookup"><span data-stu-id="91061-191">Performance test</span></span>

<span data-ttu-id="91061-192">Esse teste relatórios de desempenho de saudação de nuvem por meio de latências de leitura-gravação de nuvem Olá para seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="91061-193">Essa ferramenta pode ser usada tooestablish uma linha de base de desempenho de saudação de nuvem que você pode obter com o StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="91061-194">Olá ferramenta Olá máximo desempenho de relatórios (melhor cenário de caso de latências de leitura / gravação) que você pode obter a conexão.</span><span class="sxs-lookup"><span data-stu-id="91061-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="91061-195">Como a ferramenta Olá relatórios Olá possível obter o desempenho máximo, podemos usar Olá relatada latências de leitura / gravação, como destinos ao implantar Olá cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="91061-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="91061-196">teste Olá simula tamanhos de blob Olá associados a tipos de volume diferente Olá no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="91061-197">Volumes normais em camadas e backups de volumes localmente fixados usam um tamanho de blob de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="91061-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="91061-198">Volumes em camadas com opção de arquivamento marcada usam um tamanho de dados de blob de 512 KB.</span><span class="sxs-lookup"><span data-stu-id="91061-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="91061-199">Se o dispositivo tiver volumes localmente afixados e hierárquicos configurado, somente Olá teste too64 KB blob correspondente tamanho dos dados é executado.</span><span class="sxs-lookup"><span data-stu-id="91061-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="91061-200">toouse essa ferramenta, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="91061-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="91061-201">Primeiro, crie uma mistura de volumes em camadas e em camadas com a opção de arquivamento marcada.</span><span class="sxs-lookup"><span data-stu-id="91061-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="91061-202">Esta ação garante que essa ferramenta Olá executa testes Olá para 64 KB e 512 KB tamanhos de blob.</span><span class="sxs-lookup"><span data-stu-id="91061-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="91061-203">Execute o cmdlet de saudação depois que você criou e configurou volumes hello.</span><span class="sxs-lookup"><span data-stu-id="91061-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="91061-204">Tipo:</span><span class="sxs-lookup"><span data-stu-id="91061-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="91061-205">Anote as latências de leitura-gravação de Olá relatados pela ferramenta hello.</span><span class="sxs-lookup"><span data-stu-id="91061-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="91061-206">Este teste pode levar vários toorun de minutos antes de relatar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="91061-207">Se Olá latências de conexão são todos com hello intervalo esperado, hello latências relatadas pela ferramenta Olá podem ser usadas como destino viável máximo durante a implantação de cargas de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="91061-208">Considere uma sobrecarga para o processamento de dados interno.</span><span class="sxs-lookup"><span data-stu-id="91061-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="91061-209">Se latências de leitura / gravação da saudação relatado pela ferramenta de diagnóstico de saudação são alta:</span><span class="sxs-lookup"><span data-stu-id="91061-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="91061-210">Configurar o Storage Analytics para serviços blob e analisar Olá saída toounderstand Olá latências de saudação conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="91061-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="91061-211">Para obter instruções detalhadas, consulte muito[habilitar e configurar o Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="91061-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="91061-212">Se as latências também são números de alta e comparável toohello recebida do Olá, ferramenta de diagnóstico de StorSimple, você precisa toolog uma solicitação de serviço com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="91061-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="91061-213">Se as latências de conta de armazenamento Olá baixas, contate seu tooinvestigate do administrador de rede alguma latência problemas em sua rede.</span><span class="sxs-lookup"><span data-stu-id="91061-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="91061-214">Exemplo de saída de uma execução de teste de desempenho em um dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="91061-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="91061-215">Apêndice: interpretação das informações do sistema</span><span class="sxs-lookup"><span data-stu-id="91061-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="91061-216">Aqui está uma tabela que descreve quais Olá mapeiam vários parâmetros do Windows PowerShell em informações do sistema Olá para.</span><span class="sxs-lookup"><span data-stu-id="91061-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="91061-217">Parâmetro do PowerShell</span><span class="sxs-lookup"><span data-stu-id="91061-217">PowerShell Parameter</span></span>    | <span data-ttu-id="91061-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="91061-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="91061-219">ID da instância</span><span class="sxs-lookup"><span data-stu-id="91061-219">Instance ID</span></span>             | <span data-ttu-id="91061-220">Cada controlador tem um identificador exclusivo ou um GUID associado a ele.</span><span class="sxs-lookup"><span data-stu-id="91061-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="91061-221">Nome</span><span class="sxs-lookup"><span data-stu-id="91061-221">Name</span></span>                    | <span data-ttu-id="91061-222">nome amigável de saudação do dispositivo Olá conforme configurado por meio de saudação portal do Azure durante a implantação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="91061-223">nome amigável da saudação padrão é o número de série do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="91061-224">Modelo</span><span class="sxs-lookup"><span data-stu-id="91061-224">Model</span></span>                   | <span data-ttu-id="91061-225">modelo de saudação do seu dispositivo da série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="91061-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="91061-226">modelo de saudação pode ser 8100 ou 8600.</span><span class="sxs-lookup"><span data-stu-id="91061-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="91061-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="91061-227">SerialNumber</span></span>            | <span data-ttu-id="91061-228">número de série do dispositivo Olá é atribuído na fábrica hello e 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="91061-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="91061-229">Por exemplo, 8600-SHX0991003G44HT indica:</span><span class="sxs-lookup"><span data-stu-id="91061-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="91061-230">8600 – é o modelo de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="91061-231">SHX – é fabricação Olá o site.</span><span class="sxs-lookup"><span data-stu-id="91061-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="91061-232">0991003 - É um produto específico.</span><span class="sxs-lookup"><span data-stu-id="91061-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="91061-233">G44HT-Olá últimos 5 dígitos são incrementados toocreate números de série exclusivos.</span><span class="sxs-lookup"><span data-stu-id="91061-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="91061-234">Pode ser um conjunto não sequencial de números.</span><span class="sxs-lookup"><span data-stu-id="91061-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="91061-235">timeZone</span><span class="sxs-lookup"><span data-stu-id="91061-235">TimeZone</span></span>                | <span data-ttu-id="91061-236">Olá fuso horário do dispositivo conforme configurado no hello portal do Azure durante a implantação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="91061-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="91061-237">CurrentController</span></span>       | <span data-ttu-id="91061-238">controlador de saudação que você está conectado toothrough interface de Windows PowerShell Olá do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="91061-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="91061-239">ActiveController</span></span>        | <span data-ttu-id="91061-240">controlador de saudação que está ativo no seu dispositivo e controla todas as operações de rede e disco hello.</span><span class="sxs-lookup"><span data-stu-id="91061-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="91061-241">Pode ser o Controlador 0 ou Controlador 1.</span><span class="sxs-lookup"><span data-stu-id="91061-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="91061-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="91061-242">Controller0Status</span></span>       | <span data-ttu-id="91061-243">status de saudação do controlador 0 em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="91061-244">status do controlador Olá pode ser normal, no modo de recuperação, ou está inacessível.</span><span class="sxs-lookup"><span data-stu-id="91061-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="91061-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="91061-245">Controller1Status</span></span>       | <span data-ttu-id="91061-246">status de saudação do controlador 1 no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="91061-247">status do controlador Olá pode ser normal, no modo de recuperação, ou está inacessível.</span><span class="sxs-lookup"><span data-stu-id="91061-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="91061-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="91061-248">SystemMode</span></span>              | <span data-ttu-id="91061-249">Olá status geral do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="91061-250">status do dispositivo Olá pode ser normal, manutenção, ou encerrado (corresponde toodeactivated em Olá portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="91061-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="91061-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="91061-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="91061-252">Olá cadeia de caracteres amigável que corresponde a versão do software de dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="91061-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="91061-253">Para um sistema que executa a atualização 4, versão amigável Olá seria StorSimple 8000 Series atualização 4.0.</span><span class="sxs-lookup"><span data-stu-id="91061-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="91061-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="91061-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="91061-255">Olá HCS software versão em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="91061-256">Por exemplo, Olá tooStorSimple correspondente de versão de software do HCS 8000 Series atualização 4.0 é 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="91061-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="91061-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="91061-257">ApiVersion</span></span>              | <span data-ttu-id="91061-258">versão do software de saudação do hello API do Windows PowerShell do dispositivo HCS de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="91061-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="91061-259">VhdVersion</span></span>              | <span data-ttu-id="91061-260">versão do software Olá da imagem de fábrica Olá Olá dispositivo foi fornecido com o.</span><span class="sxs-lookup"><span data-stu-id="91061-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="91061-261">Se você redefinir o dispositivo toofactory padrão, ele executa esta versão do software.</span><span class="sxs-lookup"><span data-stu-id="91061-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="91061-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="91061-262">OSVersion</span></span>               | <span data-ttu-id="91061-263">versão do software de saudação do sistema de operacional de servidor Windows hello em execução no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="91061-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="91061-264">o dispositivo StorSimple Olá Olá Windows Server 2012 R2 que corresponde a too6.3.9600 baseado.</span><span class="sxs-lookup"><span data-stu-id="91061-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="91061-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="91061-265">CisAgentVersion</span></span>         | <span data-ttu-id="91061-266">versão de saudação do seu agente de Cis em execução no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="91061-267">Esse agente ajuda a se comunicar com o serviço StorSimple Manager Olá em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="91061-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="91061-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="91061-268">MdsAgentVersion</span></span>         | <span data-ttu-id="91061-269">Olá versão correspondente toohello Mds agente em execução no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="91061-270">Esse agente move dados toohello monitoramento e diagnóstico do serviço (MDS).</span><span class="sxs-lookup"><span data-stu-id="91061-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="91061-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="91061-271">Lsisas2Version</span></span>          | <span data-ttu-id="91061-272">Olá drivers toohello LSI correspondente de versão no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="91061-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="91061-273">Capacity</span></span>                | <span data-ttu-id="91061-274">capacidade total de saudação do dispositivo Olá em bytes.</span><span class="sxs-lookup"><span data-stu-id="91061-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="91061-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="91061-275">RemoteManagementMode</span></span>    | <span data-ttu-id="91061-276">Indica se o dispositivo de saudação pode ser gerenciado remotamente por meio de sua interface do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91061-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="91061-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="91061-277">FipsMode</span></span>                | <span data-ttu-id="91061-278">Indica se o modo de Estados Unidos Federal Information Processing Standard (FIPS) hello está habilitado em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="91061-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="91061-279">padrão Olá FIPS 140 define algoritmo de criptografia aprovado para uso pelos sistemas de computador do Governo Federal dos EUA para proteção de saudação de dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="91061-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="91061-280">Para dispositivos executando a Atualização 4 ou posterior, o modo FIPS está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="91061-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="91061-281">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91061-281">Next steps</span></span>

* <span data-ttu-id="91061-282">Saiba Olá [sintaxe do cmdlet Invoke-HcsDiagnostics de saudação](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="91061-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="91061-283">Saiba mais sobre como muito[solucionar problemas de implantação](storsimple-troubleshoot-deployment.md) em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91061-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
