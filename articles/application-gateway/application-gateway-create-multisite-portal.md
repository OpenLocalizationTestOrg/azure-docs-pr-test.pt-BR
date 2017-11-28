---
title: "aaaHost vários sites com o Gateway de aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece instruções tooconfigure um gateway existente do aplicativo do Azure para hospedar vários aplicativos web em Olá mesmo gateway com hello portal do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="92deb-103">Configurar um gateway de aplicativo existente para hospedar vários aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="92deb-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="92deb-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92deb-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="92deb-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92deb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="92deb-106">Várias opções de hospedagem de site permite que você toodeploy mais de um aplicativo web em Olá mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92deb-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="92deb-107">Ele depende da presença do cabeçalho de host na solicitação HTTP entrada hello, toodetermine o ouvinte deve receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="92deb-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="92deb-108">ouvinte de Hello, em seguida, direciona o pool de back-end do tráfego tooappropriate conforme configurado na definição de regras de saudação do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="92deb-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="92deb-109">Em aplicativos da web SSL habilitado, o gateway de aplicativo depende Olá indicação de nome de servidor (SNI) extensão toochoose Olá correto ouvinte para o tráfego da web hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="92deb-110">Um uso comum para várias opções de hospedagem de site é equilibrar solicitações de tooload para pools de servidor back-end da web diferentes domínios toodifferent.</span><span class="sxs-lookup"><span data-stu-id="92deb-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="92deb-111">Da mesma forma diversos subdomínios de saudação mesmo domínio raiz também pode ser hospedado em Olá mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92deb-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="92deb-112">Cenário</span><span class="sxs-lookup"><span data-stu-id="92deb-112">Scenario</span></span>

