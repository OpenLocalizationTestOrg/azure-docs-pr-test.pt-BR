---
title: aaaGet iniciado com o PowerShell para o lote do Azure | Microsoft Docs
description: "Uma breve introdução toohello cmdlets do PowerShell do Azure você pode usar recursos de lote toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="d6f00-103">Gerenciar recursos do Lote com cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6f00-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="d6f00-104">Com hello cmdlets do PowerShell do lote do Azure, você pode executar e script muitas Olá mesmas tarefas que você realizar com hello APIs de lote, Olá portal do Azure e hello Azure Interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="d6f00-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="d6f00-105">Isso é cmdlets de toohello uma rápida introdução, você pode usar toomanage as contas de lote e trabalhar com os recursos de lote como pools, trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="d6f00-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="d6f00-106">Para obter uma lista completa de cmdlets de lote e sintaxe do cmdlet detalhadas, consulte Olá [referência de cmdlet do Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="d6f00-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="d6f00-107">Este artigo baseia-se nos cmdlets do Azure PowerShell versão 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="d6f00-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="d6f00-108">Recomendamos que você atualize o PowerShell do Azure com frequência tootake vantagem do serviço de atualizações e aprimoramentos.</span><span class="sxs-lookup"><span data-stu-id="d6f00-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6f00-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6f00-109">Prerequisites</span></span>
<span data-ttu-id="d6f00-110">Execute Olá após operações toouse Azure PowerShell toomanage seus recursos de lote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="d6f00-111">Instalar e configurar o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="d6f00-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="d6f00-112">Executar Olá **AzureRmAccount Login** cmdlet tooconnect tooyour assinatura (Olá ship do lote do Azure cmdlets no módulo do Azure Resource Manager Olá):</span><span class="sxs-lookup"><span data-stu-id="d6f00-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="d6f00-113">**Registrar com o namespace do provedor de lote Olá**.</span><span class="sxs-lookup"><span data-stu-id="d6f00-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="d6f00-114">Esta operação só precisa toobe executada **uma vez por assinatura**.</span><span class="sxs-lookup"><span data-stu-id="d6f00-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="d6f00-115">Gerenciar contas e chaves do Batch</span><span class="sxs-lookup"><span data-stu-id="d6f00-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="d6f00-116">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="d6f00-116">Create a Batch account</span></span>
<span data-ttu-id="d6f00-117">**New-AzureRmBatchAccount** cria uma conta do Lote em um grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="d6f00-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="d6f00-118">Se você ainda não tiver um grupo de recursos, crie um executando Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d6f00-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="d6f00-119">Especifique um hello Azure regiões no hello **local** parâmetro, como "Central US".</span><span class="sxs-lookup"><span data-stu-id="d6f00-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="d6f00-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d6f00-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="d6f00-121">Em seguida, crie uma conta de lote no grupo de recursos hello, especificando um nome de conta de saudação em <*account_name*> e o local de saudação e o nome do seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d6f00-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="d6f00-122">Criar conta do lote Olá pode levar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d6f00-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="d6f00-123">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d6f00-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="d6f00-124">conta do lote Olá nome deve ser exclusivo toohello região do Azure para o grupo de recursos de saudação conter entre 3 e 24 caracteres e usar somente letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="d6f00-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="d6f00-125">Obter chaves de acesso da conta</span><span class="sxs-lookup"><span data-stu-id="d6f00-125">Get account access keys</span></span>
<span data-ttu-id="d6f00-126">**Get-AzureRmBatchAccountKeys** mostra Olá chaves de acesso associadas a uma conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6f00-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="d6f00-127">Por exemplo, execute Olá tooget Olá primários e secundários as chaves da conta Olá criado a seguir.</span><span class="sxs-lookup"><span data-stu-id="d6f00-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="d6f00-128">Gerar uma nova chave de acesso</span><span class="sxs-lookup"><span data-stu-id="d6f00-128">Generate a new access key</span></span>
<span data-ttu-id="d6f00-129">**New-AzureRmBatchAccountKey** gera uma nova chave de conta primária ou secundária para uma conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6f00-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="d6f00-130">Por exemplo, toogenerate uma nova chave primária para sua conta em lotes, digite:</span><span class="sxs-lookup"><span data-stu-id="d6f00-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="d6f00-131">toogenerate uma nova chave secundária, especifique "Secundário" para Olá **KeyType** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d6f00-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="d6f00-132">Você tem chaves de primárias e secundárias Olá tooregenerate separadamente.</span><span class="sxs-lookup"><span data-stu-id="d6f00-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="d6f00-133">Excluir uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="d6f00-133">Delete a Batch account</span></span>
<span data-ttu-id="d6f00-134">**Remove-AzureRmBatchAccount** exclui uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="d6f00-135">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d6f00-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="d6f00-136">Quando solicitado, confirme que você deseja tooremove Olá conta.</span><span class="sxs-lookup"><span data-stu-id="d6f00-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="d6f00-137">Remoção de conta pode levar algum tempo toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d6f00-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="d6f00-138">Criar um objeto BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="d6f00-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="d6f00-139">usando tooauthenticate Olá cmdlets do PowerShell de lote quando você cria e gerenciar pools de lote, trabalhos, tarefas, e outros recursos, primeiro crie um toostore de objeto BatchAccountContext seu nome de conta e chaves:</span><span class="sxs-lookup"><span data-stu-id="d6f00-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="d6f00-140">Você passa o objeto de BatchAccountContext Olá em cmdlets que use Olá **BatchContext** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d6f00-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="d6f00-141">Por padrão, a chave primária da conta Olá é usado para autenticação, mas você pode selecionar toouse chave Olá alterando seu objeto de BatchAccountContext **KeyInUse** propriedade: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="d6f00-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="d6f00-142">Criar e modificar recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="d6f00-142">Create and modify Batch resources</span></span>
<span data-ttu-id="d6f00-143">Como usar os cmdlets **New-AzureBatchPool**, **New-AzureBatchJob**, e **AzureBatchTask novo** toocreate recursos em uma conta de lote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="d6f00-144">Há correspondentes **Get -** e **Set -** propriedades de saudação tooupdate cmdlets dos recursos existentes, e **Remove -** cmdlets tooremove recursos em uma conta de lote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="d6f00-145">Ao usar muitos desses cmdlets em adição toopassing um objeto BatchContext, você precisa toocreate ou passa objetos que contêm configurações de recursos detalhado, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f00-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="d6f00-146">Consulte Olá ajuda detalhada para cada cmdlet para obter exemplos adicionais.</span><span class="sxs-lookup"><span data-stu-id="d6f00-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="d6f00-147">Criar um pool do Lote</span><span class="sxs-lookup"><span data-stu-id="d6f00-147">Create a Batch pool</span></span>
<span data-ttu-id="d6f00-148">Ao criar ou atualizar um pool de lote, selecione a configuração de máquina virtual de hello ou configuração de serviço de nuvem Olá para hello sistema operacional Olá nós de computação (consulte [visão geral do recurso de lote](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="d6f00-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="d6f00-149">Se você especificar a configuração do serviço de nuvem hello, seus nós de computação são representados com uma saudação [versões do sistema operacional de convidado do Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="d6f00-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="d6f00-150">Se você especificar a configuração de máquina virtual hello, você pode especificar uma saudação suporte para Linux ou imagens de VM do Windows hello listado na [Marketplace de máquinas virtuais do Azure][vm_marketplace], ou forneça um personalizado imagem que você preparou.</span><span class="sxs-lookup"><span data-stu-id="d6f00-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="d6f00-151">Quando você executa **AzureBatchPool novo**, passar um objeto PSCloudServiceConfiguration ou PSVirtualMachineConfiguration configurações do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="d6f00-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="d6f00-152">Por exemplo, hello cmdlet a seguir cria um novo pool de lote conosco de computação pequenos de tamanho na configuração de serviço de nuvem hello, criação de uma imagem com a versão do sistema operacional mais recente Olá da família 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="d6f00-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="d6f00-153">Aqui, Olá **CloudServiceConfiguration** parâmetro especifica Olá *$configuration* variável como objeto de PSCloudServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="d6f00-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="d6f00-154">Olá **BatchContext** parâmetro especifica uma variável definida anteriormente *$context* como objeto de BatchAccountContext hello.</span><span class="sxs-lookup"><span data-stu-id="d6f00-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="d6f00-155">número de destino de saudação de nós de computação no novo pool de saudação é determinado por uma fórmula de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d6f00-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="d6f00-156">Nesse caso, a fórmula de saudação é simplesmente **$TargetDedicated = 4**, indicando que o número de saudação de nós de computação no pool de saudação está 4 no máximo.</span><span class="sxs-lookup"><span data-stu-id="d6f00-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="d6f00-157">Consultar pools, trabalhos, tarefas e outros detalhes</span><span class="sxs-lookup"><span data-stu-id="d6f00-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="d6f00-158">Como usar os cmdlets **Get-AzureBatchPool**, **Get-AzureBatchJob**, e **Get-AzureBatchTask** tooquery para entidades criadas em uma conta de lote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="d6f00-159">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="d6f00-159">Query for data</span></span>
<span data-ttu-id="d6f00-160">Por exemplo, use **Get-AzureBatchPools** toofind os pools.</span><span class="sxs-lookup"><span data-stu-id="d6f00-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="d6f00-161">Por padrão essa consulta para todos os pools na sua conta, supondo que você já armazenado objeto BatchAccountContext Olá *$context*:</span><span class="sxs-lookup"><span data-stu-id="d6f00-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="d6f00-162">Usar um filtro OData</span><span class="sxs-lookup"><span data-stu-id="d6f00-162">Use an OData filter</span></span>
<span data-ttu-id="d6f00-163">Você pode fornecer um filtro OData usando Olá **filtro** toofind parâmetro hello apenas objetos que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="d6f00-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="d6f00-164">Por exemplo, você pode localizar todos os pools com ids que começam com "myPool":</span><span class="sxs-lookup"><span data-stu-id="d6f00-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="d6f00-165">Esse método não é tão flexível quanto usar "Where-Object" em um pipeline local.</span><span class="sxs-lookup"><span data-stu-id="d6f00-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="d6f00-166">No entanto, consulta Olá é enviada toohello serviço de lote diretamente para que toda a filtragem ocorre no lado do servidor de saudação, economizando largura de banda de Internet.</span><span class="sxs-lookup"><span data-stu-id="d6f00-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="d6f00-167">Use o parâmetro de Id de saudação</span><span class="sxs-lookup"><span data-stu-id="d6f00-167">Use hello Id parameter</span></span>
<span data-ttu-id="d6f00-168">Um filtro de OData tooan alternativo é Olá toouse **Id** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d6f00-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="d6f00-169">tooquery de um determinado pool com id "myPool":</span><span class="sxs-lookup"><span data-stu-id="d6f00-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="d6f00-170">Olá **Id** parâmetro oferece suporte a somente pesquisa completo-id, não curingas ou filtros de estilo do OData.</span><span class="sxs-lookup"><span data-stu-id="d6f00-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="d6f00-171">Use o parâmetro MaxCount de saudação</span><span class="sxs-lookup"><span data-stu-id="d6f00-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="d6f00-172">Por padrão, cada cmdlet retorna no máximo 1.000 objetos.</span><span class="sxs-lookup"><span data-stu-id="d6f00-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="d6f00-173">Se você atingir esse limite, refine seu filtro toobring volta menos objetos tanto definir explicitamente um máximo usando Olá **MaxCount** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d6f00-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="d6f00-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d6f00-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="d6f00-175">Definir limite superior do tooremove Olá, **MaxCount** too0 ou menos.</span><span class="sxs-lookup"><span data-stu-id="d6f00-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="d6f00-176">Usar o pipeline do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="d6f00-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="d6f00-177">Cmdlets de lote podem utilizar dados toosend de pipeline de PowerShell saudação entre cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d6f00-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="d6f00-178">Isso tem o mesmo efeito que especificar um parâmetro, mas torna trabalhar com várias entidades de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f00-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="d6f00-179">Por exemplo, localize e exiba todas as tarefas em sua conta:</span><span class="sxs-lookup"><span data-stu-id="d6f00-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="d6f00-180">Reinicializar todos os nós de computação em um pool:</span><span class="sxs-lookup"><span data-stu-id="d6f00-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="d6f00-181">Gerenciamento de pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d6f00-181">Application package management</span></span>
<span data-ttu-id="d6f00-182">Pacotes de aplicativos fornecem uma maneira de simplificado toodeploy aplicativos toohello nós de computação em seus pools.</span><span class="sxs-lookup"><span data-stu-id="d6f00-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="d6f00-183">Com hello cmdlets do PowerShell do lote, carregar e gerenciar pacotes de aplicativos em sua conta de lote e implantar nós de toocompute de versões do pacote.</span><span class="sxs-lookup"><span data-stu-id="d6f00-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="d6f00-184">**Criar** um aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d6f00-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="d6f00-185">**Adicionar** um pacote de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="d6f00-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="d6f00-186">Saudação de conjunto **versão padrão** para o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="d6f00-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="d6f00-187">**Listar** pacotes de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d6f00-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="d6f00-188">**Excluir** um pacote de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d6f00-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="d6f00-189">**Excluir** um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d6f00-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="d6f00-190">Você deve excluir todas as versões do pacote de aplicativo do aplicativo antes de excluir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d6f00-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="d6f00-191">Se você tentar toodelete um aplicativo que tem atualmente os pacotes de aplicativos, você receberá um erro de 'conflito de '.</span><span class="sxs-lookup"><span data-stu-id="d6f00-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="d6f00-192">Implantar um pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d6f00-192">Deploy an application package</span></span>
<span data-ttu-id="d6f00-193">Você pode especificar um ou mais pacotes de aplicativos para implantação durante a criação de um pool.</span><span class="sxs-lookup"><span data-stu-id="d6f00-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="d6f00-194">Quando você especificar um pacote no momento da criação de pool, é implantado tooeach nó como Olá nó junções pool.</span><span class="sxs-lookup"><span data-stu-id="d6f00-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="d6f00-195">Pacotes também são implantados quando um nó é reinicializado ou quando sua imagem é refeita.</span><span class="sxs-lookup"><span data-stu-id="d6f00-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="d6f00-196">Especifique a saudação `-ApplicationPackageReference` opção ao criar um pool toodeploy nós de um pacote toohello do pool de aplicativos ao entrarem pool hello.</span><span class="sxs-lookup"><span data-stu-id="d6f00-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="d6f00-197">Primeiro, crie um **PSApplicationPackageReference** de objeto e configurá-lo com hello Id e o pacote de versão do aplicativo deseja que nós de computação do pool de toodeploy toohello:</span><span class="sxs-lookup"><span data-stu-id="d6f00-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="d6f00-198">Agora criar pool hello e especificar o objeto de referência de pacote hello como Olá argumento toohello `ApplicationPackageReferences` opção:</span><span class="sxs-lookup"><span data-stu-id="d6f00-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="d6f00-199">Você pode encontrar mais informações sobre pacotes de aplicativos em [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d6f00-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6f00-200">Você deve [vincular uma conta de armazenamento do Azure](#linked-storage-account-autostorage) tooyour lote conta toouse pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d6f00-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="d6f00-201">Atualizar pacotes de aplicativos de um pool</span><span class="sxs-lookup"><span data-stu-id="d6f00-201">Update a pool's application packages</span></span>
<span data-ttu-id="d6f00-202">aplicativos de saudação tooupdate atribuídos tooan pool existente, primeiro crie um objeto de PSApplicationPackageReference com propriedades de saudação desejada (versão de pacote e a Id de aplicativo):</span><span class="sxs-lookup"><span data-stu-id="d6f00-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="d6f00-203">Em seguida, obter o pool de saudação do lote, limpar todos os pacotes existentes, adicionar nossa nova referência de pacote e atualizar o serviço de lote de saudação com novas configurações de pool hello:</span><span class="sxs-lookup"><span data-stu-id="d6f00-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="d6f00-204">Agora que você atualizou os propriedades do pool de saudação no serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f00-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="d6f00-205">tooactually implantar Olá novo aplicativo pacote toocompute nós no pool hello, no entanto, você deve reinicializar ou refazer em nós.</span><span class="sxs-lookup"><span data-stu-id="d6f00-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="d6f00-206">Você pode reiniciar todos os nós em um pool com este comando:</span><span class="sxs-lookup"><span data-stu-id="d6f00-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="d6f00-207">Você pode implantar vários aplicativos pacotes toohello nós de computação em um pool.</span><span class="sxs-lookup"><span data-stu-id="d6f00-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="d6f00-208">Se você quiser muito*adicionar* um pacote de aplicativo em vez de substituir os pacotes de saudação atualmente implantado, omita Olá `$pool.ApplicationPackageReferences.Clear()` linha acima.</span><span class="sxs-lookup"><span data-stu-id="d6f00-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d6f00-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6f00-209">Next steps</span></span>
* <span data-ttu-id="d6f00-210">Para obter a sintaxe detalhada do cmdlet, veja [Referência de cmdlet do Lote do Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="d6f00-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="d6f00-211">Para obter mais informações sobre aplicativos e pacotes de aplicativos em lote, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d6f00-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/