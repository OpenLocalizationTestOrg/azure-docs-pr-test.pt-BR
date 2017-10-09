---
title: certificados de aaaSecure IIS com SSL no Azure | Microsoft Docs
description: "Saiba como toosecure Olá IIS web server com certificados SSL em uma VM do Windows Azure"
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
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="39478-103">Proteger o servidor Web do IIS com certificados SSL em uma máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="39478-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="39478-104">servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser usado tooencrypt o tráfego da web.</span><span class="sxs-lookup"><span data-stu-id="39478-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="39478-105">Esses certificados SSL podem ser armazenados no cofre de chaves do Azure e permitem implantações seguras de certificados tooWindows (máquinas virtuais) no Azure.</span><span class="sxs-lookup"><span data-stu-id="39478-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="39478-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="39478-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39478-107">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="39478-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="39478-108">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="39478-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="39478-109">Criar uma máquina virtual e instalar o servidor de web IIS Olá</span><span class="sxs-lookup"><span data-stu-id="39478-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="39478-110">Injetar certificado Olá Olá VM e configurar o IIS com uma associação SSL.</span><span class="sxs-lookup"><span data-stu-id="39478-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="39478-111">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="39478-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="39478-112">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="39478-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="39478-113">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="39478-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="39478-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="39478-114">Overview</span></span>
<span data-ttu-id="39478-115">O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas.</span><span class="sxs-lookup"><span data-stu-id="39478-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="39478-116">Cofre de chaves ajuda a simplificar o processo de gerenciamento de certificado hello e permite que você controle toomaintain de chaves que acessam esses certificados.</span><span class="sxs-lookup"><span data-stu-id="39478-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="39478-117">Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.</span><span class="sxs-lookup"><span data-stu-id="39478-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="39478-118">Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução.</span><span class="sxs-lookup"><span data-stu-id="39478-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="39478-119">Esse processo garante que os certificados de mais atualizados de saudação são instalados em um servidor web durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="39478-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="39478-120">Se você renova ou substituir um certificado, você não tem também toocreate uma nova imagem VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="39478-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="39478-121">certificados mais recentes Olá são automaticamente inseridos ao criar VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="39478-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="39478-122">Durante todo o processo Olá, certificados de saudação nunca deixam Olá plataforma Windows Azure ou são expostos em um modelo, histórico de linha de comando ou script.</span><span class="sxs-lookup"><span data-stu-id="39478-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="39478-123">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="39478-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="39478-124">Antes de criar um Key Vault e certificados, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="39478-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="39478-125">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupSecureWeb* em Olá *Leste dos EUA* local:</span><span class="sxs-lookup"><span data-stu-id="39478-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="39478-126">Em seguida, crie um Key Vault com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="39478-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="39478-127">Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="39478-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="39478-128">Substitua `<mykeyvault>` no hello exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:</span><span class="sxs-lookup"><span data-stu-id="39478-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="39478-129">Gerar um certificado e armazenar no Key Vault</span><span class="sxs-lookup"><span data-stu-id="39478-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="39478-130">Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="39478-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="39478-131">Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [adicionar AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) usa Olá a diretiva de certificado padrão de [ Novo AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="39478-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="39478-132">Criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="39478-132">Create a virtual machine</span></span>
<span data-ttu-id="39478-133">Definir um nome de usuário administrador e a senha para Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="39478-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="39478-134">Agora você pode criar hello VM com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="39478-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="39478-135">Olá exemplo a seguir cria componentes de rede virtual Olá necessários, configuração Olá sistema operacional e, em seguida, cria uma VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="39478-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="39478-136">Leva alguns minutos para Olá VM toobe criado.</span><span class="sxs-lookup"><span data-stu-id="39478-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="39478-137">última etapa Hello usa Olá extensão de Script personalizado do Azure tooinstall Olá servidor web do IIS com [AzureRmVmExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="39478-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="39478-138">Adicionar um certificado tooVM do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="39478-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="39478-139">tooadd certificado de saudação do Cofre de chaves tooa VM, obter a ID de saudação do seu certificado com [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="39478-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="39478-140">Adicionar certificado de saudação toohello VM com [adicionar AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="39478-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="39478-141">Configurar IIS toouse Olá certificado</span><span class="sxs-lookup"><span data-stu-id="39478-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="39478-142">Use Olá extensão de Script personalizado novamente com [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate a configuração do IIS hello.</span><span class="sxs-lookup"><span data-stu-id="39478-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="39478-143">Esta atualização aplica-se o certificado Olá injetado do Cofre de chaves tooIIS e configura a associação de web hello:</span><span class="sxs-lookup"><span data-stu-id="39478-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

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


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="39478-144">Aplicativo de teste na web segura de Olá</span><span class="sxs-lookup"><span data-stu-id="39478-144">Test hello secure web app</span></span>
<span data-ttu-id="39478-145">Obter o endereço IP público de saudação da VM com [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="39478-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="39478-146">Olá, exemplo a seguir obtém endereço IP hello `myPublicIP` criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="39478-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="39478-147">Agora você pode abrir um navegador da web e digite `https://<myPublicIP>` na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="39478-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="39478-148">Aviso de segurança de saudação tooaccept se você usou um certificado autoassinado, selecione **detalhes** e **ir na página da Web de toohello**:</span><span class="sxs-lookup"><span data-stu-id="39478-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="39478-150">O site seguro do IIS, em seguida, é exibido como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="39478-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Exibir o site de IIS protegido em execução](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="39478-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39478-152">Next steps</span></span>

<span data-ttu-id="39478-153">Neste tutorial, você protegeu um servidor Web de IIS com um certificado SSL armazenado no Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="39478-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="39478-154">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="39478-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39478-155">Criar um Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="39478-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="39478-156">Gerar ou carregar um certificado toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="39478-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="39478-157">Criar uma máquina virtual e instalar o servidor de web IIS Olá</span><span class="sxs-lookup"><span data-stu-id="39478-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="39478-158">Injetar certificado Olá Olá VM e configurar o IIS com uma associação SSL.</span><span class="sxs-lookup"><span data-stu-id="39478-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="39478-159">Siga este toosee link pré-criadas exemplos de script da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="39478-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39478-160">Exemplos de script de máquina virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="39478-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)