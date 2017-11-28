---
title: Recursos do aplicativo Web de aaaMove tooanother grupo de recursos
description: "Descreve os cenários de saudação onde você pode mover os aplicativos Web e serviços de aplicativos de tooanother de um grupo de recursos."
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
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="10d32-103">Configurações de movimentação com suporte</span><span class="sxs-lookup"><span data-stu-id="10d32-103">Supported Move Configurations</span></span>
<span data-ttu-id="10d32-104">Você pode mover os recursos de aplicativo Web do Azure usando Olá [Resource Manager mover recursos API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="10d32-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="10d32-105">Os aplicativos Web do Azure atualmente suporta os seguintes cenários de movimentação de saudação:</span><span class="sxs-lookup"><span data-stu-id="10d32-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="10d32-106">Mover todo o conteúdo de um grupo de recursos (aplicativos da web, planos de serviço de aplicativo e certificados) Olá tooanother grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="10d32-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="10d32-107">grupo de recursos de destino de saudação não pode conter todos os recursos Microsoft neste cenário.</span><span class="sxs-lookup"><span data-stu-id="10d32-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="10d32-108">Mova o grupo de recursos diferente tooa de aplicativos web individuais, enquanto ainda hospedando-los em seu plano de serviço de aplicativo atual (Olá aplicativo serviço plano permanece no grupo de recursos antigo Olá).</span><span class="sxs-lookup"><span data-stu-id="10d32-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


