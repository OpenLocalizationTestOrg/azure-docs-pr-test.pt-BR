---
title: aaaConfigure um ouvinte externo para grupos de disponibilidade AlwaysOn | Microsoft Docs
description: "Este tutorial aborda você nas etapas de criação de um sempre no ouvinte do grupo disponibilidade no Azure que é acessível externamente usando Olá endereço IP Virtual público do hello serviço de nuvem associado."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Configurar um ouvinte externo para grupos de disponibilidade AlwaysOn no Azure
> [!div class="op_single_selector"]
> * [Ouvinte interno](../classic/ps-sql-int-listener.md)
> * [Ouvinte externo](../classic/ps-sql-ext-listener.md)
> 
> 

Este tópico mostra como tooconfigure um ouvinte para um grupo de disponibilidade AlwaysOn externamente acessível Olá da internet. Isso é possibilitado por meio da associação do serviço de nuvem Olá **IP Virtual público (VIP)** endereço com o ouvinte de saudação.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

O seu grupo de disponibilidade pode conter somente réplicas locais, somente no Azure ou locais e no Azure para configurações híbridas. Réplicas do Azure podem residir em Olá mesma região ou em várias regiões usando várias redes virtuais (VNets). Olá estas etapas pressupõem que você já tiver [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas não configurou um ouvinte.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Diretrizes e limitações para ouvintes externos
Observe Olá seguindo as diretrizes sobre o ouvinte do grupo de disponibilidade Olá no Azure durante a implantação usando Olá endereço serviço de nuvem publicado VIP:

* há suporte para o ouvinte do grupo de disponibilidade Olá no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* aplicativo de cliente Hello deve residir em um serviço de nuvem diferente Olá que contém suas máquinas virtuais do grupo de disponibilidade. Serviço de nuvem do Azure não suporta servidor direto retornar com cliente e servidor de saudação mesmo.
* Por padrão, etapas Olá neste artigo mostram como endereço IP Virtual (VIP) do serviço em nuvem tooconfigure Olá de toouse de um ouvinte. No entanto, é possível tooreserve e criar vários endereços VIP para seu serviço de nuvem. Isso permite que você toouse etapas Olá este toocreate artigo vários ouvintes que estão associados a um VIP diferente. Para obter informações sobre como toocreate vários endereços VIP, consulte [vários VIPs por serviço de nuvem](../../../load-balancer/load-balancer-multivip.md).
* Se você estiver criando um ouvinte para um ambiente híbrido, a rede de local de saudação deve ter conectividade toohello Internet pública em adição toohello VPN site a site com hello rede virtual do Azure. Quando em Olá sub-rede do Azure, o ouvinte do grupo de disponibilidade de saudação é alcançável somente pelo endereço IP público de Olá Olá respectivos do serviço de nuvem.
* Não há suporte para toocreate um ouvinte externo no hello mesmo serviço em que você também tem um ouvinte interno usando na nuvem Olá balanceador de carga interno (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar a acessibilidade de saudação do ouvinte Olá
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artigo se concentra na criação de um ouvinte que use o **balanceamento de carga externo**. Se você quiser um ouvinte de rede virtual privada tooyour, consulte versão Olá deste artigo que fornece as etapas para configurar um [ouvinte com o ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Criar pontos de extremidade da VM com balanceamento de carga com retorno de servidor direto
Balanceamento de carga externa usa Olá Olá virtual endereço IP Virtual público saudação do serviço de nuvem que hospeda suas VMs. Para que você não precisa toocreate ou configure o balanceador de carga de saudação nesse caso.

Você deve criar um ponto de extremidade de carga equilibrada para cada VM que hospeda uma réplica do Azure. Se você tiver réplicas em várias regiões, cada réplica para essa região deve estar no mesmo serviço de nuvem de saudação Olá mesma rede virtual. Criação de réplicas do Grupo de Disponibilidade que abrangem várias regiões do Azure requer configurar diversas VNets. Para obter mais informações sobre como configurar a conectividade de rede virtual cruzada, consulte [tooVNet VNet configurar conectividade](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. No portal do Azure de Olá, navegue tooeach VM hospedando uma réplica e exibir os detalhes hello.
2. Clique em Olá **pontos de extremidade** guia para cada uma das VMs hello.
3. Verifique se esse Olá **nome** e **porta pública** do ponto de extremidade de escuta Olá deseja toouse não ainda estiver em uso. O exemplo hello abaixo, Olá nome é "MyEndpoint" e porta de saudação é "1433".
4. No cliente local, baixe e instale [módulo do PowerShell mais recente Olá](https://azure.microsoft.com/downloads/).
5. Inicie o **PowerShell do Azure**. Um novo PowerShell sessão é aberta com hello módulos administrativos do Azure carregados.
6. Executar **Get-AzurePublishSettingsFile**. Esse cmdlet direciona toodownload de navegador tooa um diretório local tooa de arquivo publicar configurações. É possível que seja solicitado para inserir as suas credenciais para a assinatura do Aure.
7. Executar Olá **AzurePublishSettingsFile importação** comando com caminho Olá Olá Publicar arquivo de configurações que você baixou:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Depois que o hello Publicar arquivo de configurações é importado, você pode gerenciar sua assinatura do Azure na sessão do PowerShell hello.
    
1. Copie o script do PowerShell Olá abaixo em um editor de texto e defina Olá valores de variáveis toosuit seu ambiente (padrões foram fornecidos para alguns parâmetros). Observe que se seu grupo de disponibilidade abranger regiões do Azure, você deve executar Olá script uma vez em cada data center para o serviço de nuvem hello e nós que residem nesse datacenter.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Depois que você tiver definido as variáveis de Olá, Olá de cópia de script do editor de texto de saudação em seu toorun de sessão do PowerShell do Azure-lo. Se ainda mostrará o prompt Olá >>, digite ENTER novamente se script de saudação toomake começa a ser executado.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Verifique se KB2854082 está instalado, se necessário
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir as portas de firewall Olá em nós do grupo de disponibilidade
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Criar o ouvinte do grupo de disponibilidade Olá

Crie o ouvinte do grupo de disponibilidade de saudação em duas etapas. Primeiro, crie o recurso de cluster de ponto de acesso do hello cliente e configurar as dependências. Em seguida, configure recursos de cluster de saudação com o PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Criar ponto de acesso para cliente hello e configurar dependências de saudação de cluster
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar recursos de cluster Olá no PowerShell
1. Para o balanceamento de carga externo, você deve obter Olá endereço IP virtual público saudação do serviço de nuvem que contém suas réplicas. Faça logon no hello portal do Azure. Navegue toohello serviço de nuvem que contém o grupo de disponibilidade VM. Olá abrir **painel** exibição.
2. Observe o endereço de saudação mostrado em **endereço IP Virtual público (VIP)**. Se a sua solução abrange VNets, repita essa etapa para cada serviço de nuvem que contém uma VM que hospeda uma réplica.
3. Em um dos Olá VMs, copie Olá script do PowerShell abaixo em um editor de texto e defina as variáveis de saudação toohello valores anotados anteriormente.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Uma vez você tiver definido as variáveis de hello, abra uma janela do Windows PowerShell com privilégios elevados, copia script hello do editor de texto de saudação e colá-lo em seu toorun de sessão do PowerShell do Azure. Se ainda mostrará o prompt Olá >>, digite ENTER novamente se script de saudação toomake começa a ser executado.
5. Repita esse procedimento em cada VM. Esse script configura o recurso de endereço IP de saudação com o endereço IP Olá Olá do serviço de nuvem e define outros parâmetros como a porta de investigação de saudação. Quando Olá recurso de endereço IP está online, ele pode responder toohello sondagem na porta de investigação de saudação do ponto de extremidade com balanceamento de carga de saudação criada anteriormente neste tutorial.

## <a name="bring-hello-listener-online"></a>Coloque o ouvinte Olá online
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Itens de acompanhamento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Ouvinte de grupo de disponibilidade do teste hello (Olá na mesma rede virtual)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Ouvinte de grupo de disponibilidade do teste hello (sobre Olá da internet)
Em ordem tooaccess Olá ouvinte de rede virtual externa Olá é necessário usar o balanceamento de carga de externas/público (descrito neste tópico), em vez de ILB, que é somente acessível em hello mesma rede virtual. Na cadeia de caracteres de conexão Olá, você deve especificar o nome de serviço de nuvem hello. Por exemplo, se você tiver um serviço de nuvem com o nome da saudação *mycloudservice*, instrução de sqlcmd Olá seria o seguinte:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Ao contrário do exemplo anterior de saudação, autenticação do SQL deve ser usada, porque o chamador Olá não é possível usar a autenticação do windows em Olá internet. Para obter mais informações, consulte [AlwaysOn Availability Group in Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)(Grupo de disponibilidade AlwaysOn na VM do Azure: cenários de conectividade do cliente). Ao usar a autenticação do SQL, certifique-se de que você crie Olá mesmo logon em ambas as réplicas. Para obter mais informações sobre como solucionar problemas de logons com grupos de disponibilidade, consulte [como toomap logons ou usar contidos SQL réplicas de tooother de tooconnect de usuário de banco de dados e mapear os bancos de dados tooavailability](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Se Olá sempre em réplicas estiverem em sub-redes diferentes, os clientes deverão especificar **MultisubnetFailover = True** na cadeia de caracteres de conexão de saudação. Isso resulta em tooreplicas de tentativas de conexão paralelas em sub-redes diferentes hello. Observe que esse cenário inclui uma implantação de grupo de disponibilidade do AlwaysOn entre regiões.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

