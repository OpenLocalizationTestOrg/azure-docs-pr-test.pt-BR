---
title: "aaaIssuer nome e chave do emissor nos Serviços BizTalk | Microsoft Docs"
description: "Saiba como o nome do emissor tooretrieve e chave do emissor de barramento de serviço ou controle de acesso (ACS) nos Serviços BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="ca4d6-104">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="ca4d6-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="ca4d6-105">Serviços BizTalk do Azure usa Olá nome do emissor de barramento de serviço e chave do emissor, Olá nome do emissor de controle de acesso e chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="ca4d6-106">Especificamente:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-106">Specifically:</span></span>

| <span data-ttu-id="ca4d6-107">Tarefa</span><span class="sxs-lookup"><span data-stu-id="ca4d6-107">Task</span></span> | <span data-ttu-id="ca4d6-108">Qual nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="ca4d6-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="ca4d6-109">Implantando seu aplicativo do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca4d6-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="ca4d6-110">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="ca4d6-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="ca4d6-111">Configurando Olá Portal de Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="ca4d6-112">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="ca4d6-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="ca4d6-113">Criar retransmissões de LOB com hello serviços de adaptador do BizTalk no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca4d6-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="ca4d6-114">Nome e chave do emissor do Service Bus</span><span class="sxs-lookup"><span data-stu-id="ca4d6-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="ca4d6-115">Este tópico lista Olá etapas tooretrieve Olá nome do emissor e chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="ca4d6-116">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="ca4d6-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="ca4d6-117">Olá, nome do emissor de controle de acesso e a chave do emissor são usados pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="ca4d6-118">Seu aplicativo de serviço BizTalk do Azure criado no Visual Studio: toosuccessfully implantar seu aplicativo do BizTalk Service no Visual Studio tooAzure, digite hello nome do emissor de controle de acesso e a chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="ca4d6-119">Olá Portal de Serviços BizTalk do Azure: quando você cria um BizTalk Service e abre Olá Portal de serviços do BizTalk, o nome do emissor de controle de acesso e a chave do emissor são registradas automaticamente para implantações com hello os mesmos valores de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="ca4d6-120">Obter Olá nome do emissor de controle de acesso e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="ca4d6-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="ca4d6-121">ACS toouse para autenticação e get hello valores do nome do emissor e chave do emissor, hello etapas gerais incluem:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="ca4d6-122">Instalar Olá [cmdlets do Powershell do Azure](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="ca4d6-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="ca4d6-123">Adicionar sua conta do Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="ca4d6-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="ca4d6-124">Retornar o nome da sua assinatura: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="ca4d6-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="ca4d6-125">Selecionar sua assinatura: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="ca4d6-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="ca4d6-126">Criar um novo namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="ca4d6-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="ca4d6-127">Exemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="ca4d6-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="ca4d6-128">Quando Olá novo namespace do ACS é criado (o que pode levar vários minutos), os valores de nome do emissor e chave do emissor Olá são listados na cadeia de caracteres de conexão de saudação:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="ca4d6-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-129">toosummarize:</span></span>  
<span data-ttu-id="ca4d6-130">Nome do Emissor = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="ca4d6-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="ca4d6-131">Chave do Emissor = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="ca4d6-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="ca4d6-132">Mais informações sobre Olá [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="ca4d6-133">Nome e chave do emissor do Service Bus</span><span class="sxs-lookup"><span data-stu-id="ca4d6-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="ca4d6-134">O nome e a chave do emissor do Barramento de Serviço são usados pelos Serviços do Adaptador do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="ca4d6-135">No seu projeto de Serviços BizTalk no Visual Studio, você usar o sistema de linha de negócios (LOB) do hello serviços de adaptador do BizTalk tooconnect tooan local.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="ca4d6-136">tooconnect, criar hello retransmissão LOB e insira os detalhes do sistema LOB.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="ca4d6-137">Ao fazer isso, você também inserir hello nome do emissor de barramento de serviço e a chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="ca4d6-138">Olá tooretrieve nome do emissor de barramento de serviço e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="ca4d6-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="ca4d6-139">Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="ca4d6-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="ca4d6-140">No painel de navegação esquerdo hello, selecione **barramento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="ca4d6-141">Selecione seu namespace.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-141">Select your namespace.</span></span> <span data-ttu-id="ca4d6-142">Na barra de tarefas hello, selecione **informações de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="ca4d6-143">Isso exibe o saudação **emissor padrão** (nome do emissor) e **chave padrão** (chave de emissor).</span><span class="sxs-lookup"><span data-stu-id="ca4d6-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="ca4d6-144">Os valores podem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="ca4d6-144">Their values can be copied.</span></span>  

<span data-ttu-id="ca4d6-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-145">toosummarize:</span></span>  
<span data-ttu-id="ca4d6-146">Nome do Emissor = Emissor Padrão</span><span class="sxs-lookup"><span data-stu-id="ca4d6-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="ca4d6-147">Chave do Emissor = Chave Padrão</span><span class="sxs-lookup"><span data-stu-id="ca4d6-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="ca4d6-148">Avançar</span><span class="sxs-lookup"><span data-stu-id="ca4d6-148">Next</span></span>
<span data-ttu-id="ca4d6-149">Tópicos adicionais dos Serviços BizTalk do Azure:</span><span class="sxs-lookup"><span data-stu-id="ca4d6-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="ca4d6-150">Instalando Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="ca4d6-151">Tutoriais: Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="ca4d6-152">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="ca4d6-153">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="ca4d6-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ca4d6-154">See Also</span></span>
* [<span data-ttu-id="ca4d6-155">Como: usar serviço de gerenciamento de ACS tooConfigure identidades de serviço</span><span class="sxs-lookup"><span data-stu-id="ca4d6-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="ca4d6-156">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="ca4d6-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="ca4d6-157">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ca4d6-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="ca4d6-158">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="ca4d6-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="ca4d6-159">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="ca4d6-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="ca4d6-160">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="ca4d6-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="ca4d6-161">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="ca4d6-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

