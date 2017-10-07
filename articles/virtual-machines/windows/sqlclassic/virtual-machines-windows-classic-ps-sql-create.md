---
title: "aaaCreate uma máquina Virtual do SQL Server no Azure PowerShell (clássico) | Microsoft Docs"
description: "Fornece etapas e scripts do PowerShell para criar uma VM do Azure com imagens da galeria de máquinas virtuais do SQL Server. Este tópico usa o modo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Provisionar uma máquina virtual do SQL Server usando o Azure PowerShell (Clássico)

Este artigo fornece etapas para como toocreate uma máquina de virtual do SQL Server no Azure usando Olá cmdlets do PowerShell.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Para a versão do Gerenciador de recursos de saudação deste tópico, consulte [provisionar uma máquina virtual do SQL Server usando o Gerenciador de recursos do Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Instalar e configurar o PowerShell:
1. Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Baixe e instale os comandos do PowerShell do Azure mais recentes Olá](/powershell/azure/overview).
3. Inicie o Windows PowerShell e conectá-lo tooyour assinatura do Azure com hello **Add-AzureAccount** comando.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Determinar o região de destino do Azure

A máquina virtual do SQL Server será hospedada em um serviço de nuvem que reside em uma região específica do Azure. Olá etapas a seguir ajudam você toodetermine sua região, a conta de armazenamento e o serviço de nuvem que será usado para o restante de saudação do tutorial de saudação.

1. Determine o Datacenter Olá que você deseja toouse toohost VM do SQL Server. saudação de comando do PowerShell a seguir exibe uma lista de nomes de região disponível.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Depois de identificar o local preferencial, definir uma variável denominada **$dcLocation** toothat região. Por exemplo, Olá conjuntos Olá região muito de comando a seguir "Leste dos Estados Unidos":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Definir a assinatura e a conta de armazenamento

1. Determine Olá assinatura do Azure que você usará para a máquina virtual da nova hello.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Atribuir o toohello de assinatura do Azure de destino **$subscr** variável. Em seguida, defina isso como sua assinatura atual do Azure.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Verifique se há contas de armazenamento existentes. Olá, script a seguir exibe todas as contas de armazenamento que existem em sua região escolhida:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Se você precisar de uma nova conta de armazenamento, primeiro crie um nome de conta de armazenamento de todas as minúsculas com o comando Olá novo AzureStorageAccount como Olá exemplo a seguir:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Atribuir Olá destino armazenamento conta nome toohello **$staccount**. Em seguida, use **Set-AzureSubscription** tooset Olá assinatura e a conta de armazenamento atual.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Selecione uma imagem de máquina virtual do SQL Server

1. Descobrir a lista de saudação de imagens de máquinas virtuais do SQL Server disponíveis na Galeria de saudação. Todas essas imagens têm uma propriedade **ImageFamily** que começa com "SQL". consulta a seguir de saudação exibe Olá imagem família disponível tooyou com o SQL Server pré-instalado.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Quando você encontrar família de imagem de máquina virtual hello, pode haver várias imagens publicadas nesta família. Script a seguir de saudação do uso toofind hello mais recente publicada imagem nome da máquina virtual para sua família de imagem selecionada (como **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Criar a máquina virtual de saudação

Finalmente, crie a máquina virtual de saudação com o PowerShell:

1. Criar uma nuvem toohost serviço Olá nova VM. Observe que também é possível toouse um serviço de nuvem existente em vez disso. Criar uma nova variável **$svcname** com o nome curto de Olá Olá do serviço de nuvem.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Especifique o nome da máquina virtual hello e um tamanho. Para obter mais informações sobre tamanhos de máquina virtual, consulte [Tamanhos de Máquina Virtual para o Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Especifique a senha e a conta de administrador local hello.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Execute Olá máquina virtual do script toocreate Olá a seguir.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Para explicação adicional e opções de configuração, consulte Olá **criar o conjunto de comandos** seção [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Exemplo de script do PowerShell

Olá, script a seguir fornece um exemplo de um script completo que cria um **SQL Server 2016 RTM Enterprise no Windows Server 2012 R2** máquina virtual. Se você usar esse script, você deve personalizar variáveis inicial hello, com base em etapas de saudação anterior neste tópico.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Conectar-se à área de trabalho remota

1. Crie arquivos RDP de saudação em toolaunch de pasta de documentos do usuário atual Olá instalação de toocomplete essas máquinas virtuais:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. No diretório de documentos hello, inicie o arquivo RDP de saudação. Conecte-se com o nome de usuário de administrador hello e a senha fornecidos anteriormente (por exemplo, se seu nome de usuário foi VMAdmin, especifique "\VMAdmin" como usuário hello e fornecer a senha de saudação).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configuração de saudação completa de saudação máquina do SQL Server para acesso remoto

Depois de fazer logon na máquina toohello com área de trabalho remota, configurar o SQL Server com base nas instruções de saudação em [etapas para configurar a conectividade do SQL Server em uma VM do Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Próximas etapas

Você pode encontrar instruções adicionais para o provisionamento de máquinas virtuais com o PowerShell Olá [documentação de máquinas virtuais](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Em muitos casos, a saudação próxima etapa é toomigrate toothis seus bancos de dados nova VM do SQL Server. Para obter diretrizes de migração do banco de dados, consulte [migrando um banco de dados tooSQL Server em uma VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Se você também está interessado em usar Olá toocreate portal do Azure máquinas virtuais do SQL, consulte [provisionar uma máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Observe que esse tutorial Olá que aborda a que você por meio do portal Olá cria VMs usando Olá modelo recomendado do Gerenciador de recursos, em vez de um modelo clássico Olá usado neste tópico do PowerShell.

Além de recursos de toothese, é recomendável que você examine [outros tópicos relacionados toorunning do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
