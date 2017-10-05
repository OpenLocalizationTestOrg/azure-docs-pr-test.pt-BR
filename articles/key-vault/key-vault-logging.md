---
title: Logs do Cofre de Chaves do Azure | Microsoft Docs
description: "Use este tutorial para ajudá-lo a começar a usar os logs do Cofre da Chave do Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="6bac6-103">Logs do Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="6bac6-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="6bac6-104">O Cofre da Chave do Azure está disponível na maioria das regiões.</span><span class="sxs-lookup"><span data-stu-id="6bac6-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="6bac6-105">Para obter mais informações, consulte a [Página de preços do Cofre da Chave](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="6bac6-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="6bac6-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="6bac6-106">Introduction</span></span>
<span data-ttu-id="6bac6-107">Depois de criar um ou mais cofres de chaves, provavelmente você desejará monitorar como e quando os cofres da chave serão acessados e por quem.</span><span class="sxs-lookup"><span data-stu-id="6bac6-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="6bac6-108">Você pode fazer isso ao habilitar o log para o Cofre da Chave, que salva as informações em uma conta de armazenamento do Azure fornecida por você.</span><span class="sxs-lookup"><span data-stu-id="6bac6-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="6bac6-109">Um novo contêiner chamado **insights-logs-auditevent** é automaticamente criado para a conta de armazenamento especificada e você poderá usar essa mesma conta de armazenamento para a coleta de logs de vários cofres da chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="6bac6-110">Você pode acessar suas informações de log em até 10 minutos após a operação do cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="6bac6-111">Na maioria dos casos, será mais rápido do que isso.</span><span class="sxs-lookup"><span data-stu-id="6bac6-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="6bac6-112">Cabe a você gerenciar os logs em sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="6bac6-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="6bac6-113">Use os métodos de controle de acesso padrão do Azure para proteger seus logs ao restringir quem pode acessá-los.</span><span class="sxs-lookup"><span data-stu-id="6bac6-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="6bac6-114">Exclua os logs que você não deseja manter em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6bac6-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="6bac6-115">Use este tutorial para ajudá-lo a começar a usar os logs do Cofre da Chave do Azure, para criar sua conta de armazenamento, para habilitar o log e para interpretar as informações de log coletadas.</span><span class="sxs-lookup"><span data-stu-id="6bac6-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="6bac6-116">Este tutorial não inclui instruções sobre como criar cofres da chave, chaves ou segredos.</span><span class="sxs-lookup"><span data-stu-id="6bac6-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="6bac6-117">Para obter essas informações, confira [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="6bac6-118">Ou, para obter instruções de Interface de linha de comando entre diferentes plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="6bac6-119">No momento, não é possível configurar o Cofre da Chave do Azure no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="6bac6-120">Em vez disso, use estas instruções do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="6bac6-121">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6bac6-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bac6-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6bac6-122">Prerequisites</span></span>
<span data-ttu-id="6bac6-123">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="6bac6-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="6bac6-124">Um cofre da chave existente que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="6bac6-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="6bac6-125">Azure PowerShell, **versão mínima: 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="6bac6-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="6bac6-126">Para instalar o Azure PowerShell e associá-lo à sua assinatura do Azure, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6bac6-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="6bac6-127">Se você já tiver instalado o Azure PowerShell e não souber a versão, no console do Azure PowerShell, digite `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="6bac6-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="6bac6-128">Armazenamento suficiente no Azure para seus logs do Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="6bac6-129"><a id="connect"></a>Conectar-se a suas assinaturas</span><span class="sxs-lookup"><span data-stu-id="6bac6-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="6bac6-130">Inicie uma sessão do PowerShell do Azure e entre em sua conta do Azure com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6bac6-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="6bac6-131">Na janela pop-up do navegador, insira o nome de usuário e a senha da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="6bac6-132">O Azure PowerShell obtém todas as assinaturas que estão associadas a essa conta e, por padrão, usa a primeira.</span><span class="sxs-lookup"><span data-stu-id="6bac6-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="6bac6-133">Se você tiver várias assinaturas, talvez tenha que indicar uma assinatura específica que tenha sido usada para criar o Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="6bac6-134">Digite o seguinte para ver as assinaturas da sua conta:</span><span class="sxs-lookup"><span data-stu-id="6bac6-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="6bac6-135">Em seguida, para especificar a assinatura associada ao cofre de chaves do qual os logs serão registrados, digite:</span><span class="sxs-lookup"><span data-stu-id="6bac6-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="6bac6-136">Esta é uma etapa importante e será especialmente útil se você tiver várias assinaturas associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="6bac6-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="6bac6-137">Você poderá receber um erro para registrar Microsoft.Insights se esta etapa for ignorada.</span><span class="sxs-lookup"><span data-stu-id="6bac6-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="6bac6-138">Para saber mais sobre a configuração do Azure PowerShell, veja [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6bac6-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="6bac6-139"><a id="storage"></a>Criar uma nova conta de armazenamento para seus logs</span><span class="sxs-lookup"><span data-stu-id="6bac6-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="6bac6-140">Embora você possa usar uma conta de armazenamento existente para seus logs, criaremos uma nova conta de armazenamento que será dedicada aos logs do Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="6bac6-141">Para conveniência quando tivermos de especificar isso posteriormente, armazenaremos os detalhes em uma variável chamada **sa**.</span><span class="sxs-lookup"><span data-stu-id="6bac6-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="6bac6-142">Para facilidade de gerenciamento, também usaremos o mesmo grupo de recursos que contém o cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="6bac6-143">No [tutorial de introdução](key-vault-get-started.md), esse grupo de recursos é denominado **ContosoResourceGroup** e continuaremos a usar o local Ásia Oriental.</span><span class="sxs-lookup"><span data-stu-id="6bac6-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="6bac6-144">Substitua esses valores pelos seus, conforme aplicável:</span><span class="sxs-lookup"><span data-stu-id="6bac6-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="6bac6-145">Se você decidir usar uma conta de armazenamento existente, ela deverá usar a mesma assinatura do cofre de chaves e deverá usar o modelo de implantação do Gerenciador de Recursos em vez do modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="6bac6-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="6bac6-146"><a id="identify"></a>Identificar o cofre da chave para seus logs</span><span class="sxs-lookup"><span data-stu-id="6bac6-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="6bac6-147">Em nosso guia de introdução, o nome do cofre de chaves era **ContosoKeyVault** e, portanto, continuaremos a usar esse nome e a armazenar os detalhes em uma variável chamada **kv**:</span><span class="sxs-lookup"><span data-stu-id="6bac6-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="6bac6-148"><a id="enable"></a>Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="6bac6-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="6bac6-149">Para habilitar o log para o Cofre da Chave, usaremos o cmdlet Set-AzureRmDiagnosticSetting, junto com as variáveis que criamos para nossa nova conta de armazenamento e nosso cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="6bac6-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="6bac6-150">Também definiremos o sinalizador **-Enabled** como **$true** e definiremos a categoria como AuditEvent (a única categoria para o log do Cofre de Chaves):</span><span class="sxs-lookup"><span data-stu-id="6bac6-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="6bac6-151">A saída para isso inclui:</span><span class="sxs-lookup"><span data-stu-id="6bac6-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="6bac6-152">Isso confirma que o log está habilitado para o cofre de chave, salvando as informações na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6bac6-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="6bac6-153">Opcionalmente, você também pode definir a política de retenção para os logs, de modo que os logs mais antigos sejam automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="6bac6-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="6bac6-154">Por exemplo, defina a política de retenção usando o sinalizador **-RetentionEnabled** como **$true** e defina o parâmetro **-RetentionInDays** como **90** para que os logs de mais de 90 dias sejam automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="6bac6-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="6bac6-155">O que é registrado em log:</span><span class="sxs-lookup"><span data-stu-id="6bac6-155">What's logged:</span></span>

* <span data-ttu-id="6bac6-156">Todas as solicitações de API REST autenticadas são registradas, o que inclui as solicitações que falharam devido a permissões de acesso, erros do sistema ou solicitações inválidas.</span><span class="sxs-lookup"><span data-stu-id="6bac6-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="6bac6-157">As operações do próprio cofre da chave, o que inclui a criação, a exclusão, a configuração de políticas de acesso ao cofre da chave e a atualização dos atributos do cofre da chave, como as marcas.</span><span class="sxs-lookup"><span data-stu-id="6bac6-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="6bac6-158">As operações em chaves e segredos no cofre da chave, o que inclui criar, modificar ou excluir essas chaves ou segredos; as operações como assinar, verificar, criptografar, descriptografar, encapsular e desencapsular chaves, obter segredos, listar chaves e segredos e suas versões.</span><span class="sxs-lookup"><span data-stu-id="6bac6-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="6bac6-159">Solicitações não autenticadas que resultam em uma resposta 401.</span><span class="sxs-lookup"><span data-stu-id="6bac6-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="6bac6-160">Por exemplo, solicitações que não têm um token de portador, estão malformadas ou expiradas ou têm um token inválido.</span><span class="sxs-lookup"><span data-stu-id="6bac6-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="6bac6-161"><a id="access"></a>Acessar seus logs</span><span class="sxs-lookup"><span data-stu-id="6bac6-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="6bac6-162">Os logs do cofre de chaves são armazenados no contêiner **insights-logs-auditevent** na conta de armazenamento que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="6bac6-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="6bac6-163">Para listar todos os blobs desse contêiner, digite:</span><span class="sxs-lookup"><span data-stu-id="6bac6-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="6bac6-164">Primeiro, crie uma variável para o nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="6bac6-164">First, create a variable for the container name.</span></span> <span data-ttu-id="6bac6-165">Isso será usado no restante do passo a passo.</span><span class="sxs-lookup"><span data-stu-id="6bac6-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="6bac6-166">Para listar todos os blobs desse contêiner, digite:</span><span class="sxs-lookup"><span data-stu-id="6bac6-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="6bac6-167">A saída será parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="6bac6-167">The output will look something similar to this:</span></span>

<span data-ttu-id="6bac6-168">**URI de contêiner: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="6bac6-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="6bac6-169">**Nome**</span><span class="sxs-lookup"><span data-stu-id="6bac6-169">**Name**</span></span>

- - -
<span data-ttu-id="6bac6-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="6bac6-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="6bac6-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="6bac6-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="6bac6-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="6bac6-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="6bac6-173">Como você pode ver nessa saída, os blobs seguem uma convenção de nomenclatura: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="6bac6-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="6bac6-174">Os valores de data e hora usam UTC.</span><span class="sxs-lookup"><span data-stu-id="6bac6-174">The date and time values use UTC.</span></span>

<span data-ttu-id="6bac6-175">Como a mesma conta de armazenamento pode ser usada para coletar logs de vários recursos, a ID do recurso completa no nome do blob será muito útil para acessar ou baixar apenas os blobs que você precisa.</span><span class="sxs-lookup"><span data-stu-id="6bac6-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="6bac6-176">Mas, antes de fazer isso, primeiro vamos mostrar como baixar todos os blobs.</span><span class="sxs-lookup"><span data-stu-id="6bac6-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="6bac6-177">Primeiro, crie uma pasta para baixar os blobs.</span><span class="sxs-lookup"><span data-stu-id="6bac6-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="6bac6-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6bac6-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="6bac6-179">Em seguida, obtenha uma lista de todos os blobs:</span><span class="sxs-lookup"><span data-stu-id="6bac6-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="6bac6-180">Redirecione essa lista pelo 'Get-AzureStorageBlobContent' para baixar os blobs em nossa pasta de destino:</span><span class="sxs-lookup"><span data-stu-id="6bac6-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="6bac6-181">Quando você executar esse segundo comando, o delimitador **/** nos nomes de blob criará uma estrutura de pastas completa na pasta de destino e essa estrutura será usada para baixar e armazenar os blobs como arquivos.</span><span class="sxs-lookup"><span data-stu-id="6bac6-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="6bac6-182">Use caracteres curinga para baixar seletivamente os blobs.</span><span class="sxs-lookup"><span data-stu-id="6bac6-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="6bac6-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6bac6-183">For example:</span></span>

* <span data-ttu-id="6bac6-184">Se você tiver vários cofres da chave e quiser baixar logs de apenas um cofre da chave, chamado CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="6bac6-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="6bac6-185">Se você tiver vários grupos de recursos e quiser baixar os logs para apenas um grupo de recursos, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="6bac6-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="6bac6-186">Se você quiser baixar todos os logs do mês de janeiro de 2016, use `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="6bac6-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="6bac6-187">Agora você está pronto para começar a examinar o conteúdo dos logs.</span><span class="sxs-lookup"><span data-stu-id="6bac6-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="6bac6-188">Mas antes de fazer isso, há mais dois parâmetros para Get-AzureRmDiagnosticSetting que você precisa conhecer:</span><span class="sxs-lookup"><span data-stu-id="6bac6-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="6bac6-189">Para consultar o status das configurações de diagnóstico do recurso cofre de chaves: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="6bac6-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="6bac6-190">Para desabilitar o log do recurso cofre de chaves: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="6bac6-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="6bac6-191"><a id="interpret"></a>Interpretar os logs do Cofre de Chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="6bac6-192">Os blobs individuais são armazenados como texto, formatados como um blob JSON.</span><span class="sxs-lookup"><span data-stu-id="6bac6-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="6bac6-193">Este é um exemplo de entrada de log a partir da execução de `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="6bac6-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="6bac6-194">A tabela a seguir lista os nomes e as descrições de campo.</span><span class="sxs-lookup"><span data-stu-id="6bac6-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="6bac6-195">Nome do campo</span><span class="sxs-lookup"><span data-stu-id="6bac6-195">Field name</span></span> | <span data-ttu-id="6bac6-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="6bac6-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6bac6-197">tempo real</span><span class="sxs-lookup"><span data-stu-id="6bac6-197">time</span></span> |<span data-ttu-id="6bac6-198">Data e hora (UTC).</span><span class="sxs-lookup"><span data-stu-id="6bac6-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="6bac6-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="6bac6-199">resourceId</span></span> |<span data-ttu-id="6bac6-200">ID do Recurso do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="6bac6-201">Para os logs do Cofre de Chaves, isso sempre será a ID do recurso do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="6bac6-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="6bac6-202">operationName</span><span class="sxs-lookup"><span data-stu-id="6bac6-202">operationName</span></span> |<span data-ttu-id="6bac6-203">Nome da operação, como documentado na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="6bac6-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="6bac6-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="6bac6-204">operationVersion</span></span> |<span data-ttu-id="6bac6-205">É a versão da API REST solicitada pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="6bac6-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="6bac6-206">categoria</span><span class="sxs-lookup"><span data-stu-id="6bac6-206">category</span></span> |<span data-ttu-id="6bac6-207">Para logs do Cofre da Chave, AuditEvent é o único valor disponível.</span><span class="sxs-lookup"><span data-stu-id="6bac6-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="6bac6-208">resultType</span><span class="sxs-lookup"><span data-stu-id="6bac6-208">resultType</span></span> |<span data-ttu-id="6bac6-209">Resultado da solicitação da API REST.</span><span class="sxs-lookup"><span data-stu-id="6bac6-209">Result of REST API request.</span></span> |
| <span data-ttu-id="6bac6-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="6bac6-210">resultSignature</span></span> |<span data-ttu-id="6bac6-211">Código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bac6-211">HTTP status.</span></span> |
| <span data-ttu-id="6bac6-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="6bac6-212">resultDescription</span></span> |<span data-ttu-id="6bac6-213">Descrição adicional sobre o resultado, quando disponível.</span><span class="sxs-lookup"><span data-stu-id="6bac6-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="6bac6-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="6bac6-214">durationMs</span></span> |<span data-ttu-id="6bac6-215">Tempo necessário para atender à solicitação da API REST, em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="6bac6-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="6bac6-216">Isso não inclui a latência de rede e, portanto, o tempo medido no lado cliente pode não corresponder a esse tempo.</span><span class="sxs-lookup"><span data-stu-id="6bac6-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="6bac6-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="6bac6-217">callerIpAddress</span></span> |<span data-ttu-id="6bac6-218">Endereço IP do cliente que fez a solicitação.</span><span class="sxs-lookup"><span data-stu-id="6bac6-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="6bac6-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="6bac6-219">correlationId</span></span> |<span data-ttu-id="6bac6-220">Um GUID opcional que o cliente pode passar para correlacionar os logs do lado do cliente aos logs do lado do serviço (Chave do Cofre).</span><span class="sxs-lookup"><span data-stu-id="6bac6-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="6bac6-221">identidade</span><span class="sxs-lookup"><span data-stu-id="6bac6-221">identity</span></span> |<span data-ttu-id="6bac6-222">Identidade do token que foi apresentado ao fazer a solicitação da API REST.</span><span class="sxs-lookup"><span data-stu-id="6bac6-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="6bac6-223">Isso geralmente é um "usuário", uma "entidade de serviço" ou uma combinação "usuário+appId", como no caso de uma solicitação, resultado de um cmdlet do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bac6-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="6bac6-224">propriedades</span><span class="sxs-lookup"><span data-stu-id="6bac6-224">properties</span></span> |<span data-ttu-id="6bac6-225">Esse campo conterá informações diferentes com base na operação (operationName).</span><span class="sxs-lookup"><span data-stu-id="6bac6-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="6bac6-226">Na maioria dos casos, contém informações de cliente (a cadeia de caracteres useragent passada pelo cliente), o URI exato da solicitação da API REST e o código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bac6-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="6bac6-227">Além disso, quando um objeto é retornado como resultado de uma solicitação (por exemplo, KeyCreate ou VaultGet), também conterá o URI da Chave (como "id"), o URI do Cofre ou o URI do Segredo.</span><span class="sxs-lookup"><span data-stu-id="6bac6-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="6bac6-228">Os valores do campo **operationName** estão no formato ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="6bac6-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="6bac6-229">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6bac6-229">For example:</span></span>

* <span data-ttu-id="6bac6-230">Todas as operações do cofre de chaves têm o formato 'Vault`<action>`', como `VaultGet` e `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="6bac6-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="6bac6-231">Todas as operações da chave têm o formato 'Key`<action>`', como `KeySign` e `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="6bac6-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="6bac6-232">Todas as operações do segredo têm o formato 'Secret`<action>`', como `SecretGet` e `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="6bac6-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="6bac6-233">A tabela a seguir lista o operationName e o comando da API REST correspondente.</span><span class="sxs-lookup"><span data-stu-id="6bac6-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="6bac6-234">operationName</span><span class="sxs-lookup"><span data-stu-id="6bac6-234">operationName</span></span> | <span data-ttu-id="6bac6-235">Comando da API REST</span><span class="sxs-lookup"><span data-stu-id="6bac6-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="6bac6-236">Autenticação</span><span class="sxs-lookup"><span data-stu-id="6bac6-236">Authentication</span></span> |<span data-ttu-id="6bac6-237">Via ponto de extremidade do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6bac6-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="6bac6-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="6bac6-238">VaultGet</span></span> |[<span data-ttu-id="6bac6-239">Obter informações sobre um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6bac6-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="6bac6-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="6bac6-240">VaultPut</span></span> |[<span data-ttu-id="6bac6-241">Criar ou atualizar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6bac6-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="6bac6-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="6bac6-242">VaultDelete</span></span> |[<span data-ttu-id="6bac6-243">Excluir um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="6bac6-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="6bac6-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="6bac6-244">VaultPatch</span></span> |[<span data-ttu-id="6bac6-245">Atualizar um cofre da chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="6bac6-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="6bac6-246">VaultList</span></span> |[<span data-ttu-id="6bac6-247">Listar todos os cofres de chaves em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6bac6-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="6bac6-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="6bac6-248">KeyCreate</span></span> |[<span data-ttu-id="6bac6-249">Criar uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="6bac6-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="6bac6-250">KeyGet</span></span> |[<span data-ttu-id="6bac6-251">Obter informações sobre uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="6bac6-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="6bac6-252">KeyImport</span></span> |[<span data-ttu-id="6bac6-253">Importar uma chave para um cofre</span><span class="sxs-lookup"><span data-stu-id="6bac6-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="6bac6-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="6bac6-254">KeyBackup</span></span> |<span data-ttu-id="6bac6-255">[Fazer backup de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bac6-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="6bac6-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="6bac6-256">KeyDelete</span></span> |[<span data-ttu-id="6bac6-257">Excluir uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="6bac6-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="6bac6-258">KeyRestore</span></span> |[<span data-ttu-id="6bac6-259">Restaurar uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="6bac6-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="6bac6-260">KeySign</span></span> |[<span data-ttu-id="6bac6-261">Assinar com uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="6bac6-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="6bac6-262">KeyVerify</span></span> |[<span data-ttu-id="6bac6-263">Verificar com uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="6bac6-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="6bac6-264">KeyWrap</span></span> |[<span data-ttu-id="6bac6-265">Encapsular uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="6bac6-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="6bac6-266">KeyUnwrap</span></span> |[<span data-ttu-id="6bac6-267">Desencapsular uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="6bac6-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="6bac6-268">KeyEncrypt</span></span> |[<span data-ttu-id="6bac6-269">Criptografar com uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="6bac6-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="6bac6-270">KeyDecrypt</span></span> |[<span data-ttu-id="6bac6-271">Descriptografar com uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="6bac6-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="6bac6-272">KeyUpdate</span></span> |[<span data-ttu-id="6bac6-273">Atualizar uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="6bac6-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="6bac6-274">KeyList</span></span> |[<span data-ttu-id="6bac6-275">Listar as chaves em um cofre</span><span class="sxs-lookup"><span data-stu-id="6bac6-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="6bac6-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="6bac6-276">KeyListVersions</span></span> |[<span data-ttu-id="6bac6-277">Listar as versões de uma chave</span><span class="sxs-lookup"><span data-stu-id="6bac6-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="6bac6-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="6bac6-278">SecretSet</span></span> |[<span data-ttu-id="6bac6-279">Criar um segredo</span><span class="sxs-lookup"><span data-stu-id="6bac6-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="6bac6-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="6bac6-280">SecretGet</span></span> |[<span data-ttu-id="6bac6-281">Obter um segredo</span><span class="sxs-lookup"><span data-stu-id="6bac6-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="6bac6-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="6bac6-282">SecretUpdate</span></span> |[<span data-ttu-id="6bac6-283">Atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="6bac6-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="6bac6-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="6bac6-284">SecretDelete</span></span> |[<span data-ttu-id="6bac6-285">Excluir um segredo</span><span class="sxs-lookup"><span data-stu-id="6bac6-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="6bac6-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="6bac6-286">SecretList</span></span> |[<span data-ttu-id="6bac6-287">Listar segredos em um cofre</span><span class="sxs-lookup"><span data-stu-id="6bac6-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="6bac6-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="6bac6-288">SecretListVersions</span></span> |[<span data-ttu-id="6bac6-289">Listar versões de um segredo</span><span class="sxs-lookup"><span data-stu-id="6bac6-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="6bac6-290"><a id="loganalytics"></a>Usar Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6bac6-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="6bac6-291">Você pode usar a solução de Cofre de Chaves do Azure no Log Analytics para examinar logs AuditEvent do Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bac6-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="6bac6-292">Para obter mais informações, incluindo como configurar isso, consulte [Solução Azure Key Vault no Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="6bac6-293">Este artigo também contém instruções se você precisar migrar da solução Key Vault antiga que foi oferecida durante a versão prévia do Log Analytics, em que você primeiro roteava os logs para uma conta de armazenamento do Azure e configurava o Log Analytics para ler daquela conta.</span><span class="sxs-lookup"><span data-stu-id="6bac6-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="6bac6-294"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bac6-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="6bac6-295">Para obter um tutorial que usa o Cofre de Chaves do Azure em um aplicativo Web, confira [Usar o Cofre de Chaves do Azure em um Aplicativo Web](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="6bac6-296">Para referências de programação, consulte [Guia do desenvolvedor do Cofre da Chave do Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="6bac6-297">Para obter uma lista dos cmdlets do Azure PowerShell 1.0 para o Cofre de Chaves do Azure, confira [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="6bac6-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="6bac6-298">Para obter um tutorial sobre a rotação de chaves e o log de auditoria com o Cofre de Chaves do Azure, confira [Como configurar o Cofre de Chaves com a rotação de chaves e auditoria de ponta a ponta](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6bac6-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
