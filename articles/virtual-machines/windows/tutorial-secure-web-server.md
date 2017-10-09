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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>Proteger o servidor Web do IIS com certificados SSL em uma máquina virtual do Windows no Azure
servidores de web toosecure, um certificado mais tarde SSL (Secure Sockets) pode ser usado tooencrypt o tráfego da web. Esses certificados SSL podem ser armazenados no cofre de chaves do Azure e permitem implantações seguras de certificados tooWindows (máquinas virtuais) no Azure. Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma máquina virtual e instalar o servidor de web IIS Olá
> * Injetar certificado Olá Olá VM e configurar o IIS com uma associação SSL.

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Visão geral
O cofre da chave do Azure protege chaves criptográficas e segredos, esses certificados ou senhas. Cofre de chaves ajuda a simplificar o processo de gerenciamento de certificado hello e permite que você controle toomaintain de chaves que acessam esses certificados. Você pode criar um certificado autoassinado no Key Vault ou carregar um certificado confiável existente que você já tenha.

Em vez de usar uma imagem de VM personalizada que inclui certificados incorporados, você injeta certificados em uma VM em execução. Esse processo garante que os certificados de mais atualizados de saudação são instalados em um servidor web durante a implantação. Se você renova ou substituir um certificado, você não tem também toocreate uma nova imagem VM personalizada. certificados mais recentes Olá são automaticamente inseridos ao criar VMs adicionais. Durante todo o processo Olá, certificados de saudação nunca deixam Olá plataforma Windows Azure ou são expostos em um modelo, histórico de linha de comando ou script.


## <a name="create-an-azure-key-vault"></a>Criar um Cofre de chaves do Azure
Antes de criar um Key Vault e certificados, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupSecureWeb* em Olá *Leste dos EUA* local:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Em seguida, crie um Key Vault com [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). Cada Cofre de Chave requer um nome exclusivo e deve estar escrito com todas as letras minúsculas. Substitua `<mykeyvault>` no hello exemplo com seu próprio nome exclusivo do Cofre de chaves a seguir:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Gerar um certificado e armazenar no Key Vault
Para uso em produção, você deve importar um certificado válido assinado por um fornecedor confiável com [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). Para este tutorial, hello exemplo a seguir mostra como você pode gerar um certificado autoassinado com [adicionar AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) usa Olá a diretiva de certificado padrão de [ Novo AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

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


## <a name="create-a-virtual-machine"></a>Criar uma máquina virtual
Definir um nome de usuário administrador e a senha para Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Agora você pode criar hello VM com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm). Olá exemplo a seguir cria componentes de rede virtual Olá necessários, configuração Olá sistema operacional e, em seguida, cria uma VM denominada *myVM*:

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

Leva alguns minutos para Olá VM toobe criado. última etapa Hello usa Olá extensão de Script personalizado do Azure tooinstall Olá servidor web do IIS com [AzureRmVmExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Adicionar um certificado tooVM do Cofre de chaves
tooadd certificado de saudação do Cofre de chaves tooa VM, obter a ID de saudação do seu certificado com [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Adicionar certificado de saudação toohello VM com [adicionar AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>Configurar IIS toouse Olá certificado
Use Olá extensão de Script personalizado novamente com [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate a configuração do IIS hello. Esta atualização aplica-se o certificado Olá injetado do Cofre de chaves tooIIS e configura a associação de web hello:

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


### <a name="test-hello-secure-web-app"></a>Aplicativo de teste na web segura de Olá
Obter o endereço IP público de saudação da VM com [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Olá, exemplo a seguir obtém endereço IP hello `myPublicIP` criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Agora você pode abrir um navegador da web e digite `https://<myPublicIP>` na barra de endereços de saudação. Aviso de segurança de saudação tooaccept se você usou um certificado autoassinado, selecione **detalhes** e **ir na página da Web de toohello**:

![Aceite o aviso de segurança do navegador da web](./media/tutorial-secure-web-server/browser-warning.png)

O site seguro do IIS, em seguida, é exibido como Olá exemplo a seguir:

![Exibir o site de IIS protegido em execução](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você protegeu um servidor Web de IIS com um certificado SSL armazenado no Azure Key Vault. Você aprendeu como:

> [!div class="checklist"]
> * Criar um Cofre de chaves do Azure
> * Gerar ou carregar um certificado toohello Cofre de chaves
> * Criar uma máquina virtual e instalar o servidor de web IIS Olá
> * Injetar certificado Olá Olá VM e configurar o IIS com uma associação SSL.

Siga este toosee link pré-criadas exemplos de script da máquina virtual.

> [!div class="nextstepaction"]
> [Exemplos de script de máquina virtual do Windows](./powershell-samples.md)