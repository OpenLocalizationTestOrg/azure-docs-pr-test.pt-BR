---
title: Folha de resumo de dispositivo da StorSimple Virtual Array | Microsoft Docs
description: "Descreve a folha de resumo do dispositivo do Gerenciador de Dispositivos StorSimple e explica como usá-lo para monitorar a integridade da Matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="cd05a-103">Use a folha de resumo do dispositivo do Gerenciador de Dispositivos StorSimple conectado à Matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="cd05a-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cd05a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cd05a-104">Overview</span></span>

<span data-ttu-id="cd05a-105">A folha do dispositivo Gerenciador de Dispositivos StorSimple fornece uma exibição resumida de uma Matriz Virtual StorSimple que está registrada em determinado Gerenciador de Dispositivos StorSimple, destacando os problemas de dispositivos que precisam da atenção do administrador do sistema.</span><span class="sxs-lookup"><span data-stu-id="cd05a-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="cd05a-106">Este tutorial apresenta a folha de resumo do dispositivo, explica o conteúdo e a função e descreve as tarefas que podem ser realizadas nessa folha.</span><span class="sxs-lookup"><span data-stu-id="cd05a-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="cd05a-107">A folha de resumo do dispositivo exibe as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="cd05a-107">The device summary blade displays the following information:</span></span>

![Painel do dispositivo](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="cd05a-109">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cd05a-109">Management</span></span>

<span data-ttu-id="cd05a-110">Na folha do dispositivo StorSimple, veja as opções para gerenciar seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cd05a-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="cd05a-111">Você vê os comandos de gerenciamento na parte superior da folha e no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="cd05a-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="cd05a-112">Use essas opções para adicionar compartilhamentos ou volumes, ou atualizar ou fazer failover da sua matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="cd05a-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="cd05a-113">A área de conceitos básicos captura algumas das propriedades importantes, como o status, o modelo, a versão de software e um link para a **interface do usuário da Web** da matriz.</span><span class="sxs-lookup"><span data-stu-id="cd05a-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="cd05a-114">Se você está em uma rede interna, pode iniciar diretamente a [interface do usuário da Web local](storsimple-ova-web-ui-admin.md) para administrar sua matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="cd05a-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Conceitos básicos do dispositivo](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="cd05a-116">Resumo do dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="cd05a-116">StorSimple device summary</span></span>

* <span data-ttu-id="cd05a-117">O bloco **Alertas** fornece um instantâneo de todos os alertas ativos na sua matriz virtual agrupados por severidade do alerta.</span><span class="sxs-lookup"><span data-stu-id="cd05a-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="cd05a-118">Clique no bloco para abrir a folha **Alertas** e clique em um alerta individual para exibir detalhes adicionais sobre ele, incluindo todas as ações recomendadas.</span><span class="sxs-lookup"><span data-stu-id="cd05a-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="cd05a-119">Você também pode limpar o alerta se o problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="cd05a-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="cd05a-120">O bloco **Capacidade** mostra o armazenamento primário provisionado e restante no dispositivo virtual em relação ao armazenamento total disponível nele.</span><span class="sxs-lookup"><span data-stu-id="cd05a-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="cd05a-121">**Provisionado** refere-se à quantidade de armazenamento que é preparada e alocada para uso, enquanto **Restante** refere-se à capacidade restante que pode ser provisionada nesse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cd05a-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="cd05a-122">A capacidade **Restante em Camadas** é a capacidade disponível que pode ser provisionada, incluindo a nuvem, enquanto a capacidade **Restante Local** é a capacidade restante nos discos anexados à matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="cd05a-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="cd05a-123">No gráfico **Uso**, você pode ver o armazenamento primário usado na sua matriz virtual, bem como o armazenamento em nuvem consumido nos últimos sete dias, o período padrão.</span><span class="sxs-lookup"><span data-stu-id="cd05a-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="cd05a-124">Use a opção **Editar** no canto superior direito do gráfico para escolher uma escala de tempo diferente.</span><span class="sxs-lookup"><span data-stu-id="cd05a-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="cd05a-125">O bloco **Compartilhamentos** ou **Volumes** fornece um resumo do número de compartilhamentos ou volumes no seu dispositivo agrupado por status.</span><span class="sxs-lookup"><span data-stu-id="cd05a-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="cd05a-126">Clique no bloco para abrir a folha de lista **Compartilhamentos** ou **Volumes** e clique em um compartilhamento ou volume individual para exibir ou modificar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="cd05a-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="cd05a-127">Para saber mais, confira como [gerenciar compartilhamentos](storsimple-virtual-array-manage-shares.md) ou [gerenciar volumes](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="cd05a-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd05a-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd05a-128">Next steps</span></span>
<span data-ttu-id="cd05a-129">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="cd05a-129">Learn how to:</span></span>
- [<span data-ttu-id="cd05a-130">Gerenciar compartilhamentos em uma matriz virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="cd05a-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="cd05a-131">Gerenciar volumes em uma matriz virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="cd05a-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

