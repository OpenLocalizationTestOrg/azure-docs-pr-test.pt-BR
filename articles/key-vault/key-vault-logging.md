---
title: aaaAzure log de Cofre de chave | Microsoft Docs
description: "Use este tutorial toohelp começar com o Cofre de chaves do Azure log."
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
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="dfb64-103">Logs do Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="dfb64-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="dfb64-104">O Cofre da Chave do Azure está disponível na maioria das regiões.</span><span class="sxs-lookup"><span data-stu-id="dfb64-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="dfb64-105">Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="dfb64-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="dfb64-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="dfb64-106">Introduction</span></span>
<span data-ttu-id="dfb64-107">Depois de criar um ou mais cofres de chaves, provavelmente você desejará toomonitor como e quando sua chave de cofres são acessados e por quem.</span><span class="sxs-lookup"><span data-stu-id="dfb64-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="dfb64-108">Você pode fazer isso ao habilitar o log para o Cofre da Chave, que salva as informações em uma conta de armazenamento do Azure fornecida por você.</span><span class="sxs-lookup"><span data-stu-id="dfb64-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="dfb64-109">Um novo contêiner chamado **insights-logs-auditevent** é automaticamente criado para a conta de armazenamento especificada e você poderá usar essa mesma conta de armazenamento para a coleta de logs de vários cofres da chave.</span><span class="sxs-lookup"><span data-stu-id="dfb64-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="dfb64-110">Você pode acessar suas informações de registro em log no máximo, 10 minutos após a chave de saudação cofre a operação.</span><span class="sxs-lookup"><span data-stu-id="dfb64-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="dfb64-111">Na maioria dos casos, será mais rápido do que isso.</span><span class="sxs-lookup"><span data-stu-id="dfb64-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="dfb64-112">É o tooyou toomanage seus logs de sua conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="dfb64-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="dfb64-113">Use seus logs de toosecure de métodos de controle de acesso do Azure standard ao restringir quem pode acessá-los.</span><span class="sxs-lookup"><span data-stu-id="dfb64-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="dfb64-114">Exclua logs que você não deseja mais tookeep na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dfb64-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="dfb64-115">Use este tutorial toohelp começar com o Azure Key Vault log toocreate sua conta de armazenamento, habilitar o log e interpretar as informações de log Olá coletadas.</span><span class="sxs-lookup"><span data-stu-id="dfb64-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="dfb64-116">Este tutorial não inclui instruções sobre como toocreate chave cofres, chaves ou segredos.</span><span class="sxs-lookup"><span data-stu-id="dfb64-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="dfb64-117">Para obter essas informações, confira [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="dfb64-118">Ou, para obter instruções de Interface de linha de comando entre diferentes plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="dfb64-119">No momento, você não pode configurar o Cofre de chaves do Azure no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfb64-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="dfb64-120">Em vez disso, use estas instruções do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb64-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="dfb64-121">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="dfb64-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfb64-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dfb64-122">Prerequisites</span></span>
<span data-ttu-id="dfb64-123">toocomplete neste tutorial, você deve ter Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfb64-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="dfb64-124">Um cofre da chave existente que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="dfb64-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="dfb64-125">Azure PowerShell, **versão mínima: 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="dfb64-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="dfb64-126">tooinstall PowerShell do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfb64-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="dfb64-127">Se você já tiver instalado o PowerShell do Azure e não souber a versão de hello, no console do Azure PowerShell hello, digite `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="dfb64-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="dfb64-128">Armazenamento suficiente no Azure para seus logs do Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="dfb64-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="dfb64-129"><a id="connect"></a>Conecte-se tooyour assinaturas</span><span class="sxs-lookup"><span data-stu-id="dfb64-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="dfb64-130">Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfb64-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="dfb64-131">Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha.</span><span class="sxs-lookup"><span data-stu-id="dfb64-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="dfb64-132">O Azure PowerShell obterá todas as assinaturas de saudação que estão associadas com essa conta e, por padrão, usa Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="dfb64-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="dfb64-133">Se você tiver várias assinaturas, talvez seja necessário toospecify um específico que foi usado toocreate seu Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb64-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="dfb64-134">Digite hello assinaturas de saudação toosee para sua conta a seguir:</span><span class="sxs-lookup"><span data-stu-id="dfb64-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="dfb64-135">Em seguida, toospecify Olá assinatura associada com o Cofre de chaves que fizerem logon, tipo:</span><span class="sxs-lookup"><span data-stu-id="dfb64-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="dfb64-136">Esta é uma etapa importante e será especialmente útil se você tiver várias assinaturas associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="dfb64-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="dfb64-137">Você pode receber um erro tooregister Insights se esta etapa será ignorada.</span><span class="sxs-lookup"><span data-stu-id="dfb64-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="dfb64-138">Para obter mais informações sobre como configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfb64-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="dfb64-139"><a id="storage"></a>Criar uma nova conta de armazenamento para seus logs</span><span class="sxs-lookup"><span data-stu-id="dfb64-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="dfb64-140">Embora você possa usar uma conta de armazenamento existente para seus logs, vamos criar uma nova conta de armazenamento será dedicado tooKey cofre logs.</span><span class="sxs-lookup"><span data-stu-id="dfb64-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="dfb64-141">Para sua conveniência para quando temos toospecify isso mais tarde, armazenamos detalhes de saudação em uma variável chamada **sa**.</span><span class="sxs-lookup"><span data-stu-id="dfb64-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="dfb64-142">Para facilidade de gerenciamento, também usaremos Olá mesmo grupo de recursos como Olá que contenha o nosso Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="dfb64-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="dfb64-143">De saudação [tutorial de Introdução](key-vault-get-started.md), esse grupo de recursos é denominado **ContosoResourceGroup** e continuaremos a localização do toouse Olá Ásia Oriental.</span><span class="sxs-lookup"><span data-stu-id="dfb64-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="dfb64-144">Substitua esses valores pelos seus, conforme aplicável:</span><span class="sxs-lookup"><span data-stu-id="dfb64-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="dfb64-145">Se você decidir toouse uma conta de armazenamento existente, ele deve usar Olá a mesma assinatura conforme seu Cofre de chaves e ele devem usar modelo de implantação do Gerenciador de recursos de hello, em vez de modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="dfb64-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="dfb64-146"><a id="identify"></a>Identificar o Cofre de chaves Olá para seus logs</span><span class="sxs-lookup"><span data-stu-id="dfb64-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="dfb64-147">Em nosso tutorial de Introdução, o nome do Cofre de chaves foi **ContosoKeyVault**, portanto, continuaremos toouse que nomear e armazenar os detalhes de saudação em uma variável chamada **kv**:</span><span class="sxs-lookup"><span data-stu-id="dfb64-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="dfb64-148"><a id="enable"></a>Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="dfb64-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="dfb64-149">tooenable registro em log para o Cofre de chaves, usaremos Olá conjunto AzureRmDiagnosticSetting cmdlet, juntamente com variáveis Olá criada para a nova conta de armazenamento e nosso cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="dfb64-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="dfb64-150">Também vamos definir Olá **-habilitado** sinalizador muito**$true** e defina Olá categoria tooAuditEvent (Olá somente categoria para registro de Cofre de chaves):</span><span class="sxs-lookup"><span data-stu-id="dfb64-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="dfb64-151">saída de Hello para isso inclui:</span><span class="sxs-lookup"><span data-stu-id="dfb64-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="dfb64-152">Isso confirma que o log está ativado para seu Cofre de chaves, salvar a conta de armazenamento tooyour informações.</span><span class="sxs-lookup"><span data-stu-id="dfb64-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="dfb64-153">Opcionalmente, você também pode definir a política de retenção para os logs, de modo que os logs mais antigos sejam automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="dfb64-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="dfb64-154">Por exemplo, definir a política de retenção usando **- RetentionEnabled** sinalizador muito**$true** e defina **- RetentionInDays** parâmetro muito**90** para Se mais de 90 dias de logs serão excluídas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dfb64-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="dfb64-155">O que é registrado em log:</span><span class="sxs-lookup"><span data-stu-id="dfb64-155">What's logged:</span></span>

* <span data-ttu-id="dfb64-156">Todas as solicitações de API REST autenticadas são registradas, o que inclui as solicitações que falharam devido a permissões de acesso, erros do sistema ou solicitações inválidas.</span><span class="sxs-lookup"><span data-stu-id="dfb64-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="dfb64-157">Operações em chave Olá cofre em si, que inclui a criação, exclusão, políticas de acesso do Cofre de chaves de configuração, e atualizar os atributos de Cofre de chaves, como marcas.</span><span class="sxs-lookup"><span data-stu-id="dfb64-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="dfb64-158">Operações em chaves e segredos no cofre de chaves hello, que inclui criar, modificar ou excluir essas chaves ou segredos; operações como entrada, verifique se, criptografar, descriptografar, encapsular e descodificar chaves, obter segredos, listar chaves e segredos e suas versões.</span><span class="sxs-lookup"><span data-stu-id="dfb64-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="dfb64-159">Solicitações não autenticadas que resultam em uma resposta 401.</span><span class="sxs-lookup"><span data-stu-id="dfb64-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="dfb64-160">Por exemplo, solicitações que não têm um token de portador, estão malformadas ou expiradas ou têm um token inválido.</span><span class="sxs-lookup"><span data-stu-id="dfb64-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="dfb64-161"><a id="access"></a>Acessar seus logs</span><span class="sxs-lookup"><span data-stu-id="dfb64-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="dfb64-162">Logs de Cofre de chaves são armazenados em Olá **insights-logs-auditevent** contêiner na conta de armazenamento Olá fornecida.</span><span class="sxs-lookup"><span data-stu-id="dfb64-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="dfb64-163">toolist todos os blobs Olá nesse contêiner, digite:</span><span class="sxs-lookup"><span data-stu-id="dfb64-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="dfb64-164">Primeiro, crie uma variável para o nome do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfb64-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="dfb64-165">Isso será usado restante Olá Olá passo a passo.</span><span class="sxs-lookup"><span data-stu-id="dfb64-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="dfb64-166">toolist todos os blobs Olá nesse contêiner, digite:</span><span class="sxs-lookup"><span data-stu-id="dfb64-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="dfb64-167">saída de Hello ficará toothis algo semelhante:</span><span class="sxs-lookup"><span data-stu-id="dfb64-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="dfb64-168">**URI de contêiner: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="dfb64-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="dfb64-169">**Nome**</span><span class="sxs-lookup"><span data-stu-id="dfb64-169">**Name**</span></span>

- - -
<span data-ttu-id="dfb64-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="dfb64-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="dfb64-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="dfb64-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="dfb64-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="dfb64-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="dfb64-173">Como você pode ver nessa saída, blobs Olá seguem uma convenção de nomenclatura: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="dfb64-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="dfb64-174">os valores de data e hora Olá usam UTC.</span><span class="sxs-lookup"><span data-stu-id="dfb64-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="dfb64-175">Como hello mesma conta de armazenamento pode ser logs toocollect usado para vários recursos, hello ID de recurso completo no nome do blob Olá é muito útil tooaccess ou blobs Olá apenas de download que você precisa.</span><span class="sxs-lookup"><span data-stu-id="dfb64-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="dfb64-176">Mas antes de fazer isso, primeiro abordaremos como toodownload todos Olá blobs.</span><span class="sxs-lookup"><span data-stu-id="dfb64-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="dfb64-177">Primeiro, crie uma saudação de toodownload pasta blobs.</span><span class="sxs-lookup"><span data-stu-id="dfb64-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="dfb64-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dfb64-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="dfb64-179">Em seguida, obtenha uma lista de todos os blobs:</span><span class="sxs-lookup"><span data-stu-id="dfb64-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="dfb64-180">Direcionar essa lista por meio de blobs de saudação do 'Get-AzureStorageBlobContent' toodownload em nossa pasta de destino:</span><span class="sxs-lookup"><span data-stu-id="dfb64-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="dfb64-181">Quando você executa esse comando segundo, Olá  **/**  delimitador em nomes de blob Olá criar uma estrutura de pasta completo na pasta de destino Olá, e essa estrutura será usados toodownload e repositório Olá blobs como arquivos.</span><span class="sxs-lookup"><span data-stu-id="dfb64-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="dfb64-182">tooselectively baixar blobs, use caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="dfb64-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="dfb64-183">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dfb64-183">For example:</span></span>

* <span data-ttu-id="dfb64-184">Se você tiver vários cofres de chaves e deseja logs toodownload para apenas um cofre de chaves, chamado CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="dfb64-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="dfb64-185">Se você tiver vários grupos de recursos e quiser logs toodownload para apenas um grupo de recursos, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="dfb64-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="dfb64-186">Se você quiser toodownload todos os logs de saudação mês de saudação de janeiro de 2016, use `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="dfb64-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="dfb64-187">Você está agora pronto toostart observando o que há no hello logs.</span><span class="sxs-lookup"><span data-stu-id="dfb64-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="dfb64-188">Mas antes de passar para que, dois parâmetros mais para Get-AzureRmDiagnosticSetting que talvez você precise tooknow:</span><span class="sxs-lookup"><span data-stu-id="dfb64-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="dfb64-189">status de saudação tooquery de configurações de diagnóstico para o recurso de Cofre de chaves:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="dfb64-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="dfb64-190">log de toodisable para o recurso de Cofre de chaves:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="dfb64-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="dfb64-191"><a id="interpret"></a>Interpretar os logs do Cofre de Chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="dfb64-192">Os blobs individuais são armazenados como texto, formatados como um blob JSON.</span><span class="sxs-lookup"><span data-stu-id="dfb64-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="dfb64-193">Este é um exemplo de entrada de log a partir da execução de `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="dfb64-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="dfb64-194">Olá tabela a seguir lista nomes de campo hello e descrições.</span><span class="sxs-lookup"><span data-stu-id="dfb64-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="dfb64-195">Nome do campo</span><span class="sxs-lookup"><span data-stu-id="dfb64-195">Field name</span></span> | <span data-ttu-id="dfb64-196">Descrição</span><span class="sxs-lookup"><span data-stu-id="dfb64-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dfb64-197">tempo real</span><span class="sxs-lookup"><span data-stu-id="dfb64-197">time</span></span> |<span data-ttu-id="dfb64-198">Data e hora (UTC).</span><span class="sxs-lookup"><span data-stu-id="dfb64-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="dfb64-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="dfb64-199">resourceId</span></span> |<span data-ttu-id="dfb64-200">ID do Recurso do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb64-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="dfb64-201">Para logs de Cofre de chaves, é sempre ID de recurso de Cofre de chaves do hello.</span><span class="sxs-lookup"><span data-stu-id="dfb64-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="dfb64-202">operationName</span><span class="sxs-lookup"><span data-stu-id="dfb64-202">operationName</span></span> |<span data-ttu-id="dfb64-203">Nome da operação hello, conforme documentado na tabela a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="dfb64-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="dfb64-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="dfb64-204">operationVersion</span></span> |<span data-ttu-id="dfb64-205">Esta é a versão de API REST de saudação solicitada pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="dfb64-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="dfb64-206">categoria</span><span class="sxs-lookup"><span data-stu-id="dfb64-206">category</span></span> |<span data-ttu-id="dfb64-207">Para logs de Cofre de chaves, AuditEvent é um valor único e disponível hello.</span><span class="sxs-lookup"><span data-stu-id="dfb64-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="dfb64-208">resultType</span><span class="sxs-lookup"><span data-stu-id="dfb64-208">resultType</span></span> |<span data-ttu-id="dfb64-209">Resultado da solicitação da API REST.</span><span class="sxs-lookup"><span data-stu-id="dfb64-209">Result of REST API request.</span></span> |
| <span data-ttu-id="dfb64-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="dfb64-210">resultSignature</span></span> |<span data-ttu-id="dfb64-211">Código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="dfb64-211">HTTP status.</span></span> |
| <span data-ttu-id="dfb64-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="dfb64-212">resultDescription</span></span> |<span data-ttu-id="dfb64-213">Descrição adicional sobre o resultado de hello, quando disponível.</span><span class="sxs-lookup"><span data-stu-id="dfb64-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="dfb64-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="dfb64-214">durationMs</span></span> |<span data-ttu-id="dfb64-215">Tempo de solicitação de API REST do tooservice hello, em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="dfb64-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="dfb64-216">Isso não inclui a latência de rede Olá, para que medir no lado do cliente de saudação do tempo de saudação pode não corresponder neste momento.</span><span class="sxs-lookup"><span data-stu-id="dfb64-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="dfb64-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="dfb64-217">callerIpAddress</span></span> |<span data-ttu-id="dfb64-218">Endereço IP do cliente de saudação que fez a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfb64-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="dfb64-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="dfb64-219">correlationId</span></span> |<span data-ttu-id="dfb64-220">Um GUID opcional que Olá cliente pode passar toocorrelate logs do lado do cliente com os logs do lado do serviço (Cofre de chaves).</span><span class="sxs-lookup"><span data-stu-id="dfb64-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="dfb64-221">identidade</span><span class="sxs-lookup"><span data-stu-id="dfb64-221">identity</span></span> |<span data-ttu-id="dfb64-222">Identidade do token Olá apresentado ao fazer a solicitação de API REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="dfb64-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="dfb64-223">Isso geralmente é um "usuário", uma "entidade de serviço" ou uma combinação "usuário+appId", como no caso de uma solicitação, resultado de um cmdlet do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfb64-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="dfb64-224">propriedades</span><span class="sxs-lookup"><span data-stu-id="dfb64-224">properties</span></span> |<span data-ttu-id="dfb64-225">Este campo contém informações diferentes com base na operação de saudação (operationName).</span><span class="sxs-lookup"><span data-stu-id="dfb64-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="dfb64-226">Na maioria dos casos, contém informações de cliente (Olá useragent cadeia de caracteres passada pelo cliente Olá), Olá exata URI de solicitação de API REST e o código de status HTTP.</span><span class="sxs-lookup"><span data-stu-id="dfb64-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="dfb64-227">Além disso, quando um objeto é retornado como resultado de uma solicitação (por exemplo, KeyCreate ou VaultGet) também conterá Olá URI de chave (como "id"), o URI do cofre ou o URI do segredo.</span><span class="sxs-lookup"><span data-stu-id="dfb64-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="dfb64-228">Olá **operationName** valores de campo estão no formato de ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="dfb64-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="dfb64-229">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dfb64-229">For example:</span></span>

* <span data-ttu-id="dfb64-230">Todas as operações do Cofre de chaves têm Olá ' cofre`<action>`' formato, como `VaultGet` e `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="dfb64-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="dfb64-231">Todas as operações de chave têm Olá ' chave`<action>`' formato, como `KeySign` e `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="dfb64-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="dfb64-232">Todas as operações de segredo têm Olá ' segredo`<action>`' formato, como `SecretGet` e `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="dfb64-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="dfb64-233">Olá, a tabela a seguir lista operationName hello e comando correspondente de API REST.</span><span class="sxs-lookup"><span data-stu-id="dfb64-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="dfb64-234">operationName</span><span class="sxs-lookup"><span data-stu-id="dfb64-234">operationName</span></span> | <span data-ttu-id="dfb64-235">Comando da API REST</span><span class="sxs-lookup"><span data-stu-id="dfb64-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="dfb64-236">Autenticação</span><span class="sxs-lookup"><span data-stu-id="dfb64-236">Authentication</span></span> |<span data-ttu-id="dfb64-237">Via ponto de extremidade do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="dfb64-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="dfb64-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="dfb64-238">VaultGet</span></span> |[<span data-ttu-id="dfb64-239">Obter informações sobre um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="dfb64-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="dfb64-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="dfb64-240">VaultPut</span></span> |[<span data-ttu-id="dfb64-241">Criar ou atualizar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="dfb64-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="dfb64-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="dfb64-242">VaultDelete</span></span> |[<span data-ttu-id="dfb64-243">Excluir um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="dfb64-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="dfb64-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="dfb64-244">VaultPatch</span></span> |[<span data-ttu-id="dfb64-245">Atualizar um cofre da chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="dfb64-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="dfb64-246">VaultList</span></span> |[<span data-ttu-id="dfb64-247">Listar todos os cofres de chaves em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dfb64-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="dfb64-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="dfb64-248">KeyCreate</span></span> |[<span data-ttu-id="dfb64-249">Criar uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="dfb64-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="dfb64-250">KeyGet</span></span> |[<span data-ttu-id="dfb64-251">Obter informações sobre uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="dfb64-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="dfb64-252">KeyImport</span></span> |[<span data-ttu-id="dfb64-253">Importar uma chave para um cofre</span><span class="sxs-lookup"><span data-stu-id="dfb64-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="dfb64-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="dfb64-254">KeyBackup</span></span> |<span data-ttu-id="dfb64-255">[Fazer backup de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfb64-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="dfb64-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="dfb64-256">KeyDelete</span></span> |[<span data-ttu-id="dfb64-257">Excluir uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="dfb64-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="dfb64-258">KeyRestore</span></span> |[<span data-ttu-id="dfb64-259">Restaurar uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="dfb64-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="dfb64-260">KeySign</span></span> |[<span data-ttu-id="dfb64-261">Assinar com uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="dfb64-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="dfb64-262">KeyVerify</span></span> |[<span data-ttu-id="dfb64-263">Verificar com uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="dfb64-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="dfb64-264">KeyWrap</span></span> |[<span data-ttu-id="dfb64-265">Encapsular uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="dfb64-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="dfb64-266">KeyUnwrap</span></span> |[<span data-ttu-id="dfb64-267">Desencapsular uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="dfb64-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="dfb64-268">KeyEncrypt</span></span> |[<span data-ttu-id="dfb64-269">Criptografar com uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="dfb64-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="dfb64-270">KeyDecrypt</span></span> |[<span data-ttu-id="dfb64-271">Descriptografar com uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="dfb64-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="dfb64-272">KeyUpdate</span></span> |[<span data-ttu-id="dfb64-273">Atualizar uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="dfb64-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="dfb64-274">KeyList</span></span> |[<span data-ttu-id="dfb64-275">Lista Olá chaves em um cofre</span><span class="sxs-lookup"><span data-stu-id="dfb64-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="dfb64-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="dfb64-276">KeyListVersions</span></span> |[<span data-ttu-id="dfb64-277">Listar versões da saudação de uma chave</span><span class="sxs-lookup"><span data-stu-id="dfb64-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="dfb64-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="dfb64-278">SecretSet</span></span> |[<span data-ttu-id="dfb64-279">Criar um segredo</span><span class="sxs-lookup"><span data-stu-id="dfb64-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="dfb64-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="dfb64-280">SecretGet</span></span> |[<span data-ttu-id="dfb64-281">Obter um segredo</span><span class="sxs-lookup"><span data-stu-id="dfb64-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="dfb64-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="dfb64-282">SecretUpdate</span></span> |[<span data-ttu-id="dfb64-283">Atualizar um segredo</span><span class="sxs-lookup"><span data-stu-id="dfb64-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="dfb64-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="dfb64-284">SecretDelete</span></span> |[<span data-ttu-id="dfb64-285">Excluir um segredo</span><span class="sxs-lookup"><span data-stu-id="dfb64-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="dfb64-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="dfb64-286">SecretList</span></span> |[<span data-ttu-id="dfb64-287">Listar segredos em um cofre</span><span class="sxs-lookup"><span data-stu-id="dfb64-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="dfb64-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="dfb64-288">SecretListVersions</span></span> |[<span data-ttu-id="dfb64-289">Listar versões de um segredo</span><span class="sxs-lookup"><span data-stu-id="dfb64-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="dfb64-290"><a id="loganalytics"></a>Usar Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dfb64-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="dfb64-291">Você pode usar a solução de Cofre de chaves do Azure de saudação em tooreview de análise de logs do Azure Key Vault AuditEvent logs.</span><span class="sxs-lookup"><span data-stu-id="dfb64-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="dfb64-292">Para obter mais informações, incluindo como tooset isso, consulte [solução de Cofre de chaves do Azure na análise de Log](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="dfb64-293">Este artigo também contém instruções se você precisar toomigrate da solução Cofre de chaves antiga Olá que foi fornecida durante a visualização de análise de Log hello, em que você primeiro roteado tooan seus logs conta de armazenamento do Azure e configurado tooread de análise de Log a partir daí.</span><span class="sxs-lookup"><span data-stu-id="dfb64-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="dfb64-294"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfb64-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="dfb64-295">Para obter um tutorial que usa o Cofre de Chaves do Azure em um aplicativo Web, confira [Usar o Cofre de Chaves do Azure em um Aplicativo Web](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="dfb64-296">Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="dfb64-297">Para obter uma lista dos cmdlets do Azure PowerShell 1.0 para o Cofre de Chaves do Azure, confira [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="dfb64-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="dfb64-298">Para obter um tutorial sobre rotação de chaves e o log de auditoria com o Cofre de chaves do Azure, consulte [como toosetup Cofre de chaves com final tooend chave rotação e auditoria](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="dfb64-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
