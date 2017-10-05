---
title: "Hospedar vários sites com o Gateway de Aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece instruções para configurar um gateway de aplicativo do Azure existente para hospedar vários aplicativos Web no mesmo gateway com o portal do Azure."
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
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="37665-103">Configurar um gateway de aplicativo existente para hospedar vários aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="37665-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="37665-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="37665-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="37665-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37665-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="37665-106">A hospedagem de vários sites permite que você implante mais de um aplicativo Web no mesmo gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37665-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="37665-107">Ela depende da presença do cabeçalho de host na solicitação HTTP de entrada, para determinar quais ouvintes devem receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="37665-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="37665-108">O ouvinte, em seguida, direciona o tráfego ao pool de back-end apropriado conforme configurado na definição de regras do gateway.</span><span class="sxs-lookup"><span data-stu-id="37665-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="37665-109">No caso de aplicativos Web habilitados com SSL, o gateway de aplicativo depende da extensão de SNI (Indicação de Nome de Servidor) para escolher o ouvinte correto para o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="37665-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="37665-110">Um uso comum para a hospedagem de vários sites é balancear a carga das solicitações para domínios da Web diferentes para pools de servidor back-end diferentes.</span><span class="sxs-lookup"><span data-stu-id="37665-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="37665-111">Da mesma forma, vários subdomínios do mesmo domínio raiz também podem ser hospedados no mesmo Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37665-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="37665-112">Cenário</span><span class="sxs-lookup"><span data-stu-id="37665-112">Scenario</span></span>

