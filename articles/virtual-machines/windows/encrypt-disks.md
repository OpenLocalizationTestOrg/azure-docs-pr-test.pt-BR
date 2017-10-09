---
title: aaaEncrypt discos em uma VM do Windows Azure | Microsoft Docs
description: "Como o tooencrypt de discos virtuais em uma VM do Windows para melhor segurança usando o PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Como tooencrypt de discos virtuais em uma VM do Windows
Para conformidade e segurança aprimorados da VM (máquina virtual), os discos virtuais no Azure podem ser criptografados. Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure. Você controla essas chaves criptográficas e pode auditar seu uso. Este artigo detalhes como tooencrypt de discos virtuais em uma VM do Windows usando o PowerShell do Azure. Você também pode [criptografar uma VM do Linux usando hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Visão geral da criptografia de disco
Discos virtuais em VMs do Windows são criptografados em repouso usando o Bitlocker. Não há nenhuma taxa para criptografar discos virtuais no Azure. As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2. Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM. Você mantém o controle dessas chaves criptográficas e pode auditar seu uso. Uma entidade de serviço do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves de criptografia, enquanto as VMs são ligadas e desligadas.

processo de saudação de criptografia de uma VM é o seguinte:

1. Crie uma chave de criptografia em um Cofre de chaves do Azure.
2. Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.
3. chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, criar um serviço do Active Directory do Azure principal com as permissões adequadas hello.
4. Emita Olá comando tooencrypt seus discos virtuais, especificação de entidade de serviço do Active Directory do Azure hello e adequado toobe chave criptográfica usada.
5. solicitações do principais de serviço do Active Directory do Azure Olá Olá chave de criptografia necessária do Cofre de chaves do Azure.
6. discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.

## <a name="encryption-process"></a>Processo de criptografia
Criptografia de disco se baseia em Olá componentes adicionais a seguir:

* **Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello. 
  * Se houver um, você pode usar um Cofre de Chaves do Azure existente. Você não tem toodedicate discos tooencrypting um cofre de chaves.
  * limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.
* **Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada. 
  * Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.
  * entidade de serviço Olá fornece um mecanismo seguro toorequest e emitido chaves de criptografia apropriadas hello. Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisitos e limitações
Requisitos e cenários com suporte para criptografia de disco:

* Habilitar a criptografia em novas VMs do Windows a partir de imagens do Azure Marketplace ou de uma imagem VHD personalizada.
* Habilitar a criptografia em VMs existentes do Windows no Azure.
* Habilitar a criptografia em VMs do Windows que são configuradas usando Espaços de Armazenamento.
* Como desabilitar a criptografia no OS e em unidades de dados para VMs do Windows.
* Todos os recursos (como o Cofre de chaves, a conta de armazenamento e VM) devem estar no hello mesma região do Azure e assinatura.
* VMs de camada padrão, como as VMs da série A, D, DS, G e GS.

Criptografia de disco não é suportada em Olá os seguintes cenários:

* VMs de camada básica.
* Máquinas virtuais criadas usando o modelo de implantação clássico hello.
* Atualizando chaves de criptografia de saudação em uma VM já criptografada.
* Integração com o Serviço de Gerenciamento de Chaves local.

## <a name="create-azure-key-vault-and-keys"></a>Criar o Azure Key Vault e as chaves
Antes de começar, certifique-se se Olá a última versão de hello Azure PowerShell módulo foi instalado. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Ao longo de exemplos de comando hello, substitua todos os parâmetros de exemplo com seus próprios nomes, o local e valores de chave. Olá, exemplos a seguir usam uma convenção de *myResourceGroup*, *myKeyVault*, *myVM*, etc.

primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas. Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços. Para criptografia de disco virtual, crie um cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais. 

Habilitar provedor de Azure Key Vault hello dentro de sua assinatura do Azure com [registro AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), em seguida, crie um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um nome de grupo de recursos *myResourceGroup* em Olá *Leste dos EUA* local:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região. Criar um cofre de chaves do Azure com [AzureRmKeyVault novo](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e habilitar Olá Cofre de chaves para uso com criptografia de disco. Especifique um nome exclusivo de Key Vault para *keyVaultName* da seguinte maneira:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software. Usar um HSM requer um Cofre de Chaves premium. Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software. toocreate um cofre de chaves, premium em Olá anterior etapa Adicionar Olá *- Sku "Premium"* parâmetros. Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão. 

Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello. Crie uma chave de criptografia em seu Key Vault com [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Olá, exemplo a seguir cria uma chave chamada *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Criar hello entidade de serviço do Active Directory do Azure
Quando discos virtuais são criptografados ou descriptografados, especifique um conta toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves. Essa conta, uma entidade de serviço do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM. Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.

Crie uma entidade de serviço no Azure Active Directory com [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify uma senha segura, execute Olá [políticas de senha e restrições do Active Directory do Azure](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory tooread principal Olá as chaves de serviço. Defina permissões no Key Vault com [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Criar máquina virtual
tootest Olá o processo de criptografia, vamos criar uma máquina virtual. Olá, exemplo a seguir cria uma VM denominada *myVM* usando um *Datacenter do Windows Server 2016* imagem:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Criptografar máquina virtual
discos virtuais do tooencrypt hello, você reúne todos os componentes anteriores do hello:

1. Especifique Olá entidade de serviço do Active Directory do Azure e a senha.
2. Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.
3. Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.
4. Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.

Criptografar sua VM com [AzureRmVMDiskEncryptionExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) usando a chave de Cofre de chaves do Azure hello e credenciais de entidade de serviço do Active Directory do Azure. Olá exemplo a seguir recupera todas as informações de chave hello, em seguida, criptografa Olá VM denominada *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Aceite Olá toocontinue de prompt com criptografia de VM hello. Olá VM reinicia durante o processo de saudação. Depois de conclusão do processo de criptografia hello e hello VM será reinicializado, examinar o status de criptografia de saudação com [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

saudação de saída é similar toohello exemplo a seguir:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Próximas etapas
* Para saber mais sobre como gerenciar o Azure Key Vault, confira [Configurar o Key Vault para máquinas virtuais](key-vault-setup.md).
* Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).
