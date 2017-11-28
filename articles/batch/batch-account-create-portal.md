---
title: "uma conta de lote no portal do Azure de saudação do aaaCreate | Microsoft Docs"
description: "Saiba como conta toocreate um lote do Azure em Olá toorun portal do Azure cargas de trabalho paralelas em grande escala na nuvem Olá"
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
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="be8ee-103">Crie uma conta de lote com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="be8ee-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="be8ee-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="be8ee-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="be8ee-105">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="be8ee-106">Saiba como a conta toocreate um lote do Azure no hello [portal do Azure][azure_portal]e escolha Propriedades de conta de saudação que se adaptam a seu cenário de computação.</span><span class="sxs-lookup"><span data-stu-id="be8ee-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="be8ee-107">Saiba onde toofind propriedades de conta importantes como chaves de acesso e as URLs de conta.</span><span class="sxs-lookup"><span data-stu-id="be8ee-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="be8ee-108">Para obter informações sobre cenários e contas em lotes, consulte Olá [visão geral de recursos](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="be8ee-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="be8ee-109">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="be8ee-109">Create a Batch account</span></span>

<span data-ttu-id="be8ee-110">Use Olá portal toocreate uma conta de lote em uma saudação dois *modos de alocação de pool*: **serviço de lote** modo ou hello mais recente **assinatura de usuário** modo, o que requer mais configuração.</span><span class="sxs-lookup"><span data-stu-id="be8ee-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="be8ee-111">Para obter informações sobre esses dois modos, consulte Olá [visão geral de recursos](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="be8ee-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="be8ee-112">Para os recursos Olá assinatura de modo de usuário, consulte também Olá [postagem de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="be8ee-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="be8ee-113">Modo de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-113">Batch service mode</span></span>



1. <span data-ttu-id="be8ee-114">Entrar toohello [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="be8ee-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="be8ee-115">Clique em **Novo** > **Computação** > **Serviço de Lote**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote em Olá Marketplace][marketplace_portal]
3. <span data-ttu-id="be8ee-117">Olá **nova conta de lote** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="be8ee-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="be8ee-118">Consulte as descrições de saudação abaixo de cada elemento da folha.</span><span class="sxs-lookup"><span data-stu-id="be8ee-118">See hello descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal]

    <span data-ttu-id="be8ee-120">a.</span><span class="sxs-lookup"><span data-stu-id="be8ee-120">a.</span></span> <span data-ttu-id="be8ee-121">**Nome da conta**: nome de conta de lote Olá você escolher deve ser exclusivo dentro Olá região do Azure em que a conta de saudação é criada (consulte **local** abaixo).</span><span class="sxs-lookup"><span data-stu-id="be8ee-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="be8ee-122">nome da conta Olá pode conter apenas caracteres em minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="be8ee-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="be8ee-123">b.</span><span class="sxs-lookup"><span data-stu-id="be8ee-123">b.</span></span> <span data-ttu-id="be8ee-124">**Assinatura**: Olá assinatura no qual Olá toocreate conta do lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="be8ee-125">Se você tiver somente uma assinatura, ela será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="be8ee-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="be8ee-126">c.</span><span class="sxs-lookup"><span data-stu-id="be8ee-126">c.</span></span> <span data-ttu-id="be8ee-127">**Modo de alocação de pool**: selecione **Serviço Lote**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="be8ee-128">c.</span><span class="sxs-lookup"><span data-stu-id="be8ee-128">c.</span></span> <span data-ttu-id="be8ee-129">**Grupo de recursos**: selecione um grupo de recursos para sua nova conta do Lote ou, opcionalmente, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="be8ee-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="be8ee-130">d.</span><span class="sxs-lookup"><span data-stu-id="be8ee-130">d.</span></span> <span data-ttu-id="be8ee-131">**Local**: Olá região do Azure no qual Olá toocreate conta do lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="be8ee-132">Olá regiões de somente tem suportados por sua assinatura e o grupo de recursos são exibidas como opções.</span><span class="sxs-lookup"><span data-stu-id="be8ee-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="be8ee-133">e.</span><span class="sxs-lookup"><span data-stu-id="be8ee-133">e.</span></span> <span data-ttu-id="be8ee-134">**Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="be8ee-135">Isso é recomendado para a maioria das contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="be8ee-136">Confira [Conta do Armazenamento do Azure vinculada](#linked-azure-storage-account) mais adiante neste artigo para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="be8ee-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="be8ee-137">Clique em **criar** toocreate conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="be8ee-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="be8ee-138">portal de saudação indica a implantação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="be8ee-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="be8ee-139">Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="be8ee-140">Modo de assinatura do usuário</span><span class="sxs-lookup"><span data-stu-id="be8ee-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="be8ee-141">Permitir tooaccess de lote do Azure assinatura hello (operação única)</span><span class="sxs-lookup"><span data-stu-id="be8ee-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="be8ee-142">Ao criar sua primeira conta de lote no modo de usuário de assinatura, execute Olá tooregister as etapas a seguir sua assinatura com o lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="be8ee-143">(Se anteriormente você fez isso, ignore toohello próxima seção).</span><span class="sxs-lookup"><span data-stu-id="be8ee-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="be8ee-144">Entrar toohello [portal do Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="be8ee-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="be8ee-145">Clique em **mais serviços** > **assinaturas**e clique em assinatura Olá desejar toouse para Olá conta do lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="be8ee-146">Em Olá **assinatura** folha, clique em **(IAM) do controle de acesso** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Controle de acesso de assinatura][subscription_access]

4. <span data-ttu-id="be8ee-148">Em Olá **adicionar permissões** folha, selecione Olá **Colaborador** função, procure Olá API de lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="be8ee-149">Pesquisar para cada uma dessas cadeias de caracteres até encontrar hello API:</span><span class="sxs-lookup"><span data-stu-id="be8ee-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="be8ee-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="be8ee-151">**Lote do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="be8ee-152">Os locatários mais recentes do Azure AD podem usar esse nome.</span><span class="sxs-lookup"><span data-stu-id="be8ee-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="be8ee-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** é identificação Olá Olá API de lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="be8ee-154">Depois de encontrar hello API de lote, selecione-o e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Adicionar permissões do Lote][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="be8ee-156">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="be8ee-156">Create a key vault</span></span>
<span data-ttu-id="be8ee-157">No modo de usuário de assinatura, um cofre de chaves do Azure é necessário que pertence a toothe mesmo grupo de recursos Olá toobe de conta de lote criado.</span><span class="sxs-lookup"><span data-stu-id="be8ee-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="be8ee-158">Verifique se o grupo de recursos de saudação está em uma região em que o lote é [disponível](https://azure.microsoft.com/regions/services/) e que oferece suporte à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="be8ee-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="be8ee-159">Em Olá [portal do Azure][azure_portal], clique em **novo** > **segurança + identidade** > **Cofre de chaves** .</span><span class="sxs-lookup"><span data-stu-id="be8ee-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="be8ee-160">Em Olá **criar Cofre de chaves** folha, insira um nome para o Cofre de chaves hello e criar um grupo de recursos na região Olá você deseja para sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="be8ee-161">Deixe Olá restantes valores padrão das configurações, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="be8ee-162">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="be8ee-162">Create a Batch account</span></span>

1. <span data-ttu-id="be8ee-163">Em Olá [portal do Azure][azure_portal], clique em **novo** > **de computação** > **doserviçodelote**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Lote em Olá Marketplace][marketplace_portal]
3. <span data-ttu-id="be8ee-165">Olá **nova conta de lote** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="be8ee-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="be8ee-166">Consulte as descrições de saudação abaixo de cada elemento da folha.</span><span class="sxs-lookup"><span data-stu-id="be8ee-166">See hello descriptions below of each blade element.</span></span>

    ![Criar uma conta do Batch][account_portal_byos]

    <span data-ttu-id="be8ee-168">a.</span><span class="sxs-lookup"><span data-stu-id="be8ee-168">a.</span></span> <span data-ttu-id="be8ee-169">**Nome da conta**: nome de conta de lote Olá você escolher deve ser exclusivo dentro Olá região do Azure em que a conta de saudação é criada (consulte **local** abaixo).</span><span class="sxs-lookup"><span data-stu-id="be8ee-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="be8ee-170">nome da conta Olá pode conter apenas caracteres em minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="be8ee-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="be8ee-171">b.</span><span class="sxs-lookup"><span data-stu-id="be8ee-171">b.</span></span> <span data-ttu-id="be8ee-172">**Assinatura**: se você tiver mais de uma assinatura, selecione a assinatura de saudação que você registrou com o serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="be8ee-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="be8ee-173">c.</span><span class="sxs-lookup"><span data-stu-id="be8ee-173">c.</span></span> <span data-ttu-id="be8ee-174">**Modo de alocação de pool**: selecione **Assinatura de usuário**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="be8ee-175">d.</span><span class="sxs-lookup"><span data-stu-id="be8ee-175">d.</span></span> <span data-ttu-id="be8ee-176">**Cofre de chaves**: Cofre de chaves Olá selecione criado para sua conta do lote na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="be8ee-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="be8ee-177">Opcionalmente, crie um novo cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="be8ee-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="be8ee-178">Depois de selecionar um cofre hello, selecione caixa de seleção Olá toohello toogrant do Azure Batch acesso chave cofre.</span><span class="sxs-lookup"><span data-stu-id="be8ee-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="be8ee-179">c.</span><span class="sxs-lookup"><span data-stu-id="be8ee-179">c.</span></span> <span data-ttu-id="be8ee-180">**Grupo de recursos**: grupo de recursos de saudação Select em que você criou o Cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="be8ee-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="be8ee-181">d.</span><span class="sxs-lookup"><span data-stu-id="be8ee-181">d.</span></span> <span data-ttu-id="be8ee-182">**Local**: Olá região do Azure em que você criou o Cofre de chaves Olá para conta do lote hello.</span><span class="sxs-lookup"><span data-stu-id="be8ee-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="be8ee-183">e.</span><span class="sxs-lookup"><span data-stu-id="be8ee-183">e.</span></span> <span data-ttu-id="be8ee-184">**Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="be8ee-185">Isso é recomendado para a maioria das contas do Lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="be8ee-186">Confira [Conta vinculada do Armazenamento do Azure](#linked-azure-storage-account) abaixo para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="be8ee-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="be8ee-187">Clique em **criar** toocreate conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="be8ee-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="be8ee-188">portal de saudação indica a implantação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="be8ee-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="be8ee-189">Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="be8ee-190">Exibir propriedades de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-190">View Batch account properties</span></span>
<span data-ttu-id="be8ee-191">Olá conta foi criada, é possível abrir Olá **folha de conta de lote** tooaccess suas propriedades e configurações.</span><span class="sxs-lookup"><span data-stu-id="be8ee-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="be8ee-192">Você pode acessar todas as configurações de conta e propriedades usando menus de saudação à esquerda da folha de conta de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="be8ee-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Folha Conta do Lote no portal do Azure][account_blade]

