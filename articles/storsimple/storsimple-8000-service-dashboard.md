---
title: Usar o resumo do dispositivo StorSimple 8000 series | Microsoft Docs
description: "Descreve a folha de resumo do serviço StorSimple e explica como usá-lo para monitorar a integridade da solução StorSimple."
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
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="abfd6-103">Use a folha de resumo do serviço do dispositivo StorSimple 8000 series</span><span class="sxs-lookup"><span data-stu-id="abfd6-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="abfd6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="abfd6-104">Overview</span></span>

<span data-ttu-id="abfd6-105">A folha de resumo do serviço StorSimple Device Manager fornece uma exibição resumida de todos os dispositivos conectados ao serviço StorSimple Device Manager, realçando os dispositivos que precisam de atenção do administrador do sistema.</span><span class="sxs-lookup"><span data-stu-id="abfd6-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="abfd6-106">Este tutorial apresenta a folha de resumo do serviço, explica o conteúdo e a função do painel e descreve as tarefas que podem ser realizadas nessa página.</span><span class="sxs-lookup"><span data-stu-id="abfd6-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Resumo do serviço](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="abfd6-108">Comandos de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="abfd6-108">Management commands</span></span>

<span data-ttu-id="abfd6-109">Na folha de resumo do serviço StorSimple, é possível ver as opções para gerenciar o serviço StorSimple Device Manager, bem como os dispositivos StorSimple 8000 series registrados nesse serviço.</span><span class="sxs-lookup"><span data-stu-id="abfd6-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="abfd6-110">Você vê os comandos de gerenciamento na parte superior da folha e no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="abfd6-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Barra de comandos](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="abfd6-112">Use essas opções para executar várias operações como adicionar volumes ou compartilhamentos ou para monitorar os vários trabalhos em execução nos dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="abfd6-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="abfd6-113">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="abfd6-113">Essentials</span></span>

<span data-ttu-id="abfd6-114">A área de informações gerais captura algumas das propriedades importantes, como o grupo de recursos, a localização e a assinatura em que o StorSimple Device Manager foi criado.</span><span class="sxs-lookup"><span data-stu-id="abfd6-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Conceitos básicos](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="abfd6-116">Resumo do serviço do StorSimple Device Manager</span><span class="sxs-lookup"><span data-stu-id="abfd6-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="abfd6-117">O bloco **Alertas** fornece um instantâneo de todos os alertas ativos em todos os dispositivos, agrupados por gravidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="abfd6-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Bloco Alertas](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="abfd6-119">Se você clicar no bloco, a folha **Alertas** será aberta, em que você poderá clicar em um alerta individual para exibir detalhes adicionais sobre ele, incluindo todas as ações recomendadas.</span><span class="sxs-lookup"><span data-stu-id="abfd6-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="abfd6-120">Você também pode limpar o alerta se o problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="abfd6-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Clique no bloco Alertas](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="abfd6-122">O bloco **Capacidade** mostra o armazenamento primário provisionado e restante em todos os dispositivos com relação ao armazenamento total disponível em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="abfd6-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="abfd6-123">**Provisionado** refere-se à quantidade de armazenamento preparada e alocada para uso, enquanto **Restante** refere-se à capacidade restante que pode ser provisionada em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="abfd6-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Bloco Capacidade](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="abfd6-125">A capacidade **Restante em Camadas** é a capacidade disponível que pode ser provisionada, incluindo a nuvem, enquanto a capacidade **Restante Local** é a capacidade restante nos discos anexados aos dispositivos StorSimple 8000 series.</span><span class="sxs-lookup"><span data-stu-id="abfd6-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="abfd6-126">No gráfico **Uso**, você pode ver as métricas relevantes dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="abfd6-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="abfd6-127">Veja o armazenamento primário usado em todos os dispositivos, bem como o armazenamento em nuvem consumido pelos dispositivos nos últimos sete dias, que é o período padrão.</span><span class="sxs-lookup"><span data-stu-id="abfd6-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Bloco Uso](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="abfd6-129">Para escolher uma escala de tempo diferente, use a opção **Editar** no canto superior direito do gráfico.</span><span class="sxs-lookup"><span data-stu-id="abfd6-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Clique no bloco Uso](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Exportar dados do gráfico](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="abfd6-132">O bloco **Dispositivos** fornece um resumo do número de dispositivos StorSimple 8000 series no StorSimple Device Manager agrupados por status do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abfd6-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Bloco Dispositivos](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="abfd6-134">Clique nesse bloco para abrir a folha da lista **Dispositivos** e clique em um dispositivo individual para analisar o resumo de dispositivo específico do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abfd6-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="abfd6-135">Você também pode executar ações específicas do dispositivo de uma folha de resumo de um determinado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="abfd6-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="abfd6-136">Para obter mais informações sobre a folha de resumo do dispositivo, vá para [Folha de resumo do dispositivo](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="abfd6-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Clique no bloco Dispositivos](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="abfd6-138">Exibir os logs de atividade</span><span class="sxs-lookup"><span data-stu-id="abfd6-138">View the activity logs</span></span>

<span data-ttu-id="abfd6-139">Para exibir as diversas operações executadas no StorSimple Device Manager, clique no link **Logs de atividade** no lado esquerdo da folha de resumo do serviço do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="abfd6-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="abfd6-140">Isso o levará para a folha **Logs de atividade**, na qual você poderá ver um resumo das operações recentes executadas.</span><span class="sxs-lookup"><span data-stu-id="abfd6-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Logs de atividade](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="abfd6-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abfd6-142">Next steps</span></span>

* <span data-ttu-id="abfd6-143">Saiba mais sobre como [usar o serviço StorSimple Device Manager para administrar dispositivos StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="abfd6-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

