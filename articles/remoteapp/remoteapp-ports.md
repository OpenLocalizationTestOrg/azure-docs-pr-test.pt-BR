---
title: aaaList de toowhitelist URLs e portas para o Azure RemoteApp implantado na rede virtual do cliente | Microsoft Docs
description: "Saiba quais portas e URLs, você precisará tooconfigure para comunicação por meio do Azure RemoteApp."
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="ee0e5-103">Lista de URLs e portas de acesso de toopermit para o Azure RemoteApp implantado no cliente de rede Virtual</span><span class="sxs-lookup"><span data-stu-id="ee0e5-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee0e5-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ee0e5-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ee0e5-106">Se você estiver implantando uma coleção de nuvem ou híbrida do RemoteApp do Azure em uma rede virtual (VNET), examine Olá informações de porta a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="ee0e5-107">Para obter mais informações sobre redes virtuais, consulte [Visão Geral da Rede Virtual](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee0e5-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="ee0e5-108">Se você tiver criado um grupo de segurança de rede (NSG) restringindo os recursos de rede virtual do tráfego toohello em sua coleção, certifique-se de saudação portas a seguir é permitidas por meio de políticas de segurança de saudação na rede virtual hello e acessível.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="ee0e5-109">Para obter mais informações sobre grupos de segurança de rede, consulte [O que é um Grupo de Segurança de Rede? (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="ee0e5-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="ee0e5-110">Sub-rede RemoteApp do Azure precisa de pontos de extremidade do acesso toothese e URLs:</span><span class="sxs-lookup"><span data-stu-id="ee0e5-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="ee0e5-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee0e5-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="ee0e5-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="ee0e5-112">*.servicebus.net</span></span>
* <span data-ttu-id="ee0e5-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="ee0e5-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="ee0e5-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="ee0e5-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee0e5-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="ee0e5-117">Saída: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="ee0e5-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="ee0e5-118">Opcional – UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="ee0e5-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="ee0e5-119">Clientes do RemoteApp do Azure precisam acessar pontos de extremidade de toothese e URLs:</span><span class="sxs-lookup"><span data-stu-id="ee0e5-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="ee0e5-120">Por clientes que quero dizer Olá desktops, dispositivos etc. que as pessoas use tooconnect toohello aplicativos implantados em Olá coleção do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee0e5-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="ee0e5-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="ee0e5-122">https://*.RemoteApp.WindowsAzure.com (portas UDP opcionais de saudação são para esse endereço)</span><span class="sxs-lookup"><span data-stu-id="ee0e5-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="ee0e5-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee0e5-123">https://login.windows.net</span></span>  
* <span data-ttu-id="ee0e5-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="ee0e5-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="ee0e5-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="ee0e5-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee0e5-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="ee0e5-127">Saída: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="ee0e5-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="ee0e5-128">Opcional - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="ee0e5-128">Optional - UDP: 3391</span></span> 

