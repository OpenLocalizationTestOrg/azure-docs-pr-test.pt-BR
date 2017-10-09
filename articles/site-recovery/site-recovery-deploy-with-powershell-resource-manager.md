---
title: aaaReplicate VMs Hyper-V com o PowerShell e o Gerenciador de recursos do Azure | Microsoft Docs
description: "Automatize a replicação de saudação do tooAzure de VMs Hyper-V com o Azure Site Recovery usando o PowerShell e o Gerenciador de recursos do Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="68bd3-103">Replicar entre máquinas virtuais locais do Hyper-V e o Azure usando o PowerShell e o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68bd3-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68bd3-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="68bd3-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="68bd3-105">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68bd3-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="68bd3-106">Portal clássico</span><span class="sxs-lookup"><span data-stu-id="68bd3-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="68bd3-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="68bd3-107">Overview</span></span>
<span data-ttu-id="68bd3-108">O Azure Site Recovery contribui com a estratégia de recuperação tooyour business desastre e continuidade ao orquestrar a replicação, failover e recuperação de máquinas virtuais em vários cenários de implantação.</span><span class="sxs-lookup"><span data-stu-id="68bd3-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="68bd3-109">Para obter uma lista completa dos cenários de implantação, consulte Olá [visão geral do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68bd3-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="68bd3-110">PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68bd3-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="68bd3-111">Ele pode funcionar com dois tipos de módulos: Olá módulo de perfil do Azure ou módulo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="68bd3-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="68bd3-112">Os cmdlets do PowerShell da Recuperação de Site disponíveis com o Azure PowerShell para o Azure Resource Manager permitem que você proteja e recupere seus servidores no Azure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="68bd3-113">Este artigo descreve como toouse do Windows PowerShell, junto com o Gerenciador de recursos do Azure, toodeploy tooconfigure de recuperação de Site e orquestrar tooAzure de proteção do servidor.</span><span class="sxs-lookup"><span data-stu-id="68bd3-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="68bd3-114">exemplo Hello usado neste artigo mostra como tooprotect, failover e recupere máquinas virtuais em um tooAzure de host do Hyper-V, usando o PowerShell do Azure com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="68bd3-115">Olá cmdlets do PowerShell de recuperação de Site no momento permitem Olá tooconfigure a seguir: um tooanother de site do Virtual Machine Manager, um tooAzure de site do Virtual Machine Manager e um tooAzure de site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="68bd3-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="68bd3-116">Você não precisa toobe um toouse especialista do PowerShell deste artigo, mas é necessário toounderstand Olá os conceitos básicos, como sessões, cmdlets e módulos.</span><span class="sxs-lookup"><span data-stu-id="68bd3-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="68bd3-117">Para obter mais informações sobre o Windows PowerShell, consulte [Introdução ao PowerShell do Microsoft Azure (a página pode estar em inglês)](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="68bd3-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="68bd3-118">Leia mais sobre isso em [Usando o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="68bd3-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="68bd3-119">Parceiros da Microsoft que fazem parte do programa do provedor de solução de nuvem (CSP) Olá podem configurar e gerenciar a proteção de servidores de seus clientes tootheir respectivos CSP as assinaturas dos clientes (assinaturas de locatários).</span><span class="sxs-lookup"><span data-stu-id="68bd3-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="68bd3-120">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="68bd3-120">Before you start</span></span>
<span data-ttu-id="68bd3-121">Verifique se estes pré-requisitos estão em vigor:</span><span class="sxs-lookup"><span data-stu-id="68bd3-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="68bd3-122">Uma conta do [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="68bd3-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="68bd3-123">Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68bd3-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="68bd3-124">Além disso, você pode ler sobre [preços do Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="68bd3-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="68bd3-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="68bd3-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="68bd3-126">Para obter informações sobre esta versão e como tooinstall, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="68bd3-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="68bd3-127">Olá [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos.</span><span class="sxs-lookup"><span data-stu-id="68bd3-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="68bd3-128">Você pode obter versões mais recentes de saudação desses módulos de saudação [Galeria do PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="68bd3-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="68bd3-129">Este artigo ilustra como toouse Powershell do Azure com o Azure Resource Manager tooconfigure e gerenciar a proteção dos seus servidores.</span><span class="sxs-lookup"><span data-stu-id="68bd3-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="68bd3-130">exemplo Hello usado neste artigo mostra como tooprotect uma máquina virtual, em execução em um host Hyper-V, tooAzure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="68bd3-131">Olá pré-requisitos a seguir é exemplos de toothis específico.</span><span class="sxs-lookup"><span data-stu-id="68bd3-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="68bd3-132">Para um conjunto mais abrangente de requisitos para Olá vários cenários de recuperação de Site, consulte a documentação de toohello relativos toothat cenário.</span><span class="sxs-lookup"><span data-stu-id="68bd3-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="68bd3-133">Um host Hyper-V que executa o Windows Server 2012 R2 ou o Microsoft Hyper-V Server 2012 R2 contendo uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="68bd3-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="68bd3-134">Servidores Hyper-V conectado toohello Internet, diretamente ou através de um proxy.</span><span class="sxs-lookup"><span data-stu-id="68bd3-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="68bd3-135">Olá máquinas virtuais que você deseja tooprotect devem estar em conformidade com [pré-requisitos para a máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="68bd3-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="68bd3-136">Etapa 1: Inscrever-se em tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="68bd3-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="68bd3-137">Abrir um console do PowerShell e execute este comando toosign em tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="68bd3-138">Olá cmdlet abre uma página da web que solicitará as credenciais de conta.</span><span class="sxs-lookup"><span data-stu-id="68bd3-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="68bd3-139">Como alternativa, você também pode incluir as credenciais de conta como um parâmetro toohello `Login-AzureRmAccount` cmdlet, usando Olá `-Credential` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="68bd3-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="68bd3-140">Se você estiver trabalhando em nome de um locatário de parceiro CSP, especifique Prezado cliente como um locatário usando o nome de domínio primário tenantID ou locatário.</span><span class="sxs-lookup"><span data-stu-id="68bd3-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="68bd3-141">Uma conta pode ter várias assinaturas, para que você deve associar uma assinatura Olá deseja toouse com conta hello.</span><span class="sxs-lookup"><span data-stu-id="68bd3-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="68bd3-142">Verifique se sua assinatura está registrada toouse hello Azure provedores de serviços de recuperação e recuperação de Site, usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bd3-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="68bd3-143">Na saída de hello desses comandos, se hello **RegistrationState** está definido muito**registrado**, você poderá tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="68bd3-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="68bd3-144">Caso contrário, você deve registrar o provedor de saudação ausente na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="68bd3-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="68bd3-145">Olá tooregister provedor do Azure para recuperação de Site e serviços de recuperação, executar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bd3-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="68bd3-146">Verificar se os provedores de saudação registrado com êxito usando Olá comandos a seguir: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="68bd3-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="68bd3-147">Etapa 2: Configurar a saudação que Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="68bd3-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="68bd3-148">Crie um grupo de recursos do Gerenciador de recursos do Azure em que você criar cofre hello, ou use um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="68bd3-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="68bd3-149">Você pode criar um novo grupo de recursos usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="68bd3-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="68bd3-150">Quando a variável de saudação $ResourceGroupName contém nome Olá Olá do grupo de recursos você deseja toocreate e variável Olá $Geo contém hello Azure região na qual grupo de recursos de saudação do toocreate (por exemplo, "Sul do Brasil").</span><span class="sxs-lookup"><span data-stu-id="68bd3-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="68bd3-151">Você pode obter uma lista de grupos de recursos em sua assinatura usando Olá `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68bd3-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="68bd3-152">Crie um novo cofre dos Serviços de Recuperação do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="68bd3-153">Você pode recuperar uma lista de cofres existentes usando Olá `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68bd3-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="68bd3-154">Se você quiser tooperform operações nos cofres de recuperação de Site criados usando o portal clássico do hello ou módulo do PowerShell do Azure Service Management hello, você pode recuperar uma lista de tais cofres usando Olá `Get-AzureRmSiteRecoveryVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="68bd3-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="68bd3-155">É necessário criar um novo cofre dos Serviços de Recuperação para todas as novas operações.</span><span class="sxs-lookup"><span data-stu-id="68bd3-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="68bd3-156">cofres da recuperação de Site Olá que você criou anteriormente têm suporte, mas não tem recursos mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bd3-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="68bd3-157">Etapa 3: Definir Olá contexto de Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="68bd3-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="68bd3-158">Definir o contexto do cofre Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bd3-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="68bd3-159">Etapa 4: Criar um site do Hyper-V e gerar uma nova chave de registro do cofre para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bd3-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="68bd3-160">Crie um novo site do Hyper-V da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="68bd3-161">Esse cmdlet inicia um site do Site Recovery trabalho toocreate hello e retorna um objeto de trabalho de recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="68bd3-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="68bd3-162">Aguarde Olá toocomplete de trabalho e verificar que o trabalho Olá concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="68bd3-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="68bd3-163">Você pode recuperar o objeto de trabalho hello e, assim, verificar status atual de saudação do trabalho hello, usando o cmdlet Get-AzureRmSiteRecoveryJob de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bd3-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="68bd3-164">Gerar e baixar uma chave de registro para o site de hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="68bd3-165">Saudação de cópia baixado host toohello chave Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="68bd3-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="68bd3-166">Precisar Olá tooregister chave Olá Hyper-V host toohello site.</span><span class="sxs-lookup"><span data-stu-id="68bd3-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="68bd3-167">Etapa 5: Instalar o provedor do Azure Site Recovery hello e Azure Recovery Services Agent em seu host do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="68bd3-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="68bd3-168">Baixar o instalador Olá para a versão mais recente saudação do provedor de saudação do [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="68bd3-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="68bd3-169">Instalador de saudação de execução no host do Hyper-V e no final de saudação da instalação de saudação continuar toohello etapa de registro.</span><span class="sxs-lookup"><span data-stu-id="68bd3-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="68bd3-170">Quando solicitado, forneça Olá baixado a chave de registro de site e concluir o registro do site do Hyper-V host toohello da saudação.</span><span class="sxs-lookup"><span data-stu-id="68bd3-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="68bd3-171">Verifique se o que host Olá Hyper-V é registrado toohello site usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="68bd3-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="68bd3-172">Etapa 6: Criar uma política de replicação e associe-o contêiner de proteção Olá</span><span class="sxs-lookup"><span data-stu-id="68bd3-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="68bd3-173">Crie uma política de replicação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="68bd3-174">Saudação de seleção retornada tooensure de trabalho que a criação de política de replicação Olá terá êxito.</span><span class="sxs-lookup"><span data-stu-id="68bd3-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="68bd3-175">Olá conta de armazenamento especificada deve ser em Olá mesma região do Azure como seu Cofre de serviços de recuperação e deve ter a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="68bd3-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="68bd3-176">Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (clássico).</span><span class="sxs-lookup"><span data-stu-id="68bd3-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="68bd3-177">Se Olá especificado a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Gerenciador de recursos do Azure), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (Gerenciador de recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="68bd3-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="68bd3-178">Obter Olá proteção contêiner toohello site correspondente, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="68bd3-179">Inicie associação de saudação do recipiente de proteção de saudação com a política de replicação hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="68bd3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="68bd3-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="68bd3-181">Espere Olá associação trabalho toocomplete e certifique-se de que ela foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="68bd3-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="68bd3-182">Etapa 7: habilitar a proteção para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="68bd3-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="68bd3-183">Obter Olá proteção entidade correspondente toohello VM que você deseja tooprotect, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="68bd3-184">Inicie a proteção de máquina virtual de hello, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="68bd3-185">Olá conta de armazenamento especificada deve ser em Olá mesma região do Azure como seu Cofre de serviços de recuperação e deve ter a replicação geográfica habilitada.</span><span class="sxs-lookup"><span data-stu-id="68bd3-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="68bd3-186">Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (clássico).</span><span class="sxs-lookup"><span data-stu-id="68bd3-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="68bd3-187">Se Olá especificado a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Gerenciador de recursos do Azure), failover de saudação protegido máquinas recuperar Olá máquina tooAzure IaaS (Gerenciador de recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="68bd3-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="68bd3-188">Se Olá VM que você está protegendo tem mais de um disco anexado tooit, especifique o disco do sistema operacional hello usando Olá *OSDiskName* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="68bd3-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="68bd3-189">Aguarde Olá máquinas virtuais tooreach um estado protegido após a replicação inicial hello.</span><span class="sxs-lookup"><span data-stu-id="68bd3-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="68bd3-190">Isso pode demorar um pouco, dependendo de fatores como a quantidade de saudação de toobe dados replicado e Olá tooAzure upstream de largura de banda disponível.</span><span class="sxs-lookup"><span data-stu-id="68bd3-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="68bd3-191">Estado do trabalho Hello e StateDescription são atualizados da seguinte maneira após Olá VM atingir um estado protegido.</span><span class="sxs-lookup"><span data-stu-id="68bd3-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="68bd3-192">Atualize propriedades de recuperação, como Olá tamanho de função VM e failover de tooupon de placas de interface de rede Olá rede Azure tooattach Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68bd3-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="68bd3-193">Etapa 8: executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="68bd3-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="68bd3-194">Execute um trabalho de failover de teste, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="68bd3-195">Verifique se esse teste Olá que VM é criada no Azure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="68bd3-196">(trabalho de failover de teste hello está suspenso, depois de criar a VM de teste Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="68bd3-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="68bd3-197">Olá trabalho for concluído limpando artefatos Olá criado ao retomar o trabalho hello, conforme ilustrado na próxima etapa do hello.)</span><span class="sxs-lookup"><span data-stu-id="68bd3-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="68bd3-198">Olá completa testar o failover, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68bd3-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="68bd3-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68bd3-199">Next Steps</span></span>
<span data-ttu-id="68bd3-200">[Leia mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68bd3-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
