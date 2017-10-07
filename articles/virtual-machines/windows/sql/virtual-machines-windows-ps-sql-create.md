---
title: "aaaCreate uma máquina Virtual do SQL Server no Azure PowerShell (Gerenciador de recursos) | Microsoft Docs"
description: "Fornece etapas e scripts do PowerShell para criar uma VM do Azure com imagens da galeria de máquinas virtuais do SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Provisionar uma máquina virtual SQL Server usando o Azure PowerShell (Gerenciador de Recursos)
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Visão geral
Este tutorial mostra como toocreate uma única máquina virtual do Azure usando Olá **do Azure Resource Manager** modelo de implantação usando cmdlets do PowerShell do Azure. Neste tutorial, vamos criar uma única máquina virtual usando uma única unidade de disco de uma imagem em Olá Galeria de SQL. Vamos criar novos provedores de saudação armazenamento, rede e recursos de computação que serão usados pela máquina virtual de saudação. Se você tiver provedores existentes para qualquer um desses recursos, poderá usar tais provedores.

Se você precisa hello versão clássica deste tópico, consulte [provisionar uma máquina virtual do SQL Server usando o Azure PowerShell clássico](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Pré-requisitos
Para este tutorial, será necessário:

* Uma conta do Azure e uma assinatura antes de começar. Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview), versão mínima do 1.4.0 ou posterior (este tutorial foi escrito usando a versão 1.5.0).
  * tooretrieve sua versão, o tipo **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configurar sua assinatura
Abra o Windows PowerShell e estabelecer acesso tooyour conta do Azure executando Olá cmdlet a seguir. Você verá uma tela tooenter entrar suas credenciais. Use Olá mesmo email e a senha que você use toosign em toohello portal do Azure.

    Add-AzureRmAccount

Depois de entrar com êxito, você verá algumas informações na tela que inclui SubscriptionId Olá com a qual você entrou. Isso é assinatura Olá no qual serão criados recursos Olá para este tutorial, a menos que você alterar assinatura diferente tooa. Se você tiver vários SubscriptionIds, execute Olá tooreturn cmdlet a seguir uma lista de todos os seus SubscriptionIds:

    Get-AzureRmSubscription

tooanother toochange SubscriptionID, executar Olá cmdlet com o SubscriptionId desejado a seguir.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definir variáveis de imagem
toosimplify usabilidade e compreensão de script hello concluído deste tutorial, vamos começar com a definição de um número de variáveis. Alterar valores de parâmetro hello como achar mais conveniente, mas lembre-se de nomenclatura comprimentos de tooname relacionados restrições e caracteres especiais ao modificar valores hello fornecidos.

