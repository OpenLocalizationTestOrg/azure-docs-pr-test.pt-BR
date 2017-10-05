---
title: Criar uma conta do Lote no portal do Azure | Microsoft Docs
description: Aprenda a criar uma conta do Lote do Azure no portal do Azure para executar cargas de trabalho paralelas em larga escala na nuvem.
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 520d1d42d35b25db1a35d4317e9eb616cf5de565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="e389f-103">Criar uma conta do Lote com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e389f-103">Create a Batch account with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e389f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e389f-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="e389f-105">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="e389f-106">Saiba como criar uma conta do Lote do Azure no [portal do Azure][azure_portal] e escolha as propriedades da conta que se ajustam ao seu cenário de computação.</span><span class="sxs-lookup"><span data-stu-id="e389f-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="e389f-107">Saiba onde encontrar propriedades da conta importantes, como chaves de acesso e URLs de conta.</span><span class="sxs-lookup"><span data-stu-id="e389f-107">Learn where to find important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="e389f-108">Para saber mais sobre contas do Lote e cenários, confira a [visão geral do recurso](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e389f-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="e389f-109">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="e389f-109">Create a Batch account</span></span>

<span data-ttu-id="e389f-110">Use o portal para criar uma conta do Lote em um dos dois *modos de alocação de pool*: o modo do **serviço Lote** ou o mais recente modo de **assinatura do usuário**, que requer mais configuração.</span><span class="sxs-lookup"><span data-stu-id="e389f-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="e389f-111">Para saber mais sobre esses dois modos, confira a [visão geral do recurso](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="e389f-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="e389f-112">Para os recursos do modo de assinatura do usuário, confira também a [postagem do blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="e389f-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="e389f-113">Modo de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-113">Batch service mode</span></span>



1. <span data-ttu-id="e389f-114">Entre no [Portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e389f-114">Sign in to the [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="e389f-115">Clique em **Novo** > **Computação** > **Serviço de Lote**.</span><span class="sxs-lookup"><span data-stu-id="e389f-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote no Marketplace][marketplace_portal]
3. <span data-ttu-id="e389f-117">A folha **Nova Conta do Lote** é exibida.</span><span class="sxs-lookup"><span data-stu-id="e389f-117">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e389f-118">Confira as descrições de cada elemento de folha abaixo.</span><span class="sxs-lookup"><span data-stu-id="e389f-118">See the descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal]

    <span data-ttu-id="e389f-120">a.</span><span class="sxs-lookup"><span data-stu-id="e389f-120">a.</span></span> <span data-ttu-id="e389f-121">**Nome da conta**: o nome da conta do Lote que você escolher deve ser exclusivo dentro da região do Azure onde a conta é criada (confira **Local** abaixo).</span><span class="sxs-lookup"><span data-stu-id="e389f-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="e389f-122">O nome da conta pode conter apenas minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="e389f-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e389f-123">b.</span><span class="sxs-lookup"><span data-stu-id="e389f-123">b.</span></span> <span data-ttu-id="e389f-124">**Assinatura**: a assinatura na qual a conta do Lote será criada.</span><span class="sxs-lookup"><span data-stu-id="e389f-124">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="e389f-125">Se você tiver somente uma assinatura, ela será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="e389f-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="e389f-126">c.</span><span class="sxs-lookup"><span data-stu-id="e389f-126">c.</span></span> <span data-ttu-id="e389f-127">**Modo de alocação de pool**: selecione **Serviço Lote**.</span><span class="sxs-lookup"><span data-stu-id="e389f-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="e389f-128">c.</span><span class="sxs-lookup"><span data-stu-id="e389f-128">c.</span></span> <span data-ttu-id="e389f-129">**Grupo de recursos**: selecione um grupo de recursos para sua nova conta do Lote ou, opcionalmente, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="e389f-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="e389f-130">d.</span><span class="sxs-lookup"><span data-stu-id="e389f-130">d.</span></span> <span data-ttu-id="e389f-131">**Local**: a região do Azure na qual a conta do Lote será criada.</span><span class="sxs-lookup"><span data-stu-id="e389f-131">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="e389f-132">Somente as regiões com suporte da sua assinatura e do seu grupo de recursos são exibidas como opções.</span><span class="sxs-lookup"><span data-stu-id="e389f-132">Only the regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="e389f-133">e.</span><span class="sxs-lookup"><span data-stu-id="e389f-133">e.</span></span> <span data-ttu-id="e389f-134">**Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e389f-135">Isso é recomendado para a maioria das contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e389f-136">Confira [Conta do Armazenamento do Azure vinculada](#linked-azure-storage-account) mais adiante neste artigo para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e389f-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="e389f-137">Clique em **Criar** para criar a conta.</span><span class="sxs-lookup"><span data-stu-id="e389f-137">Click **Create** to create the account.</span></span>

   <span data-ttu-id="e389f-138">O portal indica que a implantação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e389f-138">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="e389f-139">Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="e389f-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="e389f-140">Modo de assinatura do usuário</span><span class="sxs-lookup"><span data-stu-id="e389f-140">User subscription mode</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="e389f-141">Permitir que o Lote do Azure acesse a assinatura (operação única)</span><span class="sxs-lookup"><span data-stu-id="e389f-141">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="e389f-142">Ao criar sua primeira conta do Lote no modo de assinatura do usuário, execute as etapas a seguir para registrar sua assinatura com o Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span></span> <span data-ttu-id="e389f-143">(Se você fez isso anteriormente, pule para a próxima seção.)</span><span class="sxs-lookup"><span data-stu-id="e389f-143">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="e389f-144">Entre no [Portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e389f-144">Sign in to the [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="e389f-145">Clique em **Mais Serviços** > **Assinaturas**e clique na assinatura que você deseja usar para a conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span></span>

3. <span data-ttu-id="e389f-146">Na folha **Assinatura**, clique em **Controle de acesso (IAM)** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e389f-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Controle de acesso de assinatura][subscription_access]

4. <span data-ttu-id="e389f-148">Na folha **Adicionar permissões**, selecione a função **Colaborador**, procure a API do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-148">On the **Add permissions** blade, select the **Contributor** role, search for the Batch API.</span></span> <span data-ttu-id="e389f-149">Procure cada uma dessas cadeias de caracteres até encontrar a API:</span><span class="sxs-lookup"><span data-stu-id="e389f-149">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="e389f-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="e389f-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="e389f-151">**Lote do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="e389f-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="e389f-152">Os locatários mais recentes do Azure AD podem usar esse nome.</span><span class="sxs-lookup"><span data-stu-id="e389f-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="e389f-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** é a ID para a API do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 

5. <span data-ttu-id="e389f-154">Depois de encontrar a API do Lote, selecione-a e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e389f-154">Once you find the Batch API, select it and click **Save**.</span></span>

    ![Adicionar permissões do Lote][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="e389f-156">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="e389f-156">Create a key vault</span></span>
<span data-ttu-id="e389f-157">No modo de assinatura do usuário, é necessário ter um Azure Key Vault que pertença ao mesmo grupo de recursos da conta do Lote a ser criada.</span><span class="sxs-lookup"><span data-stu-id="e389f-157">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="e389f-158">Verifique se o grupo de recursos está em uma região em que o Lote esteja [disponível](https://azure.microsoft.com/regions/services/) e que tenha suporte pela assinatura.</span><span class="sxs-lookup"><span data-stu-id="e389f-158">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="e389f-159">No [portal do Azure][azure_portal], clique em **Novo** > **Segurança + Identidade** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="e389f-159">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="e389f-160">Na folha **Criar Key Vault**, insira um nome para o cofre de chaves e crie um grupo de recursos na região desejada para a conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-160">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="e389f-161">Deixe as configurações restantes com valores padrão e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e389f-161">Leave the remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="e389f-162">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="e389f-162">Create a Batch account</span></span>

1. <span data-ttu-id="e389f-163">No [portal do Azure][azure_portal], clique em **Novo** > **Computação** > **Serviço Lote**.</span><span class="sxs-lookup"><span data-stu-id="e389f-163">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote no Marketplace][marketplace_portal]
3. <span data-ttu-id="e389f-165">A folha **Nova Conta do Lote** é exibida.</span><span class="sxs-lookup"><span data-stu-id="e389f-165">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e389f-166">Confira as descrições de cada elemento de folha abaixo.</span><span class="sxs-lookup"><span data-stu-id="e389f-166">See the descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal_byos]

    <span data-ttu-id="e389f-168">a.</span><span class="sxs-lookup"><span data-stu-id="e389f-168">a.</span></span> <span data-ttu-id="e389f-169">**Nome da conta**: o nome da conta do Lote que você escolher deve ser exclusivo dentro da região do Azure onde a conta é criada (confira **Local** abaixo).</span><span class="sxs-lookup"><span data-stu-id="e389f-169">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="e389f-170">O nome da conta pode conter apenas minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="e389f-170">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e389f-171">b.</span><span class="sxs-lookup"><span data-stu-id="e389f-171">b.</span></span> <span data-ttu-id="e389f-172">**Assinatura**: se você tiver mais de uma assinatura, selecione a que você registrou com o serviço Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-172">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span></span>

    <span data-ttu-id="e389f-173">c.</span><span class="sxs-lookup"><span data-stu-id="e389f-173">c.</span></span> <span data-ttu-id="e389f-174">**Modo de alocação de pool**: selecione **Assinatura de usuário**.</span><span class="sxs-lookup"><span data-stu-id="e389f-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="e389f-175">d.</span><span class="sxs-lookup"><span data-stu-id="e389f-175">d.</span></span> <span data-ttu-id="e389f-176">**Key Vault**: selecione o cofre de chaves que você criou para sua conta do Lote na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="e389f-176">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span></span> <span data-ttu-id="e389f-177">Opcionalmente, crie um novo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e389f-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="e389f-178">Depois de selecionar o cofre, marque a caixa de seleção para conceder ao Lote do Azure acesso ao cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e389f-178">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span></span>

    <span data-ttu-id="e389f-179">c.</span><span class="sxs-lookup"><span data-stu-id="e389f-179">c.</span></span> <span data-ttu-id="e389f-180">**Grupo de recursos**: selecione o grupo de recursos em que você criou o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e389f-180">**Resource group**: Select the resource group in which you  created the key vault.</span></span>

    <span data-ttu-id="e389f-181">d.</span><span class="sxs-lookup"><span data-stu-id="e389f-181">d.</span></span> <span data-ttu-id="e389f-182">**Local**: região do Azure em que você criou o cofre de chaves para a conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-182">**Location**: The Azure region in which you created the key vault for the Batch account.</span></span>

    <span data-ttu-id="e389f-183">e.</span><span class="sxs-lookup"><span data-stu-id="e389f-183">e.</span></span> <span data-ttu-id="e389f-184">**Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e389f-185">Isso é recomendado para a maioria das contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e389f-186">Confira [Conta vinculada do Armazenamento do Azure](#linked-azure-storage-account) abaixo para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e389f-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="e389f-187">Clique em **Criar** para criar a conta.</span><span class="sxs-lookup"><span data-stu-id="e389f-187">Click **Create** to create the account.</span></span>

   <span data-ttu-id="e389f-188">O portal indica que a implantação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e389f-188">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="e389f-189">Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="e389f-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="e389f-190">Exibir propriedades de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-190">View Batch account properties</span></span>
<span data-ttu-id="e389f-191">Após a criação da conta, você poderá abrir a **folha Conta do Lote** para acessar suas propriedades e configurações.</span><span class="sxs-lookup"><span data-stu-id="e389f-191">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span></span> <span data-ttu-id="e389f-192">Você pode acessar todas as propriedades e configurações de conta usando o menu à esquerda da folha Conta de Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-192">You can access all account settings and properties by using the left menu of the Batch account blade.</span></span>

![Folha Conta do Lote no portal do Azure][account_blade]

* <span data-ttu-id="e389f-194">**URL de conta do Lote**: ao desenvolver um aplicativo com as [APIs do Lote](batch-apis-tools.md#azure-accounts-for-batch-development), você precisará de uma URL de conta para acessar os recursos do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-194">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL to access your Batch resources.</span></span> <span data-ttu-id="e389f-195">Uma URL de conta do Lote tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="e389f-195">A Batch account URL has the following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL de conta do Lote no portal][account_url]

* <span data-ttu-id="e389f-197">**Chaves de acesso** (modo de serviço Lote): para autenticar o acesso à conta do Lote do aplicativo, você precisará de uma chave de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="e389f-197">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="e389f-198">(Essa configuração não está disponível no modo de assinatura do usuário, em que você usa a autenticação do Azure Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="e389f-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="e389f-199">Para exibir ou regenerar chaves de acesso da sua conta do Lote, insira `keys` na caixa **Pesquisar** do menu à esquerda na folha Conta do Lote e, em seguida, selecione **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="e389f-199">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span></span>

    ![Chaves de conta do Lote no portal do Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="e389f-201">Conta vinculada do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e389f-201">Linked Azure Storage account</span></span>

<span data-ttu-id="e389f-202">Você pode, opcionalmente, vincular uma conta de Armazenamento do Azure de finalidade geral à sua nova conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-202">You can optionally link a general-purpose Azure Storage account to your Batch account.</span></span> <span data-ttu-id="e389f-203">O recurso de [pacotes de aplicativos](batch-application-packages.md) do Lote usa o armazenamento de Blobs do Azure, como faz a biblioteca [.NET de Convenções de Arquivo do Lote](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="e389f-203">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="e389f-204">Esses recursos opcionais ajudarão você a implantar os aplicativos executados por suas tarefas do Lote, persistindo os dados que eles produzem.</span><span class="sxs-lookup"><span data-stu-id="e389f-204">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="e389f-205">É recomendável que você crie uma nova conta de armazenamento exclusivamente para uso com sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Criando uma conta de armazenamento de uso geral][storage_account]

> [!NOTE]
> <span data-ttu-id="e389f-207">O Lote do Azure atualmente dá suporte apenas ao tipo de conta de Armazenamento de uso geral.</span><span class="sxs-lookup"><span data-stu-id="e389f-207">Azure Batch currently supports only the general-purpose Storage account type.</span></span> <span data-ttu-id="e389f-208">Esse tipo de conta é descrito na etapa 5, [Criar uma conta de armazenamento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), em [Sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e389f-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="e389f-209">Tome cuidado ao regenerar as chaves de acesso de uma conta de Armazenamento vinculada.</span><span class="sxs-lookup"><span data-stu-id="e389f-209">Be careful when regenerating the access keys of a linked Storage account.</span></span> <span data-ttu-id="e389f-210">Regenere somente uma chave de conta do Armazenamento e clique em **Sincronizar Chaves** na folha Conta do Armazenamento vinculada.</span><span class="sxs-lookup"><span data-stu-id="e389f-210">Regenerate only one Storage account key and click **Sync Keys** on the linked Storage account blade.</span></span> <span data-ttu-id="e389f-211">Aguarde cinco minutos para permitir que as chaves sejam propagadas para os nós de computação em seus pools e regenere e sincronize a outra chave, se necessário.</span><span class="sxs-lookup"><span data-stu-id="e389f-211">Wait five minutes to allow the keys to propagate to the compute nodes in your pools, then regenerate and synchronize the other key if necessary.</span></span> <span data-ttu-id="e389f-212">Se você regenerar as chaves ao mesmo tempo, os nós de computação não poderão sincronizar nenhuma delas e, assim, perderão o acesso à conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e389f-212">If you regenerate both keys at the same time, your compute nodes will not be able to synchronize either key, and they will lose access to the Storage account.</span></span>
>
>

<span data-ttu-id="e389f-213">![Regeneração de chaves da conta de armazenamento][4]</span><span class="sxs-lookup"><span data-stu-id="e389f-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="e389f-214">Cotas e limites de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-214">Batch service quotas and limits</span></span>
<span data-ttu-id="e389f-215">Esteja ciente de que como sua assinatura do Azure e outros serviços do Azure, determinados [limites e cotas](batch-quota-limit.md) se aplicam a contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span></span> <span data-ttu-id="e389f-216">As cotas atuais em uma conta do Lote aparecem no portal nas **Propriedades**da conta.</span><span class="sxs-lookup"><span data-stu-id="e389f-216">Current quotas for a Batch account appear in the portal in the account **Properties**.</span></span>

![Cotas de conta do Lote no portal do Azure][quotas]



<span data-ttu-id="e389f-218">Adicionalmente, muitas dessas cotas podem ser aumentadas com uma solicitação de suporte do produto gratuito enviada no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e389f-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span></span> <span data-ttu-id="e389f-219">Confira [Cotas e limites para o serviço do Lote do Azure](batch-quota-limit.md) para obter detalhes sobre a solicitação de aumentos de cota.</span><span class="sxs-lookup"><span data-stu-id="e389f-219">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="e389f-220">Outras opções de gerenciamento de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-220">Other Batch account management options</span></span>
<span data-ttu-id="e389f-221">Além de usar o portal do Azure, você também pode criar e gerenciar contas do Lote com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e389f-221">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span></span>

* [<span data-ttu-id="e389f-222">Cmdlets do PowerShell do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="e389f-223">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e389f-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="e389f-224">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="e389f-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="e389f-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e389f-225">Next steps</span></span>
* <span data-ttu-id="e389f-226">Veja a [visão geral dos recursos do Lote](batch-api-basics.md) para saber mais sobre os conceitos e os recursos do serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="e389f-226">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="e389f-227">O artigo aborda os recursos principais do Lote, como pools, nós de computação, trabalhos e tarefas, e fornece uma visão geral dos recursos do serviço que permitem a execução da carga de trabalho de computação em larga escala.</span><span class="sxs-lookup"><span data-stu-id="e389f-227">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="e389f-228">Obtenha as noções básicas sobre o desenvolvimento de um aplicativo habilitado para o Lote usando a [biblioteca de cliente .NET do Lote](batch-dotnet-get-started.md) ou do [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e389f-228">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="e389f-229">O artigo introdutório orienta você por meio de um aplicativo de trabalho que usa o serviço em Lotes para executar uma carga de trabalho em vários nós de computação e que inclui o uso do Armazenamento do Azure para preparação e recuperação de um arquivo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e389f-229">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regeneração de chaves da conta de armazenamento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
