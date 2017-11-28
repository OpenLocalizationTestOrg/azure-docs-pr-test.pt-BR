---
title: "Visão geral do balanceador de carga para a Internet | Microsoft Docs"
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="c4166-104">Visão geral do balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="c4166-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="c4166-105">O balanceador de carga do Azure mapeia o endereço IP público e o número da porta do tráfego de entrada até o endereço IP privado e o número da porta da máquina virtual e vice-versa no tráfego de resposta da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4166-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="c4166-106">As regras de balanceamento de carga permitem que você distribua tipos específicos de tráfego entre várias máquinas virtuais ou serviços.</span><span class="sxs-lookup"><span data-stu-id="c4166-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="c4166-107">Por exemplo, você pode difundir a carga de tráfego de solicitação da web em vários servidores web ou funções web.</span><span class="sxs-lookup"><span data-stu-id="c4166-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="c4166-108">Para um serviço de nuvem que contenha instâncias de funções web ou funções de trabalho, você pode definir um ponto de extremidade público no arquivo de definição de serviço (.csdef).</span><span class="sxs-lookup"><span data-stu-id="c4166-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="c4166-109">O arquivo *servicedefinition.csdef* contém a configuração do ponto de extremidade e quando existem várias instâncias de função para uma implantação de função de trabalho ou da Web, o balanceador de carga é instalado para ele.</span><span class="sxs-lookup"><span data-stu-id="c4166-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="c4166-110">A maneira de adicionar instâncias à sua implantação de nuvem está alterando a contagem de instâncias no arquivo de configuração de serviço (.csfg).</span><span class="sxs-lookup"><span data-stu-id="c4166-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="c4166-111">A figura a seguir mostra um ponto de extremidade de balanceamento de carga para tráfego na Web compartilhado entre três máquinas virtuais para a porta TCP pública e privada de número 80.</span><span class="sxs-lookup"><span data-stu-id="c4166-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="c4166-112">Essas três máquinas virtuais estão em um conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="c4166-112">These three virtual machines are in a load-balanced set.</span></span>

![exemplo de balanceador de carga público](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="c4166-114">Figura 1 – Ponto de extremidade com balanceamento de carga para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="c4166-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="c4166-115">Quando os clientes da Internet enviam solicitações de página da Web para o endereço IP público do serviço de nuvem na porta TCP 80, o Azure Load Balancer distribui as solicitações entre as três máquinas virtuais no conjunto de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="c4166-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="c4166-116">Para obter mais informações sobre os algoritmos do balanceador de carga, consulte a [load balancer overview page (página de visão geral do balanceador de carga)](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="c4166-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="c4166-117">Por padrão, Azure Load Balancer distribui o tráfego de rede igualmente entre várias instâncias da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4166-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="c4166-118">Também é possível configurar a afinidade de sessão. Para obter mais informações, consulte [load balancer distribution mode (modo de distribuição do balanceador de carga)](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="c4166-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4166-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4166-119">Next steps</span></span>

<span data-ttu-id="c4166-120">Saiba mais sobre [Balanceadores de carga internos](load-balancer-internal-overview.md) para entender melhor qual balanceador de carga é mais adequado para sua implantação na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c4166-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="c4166-121">Também é possível [começar a criar um balanceador de carga para a Internet](load-balancer-get-started-internet-arm-ps.md) e configurar o tipo de [modo de distribuição](load-balancer-distribution-mode.md) para um comportamento específico de tráfego de rede do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c4166-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="c4166-122">Se seu aplicativo precisar manter conexões ativas para servidores por trás de um balanceador de carga, você poderá entender mais sobre as [configurações de tempo limite de TCP ocioso para um balanceador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="c4166-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="c4166-123">Assim, você saberá mais sobre o comportamento da conexão ociosa quando estiver usando um Balanceador de Carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4166-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
