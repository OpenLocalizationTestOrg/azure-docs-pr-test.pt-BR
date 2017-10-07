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
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="1fcbc-104">Conecte-se a rede de local de tooyour HDInsight</span><span class="sxs-lookup"><span data-stu-id="1fcbc-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="1fcbc-105">Saiba como tooconnect HDInsight tooyour local rede por meio de redes virtuais do Azure e um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="1fcbc-106">Este documento fornece informações para planejamento de como:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-106">This document provides planning information on:</span></span>

* <span data-ttu-id="1fcbc-107">Usar o HDInsight em uma rede Virtual do Azure que se conecta tooyour local rede.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="1fcbc-108">Configurando a resolução de nome DNS entre sua rede local e de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="1fcbc-109">Configurando a rede segurança grupos toorestrict internet acesso tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="1fcbc-110">Portas fornecidas pelo HDInsight na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="1fcbc-111">Criar a configuração de rede Virtual Olá</span><span class="sxs-lookup"><span data-stu-id="1fcbc-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fcbc-112">Se você estiver procurando orientação passo a passo sobre como conectar o HDInsight tooyour local de rede usando uma rede Virtual do Azure, consulte Olá [HDInsight conectar rede de local de tooyour](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="1fcbc-113">A seguir use Olá documentos toolearn como toocreate uma rede Virtual do Azure que está conectada tooyour local rede:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="1fcbc-114">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1fcbc-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="1fcbc-115">Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="1fcbc-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="1fcbc-116">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1fcbc-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="1fcbc-117">Configurar a resolução de nomes</span><span class="sxs-lookup"><span data-stu-id="1fcbc-117">Configure name resolution</span></span>

<span data-ttu-id="1fcbc-118">tooallow HDInsight e recursos em Olá Unido toocommunicate de rede por nome, você deve executar Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="1fcbc-119">Crie um servidor DNS personalizado no hello rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="1fcbc-120">Configure Olá rede virtual toouse Olá servidor DNS personalizado em vez do padrão de saudação do Azure recursiva resolvedor.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="1fcbc-121">Configure o encaminhamento entre um servidor DNS personalizado hello e seu servidor DNS no local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="1fcbc-122">Essa configuração permite que a saudação comportamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="1fcbc-123">Solicitações de nomes de domínio totalmente qualificado que têm o sufixo DNS Olá __para rede virtual Olá__ são encaminhadas a um servidor DNS personalizado toohello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="1fcbc-124">um servidor DNS personalizado Hello, em seguida, encaminha toohello essas solicitações do Azure recursiva resolvedor, que retorna o endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="1fcbc-125">Todas as outras solicitações são encaminhadas servidor DNS local toohello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="1fcbc-126">Até mesmo solicitações para recursos da internet pública, como microsoft.com são encaminhadas toohello servidor DNS local para a resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="1fcbc-127">No diagrama a seguir de Olá, linhas verdes são as solicitações para recursos que terminam no sufixo DNS de saudação da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="1fcbc-128">Linhas azuis são Olá de solicitações para recursos na rede de local de saudação ou na internet pública.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagrama de como as solicitações de DNS são resolvidas na configuração de saudação usada neste documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="1fcbc-130">Criar um servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="1fcbc-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1fcbc-131">Você deve criar e configurar o servidor DNS de saudação antes de instalar o HDInsight em rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="1fcbc-132">toocreate uma VM do Linux que usa Olá [associar](https://www.isc.org/downloads/bind/) software DNS, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="1fcbc-133">Olá, etapas a seguir usam Olá [portal do Azure](https://portal.azure.com) toocreate uma máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="1fcbc-134">Para outra maneiras toocreate uma máquina virtual, consulte Olá [criar VM - CLI do Azure](../virtual-machines/linux/quick-create-cli.md) e [criar VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documentos.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="1fcbc-135">De saudação [portal do Azure](https://portal.azure.com), selecione  __+__ , __de computação__, e __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Criar uma máquina virtual do Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="1fcbc-137">De saudação __Noções básicas de__ seção, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="1fcbc-138">__Nome__: um nome amigável que identifica esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="1fcbc-139">Por exemplo, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="1fcbc-140">__Nome de usuário__: nome de saudação do hello conta SSH.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="1fcbc-141">__Chave pública SSH__ ou __senha__: Olá o método de autenticação para Olá conta SSH.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="1fcbc-142">É recomendável usar as chaves públicas, pois elas são mais seguras.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="1fcbc-143">Para obter mais informações, consulte Olá [criar e usar chaves SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="1fcbc-144">__Grupo de recursos__: selecione __usar existente__e, em seguida, selecione o grupo de recursos de saudação que contém a rede virtual de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="1fcbc-145">__Local__: selecione Olá mesmo local da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Configuração básica da máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="1fcbc-147">Deixe outras entradas no hello valores padrão e, em seguida, selecione __Okey__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="1fcbc-148">De saudação __escolher um tamanho de__ seção, o tamanho da VM Olá select.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="1fcbc-149">Para este tutorial, selecione Olá menor e opção de custo mais baixo.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="1fcbc-150">toocontinue, use Olá __selecione__ botão.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="1fcbc-151">De saudação __configurações__ seção, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="1fcbc-152">__Rede virtual__: selecione Olá rede virtual que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="1fcbc-153">__Subrede__: selecione saudação padrão sub-rede da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="1fcbc-154">Fazer __não__ selecione Olá sub-rede usada pelo gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="1fcbc-155">__Conta de armazenamento de diagnóstico__: selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Configurações de rede virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="1fcbc-157">Deixe Olá outras entradas no valor de padrão de saudação e selecione __Okey__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="1fcbc-158">De saudação __compra__ seção, selecione Olá __compra__ máquina virtual do botão toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="1fcbc-159">Depois que a máquina virtual de saudação tiver sido criada, seu __visão geral__ é exibida.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="1fcbc-160">Na lista de Olá Olá esquerda, selecione __propriedades__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="1fcbc-161">Salvar Olá __endereço IP público__ e __endereço IP privado__ valores.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="1fcbc-162">Ele será usado na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-162">It will be used in hello next section.</span></span>

    ![Endereços IP públicos e privados](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="1fcbc-164">Instalar e configurar o Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="1fcbc-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="1fcbc-165">Usar SSH tooconnect toohello __endereço IP público__ da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="1fcbc-166">saudação de exemplo a seguir se conecta a máquina virtual de tooa em 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="1fcbc-167">Substituir `sshuser` com hello SSH conta de usuário especificado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1fcbc-168">Há uma variedade de saudação do tooobtain maneiras `ssh` utilitário.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="1fcbc-169">No Linux, Unix e macOS, ele é fornecido como parte do sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="1fcbc-170">Se você estiver usando o Windows, considere uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="1fcbc-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="1fcbc-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="1fcbc-172">Bash no Ubuntu no Windows 10</span><span class="sxs-lookup"><span data-stu-id="1fcbc-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="1fcbc-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="1fcbc-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="1fcbc-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="1fcbc-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="1fcbc-175">tooinstall Bind, use Olá comandos da sessão SSH Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="1fcbc-176">tooconfigure Bind tooforward nome resolução solicitações tooyour local no servidor DNS, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.options` arquivo:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

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
    > <span data-ttu-id="1fcbc-177">Substituir valores Olá Olá `goodclients` seção com intervalo de endereços IP Olá Olá uma rede virtual e rede local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="1fcbc-178">Esta seção define os endereços de saudação que esse servidor DNS aceita solicitações de.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="1fcbc-179">Substituir saudação `192.168.0.1` entrada hello `forwarders` seção com o endereço IP de saudação do servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="1fcbc-180">Este tooyour solicitações DNS de rotas de entrada local do servidor DNS para resolução.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="1fcbc-181">tooedit esse arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="1fcbc-182">arquivo de saudação toosave, use __Ctrl + X__, __Y__e, em seguida, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="1fcbc-183">Da sessão SSH hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="1fcbc-184">Este comando retorna um toohello semelhante valor texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="1fcbc-185">Olá `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texto é hello __sufixo DNS__ para essa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="1fcbc-186">Salve esse valor, pois ele é usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="1fcbc-187">tooconfigure Bind tooresolve nomes DNS para os recursos na rede virtual do hello, use Olá depois do texto como conteúdo de saudação do hello `/etc/bind/named.conf.local` arquivo:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="1fcbc-188">Você deve substituir Olá `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` com o sufixo DNS Olá recuperado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="1fcbc-189">tooedit esse arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="1fcbc-190">arquivo de saudação toosave, use __Ctrl + X__, __Y__e, em seguida, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="1fcbc-191">toostart Bind, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="1fcbc-192">tooverify associar pode resolver nomes de saudação de recursos em sua rede local, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1fcbc-193">Substituir `dns.mynetwork.net` com o nome de domínio totalmente qualificado (FQDN) Olá de um recurso em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="1fcbc-194">Substituir `10.0.0.4` com hello __endereço IP interno__ do seu servidor DNS personalizado na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="1fcbc-195">resposta de saudação aparece semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="1fcbc-196">Configurar Olá rede virtual toouse Olá servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="1fcbc-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="1fcbc-197">tooconfigure Olá rede virtual toouse Olá personalizado servidor DNS Olá resolução recursiva do Azure, em vez de usar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="1fcbc-198">Em Olá [portal do Azure](https://portal.azure.com), selecione a rede virtual hello e, em seguida, selecione __servidores DNS__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="1fcbc-199">Selecione __personalizado__e digite Olá __endereço IP interno__ de um servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="1fcbc-200">Por fim, selecione __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-200">Finally, select __Save__.</span></span>

    ![Definir um servidor DNS personalizado Olá para rede Olá](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="1fcbc-202">Configurar o servidor DNS local Olá</span><span class="sxs-lookup"><span data-stu-id="1fcbc-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="1fcbc-203">Na seção anterior do hello, você configurou Olá personalizado DNS server tooforward solicitações toohello no servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="1fcbc-204">Em seguida, configure Olá local DNS server tooforward solicitações toohello um servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="1fcbc-205">Para etapas específicas sobre como tooconfigure seu servidor DNS, consulte a documentação de saudação do seu software de servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="1fcbc-206">Pesquisar para obter etapas sobre como Olá tooconfigure um __encaminhador condicional__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="1fcbc-207">Um encaminhador condicional só encaminha solicitações para um sufixo DNS específico.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="1fcbc-208">Nesse caso, você deve configurar um encaminhador de sufixo DNS de saudação da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="1fcbc-209">Solicitações para esse sufixo devem ser encaminhadas toohello endereço IP de um servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="1fcbc-210">Olá, texto a seguir é um exemplo de uma configuração de encaminhador condicional de saudação **associar** software DNS:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="1fcbc-211">Para obter informações sobre como usar o DNS na **Windows Server 2016**, consulte Olá [DnsServerConditionalForwarderZone adicionar](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentação...</span><span class="sxs-lookup"><span data-stu-id="1fcbc-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="1fcbc-212">Quando você tiver configurado o servidor DNS local hello, você pode usar `nslookup` de saudação tooverify de rede de local que você pode resolver nomes na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="1fcbc-213">saudação de exemplo a seguir</span><span class="sxs-lookup"><span data-stu-id="1fcbc-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="1fcbc-214">Este exemplo usa Olá servidor DNS local 196.168.0.4 tooresolve nome de saudação do servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="1fcbc-215">Substitua o endereço IP de saudação com Olá para o servidor DNS local hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="1fcbc-216">Substituir saudação `dnsproxy` endereço com nome de domínio totalmente qualificado de saudação do servidor DNS personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="1fcbc-217">Opcional: controlar o tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="1fcbc-217">Optional: Control network traffic</span></span>

<span data-ttu-id="1fcbc-218">Você pode usar grupos de segurança de rede (NSG) ou o tráfego de rede toocontrol rotas definidas pelo usuário (UDR).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="1fcbc-219">Os NSGs permitem toofilter de entrada e saída de tráfego e permitir ou negar o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="1fcbc-220">UDRs permitem toocontrol como fluxos de tráfego entre os recursos na rede virtual Olá Olá internet e Olá rede local.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="1fcbc-221">O HDInsight requer acesso de entrada de endereços IP específicos no hello nuvem do Azure e acesso irrestrito de saída.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="1fcbc-222">Ao usar o tráfego de toocontrol NSGs ou UDRs, você deve executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="1fcbc-223">Localize Olá endereços IP para o local de saudação que contém sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="1fcbc-224">Para obter uma lista de IPs necessários por localização, consulte [Endereços IP necessários](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="1fcbc-225">Permitir tráfego de entrada de endereços IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="1fcbc-226">__NSG__: permitir __entrada__ o tráfego na porta __443__ de saudação __Internet__.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="1fcbc-227">__UDR__: Olá conjunto __próximo salto__ tipo de saudação too__Internet__ de rota.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="1fcbc-228">Para obter um exemplo do uso do Azure PowerShell ou CLI do Azure de saudação toocreate NSGs, consulte Olá [HDInsight estender com redes virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="1fcbc-229">Criar cluster do HDInsight Olá</span><span class="sxs-lookup"><span data-stu-id="1fcbc-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="1fcbc-230">Você deve configurar um servidor DNS personalizado Olá antes de instalar o HDInsight na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="1fcbc-231">Olá Use as etapas em Olá [criar um cluster HDInsight usando o portal do Azure de saudação](./hdinsight-hadoop-create-linux-clusters-portal.md) documento toocreate um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="1fcbc-232">Durante a criação do cluster, você deve escolher o local de saudação que contém sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="1fcbc-233">Em Olá __configurações avançadas__ parte da configuração, você deve selecionar uma rede virtual hello e sub-rede que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="1fcbc-234">Conexão tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="1fcbc-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="1fcbc-235">Mais documentação no HDInsight supõe que você tenha o cluster de toohello de acesso sobre Olá internet.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="1fcbc-236">Por exemplo, você pode se conectar a cluster toohello em https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1fcbc-237">Esse endereço usa o gateway pública hello, que não está disponível se você tiver usado os NSGs ou UDRs toorestrict acesso Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="1fcbc-238">toodirectly conectar tooHDInsight por meio da rede virtual hello, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="1fcbc-239">toodiscover Olá interno nomes totalmente qualificados de nós de cluster do HDInsight Olá, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="1fcbc-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

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

2. <span data-ttu-id="1fcbc-240">porta de saudação toodetermine que um serviço estiver disponível, consulte Olá [portas usadas por serviços de Hadoop no HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1fcbc-241">Alguns serviços hospedados em nós de cabeçalho hello serão apenas ativos em um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="1fcbc-242">Se você tentar acessar um serviço em um nó de cabeçalho e ele falhar, alterne toohello outro nó principal.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="1fcbc-243">Por exemplo, o Ambari só está ativo em um nó de cabeçalho por vez.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="1fcbc-244">Se você tentar acessar o Ambari em um nó de cabeçalho e retorna um erro 404, em seguida, ele é executado em Olá outro nó principal.</span><span class="sxs-lookup"><span data-stu-id="1fcbc-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fcbc-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fcbc-245">Next steps</span></span>

* <span data-ttu-id="1fcbc-246">Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="1fcbc-247">Para obter mais informações sobre redes virtuais do Azure, consulte Olá [visão geral da rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="1fcbc-248">Para obter mais informações sobre os Grupos de Segurança de Rede, veja [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="1fcbc-249">Para saber mais sobre rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fcbc-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
