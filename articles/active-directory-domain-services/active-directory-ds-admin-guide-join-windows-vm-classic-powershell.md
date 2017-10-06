---
title: "Azure Active Directory Domain Services: guia de administração | Microsoft Docs"
description: "Ingresse em um máquina virtual tooa gerenciado domínio do Windows PowerShell do Azure e o modelo de implantação clássico hello."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="8ef36-103">Ingressar em um domínio do Windows Server máquina virtual tooa gerenciado usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ef36-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ef36-104">Portal clássico do Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="8ef36-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="8ef36-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="8ef36-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="8ef36-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8ef36-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ef36-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8ef36-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="8ef36-108">Serviços de domínio do AD do Azure atualmente não dá suporte para modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ef36-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="8ef36-109">Estas etapas mostram como os comandos toocustomize um conjunto de PowerShell do Azure que criar e pré-configurar a uma máquina virtual baseados no Windows Azure usando uma abordagem de bloco de construção.</span><span class="sxs-lookup"><span data-stu-id="8ef36-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="8ef36-110">Essas etapas ajudam a criar uma máquina virtual baseados no Windows Azure e associá-la tooan domínio gerenciado por serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef36-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="8ef36-111">Estas etapas seguem uma abordagem de preencher lacunas para criar conjuntos de comandos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ef36-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="8ef36-112">Essa abordagem pode ser útil se você for novo tooPowerShell ou deseja tooknow toospecify quais valores de configuração com êxito.</span><span class="sxs-lookup"><span data-stu-id="8ef36-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="8ef36-113">Usuários avançados do PowerShell podem executar comandos hello e substitua seus próprios valores para variáveis de saudação (linhas de saudação que começam com "$").</span><span class="sxs-lookup"><span data-stu-id="8ef36-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="8ef36-114">Se você ainda não tiver feito isso, use as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell no computador local.</span><span class="sxs-lookup"><span data-stu-id="8ef36-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="8ef36-115">Em seguida, abra um prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ef36-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="8ef36-116">Etapa 1: adicionar sua conta</span><span class="sxs-lookup"><span data-stu-id="8ef36-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="8ef36-117">No prompt do PowerShell hello, digite **Add-AzureAccount** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8ef36-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="8ef36-118">Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="8ef36-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="8ef36-119">Digite a senha Olá para sua conta.</span><span class="sxs-lookup"><span data-stu-id="8ef36-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="8ef36-120">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="8ef36-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="8ef36-121">Etapa 2: Definir a assinatura e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8ef36-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="8ef36-122">Defina a assinatura do Azure e a conta de armazenamento executando esses comandos no prompt de comando do Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8ef36-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="8ef36-123">Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com nomes de saudação correto.</span><span class="sxs-lookup"><span data-stu-id="8ef36-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="8ef36-124">Você pode obter o nome de assinatura correta de saudação do hello propriedade de nome de inscrição da saída de saudação do hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="8ef36-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="8ef36-125">Você pode obter o nome de conta de armazenamento correta de saudação do Olá propriedade do rótulo de saída Olá Olá **Get-AzureStorageAccount** comando depois de executar Olá **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="8ef36-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="8ef36-126">Etapa 3: Passo a passo - provisionar a máquina virtual de saudação e ingressar em domínio gerenciado toohello</span><span class="sxs-lookup"><span data-stu-id="8ef36-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="8ef36-127">Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual, com linhas em branco entre cada bloco para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="8ef36-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="8ef36-128">Especifique informações sobre toobe de máquina virtual do Windows hello provisionado.</span><span class="sxs-lookup"><span data-stu-id="8ef36-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="8ef36-129">Para obter valores de InstanceSize Olá para D, DS ou máquinas virtuais de série G, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ef36-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="8ef36-130">Fornece informações sobre o domínio gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="8ef36-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="8ef36-131">Especifique o nome de Olá Olá do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8ef36-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="8ef36-132">Especifique o nome de saudação do Olá Olá de toowhich de rede virtual que VM deve ser unida.</span><span class="sxs-lookup"><span data-stu-id="8ef36-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="8ef36-133">Certifique-se de domínio gerenciados AAD-DS Olá está disponível na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="8ef36-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="8ef36-134">Selecione Olá VM imagem toobe usada tooprovision Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8ef36-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="8ef36-135">Configurar Olá VM - nome do conjunto de VM, instância de tamanho e imagem toobe usada.</span><span class="sxs-lookup"><span data-stu-id="8ef36-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="8ef36-136">Obter credenciais de administrador local para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8ef36-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="8ef36-137">Escolha uma senha de administrador local forte.</span><span class="sxs-lookup"><span data-stu-id="8ef36-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="8ef36-138">Obter credenciais para uma conta de usuário que pertencem a domínio grupo de toojoin VM toohello gerenciado administradores too'AAD DC.</span><span class="sxs-lookup"><span data-stu-id="8ef36-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="8ef36-139">Não especifique nome de domínio Olá - para instância, em nosso exemplo, podemos especificar 'bob' como nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ef36-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="8ef36-140">Configurar Olá VM - especificar o requisito de associação de domínio e as credenciais necessárias.</span><span class="sxs-lookup"><span data-stu-id="8ef36-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="8ef36-141">Defina uma sub-rede para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8ef36-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="8ef36-142">Opcional: Ponto toohello o endereço IP do domínio hello.</span><span class="sxs-lookup"><span data-stu-id="8ef36-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="8ef36-143">Se você definir endereços IP de saudação de saudação do hello serviços de domínio do AD do Azure domínio gerenciado toobe servidores DNS da rede virtual Olá, esta etapa não será necessária.</span><span class="sxs-lookup"><span data-stu-id="8ef36-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="8ef36-144">Agora, Olá provisionar domínio VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="8ef36-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="8ef36-145">Script tooprovision uma VM do Windows e unir automaticamente tooan domínio gerenciado por serviços de domínio do AAD</span><span class="sxs-lookup"><span data-stu-id="8ef36-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="8ef36-146">Esse conjunto de comandos do PowerShell cria uma máquina virtual para um servidor de linha de negócios que:</span><span class="sxs-lookup"><span data-stu-id="8ef36-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="8ef36-147">Usa a imagem do Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="8ef36-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="8ef36-148">É uma máquina virtual extra pequena.</span><span class="sxs-lookup"><span data-stu-id="8ef36-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="8ef36-149">Tem o nome de saudação Contoso100 teste.</span><span class="sxs-lookup"><span data-stu-id="8ef36-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="8ef36-150">É automaticamente domínio unidas toohello contoso100 domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="8ef36-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="8ef36-151">É adicionado toohello mesma rede virtual Olá gerenciados domínio.</span><span class="sxs-lookup"><span data-stu-id="8ef36-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="8ef36-152">Aqui está o hello máquina de virtual do Windows hello amostra completa script toocreate e unir automaticamente toohello domínio gerenciado por serviços de domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ef36-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="8ef36-153">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="8ef36-153">Related Content</span></span>
* [<span data-ttu-id="8ef36-154">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="8ef36-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="8ef36-155">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ef36-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