<span data-ttu-id="92deb-113">Em Olá exemplo a seguir, o gateway de aplicativo está servindo tráfego para contoso.com e fabrikam.com com dois grupos de servidor back-end: contoso pool de servidores e pool de servidores da fabrikam.</span><span class="sxs-lookup"><span data-stu-id="92deb-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="92deb-114">Configuração semelhante pode ser usado toohost subdomínios como app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="92deb-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![cenário multissite][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="92deb-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="92deb-116">Before you begin</span></span>

<span data-ttu-id="92deb-117">Esse cenário adiciona o gateway de aplicativo existente do suporte de vários locais tooan.</span><span class="sxs-lookup"><span data-stu-id="92deb-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="92deb-118">toocomplete neste cenário, um gateway existente do aplicativo precisa tooconfigure disponível toobe.</span><span class="sxs-lookup"><span data-stu-id="92deb-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="92deb-119">Visite [criar um gateway de aplicativo usando o portal de saudação](application-gateway-create-gateway-portal.md) toolearn como toocreate um application gateway básico no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="92deb-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="92deb-120">Olá seguem etapas Olá necessário gateway de aplicativo hello tooupdate:</span><span class="sxs-lookup"><span data-stu-id="92deb-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="92deb-121">Crie pools de back-end toouse para cada site.</span><span class="sxs-lookup"><span data-stu-id="92deb-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="92deb-122">Crie um ouvinte para cada site a que o gateway de aplicativo dará suporte.</span><span class="sxs-lookup"><span data-stu-id="92deb-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="92deb-123">Crie regras toomap cada ouvinte com hello apropriado back-end.</span><span class="sxs-lookup"><span data-stu-id="92deb-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="92deb-124">Requisitos</span><span class="sxs-lookup"><span data-stu-id="92deb-124">Requirements</span></span>

* <span data-ttu-id="92deb-125">**Pool de servidores de back-end:** lista de saudação de endereços IP dos servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="92deb-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="92deb-126">endereços IP Hello listado ou devem pertencer a sub-rede da rede virtual toohello ou devem ser um IP público/VIP.</span><span class="sxs-lookup"><span data-stu-id="92deb-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="92deb-127">O FQDN também pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="92deb-127">FQDN can also be used.</span></span>
* <span data-ttu-id="92deb-128">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="92deb-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="92deb-129">Essas configurações são tooa empatado pool e são aplicados tooall servidores no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="92deb-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="92deb-130">**Porta de front-end:** essa porta é a porta pública de saudação que é aberta no gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="92deb-131">Tráfego atinge essa porta e, em seguida, obtém redirecionado tooone de servidores de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="92deb-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="92deb-132">**Ouvinte:** ouvinte Olá tem uma porta de front-end, um protocolo (Http ou Https, esses valores diferenciam maiusculas de minúsculas) e o nome do certificado SSL de saudação (se a configuração de SSL de descarregamento).</span><span class="sxs-lookup"><span data-stu-id="92deb-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="92deb-133">Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.</span><span class="sxs-lookup"><span data-stu-id="92deb-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="92deb-134">**Regra:** regra Olá associa ouvinte hello, pool de servidores de back-end hello e define o tráfego de saudação do pool de servidor back-end deve ser direcionado toowhen que ele atinja um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="92deb-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="92deb-135">As regras são processadas na ordem Olá que estão listados e o tráfego será direcionado por meio de saudação primeira regra correspondente, independentemente de especificidade.</span><span class="sxs-lookup"><span data-stu-id="92deb-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="92deb-136">Por exemplo, se você tiver uma regra usando um ouvinte básico e uma regra usando um ouvinte de multissite ambos em Olá mesma regra de porta, Olá com ouvinte de multissite Olá deverá ser listada antes regra Olá com o ouvinte de saudação básica em ordem para Olá multissite regra toofunction como esperado.</span><span class="sxs-lookup"><span data-stu-id="92deb-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="92deb-137">**Certificados:** cada ouvinte exige um certificado exclusivo; neste exemplo, dois ouvintes são criados para multissite.</span><span class="sxs-lookup"><span data-stu-id="92deb-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="92deb-138">Dois certificados. pfx e senhas Olá para que eles precisam toobe criado.</span><span class="sxs-lookup"><span data-stu-id="92deb-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="92deb-139">Criar pools de back-end para cada site</span><span class="sxs-lookup"><span data-stu-id="92deb-139">Create back-end pools for each site</span></span>

<span data-ttu-id="92deb-140">É necessário um pool de back-end para cada site ao qual esse gateway de aplicativo dá suporte. Neste caso, serão criados dois: um para contoso11.com e outro para fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="92deb-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="92deb-141">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="92deb-141">Step 1</span></span>

<span data-ttu-id="92deb-142">Navegue tooan existente application gateway em hello (https://portal.azure.com) do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92deb-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="92deb-143">Selecione **Pools de back-end** e clique em **Adicionar**</span><span class="sxs-lookup"><span data-stu-id="92deb-143">Select **Backend pools** and click **Add**</span></span>

![adicionar pools do back-end][7]

### <a name="step-2"></a><span data-ttu-id="92deb-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="92deb-145">Step 2</span></span>

<span data-ttu-id="92deb-146">Preencha as informações de saudação para pool de back-end Olá **pool1**, adição de endereços ip de saudação ou FQDNs para servidores de back-end hello e clique em **Okey**</span><span class="sxs-lookup"><span data-stu-id="92deb-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![configurações do pool de back-end pool1][8]

### <a name="step-3"></a><span data-ttu-id="92deb-148">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="92deb-148">Step 3</span></span>

<span data-ttu-id="92deb-149">Na folha de pools de back-end Olá clique **adicionar** tooadd um pool de back-end adicional **pool2**, adição de endereços ip de saudação ou FQDNS para servidores de back-end hello e clique em **Okey**</span><span class="sxs-lookup"><span data-stu-id="92deb-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![configurações do pool de back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="92deb-151">Criar ouvintes para cada back-end</span><span class="sxs-lookup"><span data-stu-id="92deb-151">Create listeners for each back-end</span></span>

<span data-ttu-id="92deb-152">Application Gateway depende do HTTP 1.1 Olá de toohost de cabeçalhos de host com mais de um site da Web no mesmo endereço IP público e a porta.</span><span class="sxs-lookup"><span data-stu-id="92deb-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="92deb-153">ouvinte de básica Olá criada no portal de saudação não contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="92deb-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="92deb-154">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="92deb-154">Step 1</span></span>

<span data-ttu-id="92deb-155">Clique em **ouvintes** Olá gateway de aplicativo existente e clique em **multissite** primeiro ouvinte de saudação tooadd.</span><span class="sxs-lookup"><span data-stu-id="92deb-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![folha de visão geral de ouvintes][1]

### <a name="step-2"></a><span data-ttu-id="92deb-157">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="92deb-157">Step 2</span></span>

<span data-ttu-id="92deb-158">Preencha as informações de saudação para ouvinte hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="92deb-159">Neste exemplo, a terminação SSL está configurada; crie uma nova porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="92deb-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="92deb-160">Carregar toobe de certificado. pfx Olá usado para a terminação SSL.</span><span class="sxs-lookup"><span data-stu-id="92deb-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="92deb-161">a única diferença Olá nesta folha de ouvinte básica padrão toohello folha em comparação comparada é o nome do host hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![folha de propriedades do ouvinte][2]

### <a name="step-3"></a><span data-ttu-id="92deb-163">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="92deb-163">Step 3</span></span>

<span data-ttu-id="92deb-164">Clique em **multissite** e criar outro ouvinte conforme descrito na etapa anterior de saudação para site segundo hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="92deb-165">Verifique toouse-se de que um certificado diferente para o ouvinte segundo hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="92deb-166">a única diferença Olá nesta folha de ouvinte básica padrão toohello folha em comparação comparada é o nome do host hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="92deb-167">Preencha as informações de ouvinte Olá Olá e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="92deb-167">Fill out hello information for hello listener and click **OK**.</span></span>

![folha de propriedades do ouvinte][3]

> [!NOTE]
> <span data-ttu-id="92deb-169">A criação de ouvintes no hello portal do Azure para o application gateway é uma tarefa demorada, pode levar alguns Olá toocreate de tempo dois ouvintes nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="92deb-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="92deb-170">Quando ouvintes Olá completa exibido no portal de saudação visto Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="92deb-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![visão geral do ouvinte][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="92deb-172">Criar regras de pools de toobackend toomap ouvintes</span><span class="sxs-lookup"><span data-stu-id="92deb-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="92deb-173">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="92deb-173">Step 1</span></span>

<span data-ttu-id="92deb-174">Navegue tooan existente application gateway em hello (https://portal.azure.com) do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92deb-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="92deb-175">Selecione **regras** e escolha a regra padrão existente de saudação **rule1** e clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="92deb-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="92deb-176">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="92deb-176">Step 2</span></span>

<span data-ttu-id="92deb-177">Preencha a folha de regras de saudação visto Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="92deb-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="92deb-178">Escolhendo o primeiro ouvinte de saudação e primeiro pool e clicando em **salvar** quando concluir.</span><span class="sxs-lookup"><span data-stu-id="92deb-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![editar regra existente][6]

### <a name="step-3"></a><span data-ttu-id="92deb-180">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="92deb-180">Step 3</span></span>

<span data-ttu-id="92deb-181">Clique em **regra básica** segunda regra do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="92deb-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="92deb-182">Preencha o formulário de saudação com hello segundo ouvinte e o segundo pool back-end e clique em **Okey** toosave.</span><span class="sxs-lookup"><span data-stu-id="92deb-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![adicionar folha de regra básica][10]

<span data-ttu-id="92deb-184">Este cenário conclui Configurando um gateway existente do aplicativo com suporte a vários site por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92deb-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92deb-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92deb-185">Next steps</span></span>

<span data-ttu-id="92deb-186">Saiba como tooprotect seus sites com [Application Gateway - Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="92deb-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
