---
title: "Lista de Portas e URLs para colocar na lista de permissões do Azure RemoteApp implantado na rede virtual do cliente | Microsoft Docs"
description: "Saiba quais portas e URLs você precisará configurar para comunicação por meio do RemoteApp do Azure."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="5e8d0-103">Lista de URLs e Portas para permitir o acesso para o Azure RemoteApp implantado na Rede Virtual do cliente</span><span class="sxs-lookup"><span data-stu-id="5e8d0-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5e8d0-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="5e8d0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5e8d0-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5e8d0-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5e8d0-106">Se você estiver implantando uma nuvem ou coleção híbrida do Azure RemoteApp em uma rede virtual (VNET), examine as informações sobre as portas apresentadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e8d0-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="5e8d0-107">Para obter mais informações sobre redes virtuais, consulte [Visão Geral da Rede Virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e8d0-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="5e8d0-108">Se você tiver criado um NSG (grupo de segurança de rede) restringindo o tráfego para os recursos da rede virtual na coleção, verifique se as portas a seguir estão acessíveis e têm permissão por meio das políticas de segurança na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5e8d0-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="5e8d0-109">Para obter mais informações sobre grupos de segurança de rede, consulte [O que é um Grupo de Segurança de Rede? (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="5e8d0-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="5e8d0-110">A sub-rede do RemoteApp do Azure precisa de acesso a esses pontos de extremidade e URLs:</span><span class="sxs-lookup"><span data-stu-id="5e8d0-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="5e8d0-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="5e8d0-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="5e8d0-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="5e8d0-112">*.servicebus.net</span></span>
* <span data-ttu-id="5e8d0-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="5e8d0-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="5e8d0-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="5e8d0-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="5e8d0-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="5e8d0-117">Saída: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="5e8d0-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="5e8d0-118">Opcional – UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="5e8d0-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="5e8d0-119">Os clientes do RemoteApp do Azure precisam de acesso a esses pontos de extremidade e URLs:</span><span class="sxs-lookup"><span data-stu-id="5e8d0-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="5e8d0-120">Por clientes, quero dizer desktops, dispositivos etc. que as pessoas usam para se conectar aos aplicativos implantados na coleção de RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e8d0-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="5e8d0-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="5e8d0-122">https://*.remoteapp.windowsazure.com (as portas UDP opcionais são para esse endereço)</span><span class="sxs-lookup"><span data-stu-id="5e8d0-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="5e8d0-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="5e8d0-123">https://login.windows.net</span></span>  
* <span data-ttu-id="5e8d0-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="5e8d0-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="5e8d0-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="5e8d0-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="5e8d0-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="5e8d0-127">Saída: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="5e8d0-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="5e8d0-128">Opcional - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="5e8d0-128">Optional - UDP: 3391</span></span> 