* <span data-ttu-id="be8ee-194">**A URL da conta do lote**: ao desenvolver um aplicativo com hello [lote APIs](batch-apis-tools.md#azure-accounts-for-batch-development), você precisará uma tooaccess de URL de conta de seus recursos de lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="be8ee-195">Uma URL de conta de lote tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="be8ee-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL de conta do Lote no portal][account_url]

* <span data-ttu-id="be8ee-197">**Chaves de acesso** (modo de serviço de lote): tooauthenticate acesso tooyour conta em lotes do seu aplicativo, você precisará de uma chave de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="be8ee-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="be8ee-198">(Essa configuração não está disponível no modo de assinatura do usuário, em que você usa a autenticação do Azure Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="be8ee-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="be8ee-199">tooview ou regenerar chaves de acesso da conta em lotes, digite `keys` no menu esquerdo Olá **pesquisa** caixa na folha de conta de lote hello, em seguida, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Chaves de conta do Lote no portal do Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="be8ee-201">Conta vinculada do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="be8ee-201">Linked Azure Storage account</span></span>

<span data-ttu-id="be8ee-202">Opcionalmente, você pode vincular um tooyour de conta de armazenamento do Azure para fins gerais conta do lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="be8ee-203">Olá [pacotes de aplicativos](batch-application-packages.md) recurso de lote usa o armazenamento de BLOBs do Azure, como o hello [.NET de convenções de arquivo em lotes](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="be8ee-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="be8ee-204">Esses recursos opcionais ajudá-lo Implantando aplicativos Olá que executam as tarefas de lote e manter dados Olá geram.</span><span class="sxs-lookup"><span data-stu-id="be8ee-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="be8ee-205">É recomendável que você crie uma nova conta de armazenamento exclusivamente para uso com sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Criando uma conta de armazenamento de uso geral][storage_account]

> [!NOTE]
> <span data-ttu-id="be8ee-207">Lote do Azure atualmente suporta apenas Olá para fins gerais armazenamento tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="be8ee-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="be8ee-208">Esse tipo de conta é descrito na etapa 5, [Criar uma conta de armazenamento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), em [Sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="be8ee-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="be8ee-209">Tenha cuidado ao regenerar as chaves de acesso de saudação de uma conta de armazenamento vinculada.</span><span class="sxs-lookup"><span data-stu-id="be8ee-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="be8ee-210">Gerar apenas uma chave de conta de armazenamento e clique em **sincronizar as chaves** em Olá vinculado folha da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be8ee-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="be8ee-211">Aguarde cinco minutos tooallow Olá chaves toopropagate toohello nós de computação em seus pools, em seguida, regenerar e sincronizar Olá outra chave, se necessário.</span><span class="sxs-lookup"><span data-stu-id="be8ee-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="be8ee-212">Se você regenerar as chaves no hello mesmo tempo, seus nós de computação não será capaz de toosynchronize qualquer chave e ele perderá a conta de armazenamento toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="be8ee-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="be8ee-213">![Regeneração de chaves da conta de armazenamento][4]</span><span class="sxs-lookup"><span data-stu-id="be8ee-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="be8ee-214">Cotas e limites de serviço do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-214">Batch service quotas and limits</span></span>
<span data-ttu-id="be8ee-215">Esteja ciente de que como com sua assinatura do Azure e outros Azure serviços, determinados [cotas e limites](batch-quota-limit.md) aplicar tooBatch contas.</span><span class="sxs-lookup"><span data-stu-id="be8ee-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="be8ee-216">Cotas atuais para uma conta de lote aparecerá no portal de saudação na conta Olá **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="be8ee-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Cotas de conta do Lote no portal do Azure][quotas]



