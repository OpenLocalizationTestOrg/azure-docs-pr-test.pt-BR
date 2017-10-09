---
title: "usando o Azure Traffic Manager do método de roteamento de tráfego aaaConfigure weighted round robin | Microsoft Docs"
description: "Este artigo explica como tooload equilibrar o tráfego usando um método round robin no Gerenciador de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="0ff85-103">Configurar o método de roteamento de tráfego Olá ponderada no Gerenciador de tráfego</span><span class="sxs-lookup"><span data-stu-id="0ff85-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="0ff85-104">Um padrão de comum método de roteamento do tráfego é tooprovide um conjunto de pontos de extremidade idênticos, que incluem serviços de nuvem e sites e enviar tráfego tooeach em uma forma round-robin.</span><span class="sxs-lookup"><span data-stu-id="0ff85-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="0ff85-105">Olá, as etapas a seguir descrevem como tooconfigure desse tipo de método de roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="0ff85-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="0ff85-106">Os sites do Azure já fornecem funcionalidade de balanceamento de carga round robin para sites dentro de um data center (também conhecido como região).</span><span class="sxs-lookup"><span data-stu-id="0ff85-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="0ff85-107">O Traffic Manager permite que você toospecify método de roteamento de tráfego de round-robin para sites em data centers diferentes.</span><span class="sxs-lookup"><span data-stu-id="0ff85-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="0ff85-108">método de roteamento de tráfego tooconfigure Olá ponderada</span><span class="sxs-lookup"><span data-stu-id="0ff85-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="0ff85-109">Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ff85-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="0ff85-110">Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0ff85-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="0ff85-111">Na barra de pesquisa do portal hello, procure Olá **perfis do Traffic Manager** e clique em nome do perfil Olá que você deseja que o método de roteamento de saudação tooconfigure para.</span><span class="sxs-lookup"><span data-stu-id="0ff85-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="0ff85-112">Em Olá **perfil do Traffic Manager** folha, verifique se ambos Olá serviços de nuvem e sites que você deseja tooinclude em sua configuração estão presentes.</span><span class="sxs-lookup"><span data-stu-id="0ff85-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="0ff85-113">Em Olá **configurações** seção, clique em **configuração**e em Olá **configuração** folha, completa, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0ff85-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="0ff85-114">Para **configurações do método de roteamento de tráfego**, verifique se o método de roteamento de tráfego Olá é **ponderado**.</span><span class="sxs-lookup"><span data-stu-id="0ff85-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="0ff85-115">Se não estiver, clique em **ponderado** na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="0ff85-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="0ff85-116">Saudação de conjunto **as configurações do monitor de ponto de extremidade** idênticos para todos os cada ponto de extremidade neste perfil da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0ff85-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="0ff85-117">Selecione Olá apropriado **protocolo**e especifique Olá **porta** número.</span><span class="sxs-lookup"><span data-stu-id="0ff85-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="0ff85-118">Para **Caminho**, digite uma barra "/" */*.</span><span class="sxs-lookup"><span data-stu-id="0ff85-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="0ff85-119">pontos de extremidade toomonitor, você deve especificar um caminho e nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="0ff85-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="0ff85-120">A barra "/" é uma entrada válida para o caminho relativo do hello e indica se o arquivo hello está no diretório raiz de saudação (padrão).</span><span class="sxs-lookup"><span data-stu-id="0ff85-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="0ff85-121">Na parte superior de saudação da página de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0ff85-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="0ff85-122">Teste alterações de saudação em sua configuração da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0ff85-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="0ff85-123">Na barra de pesquisa do portal Olá, procurar por nome de perfil do Traffic Manager hello e clique em perfil do Traffic Manager Olá nos resultados de saudação que Olá exibido.</span><span class="sxs-lookup"><span data-stu-id="0ff85-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="0ff85-124">Em Olá **Traffic Manager** folha de perfil, clique em **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="0ff85-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="0ff85-125">Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado.</span><span class="sxs-lookup"><span data-stu-id="0ff85-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="0ff85-126">Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="0ff85-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="0ff85-127">Nesse caso, todas as solicitações são roteadas para cada ponto de extremidade da em round robin.</span><span class="sxs-lookup"><span data-stu-id="0ff85-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="0ff85-128">Depois que o perfil do Traffic Manager está funcionando, edite o registro DNS de saudação no seu toopoint de servidor DNS autoritativo seu nome de domínio da empresa domínio nome toohello Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="0ff85-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Configurando o método de roteamento de tráfego ponderado usando o Gerenciador de Tráfego][1]

## <a name="next-steps"></a><span data-ttu-id="0ff85-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ff85-130">Next steps</span></span>

- <span data-ttu-id="0ff85-131">Saiba mais sobre o [método de roteamento de tráfego de prioridade](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="0ff85-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="0ff85-132">Saiba mais sobre o [método de roteamento de tráfego de desempenho](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="0ff85-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="0ff85-133">Saiba mais sobre o [método de roteamento geográfico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="0ff85-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="0ff85-134">Saiba como muito[testar as configurações do Gerenciador de tráfego](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="0ff85-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
