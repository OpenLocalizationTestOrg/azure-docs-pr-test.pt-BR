---
title: aaaCreate uma VM do Windows com o PowerShell | Microsoft Docs
description: "Crie máquinas virtuais do Windows PowerShell do Azure e o modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="c9b27-103">Criar uma máquina virtual do Windows com o modelo de implantação clássico hello e PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9b27-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9b27-104">Portal do Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="c9b27-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="c9b27-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="c9b27-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="c9b27-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c9b27-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c9b27-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c9b27-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b27-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="c9b27-109">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9b27-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c9b27-110">Estas etapas mostram como os comandos toocustomize um conjunto de PowerShell do Azure que criar e pré-configurar a uma máquina virtual baseados no Windows Azure usando uma abordagem de bloco de construção.</span><span class="sxs-lookup"><span data-stu-id="c9b27-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="c9b27-111">Você pode usar esse processo tooquickly criar um conjunto de comandos para uma nova máquina virtual com base em Windows e expanda uma implantação existente ou toocreate comando vários conjuntos que rapidamente criar um personalizado de desenvolvimento/teste ou ambiente de profissional de TI.</span><span class="sxs-lookup"><span data-stu-id="c9b27-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="c9b27-112">Estas etapas seguem uma abordagem de preencher lacunas para criar conjuntos de comandos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9b27-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="c9b27-113">Essa abordagem pode ser útil se você for novo tooPowerShell ou você quiser apenas tooknow toospecify quais valores de configuração com êxito.</span><span class="sxs-lookup"><span data-stu-id="c9b27-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="c9b27-114">Usuários avançados do PowerShell podem executar comandos hello e substitua seus próprios valores para variáveis de saudação (linhas de saudação que começam com "$").</span><span class="sxs-lookup"><span data-stu-id="c9b27-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="c9b27-115">Se você ainda não tiver feito isso, use as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell no computador local.</span><span class="sxs-lookup"><span data-stu-id="c9b27-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="c9b27-116">Em seguida, abra um prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9b27-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="c9b27-117">Etapa 1: adicionar sua conta</span><span class="sxs-lookup"><span data-stu-id="c9b27-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="c9b27-118">No prompt do PowerShell hello, digite **Add-AzureAccount** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c9b27-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="c9b27-119">Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="c9b27-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="c9b27-120">Digite a senha Olá para sua conta.</span><span class="sxs-lookup"><span data-stu-id="c9b27-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="c9b27-121">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="c9b27-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="c9b27-122">Etapa 2: Definir a assinatura e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c9b27-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="c9b27-123">Defina a assinatura do Azure e a conta de armazenamento executando esses comandos no prompt de comando do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="c9b27-124">Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com nomes de saudação correto.</span><span class="sxs-lookup"><span data-stu-id="c9b27-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="c9b27-125">Você pode obter o nome de assinatura correta de saudação do hello propriedade de nome de inscrição da saída de saudação do hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="c9b27-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="c9b27-126">Você pode obter o nome de conta de armazenamento correta de saudação do Olá propriedade do rótulo de saída Olá Olá **Get-AzureStorageAccount** comando depois de executar Olá **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="c9b27-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="c9b27-127">Etapa 3: Determinar Olá ImageFamily</span><span class="sxs-lookup"><span data-stu-id="c9b27-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="c9b27-128">Em seguida, você precisa toodetermine Olá ImageFamily ou valor de rótulo para toohello correspondente de imagem específica de saudação máquina virtual do Azure que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="c9b27-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="c9b27-129">Você pode obter a lista de saudação de valores ImageFamily disponíveis com este comando.</span><span class="sxs-lookup"><span data-stu-id="c9b27-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="c9b27-130">Aqui estão alguns exemplos de valores de ImageFamily para computadores baseados em Windows:</span><span class="sxs-lookup"><span data-stu-id="c9b27-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="c9b27-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="c9b27-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="c9b27-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="c9b27-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="c9b27-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="c9b27-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="c9b27-134">SQL Server 2012 SP1 Enterprise em Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c9b27-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="c9b27-135">Se você encontrar a imagem de saudação que você está procurando, abra uma nova instância do editor de texto de saudação de sua escolha ou Olá ambiente de script integrado do PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="c9b27-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="c9b27-136">Copie o seguinte de Olá no novo arquivo de texto de saudação ou hello PowerShell ISE, substituindo o valor de ImageFamily hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="c9b27-137">Em alguns casos, o nome de imagem do hello está sendo Olá em vez da saudação ImageFamily valor da propriedade do rótulo.</span><span class="sxs-lookup"><span data-stu-id="c9b27-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="c9b27-138">Se você não encontrou a imagem de saudação que você está procurando usando a propriedade ImageFamily hello, liste imagens Olá por sua propriedade de rótulo com este comando.</span><span class="sxs-lookup"><span data-stu-id="c9b27-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="c9b27-139">Se você encontrar a imagem à direita Olá com este comando, abra uma instância atualizada do editor de texto de saudação de sua escolha ou Olá PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c9b27-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="c9b27-140">Copie o seguinte de Olá no novo arquivo de texto de saudação ou hello PowerShell ISE, substituindo o valor de rótulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b27-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="c9b27-141">Etapa 4: criar o conjunto de comandos</span><span class="sxs-lookup"><span data-stu-id="c9b27-141">Step 4: Build your command set</span></span>
<span data-ttu-id="c9b27-142">Crie restante de saudação do comando definido, copiando o conjunto apropriado de saudação de blocos abaixo para seu novo arquivo de texto ou hello ISE e, em seguida, preencher os valores de variáveis de saudação e removendo hello < e > caracteres.</span><span class="sxs-lookup"><span data-stu-id="c9b27-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="c9b27-143">Consulte Olá dois [exemplos](#examples) final Olá deste artigo para uma ideia do resultado final da saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b27-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="c9b27-144">Comece seu conjunto de comandos escolhendo um destes dois blocos de comandos (obrigatório).</span><span class="sxs-lookup"><span data-stu-id="c9b27-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="c9b27-145">Opção 1: especifique um nome e um tamanho de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9b27-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="c9b27-146">Opção 2: especifique um nome, o tamanho e o nome do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c9b27-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="c9b27-147">Para obter valores de InstanceSize Olá para D, DS ou máquinas virtuais de série G, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9b27-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c9b27-148">Se você tiver um contrato empresarial com Software Assurance e pretende tootake vantagem de saudação do Windows Server [híbrida benefício de usar](https://azure.microsoft.com/pricing/hybrid-use-benefit/), adicionar o **- LicenseType** toohello parâmetro  **New-AzureVMConfig** cmdlet, passando o valor de saudação **Windows_Server** para Olá típico caso de uso.</span><span class="sxs-lookup"><span data-stu-id="c9b27-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="c9b27-149">Certifique-se de que você estiver usando uma imagem que você carregou; Você não pode usar uma imagem padrão do hello galeria com hello híbrida benefício de usar.</span><span class="sxs-lookup"><span data-stu-id="c9b27-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="c9b27-150">Opcionalmente, para um computador com Windows autônomo, especifique Olá conta de administrador local e senha.</span><span class="sxs-lookup"><span data-stu-id="c9b27-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="c9b27-151">Escolha uma senha forte.</span><span class="sxs-lookup"><span data-stu-id="c9b27-151">Choose a strong password.</span></span> <span data-ttu-id="c9b27-152">toocheck sua intensidade, consulte [Verificador de senha: usando senhas de alta segurança](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9b27-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="c9b27-153">Olá tooadd computador tooan existente do Active Directory domínio do Windows, especificar opcionalmente conta de administrador local hello e senha, domínio Olá e Olá nome e senha de uma conta de domínio.</span><span class="sxs-lookup"><span data-stu-id="c9b27-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="c9b27-154">Para opções adicionais de configuração prévia para máquinas virtuais baseadas em Windows, consulte sintaxe Olá Olá **Windows** e **WindowsDomain** define parâmetro [ Adicionar-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="c9b27-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="c9b27-155">Opcionalmente, atribua um endereço IP específico, conhecido como um DIP estático máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="c9b27-156">Você pode verificar se um endereço IP específico está disponível com:</span><span class="sxs-lookup"><span data-stu-id="c9b27-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="c9b27-157">Opcionalmente, atribua uma sub-rede específica do hello máquina virtual tooa em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="c9b27-158">Opcionalmente, adicione uma máquina virtual de toohello de disco de dados único.</span><span class="sxs-lookup"><span data-stu-id="c9b27-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="c9b27-159">Para um controlador de domínio do Active Directory, defina $hcaching muito "None".</span><span class="sxs-lookup"><span data-stu-id="c9b27-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="c9b27-160">Opcionalmente, adicione Olá conjunto máquinas virtuais tooan existente com balanceamento de carga para tráfego externo.</span><span class="sxs-lookup"><span data-stu-id="c9b27-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="c9b27-161">Por fim, escolha um desses blocos de comando necessário para a criação de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b27-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="c9b27-162">Opção 1: Crie a máquina virtual de saudação em um serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="c9b27-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="c9b27-163">nome curto de Olá Olá do serviço de nuvem é o nome de Olá que aparece na lista de saudação dos serviços de nuvem no portal do Azure de saudação ou na lista de saudação de grupos de recursos no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="c9b27-164">Opção 2: Crie máquina virtual de saudação em um serviço de nuvem existente e a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c9b27-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="c9b27-165">Etapa 5: executar o conjunto de comandos</span><span class="sxs-lookup"><span data-stu-id="c9b27-165">Step 5: Run your command set</span></span>
<span data-ttu-id="c9b27-166">Examine o conjunto de comandos do PowerShell do Azure Olá criados em seu editor de texto ou Olá ISE do PowerShell consiste em vários blocos de comandos da etapa 4.</span><span class="sxs-lookup"><span data-stu-id="c9b27-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="c9b27-167">Certifique-se de que você especificou todas as variáveis de saudação necessário e que tenham valores corretos hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="c9b27-168">Além disso, certifique-se de que você removeu todos os caracteres hello < e >.</span><span class="sxs-lookup"><span data-stu-id="c9b27-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="c9b27-169">Se você estiver usando um editor de texto, cópia Olá comando definir toohello área de transferência e clique, em seguida, abra o prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9b27-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="c9b27-170">Isso emitirá o conjunto de comandos hello como uma série de comandos do PowerShell e criar sua máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="c9b27-171">Como alternativa, execute o comando de saudação definido no hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c9b27-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="c9b27-172">Se pretender criar novamente essa máquina virtual ou uma semelhante, você poderá:</span><span class="sxs-lookup"><span data-stu-id="c9b27-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="c9b27-173">Salvar este conjunto de comandos como um arquivo de script do PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="c9b27-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="c9b27-174">Salvar este comando definido como um runbook de automação do Azure no hello **contas de automação** seção Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="c9b27-175"><a id="examples"></a>Exemplos</span><span class="sxs-lookup"><span data-stu-id="c9b27-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="c9b27-176">Aqui estão dois exemplos de uso etapas Olá acima toobuild conjuntos de comandos de PowerShell do Azure que cria máquinas de virtuais baseadas em Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="c9b27-177">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="c9b27-177">Example 1</span></span>
<span data-ttu-id="c9b27-178">Preciso de um PowerShell comando set toocreate saudação inicial máquina de virtual para um controlador de domínio do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c9b27-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="c9b27-179">Usa a imagem do Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="c9b27-180">Tem o nome de saudação AZDC1.</span><span class="sxs-lookup"><span data-stu-id="c9b27-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="c9b27-181">É um computador autônomo.</span><span class="sxs-lookup"><span data-stu-id="c9b27-181">Is a standalone computer.</span></span>
* <span data-ttu-id="c9b27-182">Tem um disco de dados adicional de 20 GB.</span><span class="sxs-lookup"><span data-stu-id="c9b27-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="c9b27-183">Tem o endereço IP estático Olá 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="c9b27-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="c9b27-184">Está na sub-rede de back-end de saudação da rede virtual do hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="c9b27-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="c9b27-185">É no serviço de nuvem Olá TailspinToys do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="c9b27-186">Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual, com linhas em branco entre cada bloco para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="c9b27-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="c9b27-187">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="c9b27-187">Example 2</span></span>
<span data-ttu-id="c9b27-188">Preciso de um PowerShell comando set toocreate uma máquina virtual para um servidor de linha de negócios que:</span><span class="sxs-lookup"><span data-stu-id="c9b27-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="c9b27-189">Usa a imagem do Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="c9b27-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="c9b27-190">Tem o nome de saudação LOB1.</span><span class="sxs-lookup"><span data-stu-id="c9b27-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="c9b27-191">É um membro do domínio corp.contoso.com de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9b27-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="c9b27-192">Tem um disco de dados adicional de 200 GB.</span><span class="sxs-lookup"><span data-stu-id="c9b27-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="c9b27-193">Está na sub-rede de front-end de saudação da rede virtual do hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="c9b27-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="c9b27-194">É no serviço de nuvem Olá TailspinToys do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9b27-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="c9b27-195">Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9b27-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="c9b27-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9b27-196">Next steps</span></span>
<span data-ttu-id="c9b27-197">Se você precisar de um disco do sistema operacional que é maior do que 127 GB, você pode [Expandir unidade Olá SO](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9b27-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

