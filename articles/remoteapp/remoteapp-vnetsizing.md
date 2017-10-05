---
title: "Informações de dimensionamento de uma VNET no Azure RemoteApp | Microsoft Docs"
description: "Saiba mais sobre os requisitos de endereço IP para o RemoteApp do Azure em execução com uma VNET"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="37397-103">Dimensionamento de informações de um VNET no RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="37397-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="37397-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="37397-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="37397-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="37397-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="37397-106">Quando você usa o RemoteApp do Azure com uma rede virtual (VNET), o RemoteApp usa endereços IP dentro da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="37397-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="37397-107">Com base na escala de seu serviço do RemoteApp, você precisa garantir que sua sub-rede tenha endereços IP suficientes disponíveis para máquinas virtuais do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="37397-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="37397-108">Embora essa orientação de dimensionamento não seja perfeita, visto o modo como o RemoteApp faz a rotação dinâmica de máquinas virtuais para cima e para baixo dentro de uma coleção, ele ajudará a calcular o intervalo de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="37397-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="37397-109">Isso é especialmente importante já que, quando um serviço do RemoteApp é colocado em uma VNET, você não pode aumentar o tamanho da sub-rede sem remover o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="37397-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="37397-110">Para cada coleção de RemoteApp que você deseja executar em capacidade máxima você deve ter 100 endereços IP disponíveis.</span><span class="sxs-lookup"><span data-stu-id="37397-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="37397-111">Por exemplo, se você tiver uma coleção do RemoteApp no plano Padrão desejar ter no máximo 500 usuários, você deve ter 100 endereços IP para essa coleção.</span><span class="sxs-lookup"><span data-stu-id="37397-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="37397-112">Do mesmo modo, você precisa de 100 endereços IP para uma coleção de RemoteApp no plano Básico com 800 usuários.</span><span class="sxs-lookup"><span data-stu-id="37397-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="37397-113">Se você planeja ter menos usuários (menos que o máximo), você pode reduzir os endereços IP necessários por coleção.</span><span class="sxs-lookup"><span data-stu-id="37397-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="37397-114">O requisito de tamanho mínimo de sub-rede é 30 endereços IP (/27).</span><span class="sxs-lookup"><span data-stu-id="37397-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="37397-115">Confira as informações a seguir para confirmar se sua VNET está configurada e funcionando corretamente:</span><span class="sxs-lookup"><span data-stu-id="37397-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="37397-116">Migrar de uma VNET pessoal para uma VNET do Azure</span><span class="sxs-lookup"><span data-stu-id="37397-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="37397-117">Validar o VNET do Azure para usar com o RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="37397-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

