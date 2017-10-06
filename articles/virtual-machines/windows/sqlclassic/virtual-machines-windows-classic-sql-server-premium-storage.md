---
title: aaaUse armazenamento Premium do Azure com o SQL Server | Microsoft Docs
description: "Este artigo usa recursos criados com o modelo de implantação clássico hello e fornece orientação sobre como usar o armazenamento Premium do Azure com o SQL Server em execução em máquinas virtuais do Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Usar o Armazenamento Premium do Azure com o SQL Server em máquinas virtuais
## <a name="overview"></a>Visão geral
[Armazenamento Premium do Azure](../../../storage/common/storage-premium-storage.md) Olá a próxima geração de armazenamento que proporciona baixa latência e alta taxa de transferência e/s. Ele funciona melhor para cargas de trabalho de uso intensivo de E/S de chave, como [Máquinas Virtuais](https://azure.microsoft.com/services/virtual-machines/)do SQL Server no IaaS.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Este artigo fornece planejamento e instruções sobre como migrar uma máquina Virtual que executa o SQL Server toouse armazenamento Premium. Isso inclui a infraestrutura do Azure (rede, armazenamento) e as etapas de VM do Windows de convidado. exemplo Hello Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) mostra uma migração completa abrangente final tooend como toomove maior VMs tootake aproveitar melhor local armazenamento SSD com o PowerShell.

É importante toounderstand Olá ponta a ponta processo utilizando armazenamento do Premium do Azure com o SQL Server em VMs de IAAS. Isso inclui:

* Identificação da saudação pré-requisitos toouse armazenamento Premium.
* Exemplos de implantação do SQL Server no IaaS tooPremium armazenamento para novas implantações.
* Exemplos de migração de implantações existentes, de servidores autônomos e implantações usando grupos de disponibilidade SQL AlwaysOn.
* Abordagens de migração possíveis.
* Exemplo completo de ponta a ponta, mostrando as etapas do Azure, Windows e SQL Server para a migração de saudação de uma implementação existente do AlwaysOn.

Para obter informações gerais sobre o SQL Server nas Máquinas Virtuais do Azure, consulte [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Autor:** Daniel Sol **Revisores Técnicos:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Pré-requisitos para o Armazenamento Premium
Existem vários pré-requisitos para o uso do Armazenamento Premium.

### <a name="machine-size"></a>Tamanho do computador
Para usar o armazenamento Premium, você precisará toouse DS série máquinas virtuais (VM). Se você não usou máquinas da série DS no seu serviço de nuvem antes, exclua Olá existente VM, mantenha os discos Olá anexado e, em seguida, criar um novo serviço de nuvem antes de recriar Olá VM como tamanho de função DS *. Para saber mais sobre os tamanhos das Máquinas Virtuais, consulte [Tamanhos da Máquina Virtual e do Serviço de Nuvem do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Serviços de Nuvem
Você só poderá usar VMs DS* com Armazenamento Premium quando elas forem criadas em um novo serviço de nuvem. Se você estiver usando o SQL Server Always On no Azure, Olá sempre ouvinte fará referência toohello endereço interno do Azure ou de IP externo de Balanceador de carga que está associado um serviço de nuvem. Este artigo se concentra em como toomigrate mantendo a disponibilidade nesse cenário.

> [!NOTE]
> Uma série DS * deve ser Olá primeira VM é implantada toohello novo serviço de nuvem.
>
>

### <a name="regional-vnets"></a>VNETS regionais
Para VMs DS *, você deve configurar Olá rede Virtual (VNET) hospeda seu toobe VMs regional. Este hello "amplia" VNET é tooallow Olá maior VMs toobe provisionado em outros clusters e permitir a comunicação entre eles. Olá captura de tela a seguir, hello local realçado mostra VNETs regionais, enquanto o primeiro resultado de saudação mostra uma rede virtual "restrito".

![RegionalVNET][1]

Você pode gerar um tooa de toomigrate do tíquete de suporte Microsoft VNET regional, Microsoft fará uma alteração, então toocomplete Olá migração tooregional VNETs, altere a propriedade de Olá AffinityGroup na configuração de rede de saudação. Exportar primeiro Olá configuração de rede no PowerShell e substitua Olá **AffinityGroup** propriedade Olá **VirtualNetworkSite** elemento com um **local** propriedade. Especifique `Location = XXXX` onde `XXXX` é uma região do Azure. Importe configuração nova hello.

Por exemplo, considerando Olá configuração da rede virtual a seguir:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove este tooa VNET regional na Europa Ocidental, alterar Olá toohello de configuração a seguir:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Contas de armazenamento
Você precisará toocreate uma nova conta de armazenamento que está configurada para o armazenamento Premium. Observe que o uso de saudação do armazenamento Premium é definido na conta de armazenamento hello, não em VHDs individuais, no entanto, ao usar uma VM série DS * você pode anexar do VHD de contas de armazenamento padrão e Premium. Você pode considerar isso se você não quiser tooplace Olá VHD do sistema operacional em toohello conta de armazenamento Premium.

a seguir Olá **New-AzureStorageAccountPowerShell** com hello "Premium_LRS" **tipo** cria uma conta de armazenamento Premium:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Configurações de Cache de VHDs
Olá principal diferença entre a criação de discos que fazem parte de uma conta de armazenamento Premium é configuração de cache de disco de saudação. Para discos do volume SQL Server Data, recomendamos que você use ‘**Caching de Leitura**’. Para volumes de log de transações, configuração de cache de disco de saudação deve ser definida muito '**nenhum**'. Isso é diferente das recomendações Olá para contas de armazenamento padrão.

Depois que os VHDs Olá foram anexados, configuração de cache de saudação não pode ser alterada. Você precisa toodetach e reconecte Olá VHD com uma configuração de cache atualizado.

### <a name="windows-storage-spaces"></a>Espaços de armazenamento do Windows
Você pode usar [espaços de armazenamento do Windows](https://technet.microsoft.com/library/hh831739.aspx) como você fez com o armazenamento padrão anterior, isso permitirá que você toomigrate uma máquina virtual que já está usando espaços de armazenamento. exemplo Hello [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (etapa 9 e posteriores) demonstra Olá tooextract de código do Powershell e importar uma VM com vários VHDs anexados.

Pools de armazenamento foram usados com taxa de transferência tooenhance conta de armazenamento de Azure padrão e reduzem a latência. Talvez você ache interessante testar Pools de Armazenamento com o Armazenamento Premium para novas implantações, mas isso agrega uma complexidade adicional com a configuração do armazenamento.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Como toofind toostorage pools de mapear os discos virtuais do Azure
Como há recomendações de configuração de cache diferentes para VHDs anexados, você pode decidir toocopy Olá VHDs tooa conta de armazenamento Premium. No entanto, quando você reconectá-las toohello nova série DS VM, talvez seja necessário tooalter as configurações de cache de saudação. É mais simples Olá tooapply que armazenamento Premium recomendada as configurações de cache quando houver VHDs separados para Olá de dados do SQL arquivos e log arquivos (em vez de um único VHD que contém ambos).

> [!NOTE]
> Se você tiver arquivos de log e de dados do SQL Server no mesmo volume, Olá cache opção que você escolher depende de padrões de acesso de e/s de saudação para suas cargas de trabalho do banco de dados de saudação. Apenas o teste pode demonstrar qual opção de cache é ideal para esse cenário.
>
>

No entanto, se você estiver usando espaços de armazenamento do Windows que são compostos de vários VHDs, você precisará toolook no seu tooidentify scripts originais que VHDs anexos são em qual pool específico, então você pode definir as configurações de cache Olá adequadamente para cada disco.

Se você não tiver original tooshow disponíveis do script qual mapeiam VHDs toohello pool de armazenamento, você pode usar o hello mapeamento de pool de armazenamento em disco/etapas toodetermine Olá a seguir.

Para cada disco, use Olá etapas a seguir:

1. Obter uma lista de discos anexados tooVM com hello **Get-AzureVM** comando:

    Get-AzureVM -ServiceName <servicename> -Nome <vmname> | Get-AzureDataDisk
2. Observe hello Diskname e LUN.

    ![DisknameAndLUN][2]
3. Área de trabalho remota Olá VM. Em seguida, acesse muito**gerenciamento do computador** | **Gerenciador de dispositivos** | **unidades de disco**. Examinar as propriedades de saudação de cada Olá 'Microsoft discos virtuais'

    ![VirtualDiskProperties][3]
4. número LUN Olá aqui é um número LUN de toohello referência que você especificar ao anexar o VHD de saudação toohello VM.
5. Para Olá 'Microsoft Virtual Disk' go toohello **detalhes** guia e, em seguida, na Olá **propriedade** lista, vá muito**chave Driver**. Em Olá **valor**, Olá Observação **deslocamento**, que é 0002 em Olá captura de tela a seguir. Olá 0002 denota hello PhysicalDisk2 Olá referências de pool de armazenamento.

    ![VirtualDiskPropertyDetails][4]
6. Para cada pool de armazenamento, o despejo de saudação associado discos:

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Agora você pode usar este tooassociate informações anexado VHDs tooPhysical discos em Pools de armazenamento.

Depois que você mapeou VHDs tooPhysical discos em Pools de armazenamento, em seguida, você pode desanexar e copiá-los em tooa conta de armazenamento Premium, em seguida, anexá-los com configuração de cache correto hello. Consulte o exemplo hello em hello [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), as etapas de 8 a 12. Estas etapas mostram como tooextract um VHD anexado VMs disco tooa CSV arquivo de configuração copiar VHDs hello, alterar configurações de cache de configuração de disco hello e finalmente reimplantar Olá VM como conectado de uma VM da série DS com hello todos os discos.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Largura de banda de armazenamento de VM e taxa de transferência de armazenamento de VHD
saudação de desempenho de armazenamento depende Olá tamanho de DS * VM especificado e Olá tamanhos VHD. Olá VMs tem permissões diferentes para o número de saudação de VHDs que podem ser anexados e Olá largura de banda máxima (MB/s) será oferecido suporte. Para números de largura de banda específica hello, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Mais IOPS são obtidos com tamanhos de disco maiores. Considere isso quando você pensar em seu caminho de migração. Para obter detalhes, [consulte tabela Olá para tipos de disco de IOPS e](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Por fim, considere que as VMs têm larguras de banda máxima de disco diferentes que aceitarão para todos os discos anexados. Sob alta carga, você pode saturar Olá disco máxima largura de banda disponível para esse tamanho de função VM. Por exemplo um Standard_DS14 dará suporte a too512MB/s. Portanto, com três discos P30 você poderia saturar a largura de banda de disco de saudação do hello VM. Mas, neste exemplo, o limite de taxa de transferência Olá poderá ser excedido dependendo da combinação de saudação de leitura e gravação de IOs.

## <a name="new-deployments"></a>Novas implantações
duas seções seguintes Olá demonstram como você pode implantar VMs do SQL Server tooPremium armazenamento. Como mencionado anteriormente, não é necessariamente necessário disco do sistema operacional Olá tooplace em armazenamento Premium. Você pode escolher toodo isso se você estiver pretendendo tooplace qualquer cargas de trabalho intensivas de e/s em Olá VHD do sistema operacional.

Olá primeiro exemplo demonstra o uso de imagens da galeria existente do Azure. Olá segundo exemplo mostra como toouse uma VM personalizada da imagem que você tem em uma conta de armazenamento padrão existente.

> [!NOTE]
> Esses exemplos pressupõem que você já tenha criou um VNET regional.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Criar uma nova VM com Armazenamento Premium com Imagem da Galeria
exemplo Hello abaixo mostra como tooplace Olá VHD do sistema operacional para o armazenamento premium e anexar VHDs de armazenamento Premium. No entanto, você pode também colocar o disco do sistema operacional Olá em uma conta de armazenamento padrão e, em seguida, anexar VHDs que residem em uma conta de armazenamento Premium. Ambos os cenários são demonstrados.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Etapa 1: criar uma conta de Armazenamento Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Etapa 2: criar um novo serviço de nuvem
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Etapa 3: reservar um VIP de serviço de nuvem (opcional)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Etapa 4: criar um contêiner de VM
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Etapa 5: colocar o VHD do sistema operacional no armazenamento Padrão ou Premium
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Etapa 6: criar uma VM
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Criar um novo toouse VM armazenamento Premium com uma imagem personalizada
Este cenário demonstra onde você tem imagens personalizadas existentes que residem em uma conta de Armazenamento Padrão. Conforme mencionado se você quiser tooplace Olá VHD do sistema operacional no armazenamento Premium que você precisará toocopy Olá imagem que existe na conta de armazenamento padrão de saudação e transferi-las tooa armazenamento Premium antes de ser usada. Se você tiver uma imagem no local, você pode também usar esse método toocopy diretamente toohello conta de armazenamento Premium.

#### <a name="step-1-create-storage-account"></a>Etapa 1: criar conta de armazenamento
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Etapa 2: criar serviço de nuvem
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Etapa 3: Usar a imagem existente
Você pode usar uma imagem existente. Ou você também pode [capturar uma imagem de uma máquina existente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Máquina de saudação Observação que você a imagem não tem toobe DS * máquina. Uma vez que a imagem de hello, Olá mostram as etapas a seguir como toocopy-toohello conta de armazenamento Premium Olá **AzureStorageBlobCopy início** commandlet PowerShell.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Etapa 4: copiar o Blob entre contas de armazenamento
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Etapa 5: verificar regularmente o status da cópia:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Etapa 6: Adicionar tooAzure de disco imagem repositório na assinatura
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Você pode achar que, embora os relatórios de status de saudação como êxito, você pode obter um erro de concessão de disco. Nesse caso, espere cerca de 10 minutos.
>
>

#### <a name="step-7--build-hello-vm"></a>Etapa 7: Criar hello VM
Aqui, você está criando Olá VM de sua imagem e anexar dois VHDs de armazenamento Premium:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Implantações existentes que não usam grupos de disponibilidade AlwaysOn
> [!NOTE]
> Para as implantações existentes, consulte primeiro Olá [pré-requisitos](#prerequisites-for-premium-storage) seção deste tópico.
>
>

Há considerações diferentes para implantações do SQL Server que não usam grupos de disponibilidade AlwaysOn e aquelas que usam. Se você não estiver usando o AlwaysOn e tiver um autônomo existente do SQL Server, você pode atualizar tooPremium armazenamento usando uma nova conta de armazenamento e serviços de nuvem. Considere Olá as opções a seguir:

* **Criar uma nova VM do SQL Server**. Você pode criar uma nova VM do SQL Server que usa uma conta de Armazenamento Premium, conforme documentado em Novas implantações. Em seguida, faça uma operação de backup e restauração de seus bancos de dados de configuração e usuário do SQL Server. Olá aplicativo precisará toobe atualizado tooreference Olá novo SQL Server se ele estiver sendo acessado interna ou externamente. Você precisaria toocopy todos os objetos 'fora do banco de dados' como se fosse uma migração do lado a lado (SxS) SQL Server. Isso inclui objetos como logons, certificados e servidores vinculados.
* **Migrar uma VM existente do SQL Server**. Isso exigirá colocar offline o hello VM do SQL Server e, em seguida, transferi-lo tooa novo serviço de nuvem, que inclui a cópia de todos os seu toohello de VHDs anexado conta de armazenamento Premium. Quando Olá VM fica online, aplicativo hello fará referência a nome de host de servidor hello como antes. Lembre-se de que o tamanho Olá de disco existente Olá afetará características de desempenho de saudação. Por exemplo, um disco de 400 GB obtém arredondado tooa P20. Se você souber que você não precisa que o desempenho do disco, você pode recriar Olá VM como uma VM da série DS e anexar VHDs de armazenamento Premium da especificação de tamanho e desempenho Olá que precisar. Em seguida, você pode desanexar e anexar novamente os arquivos de banco de dados SQL Olá.

> [!NOTE]
> Ao copiar os discos VHD de saudação, você deve estar ciente do tamanho hello, dependendo do tamanho da saudação significa que o tipo de disco de armazenamento Premium eles se encaixam, isso determina a especificação de desempenho de disco. Tamanho do Azure será arredondado backup toohello mais próximo do disco, para que se você tiver um disco de 400 GB, isso será arredondado tooa P20. Dependendo dos requisitos de e/s existentes de saudação VHD do sistema operacional, talvez não seja necessário toomigrate este tooa conta de armazenamento Premium.
>
>

Se o SQL Server for acessado externamente, Olá VIP de serviço de nuvem será alterado. Você também terá DNS, as ACLs e pontos de extremidade tooupdate configurações.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Implantações existentes que usam grupos de disponibilidade AlwaysOn
> [!NOTE]
> Para as implantações existentes, consulte primeiro Olá [pré-requisitos](#prerequisites-for-premium-storage) seção deste tópico.
>
>

No início desta seção, vamos examinar como o AlwaysOn interage com a Rede do Azure. Em seguida, dividiremos migrações em cenários de tootwo: migrações onde algum tempo de inatividade pode ser tolerado e migrações onde você deve obter o tempo de inatividade mínimo.

Os grupos de disponibilidade AlwaysOn locais do SQL Server usam um Ouvinte local que registra um nome DNS virtual junto com um endereço IP que é compartilhado entre um ou mais SQL Servers. Quando os clientes se conectam sejam roteadas por meio de saudação ouvinte IP toohello principal do SQL Server. Este é o servidor de saudação que possui Olá recurso sempre IP nesse momento.

![DeploymentsUseAlways On][6]

No Microsoft Azure, você pode ter tooa de endereço atribuído apenas um IP NIC em Olá VM, na ordem tooachieve Olá mesma camada de abstração, como local, Azure utiliza o endereço IP de saudação que é atribuído a balanceadores de carga interno ou externo toohello ILB/ELB (). o recurso IP Hello que é compartilhado entre servidores hello está definido toohello mesmo IP como Olá ILB/ELB. Isso é publicado no hello DNS, e o tráfego do cliente é passado por meio de réplica do hello ILB/ELB toohello SQL Server primário. Olá ILB/ELB sabe a qual o SQL Server é primário desde que ele usa testes tooprobe Olá sempre IP recursos. No exemplo anterior de saudação, sondas de cada nó que possui um ponto de extremidade referenciado por Olá ELB/ILB, aquele que responde é Olá principal do SQL Server.

> [!NOTE]
> Olá ILB e ELB forem atribuídos tooa serviço de nuvem do Azure específica, portanto qualquer migração para a nuvem no Azure provavelmente significa que Olá que IP do balanceador de carga será alterado.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migrando implantações AlwaysOn que podem permitir algum tempo de inatividade
Há duas estratégias toomigrate sempre em implantações que permitem a algum tempo de inatividade:

1. **Adicionar mais tooan réplicas secundárias existentes sempre em Cluster**
2. **Migrar tooa sempre no Cluster novo**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Adicionar mais tooan de réplicas secundárias existentes sempre Cluster
Uma estratégia é tooadd mais secundários toohello grupo de disponibilidade AlwaysOn. Você precisa tooadd em um novo serviço de nuvem e atualize o ouvinte Olá com hello novo IP do balanceador de carga.

##### <a name="points-of-downtime"></a>Pontos de tempo de inatividade:
* Validação de cluster.
* Testando failovers AlwaysOn para secundárias novas.

Se você estiver usando Pools de armazenamento do Windows em Olá VM para maior taxa de transferência de e/s, em seguida, eles serão colocados offline durante uma validação completa de Cluster. é necessário um teste de validação de Hello quando você adicionar nós toohello cluster. Olá tempo toorun teste de saudação pode variar, você deve testar isso em seu tooget do ambiente de teste representativo uma hora aproximada de quanto tempo isso leva.

Você deve provisionar o tempo em que você pode executar o failover manual e caos testes em Olá recentemente adicionado nós tooensure sempre em funções de alta disponibilidade, conforme o esperado.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Você deve interromper todas as instâncias do SQL Server onde Olá Pools de armazenamento são usados antes hello validação é executada.
>
> ##### <a name="high-level-steps"></a>Etapas de alto nível
>

1. Crie dois novos SQL Servers no novo serviço de nuvem com Armazenamento Premium anexado.
2. Copie sobre backups e restauração completos com **NORECOVERY**.
3. Copie sobre objetos dependentes de ‘banco de dados fora do usuário’, como logons etc.
4. Crie um novo ILB (balanceador de carga interno) ou use um ELB (balanceador de carga externo) e configure pontos de extremidade balanceados de carga em ambos os nós novos.

   > [!NOTE]
   > Verificar que todos os nós têm a configuração de ponto de extremidade correto Olá antes de continuar
   >
   >
5. Pare toohello de acesso de usuário e de aplicativo do SQL Server (se estiver usando Pools de armazenamento).
6. Interrompa serviços de mecanismo do SQL Server em todos os nós (se você estiver usando pools de armazenamento).
7. Adicionar novo toocluster de nós e execute a validação completa.
8. Depois que a validação for bem-sucedida, inicie todos os Serviços do SQL Server.
9. Faça backup dos logs de transações e restaure os bancos de dados do usuário.
10. Adicione novos nós Olá grupo de disponibilidade AlwaysOn e colocar a replicação em **síncrona**.
11. Adicionar IP hello recurso de endereço de saudação serviço de nuvem novo ILB/ELB por meio do PowerShell do AlwaysOn com base no exemplo de multissite Olá Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). No cluster do Windows, defina Olá **possíveis proprietários** de saudação **endereço IP** recurso toohello novos nós antigos. Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Tooone de failover de nós de novo hello.
13. Faça Olá novos nós parceiros de Failover automático e failovers de teste.
14. Remova os nós originais do grupo de disponibilidade.

##### <a name="advantages"></a>Vantagens
* Novos servidores SQL pode ser testado (SQL Server e aplicativo) antes de serem adicionados tooAlways em.
* Você pode alterar o tamanho da VM hello e personalizar os requisitos exatos do hello armazenamento tooyour. No entanto, seria útil tookeep todos os caminhos de arquivo SQL Olá Olá mesmo.
* Você pode controlar quando a transferência de saudação do toohello de backups de banco de dados de saudação réplicas secundárias são iniciados. Isso é diferente de usar o Azure **AzureStorageBlobCopy início** toocopy commandlet VHDs, pois é uma cópia assíncrona.

##### <a name="disadvantages"></a>Desvantagens
* Ao usar Pools de armazenamento do Windows, há um tempo de inatividade do Cluster durante a saudação validação completa de Cluster para nós adicionais do novo hello.
* Dependendo Olá versão do SQL Server e do número de existente Olá das réplicas secundárias, você pode não ser capaz de tooadd mais réplicas secundárias sem remover secundários existentes.
* Pode haver muito tempo de transferência de dados SQL durante a configuração secundários hello.
* Há custos adicionais durante a migração quando há novas máquinas em execução em paralelo.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Migrar tooa sempre no Cluster novo
Outra estratégia é toocreate uma nova sempre em Cluster conosco de novos no novo serviço de nuvem e, em seguida, redirecione Olá clientes toouse-lo.

##### <a name="points-of-downtime"></a>Pontos de tempo de inatividade
Não há tempo de inatividade durante a transferência de aplicativos e usuários toohello novo sempre no ouvinte. tempo de inatividade Olá depende:

* Olá tempo toorestore toodatabases de backups de log de transações final em novos servidores.
* Olá tempo tooupdate cliente aplicativos toouse novo sempre no ouvinte.

##### <a name="advantages"></a>Vantagens
* Você pode testar o ambiente de produção real hello, SQL Server, e alterações de build do sistema operacional.
* Você tem o armazenamento de Olá Olá opção toocustomize e toopotentially reduzir o tamanho da VM. Isso pode resultar na redução de custos.
* Você pode atualizar sua compilação ou versão do SQL Server durante esse processo. Você também pode atualizar o sistema operacional de saudação.
* Olá que anterior sempre Cluster pode agir como um destino de reversão sólido.

##### <a name="disadvantages"></a>Desvantagens
* Se você quiser que ambos os clusters sempre em execução simultaneamente, é necessário toochange nome DNS de saudação do ouvinte de saudação. Isso adiciona administração sobrecarga durante a migração de saudação como cadeias de caracteres de aplicativo cliente devem refletir o novo nome de ouvinte hello.
* Você deve implementar um mecanismo de sincronização entre Olá dois ambientes tookeep-los como fechar como requisitos de sincronização final Olá toominimize possíveis antes da migração.
* Há adicionada custo durante a migração enquanto você tem o novo ambiente de saudação em execução.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migrando implantações AlwaysOn para tempo de inatividade mínimo
Existem duas estratégias para migrar implantações AlwaysOn para o tempo de inatividade mínimo:

1. **Utilizar uma réplica secundária existente: site único**
2. **Utilizar réplicas secundárias existentes: vários sites**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Utilizar uma réplica secundária existente: site único
Uma estratégia para o tempo de inatividade mínimo é tootake uma nuvem existente secundária e removê-lo Olá atual do serviço de nuvem. Copie Olá VHDs toohello nova conta de armazenamento Premium e crie Olá VM no novo serviço de nuvem hello. Em seguida, atualize o ouvinte Olá em cluster e o failover.

##### <a name="points-of-downtime"></a>Pontos de tempo de inatividade
* Não há tempo de inatividade quando você atualiza o nó final Olá com ponto de extremidade com balanceamento de carga do hello.
* A reconexão do cliente pode ser atrasada dependendo da configuração do cliente/DNS.
* Não há tempo de inatividade adicional se você escolher o grupo tootake Olá sempre Cluster offline tooswap endereços de IP hello. Você pode evitar isso usando uma dependência ou e proprietários possíveis para Olá adicionou o recurso de endereço IP. Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Quando você quiser Olá toopartake nó adicionado no como um sempre no parceiro de Failover, você precisa tooadd um ponto de extremidade do Azure com um toohello de referência de carga balanceada definido. Quando você executa Olá **Add-AzureEndpoint** comando toodo, tooremain atual de conexões aberta, mas o novo ouvinte de toohello conexões não será capaz de toobe estabelecido balanceador de carga Olá foi atualizado. No teste foi visto toolast 90-120seconds, isso deve ser testado.
>
>

##### <a name="advantages"></a>Vantagens
* Sem custo extra incorrido durante a migração.
* Uma migração um-para-um.
* Redução da complexidade.
* Permite maior IOPS de SKUs de Armazenamento Premium. Quando parte de um 3º Olá discos são desanexados de saudação VM e copiados toohello novo serviço de nuvem, a ferramenta pode ser usado tooincrease Olá tamanho do VHD, que fornece a taxas de transferência mais altas. Para tamanhos de VHD maiores, consulte este [fórum de discussão](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Desvantagens
* Há uma perda temporária de alta disponibilidade e recuperação de desastre durante a migração.
* Como esta é uma migração 1:1, você terá toouse um tamanho de VM mínimo que oferecerá suporte ao seu número de VHDs, portanto você pode não ser capaz de toodownsize suas VMs.
* Esse cenário usa hello Azure **AzureStorageBlobCopy início** commandlet, que é assíncrona. Não há nenhum SLA na conclusão da cópia. tempo de saudação de cópias de saudação varia, enquanto isso depende de espera em fila também depende de quantidade de saudação do tootransfer de dados. tempo de cópia de saudação aumenta se a transferência de saudação for tooanother data center do Azure que dá suporte ao armazenamento Premium em outra região. Se você tiver apenas 2 nós, considere uma possível redução no caso de cópia Olá demora mais do que no teste. Isso pode incluir Olá ideias a seguir.
  * Adicione um nó do SQL Server 3º temporário para HA antes da migração de saudação com tempo de inatividade acordada.
  * Execute a migração Olá fora do Azure manutenção agendada.
  * Verifique se você configurou corretamente o quorum do cluster.  

##### <a name="high-level-steps"></a>Etapas de alto nível
Este documento demonstra um exemplo de tooend final completa, porém Olá [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fornece detalhes que podem ser utilizado tooperform isso.

![MinimalDowntime][8]

* Obter configuração de disco e remover nó de saudação (não excluir VHDs anexados).
* Crie uma conta de armazenamento Premium e copiar VHDs de saudação conta de armazenamento padrão
* Criar novo serviço de nuvem e reimplantar Olá VM SQL2 no serviço em nuvem. Criar hello VM usar Olá copiados VHD original do sistema operacional e anexar Olá copiados VHDs.
* Configure o ILB / ELB e adicione pontos de extremidade.
* Siga um destes procedimentos para atualizar o ouvinte:
  * Levando Olá sempre grupo off-line e atualização Olá sempre no ouvinte com o novo ILB / endereço IP ELB.
  * Ou adicionar o recurso de endereço IP hello da nova nuvem serviço ILB/ELB por meio do PowerShell para clusters do Windows. Em seguida, conjunto Olá possíveis proprietários de saudação toohello de recurso de endereço IP migrados nó, SQL2 e defini-lo como dependência OR em Olá nome de rede. Consulte a seção 'Adicionar recurso de endereço IP na mesma sub-rede' hello de saudação [apêndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Verifique se os clientes toohello de configuração/propagação DNS.
* Migre a VM do SQL1 e siga as etapas 2 a 4.
* Se usar as etapas 5ii, em seguida, adicione SQL1 como um possível proprietário de saudação adicionado o recurso de endereço IP
* Failovers de teste.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Utilizar réplicas secundárias existentes: vários sites
Se você tiver nós em mais de um datacenter do Azure (controlador de domínio) ou se você tiver um ambiente híbrido, você pode usar uma configuração de AlwaysOn esse tempo de inatividade do ambiente toominimize.

abordagem de saudação é toochange Olá sempre em sincronização tooSynchronous para Olá local ou controlador de domínio secundário do Azure e failover toothat do SQL Server. Copie Olá VHDs tooa conta de armazenamento Premium e reimplantar a máquina de saudação em um novo serviço de nuvem. Atualize o ouvinte hello e, em seguida, execute o failback.

##### <a name="points-of-downtime"></a>Pontos de tempo de inatividade
tempo de inatividade Olá consiste em toofailover toohello alternativa DC do hello tempo e vice-versa. Também depende da sua configuração cliente/DNS e a reconexão do cliente poder ser atrasada.
Considere Olá seguinte exemplo de uma configuração híbrida AlwaysOn:

![MultiSite1][9]

##### <a name="advantages"></a>Vantagens
* Você pode utilizar a infraestrutura existente.
* Você tem Olá toopre a atualização da opção Olá armazenamento do Azure em hello Azure DR DC primeiro.
* saudação de armazenamento do Azure DR DC pode ser reconfigurada.
* Há um mínimo de dois failovers durante a migração, excluindo failovers de teste.
* Você não precisa de dados do SQL Server toomove com backup e restauração.

##### <a name="disadvantages"></a>Desvantagens
* Dependendo tooSQL de acesso de cliente servidor, pode haver latência aumentada quando o SQL Server está em execução em um aplicativo de toohello do controlador de domínio alternativo.
* tempo de cópia de saudação de VHDs tooPremium armazenamento pode ser longo. Isso pode afetar sua decisão sobre se tookeep Olá Olá grupo de disponibilidade do nó. Considere o seguinte para quando o trabalho intensivas de log cargas estão em execução durante a migração de saudação é necessário, desde que o nó primário Olá terá tookeep Olá transações não replicadas no log de transações. Portanto, isso pode crescer significativamente.
* Esse cenário usa hello Azure **AzureStorageBlobCopy início** commandlet, que é assíncrona. Não há nenhum SLA a concluir. Olá tempo de saudação cópias varia, enquanto isso depende de espera na fila, também depende de quantidade de saudação do tootransfer de dados. Portanto você tiver apenas um nó em seu data center 2, você deve executar etapas de mitigação no caso de cópia Olá demora mais do que no teste. Isso pode incluir Olá ideias a seguir.
  * Adicione um nó SQL 2º temporário para HA antes da migração de saudação com tempo de inatividade acordada.
  * Execute a migração Olá fora do Azure manutenção agendada.
  * Verifique se você configurou corretamente o quorum do cluster.

Este cenário pressupõe que você deixe de documentar a instalação e sabe como armazenamento Olá é mapeado em ordem toomake será alterado para configurações de cache ideais.

##### <a name="high-level-steps"></a>Etapas de alto nível
![Multisite2][10]

* Tornar Olá local / alternativa saudação do controlador de domínio do Azure SQL Server primário e torná-lo Olá outros parceiro de Failover automático (AFP).
* Coletar informações de configuração de disco do SQL2 e remover nó de saudação (não excluir VHDs anexados).
* Crie uma conta de armazenamento Premium e copiar VHDs de saudação conta de armazenamento padrão.
* Criar um novo serviço de nuvem e crie Olá VM SQL2 com seus discos de armazenamento gratificações anexados.
* Configure o ILB / ELB e adicione pontos de extremidade.
* Saudação de atualização sempre no ouvinte com o novo ILB / failover de teste e o endereço IP ELB.
* Verifique a configuração de DNS hello.
* Alterar Olá AFP tooSQL2 e, em seguida, migrar SQL1 e percorrer as etapas 2 a 5.
* Failovers de teste.
* Alternar tooSQL1 back Olá AFP e SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Apêndice: Migrar um armazenamento de tooPremium de multissite sempre em Cluster
Olá restante este tópico fornece um exemplo detalhado de conversão de um armazenamento de multissite AlwaysOn cluster tooPremium. Ele também converte Olá ouvinte usa um balanceador de carga interno de tooan (ELB) do balanceador externo de carga (ILB).

### <a name="environment"></a>Ambiente
* Windows 2k12 / SQL 2k12
* 1 arquivo de banco de dados no SP
* 2 x pools de armazenamento por nó

![Appendix1][11]

### <a name="vm"></a>VM:
Neste exemplo, vamos toodemonstrate mover de um tooILB ELB. ELB estava disponível antes de ILB, então isso mostra como toothis tooswitch durante Olá migração.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>As etapas anteriores: Conectar tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Etapa 1: criar a nova conta de armazenamento e o serviço de nuvem
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Etapa 2: Saudação de aumento permitida falhas nos recursos<Optional>
Em determinados recursos que pertencem a tooyour grupo de disponibilidade AlwaysOn, há limites no quantas falhas que podem ocorrer em um período, em que o serviço de cluster Olá tentará toorestart grupo de recursos de saudação. É recomendável que aumentar esse enquanto são acompanhará neste procedimento, pois se você não manualmente failovers de failover e gatilho desligando máquinas você pode obter o limite de toothis fechar.

Ele seria ser limite de falha de Olá toodouble prudente, toodo isso no Gerenciador de Cluster de Failover, consulte Propriedades toohello Olá AlwaysOn do grupo de recursos:

![Appendix3][13]

Altere Olá too6 máximo de falhas.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Etapa 3: Adição do recurso de endereço IP ao grupo de clusters <Optional>
Se você tiver apenas um endereço IP para Olá grupo de clusters e isso é alinhado toohello nuvem sub-rede, lembre-se, se você acidentalmente coloca offline todos os nós de cluster na nuvem de saudação que rede e recursos de Cluster IP hello e nome de rede do Cluster não será capaz de toocome on-line. Olá evento isso impedirá atualiza tooother os recursos de cluster.

#### <a name="step-4-dns-configuration"></a>Etapa 4: Configuração de DNS
tooimplement uma transição suave depende de como o DNS está sendo utilizado e atualizado.
Quando AlwaysOn é instalado, ele cria um grupo de recursos de Cluster do Windows, se você abrir o Gerenciador de Cluster de Failover, você verá que, no mínimo, ele terá três recursos, Olá dois que Olá documento se refere a tooare:

* Nome de rede virtual (VNN) – Este é Olá DNS nome que o cliente se conectar toowhen desejarem tooconnect tooSQL servidores por meio do AlwaysOn.
* Recurso de endereço IP – isso é Olá de endereços IP que associado Olá VNN, você pode ter mais de um e uma configuração multissite, você terá um endereço IP por sub-rede/site.

Ao conectar tooSQL Server, o driver do SQL Server Client Olá será recuperar os registros DNS Olá associados ouvinte hello e tente tooconnect tooeach AlwaysOn associado endereço IP, abaixo, discutiremos alguns fatores que podem influenciar a isso.

Olá número de registros DNS simultâneos que estão associados com o nome do ouvinte Olá depende não apenas número de saudação de endereços IP associados, mas Olá ' RegisterAllIpProviders'setting no cluster de Failover para Olá recursos sempre ON VNN.

Quando você implanta sempre ativa no Azure há etapas diferentes toocreate Olá ouvinte e endereços IP, toomanually configurar Olá 'RegisterAllIpProviders' too1, isso é tooan diferentes locais sempre na implantação em que ele já está definido too1.

Se 'RegisterAllIpProviders' for 0, em seguida, você só verá o registro DNS no DNS associado Olá ouvinte:

![Appendix4][14]

Se 'RegisterAllIpProviders' for 1:

![Appendix5][15]

Olá código abaixo despejar Olá configurações VNN e defina-a para você,. Observe que, para hello alterar tootake efeito você precisará tootake Olá VNN off-line e ligue-o novamente online, essa colocando Olá offline interrupção causando conectividade de cliente ouvinte.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

Em uma etapa posterior da migração, você precisará tooupdate Olá sempre no ouvinte com um endereço IP atualizado que fazem referência a um balanceador de carga, isso envolverá uma remoção do recurso de endereço IP e a adição. Após a atualização IP hello, é necessário tooensure Olá novo endereço IP foi atualizado na zona DNS e que os clientes de saudação estão atualizando seu cache DNS local.

Se os clientes residem em um segmento de rede diferente e fazer referência a um servidor DNS diferente, será necessário tooconsider o que acontece com transferência de zona DNS durante a migração de saudação hello aplicativo reconectá tempo será limitado pelo menos Olá tempo de transferência de zona de qualquer novos endereços IP de ouvinte de saudação. Se você estiver na restrição de tempo aqui, você deve discutir e testar a imposição de uma transferência de zona incremental com as equipes de Windows, e também colocar Olá DNS tooa de registro de host reduzir tempo tooLive (TTL), para atualizam clientes de saudação. Para obter mais informações, consulte [Transferências de Zona Incrementais](https://technet.microsoft.com/library/cc958973.aspx) e [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Por saudação padrão TTL de registro de DNS que está associado a saudação ouvinte AlwaysOn no Azure é 1200 segundos. Talvez você queira tooreduce isso se você estiver na restrição de tempo durante a atualização de clientes migração tooensure Olá seus DNS com IP hello atualizado o endereço para o ouvinte de saudação. Você pode ver e modificar a configuração de saudação despejando configuração de saudação do hello VNN:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Observe, Olá Olá inferior 'HostRecordTTL', ocorrerá uma quantidade maior de tráfego DNS.

##### <a name="client-application-settings"></a>Configurações de aplicativo cliente
Se seu aplicativo de cliente SQL oferece suporte Olá .net 4.5 SQLClient, em seguida, você pode usar ' MULTISUBNETFAILOVER = TRUE' palavra-chave, isso é recomendado toobe aplicada conforme permite tooSQL mais rápido de conexão sempre no grupo de disponibilidade durante o failover. Ele enumera através de todos os endereços IP associados Olá sempre no ouvinte de em paralelo e executa uma velocidade de repetição de conexão TCP mais agressiva durante um failover.

Para obter mais informações sobre configurações de saudação acima, consulte [palavra-chave MultiSubnetFailover e recursos associados ao](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Consulte também [Suporte do SqlClient para a Alta Disponibilidade e a Recuperação de Desastre](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Etapa 5: Configurações de quórum do cluster
Como você vai toobe fazer pelo menos um SQL Server para baixo em um momento, você deve modificar a configuração de quorum do cluster hello, se usar testemunha de compartilhamento de arquivo (FSW) com 2 nós, você deve definir a maioria de nós Olá quorum tooallow e utilizar votação dinâmico, e isso é tooallow para constantes de tooremain um único nó.

    Set-ClusterQuorum -NodeMajority  

Para obter mais informações sobre como gerenciar e configurar quorum do cluster hello, consulte [Olá a configurar e gerenciar o Quorum em um Cluster de Failover do Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Etapa 6: extrair ACLs e pontos de extremidade existentes
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Salve esses arquivos de texto tooa.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Etapa 7: alterar parceiros de failover e modos de replicação
Se você tiver mais de 2 servidores do SQL, você deve alterar o failover de saudação da outra réplica secundária em outro controlador de domínio ou local 'too'Synchronous e torná-lo um parceiro de Failover automático (AFP), isso é para manter alta disponibilidade enquanto você estiver fazendo alterações. Você pode fazer isso por meio do TSQL ou modificar por SSMS:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Etapa 8: Remover a VM secundária do serviço de nuvem
Você deve estar planejando toomigrate um nó secundário nuvem pela primeira vez, se isso for primário no momento, você deve iniciar um failover manual.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Etapa 9: Alterar as configurações de caching de disco no arquivo CSV e salvar
Para volumes de dados essas devem ser definidas tooREADONLY.

Para volumes TLOG esses devem ser definidos tooNONE.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Etapa 10: copiar VHDS
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Você pode verificar o status da cópia Olá de saudação VHDs toohello conta de armazenamento Premium:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Aguarde até que todos esses itens sejam registrados como êxito.

Para obter informações para blobs individuais:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Etapa 11: Registrar o disco do sistema operacional
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Etapa 12: Importar a réplica secundária para o novo serviço de nuvem
opção de código Olá abaixo também Olá usa adicionado aqui você pode importar máquina hello e use o VIP devem ser retidos hello.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Etapa 13: criar ILB no novo Svc de nuvem, adicionar pontos de extremidade de carga balanceada e ACLs
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Etapa 14: Atualizar AlwaysOn
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Agora, remova o serviço de nuvem antigo Olá endereço IP.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Etapa 15: Verificar a atualização do DNS
Agora, verifique os servidores DNS em suas redes de cliente do SQL Server e certifique-se de que o cluster adicionou Olá registro de host adicionais para Olá adicionou o endereço IP. Se os servidores DNS não atualizou, considere forçar uma transferência de zona DNS e garantir que os clientes na sub-rede há hello são capazes de tooresolve tooboth sempre em endereços IP, isso é para que você não precisa toowait para a replicação automática do DNS.

#### <a name="step-16-reconfigure-always-on"></a>Etapa 16: Reconfigurar o AlwaysOn
Neste ponto você aguardar Olá secundária desse nó que foi migrado toofully ressincronizar com o nó local do hello e alternar o nó de replicação toosynchronous e torná-lo Olá AFP.  

#### <a name="step-17-migrate-second-node"></a>Etapa 17: Migrar o segundo nó
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Etapa 18: Alterar as configurações de caching de disco no arquivo CSV e salvar
Para volumes de dados essas devem ser definidas tooREADONLY.

Para volumes TLOG esses devem ser definidos tooNONE.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Etapa 19: criar a nova conta de armazenamento independente para o nó secundário
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Etapa 20: copiar VHDs
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Você pode verificar o status da cópia do VHD Olá para todos os VHDs: ForEach ($disk em $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Etiqueta de disco $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Aguarde até que todos esses itens sejam registrados como êxito.

Para obter informações para blobs individuais:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Etapa 21: Registrar o disco do sistema operacional
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Etapa 22: adicionar pontos de extremidade de carga balanceada e ACLs
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Etapa 23: Failover de teste
Você agora deve permitir que nós migrados Olá sincronizar com o nó local do AlwaysOn hello, colocá-lo no modo de replicação toosynchronous e aguarde até que ele seja sincronizado. Em seguida, o failover de local toohello primeiro nó migrado, que é Olá AFP. Depois que funcionou, alteração Olá migrados pela última vez nó toohello AFP.

Você deve testar failovers entre todos os nós e executar Embora testes caos tooensure failovers funcionam como esperado e em um tempo manor.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Etapa 24: colocar de volta configurações de quorum de cluster / TTL DNS / Failover de impressoras / Configurações de sincronização
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Adicionando recurso de endereço IP na mesma sub-rede
Se você tiver apenas 2 servidores SQL e quiser toomigrate-los tooa novo serviço de nuvem, mas deseja tookeep-los em Olá mesma sub-rede, você pode evitar deixar ouvinte Olá original de saudação toodelete off-line sempre no endereço IP e adicionar Olá novo endereço IP. Se você estiver migrando Olá VMs tooanother subrede não será necessário toodo isso, haverá uma rede de cluster adicionais que fazem referência a essa sub-rede.

Depois de abrir hello migrados secundário e adicionado ao novo recurso de endereço IP Olá Olá novo serviço de nuvem antes de failover Olá primário existente, você deve executar essas etapas em Olá Gerenciador de Cluster de Failover:

tooadd no endereço IP, consulte Olá [apêndice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), etapa 14.

1. Para o recurso de endereço IP atual hello, alterar Olá possível proprietário too'Existing SQL Server primário ', no exemplo hello abaixo 'dansqlams4':

    ![Appendix13][23]
2. Para o novo recurso de endereço IP hello alterar Olá possível proprietário too'Migrated secundário do SQL Server', no exemplo hello abaixo 'dansqlams5':

    ![Appendix14][24]
3. Depois que isso for definido, você poderá realizar failover, e quando é migrado do último nó Olá Olá possíveis proprietários devem ser editados para que esse nó é adicionado como um possível proprietário:

    ![Appendix15][25]

## <a name="additional-resources"></a>Recursos adicionais
* [Armazenamento Premium do Azure](../../../storage/common/storage-premium-storage.md)
* [Máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server nas Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
