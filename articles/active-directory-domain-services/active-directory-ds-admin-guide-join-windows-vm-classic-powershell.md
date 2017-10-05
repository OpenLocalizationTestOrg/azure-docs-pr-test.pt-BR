---
title: "Azure Active Directory Domain Services: guia de administração | Microsoft Docs"
description: "Ingresse uma máquina virtual do Windows em um domínio gerenciado usando o Azure PowerShell e o modelo de implantação clássico."
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
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="cfac9-103">Ingressar uma máquina virtual do Windows Server em um domínio gerenciado usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfac9-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfac9-104">Portal clássico do Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="cfac9-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="cfac9-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="cfac9-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="cfac9-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cfac9-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cfac9-107">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="cfac9-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="cfac9-108">Os Serviços de Domínio do Azure AD no momento não dá suporte para o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cfac9-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="cfac9-109">Estas etapas mostram como personalizar um conjunto de comandos do Azure PowerShell que criam e pré-configuram uma máquina virtual do Azure baseada em Windows usando uma abordagem de bloco de construção.</span><span class="sxs-lookup"><span data-stu-id="cfac9-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="cfac9-110">Essas etapas ajudam a criar uma máquina virtual do Azure baseada no Windows e a ingressá-la no domínio gerenciado dos Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfac9-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="cfac9-111">Estas etapas seguem uma abordagem de preencher lacunas para criar conjuntos de comandos do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfac9-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="cfac9-112">Esta abordagem poderá ser útil se você ainda não conhece o PowerShell ou se quiser saber quais valores especificar para uma configuração bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="cfac9-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="cfac9-113">Os usuários avançados do PowerShell podem pegar os comandos e substituí-los por seus próprios valores de variáveis (as linhas que começam com "$").</span><span class="sxs-lookup"><span data-stu-id="cfac9-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="cfac9-114">Se você ainda não fez isso, use as instruções em [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview) para instalar o PowerShell do Azure no computador local.</span><span class="sxs-lookup"><span data-stu-id="cfac9-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="cfac9-115">Em seguida, abra um prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfac9-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="cfac9-116">Etapa 1: adicionar sua conta</span><span class="sxs-lookup"><span data-stu-id="cfac9-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="cfac9-117">No prompt do PowerShell, digite **Add-AzureAccount** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cfac9-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="cfac9-118">Digite o endereço de email associado à sua assinatura do Azure e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="cfac9-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="cfac9-119">Digite a senha da sua conta.</span><span class="sxs-lookup"><span data-stu-id="cfac9-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="cfac9-120">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="cfac9-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="cfac9-121">Etapa 2: Definir a assinatura e a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="cfac9-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="cfac9-122">Defina a assinatura e a conta de armazenamento do Azure executando estes comandos no prompt de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfac9-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="cfac9-123">Substitua tudo que estiver entre aspas, incluindo os caracteres < e >, pelos nomes corretos.</span><span class="sxs-lookup"><span data-stu-id="cfac9-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="cfac9-124">Você pode obter o nome de assinatura correto na propriedade SubscriptionName da saída do comando **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="cfac9-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="cfac9-125">Você pode obter o nome da conta de armazenamento correto na propriedade Label da saída do comando **Get-AzureStorageAccount**, após executar o comando **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="cfac9-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="cfac9-126">Etapa 3: Passo a passo - provisionar a máquina virtual e ingressa-la ao domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="cfac9-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="cfac9-127">Aqui está o conjunto de comandos do PowerShell do Azure correspondente para criar essa máquina virtual, com linhas em branco entre cada bloco para facilitar a leitura.</span><span class="sxs-lookup"><span data-stu-id="cfac9-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="cfac9-128">Especifique as informações sobre a máquina virtual do Windows a ser provisionada.</span><span class="sxs-lookup"><span data-stu-id="cfac9-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="cfac9-129">Para os valores de InstanceSize para máquinas virtuais da série D, DS ou G, confira [Tamanhos de máquina virtual e serviços de nuvem no Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfac9-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="cfac9-130">Forneça informações sobre o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="cfac9-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="cfac9-131">Especifique o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cfac9-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="cfac9-132">Especifique o nome da rede virtual na qual a VM deve ser ingressada.</span><span class="sxs-lookup"><span data-stu-id="cfac9-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="cfac9-133">Certifique-se de que o domínio gerenciado do DS do AAD esteja disponível nessa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cfac9-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="cfac9-134">Selecione a imagem da VM a ser usada para provisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="cfac9-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="cfac9-135">Configure a VM: defina o nome da VM, o tamanho da instância e a imagem a ser usada.</span><span class="sxs-lookup"><span data-stu-id="cfac9-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="cfac9-136">Obtenha credenciais de administrador local para a VM.</span><span class="sxs-lookup"><span data-stu-id="cfac9-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="cfac9-137">Escolha uma senha de administrador local forte.</span><span class="sxs-lookup"><span data-stu-id="cfac9-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="cfac9-138">Obtenha credenciais de uma conta de usuário que pertence ao grupo ‘Administradores do DC do AAD’ para ingressar a VM ao domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="cfac9-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="cfac9-139">Não especifique o nome de domínio: por exemplo, em nosso exemplo, podemos especificar “bob” como nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="cfac9-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="cfac9-140">Configure a VM: especifique o requisito de ingresso no domínio e as credenciais necessárias.</span><span class="sxs-lookup"><span data-stu-id="cfac9-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="cfac9-141">Defina uma sub-rede para a VM.</span><span class="sxs-lookup"><span data-stu-id="cfac9-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="cfac9-142">Opcional: aponte para o endereço IP do domínio.</span><span class="sxs-lookup"><span data-stu-id="cfac9-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="cfac9-143">Se você definir os endereços IP dos domínios gerenciados de Serviços de Domínio do Azure AD para serem servidores DNS para a rede virtual, essa etapa não será necessária.</span><span class="sxs-lookup"><span data-stu-id="cfac9-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="cfac9-144">Agora, provisione a VM do Windows ingressada no domínio.</span><span class="sxs-lookup"><span data-stu-id="cfac9-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="cfac9-145">Script para provisionar uma VM do Windows e automaticamente ingressar em um domínio gerenciado dos Serviços de Domínio do AAD</span><span class="sxs-lookup"><span data-stu-id="cfac9-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="cfac9-146">Esse conjunto de comandos do PowerShell cria uma máquina virtual para um servidor de linha de negócios que:</span><span class="sxs-lookup"><span data-stu-id="cfac9-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="cfac9-147">Usa a imagem do Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="cfac9-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="cfac9-148">É uma máquina virtual extra pequena.</span><span class="sxs-lookup"><span data-stu-id="cfac9-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="cfac9-149">Tem o nome Contoso100-test.</span><span class="sxs-lookup"><span data-stu-id="cfac9-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="cfac9-150">É automaticamente ingressada no domínio para o domínio gerenciado contoso100.</span><span class="sxs-lookup"><span data-stu-id="cfac9-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="cfac9-151">É adicionado à mesma rede virtual como o domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="cfac9-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="cfac9-152">Aqui está o script de exemplo completo para criar a máquina virtual do Windows e ingressá-la automaticamente no domínio gerenciado dos Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfac9-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="cfac9-153">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="cfac9-153">Related Content</span></span>
* [<span data-ttu-id="cfac9-154">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="cfac9-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="cfac9-155">Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfac9-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
