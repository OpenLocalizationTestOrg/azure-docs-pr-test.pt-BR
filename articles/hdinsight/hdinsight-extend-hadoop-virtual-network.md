---
title: aaaExtend HDInsight com a rede Virtual - Azure | Microsoft Docs
description: Saiba como toouse rede Virtual do Azure tooconnect HDInsight tooother nuvem recursos ou recursos no seu datacenter
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Estender o Azure HDInsight usando uma Rede Virtual do Azure

Saiba como toouse HDInsight com um [rede Virtual do Azure](../virtual-network/virtual-networks-overview.md). Usar uma rede Virtual do Azure permite Olá os seguintes cenários:

* Conectando tooHDInsight diretamente de uma rede local.

* Conectar HDInsight toodata armazena em uma rede Virtual do Azure.

* Diretamente o acesso a serviços Hadoop que não estão disponível publicamente em Olá da internet. Por exemplo, as APIs de Kafka ou Olá HBase Java API.

> [!WARNING]
> informações de saudação neste documento requerem uma compreensão de rede TCP/IP. Se você não estiver familiarizado com a rede de TCP/IP, você deve trabalhar junto com alguém que está antes de fazer modificações tooproduction redes.

## <a name="planning"></a>Planejamento

Olá seguem perguntas Olá que você deve responder ao planejar tooinstall HDInsight em uma rede virtual:

