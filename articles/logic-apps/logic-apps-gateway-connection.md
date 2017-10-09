---
title: "aaaAccess fontes de dados no local para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Configurar o gateway de dados local Olá para que possa acessar fontes de dados em instalações de aplicativos lógicos"
keywords: "acessar dados, local, transferência de dados, criptografia, fontes de dados"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="cc147-104">Acessar fontes de dados em instalações de aplicativos lógicos com o gateway de dados local Olá</span><span class="sxs-lookup"><span data-stu-id="cc147-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="cc147-105">tooaccess fontes de dados no local de seus aplicativos lógicos, configure um gateway de dados local que podem usar aplicativos lógicos com conectores com suporte.</span><span class="sxs-lookup"><span data-stu-id="cc147-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="cc147-106">gateway de saudação atua como uma ponte que fornece transferência de dados rápida e criptografia entre fontes de dados no local e seus aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="cc147-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="cc147-107">gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc147-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="cc147-108">Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc147-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="cc147-109">Saiba mais sobre [como funciona o gateway de dados Olá](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cc147-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="cc147-110">gateway Olá dá suporte a fontes de dados de toothese de conexões no local:</span><span class="sxs-lookup"><span data-stu-id="cc147-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="cc147-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="cc147-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="cc147-112">DB2</span><span class="sxs-lookup"><span data-stu-id="cc147-112">DB2</span></span>  
*   <span data-ttu-id="cc147-113">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="cc147-113">File System</span></span>
*   <span data-ttu-id="cc147-114">Informix</span><span class="sxs-lookup"><span data-stu-id="cc147-114">Informix</span></span>
*   <span data-ttu-id="cc147-115">MQ</span><span class="sxs-lookup"><span data-stu-id="cc147-115">MQ</span></span>
*   <span data-ttu-id="cc147-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="cc147-116">MySQL</span></span>
*   <span data-ttu-id="cc147-117">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="cc147-117">Oracle Database</span></span>
*   <span data-ttu-id="cc147-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cc147-118">PostgreSQL</span></span>
*   <span data-ttu-id="cc147-119">Servidor de aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="cc147-119">SAP Application Server</span></span> 
*   <span data-ttu-id="cc147-120">Servidor de mensagens SAP</span><span class="sxs-lookup"><span data-stu-id="cc147-120">SAP Message Server</span></span>
*   <span data-ttu-id="cc147-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc147-121">SharePoint</span></span>
*   <span data-ttu-id="cc147-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cc147-122">SQL Server</span></span>
*   <span data-ttu-id="cc147-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="cc147-123">Teradata</span></span>

<span data-ttu-id="cc147-124">Estas etapas mostram como tooset backup Olá local toowork de gateway de dados com seus aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="cc147-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="cc147-125">Para obter mais informações sobre os conectores com suporte, consulte [Conectores para Aplicativo Lógico do Azure](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="cc147-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="cc147-126">Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="cc147-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="cc147-127">Gateway de dados local do Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="cc147-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="cc147-128">Gateway de dados local do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="cc147-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="cc147-129">Gateway de dados local do Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="cc147-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="cc147-130">Gateway de dados local do Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="cc147-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="cc147-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="cc147-131">Requirements</span></span>

