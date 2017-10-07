---
title: "informações de aaaSizing para uma rede virtual no Azure RemoteApp | Microsoft Docs"
description: "Saiba mais sobre os requisitos de endereço IP da saudação do Azure RemoteApp em execução com uma rede virtual"
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="f4cea-103">Dimensionamento de informações de um VNET no RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="f4cea-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f4cea-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f4cea-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f4cea-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f4cea-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f4cea-106">Quando você usa o Azure RemoteApp com uma rede virtual (VNET), o RemoteApp usa endereços IP de sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="f4cea-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="f4cea-107">Com base em escala de saudação do seu serviço RemoteApp, é necessário tooensure sua sub-rede tem endereços IP suficientes disponíveis para máquinas virtuais de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f4cea-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="f4cea-108">Embora essa orientação de dimensionamento não seja perfeita, visto o modo como o RemoteApp faz a rotação dinâmica de máquinas virtuais para cima e para baixo dentro de uma coleção, ele ajudará a calcular o intervalo de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f4cea-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="f4cea-109">Isso é especialmente importante que, quando um serviço do RemoteApp é colocado em uma rede virtual, não é possível aumentar o tamanho da sub-rede Olá sem remover o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f4cea-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="f4cea-110">Para cada coleção do RemoteApp que você deseja toorun na capacidade máxima, você deve ter 100 endereços IP disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f4cea-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="f4cea-111">Por exemplo, se você tiver uma coleção do RemoteApp no plano de saudação padrão e deseja toohave Olá máximo 500 usuários, você deve ter 100 endereços IP para essa coleção.</span><span class="sxs-lookup"><span data-stu-id="f4cea-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="f4cea-112">Da mesma forma, você precisa 100 endereços IP para uma coleção do RemoteApp no plano básico de saudação com 800 usuários.</span><span class="sxs-lookup"><span data-stu-id="f4cea-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="f4cea-113">Se você planejar toohave menos usuários (menor que o máximo de saudação), você pode reduzir a endereços IP hello necessários por coleção.</span><span class="sxs-lookup"><span data-stu-id="f4cea-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="f4cea-114">requisito de tamanho mínimo de sub-rede Olá é 30 endereços IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="f4cea-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="f4cea-115">Check-out Olá seguindo informações toomake-se de que sua rede virtual está configurada e funcionando propertly:</span><span class="sxs-lookup"><span data-stu-id="f4cea-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="f4cea-116">Migrar de uma tooan de rede virtual pessoal VNET do Azure</span><span class="sxs-lookup"><span data-stu-id="f4cea-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="f4cea-117">Validar Olá toouse de rede virtual do Azure com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f4cea-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

