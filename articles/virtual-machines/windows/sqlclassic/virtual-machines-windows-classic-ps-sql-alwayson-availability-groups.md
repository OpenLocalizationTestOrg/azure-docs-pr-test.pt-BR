---
title: "aaaConfigure Olá sempre no grupo de disponibilidade em uma VM do Azure usando o PowerShell | Microsoft Docs"
description: "Este tutorial usa recursos que foram criados com o modelo de implantação clássico hello. Use o PowerShell toocreate um grupo de disponibilidade AlwaysOn no Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="8eefc-104">Configurar Olá sempre no grupo de disponibilidade em uma VM do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8eefc-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8eefc-105">Clássico: Interface de usuário</span><span class="sxs-lookup"><span data-stu-id="8eefc-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="8eefc-106">[Clássico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="8eefc-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="8eefc-107">Antes de começar, considere que agora você pode concluir esta tarefa no modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8eefc-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="8eefc-108">O modelo do Azure Resource Manager é recomendável para novas implantações.</span><span class="sxs-lookup"><span data-stu-id="8eefc-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="8eefc-109">Confira, [Introdução aos grupos de disponibilidade Always On do SQL Server em máquinas virtuais do Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8eefc-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8eefc-110">É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8eefc-111">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8eefc-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8eefc-112">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="8eefc-113">Máquinas virtuais (VMs) do Azure pode ajudar o custo de saudação de toolower de administradores de banco de dados de um sistema de alta disponibilidade do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="8eefc-114">Este tutorial mostra como tooimplement uma disponibilidade de grupo usando o SQL Server Always On ponta a ponta em um ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="8eefc-115">No final de saudação do tutorial hello, sua solução SQL Server Always On no Azure consistirá Olá elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="8eefc-116">Uma rede virtual que contém várias sub-redes, incluindo uma de front-end e uma de back-end.</span><span class="sxs-lookup"><span data-stu-id="8eefc-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="8eefc-117">Um controlador de domínio com um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8eefc-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="8eefc-118">Duas VMs do SQL Server que são implantados toohello sub-rede de back-end e toohello ingressado no domínio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8eefc-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="8eefc-119">Um cluster de failover do Windows três nós com o modelo de quorum de maioria de nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="8eefc-120">Um grupo de disponibilidade com duas réplicas de confirmação síncrona de um banco de dados de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8eefc-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="8eefc-121">Esse cenário é uma boa escolha por sua simplicidade no Azure, não pela economia ou outros fatores.</span><span class="sxs-lookup"><span data-stu-id="8eefc-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="8eefc-122">Por exemplo, você pode minimizar o número de saudação de VMs para um toosave do grupo de disponibilidade de duas réplicas horas de computação no Azure usando o controlador de domínio hello como testemunha de compartilhamento de arquivo hello quorum em um cluster de failover de dois nós.</span><span class="sxs-lookup"><span data-stu-id="8eefc-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="8eefc-123">Esse método reduz a contagem de VM de Olá por um de saudação acima de configuração.</span><span class="sxs-lookup"><span data-stu-id="8eefc-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="8eefc-124">Este tutorial é dirigido a tooshow Olá etapas que são necessária tooset backup Olá descrito solução acima sem elaborar os detalhes de saudação de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="8eefc-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="8eefc-125">Portanto, em vez de fornecer as etapas de configuração de saudação GUI, ele usa tootake de scripts do PowerShell você rapidamente a cada etapa.</span><span class="sxs-lookup"><span data-stu-id="8eefc-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="8eefc-126">Este tutorial pressupõe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="8eefc-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="8eefc-127">Você já tem uma conta do Azure com assinatura de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="8eefc-128">Você instalou Olá [cmdlets do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8eefc-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8eefc-129">Você já tem uma compreensão sólida dos grupos de disponibilidade Always On para soluções locais.</span><span class="sxs-lookup"><span data-stu-id="8eefc-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="8eefc-130">Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="8eefc-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="8eefc-131">Conecte-se tooyour assinatura do Azure e criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="8eefc-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="8eefc-132">Em uma janela do PowerShell no computador local, importar Olá módulo do Azure, baixe Olá máquina de tooyour do arquivo de configurações de publicação e conectar-se a sua sessão de PowerShell tooyour assinatura do Azure importando as configurações de publicação Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="8eefc-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="8eefc-133">Olá **AzurePublishSettingsFile Get** comando baixa tooyour máquina e gera um certificado de gerenciamento com o Azure automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8eefc-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="8eefc-134">Um navegador é aberto automaticamente e você está tooenter solicitadas Olá credenciais de conta da Microsoft para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="8eefc-135">Olá baixado **. publishsettings** arquivo contém todas as informações de saudação necessário toomanage sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="8eefc-136">Depois de salvar este diretório local do arquivo tooa, importá-lo usando Olá **AzurePublishSettingsFile importação** comando.</span><span class="sxs-lookup"><span data-stu-id="8eefc-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8eefc-137">arquivo. publishsettings de saudação contém suas credenciais (sem codificação) que são usado tooadminister suas assinaturas do Azure e serviços.</span><span class="sxs-lookup"><span data-stu-id="8eefc-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="8eefc-138">prática recomendada de segurança Olá para esse arquivo é toostore-lo temporariamente fora dos diretórios de origem (por exemplo, na pasta de bibliotecas\documentos Olá) e, em seguida, excluí-lo após a importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="8eefc-139">Um usuário mal-intencionado que obtém o arquivo. publishsettings do access toohello pode editar, criar e excluir seus serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="8eefc-140">Defina uma série de variáveis que você usará toocreate sua nuvem de infraestrutura de TI.</span><span class="sxs-lookup"><span data-stu-id="8eefc-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="8eefc-141">Preste atenção toohello tooensure que os comandos tenham êxito posterior a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="8eefc-142">Variáveis **$storageAccountName** e **$dcServiceName** devem ser exclusivas porque são usados tooidentify de sua conta de armazenamento de nuvem e o servidor de nuvem, respectivamente, no hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="8eefc-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="8eefc-143">Olá nomes que você especificar para variáveis **$affinityGroupName** e **$virtualNetworkName** são configurados no documento de configuração de rede virtual Olá que você usará mais tarde.</span><span class="sxs-lookup"><span data-stu-id="8eefc-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="8eefc-144">**$sqlImageName** especifica nome hello atualizado da imagem VM Olá que contém o SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="8eefc-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="8eefc-145">Para simplificar, **Contoso! 000** é Olá a mesma senha que é usada em todo o tutorial todo hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="8eefc-146">Crie um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="8eefc-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="8eefc-147">Crie uma rede virtual importando um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="8eefc-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="8eefc-148">arquivo de configuração de saudação contém Olá documento XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="8eefc-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="8eefc-149">Em suma, ele especifica uma rede virtual chamada **ContosoNET** no grupo de afinidade Olá chamado **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="8eefc-150">Tem espaço de endereço Olá **10.10.0.0/16** e duas sub-redes, **10.10.1.0/24** e **10.10.2.0/24**, que são sub-rede front hello e posterior, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8eefc-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="8eefc-151">a sub-rede front Olá é onde você pode colocar aplicativos cliente, como o Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8eefc-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="8eefc-152">subrede back Olá é onde você colocará Olá VMs do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="8eefc-153">Se você alterar Olá **$affinityGroupName** e **$virtualNetworkName** variáveis anteriores, você deve também alterar Olá correspondente nomes abaixo.</span><span class="sxs-lookup"><span data-stu-id="8eefc-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="8eefc-154">Crie uma conta de armazenamento que está associado a grupo de afinidade Olá que você criou e defina-a como conta de armazenamento atual da saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8eefc-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="8eefc-155">Crie servidor do controlador de domínio Olá no hello nova nuvem serviço e conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8eefc-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="8eefc-156">Esses comandos conectados Olá coisas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="8eefc-157">**New-AzureVMConfig** cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="8eefc-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="8eefc-158">**Adicionar-AzureProvisioningConfig** fornece Olá parâmetros de configuração de um servidor autônomo do Windows.</span><span class="sxs-lookup"><span data-stu-id="8eefc-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="8eefc-159">**Adicionar-AzureDataDisk** adiciona Olá disco de dados que você usará para armazenar dados do Active Directory, com hello tooNone de conjunto de opção de cache.</span><span class="sxs-lookup"><span data-stu-id="8eefc-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="8eefc-160">**New-AzureVM** cria um novo serviço de nuvem e cria Olá nova VM do Azure no novo serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="8eefc-161">Espere Olá nova VM toobe totalmente provisionada e baixe a pasta de trabalho de tooyour Olá arquivo de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="8eefc-162">Como hello nova VM do Azure usa um tooprovision muito tempo, Olá `while` loop continua toopoll Olá nova VM até que ele está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="8eefc-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="8eefc-163">servidor do controlador de domínio Olá agora está provisionado com êxito.</span><span class="sxs-lookup"><span data-stu-id="8eefc-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="8eefc-164">Em seguida, você configurará o domínio do Active Directory Olá neste servidor de controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="8eefc-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="8eefc-165">Janela do PowerShell Olá deixe aberta no computador local.</span><span class="sxs-lookup"><span data-stu-id="8eefc-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="8eefc-166">Você vai usá-lo novamente toocreate posterior Olá duas VMs do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="8eefc-167">Configurar o controlador de domínio Olá</span><span class="sxs-lookup"><span data-stu-id="8eefc-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="8eefc-168">Conecte-se servidor do controlador de domínio toohello iniciando Olá arquivo da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="8eefc-169">Usar AzureAdmin de nome de usuário e a senha do administrador do computador Olá **Contoso! 000**, que você especificou quando criou Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="8eefc-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="8eefc-170">Abra uma janela do PowerShell no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="8eefc-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="8eefc-171">Execute seguinte Olá **DCPROMO. EXE** tooset do comando backup Olá **corp.contoso.com** domínio, com diretórios de dados de saudação na unidade M.</span><span class="sxs-lookup"><span data-stu-id="8eefc-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="8eefc-172">Após a conclusão do comando hello, Olá VM será reiniciada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8eefc-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="8eefc-173">Conecte novamente o servidor do controlador de domínio toohello iniciando Olá arquivo de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="8eefc-174">Desta vez, faça logon como **CORP\Administrador**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="8eefc-175">Abra uma janela do PowerShell no modo de administrador e importar o módulo do Active Directory PowerShell hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="8eefc-176">Execute Olá comandos tooadd três usuários toohello o domínio a seguir.</span><span class="sxs-lookup"><span data-stu-id="8eefc-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="8eefc-177">**CORP\Install** é usado tooconfigure tudo relacionado toohello instâncias de serviço do SQL Server, o cluster de failover hello e o grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="8eefc-178">**CORP\SQLSvc1** e **CORP\SQLSvc2** são usados como contas de serviço do SQL Server Olá Olá duas VMs do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="8eefc-179">A seguir Olá Avançar, execute comandos toogive **CORP\Install** Olá objetos de computador toocreate permissões no domínio hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="8eefc-180">Olá GUID especificado acima é hello GUID para o tipo de objeto de computador hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="8eefc-181">Olá **CORP\Install** conta precisa Olá **ler todas as propriedades** e **criar objetos de computador** Olá de toocreate permissão Active Direct objetos para o failover de saudação cluster.</span><span class="sxs-lookup"><span data-stu-id="8eefc-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="8eefc-182">Olá **ler todas as propriedades** permissão já foi atribuída tooCORP\Install por padrão, portanto, você não precisa toogrant-lo explicitamente.</span><span class="sxs-lookup"><span data-stu-id="8eefc-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="8eefc-183">Para obter mais informações sobre as permissões que são necessárias cluster de failover do toocreate hello, consulte [guia do passo a passo de Cluster de Failover: Configurando contas no Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="8eefc-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="8eefc-184">Agora que você terminou a configuração do Active Directory e objetos de saudação do usuário, você criará duas VMs do SQL Server e associá-las toothis domínio.</span><span class="sxs-lookup"><span data-stu-id="8eefc-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="8eefc-185">Criar hello VMs do SQL Server</span><span class="sxs-lookup"><span data-stu-id="8eefc-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="8eefc-186">Continue toouse Olá PowerShell janela aberta no computador local.</span><span class="sxs-lookup"><span data-stu-id="8eefc-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="8eefc-187">Defina Olá variáveis adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="8eefc-188">Olá endereço IP **10.10.0.4** normalmente é atribuído toohello primeira máquina virtual que você cria no hello **10.10.0.0/16** sub-rede da rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="8eefc-189">Você deve verificar se este é o endereço de saudação do seu servidor do controlador de domínio executando **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="8eefc-190">Execução Olá Olá de toocreate comandos conectados a seguir primeiro VM no cluster de failover hello, denominado **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="8eefc-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="8eefc-191">Observe o seguinte de saudação sobre Olá comando acima:</span><span class="sxs-lookup"><span data-stu-id="8eefc-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="8eefc-192">**New-AzureVMConfig** cria uma configuração de VM com o nome do conjunto de disponibilidade desejado hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="8eefc-193">Olá VMs subsequentes serão criadas com hello mesmo nome do conjunto de disponibilidade para que elas são unidas toohello mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8eefc-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="8eefc-194">**Adicionar-AzureProvisioningConfig** junções Olá domínio do Active Directory do VM toohello que você criou.</span><span class="sxs-lookup"><span data-stu-id="8eefc-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="8eefc-195">**Conjunto AzureSubnet** casas Olá VM na sub-rede back hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="8eefc-196">**New-AzureVM** cria um novo serviço de nuvem e cria Olá nova VM do Azure no novo serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="8eefc-197">Olá **DnsSettings** parâmetro especifica o servidor DNS Olá para servidores no novo serviço de nuvem Olá Olá tem endereço IP hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="8eefc-198">Esse é o endereço IP de saudação do servidor de saudação do controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="8eefc-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="8eefc-199">Esse parâmetro é necessário tooenable Olá novas VMs no domínio do Active Directory do hello nuvem serviço toojoin toohello com êxito.</span><span class="sxs-lookup"><span data-stu-id="8eefc-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="8eefc-200">Sem esse parâmetro, você deve manualmente definir configurações de IPv4 Olá em seu servidor de controlador de domínio do VM toouse hello como servidor DNS primário Olá após Olá VM é provisionada e, em seguida, ingressar em domínio do Active Directory do hello VM toohello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="8eefc-201">Saudação de execução a seguir canalizado comandos toocreate Olá VMs do SQL Server, chamado **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="8eefc-202">Observe o seguinte de saudação sobre Olá comandos acima:</span><span class="sxs-lookup"><span data-stu-id="8eefc-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="8eefc-203">**New-AzureVMConfig** usa Olá mesmo nome do conjunto de disponibilidade como servidor de controlador de domínio hello e usa Olá imagem do SQL Server 2012 Service Pack 1 Enterprise Edition na Galeria de máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="8eefc-204">Ele também define Olá operacional sistema tooread do cache de disco somente (sem cache de gravação).</span><span class="sxs-lookup"><span data-stu-id="8eefc-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="8eefc-205">É recomendável que você migre Olá banco de dados arquivos tooa disco de dados separado anexar toohello VM e configurá-lo com nenhuma leitura ou gravação em cache.</span><span class="sxs-lookup"><span data-stu-id="8eefc-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="8eefc-206">No entanto, Olá próxima melhor é tooremove cache de gravação no disco do sistema operacional Olá porque você não pode remover cache de leitura no disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="8eefc-207">**Adicionar-AzureProvisioningConfig** junções Olá domínio do Active Directory do VM toohello que você criou.</span><span class="sxs-lookup"><span data-stu-id="8eefc-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="8eefc-208">**Conjunto AzureSubnet** casas Olá VM na sub-rede back hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="8eefc-209">**Adicionar-AzureEndpoint** adiciona pontos de extremidade de acesso para que os aplicativos cliente possam acessar essas instâncias de serviços do SQL Server no hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="8eefc-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="8eefc-210">Portas diferentes são atribuídas tooContosoSQL1 e ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="8eefc-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="8eefc-211">**New-AzureVM** cria Olá nova VM do SQL Server no hello mesmo serviço de nuvem como ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="8eefc-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="8eefc-212">Você deve colocar Olá VMs no hello mesmo serviço de nuvem se você deseja que eles toobe em Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8eefc-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="8eefc-213">Aguarde para cada toobe VM totalmente provisionado e toodownload cada VM seu diretório de trabalho de tooyour de arquivo de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="8eefc-214">Olá `for` loop for percorre Olá três novas VMs e executa comandos de saudação dentro Olá chaves de nível superior para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="8eefc-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="8eefc-215">Olá VMs do SQL Server agora estão provisionadas e em execução, mas ele estão instalado com o SQL Server com as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="8eefc-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="8eefc-216">Inicializar máquinas virtuais do cluster de failover Olá</span><span class="sxs-lookup"><span data-stu-id="8eefc-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="8eefc-217">Nesta seção, você precisa toomodify Olá três servidores que você usará no cluster de failover do hello e instalação do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="8eefc-218">Especificamente:</span><span class="sxs-lookup"><span data-stu-id="8eefc-218">Specifically:</span></span>

