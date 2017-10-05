---
title: "Introdução ao PowerShell do Lote do Azure | Microsoft Docs"
description: "Uma rápida introdução aos cmdlets do Azure PowerShell que podem ser usados para gerenciar os recursos do Lote."
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
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="77d03-103">Gerenciar recursos do Lote com cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="77d03-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="77d03-104">Com os cmdlets do PowerShell do Lote do Azure, você pode executar e criar scripts para muitas das mesmas tarefas que executa com as APIs do Lote, o portal do Azure e a CLI (Interface de Linha de Comando) do Azure.</span><span class="sxs-lookup"><span data-stu-id="77d03-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="77d03-105">Essa é uma breve introdução aos cmdlets que você pode usar para gerenciar suas contas do Lote e trabalhar com seus recursos do Lote, como pools, trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="77d03-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="77d03-106">Para obter uma lista completa de cmdlets do Lote e a sintaxe detalhada do cmdlet, consulte a [Referência de cmdlet do Lote do Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="77d03-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="77d03-107">Este artigo baseia-se nos cmdlets do Azure PowerShell versão 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="77d03-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="77d03-108">É recomendável que você atualize o Azure PowerShell com frequência para tirar proveito de atualizações e aprimoramentos do serviço.</span><span class="sxs-lookup"><span data-stu-id="77d03-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77d03-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77d03-109">Prerequisites</span></span>
<span data-ttu-id="77d03-110">Execute as seguintes operações para usar o Azure PowerShell para gerenciar os recursos de Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="77d03-111">Instalar e configurar o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="77d03-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="77d03-112">Execute o cmdlet **Login-AzureRmAccount** para se conectar à sua assinatura (os cmdlets do Lote do Azure são fornecidos no módulo Azure Resource Manager):</span><span class="sxs-lookup"><span data-stu-id="77d03-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="77d03-113">**Registrar com o namespace do provedor de Lote**.</span><span class="sxs-lookup"><span data-stu-id="77d03-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="77d03-114">Essa operação só precisa ser executada **uma vez por assinatura**.</span><span class="sxs-lookup"><span data-stu-id="77d03-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="77d03-115">Gerenciar contas e chaves do Batch</span><span class="sxs-lookup"><span data-stu-id="77d03-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="77d03-116">Criar uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="77d03-116">Create a Batch account</span></span>
<span data-ttu-id="77d03-117">**New-AzureRmBatchAccount** cria uma conta do Lote em um grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="77d03-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="77d03-118">Se você ainda não tiver um grupo de recursos, crie um executando o cmdlet [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="77d03-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="77d03-119">Especifique uma das regiões do Azure no parâmetro**Location**, como "EUA Central”.</span><span class="sxs-lookup"><span data-stu-id="77d03-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="77d03-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="77d03-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="77d03-121">Em seguida, crie uma conta do Lote no grupo de recursos, especificando um nome para a conta em <*nome_da_conta*> e o local e o nome de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77d03-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="77d03-122">A criação da conta de lote pode levar algum tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="77d03-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="77d03-123">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="77d03-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="77d03-124">O nome da conta do Lote deve ser exclusivo na região do Azure para o grupo de recursos, conter entre três e 24 caracteres e usar somente números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="77d03-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="77d03-125">Obter chaves de acesso da conta</span><span class="sxs-lookup"><span data-stu-id="77d03-125">Get account access keys</span></span>
<span data-ttu-id="77d03-126">**Get-AzureRmBatchAccountKeys** mostra as chaves de acesso associadas a uma conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="77d03-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="77d03-127">Por exemplo, execute o seguinte para obter as chaves primária e secundária da conta criada por você.</span><span class="sxs-lookup"><span data-stu-id="77d03-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="77d03-128">Gerar uma nova chave de acesso</span><span class="sxs-lookup"><span data-stu-id="77d03-128">Generate a new access key</span></span>
<span data-ttu-id="77d03-129">**New-AzureRmBatchAccountKey** gera uma nova chave de conta primária ou secundária para uma conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="77d03-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="77d03-130">Por exemplo, para gerar uma nova chave primária para a sua conta do Batch, digite:</span><span class="sxs-lookup"><span data-stu-id="77d03-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="77d03-131">Para gerar uma nova chave secundária, especifique "Secondary" para o parâmetro **KeyType** .</span><span class="sxs-lookup"><span data-stu-id="77d03-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="77d03-132">É necessário gerar novamente as chaves primária e secundária separadamente.</span><span class="sxs-lookup"><span data-stu-id="77d03-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="77d03-133">Excluir uma conta do Batch</span><span class="sxs-lookup"><span data-stu-id="77d03-133">Delete a Batch account</span></span>
<span data-ttu-id="77d03-134">**Remove-AzureRmBatchAccount** exclui uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="77d03-135">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="77d03-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="77d03-136">Quando solicitado, confirme que você deseja remover a conta.</span><span class="sxs-lookup"><span data-stu-id="77d03-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="77d03-137">A remoção de conta pode levar algum tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="77d03-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="77d03-138">Criar um objeto BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="77d03-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="77d03-139">Para se autenticar usando os cmdlets do PowerShell do Lote ao criar e gerenciar pools, trabalhos, tarefas e outros recursos do Lote, primeiro crie um objeto BatchAccountContext para armazenar o nome e as chaves da conta:</span><span class="sxs-lookup"><span data-stu-id="77d03-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="77d03-140">Você passa o objeto BatchAccountContext para os cmdlets que usam o parâmetro **BatchContext** .</span><span class="sxs-lookup"><span data-stu-id="77d03-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="77d03-141">Por padrão, a chave primária da conta é usada para autenticação, mas você pode selecionar a chave a ser usada alterando a propriedade **KeyInUse** do seu objeto de BatchAccountContext: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="77d03-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="77d03-142">Criar e modificar recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="77d03-142">Create and modify Batch resources</span></span>
<span data-ttu-id="77d03-143">Use cmdlets como **New-AzureBatchPool**, **New-AzureBatchJob** e **New-AzureBatchTask** para criar recursos em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="77d03-144">Há cmdlets correspondentes **Get-** e **Set-** para atualizar as propriedades de recursos existentes e cmdlets **Remove-** para remover recursos em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="77d03-145">Ao usar muitos desses cmdlets, além de passar um objeto BatchContext, você precisa criar ou passar objetos que contêm as configurações detalhadas de recursos, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="77d03-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="77d03-146">Confira a ajuda detalhada de cada cmdlet para obter exemplos adicionais.</span><span class="sxs-lookup"><span data-stu-id="77d03-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="77d03-147">Criar um pool do Lote</span><span class="sxs-lookup"><span data-stu-id="77d03-147">Create a Batch pool</span></span>
<span data-ttu-id="77d03-148">Ao criar ou atualizar um pool de lote, selecione a configuração de serviço de nuvem ou a configuração de máquina virtual para o sistema operacional em nós de computação (confira [Visão geral do recurso de Lote](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="77d03-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="77d03-149">Se você especificar a configuração do serviço de nuvem, os nós de computação serão representados com uma das [versões do sistema operacional convidado do Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="77d03-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="77d03-150">Se você especificar a configuração da máquina virtual, poderá especificar uma das imagens de VM Linux ou Windows com suporte listadas no [Marketplace de Máquinas Virtuais do Azure][vm_marketplace] ou fornecer uma imagem personalizada preparada.</span><span class="sxs-lookup"><span data-stu-id="77d03-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="77d03-151">Ao executar **New-AzureBatchPool**, passe as configurações do sistema operacional em um objeto PSCloudServiceConfiguration ou PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="77d03-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="77d03-152">Por exemplo, o cmdlet a seguir cria um novo pool do Lote com nós de computação de tamanho pequeno na configuração de serviço de nuvem, com a imagem criada com a última versão do sistema operacional da família 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="77d03-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="77d03-153">Aqui, o parâmetro **CloudServiceConfiguration** especifica a variável *$configuration* do objeto PSCloudServiceConfiguration.</span><span class="sxs-lookup"><span data-stu-id="77d03-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="77d03-154">O parâmetro **BatchContext** especifica uma variável definida anteriormente *$context* como o objeto BatchAccountContext.</span><span class="sxs-lookup"><span data-stu-id="77d03-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="77d03-155">O número de nós de computação no novo pool de destino é determinado por uma fórmula de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="77d03-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="77d03-156">Nesse caso, a fórmula é simplesmente **$TargetDedicated=4**, indicando que o número de nós de computação no pool é 4, no máximo.</span><span class="sxs-lookup"><span data-stu-id="77d03-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="77d03-157">Consultar pools, trabalhos, tarefas e outros detalhes</span><span class="sxs-lookup"><span data-stu-id="77d03-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="77d03-158">Use cmdlets como**Get-AzureBatchPool**, **Get-AzureBatchJob** e **Get-AzureBatchTask** para consultar entidades criadas em uma conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="77d03-159">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="77d03-159">Query for data</span></span>
<span data-ttu-id="77d03-160">Por exemplo, use **Get-AzureBatchPools** para encontrar os pools.</span><span class="sxs-lookup"><span data-stu-id="77d03-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="77d03-161">Por padrão, isso consulta todos os pools em sua conta, supondo que você já tenha armazenado o objeto BatchAccountContext em *$context*:</span><span class="sxs-lookup"><span data-stu-id="77d03-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="77d03-162">Usar um filtro OData</span><span class="sxs-lookup"><span data-stu-id="77d03-162">Use an OData filter</span></span>
<span data-ttu-id="77d03-163">Você pode fornecer um filtro OData usando o parâmetro **Filter** para localizar apenas os objetos de seu interesse.</span><span class="sxs-lookup"><span data-stu-id="77d03-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="77d03-164">Por exemplo, você pode localizar todos os pools com ids que começam com "myPool":</span><span class="sxs-lookup"><span data-stu-id="77d03-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="77d03-165">Esse método não é tão flexível quanto usar "Where-Object" em um pipeline local.</span><span class="sxs-lookup"><span data-stu-id="77d03-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="77d03-166">No entanto, a consulta é enviada para o serviço Batch diretamente para que toda a filtragem ocorra no servidor, poupando largura de banda de Internet.</span><span class="sxs-lookup"><span data-stu-id="77d03-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="77d03-167">Use o parâmetro de Id</span><span class="sxs-lookup"><span data-stu-id="77d03-167">Use the Id parameter</span></span>
<span data-ttu-id="77d03-168">Uma alternativa a um filtro OData é usar o parâmetro **Id** .</span><span class="sxs-lookup"><span data-stu-id="77d03-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="77d03-169">Para consultar um pool específico com id "myPool":</span><span class="sxs-lookup"><span data-stu-id="77d03-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="77d03-170">O parâmetro **ID** só dá suporte à pesquisa de ID completo, não a curingas ou a filtros de estilo OData.</span><span class="sxs-lookup"><span data-stu-id="77d03-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="77d03-171">Usar o parâmetro MaxCount</span><span class="sxs-lookup"><span data-stu-id="77d03-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="77d03-172">Por padrão, cada cmdlet retorna no máximo 1.000 objetos.</span><span class="sxs-lookup"><span data-stu-id="77d03-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="77d03-173">Se você atingir esse limite, refine seu filtro para retornar menos objetos ou defina explicitamente um máximo usando o parâmetro **MaxCount** .</span><span class="sxs-lookup"><span data-stu-id="77d03-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="77d03-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="77d03-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="77d03-175">Para remover o limite superior, defina **MaxCount** como 0 ou menos.</span><span class="sxs-lookup"><span data-stu-id="77d03-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="77d03-176">Usar o pipeline do PowerShell</span><span class="sxs-lookup"><span data-stu-id="77d03-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="77d03-177">Os cmdlets do Batch podem aproveitar o pipeline do PowerShell para enviar dados entre cmdlets.</span><span class="sxs-lookup"><span data-stu-id="77d03-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="77d03-178">Isso tem o mesmo efeito que especificar um parâmetro, mas facilita o trabalho com várias entidades.</span><span class="sxs-lookup"><span data-stu-id="77d03-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="77d03-179">Por exemplo, localize e exiba todas as tarefas em sua conta:</span><span class="sxs-lookup"><span data-stu-id="77d03-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="77d03-180">Reinicializar todos os nós de computação em um pool:</span><span class="sxs-lookup"><span data-stu-id="77d03-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="77d03-181">Gerenciamento de pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="77d03-181">Application package management</span></span>
<span data-ttu-id="77d03-182">Os pacotes de aplicativos fornecem uma maneira simplificada de implantar aplicativos para nós de computação em seus pools.</span><span class="sxs-lookup"><span data-stu-id="77d03-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="77d03-183">Com os cmdlets do PowerShell do Lote, carregue e gerencie pacotes de aplicativos em sua conta do Lote e implante versões do pacote para nós de computação.</span><span class="sxs-lookup"><span data-stu-id="77d03-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="77d03-184">**Criar** um aplicativo:</span><span class="sxs-lookup"><span data-stu-id="77d03-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="77d03-185">**Adicionar** um pacote de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="77d03-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="77d03-186">Defina a **versão padrão** para o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="77d03-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="77d03-187">**Listar** pacotes de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="77d03-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="77d03-188">**Excluir** um pacote de aplicativo</span><span class="sxs-lookup"><span data-stu-id="77d03-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="77d03-189">**Excluir** um aplicativo</span><span class="sxs-lookup"><span data-stu-id="77d03-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="77d03-190">Você deve excluir todas as versões do pacote do aplicativo antes de excluir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77d03-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="77d03-191">Se você tentar excluir um aplicativo que atualmente tem pacotes de aplicativos, receberá um erro de 'Conflito'.</span><span class="sxs-lookup"><span data-stu-id="77d03-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="77d03-192">Implantar um pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="77d03-192">Deploy an application package</span></span>
<span data-ttu-id="77d03-193">Você pode especificar um ou mais pacotes de aplicativos para implantação durante a criação de um pool.</span><span class="sxs-lookup"><span data-stu-id="77d03-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="77d03-194">Quando você especifica um pacote no momento da criação do pool, ele é implantado em cada nó como o pool de junções de nó.</span><span class="sxs-lookup"><span data-stu-id="77d03-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="77d03-195">Pacotes também são implantados quando um nó é reinicializado ou quando sua imagem é refeita.</span><span class="sxs-lookup"><span data-stu-id="77d03-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="77d03-196">Especifique a opção `-ApplicationPackageReference` durante a criação de um pool para implantar um pacote de aplicativos nos nós do pool à medida que eles ingressarem no pool.</span><span class="sxs-lookup"><span data-stu-id="77d03-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="77d03-197">Primeiro, crie um objeto **PSApplicationPackageReference** e configure-o com a versão do pacote e a Id de aplicativo que deseja implantar em nós de computação do pool:</span><span class="sxs-lookup"><span data-stu-id="77d03-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="77d03-198">Agora, crie o pool e especifique o objeto de referência do pacote como o argumento para a opção `ApplicationPackageReferences`:</span><span class="sxs-lookup"><span data-stu-id="77d03-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="77d03-199">Veja mais informações sobre pacotes de aplicativos em [Implantar aplicativos em nós de computação com pacotes de aplicativos do Lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="77d03-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77d03-200">Você deve [vincular uma conta de Armazenamento do Azure](#linked-storage-account-autostorage) à sua conta do Lote para usar os pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77d03-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="77d03-201">Atualizar pacotes de aplicativos de um pool</span><span class="sxs-lookup"><span data-stu-id="77d03-201">Update a pool's application packages</span></span>
<span data-ttu-id="77d03-202">Para atualizar os aplicativos atribuídos a um pool existente, primeiro crie um objeto PSApplicationPackageReference com as propriedades desejadas (versão do pacote e Id de aplicativo):</span><span class="sxs-lookup"><span data-stu-id="77d03-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="77d03-203">Em seguida, obtenha o pool do Lote, apague todos os pacotes existentes, adicione nossa nova referência de pacote e atualize o serviço do Lote com as novas configurações do pool:</span><span class="sxs-lookup"><span data-stu-id="77d03-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="77d03-204">Agora você atualizou as propriedades do pool no serviço de Lote.</span><span class="sxs-lookup"><span data-stu-id="77d03-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="77d03-205">Para realmente implantar o novo pacote de aplicativo para nós de computação no pool, entretanto, reinicie ou recrie esses nós.</span><span class="sxs-lookup"><span data-stu-id="77d03-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="77d03-206">Você pode reiniciar todos os nós em um pool com este comando:</span><span class="sxs-lookup"><span data-stu-id="77d03-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="77d03-207">Você pode implantar vários pacotes de aplicativos nos nós de computação em um pool.</span><span class="sxs-lookup"><span data-stu-id="77d03-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="77d03-208">Se você quiser *adicionar* um pacote de aplicativo em vez de substituir os pacotes implantados atualmente, omita a linha `$pool.ApplicationPackageReferences.Clear()` acima.</span><span class="sxs-lookup"><span data-stu-id="77d03-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="77d03-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77d03-209">Next steps</span></span>
* <span data-ttu-id="77d03-210">Para obter a sintaxe detalhada do cmdlet, veja [Referência de cmdlet do Lote do Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="77d03-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="77d03-211">Para obter mais informações sobre aplicativos e pacotes de aplicativos no Lote, confira [Implantação de aplicativos com pacotes de aplicativos do Lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="77d03-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/