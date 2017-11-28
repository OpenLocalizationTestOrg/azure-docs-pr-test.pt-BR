---
title: "Replicar VMs do Hyper-V no Azure no Portal Clássico com o PowerShell |Microsoft Docs"
description: "Automatizar a replicação de máquinas virtuais do Hyper-V em nuvens do VMM usando o Site Recovery e o PowerShell no Portal Clássico"
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="68344-103">Replicar VMs do Hyper-V no Azure com o PowerShell no Portal Clássico</span><span class="sxs-lookup"><span data-stu-id="68344-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68344-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="68344-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="68344-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68344-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="68344-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="68344-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="68344-107">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="68344-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="68344-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="68344-108">Overview</span></span>
<span data-ttu-id="68344-109">O Azure Site Recovery colabora com sua estratégia de BCDR (continuidade de negócios e recuperação de desastre) gerenciando replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="68344-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="68344-110">Para obter uma lista completa de cenários de implantação, consulte a [Visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68344-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="68344-111">Este artigo mostra como usar o PowerShell para automatizar tarefas comuns que você precisa executar quando você configura o Azure Site Recovery para replicar máquinas virtuais Hyper-V em nuvens do System Center VMM para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="68344-112">O artigo inclui os pré-requisitos para o cenário e mostra como configurar um cofre de Recuperação de Site, instalar o Provedor do Azure Site Recovery no servidor VMM de origem, registrar o servidor no cofre, adicionar uma conta de armazenamento do Azure, instalar o agente dos Serviços de Recuperação do Azure nos servidores de host Hyper-V, definir configurações de proteção para nuvens VMM que serão aplicadas a todas as máquinas virtuais protegidas e habilitar a proteção para essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="68344-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="68344-113">Conclua testando o failover para verificar se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="68344-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="68344-114">Se você enfrentar problemas ao configurar esse cenário, publique suas perguntas no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="68344-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="68344-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="68344-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="68344-116">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="68344-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="68344-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="68344-117">Before you start</span></span>
<span data-ttu-id="68344-118">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="68344-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="68344-119">Pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="68344-119">Azure prerequisites</span></span>
* <span data-ttu-id="68344-120">Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="68344-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="68344-121">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68344-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="68344-122">Você precisará de uma conta de armazenamento do Azure para armazenar os dados replicados no Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="68344-123">A conta precisa estar com a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="68344-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="68344-124">Ela deve estar localizada na mesma região que o cofre do Azure Site Recovery e ser associada à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="68344-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="68344-125">[Saiba mais sobre o Armazenamento do Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="68344-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="68344-126">Você precisará verificar se as máquinas virtuais que deseja proteger atendem aos [requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="68344-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="68344-127">Pré-requisitos do VMM</span><span class="sxs-lookup"><span data-stu-id="68344-127">VMM prerequisites</span></span>
* <span data-ttu-id="68344-128">Você precisará do servidor VMM em execução no System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="68344-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="68344-129">Você precisará de pelo menos uma nuvem no servidor VMM que deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="68344-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="68344-130">A nuvem deve conter:</span><span class="sxs-lookup"><span data-stu-id="68344-130">The cloud should contain:</span></span>
  * <span data-ttu-id="68344-131">Um ou mais grupos de hosts do VMM</span><span class="sxs-lookup"><span data-stu-id="68344-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="68344-132">Um ou mais servidores host Hyper-V ou clusters em cada grupo de hosts.</span><span class="sxs-lookup"><span data-stu-id="68344-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="68344-133">Uma ou mais máquinas virtuais no servidor Hyper-V de origem.</span><span class="sxs-lookup"><span data-stu-id="68344-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="68344-134">Pré-requisitos do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="68344-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="68344-135">Os servidores host do Hyper-V devem estar executando pelo menos o **Windows Server 2012** com a função Hyper-V ou o **Microsoft Hyper-V Server 2012** e ter as atualizações mais recentes instaladas.</span><span class="sxs-lookup"><span data-stu-id="68344-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="68344-136">Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente se você tiver um cluster de baseados em endereços IP estáticos.</span><span class="sxs-lookup"><span data-stu-id="68344-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="68344-137">Você precisará configurar o agente de cluster manualmente.</span><span class="sxs-lookup"><span data-stu-id="68344-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="68344-138">Para fazer isso, no Gerenciador do Servidor > Gerenciador de Cluster de Failover, conecte-se ao cluster, clique em **Configurar função** e selecione **Agente de Réplica do Hyper-V** na tela **Selecionar função** do Assistente para Alta Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="68344-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="68344-139">Qualquer cluster ou servidor host Hyper-V para o qual você desejar gerenciar a proteção deverá ser incluído em uma nuvem VMM.</span><span class="sxs-lookup"><span data-stu-id="68344-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="68344-140">Pré-requisitos de mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="68344-140">Network mapping prerequisites</span></span>
<span data-ttu-id="68344-141">Quando você proteger máquinas virtuais na rede do Azure mapeando mapas entre redes VM no servidor VMM de origem e nas redes do Azure destino para habilitar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="68344-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="68344-142">Todas as máquinas que passarem por failover na mesma rede poderão se conectar entre si, independentemente do plano de recuperação em que estão.</span><span class="sxs-lookup"><span data-stu-id="68344-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="68344-143">Além disso, se um gateway de rede for configurado na rede Azure de destino, as máquinas virtuais poderão se conectar a outras máquinas virtuais locais.</span><span class="sxs-lookup"><span data-stu-id="68344-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="68344-144">Se você não configurar o mapeamento de rede, somente máquinas virtuais com failover no mesmo plano de recuperação poderão se conectar entre si após o failover no Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="68344-145">Se desejar implantar o mapeamento de rede, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="68344-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="68344-146">As máquinas virtuais que você deseja proteger no servidor VMM de origem devem estar conectadas a uma rede VM.</span><span class="sxs-lookup"><span data-stu-id="68344-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="68344-147">Essa rede deve ser vinculada a uma rede lógica que esteja associada à nuvem.</span><span class="sxs-lookup"><span data-stu-id="68344-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="68344-148">Uma rede do Azure à qual as máquinas virtuais replicadas possam se conectar após o failover.</span><span class="sxs-lookup"><span data-stu-id="68344-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="68344-149">Você selecionará esta rede no momento do failover.</span><span class="sxs-lookup"><span data-stu-id="68344-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="68344-150">A rede deve estar na mesma região de sua assinatura do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="68344-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="68344-151">Pré-requisitos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="68344-151">PowerShell prerequisites</span></span>
<span data-ttu-id="68344-152">Verifique se você tem o PowerShell do Azure pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="68344-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="68344-153">Se você já estiver usando o PowerShell, precisará atualizar para a versão 0.8.10 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="68344-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="68344-154">Para saber mais sobre como configurar o PowerShell, confira [Como instalar e configurar o PowerShell do Azure](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="68344-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="68344-155">Depois de instalar e configurar o PowerShell, você poderá exibir todos os cmdlets disponíveis para o serviço [aqui](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="68344-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="68344-156">Para obter dicas que podem ajudar você a usar os cmdlets, por exemplo, como os valores de parâmetro, as entradas e saídas são tratadas normalmente no Azure PowerShell, confira [Introdução aos cmdlets do Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="68344-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="68344-157">Etapa 1: definir a assinatura</span><span class="sxs-lookup"><span data-stu-id="68344-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="68344-158">No PowerShell, execute estes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="68344-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="68344-159">Substitua os elementos dentro de "< >" por suas informações específicas.</span><span class="sxs-lookup"><span data-stu-id="68344-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="68344-160">Etapa 2: criar um cofre da Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="68344-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="68344-161">No PowerShell, substitua os elementos dentro de "< >" por informações específicas, e execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="68344-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="68344-162">Etapa 3: gerar uma chave de registro do cofre</span><span class="sxs-lookup"><span data-stu-id="68344-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="68344-163">Gere uma chave de registro no cofre.</span><span class="sxs-lookup"><span data-stu-id="68344-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="68344-164">Após baixar o Provedor do Azure Site Recovery e instalá-lo no servidor VMM, você usará essa chave para registrar o servidor VMM no cofre.</span><span class="sxs-lookup"><span data-stu-id="68344-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="68344-165">Obtenha o arquivo de configuração do cofre e defina o contexto:</span><span class="sxs-lookup"><span data-stu-id="68344-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="68344-166">Defina o contexto de cofre, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="68344-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="68344-167">Etapa 4: instalar o Provedor do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="68344-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="68344-168">Na máquina da VMM, crie um diretório executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="68344-169">Extraia os arquivos usando o provedor baixado, executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="68344-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="68344-170">Instale o provedor usando os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68344-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="68344-171">Aguarde a conclusão da instalação.</span><span class="sxs-lookup"><span data-stu-id="68344-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="68344-172">Registre o servidor no cofre usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="68344-173">Etapa 5: criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="68344-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="68344-174">Se você não tiver uma conta de armazenamento do Azure, crie uma conta com replicação geográfica habilitada executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="68344-175">Observe que a conta de armazenamento precisa estar na mesma região que o serviço Azure Site Recovery e associada à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="68344-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="68344-176">Etapa 6: instalar o agente dos Serviços de Recuperação do Azure</span><span class="sxs-lookup"><span data-stu-id="68344-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="68344-177">No Portal do Azure, instale o agente dos Serviços de Recuperação do Azure em cada servidor de host Hyper-V localizado nas nuvens VMM que você deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="68344-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="68344-178">Execute o comando a seguir em todos os hosts VMM:</span><span class="sxs-lookup"><span data-stu-id="68344-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="68344-179">Etapa 7: definir as configurações da proteção de nuvem</span><span class="sxs-lookup"><span data-stu-id="68344-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="68344-180">Crie um perfil de proteção de nuvem no Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="68344-181">Obtenha um contêiner de proteção executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="68344-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="68344-182">Inicie a associação do contêiner de proteção com a nuvem:</span><span class="sxs-lookup"><span data-stu-id="68344-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="68344-183">Após a conclusão do trabalho, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="68344-184">Após a conclusão do processamento do trabalho, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="68344-185">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="68344-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="68344-186">Etapa 8: configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="68344-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="68344-187">Antes de começar o mapeamento de rede, verifique se as máquinas virtuais no servidor VMM de origem estão conectadas a uma rede VM.</span><span class="sxs-lookup"><span data-stu-id="68344-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="68344-188">Além disso, crie uma ou mais redes virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="68344-189">Observe que várias redes VM podem ser mapeadas para uma única rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="68344-190">Observe que, se a rede de destino tiver várias sub-redes, e uma dessas sub-redes tiver o mesmo nome que a sub-rede em que a máquina virtual de origem está localizada, a máquina virtual de réplica será conectada à sub-rede de destino após o failover.</span><span class="sxs-lookup"><span data-stu-id="68344-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="68344-191">Se não houver uma sub-rede de destino com um nome correspondente, a máquina virtual será conectada à primeira sub-rede na rede.</span><span class="sxs-lookup"><span data-stu-id="68344-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="68344-192">O primeiro comando obtém servidores para o cofre atual do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="68344-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="68344-193">O comando armazena os servidores do Microsoft Azure Site Recovery na variável de matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="68344-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="68344-194">O segundo comando obtém a rede de recuperação de site para o primeiro servidor na matriz $Servers.</span><span class="sxs-lookup"><span data-stu-id="68344-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="68344-195">O comando armazena as redes na variável $Networks.</span><span class="sxs-lookup"><span data-stu-id="68344-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="68344-196">O terceiro comando obtém suas assinaturas do Azure usando o cmdlet Get-AzureSubscription e, em seguida, armazena esse valor na variável $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="68344-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="68344-197">O quarto comando obtém redes virtuais do Azure usando o cmdlet Get-AzureVNetSite e, em seguida, armazena esse valor na variável $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="68344-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="68344-198">O cmdlet final cria um mapeamento entre a rede principal e a rede de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="68344-199">O cmdlet especifica a rede principal como o primeiro elemento de $Networks.</span><span class="sxs-lookup"><span data-stu-id="68344-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="68344-200">O cmdlet especifica uma rede de máquina virtual como o primeiro elemento de $AzureVmNetworks usando sua ID.</span><span class="sxs-lookup"><span data-stu-id="68344-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="68344-201">O comando inclui a ID da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="68344-202">Etapa 9: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="68344-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="68344-203">Depois de redes, servidores e nuvens estarem configurados corretamente, você pode ativar a proteção para máquinas virtuais na nuvem.</span><span class="sxs-lookup"><span data-stu-id="68344-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="68344-204">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="68344-204">Note the following:</span></span>

<span data-ttu-id="68344-205">Máquinas virtuais devem cumprir os [Pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="68344-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="68344-206">Para habilitar a proteção, o sistema operacional e as propriedades do disco do sistema operacional devem estar definidos para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="68344-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="68344-207">Ao criar uma máquina virtual no VMM usando um modelo de máquina virtual, é possível definir a propriedade.</span><span class="sxs-lookup"><span data-stu-id="68344-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="68344-208">Você também pode definir essas propriedades para máquinas virtuais existentes nas guias **Geral** e **Configuração de Hardware** das propriedades da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68344-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="68344-209">Se você não definir essas propriedades no VMM, poderá configurá-las no portal de Recuperação de Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="68344-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="68344-210">Para habilitar a proteção, execute o seguinte comando para obter o contêiner de proteção:</span><span class="sxs-lookup"><span data-stu-id="68344-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="68344-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="68344-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="68344-212">Obtenha a entidade de proteção (VM) executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="68344-213">Habilite o DR para a VM executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="68344-214">Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="68344-214">Test your deployment</span></span>
<span data-ttu-id="68344-215">Para testar sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consistente de várias máquinas virtuais e executar um failover de teste para o plano.</span><span class="sxs-lookup"><span data-stu-id="68344-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="68344-216">O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.</span><span class="sxs-lookup"><span data-stu-id="68344-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="68344-217">Observe que:</span><span class="sxs-lookup"><span data-stu-id="68344-217">Note that:</span></span>

* <span data-ttu-id="68344-218">Se você quiser se conectar à máquina virtual no Azure usando a Área de trabalho remota após o failover, habilite a Conexão de Área de Trabalho Remota na máquina virtual antes de executar o teste de failover.</span><span class="sxs-lookup"><span data-stu-id="68344-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="68344-219">Após o failover, você usará um endereço IP público para conectar-se à máquina virtual no Azure usando a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="68344-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="68344-220">Se você quiser fazer isso, verifique se não tem nenhuma política de domínio que o impeça de se conectar a uma máquina virtual usando um endereço público.</span><span class="sxs-lookup"><span data-stu-id="68344-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="68344-221">Para verificar a conclusão da operação, execute as etapas em [Monitorar a Atividade](#monitor).</span><span class="sxs-lookup"><span data-stu-id="68344-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="68344-222">Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="68344-222">Create a recovery plan</span></span>
1. <span data-ttu-id="68344-223">Crie um arquivo .xml como um modelo para seu plano de recuperação usando os dados a seguir e salve-o como "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="68344-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="68344-224">Altere a ID do nó RecoveryPlan, o Nome, PrimaryServerId e SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="68344-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="68344-225">Altere o nó ProtectionEntity, PrimaryProtectionEntityId (vmid de VMM).</span><span class="sxs-lookup"><span data-stu-id="68344-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="68344-226">Você pode adicionar mais VMs adicionando mais nós ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="68344-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="68344-227">Preencha os dados no modelo:</span><span class="sxs-lookup"><span data-stu-id="68344-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="68344-228">Crie o RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="68344-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="68344-229">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="68344-229">Run a test failover</span></span>
1. <span data-ttu-id="68344-230">Obtenha o objeto RecoveryPlan executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="68344-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="68344-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="68344-232">Inicie o teste de failover executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68344-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="68344-233"><a name=monitor></a> Monitorar a atividade</span><span class="sxs-lookup"><span data-stu-id="68344-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="68344-234">Use os seguintes comandos para monitorar a atividade.</span><span class="sxs-lookup"><span data-stu-id="68344-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="68344-235">Observe que é necessário aguardar a conclusão do processamento entre os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="68344-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="68344-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68344-236">Next steps</span></span>
<span data-ttu-id="68344-237">[Leia mais](/powershell/azure/overview) sobre os cmdlets do PowerShell do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="68344-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="68344-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="68344-238"></a>.</span></span>