### <a name="location-and-resource-group"></a>Local e Grupo de Recursos
Use duas variáveis toodefine Olá dados região e hello grupo de recursos no qual você irá criar hello outros recursos para a máquina virtual de saudação.

Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlets a seguir essas variáveis.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Propriedades de armazenamento
Use Olá variáveis toodefine Olá conta e hello tipo de armazenamento do toobe de armazenamento usada pela máquina virtual de saudação a seguir.

Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis. Observe que, neste exemplo estamos usando o [Armazenamento Premium](../../../storage/common/storage-premium-storage.md), que é recomendado para cargas de trabalho de produção. Para obter detalhes sobre essas diretrizes e outras recomendações, confira [Melhores práticas para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Propriedades da rede
Use Olá seguindo a interface de rede variáveis toodefine hello, método de alocação de TCP/IP hello, nome de rede virtual Olá, nome de sub-rede virtual hello, Olá intervalo de endereços IP para rede virtual hello, Olá intervalo de endereços IP de sub-rede hello e hello rótulo de nome de domínio público toobe usada pela rede Olá na máquina virtual de saudação.

Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Propriedades de máquina virtual
Saudação de uso após o nome da máquina virtual variáveis toodefine Olá, nome do computador hello, tamanho da máquina virtual hello e nome de disco do sistema operacional Olá para a máquina virtual de saudação.

Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Propriedades da imagem
Use Olá variáveis toodefine Olá imagem toouse para a máquina virtual de saudação a seguir. Neste exemplo, a imagem do SQL Server 2016 Enterprise Olá é usada.

Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Observe que você pode obter uma lista completa de ofertas de imagem do SQL Server com o comando Get-AzureRmVMImageOffer de saudação:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

E você pode ver Olá Skus disponíveis para uma oferta com o comando Get-AzureRmVMImageSku de saudação. Olá, comando a seguir mostra todos os Skus disponíveis para Olá **SQL2014SP1 WS2012R2** oferecem.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Com o modelo de implantação do Gerenciador de recursos de hello, o primeiro objeto do hello que você cria é grupo de recursos de saudação. Usaremos Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate cmdlet de um grupo de recursos do Azure e seus recursos com recursos de saudação grupo nome e local definido pelas variáveis de saudação inicializado anteriormente.

Execute Olá toocreate cmdlet a seguir em seu novo grupo de recursos.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
máquina virtual de saudação requer recursos de armazenamento de disco do sistema operacional hello e hello dados do SQL Server e os arquivos de log. Para simplificar, criaremos um único disco para ambos. Você pode anexar discos adicionais posteriormente usando Olá [Azure adicionar disco](/powershell/module/azure/add-azuredisk) cmdlet na ordem tooplace os dados do SQL Server e arquivos de log em discos dedicados. Usaremos Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate um armazenamento padrão da conta no seu novo grupo de recursos e com o nome de conta de armazenamento Olá, nome do Sku de armazenamento e local definido usando variáveis de saudação que você inicializado anteriormente.

Execute Olá toocreate cmdlet a seguir em sua nova conta de armazenamento.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Criar recursos da rede
máquina virtual de saudação requer um número de recursos de rede para conectividade de rede.

* Cada máquina virtual exige um rede virtual.
* Uma rede virtual deve ter pelo menos uma sub-rede definida.
* Uma interface de rede deve ser definida com um público ou um endereço IP privado.

### <a name="create-a-virtual-network-subnet-configuration"></a>Criar uma configuração de sub-rede da rede virtual
Vamos começar criando uma configuração de sub-rede para nossa rede virtual. Para nosso tutorial, vamos criar uma sub-rede padrão usando Olá [AzureRmVirtualNetworkSubnetConfig novo](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. Vamos criar nossa configuração de sub-rede da rede virtual com produtos de prefixo de nome e endereço de sub-rede Olá definido usando variáveis de saudação inicializado anteriormente.

> [!NOTE]
> Você pode definir propriedades adicionais de configuração de sub-rede da rede virtual de saudação usando esse cmdlet, mas que está além do escopo deste tutorial hello.
>
>

Execute Olá toocreate cmdlet a seguir em sua configuração de sub-rede virtual.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Criar uma rede virtual
Em seguida, vamos criar rede virtual usando Olá [AzureRmVirtualNetwork novo](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. Vamos criar rede virtual em seu novo grupo de recursos, com o nome hello, o local e o prefixo de endereço definido usando variáveis de saudação inicializado anteriormente e usando a configuração de sub-rede Olá definida na etapa anterior hello.

Execute Olá toocreate cmdlet a seguir em sua rede virtual.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Criar endereço IP público de saudação
Agora que temos de rede virtual definido, é preciso tooconfigure um endereço IP da máquina de virtual toohello conectividade. Para este tutorial, vamos criar um endereço IP público usando toosupport conectividade com a Internet de endereçamento de IP dinâmico. Usaremos Olá [AzureRmPublicIpAddress novo](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Olá endereço IP público no hello recurso grupo criado prevously e com o nome hello, local, método de alocação e rótulo de nome de domínio DNS definido usando Olá variáveis que inicializado anteriormente.

> [!NOTE]
> Você pode definir propriedades adicionais do endereço IP público hello usando esse cmdlet, mas que está além do escopo Olá deste tutorial inicial. Você também pode criar um endereço privado ou um endereço com um endereço estático, mas que também está além do escopo deste tutorial hello.
>
>

Execute Olá toocreate cmdlet a seguir em seu endereço IP público.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá
Agora estamos interface de rede do hello toocreate pronto nossa máquina virtual será usado. Usaremos Olá [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nossa interface de rede no grupo de recursos de saudação criado anteriormente e com o nome hello, local, sub-rede e o endereço IP público definido anteriormente.

Execute Olá toocreate cmdlet a seguir em sua interface de rede.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configurar um objeto da VM
Agora que temos os recursos de armazenamento e rede definidos, estamos prontos toodefine recursos de computação para a máquina virtual de saudação. Para nosso tutorial, nós será especificar o tamanho da máquina virtual hello e várias propriedades de sistema operacional, especifique a interface de rede de saudação que criamos anteriormente, definir armazenamento de blob e, em seguida, especifique o disco do sistema operacional Olá.

### <a name="create-hello-vm-object"></a>Criar objeto VM Olá
Vamos começar com a especificação de tamanho da máquina virtual hello. Para este tutorial, estamos especificando um DS13. Usaremos Olá [AzureRmVMConfig novo](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate um objeto de máquina de virtual configuráveis com nome hello e o tamanho definido usando variáveis de saudação inicializado anteriormente.

Execute Olá após o objeto de máquina virtual do cmdlet toocreate hello.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Criar um nome da credencial objeto toohold hello e uma senha para credenciais de administrador local Olá
Antes que podemos definir propriedades do sistema operacional Olá para a máquina virtual de hello, precisamos de toosupply Olá credenciais Olá conta de administrador local como uma cadeia de caracteres segura. tooaccomplish isso, usaremos Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Execute Olá cmdlet a seguir e, na janela de solicitação de credencial do hello Windows PowerShell, digite toouse de nome e senha Olá Olá conta de administrador local na máquina de virtual do Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Definir as propriedades de sistema operacional Olá para a máquina virtual de saudação
Agora, estamos propriedades do sistema operacional da máquina de virtual Olá tooset pronto. Usaremos Olá [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset Olá tipo de sistema operacional como janelas, exigem Olá [agente da máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique que Olá habilita automaticamente atualizar e defina o nome da máquina virtual Olá, nome de computador hello e credencial hello usando variáveis de saudação inicializado anteriormente.

Execute Olá seguintes propriedades de sistema operacional do cmdlet tooset Olá para sua máquina virtual.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Adicionar a máquina virtual do hello rede interface toohello
Em seguida, adicionaremos a interface de rede de saudação que criamos anteriormente toohello VM. Usaremos Olá [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interface de rede do cmdlet tooadd hello usando a variável de interface de rede Olá definido anteriormente.

Execute Olá interface de rede do cmdlet tooset Olá para sua máquina virtual a seguir.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Defina o local de armazenamento de blob Olá para Olá disco toobe usada pela máquina virtual de saudação
Em seguida, vamos definir local de armazenamento de blob Olá para Olá disco toobe usada pela máquina virtual de saudação usando variáveis de saudação definido anteriormente.

Execute Olá local de armazenamento de blob do cmdlet tooset Olá a seguir.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Definir propriedades de disco da máquina virtual de saudação de sistema de operacional de saudação
Em seguida, vamos definir sistema de operacional Olá propriedades do disco da máquina virtual de saudação. Usaremos Olá [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet que Olá o sistema operacional da máquina virtual de saudação será proveniente de uma imagem, tooset tooread apenas de cache (porque o SQL Server está sendo instalado na Olá mesmo disco) e definir nome da máquina virtual Hello e o disco do sistema operacional Olá definido usando variáveis de saudação que definimos anteriormente.

Execute Olá seguintes propriedades de disco do sistema operacional do cmdlet tooset Olá para sua máquina virtual.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Especifique a imagem da plataforma Olá para a máquina virtual de saudação
Nossa última etapa de configuração é a imagem da plataforma toospecify Olá para nossa máquina virtual. Para nosso tutorial, estamos usando imagem do SQL Server 2016 CTP mais recente hello. Usaremos Olá [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse essa imagem conforme definido pelas variáveis Olá definido anteriormente.

Execute Olá imagem da plataforma do cmdlet toospecify Olá para sua máquina virtual a seguir.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Criar hello VM do SQL
Agora que você concluiu as etapas de configuração hello, você está pronto toocreate Olá VM. Usaremos Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Olá VM usando variáveis de saudação que definimos.

Execute Olá toocreate cmdlet a seguir em sua máquina virtual.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

máquina virtual de saudação é criada. Observe que uma conta de armazenamento padrão é criada para o diagnóstico de inicialização porque Olá especificado a conta de armazenamento para Olá disco de máquina virtual é uma conta de armazenamento premium.

Agora você pode exibir esta máquina no hello Azure Portal toosee [seu endereço IP público e seu nome de domínio totalmente qualificado](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Script de exemplo
Olá script a seguir contém Olá completa script do PowerShell para este tutorial. Ele pressupõe que você já tenha instalação Olá assinatura do Azure toouse com hello **adicionar AzureRmAccount** e **AzureRmSubscription selecione** comandos.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Próximas etapas
Após a criação de máquina virtual de saudação, você está pronto tooconnect toohello VM usando o RDP e configuração de conectividade. Para obter mais informações, consulte [conectar tooa Máquina Virtual do SQL Server no Azure (Gerenciador de recursos)](virtual-machines-windows-sql-connect.md).

