---
title: "usando o Azure Traffic Manager do método de roteamento de tráfego de desempenho aaaConfigure | Microsoft Docs"
description: "Este artigo explica como tooconfigure tooroute Traffic Manager tráfego toohello de ponto de extremidade com a menor latência"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="de6cc-103">Configurar o método de roteamento de tráfego Olá desempenho</span><span class="sxs-lookup"><span data-stu-id="de6cc-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="de6cc-104">Olá método de roteamento de tráfego de desempenho permite ponto de extremidade do toodirect tráfego toohello com a menor latência Olá da rede saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="de6cc-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="de6cc-105">Normalmente, Olá datacenter com a menor latência de saudação é hello mais próximo na distância geográfica.</span><span class="sxs-lookup"><span data-stu-id="de6cc-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="de6cc-106">Esse método de roteamento de tráfego não consegue considerar as alterações em tempo real à configuração ou à carga de rede.</span><span class="sxs-lookup"><span data-stu-id="de6cc-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="de6cc-107">método de roteamento de desempenho tooconfigure</span><span class="sxs-lookup"><span data-stu-id="de6cc-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="de6cc-108">Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de6cc-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="de6cc-109">Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="de6cc-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="de6cc-110">Na barra de pesquisa do portal hello, procure Olá **perfis do Traffic Manager** e clique em nome do perfil Olá que você deseja que o método de roteamento de saudação tooconfigure para.</span><span class="sxs-lookup"><span data-stu-id="de6cc-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="de6cc-111">Em Olá **perfil do Traffic Manager** folha, verifique se ambos Olá serviços de nuvem e sites que você deseja tooinclude em sua configuração estão presentes.</span><span class="sxs-lookup"><span data-stu-id="de6cc-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="de6cc-112">Em Olá **configurações** seção, clique em **configuração**e em Olá **configuração** folha, completa, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="de6cc-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="de6cc-113">Em **Configurações do método de roteamento de tráfego**, para **Método de roteamento** selecione **Desempenho**.</span><span class="sxs-lookup"><span data-stu-id="de6cc-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="de6cc-114">Saudação de conjunto **as configurações do monitor de ponto de extremidade** idênticos para todos os cada ponto de extremidade neste perfil da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="de6cc-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="de6cc-115">Selecione Olá apropriado **protocolo**e especifique Olá **porta** número.</span><span class="sxs-lookup"><span data-stu-id="de6cc-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="de6cc-116">Para **Caminho**, digite uma barra "/" */*.</span><span class="sxs-lookup"><span data-stu-id="de6cc-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="de6cc-117">pontos de extremidade toomonitor, você deve especificar um caminho e nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="de6cc-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="de6cc-118">A barra "/" é uma entrada válida para o caminho relativo do hello e indica se o arquivo hello está no diretório raiz de saudação (padrão).</span><span class="sxs-lookup"><span data-stu-id="de6cc-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="de6cc-119">Na parte superior de saudação da página de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="de6cc-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="de6cc-120">Teste alterações de saudação em sua configuração da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="de6cc-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="de6cc-121">Na barra de pesquisa do portal Olá, procurar por nome de perfil do Traffic Manager hello e clique em perfil do Traffic Manager Olá nos resultados de saudação que Olá exibido.</span><span class="sxs-lookup"><span data-stu-id="de6cc-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="de6cc-122">Em Olá **Traffic Manager** folha de perfil, clique em **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="de6cc-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="de6cc-123">Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado.</span><span class="sxs-lookup"><span data-stu-id="de6cc-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="de6cc-124">Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello.</span><span class="sxs-lookup"><span data-stu-id="de6cc-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="de6cc-125">Nesse caso, todas as solicitações são toohello roteado de ponto de extremidade com a menor latência Olá da rede saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="de6cc-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="de6cc-126">Depois que o perfil do Traffic Manager está funcionando, edite o registro DNS de saudação no seu toopoint de servidor DNS autoritativo seu nome de domínio da empresa domínio nome toohello Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="de6cc-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Configurando o método de roteamento de tráfego de desempenho usando o Gerenciador de Tráfego][1]

## <a name="next-steps"></a><span data-ttu-id="de6cc-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="de6cc-128">Next steps</span></span>

- <span data-ttu-id="de6cc-129">Saiba mais sobre o [método de roteamento de tráfego ponderado](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="de6cc-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="de6cc-130">Saiba mais sobre o [método de roteamento de prioridade](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="de6cc-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="de6cc-131">Saiba mais sobre o [método de roteamento geográfico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="de6cc-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="de6cc-132">Saiba como muito[testar as configurações do Gerenciador de tráfego](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="de6cc-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png