* Você precisa tooinstall HDInsight em uma rede virtual existente? Ou você está criando uma nova rede?

    Se você estiver usando uma rede virtual existente, talvez seja necessário toomodify configuração de rede de saudação antes de instalar o HDInsight. Para obter mais informações, consulte Olá [adicionar a rede virtual existente do HDInsight tooan](#existingvnet) seção.

* Você deseja que sua rede local ou rede virtual do hello tooconnect que contém a rede virtual do HDInsight tooanother?

    trabalho de tooeasily com recursos em redes, você pode precisar toocreate um DNS personalizado e configure o encaminhamento de DNS. Para obter mais informações, consulte Olá [conectar várias redes](#multinet) seção.

* Você deseja toorestrict/redirecionar tráfego de entrada ou saída tooHDInsight?

    HDInsight deve ter irrestrito a comunicação com endereços IP específicos no hello data center do Azure. Também há diversas portas que devem receber permissão por meio de firewalls para a comunicação do cliente. Para obter mais informações, consulte Olá [controlando o tráfego de rede](#networktraffic) seção.

## <a id="existingvnet"></a>Adicionar a rede virtual existente do HDInsight tooan

Use etapas Olá toodiscover esta seção como tooadd um novo tooan de HDInsight existente da rede Virtual do Azure.

> [!NOTE]
> Não é possível adicionar um cluster HDInsight existente a uma rede virtual.

1. Você está usando um clássico ou modelo de implantação do Gerenciador de recursos de rede virtual Olá?

    O HDInsight 3.4 e posterior exige uma rede virtual do Resource Manager. Versões anteriores do HDInsight exigiam uma rede virtual clássica.

    Se sua rede existente é uma rede virtual clássica, crie uma rede virtual do Gerenciador de recursos e, em seguida, conecte-se Olá dois. [Conectando clássico VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Depois de ingressar, HDInsight instalado na rede do Gerenciador de recursos de saudação pode interagir com recursos de rede clássicos hello.

2. Você usa o túnel forçado? O túnel forçado é uma configuração de sub-rede que força a saída dispositivo tooa de tráfego de Internet para inspeção e registro em log. O HDInsight não dá suporte ao túnel forçado. Remova o túnel forçado antes de instalar o HDInsight em uma sub-rede ou crie uma nova sub-rede para o HDInsight.

3. Você usa grupos de segurança de rede, rotas definidas pelo usuário ou o tráfego de toorestrict de dispositivos de rede Virtual para ou de rede virtual Olá?

    Como um serviço gerenciado, o HDInsight requer acesso irrestrito tooseveral endereços IP no hello data center do Azure. comunicação tooallow com esses endereços IP, atualizar todos os grupos de segurança de rede existentes ou rotas definidas pelo usuário.

    O HDInsight hospeda vários serviços, que usam uma variedade de portas. Não bloquear o tráfego de portas toothese. Para obter uma lista de portas tooallow através de firewalls de dispositivo virtual, consulte Olá [segurança](#security) seção.

    toofind sua configuração de segurança existente, use hello Azure PowerShell ou CLI do Azure comandos a seguir:

    * Grupos de segurança de rede

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Para obter mais informações, consulte Olá [solucionar problemas de grupos de segurança de rede](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.

        > [!IMPORTANT]
        > As regras do grupo de segurança de rede são aplicadas em ordem, com base na prioridade da regra. Olá primeira regra correspondente padrão de tráfego de saudação é aplicada, e nenhum outro são aplicados para que o tráfego. Regras de ordem do mais permissivo tooleast permissivo. Para obter mais informações, consulte Olá [filtrar o tráfego de rede com os grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) documento.

    * Rotas definidas pelo usuário

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Para obter mais informações, consulte Olá [solucionar rotas](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.

4. Criar um cluster HDInsight e selecione Olá rede Virtual do Azure durante a configuração. Use as etapas de Olá Olá seguindo o processo de criação de cluster do documentos toounderstand hello:

    * [Criar HDInsight usando Olá portal do Azure](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Criar o HDInsight usando o Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Criar o HDInsight usando a CLI do Azure 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Criar o HDInsight usando um modelo do Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Rede virtual tooa adicionando HDInsight é uma etapa de configuração opcional. Ser-se de rede virtual Olá de tooselect durante a configuração de cluster de saudação.

## <a id="multinet"></a>Conectando várias redes

Olá maior desafio com uma configuração de multi-rede de é a resolução de nomes entre redes de saudação.

O Azure fornece a resolução de nomes para os serviços do Azure instalados em uma rede virtual do Azure. Essa resolução de nome interno permite HDInsight tooconnect toohello a seguir de recursos usando um nome de domínio totalmente qualificado (FQDN):

* Qualquer recurso que está disponível no hello da internet. Por exemplo, microsoft.com, google.com.

* Qualquer recurso que está em Olá mesma rede Virtual do Azure, usando Olá __nome DNS interno__ do recurso de saudação. Por exemplo, ao usar a resolução de nome padrão hello, Olá seguem exemplo interno DNS nomes atribuídos tooHDInsight nós de trabalho:

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Esses dois nós podem se comunicar diretamente um com o outro e com outros nós no HDInsight, usando nomes DNS internos.

resolução de nome padrão Olá __não__ permitir HDInsight tooresolve nomes de saudação de recursos em redes de rede virtual toohello unidas. Por exemplo, é comum toojoin seu local de rede virtual toohello de rede. Apenas saudação padrão resolução de nomes, HDInsight não pode acessar recursos na rede de local de saudação por nome. Olá oposto também é verdadeiro, recursos em sua rede local não podem acessar recursos na rede virtual Olá por nome.

> [!WARNING]
> Você deve criar um servidor DNS personalizado hello e configurar Olá rede virtual toouse-lo antes de criar hello cluster HDInsight.

resolução de nomes de tooenable entre a rede virtual hello e recursos em redes associadas, você deve executar Olá ações a seguir:

1. Crie um servidor DNS personalizado no hello rede Virtual do Azure, onde você planeja tooinstall HDInsight.

2. Configure Olá rede virtual toouse Olá servidor DNS personalizado.

3. Localize hello que Azure atribuiu sufixo DNS para sua rede virtual. Esse valor é muito semelhante`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Para obter informações sobre como encontrar o sufixo DNS hello, consulte Olá [exemplo: DNS personalizado](#example-dns) seção.

4. Configure o encaminhamento entre os servidores DNS hello. configuração Olá depende do tipo hello da rede remota.

    * Se a rede remota Olá é uma rede local, configure o DNS da seguinte maneira:
        
        * __DNS personalizado__ (na rede virtual de saudação):

            * Encaminhar solicitações para o sufixo DNS de saudação do resolvedor do Azure recursiva toohello do hello rede virtual (168.63.129.16). Azure lida com solicitações de recursos na rede virtual Olá

            * Encaminhe todas as outra solicitações toohello no servidor DNS local. Olá locais DNS manipula todas as outras solicitações de resolução de nome, até mesmo solicitações para recursos de internet, como Microsoft.com.

        * __DNS local__: encaminhar solicitações para Olá rede virtual DNS sufixo toohello um servidor DNS personalizado. um servidor DNS personalizado Hello, em seguida, encaminha toohello recursiva Azure resolvedor.

        Solicitações de rotas essa configuração para totalmente qualificado de nomes de domínio que contêm o sufixo DNS Olá Olá virtual toohello personalizado DNS do servidor de rede. Todas as outras solicitações (até mesmo para endereços da internet pública) são manipuladas pelo servidor DNS local hello.

    * Se a rede remota Olá é outra rede Virtual do Azure, configure DNS da seguinte maneira:

        * __DNS personalizado__ (em cada rede virtual):

            * As solicitações para o sufixo DNS de saudação de redes virtuais Olá são encaminhadas toohello servidores DNS personalizados. Olá DNS em cada rede virtual é responsável por resolver recursos em sua rede.

            * Encaminhe todos os outros resolvedor de Azure recursiva de toohello solicitações. resolvedor de recursiva Olá é responsável por resolver o local e os recursos da internet.

        servidor DNS Olá para cada rede encaminha solicitações toohello outros, com base em sufixo DNS. Outras solicitações são resolvidas usando hello Azure recursiva resolvedor.

    Para obter um exemplo de cada configuração, consulte Olá [exemplo: DNS personalizado](#example-dns) seção.

Para obter mais informações, consulte Olá [resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.

## <a name="directly-connect-toohadoop-services"></a>Conectar-se diretamente tooHadoop serviços

Mais documentação no HDInsight supõe que você tenha o cluster de toohello de acesso sobre Olá internet. Por exemplo, você pode se conectar a cluster toohello em https://CLUSTERNAME.azurehdinsight.net. Esse endereço usa o gateway pública hello, que não está disponível se você tiver usado os NSGs ou UDRs toorestrict acesso Olá da internet.

tooconnect tooAmbari e outras páginas da web por meio da rede virtual do hello, use Olá etapas a seguir:

1. toodiscover Olá interno nomes totalmente qualificados (FQDN) de nós de cluster do HDInsight hello, use um dos métodos a seguir de saudação:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    Na lista de saudação de nós retornados, localize Olá FQDN para Olá nós de cabeçalho e use Olá FQDNs tooconnect tooAmbari e outros serviços da web. Por exemplo, use `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Alguns serviços hospedados em nós de cabeçalho hello serão apenas ativos em um nó por vez. Se você tentar acessar um serviço em um nó de cabeçalho e retorna um erro 404, alterne toohello outro nó principal.

2. nó de saudação toodetermine e porta de um serviço estiver disponível, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

## <a id="networktraffic"></a> Controlando o tráfego de rede

Tráfego de rede em redes virtuais do Azure pode ser controlado usando Olá métodos a seguir:

* **Grupos de segurança de rede** (NSG) permitem o tráfego de entrada e saída de toofilter toohello de rede. Para obter mais informações, consulte Olá [filtrar o tráfego de rede com os grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) documento.

    > [!WARNING]
    > O HDInsight não dá suporte à restrição do tráfego de saída.

* **Rotas definidas pelo usuário** (UDR) definem como os fluxos de tráfego entre os recursos na rede de saudação. Para obter mais informações, consulte Olá [rotas definidas pelo usuário e encaminhamento de IP](../virtual-network/virtual-networks-udr-overview.md) documento.

* **Soluções de virtualização de rede** duplicar a funcionalidade de saudação de dispositivos, como roteadores e firewalls. Para obter mais informações, consulte Olá [dispositivos de rede](https://azure.microsoft.com/solutions/network-appliances) documento.

Como um serviço gerenciado, o HDInsight requer acesso irrestrito tooAzure integridade e o gerenciamento de serviços na nuvem do Azure de saudação. Ao usar NSGs e UDRs, verifique se o HDInsight e esses serviços podem se comunicar com o HDInsight.

O HDInsight expõe serviços em várias portas. Ao usar um firewall de dispositivo virtual, você deve permitir tráfego na Olá portas usadas para esses serviços. Para obter mais informações, consulte a seção de saudação [portas necessárias].

### <a id="hdinsight-ip"></a> HDInsight com grupos de segurança de rede e rotas definidas pelo usuário

Se você planeja usar **grupos de segurança de rede** ou **rotas definidas pelo usuário** toocontrol o tráfego de rede, execute Olá ações a seguir antes de instalar o HDInsight:

1. Identifica Olá região do Azure que você planeje toouse para HDInsight.

2. Identificar os endereços IP hello exigidos pelo HDInsight. Para obter mais informações, consulte Olá [endereços IP necessários para HDInsight](#hdinsight-ip) seção.

3. Criar ou modificar grupos de segurança de rede hello ou rotas definidas pelo usuário para a sub-rede de saudação que você planeje tooinstall HDInsight em.

    * __Grupos de segurança de rede__: permitir __entrada__ o tráfego na porta __443__ de endereços IP de saudação.
    * __Rotas definidas pelo usuário__: criar um endereço IP de tooeach de rota e defina Olá __tipo do próximo salto__ too__Internet__.

Para obter mais informações sobre grupos de segurança de rede ou rotas definidas pelo usuário, consulte Olá documentação a seguir:

* [Grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md)

* [Rotas definidas pelo usuário](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Túnel forçado

O túnel forçado é uma configuração de roteamento definido pelo usuário em que todo o tráfego de uma sub-rede é forçado tooa específicos de rede ou local, como sua rede local. O HDInsight __não__ dá suporte ao túnel forçado.

## <a id="hdinsight-ip"></a> Endereços IP obrigatórios

> [!IMPORTANT]
> Olá integridade do Azure e serviços de gerenciamento devem ser capaz de toocommunicate com HDInsight. Se você usar grupos de segurança de rede ou rotas definidas pelo usuário, permita o tráfego da saudação endereços IP para essas tooreach serviços HDInsight.
>
> Se você não usar grupos de segurança de rede ou tráfego de toocontrol rotas definidas pelo usuário, você pode ignorar esta seção.

Se você usar grupos de segurança de rede ou rotas definidas pelo usuário, você deve permitir tráfego do hello integridade do Azure e serviços de gerenciamento tooreach HDInsight. Use Olá etapas toofind Olá endereços IP devem ser permitidos a seguir:

1. Você sempre deve permitir o tráfego de saudação endereços IP a seguir:

    | Endereço IP | Porta permitida | Direção |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Entrada |
    | 23.99.5.239 | 443 | Entrada |
    | 168.61.48.131 | 443 | Entrada |
    | 138.91.141.162 | 443 | Entrada |

2. Se seu cluster HDInsight está em uma saudação regiões a seguir, você deve permitir tráfego de endereços IP de saudação listados para região hello:

    > [!IMPORTANT]
    > Se Olá região do Azure que você está usando não estiver listado, só use quatro endereços IP hello da etapa 1.

    | País | Região | Endereços IP permitidos | Porta permitida | Direção |
    | ---- | ---- | ---- | ---- | ----- |
    | Ásia | Ásia Oriental | 23.102.235.122</br>52.175.38.134 | 443 | Entrada |
    | &nbsp; | Sudeste Asiático | 13.76.245.160</br>13.76.136.249 | 443 | Entrada |
    | Austrália | Leste da Austrália | 104.210.84.115</br>13.75.152.195 | 443 | Entrada |
    | &nbsp; | Sudeste da Austrália | 13.77.2.56</br>13.77.2.94 | 443 | Entrada |
    | Brasil | Sul do Brasil | 191.235.84.104</br>191.235.87.113 | 443 | Entrada |
    | Canadá | Leste do Canadá | 52.229.127.96</br>52.229.123.172 | 443 | Entrada |
    | &nbsp; | Canadá Central | 52.228.37.66</br>52.228.45.222 | 443 | Entrada |
    | China | Norte da China | 42.159.96.170</br>139.217.2.219 | 443 | Entrada |
    | &nbsp; | Leste da China | 42.159.198.178</br>42.159.234.157 | 443 | Entrada |
    | Europa | Norte da Europa | 52.164.210.96</br>13.74.153.132 | 443 | Entrada |
    | &nbsp; | Europa Ocidental| 52.166.243.90</br>52.174.36.244 | 443 | Entrada |
    | Alemanha | Alemanha Central | 51.4.146.68</br>51.4.146.80 | 443 | Entrada |
    | &nbsp; | Nordeste da Alemanha | 51.5.150.132</br>51.5.144.101 | 443 | Entrada |
    | Índia | Índia Central | 52.172.153.209</br>52.172.152.49 | 443 | Entrada |
    | Japão | Leste do Japão | 13.78.125.90</br>13.78.89.60 | 443 | Entrada |
    | &nbsp; | Oeste do Japão | 40.74.125.69</br>138.91.29.150 | 443 | Entrada |
    | Coreia | Coreia Central | 52.231.39.142</br>52.231.36.209 | 433 | Entrada |
    | &nbsp; | Sul da Coreia | 52.231.203.16</br>52.231.205.214 | 443 | Entrada
    | Reino Unido | Oeste do Reino Unido | 51.141.13.110</br>51.141.7.20 | 443 | Entrada |
    | &nbsp; | Sul do Reino Unido | 51.140.47.39</br>51.140.52.16 | 443 | Entrada |
    | Estados Unidos | Centro dos EUA | 13.67.223.215</br>40.86.83.253 | 443 | Entrada |
    | &nbsp; | Centro-Norte dos EUA | 157.56.8.38</br>157.55.213.99 | 443 | Entrada |
    | &nbsp; | Centro-Oeste dos EUA | 52.161.23.15</br>52.161.10.167 | 443 | Entrada |
    | &nbsp; | Oeste dos EUA 2 | 52.175.211.210</br>52.175.222.222 | 443 | Entrada |

    Para obter informações sobre IP hello endereços toouse para governo do Azure, consulte Olá [Azure governamental Intelligence + análise](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.

3. Se você usar um servidor DNS personalizado com a rede virtual, também deverá permitir o acesso de __168.63.129.16__. Esse endereço é o resolvedor recursivo do Azure. Para obter mais informações, consulte Olá [resolução de nomes para VMs e função instâncias](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.

Para obter mais informações, consulte Olá [controlando o tráfego de rede](#networktraffic) seção.

## <a id="hdinsight-ports"></a> Portas obrigatórias

Se você planeja usar uma rede **firewall do dispositivo virtual** toosecure Olá rede virtual, e você deve permitir o tráfego de saída no Olá portas a seguir:

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Para obter uma lista de portas para serviços específicos, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.

Para obter mais informações sobre regras de firewall para dispositivos virtuais, consulte Olá [cenário de dispositivo virtual](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.

## <a id="hdinsight-nsg"></a>Exemplo: grupos de segurança de rede com o HDInsight

Olá os exemplos nesta seção demonstram como o grupo de segurança de rede toocreate regras que permitem o HDInsight toocommunicate com hello serviços de gerenciamento do Azure. Antes de usar os exemplos de hello, ajuste Olá IP endereços toomatch hello aqueles para Olá região do Azure que você está usando. Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.

### <a name="azure-resource-management-template"></a>Modelo do Azure Resource Manager

Hello modelo gerenciamento de recursos a seguir cria uma rede virtual que restringe o tráfego de entrada, mas permite que o tráfego de endereços IP de saudação exigido pelo HDInsight. Esse modelo também cria um cluster HDInsight na rede virtual hello.

* [Implantar uma Rede Virtual protegida do Azure e um cluster HDInsight Hadoop](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando. Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.

### <a name="azure-powershell"></a>Azure PowerShell

Use Olá toocreate de script do PowerShell uma rede virtual que restringe o tráfego de entrada e permite o tráfego de saudação endereços IP para a região do Norte da Europa Olá a seguir.

> [!IMPORTANT]
> Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando. Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> Este exemplo demonstra como o tráfego em endereços IP hello necessário de entrada tooadd tooallow de regras. Ele não contém um toorestrict de regra de acesso de outras fontes de entrada.
>
> Olá exemplo a seguir demonstra como acessar o tooenable SSH de saudação da Internet:
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>CLI do Azure

Use Olá seguindo as etapas toocreate uma rede virtual que restringe o tráfego de entrada, mas permite que o tráfego de endereços IP de saudação exigido pelo HDInsight.

1. Saudação de uso após o comando toocreate um novo grupo de segurança de rede denominado `hdisecure`. Substituir **RESOURCEGROUPNAME** com grupo de recursos de saudação que contém Olá rede Virtual do Azure. Substituir **local** local hello (região) grupo Olá foi criado na.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Quando o grupo de saudação tiver sido criado, você recebe informações no novo grupo de saudação.

2. Use Olá tooadd regras toohello nova rede grupo de segurança que permitem a comunicação de entrada na porta 443 de saudação serviço de integridade e o gerenciamento do Azure HDInsight a seguir. Substituir **RESOURCEGROUPNAME** com nome Olá Olá do grupo de recursos que contém Olá rede Virtual do Azure.

    > [!IMPORTANT]
    > Altere os endereços IP hello usados na saudação de toomatch exemplo região do Azure que você está usando. Você pode encontrar essas informações no hello [HDInsight com rotas definidas pelo usuário e grupos de segurança de rede](#hdinsight-ip) seção.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve Olá identificador exclusivo para esse grupo de segurança de rede, use Olá comando a seguir:

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Este comando retorna um toohello semelhante valor texto a seguir:

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Use aspas duplas em torno de id no comando Olá se você não obtiver os resultados de saudação esperado.

4. Use Olá comando tooapply Olá segurança grupo tooa sub-rede a seguir. Substituir saudação __GUID__ e __RESOURCEGROUPNAME__ valores com hello aqueles retornados da etapa anterior hello. Substituir __VNETNAME__ e __SUBNETNAME__ com o nome de rede virtual hello e nome da sub-rede que você deseja toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Depois que esse comando for concluído, você pode instalar o HDInsight em Olá rede Virtual.

> [!IMPORTANT]
> Estas etapas só abra toohello HDInsight integridade e o gerenciamento de serviço de acesso no hello nuvem do Azure. Qualquer outro acesso toohello cluster HDInsight da saudação fora rede Virtual está bloqueada. tooenable acesso de rede virtual Olá externa, você deve adicionar regras de grupo de segurança de rede adicionais.
>
> Olá exemplo a seguir demonstra como acessar o tooenable SSH de saudação da Internet:
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> Exemplo: configuração de DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Resolução de nomes entre uma rede virtual e uma rede local conectada

Este exemplo faz Olá seguintes suposições:

* Você tem uma rede Virtual do Azure que é a rede de local de tooan conectado usando um gateway VPN.

* um servidor DNS personalizado Olá na rede virtual Olá está executando Linux ou Unix como sistema operacional de saudação.

* [Associar](https://www.isc.org/downloads/bind/) está instalado em um servidor DNS personalizado hello.

No servidor DNS de personalizado hello, na rede virtual hello:

1. Use o Azure PowerShell ou CLI do Azure toofind Olá sufixo DNS da rede virtual hello:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. No hello um servidor DNS personalizado para a rede virtual hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.local` arquivo:

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Substituir saudação `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor com o sufixo DNS de saudação da sua rede virtual.

    Essa configuração roteia todas as solicitações DNS para o sufixo DNS de saudação do resolvedor do hello rede virtual toohello recursiva do Azure.

2. No hello um servidor DNS personalizado para a rede virtual hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Substituir saudação `10.0.0.0/16` valor com o intervalo de endereços IP hello da sua rede virtual. Essa entrada permite endereços de solicitações de resolução de nomes dentro desse intervalo.

    * Adicionar intervalo de endereços IP hello de saudação local rede toohello `acl goodclients { ... }` seção.  entrada permite solicitações de resolução de nomes de recursos na rede de local de saudação.
    
    * Substituir valor Olá `192.168.0.1` com o endereço IP de saudação do servidor DNS local. Essa entrada encaminha todos os outros DNS solicitações toohello no servidor DNS local.

3. configuração de saudação toouse, reinicie a ligação. Por exemplo: `sudo service bind9 restart`.

4. Adicione um servidor DNS do encaminhador condicional toohello no local. Configure solicitações de toosend Olá encaminhador condicional para o sufixo DNS de saudação da etapa 1 toohello um servidor DNS personalizado.

    > [!NOTE]
    > Consulte a documentação de saudação do seu software DNS para obter informações específicas sobre como tooadd um encaminhador condicional.

Depois de concluir essas etapas, você pode conectar tooresources na rede usando nomes de domínio totalmente qualificado (FQDN). Agora você pode instalar o HDInsight em rede virtual hello.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Resolução de nomes entre duas redes virtuais conectadas

Este exemplo faz Olá seguintes suposições:

* Você tem duas Redes Virtuais do Azure conectadas usando um gateway de VPN ou um emparelhamento.

* um servidor DNS personalizado Olá em ambas as redes está executando o Linux ou Unix como sistema operacional de saudação.

* [Associar](https://www.isc.org/downloads/bind/) é instalado em servidores DNS personalizados hello.

1. Use o Azure PowerShell ou CLI do Azure toofind Olá sufixo DNS de ambas as redes virtuais:

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Saudação de uso após o texto como conteúdo de saudação do hello `/etc/bind/named.config.local` arquivo em um servidor DNS personalizado hello. Fazer essa alteração em um servidor DNS personalizado Olá em ambas as redes virtuais.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Substituir saudação `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valor com o sufixo DNS Olá Olá __outros__ rede virtual. Essa entrada encaminha solicitações para o sufixo DNS Olá Olá rede remota toohello personalizado DNS nessa rede.

3. Em servidores DNS de personalizado hello, em ambas as redes virtuais, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Substituir saudação `10.0.0.0/16` e `10.1.0.0/16` valores com hello IP endereço intervalos de suas redes virtuais. Essa entrada permite que os recursos em cada rede toomake solicitações de servidores DNS a saudação.

    Todas as solicitações que não são de sufixos DNS de saudação de redes virtuais da saudação (por exemplo, microsoft.com) é manipulados pelo resolvedor de Azure recursiva de saudação.

4. configuração de saudação toouse, reinicie a ligação. Por exemplo, `sudo service bind9 restart` em ambos os servidores DNS.

Depois de concluir essas etapas, você pode conectar tooresources na rede virtual do hello usando nomes de domínio totalmente qualificado (FQDN). Agora você pode instalar o HDInsight em rede virtual hello.

## <a name="next-steps"></a>Próximas etapas

* Para obter um exemplo de ponta a ponta de configuração de rede local do HDInsight tooconnect tooan, consulte [HDInsight conectar rede de local de tooan](./connect-on-premises-network.md).

* Para obter mais informações sobre redes virtuais do Azure, consulte Olá [visão geral da rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).

* Para obter mais informações sobre os Grupos de Segurança de Rede, veja [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).

* Para saber mais sobre rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).