---
title: "Nome do emissor e chave do emissor nos Serviços BizTalk | Microsoft Docs"
description: "Saiba como recuperar o nome do emissor e chave do emissor para barramento de serviço ou controle de acesso (ACS) nos serviços BizTalk. MABS, WABS"
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
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="cdaaf-104">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="cdaaf-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="cdaaf-105">Os Serviços BizTalk do Azure usam o nome e a chave do emissor do Barramento de Serviço e o nome e a chave do emissor do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="cdaaf-106">Especificamente:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-106">Specifically:</span></span>

| <span data-ttu-id="cdaaf-107">Tarefa</span><span class="sxs-lookup"><span data-stu-id="cdaaf-107">Task</span></span> | <span data-ttu-id="cdaaf-108">Qual nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="cdaaf-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="cdaaf-109">Implantando seu aplicativo do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdaaf-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="cdaaf-110">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="cdaaf-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="cdaaf-111">Configurando o Portal dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="cdaaf-112">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="cdaaf-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="cdaaf-113">Criando retransmissões de LOB com os Serviços do Adaptador do BizTalk no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cdaaf-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="cdaaf-114">Nome e chave do emissor do Service Bus</span><span class="sxs-lookup"><span data-stu-id="cdaaf-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="cdaaf-115">Este tópico lista as etapas para recuperar o Nome e a Chave do Emissor.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="cdaaf-116">Nome e chave do emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="cdaaf-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="cdaaf-117">O nome e a chave do emissor do Controle de Acesso são usados pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="cdaaf-118">Seu aplicativo do Serviço do BizTalk do Azure criado no Visual Studio: para implantar seu aplicativo do Serviço do BizTalk no Visual Studio para Azure, você insere o nome e a chave do emissor do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="cdaaf-119">O Portal de Serviços BizTalk do Azure: quando você cria um Serviço BizTalk e abre o Portal de Serviços BizTalk, o Nome de Emissor do Controle de Acesso e a Chave do Emissor são automaticamente registrados para implantações com os mesmos valores de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="cdaaf-120">Obtenha o Nome e a Chave do Emissor do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="cdaaf-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="cdaaf-121">Para usar o ACS para autenticação e obter os valores de Nome do Emissor e Chave do Emissor, as etapas gerais incluem:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="cdaaf-122">Instalar os [cmdlets do Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="cdaaf-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="cdaaf-123">Adicionar sua conta do Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="cdaaf-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="cdaaf-124">Retornar o nome da sua assinatura: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="cdaaf-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="cdaaf-125">Selecionar sua assinatura: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="cdaaf-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="cdaaf-126">Criar um novo namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="cdaaf-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="cdaaf-127">Exemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="cdaaf-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="cdaaf-128">Quando o novo namespace do ACS for criado (o que pode levar vários minutos), os valores de Nome do Emissor e Chave do Emissor serão listados na cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

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

<span data-ttu-id="cdaaf-129">Resumidamente:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-129">To summarize:</span></span>  
<span data-ttu-id="cdaaf-130">Nome do Emissor = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="cdaaf-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="cdaaf-131">Chave do Emissor = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="cdaaf-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="cdaaf-132">Mais no cmdlet [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdaaf-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="cdaaf-133">Nome e chave do emissor do Service Bus</span><span class="sxs-lookup"><span data-stu-id="cdaaf-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="cdaaf-134">O nome e a chave do emissor do Barramento de Serviço são usados pelos Serviços do Adaptador do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="cdaaf-135">Em seu projeto de Serviços BizTalk no Visual Studio, você usa os Serviços do Adaptador BizTalk para se conectar a um sistema de Linha de Negócios (LOB) local.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="cdaaf-136">Para se conectar, você cria a retransmissão de LOB e insere os detalhes do seu sistema de LOB.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="cdaaf-137">Ao fazer isso, você também insere o nome e a chave do emissor do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="cdaaf-138">Para recuperar o nome e a chave do emissor do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="cdaaf-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="cdaaf-139">Entre no [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cdaaf-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cdaaf-140">No painel de navegação esquerdo, selecione **Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="cdaaf-141">Selecione seu namespace.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-141">Select your namespace.</span></span> <span data-ttu-id="cdaaf-142">Na barra de tarefas, selecione **Informações da Conexão**.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="cdaaf-143">Isso exibe o **Emissor Padrão** (Nome do Emissor) e a **Chave Padrão** (Chave do Emissor).</span><span class="sxs-lookup"><span data-stu-id="cdaaf-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="cdaaf-144">Os valores podem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="cdaaf-144">Their values can be copied.</span></span>  

<span data-ttu-id="cdaaf-145">Resumidamente:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-145">To summarize:</span></span>  
<span data-ttu-id="cdaaf-146">Nome do Emissor = Emissor Padrão</span><span class="sxs-lookup"><span data-stu-id="cdaaf-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="cdaaf-147">Chave do Emissor = Chave Padrão</span><span class="sxs-lookup"><span data-stu-id="cdaaf-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="cdaaf-148">Avançar</span><span class="sxs-lookup"><span data-stu-id="cdaaf-148">Next</span></span>
<span data-ttu-id="cdaaf-149">Tópicos adicionais dos Serviços BizTalk do Azure:</span><span class="sxs-lookup"><span data-stu-id="cdaaf-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="cdaaf-150">Instalando o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="cdaaf-151">Tutoriais: Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="cdaaf-152">Como começar a usar o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="cdaaf-153">Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="cdaaf-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cdaaf-154">See Also</span></span>
* [<span data-ttu-id="cdaaf-155">Como usar o Serviço de Gerenciamento do ACS para configurar identidades de serviço</span><span class="sxs-lookup"><span data-stu-id="cdaaf-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="cdaaf-156">Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="cdaaf-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="cdaaf-157">Serviços BizTalk: provisionamento usando o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="cdaaf-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="cdaaf-158">Serviços BizTalk: gráfico do status do provisionamento</span><span class="sxs-lookup"><span data-stu-id="cdaaf-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="cdaaf-159">Serviços BizTalk: guias Painel, Monitor e Escala</span><span class="sxs-lookup"><span data-stu-id="cdaaf-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="cdaaf-160">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="cdaaf-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="cdaaf-161">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="cdaaf-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

