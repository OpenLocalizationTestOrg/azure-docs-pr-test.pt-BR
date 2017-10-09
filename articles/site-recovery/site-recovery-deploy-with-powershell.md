---
title: "aaaReplicate tooAzure de VMs Hyper-V no portal clássico do hello com o PowerShell | Microsoft Docs"
description: "Automatizar a replicação de saudação de máquinas virtuais de Hyper-V nas nuvens do VMM usando o PowerShell e recuperação de Site no portal clássico Olá"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="49c7b-103">Replicar tooAzure de VMs Hyper-V com o PowerShell no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="49c7b-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49c7b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="49c7b-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="49c7b-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="49c7b-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="49c7b-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="49c7b-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="49c7b-107">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="49c7b-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="49c7b-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="49c7b-108">Overview</span></span>
<span data-ttu-id="49c7b-109">O Azure Site Recovery contribui com a estratégia de recuperação (BCDR) tooyour business desastre e continuidade ao orquestrar a replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="49c7b-110">Para obter uma lista completa de implantação de cenários consulte Olá [visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49c7b-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="49c7b-111">Este artigo mostra como as tarefas comuns do toouse PowerShell tooautomate precisar tooperform ao configurar máquinas virtuais do Azure Site Recovery tooreplicate Hyper-V no armazenamento do System Center VMM nuvens tooAzure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="49c7b-112">artigo Olá inclui os pré-requisitos para o cenário de saudação e mostra a você como tooset um cofre da recuperação de Site, instale Olá provedor Azure Site Recovery no servidor do VMM de origem de saudação, registrar o servidor de saudação no cofre hello, adicione uma conta de armazenamento do Azure, instale o hello Azure Agente de serviços de recuperação em servidores de host do Hyper-V, definir configurações de proteção para nuvens do VMM que serão máquinas virtuais de tooall aplicada protegido e, em seguida, habilite a proteção para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="49c7b-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="49c7b-113">Concluir teste Olá failover toomake se que tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="49c7b-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="49c7b-114">Se você tiver problemas para configurar esse cenário, publique suas perguntas sobre Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="49c7b-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="49c7b-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="49c7b-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="49c7b-116">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="49c7b-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="49c7b-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="49c7b-117">Before you start</span></span>
<span data-ttu-id="49c7b-118">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="49c7b-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="49c7b-119">Pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="49c7b-119">Azure prerequisites</span></span>
* <span data-ttu-id="49c7b-120">Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="49c7b-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="49c7b-121">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49c7b-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="49c7b-122">Você precisará de um toostore replicado dados da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="49c7b-123">conta de saudação precisa de replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="49c7b-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="49c7b-124">Deve estar no hello mesma região do cofre do Azure Site Recovery hello e associar Olá a mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="49c7b-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="49c7b-125">[Saiba mais sobre o Armazenamento do Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49c7b-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="49c7b-126">Você precisará toomake-se de que máquinas virtuais que você deseja tooprotect estejam em conformidade com [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="49c7b-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="49c7b-127">Pré-requisitos do VMM</span><span class="sxs-lookup"><span data-stu-id="49c7b-127">VMM prerequisites</span></span>
* <span data-ttu-id="49c7b-128">Você precisará do servidor VMM em execução no System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="49c7b-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="49c7b-129">Você precisará de pelo menos uma nuvem em Olá servidor VMM que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="49c7b-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="49c7b-130">Olá nuvem deve conter:</span><span class="sxs-lookup"><span data-stu-id="49c7b-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="49c7b-131">Um ou mais grupos de hosts do VMM</span><span class="sxs-lookup"><span data-stu-id="49c7b-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="49c7b-132">Um ou mais servidores host Hyper-V ou clusters em cada grupo de hosts.</span><span class="sxs-lookup"><span data-stu-id="49c7b-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="49c7b-133">Um ou mais VMs no servidor de origem Hyper-V de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="49c7b-134">Pré-requisitos do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="49c7b-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="49c7b-135">Olá servidores host Hyper-V devem estar executando pelo menos **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá as últimas atualizações instaladas.</span><span class="sxs-lookup"><span data-stu-id="49c7b-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="49c7b-136">Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos.</span><span class="sxs-lookup"><span data-stu-id="49c7b-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="49c7b-137">Você precisará agente do cluster Olá tooconfigure manualmente.</span><span class="sxs-lookup"><span data-stu-id="49c7b-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="49c7b-138">toodo isso, no Gerenciador do servidor > Gerenciador de Cluster de Failover, conecte-se o cluster toohello, clique em **configurar função** e selecione **agente de réplica do Hyper-V** em Olá **Selecionar função**tela do Assistente para alta disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="49c7b-139">Qualquer servidor de host do Hyper-V ou cluster para o qual você deseja toomanage proteção deve ser incluído em uma nuvem VMM.</span><span class="sxs-lookup"><span data-stu-id="49c7b-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="49c7b-140">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="49c7b-140">Network mapping prerequisites</span></span>
<span data-ttu-id="49c7b-141">Quando você protege máquinas virtuais no mapeamento de rede do Azure mapeia entre redes VM no servidor do VMM de origem de saudação e procedimentos de saudação do destino redes do Azure tooenable:</span><span class="sxs-lookup"><span data-stu-id="49c7b-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="49c7b-142">Todos os computadores que o failover em Olá mesmo rede pode se conectar a outro, independentemente do plano de recuperação que estão em tooeach.</span><span class="sxs-lookup"><span data-stu-id="49c7b-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="49c7b-143">Se um gateway de rede estiver instalado na rede Azure de destino hello, máquinas virtuais podem se conectar a tooother em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="49c7b-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="49c7b-144">Se você não configurar rede mapeamento apenas as máquinas virtuais que fazem failover no hello mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de failover.</span><span class="sxs-lookup"><span data-stu-id="49c7b-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="49c7b-145">Se você quiser que o mapeamento de rede toodeploy você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="49c7b-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="49c7b-146">saudação de máquinas virtuais que deseja tooprotect no servidor do VMM de origem de saudação deve ser conectado tooa rede VM.</span><span class="sxs-lookup"><span data-stu-id="49c7b-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="49c7b-147">Essa rede deve ser vinculado tooa rede lógica associada à nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="49c7b-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="49c7b-148">Máquinas de virtuais de toowhich replicado uma rede do Azure podem se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="49c7b-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="49c7b-149">Você selecionará essa rede no tempo de saudação de failover.</span><span class="sxs-lookup"><span data-stu-id="49c7b-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="49c7b-150">rede Olá deve estar no hello mesma região que sua assinatura do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="49c7b-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="49c7b-151">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="49c7b-151">PowerShell prerequisites</span></span>
<span data-ttu-id="49c7b-152">Certifique-se de que ter toogo pronto do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="49c7b-153">Se você já estiver usando o PowerShell, você precisará tooupgrade tooversion 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="49c7b-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="49c7b-154">Para obter informações sobre como configurar o PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="49c7b-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="49c7b-155">Depois de você ter instalado e configurado o PowerShell, você pode exibir todos os cmdlets de saudação disponíveis para o serviço de saudação [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49c7b-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="49c7b-156">toolearn sobre dicas que podem ajudá-lo a usar os cmdlets de saudação, como como valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, consulte [Introdução aos Cmdlets do Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="49c7b-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="49c7b-157">Etapa 1: Definir a assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="49c7b-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="49c7b-158">No PowerShell, execute estes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="49c7b-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="49c7b-159">Substitua elementos Olá Olá "< >" com as informações específicas.</span><span class="sxs-lookup"><span data-stu-id="49c7b-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="49c7b-160">Etapa 2: criar um cofre da Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="49c7b-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="49c7b-161">No PowerShell, substitua elementos Olá Olá "< >" com suas informações específicas e execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="49c7b-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="49c7b-162">Etapa 3: gerar uma chave de registro do cofre</span><span class="sxs-lookup"><span data-stu-id="49c7b-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="49c7b-163">Gere uma chave de registro no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="49c7b-164">Depois de baixar Olá provedor Azure Site Recovery e instalá-lo no servidor do VMM hello, você usará esse servidor do VMM Olá tooregister chave no cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="49c7b-165">Obter o arquivo de configuração do cofre hello e defina o contexto de saudação:</span><span class="sxs-lookup"><span data-stu-id="49c7b-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="49c7b-166">Definir o contexto do cofre Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="49c7b-167">Etapa 4: Instalar Olá provedor Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="49c7b-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="49c7b-168">Na máquina do VMM hello, crie um diretório executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="49c7b-169">Extrair arquivos hello usando o provedor de saudação baixada executando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="49c7b-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="49c7b-170">Instale o provedor de saudação usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-170">Install hello provider using hello following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="49c7b-171">Aguarde Olá toofinish de instalação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="49c7b-172">Registre o servidor de saudação no cofre de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="49c7b-173">Etapa 5: criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="49c7b-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="49c7b-174">Se você não tiver uma conta de armazenamento do Azure, crie uma conta de replicação geográfica habilitada executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="49c7b-175">Observe que a conta de armazenamento Olá deve ser Olá mesma região que o serviço do Azure Site Recovery hello e associar Olá a mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="49c7b-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="49c7b-176">Etapa 6: Instalar hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="49c7b-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="49c7b-177">Olá portal do Azure, o agente de serviços de recuperação do Azure Olá instalação em cada servidor de host do Hyper-V localizado nas nuvens do VMM Olá deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="49c7b-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="49c7b-178">Execute Olá comando a seguir em todos os hosts do VMM:</span><span class="sxs-lookup"><span data-stu-id="49c7b-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="49c7b-179">Etapa 7: definir as configurações da proteção de nuvem</span><span class="sxs-lookup"><span data-stu-id="49c7b-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="49c7b-180">Crie um tooAzure de perfil de proteção de nuvem executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="49c7b-181">Obtenha um contêiner de proteção executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="49c7b-182">Inicie associação de saudação do recipiente de proteção de saudação com nuvem hello:</span><span class="sxs-lookup"><span data-stu-id="49c7b-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="49c7b-183">Após o trabalho de hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="49c7b-184">Depois que o trabalho de saudação concluiu o processamento, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-184">After hello job has finished processing, run hello following command:</span></span>

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



<span data-ttu-id="49c7b-185">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="49c7b-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="49c7b-186">Etapa 8: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="49c7b-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="49c7b-187">Antes de começar o mapeamento de rede Verifique se máquinas virtuais no servidor do VMM de origem de saudação tooa conectado rede VM.</span><span class="sxs-lookup"><span data-stu-id="49c7b-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="49c7b-188">Além disso, crie uma ou mais redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="49c7b-189">Observe que várias redes VM podem ser mapeadas tooa única rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="49c7b-190">Observe que se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover.</span><span class="sxs-lookup"><span data-stu-id="49c7b-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="49c7b-191">Se não houver uma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="49c7b-192">Olá primeiro comando obtém servidores para o Cofre de recuperação de Site do Azure atual hello.</span><span class="sxs-lookup"><span data-stu-id="49c7b-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="49c7b-193">comando Olá armazena servidores do Microsoft Azure Site Recovery Olá na variável de matriz de saudação $Servers.</span><span class="sxs-lookup"><span data-stu-id="49c7b-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="49c7b-194">Olá segundo comando obtém a rede de recuperação de site Olá para o primeiro servidor de saudação na matriz de saudação $Servers.</span><span class="sxs-lookup"><span data-stu-id="49c7b-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="49c7b-195">comando Olá armazena redes Olá na variável de saudação $Networks.</span><span class="sxs-lookup"><span data-stu-id="49c7b-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="49c7b-196">Olá terceiro comando obtém suas assinaturas do Azure usando o cmdlet Get-AzureSubscription de Olá e, em seguida, armazena esse valor na variável Olá $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="49c7b-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="49c7b-197">Olá quarto comando obtém as redes virtuais do Azure usando o cmdlet Get-AzureVNetSite de saudação e, em seguida, esse valor na variável Olá $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="49c7b-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="49c7b-198">Olá final cria um mapeamento entre Olá primário e rede Olá máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="49c7b-199">Olá cmdlet especifica a rede primária hello como o primeiro elemento de saudação do $Networks.</span><span class="sxs-lookup"><span data-stu-id="49c7b-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="49c7b-200">Olá cmdlet especifica uma rede de máquina virtual como o primeiro elemento de saudação do $AzureVmNetworks usando sua ID.</span><span class="sxs-lookup"><span data-stu-id="49c7b-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="49c7b-201">comando de saudação inclui sua ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="49c7b-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="49c7b-202">Etapa 9: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="49c7b-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="49c7b-203">Depois de servidores, nuvens e redes configuradas corretamente, você pode habilitar a proteção para máquinas virtuais na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="49c7b-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="49c7b-204">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="49c7b-204">Note hello following:</span></span>

<span data-ttu-id="49c7b-205">Máquinas virtuais devem cumprir os [Pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="49c7b-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="49c7b-206">sistema operacional do tooenable proteção hello e propriedades do disco do sistema operacional devem ser definidas para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="49c7b-207">Quando você cria uma máquina virtual no VMM usando um modelo de máquina virtual, você pode definir propriedade de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="49c7b-208">Você também pode definir essas propriedades para máquinas virtuais existentes em Olá **geral** e **configuração de Hardware** guias de propriedades de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="49c7b-209">Se você não definir essas propriedades no VMM, você será capaz de tooconfigure-los no portal do Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="49c7b-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="49c7b-210">proteção de tooenable executar Olá contêiner de proteção do comando tooget Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="49c7b-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="49c7b-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="49c7b-212">Obtenha a entidade de proteção de saudação (VM) executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="49c7b-213">Habilite hello DR para Olá VM executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="49c7b-214">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="49c7b-214">Test your deployment</span></span>
<span data-ttu-id="49c7b-215">planejar a sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar um failover de teste para Olá tootest.</span><span class="sxs-lookup"><span data-stu-id="49c7b-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="49c7b-216">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="49c7b-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="49c7b-217">Observe que:</span><span class="sxs-lookup"><span data-stu-id="49c7b-217">Note that:</span></span>

* <span data-ttu-id="49c7b-218">Se você quiser tooconnect toohello VM no Azure usando a área de trabalho remota após o failover hello, habilite Conexão de área de trabalho remota na máquina virtual de saudação antes de executar o failover de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="49c7b-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="49c7b-219">Após o failover, você usará uma público IP endereço tooconnect toohello VM no Azure usando a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="49c7b-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="49c7b-220">Se você quiser toodo isso, certifique-se de que você não tem qualquer política de domínio que impedem a máquina de virtual tooa conectar usando um endereço público.</span><span class="sxs-lookup"><span data-stu-id="49c7b-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="49c7b-221">conclusão de saudação do toocheck da operação de Olá, siga as etapas de saudação em [monitorar a atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="49c7b-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="49c7b-222">Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="49c7b-222">Create a recovery plan</span></span>
1. <span data-ttu-id="49c7b-223">Criar um arquivo. XML como um modelo para o plano de recuperação usando dados de saudação abaixo e salve-o como "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="49c7b-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="49c7b-224">Alterar o nó de RecoveryPlan Olá Id, nome, PrimaryServerId e SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="49c7b-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="49c7b-225">Altere Olá ProtectionEntity nó PrimaryProtectionEntityId (vmid do VMM).</span><span class="sxs-lookup"><span data-stu-id="49c7b-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="49c7b-226">Você pode adicionar mais VMs adicionando mais nós ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="49c7b-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="49c7b-227">Preencha dados Olá no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="49c7b-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="49c7b-228">Crie hello RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="49c7b-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="49c7b-229">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="49c7b-229">Run a test failover</span></span>
1. <span data-ttu-id="49c7b-230">Obter o objeto de RecoveryPlan de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="49c7b-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="49c7b-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="49c7b-232">Inicie o failover de teste Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="49c7b-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="49c7b-233"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="49c7b-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="49c7b-234">Use hello atividade de saudação toomonitor comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="49c7b-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="49c7b-235">Observe que você tenha toowait entre trabalhos de saudação toofinish de processamento.</span><span class="sxs-lookup"><span data-stu-id="49c7b-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="49c7b-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49c7b-236">Next steps</span></span>
<span data-ttu-id="49c7b-237">[Leia mais](/powershell/azure/overview) sobre os cmdlets do PowerShell do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="49c7b-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="49c7b-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="49c7b-238"></a>.</span></span>