<span data-ttu-id="be8ee-218">Além disso, muitas dessas cotas podem ser aumentadas simplesmente com uma solicitação de suporte de produto livre enviada no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="be8ee-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="be8ee-219">Consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre como solicitar o aumento de cota.</span><span class="sxs-lookup"><span data-stu-id="be8ee-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="be8ee-220">Outras opções de gerenciamento de conta do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-220">Other Batch account management options</span></span>
<span data-ttu-id="be8ee-221">Além disso, toousing Olá portal do Azure, você também pode criar e gerenciar contas de lote com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="be8ee-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="be8ee-222">Cmdlets do PowerShell do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="be8ee-223">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="be8ee-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="be8ee-224">.NET de Gerenciamento do Lote</span><span class="sxs-lookup"><span data-stu-id="be8ee-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="be8ee-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be8ee-225">Next steps</span></span>
* <span data-ttu-id="be8ee-226">Consulte Olá [visão geral do recurso de lote](batch-api-basics.md) toolearn mais sobre recursos e conceitos do serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="be8ee-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="be8ee-227">Olá artigo aborda os principais recursos de lote hello, como pools, nós de computação, trabalhos e tarefas e fornece uma visão geral da saudação recursos do serviço que permitem a execução da carga de trabalho de computação em larga escala.</span><span class="sxs-lookup"><span data-stu-id="be8ee-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="be8ee-228">Conheça os fundamentos de saudação do desenvolvimento de um aplicativo habilitado para lote usando Olá [biblioteca cliente .NET do lote](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="be8ee-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="be8ee-229">Esses artigos introdutórios guiá-lo por meio de um aplicativo de trabalho que usa tooexecute de serviço de lote Olá uma carga de trabalho em vários nós de computação e inclui o uso de armazenamento do Azure para recuperação e preparação de arquivo de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="be8ee-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

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
