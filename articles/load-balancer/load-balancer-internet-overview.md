---
title: "aaaInternet voltado para a visão geral do balanceador de carga | Microsoft Docs"
description: "Visão geral do balanceador de carga para a Internet e seus recursos. Como um balanceador de carga funciona no Azure usando máquinas virtuais e serviços de nuvem."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="91876-104">Visão geral do balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="91876-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="91876-105">Balanceador de carga do Azure mapeia Olá público IP endereço e número da porta de entrada tráfego toohello privado IP endereço e número da porta da máquina virtual de saudação e vice-versa para o tráfego de resposta de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="91876-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="91876-106">Regras de balanceamento de carga permitem que você toodistribute a tipos específicos de tráfego entre várias máquinas virtuais ou serviços.</span><span class="sxs-lookup"><span data-stu-id="91876-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="91876-107">Por exemplo, você pode distribuir a carga de saudação do tráfego de solicitação da web em vários servidores web ou funções da web.</span><span class="sxs-lookup"><span data-stu-id="91876-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="91876-108">Para um serviço de nuvem que contém as instâncias de funções web ou funções de trabalho, você pode definir um ponto de extremidade público no arquivo de definição (. csdef) do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="91876-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="91876-109">Olá *servicedefinition. csdef* arquivo contém a configuração de ponto de extremidade hello e quando você tiver várias instâncias de função para uma implantação de função web ou de trabalho, o balanceador de carga Olá será instalado para ele.</span><span class="sxs-lookup"><span data-stu-id="91876-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="91876-110">implantação em nuvem Olá maneira tooadd instâncias tooyour é alterar a contagem de instâncias de saudação do arquivo de configuração de serviço hello (. csfg).</span><span class="sxs-lookup"><span data-stu-id="91876-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="91876-111">Olá figura a seguir mostra um ponto de extremidade com balanceamento de carga no tráfego da web que é compartilhado entre três máquinas virtuais para Olá pública e privada a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="91876-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="91876-112">Essas três máquinas virtuais estão em um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="91876-112">These three virtual machines are in a load-balanced set.</span></span>

![exemplo de balanceador de carga público](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="91876-114">Figura 1 – Ponto de extremidade com balanceamento de carga para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="91876-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="91876-115">Quando os clientes da Internet enviam solicitações de página da web toohello de endereço IP público do serviço de nuvem Olá na porta TCP 80, Olá balanceador de carga do Azure distribui as solicitações de saudação entre Olá três máquinas virtuais em conjunto com balanceamento de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="91876-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="91876-116">Para obter mais informações sobre algoritmos de Balanceador de carga, consulte Olá [página de visão geral do balanceador de carga](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="91876-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="91876-117">Por padrão, Azure Load Balancer distribui o tráfego de rede igualmente entre várias instâncias da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="91876-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="91876-118">Também é possível configurar a afinidade de sessão. Para obter mais informações, consulte [load balancer distribution mode (modo de distribuição do balanceador de carga)](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="91876-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91876-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91876-119">Next steps</span></span>

<span data-ttu-id="91876-120">Saiba mais sobre [balanceador de carga interno](load-balancer-internal-overview.md) toobetter entender qual balanceador de carga é uma escolha melhor para sua implantação de nuvem.</span><span class="sxs-lookup"><span data-stu-id="91876-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="91876-121">Também é possível [começar a criar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="91876-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="91876-122">Se seu aplicativo precisa tookeep conexões ativo para os servidores atrás de um balanceador de carga, você pode saber mais sobre [ocioso configurações de tempo limite TCP para um balanceador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="91876-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="91876-123">Ele ajudará toolearn sobre o comportamento de conexão ociosa, quando você estiver usando um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="91876-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
