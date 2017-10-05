---
title: Mover os recursos do aplicativo Web para outro grupo de recursos
description: "Descreve os cenários em que você pode mover aplicativos Web e Serviços de Aplicativos de um grupo de recursos para outro."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="cbfa1-103">Configurações de movimentação com suporte</span><span class="sxs-lookup"><span data-stu-id="cbfa1-103">Supported Move Configurations</span></span>
<span data-ttu-id="cbfa1-104">Você pode mover recursos de Aplicativo Web do Azure usando a [API Mover Recursos do Resource Manager](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cbfa1-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="cbfa1-105">Atualmente, os aplicativos Web do Azure dão suporte para os seguintes cenários de movimentação:</span><span class="sxs-lookup"><span data-stu-id="cbfa1-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="cbfa1-106">Mover todo o conteúdo de um grupo de recursos (aplicativos Web, planos do serviço de aplicativo e certificados) para outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="cbfa1-107">O grupo de recursos de destino não pode conter nenhum recurso Microsoft.Web nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="cbfa1-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="cbfa1-108">Mover aplicativos Web individuais para um grupo de recursos diferente, enquanto ainda os hospeda em seu plano do serviço de aplicativo atual (o plano do serviço de aplicativo permanece no grupo de recursos antigo).</span><span class="sxs-lookup"><span data-stu-id="cbfa1-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


