---
title: Proteger o IIS com certificados SSL no Azure | Microsoft Docs
description: Saiba como proteger o servidor Web do IIS com certificados SSL em uma VM do Windows Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="a25bf-103">Proteger o servidor Web do IIS com certificados SSL em uma máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="a25bf-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="a25bf-104">Para proteger os servidores Web, um certificado SSL (Secure Sockets Layer) pode ser usado para criptografar o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="a25bf-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="a25bf-105">Esses certificados SSL podem ser armazenados no Azure Key Vault e permitem implantações seguras de certificados em VMs (máquinas virtuais) do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="a25bf-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="a25bf-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="a25bf-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a25bf-107">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="a25bf-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a25bf-108">Gerar ou carregar um certificado para o Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="a25bf-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="a25bf-109">Criar uma VM e instalar o servidor Web do IIS</span><span class="sxs-lookup"><span data-stu-id="a25bf-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="a25bf-110">Inserir o certificado na VM e configurar o IIS com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="a25bf-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="a25bf-111">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a25bf-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a25bf-112">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="a25bf-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="a25bf-113">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a25bf-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="a25bf-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a25bf-114">Overview</span></span>
<span data-ttu-id="a25bf-115">O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas.</span><span class="sxs-lookup"><span data-stu-id="a25bf-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="a25bf-116">O Key Vault simplifica o processo de gerenciamento de certificados e permite que você mantenha o controle das chaves que acessam esses certificados.</span><span class="sxs-lookup"><span data-stu-id="a25bf-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="a25bf-117">Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.</span><span class="sxs-lookup"><span data-stu-id="a25bf-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="a25bf-118">Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="a25bf-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="a25bf-119">Esse processo garante que os certificados mais recentes sejam instalados em um servidor Web durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a25bf-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="a25bf-120">Se você renova ou substitui um certificado, também não precisa criar uma nova imagem de VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="a25bf-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="a25bf-121">Os certificados mais recentes são inseridos automaticamente, conforme você cria outras VMs.</span><span class="sxs-lookup"><span data-stu-id="a25bf-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="a25bf-122">Durante todo o processo, os certificados nunca deixam a plataforma do Azure ou são expostos em um script, no histórico da linha de comando ou no modelo.</span><span class="sxs-lookup"><span data-stu-id="a25bf-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="a25bf-123">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="a25bf-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="a25bf-124">Antes de criar um Key Vault e certificados, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a25bf-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="a25bf-125">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroupSecureWeb* no local *Leste dos EUA*:</span><span class="sxs-lookup"><span data-stu-id="a25bf-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="a25bf-126">Em seguida, crie um Key Vault com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="a25bf-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="a25bf-127">Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a25bf-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="a25bf-128">Substitua `<mykeyvault>` no exemplo a seguir com seu próprio nome exclusivo de Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="a25bf-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="a25bf-129">Gerar um certificado e armazenar no Key Vault</span><span class="sxs-lookup"><span data-stu-id="a25bf-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="a25bf-130">Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="a25bf-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="a25bf-131">Para este tutorial, o exemplo a seguir mostra como você pode gerar um certificado autoassinado com [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate), que usa a política de certificado padrão de [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="a25bf-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="a25bf-132">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a25bf-132">Create a virtual machine</span></span>
<span data-ttu-id="a25bf-133">Defina o nome de usuário e a senha de um administrador para a VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="a25bf-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="a25bf-134">Agora você pode criar uma VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a25bf-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="a25bf-135">O exemplo a seguir cria os componentes de rede virtual necessários, a configuração do SO e, em seguida, cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a25bf-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="a25bf-136">A criação da VM demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a25bf-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="a25bf-137">A última etapa usa a Extensão de Script Personalizado do Azure para instalar o servidor Web do IIS com [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="a25bf-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="a25bf-138">Adicionar um certificado à VM a partir do Key Vault</span><span class="sxs-lookup"><span data-stu-id="a25bf-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="a25bf-139">Para adicionar o certificado a partir do Key Vault para uma VM, obtenha a ID de seu certificado com [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="a25bf-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="a25bf-140">Adicione o certificado à VM com [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="a25bf-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="a25bf-141">Configurar o IIS para usar o certificado</span><span class="sxs-lookup"><span data-stu-id="a25bf-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="a25bf-142">Use a Extensão de Script Personalizado novamente com [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para atualizar a configuração do IIS.</span><span class="sxs-lookup"><span data-stu-id="a25bf-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="a25bf-143">Esta atualização aplica o certificado inserido do Key Vault para o IIS e configura a associação da Web:</span><span class="sxs-lookup"><span data-stu-id="a25bf-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="a25bf-144">Testar o aplicativo Web protegido</span><span class="sxs-lookup"><span data-stu-id="a25bf-144">Test the secure web app</span></span>
<span data-ttu-id="a25bf-145">Obtenha os endereços IP públicos da VM com [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="a25bf-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="a25bf-146">O exemplo a seguir obtém o endereço IP para `myPublicIP` criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a25bf-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="a25bf-147">Agora, abra um navegador da Web e digite `https://<myPublicIP>` na barra de endereços.</span><span class="sxs-lookup"><span data-stu-id="a25bf-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="a25bf-148">Para aceitar o aviso de segurança se você usou um certificado autoassinado, selecione **Detalhes** e **Prosseguir para a página da Web**:</span><span class="sxs-lookup"><span data-stu-id="a25bf-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="a25bf-150">Seu site de IIS protegido é exibido, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a25bf-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Exibir o site de IIS protegido em execução](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="a25bf-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a25bf-152">Next steps</span></span>

<span data-ttu-id="a25bf-153">Neste tutorial, você protegeu um servidor Web de IIS com um certificado SSL armazenado no Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a25bf-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="a25bf-154">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="a25bf-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a25bf-155">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="a25bf-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a25bf-156">Gerar ou carregar um certificado para o Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="a25bf-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="a25bf-157">Criar uma VM e instalar o servidor Web do IIS</span><span class="sxs-lookup"><span data-stu-id="a25bf-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="a25bf-158">Inserir o certificado na VM e configurar o IIS com uma associação de SSL</span><span class="sxs-lookup"><span data-stu-id="a25bf-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="a25bf-159">Siga este link para ver exemplos de script de máquina virtual predefinido.</span><span class="sxs-lookup"><span data-stu-id="a25bf-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a25bf-160">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="a25bf-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)