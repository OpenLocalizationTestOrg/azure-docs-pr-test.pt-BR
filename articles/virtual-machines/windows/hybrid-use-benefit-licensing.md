---
title: "aaaAzure híbrida benefício de usar para o Windows Server e Windows Client | Microsoft Docs"
description: "Saiba como toomaximize seu toobring benefícios de garantia de Software do Windows local tooAzure de licenças"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Benefício de Uso Híbrido do Azure para o Windows Server e o Windows Client
Para clientes com Software Assurance, o benefício de uso do Azure híbrido permite toouse suas licenças de cliente Windows Server e Windows de local e executadas máquinas virtuais do Windows no Azure a um custo reduzido. O Benefício de Uso Híbrido do Azure para o Windows Server inclui o Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016. O Benefício de Uso Híbrido do Azure para o Windows Client inclui o Windows 10. Para obter mais informações, consulte Olá [página de licenciamento do benefício de uso do Azure híbrido](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure híbrido Use benefícios para o cliente do Windows está atualmente em visualização usando imagem Olá Windows 10 em hello Azure Marketplace. Somente clientes Enterprise com o Windows 10 Enterprise E3/E5 por usuário ou o Windows VDA por usuário (Licenças de Assinatura de Usuário ou Licenças de Assinatura de Usuário Complementares) (“Licenças Aplicáveis”) são qualificados.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Maneiras toouse benefício de uso do Azure híbrido
Há duas maneiras diferentes toodeploy VMs do Windows com hello benefício de uso do Azure híbrido:

1. Você pode implantar VMs das [imagens específicas do Marketplace](#deploy-a-vm-using-the-azure-marketplace) que são pré-configuradas com o benefício de uso do Azure Hybrid – Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.
2. Você pode [carregar uma VM personalizada](#upload-a-windows-vhd) e [implantar usando um modelo do Resource Manager](#deploy-a-vm-via-resource-manager) ou [do Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Implantar uma VM usando hello Azure Marketplace
Imagens a seguir estão disponíveis no hello Marketplace pré-configurado com o benefício de uso do Azure híbrido: Windows Server 2016, o Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1. Essas imagens podem ser implantadas diretamente de saudação portal do Azure, modelos do Gerenciador de recursos ou do PowerShell do Azure.

Você pode implantar essas imagens diretamente do hello portal do Azure. Para uso em modelos do Gerenciador de recursos e com o Azure PowerShell, exiba a lista de saudação de imagens da seguinte maneira:

Para Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter versão 2016.127.20170406 ou superior

- 2012-R2-Datacenter versão 4.127.20170406 ou superior

- 2012-Datacenter versão 3.127.20170406 ou superior

- 2008-R2-SP1 versão 2.127.20170406 ou superior

Para Windows Client:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Carregar um VHD do Windows Server
toodeploy uma VM do Windows Server no Azure, você primeiro precisa toocreate um VHD que contém seu build do Windows base. Esse VHD deve estar preparado adequadamente por meio de Sysprep antes de carregá-lo tooAzure. Você pode [Leia mais sobre o processo do Sysprep e os requisitos de VHD de saudação](upload-generalized-managed.md) e [suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Faça backup Olá VM antes de executar o Sysprep. 

Verifique se você tem [mais recente do PowerShell do Azure instalado e configurado hello](/powershell/azure/overview). Depois de preparar o VHD, carregar conta de armazenamento do Azure Olá VHD tooyour usando Olá `Add-AzureRmVhd` cmdlet da seguinte maneira:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> O Microsoft SQL Server, SharePoint Server e Dynamics também podem utilizar o licenciamento Software Assurance. Você ainda precisa imagem de servidor do Windows hello tooprepare instalando os componentes do aplicativo e fornecendo as chaves de licença adequadamente, em seguida, carregar Olá tooAzure de imagem de disco. Examine a documentação apropriada Olá para executar o Sysprep com seu aplicativo, como [considerações sobre a instalação do SQL Server usando Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) ou [montar uma imagem de referência do SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Você também pode ler mais sobre [Olá VHD tooAzure processo de carregamento](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Implantar uma VM por meio de um modelo do Resource Manager
Nos modelos do Resource Manager, um parâmetro adicional para `licenseType` pode ser especificado. Você pode ler mais sobre a [criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md). Uma vez que o VHD carregado tooAzure, edite é o tipo de licença do Gerenciador de recursos modelo tooinclude hello como parte da saudação provedor de computação e implantar o modelo como normal:

Para Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Para o cliente do Windows toouse com a imagem do Azure Marketplace só:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Implantar uma VM por meio do início rápido do PowerShell
Ao implantar a VM do Windows Server por meio do PowerShell, você tem um parâmetro adicional para `-LicenseType`. Uma vez que o VHD carregado tooAzure, criar uma VM usando `New-AzureRmVM` e especificar o tipo de licenciamento de saudação da seguinte maneira:

Para Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Para o cliente do Windows toouse com a imagem do Azure Marketplace só:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Você pode [ler uma explicação mais detalhada sobre como implantar uma VM no Azure por meio do PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) abaixo ou leitura um guia mais descritivo Olá diferentes etapas muito[criar uma VM do Windows usando o Gerenciador de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Verifique se que a VM está utilizando o benefício de licenciamento Olá
Depois de implantar sua VM por meio de saudação do PowerShell ou método de implantação do Gerenciador de recursos, verificar o tipo de licença de saudação com `Get-AzureRmVM` da seguinte maneira:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

saudação de saída é similar toohello exemplo a seguir para o Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Essa saída contrasta com hello que seguir VM implantada sem licenciamento benefício de uso do Azure híbrido, como uma VM implantada diretamente da saudação Galeria do Azure:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Passo a passo detalhado de implantação do PowerShell
a seguir Olá detalhadas Mostrar de etapas do PowerShell uma implantação completa de uma VM. Você pode ler mais contexto como cmdlets real toohello e componentes diferentes, que está sendo criados no [criar uma VM do Windows usando o Gerenciador de recursos e o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Você passa pela criação de seu grupo de recursos, da conta de armazenamento e da rede virtual e, por fim, define e crie sua VM.

Primeiro, obtenha credenciais com segurança, defina um local e o nome do grupo de recursos:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Criar um IP público:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Defina sua sub-rede, NIC e VNET:

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

Nomeie sua VM e crie uma configuração da VM:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Defina seu sistema operacional:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Adicione seu toohello NIC VM:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Defina Olá toouse de conta de armazenamento:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Carregar o VHD, adequadamente preparado e anexar tooyour VM para uso:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Finalmente, crie sua VM e definir Olá tipo tooutilize benefício de uso do Azure híbrido de licenciamento:

Para Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Implantar um conjunto de dimensionamento de máquinas virtuais por meio do modelo do Gerenciador de Recursos
Nos modelos do Gerenciador de Recursos VMSS, um parâmetro adicional para `licenseType` deve ser especificado. Você pode ler mais sobre a [criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md). Editar a propriedade de licenseType saudação do Gerenciador de recursos modelo tooinclude como parte do virtualMachineProfile do conjunto de escala hello e implantar o modelo como normal - consulte o exemplo a seguir usando a imagem do Windows Server 2016:


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> O suporte para implantação de um conjunto de dimensionamento da máquina virtual com benefícios AHUB por meio do PowerShell e de outras ferramentas de SDK está disponível em breve.
>

## <a name="next-steps"></a>Próximas etapas
Leia mais sobre o [Licenciamento do Benefício de Uso Híbrido do Azure](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Saiba mais sobre como [usar os modelos do Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Saiba mais sobre [benefício de usar híbrido do Azure e o Azure Site Recovery fazem migração tooAzure de aplicativos ainda mais econômica](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