* <span data-ttu-id="8eefc-219">Todos os servidores: você precisa Olá tooinstall **Clustering de Failover** recurso.</span><span class="sxs-lookup"><span data-stu-id="8eefc-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="8eefc-220">Todos os servidores: É necessário tooadd **CORP\Install** como máquina Olá **administrador**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="8eefc-221">ContosoSQL1 e ContosoSQL2 somente: É necessário tooadd **CORP\Install** como um **sysadmin** função no banco de dados de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="8eefc-222">ContosoSQL1 e ContosoSQL2 somente: É necessário tooadd **NT AUTHORITY\System** como uma entrada com hello as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="8eefc-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="8eefc-223">Alterar qualquer grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="8eefc-223">Alter any availability group</span></span>
  * <span data-ttu-id="8eefc-224">Conectar o SQL</span><span class="sxs-lookup"><span data-stu-id="8eefc-224">Connect SQL</span></span>
  * <span data-ttu-id="8eefc-225">Exibir o estado do servidor</span><span class="sxs-lookup"><span data-stu-id="8eefc-225">View server state</span></span>
* <span data-ttu-id="8eefc-226">ContosoSQL1 e ContosoSQL2 somente: Olá **TCP** protocolo já está habilitado em Olá VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="8eefc-227">No entanto, você ainda precisa firewall de saudação tooopen para acesso remoto do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="8eefc-228">Agora, você está pronto toostart.</span><span class="sxs-lookup"><span data-stu-id="8eefc-228">Now, you're ready toostart.</span></span> <span data-ttu-id="8eefc-229">Começando com **ContosoQuorum**, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="8eefc-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="8eefc-230">Conecte-se muito**ContosoQuorum** iniciando Olá arquivos de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="8eefc-231">Usar nome de usuário do administrador do computador Olá **AzureAdmin** e a senha **Contoso! 000**, que você especificou quando criou Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="8eefc-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="8eefc-232">Verifique se que os computadores Olá tem Unidos com êxito muito**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="8eefc-233">Aguarde toofinish de instalação do SQL Server Olá Olá automatizada tarefas de inicialização antes de continuar em execução.</span><span class="sxs-lookup"><span data-stu-id="8eefc-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="8eefc-234">Abra uma janela do PowerShell no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="8eefc-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="8eefc-235">Instale o recurso de cluster de Failover do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="8eefc-236">Adicione **CORP\Install** como um administrador local.</span><span class="sxs-lookup"><span data-stu-id="8eefc-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="8eefc-237">Saia de ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="8eefc-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="8eefc-238">A tarefa nesse servidor foi concluída.</span><span class="sxs-lookup"><span data-stu-id="8eefc-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="8eefc-239">Em seguida, inicialize **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="8eefc-240">Siga as etapas de saudação abaixo, que são idênticas para ambas as VMs do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="8eefc-241">Conecte toohello duas VMs do SQL Server, iniciando Olá arquivos da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="8eefc-242">Usar nome de usuário do administrador do computador Olá **AzureAdmin** e a senha **Contoso! 000**, que você especificou quando criou Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="8eefc-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="8eefc-243">Verifique se que os computadores Olá tem Unidos com êxito muito**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="8eefc-244">Aguarde toofinish de instalação do SQL Server Olá Olá automatizada tarefas de inicialização antes de continuar em execução.</span><span class="sxs-lookup"><span data-stu-id="8eefc-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="8eefc-245">Abra uma janela do PowerShell no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="8eefc-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="8eefc-246">Instale o recurso de cluster de Failover do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="8eefc-247">Adicione **CORP\Install** como um administrador local.</span><span class="sxs-lookup"><span data-stu-id="8eefc-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="8eefc-248">Importe Olá provedor SQL Server PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eefc-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="8eefc-249">Adicionar **CORP\Install** como uma função de sysadmin Olá Olá padrão instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="8eefc-250">Adicionar **NT AUTHORITY\System** como uma entrada com permissões de saudação três descrito acima.</span><span class="sxs-lookup"><span data-stu-id="8eefc-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="8eefc-251">Abra o firewall Olá para acesso remoto do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8eefc-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="8eefc-252">Saia de ambas as VMs.</span><span class="sxs-lookup"><span data-stu-id="8eefc-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="8eefc-253">Por fim, você está pronto tooconfigure grupo de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="8eefc-254">Você usará tooperform do provedor do SQL Server PowerShell Olá todos Olá funcionam em **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="8eefc-255">Configurar o grupo de disponibilidade Olá</span><span class="sxs-lookup"><span data-stu-id="8eefc-255">Configure hello availability group</span></span>
1. <span data-ttu-id="8eefc-256">Conecte-se muito**ContosoSQL1** novamente por iniciando Olá arquivos da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8eefc-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="8eefc-257">Em vez de entrar usando a conta da máquina hello, entrar usando **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="8eefc-258">Abra uma janela do PowerShell no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="8eefc-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="8eefc-259">Defina Olá variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="8eefc-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="8eefc-260">Importe Olá provedor SQL Server PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eefc-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="8eefc-261">Alterar a conta de serviço do SQL Server Olá para ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="8eefc-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="8eefc-262">Alterar a conta de serviço do SQL Server Olá para ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="8eefc-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="8eefc-263">Baixar **CreateAzureFailoverCluster.ps1** de [criar o Cluster de Failover para grupos de disponibilidade AlwaysOn em VM do Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello diretório de trabalho local.</span><span class="sxs-lookup"><span data-stu-id="8eefc-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="8eefc-264">Você usará essa toohelp de script que você criar um cluster de failover funcional.</span><span class="sxs-lookup"><span data-stu-id="8eefc-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="8eefc-265">Para obter informações importantes sobre como o Clustering de Failover do Windows interage com hello Azure de rede, consulte [alta disponibilidade e recuperação de desastres para o SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8eefc-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="8eefc-266">Alterar o diretório de trabalho tooyour e criar o cluster de failover de saudação com script hello baixado.</span><span class="sxs-lookup"><span data-stu-id="8eefc-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="8eefc-267">Habilitar grupos de disponibilidade AlwaysOn para instâncias de SQL Server saudação padrão em **ContosoSQL1** e **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="8eefc-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="8eefc-268">Crie um diretório de backup e conceda permissões para contas de serviço do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="8eefc-269">Você usará esse banco de dados do diretório tooprepare Olá disponibilidade na réplica secundária hello.</span><span class="sxs-lookup"><span data-stu-id="8eefc-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="8eefc-270">Criar um banco de dados em **ContosoSQL1** chamado **MyDB1**, faça um backup completo e um backup de log e restaure-os em **ContosoSQL2** com hello **WITH NORECOVERY** opção.</span><span class="sxs-lookup"><span data-stu-id="8eefc-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="8eefc-271">Criar pontos de extremidade de grupo de disponibilidade Olá em Olá VMs do SQL Server e defina as permissões adequadas Olá nos pontos de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="8eefc-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="8eefc-272">Crie hello réplicas de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8eefc-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="8eefc-273">Finalmente, crie o grupo de disponibilidade hello e o grupo de disponibilidade de toohello do junção Olá réplica secundária.</span><span class="sxs-lookup"><span data-stu-id="8eefc-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="8eefc-274">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8eefc-274">Next steps</span></span>
<span data-ttu-id="8eefc-275">Agora você implementou com êxito o SQL Server Always On criando um grupo de disponibilidade no Azure.</span><span class="sxs-lookup"><span data-stu-id="8eefc-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="8eefc-276">tooconfigure um ouvinte para esse grupo de disponibilidade, consulte [configurar um ouvinte de ILB para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="8eefc-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="8eefc-277">Para obter outras informações sobre como usar o SQL Server no Azure, veja [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8eefc-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
