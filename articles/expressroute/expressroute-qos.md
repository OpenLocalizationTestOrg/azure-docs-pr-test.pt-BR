---
title: Requisitos do ExpressRoute de aaaQoS | Microsoft Docs
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
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="8a703-103">Requisitos de QoS para o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8a703-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="8a703-104">Skype for Business tem várias cargas de trabalho que exigem tratamento de QoS diferenciado.</span><span class="sxs-lookup"><span data-stu-id="8a703-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="8a703-105">Se você planejar serviços de voz tooconsume por meio de rota expressa, você deve seguir toohello requisitos descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="8a703-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="8a703-106">Requisitos de QoS se aplica a toohello emparelhamento da Microsoft somente.</span><span class="sxs-lookup"><span data-stu-id="8a703-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="8a703-107">valores de DSCP Olá em seu tráfego de rede recebido no emparelhamento público do Azure e emparelhamento particular do Azure será too0 de redefinição.</span><span class="sxs-lookup"><span data-stu-id="8a703-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="8a703-108">Olá tabela a seguir fornece uma lista de marcações de DSCP usado pelo Skype for Business.</span><span class="sxs-lookup"><span data-stu-id="8a703-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="8a703-109">Consulte também[gerenciamento de QoS para o Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8a703-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="8a703-110">**Classe de Tráfego**</span><span class="sxs-lookup"><span data-stu-id="8a703-110">**Traffic Class**</span></span> | <span data-ttu-id="8a703-111">**Tratamento (Marcação DSCP)**</span><span class="sxs-lookup"><span data-stu-id="8a703-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="8a703-112">**Cargas de Trabalho do Skype for Business**</span><span class="sxs-lookup"><span data-stu-id="8a703-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a703-113">**Voz**</span><span class="sxs-lookup"><span data-stu-id="8a703-113">**Voice**</span></span> |<span data-ttu-id="8a703-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="8a703-114">EF (46)</span></span> |<span data-ttu-id="8a703-115">Voz do Skype / Lync</span><span class="sxs-lookup"><span data-stu-id="8a703-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="8a703-116">**Interativo**</span><span class="sxs-lookup"><span data-stu-id="8a703-116">**Interactive**</span></span> |<span data-ttu-id="8a703-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="8a703-117">AF41 (34)</span></span> |<span data-ttu-id="8a703-118">Vídeo, VBSS</span><span class="sxs-lookup"><span data-stu-id="8a703-118">Video, VBSS</span></span> |
| <span data-ttu-id="8a703-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="8a703-119">AF21 (18)</span></span> |<span data-ttu-id="8a703-120">Compartilhamento de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8a703-120">App sharing</span></span> | |
| <span data-ttu-id="8a703-121">**Padrão**</span><span class="sxs-lookup"><span data-stu-id="8a703-121">**Default**</span></span> |<span data-ttu-id="8a703-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="8a703-122">AF11 (10)</span></span> |<span data-ttu-id="8a703-123">Transferência de arquivo</span><span class="sxs-lookup"><span data-stu-id="8a703-123">File transfer</span></span> |
| <span data-ttu-id="8a703-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="8a703-124">CS0 (0)</span></span> |<span data-ttu-id="8a703-125">Qualquer outra coisa</span><span class="sxs-lookup"><span data-stu-id="8a703-125">Anything else</span></span> | |

* <span data-ttu-id="8a703-126">Você deve classificar as cargas de trabalho de saudação e marcar os valores de DSCP saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="8a703-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="8a703-127">Siga a orientação Olá fornecida [aqui](https://technet.microsoft.com/library/gg405409.aspx) sobre como as marcações de DSCP tooset em sua rede.</span><span class="sxs-lookup"><span data-stu-id="8a703-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="8a703-128">Você deve configurar e dar suporte a várias filas de QoS em sua rede.</span><span class="sxs-lookup"><span data-stu-id="8a703-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="8a703-129">Voz deve ser uma classe autônoma e receber o tratamento de EF Olá especificado no RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="8a703-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="8a703-130">Você pode decidir Olá mecanismo, a política de detecção de congestionamento e alocação de largura de banda por classe de tráfego de enfileiramento de mensagens.</span><span class="sxs-lookup"><span data-stu-id="8a703-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="8a703-131">Porém, hello DSCP marcando para Skype para cargas de trabalho de negócios deve ser preservado.</span><span class="sxs-lookup"><span data-stu-id="8a703-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="8a703-132">Se você estiver usando marcas DSCP não listadas acima, por exemplo, AF31 (26), você deve reescrever esse too0 do valor DSCP antes de enviar Olá tooMicrosoft de pacote.</span><span class="sxs-lookup"><span data-stu-id="8a703-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="8a703-133">Microsoft envia somente pacotes marcados com hello valor DSCP mostrado no hello acima da tabela.</span><span class="sxs-lookup"><span data-stu-id="8a703-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8a703-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a703-134">Next steps</span></span>
* <span data-ttu-id="8a703-135">Consulte os requisitos de toohello para [roteamento](expressroute-routing.md) e [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="8a703-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="8a703-136">Veja a seguir Olá links tooconfigure sua conexão de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="8a703-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="8a703-137">Criar um circuito do ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8a703-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="8a703-138">Configurar o roteamento</span><span class="sxs-lookup"><span data-stu-id="8a703-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="8a703-139">Vincular um circuito de rota expressa do tooan de rede virtual</span><span class="sxs-lookup"><span data-stu-id="8a703-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

