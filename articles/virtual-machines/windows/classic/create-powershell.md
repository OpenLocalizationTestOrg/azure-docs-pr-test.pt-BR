---
title: aaaCreate uma VM do Windows com o PowerShell | Microsoft Docs
description: "Crie máquinas virtuais do Windows PowerShell do Azure e o modelo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Criar uma máquina virtual do Windows com o modelo de implantação clássico hello e PowerShell
> [!div class="op_single_selector"]
> * [Portal do Azure - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Estas etapas mostram como os comandos toocustomize um conjunto de PowerShell do Azure que criar e pré-configurar a uma máquina virtual baseados no Windows Azure usando uma abordagem de bloco de construção. Você pode usar esse processo tooquickly criar um conjunto de comandos para uma nova máquina virtual com base em Windows e expanda uma implantação existente ou toocreate comando vários conjuntos que rapidamente criar um personalizado de desenvolvimento/teste ou ambiente de profissional de TI.

Estas etapas seguem uma abordagem de preencher lacunas para criar conjuntos de comandos do Azure PowerShell. Essa abordagem pode ser útil se você for novo tooPowerShell ou você quiser apenas tooknow toospecify quais valores de configuração com êxito. Usuários avançados do PowerShell podem executar comandos hello e substitua seus próprios valores para variáveis de saudação (linhas de saudação que começam com "$").

Se você ainda não tiver feito isso, use as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell no computador local. Em seguida, abra um prompt de comando do Windows PowerShell.

## <a name="step-1-add-your-account"></a>Etapa 1: adicionar sua conta
1. No prompt do PowerShell hello, digite **Add-AzureAccount** e clique em **Enter**. 
2. Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**. 
3. Digite a senha Olá para sua conta. 
4. Clique em **Entrar**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Etapa 2: Definir a assinatura e a conta de armazenamento
Defina a assinatura do Azure e a conta de armazenamento executando esses comandos no prompt de comando do Windows PowerShell hello. Substitua tudo entre aspas hello, incluindo hello < e > caracteres, com nomes de saudação correto.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Você pode obter o nome de assinatura correta de saudação do hello propriedade de nome de inscrição da saída de saudação do hello **Get-AzureSubscription** comando. Você pode obter o nome de conta de armazenamento correta de saudação do Olá propriedade do rótulo de saída Olá Olá **Get-AzureStorageAccount** comando depois de executar Olá **Select-AzureSubscription** comando.

## <a name="step-3-determine-hello-imagefamily"></a>Etapa 3: Determinar Olá ImageFamily
Em seguida, você precisa toodetermine Olá ImageFamily ou valor de rótulo para toohello correspondente de imagem específica de saudação máquina virtual do Azure que você deseja toocreate. Você pode obter a lista de saudação de valores ImageFamily disponíveis com este comando.

    Get-AzureVMImage | select ImageFamily -Unique

Aqui estão alguns exemplos de valores de ImageFamily para computadores baseados em Windows:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise em Windows Server 2012

Se você encontrar a imagem de saudação que você está procurando, abra uma nova instância do editor de texto de saudação de sua escolha ou Olá ambiente de script integrado do PowerShell (ISE). Copie o seguinte de Olá no novo arquivo de texto de saudação ou hello PowerShell ISE, substituindo o valor de ImageFamily hello.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Em alguns casos, o nome de imagem do hello está sendo Olá em vez da saudação ImageFamily valor da propriedade do rótulo. Se você não encontrou a imagem de saudação que você está procurando usando a propriedade ImageFamily hello, liste imagens Olá por sua propriedade de rótulo com este comando.

    Get-AzureVMImage | select Label -Unique

Se você encontrar a imagem à direita Olá com este comando, abra uma instância atualizada do editor de texto de saudação de sua escolha ou Olá PowerShell ISE. Copie o seguinte de Olá no novo arquivo de texto de saudação ou hello PowerShell ISE, substituindo o valor de rótulo de saudação.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Etapa 4: criar o conjunto de comandos
Crie restante de saudação do comando definido, copiando o conjunto apropriado de saudação de blocos abaixo para seu novo arquivo de texto ou hello ISE e, em seguida, preencher os valores de variáveis de saudação e removendo hello < e > caracteres. Consulte Olá dois [exemplos](#examples) final Olá deste artigo para uma ideia do resultado final da saudação.

Comece seu conjunto de comandos escolhendo um destes dois blocos de comandos (obrigatório).

Opção 1: especifique um nome e um tamanho de máquina virtual.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Opção 2: especifique um nome, o tamanho e o nome do conjunto de disponibilidade.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Para obter valores de InstanceSize Olá para D, DS ou máquinas virtuais de série G, consulte [Máquina Virtual e tamanhos de serviço de nuvem para Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Se você tiver um contrato empresarial com Software Assurance e pretende tootake vantagem de saudação do Windows Server [híbrida benefício de usar](https://azure.microsoft.com/pricing/hybrid-use-benefit/), adicionar o **- LicenseType** toohello parâmetro  **New-AzureVMConfig** cmdlet, passando o valor de saudação **Windows_Server** para Olá típico caso de uso.  Certifique-se de que você estiver usando uma imagem que você carregou; Você não pode usar uma imagem padrão do hello galeria com hello híbrida benefício de usar.
> 
> 

Opcionalmente, para um computador com Windows autônomo, especifique Olá conta de administrador local e senha.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Escolha uma senha forte. toocheck sua intensidade, consulte [Verificador de senha: usando senhas de alta segurança](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Olá tooadd computador tooan existente do Active Directory domínio do Windows, especificar opcionalmente conta de administrador local hello e senha, domínio Olá e Olá nome e senha de uma conta de domínio.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Para opções adicionais de configuração prévia para máquinas virtuais baseadas em Windows, consulte sintaxe Olá Olá **Windows** e **WindowsDomain** define parâmetro [ Adicionar-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Opcionalmente, atribua um endereço IP específico, conhecido como um DIP estático máquina virtual hello.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Você pode verificar se um endereço IP específico está disponível com:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Opcionalmente, atribua uma sub-rede específica do hello máquina virtual tooa em uma rede virtual do Azure.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Opcionalmente, adicione uma máquina virtual de toohello de disco de dados único.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Para um controlador de domínio do Active Directory, defina $hcaching muito "None".

Opcionalmente, adicione Olá conjunto máquinas virtuais tooan existente com balanceamento de carga para tráfego externo.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Por fim, escolha um desses blocos de comando necessário para a criação de máquina virtual de saudação.

Opção 1: Crie a máquina virtual de saudação em um serviço de nuvem existente.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

nome curto de Olá Olá do serviço de nuvem é o nome de Olá que aparece na lista de saudação dos serviços de nuvem no portal do Azure de saudação ou na lista de saudação de grupos de recursos no hello portal do Azure.

Opção 2: Crie máquina virtual de saudação em um serviço de nuvem existente e a rede virtual.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Etapa 5: executar o conjunto de comandos
Examine o conjunto de comandos do PowerShell do Azure Olá criados em seu editor de texto ou Olá ISE do PowerShell consiste em vários blocos de comandos da etapa 4. Certifique-se de que você especificou todas as variáveis de saudação necessário e que tenham valores corretos hello. Além disso, certifique-se de que você removeu todos os caracteres hello < e >.

Se você estiver usando um editor de texto, cópia Olá comando definir toohello área de transferência e clique, em seguida, abra o prompt de comando do Windows PowerShell. Isso emitirá o conjunto de comandos hello como uma série de comandos do PowerShell e criar sua máquina virtual do Azure. Como alternativa, execute o comando de saudação definido no hello PowerShell ISE.

Se pretender criar novamente essa máquina virtual ou uma semelhante, você poderá:

* Salvar este conjunto de comandos como um arquivo de script do PowerShell (*.ps1).
* Salvar este comando definido como um runbook de automação do Azure no hello **contas de automação** seção Olá portal do Azure.

## <a id="examples"></a>Exemplos
Aqui estão dois exemplos de uso etapas Olá acima toobuild conjuntos de comandos de PowerShell do Azure que cria máquinas de virtuais baseadas em Windows Azure.

### <a name="example-1"></a>Exemplo 1
Preciso de um PowerShell comando set toocreate saudação inicial máquina de virtual para um controlador de domínio do Active Directory:

* Usa a imagem do Windows Server 2012 R2 Datacenter hello.
* Tem o nome de saudação AZDC1.
* É um computador autônomo.
* Tem um disco de dados adicional de 20 GB.
* Tem o endereço IP estático Olá 192.168.244.4.
* Está na sub-rede de back-end de saudação da rede virtual do hello AZDatacenter.
* É no serviço de nuvem Olá TailspinToys do Azure.

Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual, com linhas em branco entre cada bloco para facilitar a leitura.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Exemplo 2
Preciso de um PowerShell comando set toocreate uma máquina virtual para um servidor de linha de negócios que:

* Usa a imagem do Windows Server 2012 R2 Datacenter hello.
* Tem o nome de saudação LOB1.
* É um membro do domínio corp.contoso.com de saudação.
* Tem um disco de dados adicional de 200 GB.
* Está na sub-rede de front-end de saudação da rede virtual do hello AZDatacenter.
* É no serviço de nuvem Olá TailspinToys do Azure.

Aqui está Olá correspondente do Azure PowerShell comando conjunto toocreate esta máquina virtual.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Próximas etapas
Se você precisar de um disco do sistema operacional que é maior do que 127 GB, você pode [Expandir unidade Olá SO](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

