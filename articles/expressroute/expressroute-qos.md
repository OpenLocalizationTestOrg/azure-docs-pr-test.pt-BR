---
title: Requisitos de QoS para ExpressRoute | Microsoft Docs
description: "Esta página fornece requisitos detalhados para a configuração e gerenciamento de QoS para circuitos do ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="96f7a-103">Requisitos de QoS para o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="96f7a-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="96f7a-104">Skype for Business tem várias cargas de trabalho que exigem tratamento de QoS diferenciado.</span><span class="sxs-lookup"><span data-stu-id="96f7a-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="96f7a-105">Se você planeja utilizar serviços de voz por meio de ExpressRoute, siga os requisitos descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="96f7a-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="96f7a-106">Os requisitos de QoS aplicam-se somente ao emparelhamento Microsoft.</span><span class="sxs-lookup"><span data-stu-id="96f7a-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="96f7a-107">Os valores de DSCP no tráfego de rede recebido no emparelhamento público e no emparelhamento privado do Azure serão redefinidos como 0.</span><span class="sxs-lookup"><span data-stu-id="96f7a-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="96f7a-108">A tabela a seguir fornece uma lista de marcações DSCP usadas pelo Skype for Business.</span><span class="sxs-lookup"><span data-stu-id="96f7a-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="96f7a-109">Para obter mais informações, consulte [Gerenciamento de QoS para Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) .</span><span class="sxs-lookup"><span data-stu-id="96f7a-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="96f7a-110">**Classe de Tráfego**</span><span class="sxs-lookup"><span data-stu-id="96f7a-110">**Traffic Class**</span></span> | <span data-ttu-id="96f7a-111">**Tratamento (Marcação DSCP)**</span><span class="sxs-lookup"><span data-stu-id="96f7a-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="96f7a-112">**Cargas de Trabalho do Skype for Business**</span><span class="sxs-lookup"><span data-stu-id="96f7a-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96f7a-113">**Voz**</span><span class="sxs-lookup"><span data-stu-id="96f7a-113">**Voice**</span></span> |<span data-ttu-id="96f7a-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="96f7a-114">EF (46)</span></span> |<span data-ttu-id="96f7a-115">Voz do Skype / Lync</span><span class="sxs-lookup"><span data-stu-id="96f7a-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="96f7a-116">**Interativo**</span><span class="sxs-lookup"><span data-stu-id="96f7a-116">**Interactive**</span></span> |<span data-ttu-id="96f7a-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="96f7a-117">AF41 (34)</span></span> |<span data-ttu-id="96f7a-118">Vídeo, VBSS</span><span class="sxs-lookup"><span data-stu-id="96f7a-118">Video, VBSS</span></span> |
| <span data-ttu-id="96f7a-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="96f7a-119">AF21 (18)</span></span> |<span data-ttu-id="96f7a-120">Compartilhamento de aplicativo</span><span class="sxs-lookup"><span data-stu-id="96f7a-120">App sharing</span></span> | |
| <span data-ttu-id="96f7a-121">**Padrão**</span><span class="sxs-lookup"><span data-stu-id="96f7a-121">**Default**</span></span> |<span data-ttu-id="96f7a-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="96f7a-122">AF11 (10)</span></span> |<span data-ttu-id="96f7a-123">Transferência de arquivo</span><span class="sxs-lookup"><span data-stu-id="96f7a-123">File transfer</span></span> |
| <span data-ttu-id="96f7a-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="96f7a-124">CS0 (0)</span></span> |<span data-ttu-id="96f7a-125">Qualquer outra coisa</span><span class="sxs-lookup"><span data-stu-id="96f7a-125">Anything else</span></span> | |

* <span data-ttu-id="96f7a-126">Você deve classificar as cargas de trabalho e marcar os valores DSCP corretos.</span><span class="sxs-lookup"><span data-stu-id="96f7a-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="96f7a-127">Siga as orientações fornecidas [aqui](https://technet.microsoft.com/library/gg405409.aspx) sobre como definir as marcações de DSCP em sua rede.</span><span class="sxs-lookup"><span data-stu-id="96f7a-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="96f7a-128">Você deve configurar e dar suporte a várias filas de QoS em sua rede.</span><span class="sxs-lookup"><span data-stu-id="96f7a-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="96f7a-129">Voz deve ser uma classe autônoma e receber o tratamento de EF especificado no RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="96f7a-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="96f7a-130">Você pode decidir o mecanismo de enfileiramento, a política de detecção de congestionamento e a alocação de largura de banda por classe de tráfego.</span><span class="sxs-lookup"><span data-stu-id="96f7a-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="96f7a-131">Porém, a marcação DSCP para cargas de trabalho do Skype for Business deve ser preservada.</span><span class="sxs-lookup"><span data-stu-id="96f7a-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="96f7a-132">Se você estiver usando marcas DSCP não listadas acima, por exemplo, AF31 (26), você deve reescrever esse valor DSCP para 0 antes de enviar o pacote para a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="96f7a-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="96f7a-133">A Microsoft envia somente pacotes marcados com o valor DSCP mostrado na tabela acima.</span><span class="sxs-lookup"><span data-stu-id="96f7a-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="96f7a-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96f7a-134">Next steps</span></span>
* <span data-ttu-id="96f7a-135">Consulte os requisitos para [Roteamento](expressroute-routing.md) e [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="96f7a-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="96f7a-136">Consulte os links a seguir para configurar a conexão do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="96f7a-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="96f7a-137">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="96f7a-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="96f7a-138">Configurar o roteamento</span><span class="sxs-lookup"><span data-stu-id="96f7a-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="96f7a-139">Vincular uma rede virtual a um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="96f7a-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