* <span data-ttu-id="cc147-132">É necessário já ter [instalado o gateway de dados Olá em um computador local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cc147-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="cc147-133">Quando você entrar no toohello portal do Azure, você tem toouse Olá mesmo trabalho ou escola conta que foi usada muito[instalar o gateway de dados local Olá](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="cc147-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="cc147-134">Sua conta também deve ter uma assinatura do Azure toouse quando você cria um recurso de gateway no hello portal do Azure para sua instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="cc147-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="cc147-135">Sua instalação do gateway não pode já ter sido reivindicada por um recurso de gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="cc147-136">Você pode associar o recurso gateway instalação tooonly um gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="cc147-137">Declaração acontece quando você criar recursos de gateway Olá para que a instalação de saudação não está disponível para outros recursos.</span><span class="sxs-lookup"><span data-stu-id="cc147-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="cc147-138">Configurar a conexão de gateway de dados Olá</span><span class="sxs-lookup"><span data-stu-id="cc147-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="cc147-139">1. Saudação de instalar o gateway de dados local</span><span class="sxs-lookup"><span data-stu-id="cc147-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="cc147-140">Se você ainda não fez isso, siga Olá [gateway de dados local do etapas tooinstall Olá](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cc147-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="cc147-141">Antes de continuar com hello outras etapas, certifique-se de que você instalou o gateway de dados de saudação em um computador local.</span><span class="sxs-lookup"><span data-stu-id="cc147-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="cc147-142">2. Criar um recurso do Azure para o gateway de dados local Olá</span><span class="sxs-lookup"><span data-stu-id="cc147-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="cc147-143">Depois de instalar o gateway de saudação em um computador local, você deve criar o gateway de dados como um recurso no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="cc147-144">Essa etapa também associa o recurso de gateway à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="cc147-145">Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="cc147-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="cc147-146">Certifique-se de toouse Olá mesmo trabalho do Azure ou o endereço de email escolar usado tooinstall gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc147-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="cc147-147">No menu à esquerda do hello no Azure, escolha **novo** > **integração corporativa** > **gateway de dados no local** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="cc147-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Localize “Gateway de dados local”](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="cc147-149">Em Olá **criar gateway de conexão** folha, fornecer esses detalhes toocreate seu recurso de gateway de dados:</span><span class="sxs-lookup"><span data-stu-id="cc147-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="cc147-150">**Nome**: insira um nome para o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="cc147-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="cc147-151">**Assinatura**: selecione Olá tooassociate de assinatura do Azure com o recurso de gateway.</span><span class="sxs-lookup"><span data-stu-id="cc147-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="cc147-152">Essa assinatura deve ser Olá a mesma assinatura que seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="cc147-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="cc147-153">assinatura do saudação padrão baseia-se em Olá conta do Azure que você usou toosign no.</span><span class="sxs-lookup"><span data-stu-id="cc147-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="cc147-154">**Grupo de recursos**: crie um grupo de recursos ou selecione um grupo de recursos existente para implantar seu recurso de gateway.</span><span class="sxs-lookup"><span data-stu-id="cc147-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="cc147-155">Grupos de recursos ajudam a gerenciar os ativos do Azure relacionados como uma coleção.</span><span class="sxs-lookup"><span data-stu-id="cc147-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="cc147-156">**Local**: Azure restringe esse local toohello mesma região que foi selecionado para o serviço de nuvem do gateway Olá durante [instalação do gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cc147-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="cc147-157">Verifique se o local de recursos de gateway Olá corresponde local do serviço de nuvem de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc147-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="cc147-158">Caso contrário, a instalação do gateway pode não aparecer na lista de gateways de saudação instalada para você tooselect na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="cc147-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="cc147-159">Você pode usar diferentes regiões para o recurso de gateway e para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="cc147-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="cc147-160">**Nome da instalação**: se a instalação do gateway não estiver selecionada, selecione gateway Olá instalada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cc147-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="cc147-161">tooadd Olá gateway recurso tooyour do painel do Azure, escolha **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="cc147-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="cc147-162">Quando terminar, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc147-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="cc147-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cc147-163">For example:</span></span>

    ![Forneça detalhes toocreate seu gateway de dados local](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="cc147-165">toofind ou exibição, o gateway de dados a qualquer momento do hello Azure esquerdo menu principal, vá muito **mais serviços** > **integração corporativa** > **dados locais Gateways**.</span><span class="sxs-lookup"><span data-stu-id="cc147-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Vá muito "Mais serviços", "Enterprise integração", "Gateways de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="cc147-167">3. Conecte-se o gateway de dados lógica aplicativo toohello local</span><span class="sxs-lookup"><span data-stu-id="cc147-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="cc147-168">Agora que você criou o recurso de gateway de dados e sua assinatura do Azure associado ao recurso, crie uma conexão entre o gateway de dados de aplicativo e hello lógica.</span><span class="sxs-lookup"><span data-stu-id="cc147-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="cc147-169">Seu local de conexão do gateway deve existir no hello mesma região que seu aplicativo lógico, mas você pode usar um gateway de dados que existe em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="cc147-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="cc147-170">No hello portal do Azure, crie ou abra o aplicativo lógica no Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc147-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="cc147-171">Adicione um conector que dê suporte a conexões locais, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cc147-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="cc147-172">Ordem de saudação mostrado, selecione **conectar por meio do gateway de dados local**, forneça um nome de conexão exclusivo Olá informações necessárias e selecione Olá recurso de gateway de dados que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="cc147-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="cc147-173">Quando terminar, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc147-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="cc147-174">Um nome de conexão exclusivo ajuda a identificar facilmente essa conexão mais tarde, especialmente quando você cria várias conexões.</span><span class="sxs-lookup"><span data-stu-id="cc147-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="cc147-175">Se aplicável, também incluem qualificado Olá para seu nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="cc147-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Criar a conexão entre o aplicativo lógico e o gateway de dados](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="cc147-177">Parabéns, sua conexão de gateway agora está pronto para toouse de aplicativo sua lógica.</span><span class="sxs-lookup"><span data-stu-id="cc147-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="cc147-178">Editar as configurações da conexão do gateway</span><span class="sxs-lookup"><span data-stu-id="cc147-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="cc147-179">Depois de criar uma conexão de gateway para seu aplicativo lógico, talvez você queira toolater configurações de saudação de atualização para essa conexão específica.</span><span class="sxs-lookup"><span data-stu-id="cc147-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="cc147-180">conexão de gateway de saudação toofind:</span><span class="sxs-lookup"><span data-stu-id="cc147-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="cc147-181">Na folha de aplicativo de lógica de hello, em **ferramentas de desenvolvimento**, selecione **API conexões**.</span><span class="sxs-lookup"><span data-stu-id="cc147-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="cc147-182">Olá **API conexões** painel mostra todas as conexões de API associadas ao seu aplicativo lógica, incluindo as conexões de gateway.</span><span class="sxs-lookup"><span data-stu-id="cc147-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Vá tooyour lógica app, selecione "Conexões de API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="cc147-184">Ou, no hello Azure esquerdo menu principal, vá muito **mais serviços** > **Web e serviços móveis** > **API conexões** para todas as conexões de API incluindo conexões de gateway, que estão associados com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="cc147-185">Ou, em hello Azure esquerdo menu principal, vá muito**todos os recursos** para todas as conexões de API, incluindo conexões de gateway, que estão associados a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc147-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="cc147-186">Selecione a conexão de gateway Olá que você deseja tooview ou editar e escolha **conexão Editar API**.</span><span class="sxs-lookup"><span data-stu-id="cc147-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="cc147-187">Se as atualizações não têm efeito, tente [interromper e reiniciar o serviço do Windows hello gateway](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="cc147-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="cc147-188">Mudar ou excluir o recurso de gateway de dados local</span><span class="sxs-lookup"><span data-stu-id="cc147-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="cc147-189">toocreate um recurso de gateway diferente, associar seu gateway um recurso diferente ou remova o recurso de gateway de saudação, você poderá excluir o recurso de gateway de saudação sem afetar a instalação do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="cc147-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="cc147-190">Menu Olá principal do Azure à esquerda, vá muito**todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="cc147-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="cc147-191">Localize e selecione seu recurso de gateway de dados.</span><span class="sxs-lookup"><span data-stu-id="cc147-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="cc147-192">Escolha **Gateway de dados no local**e na barra de ferramentas de recurso hello, escolha **excluir**.</span><span class="sxs-lookup"><span data-stu-id="cc147-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="cc147-193">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="cc147-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="cc147-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc147-194">Next steps</span></span>

* [<span data-ttu-id="cc147-195">Proteja seus aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="cc147-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="cc147-196">Exemplos comuns e cenários de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="cc147-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
