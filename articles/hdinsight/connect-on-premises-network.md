---
title: rede de local do aaaConnect HDInsight tooyour - HDInsight do Azure | Microsoft Docs
description: "Saiba como toocreate uma HDInsight cluster em uma rede Virtual do Azure e, em seguida, conectá-lo a rede de local de tooyour. Saiba como tooconfigure a resolução de nomes entre HDInsight e sua rede local usando um servidor DNS personalizado."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>Conecte-se a rede de local de tooyour HDInsight

Saiba como tooconnect HDInsight tooyour local rede por meio de redes virtuais do Azure e um gateway de VPN. Este documento fornece informações para planejamento de como:

* Usar o HDInsight em uma rede Virtual do Azure que se conecta tooyour local rede.

* Configurando a resolução de nome DNS entre sua rede local e de rede virtual hello.

* Configurando a rede segurança grupos toorestrict internet acesso tooHDInsight.

* Portas fornecidas pelo HDInsight na rede virtual hello.

## <a name="create-hello-virtual-network-configuration"></a>Criar a configuração de rede Virtual Olá

> [!IMPORTANT]
> Se você estiver procurando orientação passo a passo sobre como conectar o HDInsight tooyour local de rede usando uma rede Virtual do Azure, consulte Olá [HDInsight conectar rede de local de tooyour](connect-on-premises-network.md) documento.

A seguir use Olá documentos toolearn como toocreate uma rede Virtual do Azure que está conectada tooyour local rede:
    
