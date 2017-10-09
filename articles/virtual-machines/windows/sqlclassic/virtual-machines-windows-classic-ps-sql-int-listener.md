---
title: aaaConfigure um ouvinte ILB para grupos de disponibilidade AlwaysOn no Azure | Microsoft Docs
description: "Este tutorial usa recursos criados com o modelo de implantação clássico hello e cria um ouvinte de disponibilidade do grupo AlwaysOn no Azure que usa um balanceador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Configurar um ouvinte de ILB para grupos de disponibilidade AlwaysOn no Azure
> [!div class="op_single_selector"]
> * [Ouvinte interno](../classic/ps-sql-int-listener.md)
> * [Ouvinte externo](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Visão geral

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange o uso de saudação do modelo de implantação clássico hello. É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

tooconfigure um ouvinte para um grupo de disponibilidade AlwaysOn no modelo do Gerenciador de recursos de hello, consulte [configurar um balanceador de carga para um grupo de disponibilidade AlwaysOn no Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

O seu grupo de disponibilidade pode conter réplicas somente locais, somente no Azure ou tanto locais quanto no Azure para configurações híbridas. Réplicas do Azure podem residir em Olá mesma região ou em várias regiões que usam várias redes virtuais. Olá procedimentos neste artigo presumem que você tenha já [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas ainda não configurou um ouvinte.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Diretrizes e limitações para ouvintes internos
uso de saudação de um balanceador de carga interno (ILB) com um ouvinte de grupo de disponibilidade no Azure é toohello assunto diretrizes a seguir:

* há suporte para o ouvinte do grupo de disponibilidade Olá no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Somente um ouvinte do grupo interno de disponibilidade é suportado para cada serviço de nuvem, pois ouvinte Olá configurado toohello ILB, e há apenas um ILB para cada serviço de nuvem. No entanto, é possível toocreate vários ouvintes externos. Para obter mais informações, veja [Configurar um ouvinte externo para grupos de disponibilidade AlwaysOn no Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar a acessibilidade de saudação do ouvinte Olá
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artigo concentra-se na criação de um ouvinte que use um ILB. Se você precisar de um ouvinte público ou externo, consulte versão Olá deste artigo que aborda a configuração de backup de um [ouvinte externo](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Criar pontos de extremidade da VM com balanceamento de carga com retorno de servidor direto
Você primeiro crie um ILB, executando o script hello posteriormente nesta seção.

Crie um ponto de extremidade com carga equilibrada para cada VM que hospeda uma réplica do Azure. Se você tiver réplicas em várias regiões, cada réplica para essa região deve estar no mesmo serviço de nuvem de saudação Olá mesma rede virtual do Azure. A criação de réplicas do grupo de disponibilidade que abrangem várias regiões do Azure exige a configuração de diversas redes virtuais. Para obter mais informações sobre como configurar cruzada conectividade de rede virtual, consulte [configurar conectividade de rede rede virtual toovirtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. No hello portal do Azure, vá tooeach VM que hospeda uma réplica tooview Olá os detalhes.

2. Clique em Olá **pontos de extremidade** guia para cada VM.

3. Verifique se esse Olá **nome** e **porta pública** do ponto de extremidade de escuta Olá que você deseja toouse não já estão em uso. O exemplo hello nesta seção, Olá nome é *MyEndpoint*, e porta Olá *1433*.

4. No cliente local, baixe e instale o hello mais recente [módulo PowerShell](https://azure.microsoft.com/downloads/).

5. Iniciar o Azure PowerShell.  
    Abre uma nova sessão do PowerShell, com hello Azure administrativos módulos carregados.

6. Execute `Get-AzurePublishSettingsFile`. Esse cmdlet direciona toodownload de navegador tooa um diretório local tooa de arquivo publicar configurações. Talvez você receba uma solicitação para inserir as suas credenciais de entrada de sua assinatura do Aure.

7. Execute seguinte Olá `Import-AzurePublishSettingsFile` comando com caminho Olá Olá Publicar arquivo de configurações que você baixou:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Depois de publicar Olá arquivo de configurações é importado, você pode gerenciar sua assinatura do Azure na sessão do PowerShell Olá.

8. Para o *ILB*, atribua um endereço IP estático. Examine a configuração atual de rede virtual Olá executando o comando a seguir de saudação:

        (Get-AzureVNetConfig).XMLConfiguration
9. Saudação de Observação *sub-rede* nome para a sub-rede de saudação que contém Olá VMs que hospedam réplicas de saudação. Esse nome é usado no parâmetro hello $SubnetName no script hello.

10. Saudação de Observação *VirtualNetworkSite* nomear e Olá iniciando *AddressPrefix* para a sub-rede de saudação que contém Olá VMs que hospedam réplicas de saudação. Procure um endereço IP disponível, passando os dois valores toohello `Test-AzureStaticVNetIP` comando e examinando Olá *AvailableAddresses*. Por exemplo, se hello rede virtual é chamada *MyVNet* e tem um intervalo de endereços de sub-rede que começa em *172.16.0.128*, seguinte Olá comando lista os endereços disponíveis:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Selecione um dos endereços disponíveis hello e usá-lo no parâmetro hello $ILBStaticIP do script hello na próxima etapa do hello.

12. Copiar Olá editor de texto de tooa de script do PowerShell a seguir e defina Olá valores de variáveis toosuit seu ambiente. Alguns parâmetros já receberam valores padrão.  

    Observe que as implantações existentes que usam grupos de afinidade não podem adicionar o ILB. Para saber mais sobre os requisitos do ILB, consulte [Visão geral do balanceador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).

    Além disso, se seu grupo de disponibilidade abranger regiões do Azure, você deve executar script hello uma vez em cada data center para o serviço de nuvem hello e nós que residem nesse datacenter.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Depois que você tiver definido as variáveis de Olá, Olá cópia script de saudação texto editor tooyour PowerShell sessão toorun-lo. Se ainda mostrará o prompt Olá  **>>** , pressione Enter novamente se script de saudação toomake começa a ser executado.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Verifique se KB2854082 está instalado, se necessário
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir as portas de firewall Olá em nós do grupo de disponibilidade
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Criar o ouvinte do grupo de disponibilidade Olá

Crie o ouvinte do grupo de disponibilidade de saudação em duas etapas. Primeiro, crie o recurso de cluster de ponto de acesso do hello cliente e configurar as dependências. Em seguida, configure recursos de cluster Olá no PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Criar ponto de acesso para cliente hello e configurar dependências de saudação de cluster
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar recursos de cluster Olá no PowerShell
1. Para ILB, você deve usar o endereço IP de saudação do hello ILB criado anteriormente. tooobtain esse IP endereço no PowerShell, use Olá script a seguir:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Em um dos Olá VMs, copie o script do PowerShell de saudação para seu editor de texto de tooa do sistema operacional e então definir variáveis de saudação toohello valores anotados anteriormente.

    Para o Windows Server 2012 ou posterior, use Olá script a seguir:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Para Windows Server 2008 R2, use Olá script a seguir:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Depois de ter conjunto Olá variáveis, abra uma janela elevada do Windows PowerShell, Olá colar o script do editor de texto de saudação em seu toorun de sessão do PowerShell-lo. Se ainda mostrará o prompt Olá  **>>** , pressione Enter novamente toomake-se de que o script hello inicia em execução.

4. Repita Olá etapas anteriores para cada VM.  
    Esse script configura o recurso de endereço IP hello com o endereço IP Olá Olá do serviço de nuvem e define outros parâmetros, como a porta de investigação de saudação. Quando o recurso de endereço IP hello é colocado online, ele pode responder toohello sondagem na porta de investigação de saudação do ponto de extremidade com balanceamento de carga Olá que você criou anteriormente.

## <a name="bring-hello-listener-online"></a>Coloque o ouvinte Olá online
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Itens de acompanhamento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Ouvinte de grupo de disponibilidade do teste hello (Olá na mesma rede virtual)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