<span data-ttu-id="37665-113">No exemplo a seguir, o gateway de aplicativo está fornecendo o tráfego para contoso.com e fabrikam.com com dois pools de servidor back-end: o pool de servidores contoso e o pool de servidores fabrikam.</span><span class="sxs-lookup"><span data-stu-id="37665-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="37665-114">É possível usar uma configuração semelhante para hospedar subdomínios, como app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="37665-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![cenário multissite][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="37665-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="37665-116">Before you begin</span></span>

<span data-ttu-id="37665-117">Esse cenário adiciona suporte multissite a um gateway de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="37665-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="37665-118">Para concluir esse cenário, um gateway de aplicativo existente precisa estar disponível para configuração.</span><span class="sxs-lookup"><span data-stu-id="37665-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="37665-119">Acesse [Criar um Gateway de Aplicativo usando o portal](application-gateway-create-gateway-portal.md) para aprender a criar um gateway de aplicativo básico no portal.</span><span class="sxs-lookup"><span data-stu-id="37665-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="37665-120">A seguir estão as etapas necessárias para atualizar o gateway de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="37665-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="37665-121">Crie pools de back-end para usar para cada site.</span><span class="sxs-lookup"><span data-stu-id="37665-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="37665-122">Crie um ouvinte para cada site a que o gateway de aplicativo dará suporte.</span><span class="sxs-lookup"><span data-stu-id="37665-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="37665-123">Crie regras para mapear cada ouvinte com o back-end apropriado.</span><span class="sxs-lookup"><span data-stu-id="37665-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="37665-124">Requisitos</span><span class="sxs-lookup"><span data-stu-id="37665-124">Requirements</span></span>

* <span data-ttu-id="37665-125">**Pool de servidores back-end:** a lista de endereços IP dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="37665-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="37665-126">Os endereços IP listados devem pertencer à sub-rede da rede virtual ou devem ser um IP/VIP público.</span><span class="sxs-lookup"><span data-stu-id="37665-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="37665-127">O FQDN também pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="37665-127">FQDN can also be used.</span></span>
* <span data-ttu-id="37665-128">**Configurações do pool de servidores back-end:** cada pool tem configurações como porta, protocolo e afinidade baseada em cookie.</span><span class="sxs-lookup"><span data-stu-id="37665-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="37665-129">Essas configurações são vinculadas a um pool e aplicadas a todos os servidores no pool.</span><span class="sxs-lookup"><span data-stu-id="37665-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="37665-130">**Porta front-end:** essa porta é a porta pública aberta no gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37665-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="37665-131">O tráfego atinge essa porta e é redirecionado para um dos servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="37665-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="37665-132">**Ouvinte:** o ouvinte tem uma porta front-end, um protocolo (HTTP ou HTTPS, esses valores diferenciam maiúsculas de minúsculas) e o nome do certificado SSL (caso esteja configurando o descarregamento SSL).</span><span class="sxs-lookup"><span data-stu-id="37665-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="37665-133">Para Application Gateways habilitados para vários sites, os indicadores de SNI e nome do host também são adicionados.</span><span class="sxs-lookup"><span data-stu-id="37665-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="37665-134">**Regra:** a regra vincula o ouvinte e o pool de servidores back-end e define a qual pool de servidores back-end o tráfego deve ser direcionado ao atingir um ouvinte específico.</span><span class="sxs-lookup"><span data-stu-id="37665-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="37665-135">As regras são processadas na ordem em que são listadas e o tráfego será direcionado por meio da primeira regra correspondente, independentemente de especificidade.</span><span class="sxs-lookup"><span data-stu-id="37665-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="37665-136">Por exemplo, se você tiver uma regra usando um ouvinte básico e outra usando um ouvinte multissite, ambas na mesma porta, a regra com o ouvinte multissite deverá ser listada antes daquela com o ouvinte básico, para que a função multissite funcione conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="37665-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="37665-137">**Certificados:** cada ouvinte exige um certificado exclusivo; neste exemplo, dois ouvintes são criados para multissite.</span><span class="sxs-lookup"><span data-stu-id="37665-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="37665-138">Dois certificados .pfx e as respectivas senhas precisam ser criados.</span><span class="sxs-lookup"><span data-stu-id="37665-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="37665-139">Criar pools de back-end para cada site</span><span class="sxs-lookup"><span data-stu-id="37665-139">Create back-end pools for each site</span></span>

<span data-ttu-id="37665-140">É necessário um pool de back-end para cada site ao qual esse gateway de aplicativo dá suporte. Neste caso, serão criados dois: um para contoso11.com e outro para fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="37665-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="37665-141">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="37665-141">Step 1</span></span>

<span data-ttu-id="37665-142">Navegue para um gateway de aplicativo existente no portal do Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37665-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="37665-143">Selecione **Pools de back-end** e clique em **Adicionar**</span><span class="sxs-lookup"><span data-stu-id="37665-143">Select **Backend pools** and click **Add**</span></span>

![adicionar pools do back-end][7]

### <a name="step-2"></a><span data-ttu-id="37665-145">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="37665-145">Step 2</span></span>

<span data-ttu-id="37665-146">Preencha as informações para o pool de back-end **pool1**, adicionando os endereços ip ou FQDNs para os servidores back-end e clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="37665-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![configurações do pool de back-end pool1][8]

### <a name="step-3"></a><span data-ttu-id="37665-148">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="37665-148">Step 3</span></span>

<span data-ttu-id="37665-149">Na folha de pools de back-end, clique em **Adicionar** para adicionar um pool de back-end **pool2** extra, adicionando os endereços ip ou FQDNS para os servidores back-end e clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="37665-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![configurações do pool de back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="37665-151">Criar ouvintes para cada back-end</span><span class="sxs-lookup"><span data-stu-id="37665-151">Create listeners for each back-end</span></span>

<span data-ttu-id="37665-152">O Gateway de Aplicativo depende de cabeçalhos de host HTTP 1.1 para hospedar mais de um site na mesma porta e endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="37665-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="37665-153">O ouvinte básico criado no portal não contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="37665-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="37665-154">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="37665-154">Step 1</span></span>

<span data-ttu-id="37665-155">Clique em **Ouvintes** no gateway de aplicativo existente e clique em **Multissite** para adicionar o primeiro ouvinte.</span><span class="sxs-lookup"><span data-stu-id="37665-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![folha de visão geral de ouvintes][1]

### <a name="step-2"></a><span data-ttu-id="37665-157">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="37665-157">Step 2</span></span>

<span data-ttu-id="37665-158">Preencha as informações para o ouvinte.</span><span class="sxs-lookup"><span data-stu-id="37665-158">Fill out the information for the listener.</span></span> <span data-ttu-id="37665-159">Neste exemplo, a terminação SSL está configurada; crie uma nova porta de front-end.</span><span class="sxs-lookup"><span data-stu-id="37665-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="37665-160">Carregue o certificado .pfx a ser usado para a terminação SSL.</span><span class="sxs-lookup"><span data-stu-id="37665-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="37665-161">A única diferença nessa folha em comparação à folha de ouvinte básica padrão é o nome do host.</span><span class="sxs-lookup"><span data-stu-id="37665-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![folha de propriedades do ouvinte][2]

### <a name="step-3"></a><span data-ttu-id="37665-163">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="37665-163">Step 3</span></span>

<span data-ttu-id="37665-164">Clique em **Multissite** e crie outro ouvinte conforme descrito na etapa anterior para o segundo site.</span><span class="sxs-lookup"><span data-stu-id="37665-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="37665-165">Certifique-se de usar um certificado diferente para o segundo ouvinte.</span><span class="sxs-lookup"><span data-stu-id="37665-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="37665-166">A única diferença nessa folha em comparação à folha de ouvinte básica padrão é o nome do host.</span><span class="sxs-lookup"><span data-stu-id="37665-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="37665-167">Preencha as informações para o ouvinte e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="37665-167">Fill out the information for the listener and click **OK**.</span></span>

![folha de propriedades do ouvinte][3]

> [!NOTE]
> <span data-ttu-id="37665-169">A criação de ouvintes no portal do Azure para o gateway de aplicativo é uma tarefa demorada; pode levar algum tempo para criar dois ouvintes nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="37665-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="37665-170">Ao concluir, os ouvintes são mostrados no portal conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="37665-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![visão geral do ouvinte][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="37665-172">Criar regras para mapear ouvintes para pools de back-end</span><span class="sxs-lookup"><span data-stu-id="37665-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="37665-173">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="37665-173">Step 1</span></span>

<span data-ttu-id="37665-174">Navegue para um gateway de aplicativo existente no portal do Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="37665-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="37665-175">Selecione **Regras** e escolha a regra padrão existente **rule1** e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="37665-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="37665-176">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="37665-176">Step 2</span></span>

<span data-ttu-id="37665-177">Preencha a folha de regras conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="37665-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="37665-178">Escolher o primeiro ouvinte e o primeiro pool e clicar em **Salvar** ao concluir.</span><span class="sxs-lookup"><span data-stu-id="37665-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![editar regra existente][6]

### <a name="step-3"></a><span data-ttu-id="37665-180">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="37665-180">Step 3</span></span>

<span data-ttu-id="37665-181">Clique em **Regra básica** para criar a segunda regra.</span><span class="sxs-lookup"><span data-stu-id="37665-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="37665-182">Preencha o formulário com o segundo ouvinte e o segundo pool de back-end e clique em **OK** para salvar.</span><span class="sxs-lookup"><span data-stu-id="37665-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![adicionar folha de regra básica][10]

<span data-ttu-id="37665-184">Esse cenário conclui a configuração de um gateway de aplicativo existente com suporte a multissite por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="37665-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37665-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37665-185">Next steps</span></span>

<span data-ttu-id="37665-186">Saiba como proteger seus sites com o [Gateway de Aplicativo - Firewall de Aplicativo Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="37665-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
