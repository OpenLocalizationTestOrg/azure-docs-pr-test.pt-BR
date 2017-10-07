---
title: "dispositivo da série aaaUse StorSimple 8000 resumo | Microsoft Docs"
description: "Descreve o dispositivo de serviço de Gerenciador de dispositivos de StorSimple Olá resumo e como toouse-tooview as métricas de armazenamento e iniciadores conectados e localizar Olá número de série e o IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="9d3bc-103">Usar Olá dispositivo resumo no serviço do Gerenciador de dispositivos de StorSimple</span><span class="sxs-lookup"><span data-stu-id="9d3bc-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="9d3bc-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9d3bc-104">Overview</span></span>
<span data-ttu-id="9d3bc-105">folha de resumo Olá StorSimple dispositivo fornece uma visão geral das informações de um dispositivo StorSimple específico, em contraste toohello serviço folha resumida, que fornece informações sobre todos os dispositivos de saudação incluídos em sua solução do Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="9d3bc-106">folha de resumo de dispositivo Olá fornece uma exibição resumida de um dispositivo da série StorSimple 8000 que está registrado com um determinado StorSimple Gerenciador de dispositivos, realçando os problemas de dispositivos que precisam de atenção do administrador do sistema.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="9d3bc-107">Este tutorial apresenta a folha de resumo de dispositivo hello, explica a função e o conteúdo de saudação e descreve Olá tarefas que você pode executar com esta folha.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="9d3bc-108">folha de resumo de dispositivo Olá exibe Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d3bc-108">hello device summary blade displays hello following information:</span></span>

![Folha de resumo do dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="9d3bc-110">Barra de comandos de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="9d3bc-110">Management command bar</span></span>

<span data-ttu-id="9d3bc-111">Na folha de dispositivo do StorSimple Olá, você verá opções de saudação para gerenciar seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="9d3bc-112">Você ver os comandos de gerenciamento de saudação na superior de saudação da folha de saudação e no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="9d3bc-113">Use essas opções tooadd compartilhamentos ou volumes, ou atualizar ou failover de seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Barra de comandos de gerenciamento](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="9d3bc-115">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="9d3bc-115">Essentials</span></span>

<span data-ttu-id="9d3bc-116">área do essentials Olá captura algumas das propriedades de saudação importantes, como, status hello, modelo, IQN de destino e versão do software hello.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Conceitos básicos do dispositivo](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="9d3bc-118">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="9d3bc-118">Monitoring</span></span>

* <span data-ttu-id="9d3bc-119">Olá **alertas** lado a lado fornece um instantâneo de todos os alertas ativos de saudação do seu dispositivo, agrupado por severidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Bloco de alerta](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="9d3bc-121">Clique em Olá bloco tooopen Olá **alertas** folha e depois clique em um indivíduo alerta tooview mais detalhes sobre esse alerta, incluindo as ações recomendadas.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="9d3bc-122">Você também pode limpar o alerta de saudação se Olá problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Clique no bloco de alerta](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="9d3bc-124">Olá **Status e integridade** lado a lado fornece ideias sobre a integridade dos componentes de hardware Olá para um dispositivo, incluindo status de saudação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="9d3bc-125">status de saudação do dispositivo pode ser tooset offline, online, desativado ou pronto para cima.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Bloco de status e integridade](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="9d3bc-127">Olá **Volumes** lado a lado fornece um resumo do número de saudação de volumes no seu dispositivo agrupados por status.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Bloco Volumes](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="9d3bc-129">Clique em Olá bloco tooopen Olá **Volumes** folha e, em seguida, clique em um volume individual tooview ou modificar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Clique no bloco Volumes](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="9d3bc-131">Para obter mais informações, consulte como muito[gerenciar volumes](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="9d3bc-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="9d3bc-132">Em Olá **uso** gráfico, você pode exibir o armazenamento primário de saudação usado em seu dispositivo e o armazenamento em nuvem Olá consumida durante saudação últimos 7 dias, o padrão de saudação período de tempo.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Bloco Uso](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="9d3bc-134">toochoose uma escala de tempo diferentes, use Olá **editar** opção no canto superior direito de saudação do gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Editar gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="9d3bc-136">Neste gráfico, você pode exibir métricas para armazenamento primário total hello (quantidade Olá dos dados gravados pelo dispositivo de tooyour hosts) e Olá total consumido por seu dispositivo em um período de tempo de armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="9d3bc-137">Nesse contexto, *armazenamento primário* refere-se a quantidade total de toohello dos dados gravados pelo host hello e podem ser divididos por tipo de volume: *armazenamento hierárquico primário* inclui tanto armazenadas localmente os dados e dados nuvem toohello em camadas.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="9d3bc-138">O *armazenamento primário fixado localmente* inclui apenas os dados armazenados localmente.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="9d3bc-139">*Armazenamento em nuvem*, em Olá outro lado, é uma medida da quantidade total de saudação dos dados armazenados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="9d3bc-140">Esse armazenamento inclui dados em camadas e backups.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="9d3bc-141">Olá dados armazenados na nuvem Olá com eliminação de duplicação e compactados, enquanto o armazenamento primário indica a quantidade de saudação do armazenamento usado antes de dados saudação está com eliminação de duplicação e compactados.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="9d3bc-142">(Você pode comparar esses dois números tooget uma ideia da taxa de compactação de saudação). Para o principal e o armazenamento na nuvem, Olá valores mostrados se baseiam no hello frequência de configuração de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="9d3bc-143">Por exemplo, se você escolher uma frequência de uma semana, Olá gráfico mostra dados de cada dia em Olá semana anterior.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="9d3bc-144">quantidade de saudação toosee de armazenamento em nuvem consumido por tempo, selecione Olá **armazenamento de nuvem usado** opção.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="9d3bc-145">toosee Olá total de armazenamento que foi gravado pelo host hello, selecione Olá **armazenamento primário em camadas, usado** e **LOCALMENTE FIXADOS armazenamento primário usado** opções.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="9d3bc-146">Para obter mais informações, consulte [Use Olá toomonitor de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="9d3bc-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="9d3bc-147">Olá **capacidade** Olá lado a lado exibe Olá armazenamento primário provisionado e o restante em Olá dispositivo toohello relativo armazenamento total disponível para a mesma.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="9d3bc-148">**Provisionado** refere-se a quantidade de toohello de armazenamento preparado e alocado para uso, **restante** refere-se toohello capacidade que pode ser provisionada por este dispositivo restante.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Bloco Uso](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="9d3bc-150">Clique neste tooview lado a lado como capacidade Olá é provisionada em volumes fixados localmente e em camadas.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="9d3bc-151">Olá **camadas restantes** capacidade é a capacidade disponível de saudação que pode ser provisionada incluindo nuvem durante a saudação **restantes Local** é toothis dispositivo conectado à capacidade restante em discos de saudação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d3bc-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Clique no gráfico de uso](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="9d3bc-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d3bc-153">Next steps</span></span>
* <span data-ttu-id="9d3bc-154">Saiba mais sobre Olá [folha de resumo de serviço do StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="9d3bc-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="9d3bc-155">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9d3bc-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