* [Usando Olá portal do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Usando o PowerShell do Azure](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Usar a CLI do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Configurar a resolução de nomes

tooallow HDInsight e recursos em Olá Unido toocommunicate de rede por nome, você deve executar Olá ações a seguir:

* Crie um servidor DNS personalizado no hello rede Virtual do Azure.

* Configure Olá rede virtual toouse Olá servidor DNS personalizado em vez do padrão de saudação do Azure recursiva resolvedor.

* Configure o encaminhamento entre um servidor DNS personalizado hello e seu servidor DNS no local.

Essa configuração permite que a saudação comportamento a seguir:

* Solicitações de nomes de domínio totalmente qualificado que têm o sufixo DNS Olá __para rede virtual Olá__ são encaminhadas a um servidor DNS personalizado toohello. um servidor DNS personalizado Hello, em seguida, encaminha toohello essas solicitações do Azure recursiva resolvedor, que retorna o endereço IP de saudação.

* Todas as outras solicitações são encaminhadas servidor DNS local toohello. Até mesmo solicitações para recursos da internet pública, como microsoft.com são encaminhadas toohello servidor DNS local para a resolução de nome.

No diagrama a seguir de Olá, linhas verdes são as solicitações para recursos que terminam no sufixo DNS de saudação da rede virtual hello. Linhas azuis são Olá de solicitações para recursos na rede de local de saudação ou na internet pública.

![Diagrama de como as solicitações de DNS são resolvidas na configuração de saudação usada neste documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Criar um servidor DNS personalizado

> [!IMPORTANT]
> Você deve criar e configurar o servidor DNS de saudação antes de instalar o HDInsight em rede virtual hello.

toocreate uma VM do Linux que usa Olá [associar](https://www.isc.org/downloads/bind/) software DNS, Olá use as etapas a seguir:

> [!NOTE]
> Olá, etapas a seguir usam Olá [portal do Azure](https://portal.azure.com) toocreate uma máquina Virtual do Azure. Para outra maneiras toocreate uma máquina virtual, consulte Olá [criar VM - CLI do Azure](../virtual-machines/linux/quick-create-cli.md) e [criar VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documentos.

1. De saudação [portal do Azure](https://portal.azure.com), selecione  __+__ , __de computação__, e __Ubuntu Server 16.04 LTS__.

    ![Criar uma máquina virtual do Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. De saudação __Noções básicas de__ seção, digite Olá informações a seguir:

    * __Nome__: um nome amigável que identifica esta máquina virtual. Por exemplo, __DNSProxy__.
    * __Nome de usuário__: nome de saudação do hello conta SSH.
    * __Chave pública SSH__ ou __senha__: Olá o método de autenticação para Olá conta SSH. É recomendável usar as chaves públicas, pois elas são mais seguras. Para obter mais informações, consulte Olá [criar e usar chaves SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.
    * __Grupo de recursos__: selecione __usar existente__e, em seguida, selecione o grupo de recursos de saudação que contém a rede virtual de saudação criado anteriormente.
    * __Local__: selecione Olá mesmo local da rede virtual hello.

    ![Configuração básica da máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    Deixe outras entradas no hello valores padrão e, em seguida, selecione __Okey__.

3. De saudação __escolher um tamanho de__ seção, o tamanho da VM Olá select. Para este tutorial, selecione Olá menor e opção de custo mais baixo. toocontinue, use Olá __selecione__ botão.

4. De saudação __configurações__ seção, digite Olá informações a seguir:

    * __Rede virtual__: selecione Olá rede virtual que você criou anteriormente.

    * __Subrede__: selecione saudação padrão sub-rede da rede virtual hello. Fazer __não__ selecione Olá sub-rede usada pelo gateway VPN hello.

    * __Conta de armazenamento de diagnóstico__: selecione uma conta de armazenamento existente ou crie uma nova.

    ![Configurações de rede virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    Deixe Olá outras entradas no valor de padrão de saudação e selecione __Okey__ toocontinue.

5. De saudação __compra__ seção, selecione Olá __compra__ máquina virtual do botão toocreate hello.

6. Depois que a máquina virtual de saudação tiver sido criada, seu __visão geral__ é exibida. Na lista de Olá Olá esquerda, selecione __propriedades__. Salvar Olá __endereço IP público__ e __endereço IP privado__ valores. Ele será usado na próxima seção, Olá.

    ![Endereços IP públicos e privados](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Instalar e configurar o Bind (software DNS)

1. Usar SSH tooconnect toohello __endereço IP público__ da máquina virtual de saudação. saudação de exemplo a seguir se conecta a máquina virtual de tooa em 40.68.254.142:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Substituir `sshuser` com hello SSH conta de usuário especificado ao criar o cluster de saudação.

    > [!NOTE]
    > Há uma variedade de saudação do tooobtain maneiras `ssh` utilitário. No Linux, Unix e macOS, ele é fornecido como parte do sistema operacional de saudação. Se você estiver usando o Windows, considere uma saudação as opções a seguir:
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [Bash no Ubuntu no Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall Bind, use Olá comandos da sessão SSH Olá a seguir:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure Bind tooforward nome resolução solicitações tooyour local no servidor DNS, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Substituir valores Olá Olá `goodclients` seção com intervalo de endereços IP Olá Olá uma rede virtual e rede local. Esta seção define os endereços de saudação que esse servidor DNS aceita solicitações de.
    >
    > Substituir saudação `192.168.0.1` entrada hello `forwarders` seção com o endereço IP de saudação do servidor DNS local. Este tooyour solicitações DNS de rotas de entrada local do servidor DNS para resolução.

    tooedit esse arquivo, use Olá comando a seguir:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    arquivo de saudação toosave, use __Ctrl + X__, __Y__e, em seguida, __Enter__.

4. Da sessão SSH hello, use Olá comando a seguir:

    ```bash
    hostname -f
    ```

    Este comando retorna um toohello semelhante valor texto a seguir:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Olá `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texto é hello __sufixo DNS__ para essa rede virtual. Salve esse valor, pois ele é usado mais tarde.

5. tooconfigure Bind tooresolve nomes DNS para os recursos na rede virtual do hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.local` arquivo:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Você deve substituir Olá `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` com o sufixo DNS Olá recuperado anteriormente.

    tooedit esse arquivo, use Olá comando a seguir:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    arquivo de saudação toosave, use __Ctrl + X__, __Y__e, em seguida, __Enter__.

6. toostart Bind, use Olá comando a seguir:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify associar pode resolver nomes de saudação de recursos em sua rede local, use Olá comandos a seguir:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Substituir `dns.mynetwork.net` com o nome de domínio totalmente qualificado (FQDN) Olá de um recurso em sua rede local.
    >
    > Substituir `10.0.0.4` com hello __endereço IP interno__ do seu servidor DNS personalizado na rede virtual hello.

    resposta de saudação aparece semelhante toohello texto a seguir:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Configurar Olá rede virtual toouse Olá servidor DNS personalizado

tooconfigure Olá rede virtual toouse Olá personalizado servidor DNS Olá resolução recursiva do Azure, em vez de usar Olá etapas a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com), selecione a rede virtual hello e, em seguida, selecione __servidores DNS__.

2. Selecione __personalizado__e digite Olá __endereço IP interno__ de um servidor DNS personalizado hello. Por fim, selecione __Salvar__.

    ![Definir um servidor DNS personalizado Olá para rede Olá](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Configurar o servidor DNS local Olá

Na seção anterior do hello, você configurou Olá personalizado DNS server tooforward solicitações toohello no servidor DNS local. Em seguida, configure Olá local DNS server tooforward solicitações toohello um servidor DNS personalizado.

Para etapas específicas sobre como tooconfigure seu servidor DNS, consulte a documentação de saudação do seu software de servidor DNS. Pesquisar para obter etapas sobre como Olá tooconfigure um __encaminhador condicional__.

Um encaminhador condicional só encaminha solicitações para um sufixo DNS específico. Nesse caso, você deve configurar um encaminhador de sufixo DNS de saudação da rede virtual hello. Solicitações para esse sufixo devem ser encaminhadas toohello endereço IP de um servidor DNS personalizado hello. 

Olá, texto a seguir é um exemplo de uma configuração de encaminhador condicional de saudação **associar** software DNS:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Para obter informações sobre como usar o DNS na **Windows Server 2016**, consulte Olá [DnsServerConditionalForwarderZone adicionar](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentação...

Quando você tiver configurado o servidor DNS local hello, você pode usar `nslookup` de saudação tooverify de rede de local que você pode resolver nomes na rede virtual hello. saudação de exemplo a seguir 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

Este exemplo usa Olá servidor DNS local 196.168.0.4 tooresolve nome de saudação do servidor DNS personalizado hello. Substitua o endereço IP de saudação com Olá para o servidor DNS local hello. Substituir saudação `dnsproxy` endereço com nome de domínio totalmente qualificado de saudação do servidor DNS personalizado hello.

## <a name="optional-control-network-traffic"></a>Opcional: controlar o tráfego de rede

Você pode usar grupos de segurança de rede (NSG) ou o tráfego de rede toocontrol rotas definidas pelo usuário (UDR). Os NSGs permitem toofilter de entrada e saída de tráfego e permitir ou negar o tráfego de saudação. UDRs permitem toocontrol como fluxos de tráfego entre os recursos na rede virtual Olá Olá internet e Olá rede local.

> [!WARNING]
> O HDInsight requer acesso de entrada de endereços IP específicos no hello nuvem do Azure e acesso irrestrito de saída. Ao usar o tráfego de toocontrol NSGs ou UDRs, você deve executar Olá etapas a seguir:
>
> 1. Localize Olá endereços IP para o local de saudação que contém sua rede virtual. Para obter uma lista de IPs necessários por localização, consulte [Endereços IP necessários](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Permitir tráfego de entrada de endereços IP de saudação.
>
>    * __NSG__: permitir __entrada__ o tráfego na porta __443__ de saudação __Internet__.
>    * __UDR__: Olá conjunto __próximo salto__ tipo de saudação too__Internet__ de rota.

Para obter um exemplo do uso do Azure PowerShell ou CLI do Azure de saudação toocreate NSGs, consulte Olá [HDInsight estender com redes virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.

## <a name="create-hello-hdinsight-cluster"></a>Criar cluster do HDInsight Olá

> [!WARNING]
> Você deve configurar um servidor DNS personalizado Olá antes de instalar o HDInsight na rede virtual hello.

Olá Use as etapas em Olá [criar um cluster HDInsight usando o portal do Azure de saudação](./hdinsight-hadoop-create-linux-clusters-portal.md) documento toocreate um cluster HDInsight.

> [!WARNING]
> * Durante a criação do cluster, você deve escolher o local de saudação que contém sua rede virtual.
>
> * Em Olá __configurações avançadas__ parte da configuração, você deve selecionar uma rede virtual hello e sub-rede que você criou anteriormente.

## <a name="connecting-toohdinsight"></a>Conexão tooHDInsight

Mais documentação no HDInsight supõe que você tenha o cluster de toohello de acesso sobre Olá internet. Por exemplo, você pode se conectar a cluster toohello em https://CLUSTERNAME.azurehdinsight.net. Esse endereço usa o gateway pública hello, que não está disponível se você tiver usado os NSGs ou UDRs toorestrict acesso Olá da internet.

toodirectly conectar tooHDInsight por meio da rede virtual hello, use Olá etapas a seguir:

1. toodiscover Olá interno nomes totalmente qualificados de nós de cluster do HDInsight Olá, use um dos métodos a seguir de saudação:

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

2. porta de saudação toodetermine que um serviço estiver disponível, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

    > [!IMPORTANT]
    > Alguns serviços hospedados em nós de cabeçalho hello serão apenas ativos em um nó por vez. Se você tentar acessar um serviço em um nó de cabeçalho e ele falhar, alterne toohello outro nó principal.
    >
    > Por exemplo, o Ambari só está ativo em um nó de cabeçalho por vez. Se você tentar acessar o Ambari em um nó de cabeçalho e retorna um erro 404, em seguida, ele é executado em Olá outro nó principal.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Para obter mais informações sobre redes virtuais do Azure, consulte Olá [visão geral da rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).

* Para obter mais informações sobre os Grupos de Segurança de Rede, veja [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).

* Para saber mais sobre rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).
