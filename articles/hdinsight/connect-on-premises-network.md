---
title: "Conecte o HDInsight à sua rede local – Azure HDInsight | Microsoft Docs"
description: "Saiba como criar um cluster HDInsight em uma Rede Virtual do Azure e, em seguida, conecte-o à sua rede local. Saiba como configurar a resolução de nomes entre HDInsight e sua rede local usando um servidor DNS personalizado."
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
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="af300-104">Conectar o HDInsight à sua rede local</span><span class="sxs-lookup"><span data-stu-id="af300-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="af300-105">Saiba como conectar o HDInsight à sua rede local por meio de redes virtuais do Azure e de um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="af300-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="af300-106">Este documento fornece informações para planejamento de como:</span><span class="sxs-lookup"><span data-stu-id="af300-106">This document provides planning information on:</span></span>

* <span data-ttu-id="af300-107">usar o HDInsight em uma Rede Virtual do Azure que se conecta à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="af300-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="af300-108">configurar a resolução de nome DNS entre a rede virtual e sua rede local.</span><span class="sxs-lookup"><span data-stu-id="af300-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="af300-109">configurar grupos de segurança de rede para restringir o acesso à Internet para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="af300-110">Portas fornecidas pelo HDInsight na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="af300-111">Criar a configuração de rede Virtual</span><span class="sxs-lookup"><span data-stu-id="af300-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af300-112">Se estiver buscando orientações passo a passo sobre como conectar o HDInsight à sua rede local usando uma Rede Virtual do Azure, consulte o documento [Conectar o HDInsight à sua rede local](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="af300-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="af300-113">Use os documentos a seguir para aprender a criar uma Rede Virtual do Azure conectada à sua rede local:</span><span class="sxs-lookup"><span data-stu-id="af300-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="af300-114">Usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="af300-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="af300-115">Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="af300-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="af300-116">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="af300-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="af300-117">Configurar a resolução de nomes</span><span class="sxs-lookup"><span data-stu-id="af300-117">Configure name resolution</span></span>

<span data-ttu-id="af300-118">Para permitir que o HDInsight e os recursos na rede ingressada se comuniquem por nome, você deve executar as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="af300-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="af300-119">Crie um servidor DNS personalizado na Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="af300-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="af300-120">Configure a rede virtual para usar o servidor DNS personalizado em vez do resolvedor recursivo padrão do Azure.</span><span class="sxs-lookup"><span data-stu-id="af300-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="af300-121">Configure o encaminhamento entre o servidor DNS personalizado e seu servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="af300-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="af300-122">Essa configuração habilita o seguinte comportamento:</span><span class="sxs-lookup"><span data-stu-id="af300-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="af300-123">Solicitações de nomes de domínio totalmente qualificados que têm o sufixo DNS __para a rede virtual__ são encaminhados para o servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="af300-124">O servidor DNS personalizado, em seguida, encaminha essas solicitações para o resolvedor recursivo do Azure, que retorna o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="af300-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="af300-125">Todas as outras solicitações são encaminhadas ao servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="af300-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="af300-126">Até mesmo solicitações para recursos da Internet pública como microsoft.com são encaminhadas ao servidor DNS local para a resolução de nomes.</span><span class="sxs-lookup"><span data-stu-id="af300-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="af300-127">No diagrama a seguir, linhas verdes são solicitações de recursos que terminam com o sufixo DNS da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="af300-128">Linhas azuis são as solicitações para recursos na rede local ou na Internet pública.</span><span class="sxs-lookup"><span data-stu-id="af300-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagrama de como as solicitações DNS são resolvidas na configuração usada neste documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="af300-130">Criar um servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="af300-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af300-131">Você deve criar e configurar o servidor DNS antes de instalar o HDInsight na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="af300-132">Para criar uma VM Linux que usa o software DNS [Bind](https://www.isc.org/downloads/bind/), use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="af300-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="af300-133">Use as etapas a seguir no [Portal do Azure](https://portal.azure.com) para criar uma Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="af300-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="af300-134">Para outras maneiras de criar uma máquina virtual, consulte os documentos [Criar VM – CLI do Azure](../virtual-machines/linux/quick-create-cli.md) e [Criar VM – Azure PowerShell](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af300-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="af300-135">Do [portal do Azure](https://portal.azure.com), selecione __+__, __Computação__ e __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="af300-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Criar uma máquina virtual do Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="af300-137">Na seção __Básico__, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="af300-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="af300-138">__Nome__: um nome amigável que identifica esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="af300-139">Por exemplo, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="af300-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="af300-140">__Nome de usuário__: o nome da conta SSH.</span><span class="sxs-lookup"><span data-stu-id="af300-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="af300-141">__Chave pública de SSH__ ou __Senha__: o método de autenticação para a conta SSH.</span><span class="sxs-lookup"><span data-stu-id="af300-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="af300-142">É recomendável usar as chaves públicas, pois elas são mais seguras.</span><span class="sxs-lookup"><span data-stu-id="af300-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="af300-143">Para obter mais informações, consulte o documento [Criar e usar chaves SSH para VMs Linux](../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="af300-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="af300-144">__Grupo de recursos__: selecione __usar existente__ e, em seguida, selecione o grupo de recursos que contém a rede virtual criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af300-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="af300-145">Para __Local__, selecione o mesmo local da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Configuração básica da máquina virtual](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="af300-147">Deixe outras entradas com os valores padrão e, em seguida, selecione __OK__.</span><span class="sxs-lookup"><span data-stu-id="af300-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="af300-148">Na seção __Escolher um tamanho__, selecione o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="af300-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="af300-149">Para este tutorial, selecione a opção menor e com custo mais baixo.</span><span class="sxs-lookup"><span data-stu-id="af300-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="af300-150">Para continuar, use o botão __Selecionar__.</span><span class="sxs-lookup"><span data-stu-id="af300-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="af300-151">Na seção __Configurações__, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="af300-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="af300-152">__Rede virtual__: selecione a rede virtual que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af300-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="af300-153">__Sub-rede__: selecione a sub-rede padrão para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="af300-154">__Não__ selecione a sub-rede usada pelo gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="af300-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="af300-155">__Conta de armazenamento de diagnóstico__: selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="af300-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Configurações de rede virtual](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="af300-157">Deixe as outras entradas com os valores padrão e, em seguida, selecione __OK__ para continuar.</span><span class="sxs-lookup"><span data-stu-id="af300-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="af300-158">Na seção __Comprar__, selecione o botão __Comprar__ para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="af300-159">Quando a máquina virtual tiver sido criada, sua seção __Visão geral__ será exibida.</span><span class="sxs-lookup"><span data-stu-id="af300-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="af300-160">Na lista à esquerda, selecione __Propriedades__.</span><span class="sxs-lookup"><span data-stu-id="af300-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="af300-161">Salve os valores de __Endereço IP público__ e __Endereço IP privado__.</span><span class="sxs-lookup"><span data-stu-id="af300-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="af300-162">Eles serão usados na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="af300-162">It will be used in the next section.</span></span>

    ![Endereços IP públicos e privados](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="af300-164">Instalar e configurar o Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="af300-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="af300-165">Use SSH para conexão com o __endereço IP público__ da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="af300-166">O exemplo a seguir se conecta a uma máquina virtual em 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="af300-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="af300-167">Substitua `sshuser` pela conta de usuário SSH que você especificou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="af300-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af300-168">Há uma variedade de maneiras para obter o utilitário `ssh`.</span><span class="sxs-lookup"><span data-stu-id="af300-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="af300-169">No Linux, Unix e macOS, ele é fornecido como parte do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="af300-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="af300-170">Se você estiver usando o Windows, considere uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="af300-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="af300-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="af300-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="af300-172">Bash no Ubuntu no Windows 10</span><span class="sxs-lookup"><span data-stu-id="af300-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="af300-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="af300-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="af300-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="af300-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="af300-175">Para instalar o Bind, use os seguintes comandos da sessão SSH:</span><span class="sxs-lookup"><span data-stu-id="af300-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="af300-176">Para configurar o Bind para encaminhar solicitações de resolução de nomes para o servidor DNS local, use o seguinte texto como o conteúdo do arquivo `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="af300-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="af300-177">Substitua os valores na seção `goodclients` com o intervalo de endereços IP da rede virtual e rede local.</span><span class="sxs-lookup"><span data-stu-id="af300-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="af300-178">Esta seção define os endereços dos quais esse servidor DNS aceita solicitações.</span><span class="sxs-lookup"><span data-stu-id="af300-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="af300-179">Substitua a entrada `192.168.0.1` na seção `forwarders` pelo endereço IP do servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="af300-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="af300-180">Essa entrada roteia solicitações DNS para o servidor DNS local para resolução.</span><span class="sxs-lookup"><span data-stu-id="af300-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="af300-181">Para editar esse arquivo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="af300-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="af300-182">Para salvar o arquivo, use __Ctrl+X__, __Y__ e, em seguida, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="af300-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="af300-183">Na sessão do SSH, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="af300-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="af300-184">Esse comando retorna um valor semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="af300-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="af300-185">O texto `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` é o __sufixo DNS__ para essa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="af300-186">Salve esse valor, pois ele é usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="af300-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="af300-187">Para configurar o Bind para resolver nomes DNS para os recursos na rede virtual, use o seguinte texto como o conteúdo do arquivo `/etc/bind/named.conf.local`:</span><span class="sxs-lookup"><span data-stu-id="af300-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="af300-188">Você deve substituir o `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` com o sufixo DNS que você recuperou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af300-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="af300-189">Para editar esse arquivo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="af300-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="af300-190">Para salvar o arquivo, use __Ctrl+X__, __Y__ e, em seguida, __Enter__.</span><span class="sxs-lookup"><span data-stu-id="af300-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="af300-191">Para iniciar o Bind, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="af300-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="af300-192">Para verificar se o Bind pode resolver os nomes de recursos em sua rede local, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="af300-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="af300-193">Substitua `dns.mynetwork.net` pelo FQDN (nome de domínio totalmente qualificado) de um recurso em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="af300-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="af300-194">Substitua `10.0.0.4` pelo __endereço IP interno__ do seu servidor DNS personalizado na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="af300-195">A resposta aparece semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="af300-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="af300-196">Configurar a rede virtual para usar o servidor DNS personalizado</span><span class="sxs-lookup"><span data-stu-id="af300-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="af300-197">Para configure a rede virtual para usar o servidor DNS personalizado em vez do resolvedor recursivo do Azure, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="af300-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="af300-198">No [portal do Azure](https://portal.azure.com), selecione a rede virtual e, em seguida, selecione __Servidores DNS__.</span><span class="sxs-lookup"><span data-stu-id="af300-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="af300-199">Selecione __Personalizado__e insira o __endereço IP interno__ do servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="af300-200">Por fim, selecione __Salvar__.</span><span class="sxs-lookup"><span data-stu-id="af300-200">Finally, select __Save__.</span></span>

    ![Definir o servidor DNS personalizado para a rede](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="af300-202">Configurar o servidor DNS local</span><span class="sxs-lookup"><span data-stu-id="af300-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="af300-203">Na seção anterior, você configurou o servidor DNS personalizado para encaminhar solicitações para o servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="af300-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="af300-204">Em seguida, você deve configurar o servidor DNS local para encaminhar solicitações para o servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="af300-205">Para etapas específicas sobre como configurar seu servidor DNS, consulte a documentação do seu software para servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="af300-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="af300-206">Procure as etapas sobre como configurar um __encaminhador condicional__.</span><span class="sxs-lookup"><span data-stu-id="af300-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="af300-207">Um encaminhador condicional só encaminha solicitações para um sufixo DNS específico.</span><span class="sxs-lookup"><span data-stu-id="af300-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="af300-208">Nesse caso, você deve configurar um encaminhador para o sufixo DNS da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="af300-209">Solicitações para esse sufixo devem ser encaminhadas para o endereço IP do servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="af300-210">O texto a seguir é um exemplo de uma configuração de encaminhador condicional para o software DNS do **Bind**:</span><span class="sxs-lookup"><span data-stu-id="af300-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="af300-211">Para obter informações sobre como usar o DNS no **Windows Server 2016**, consulte a documentação [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone)...</span><span class="sxs-lookup"><span data-stu-id="af300-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="af300-212">Depois de configurar o servidor DNS local, você pode usar `nslookup` da rede local para verificar se você pode resolver nomes na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="af300-213">O exemplo a seguir</span><span class="sxs-lookup"><span data-stu-id="af300-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="af300-214">Este exemplo usa o servidor DNS local em 196.168.0.4 para resolver o nome do servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="af300-215">Substitua o endereço IP por aquele para o servidor DNS local.</span><span class="sxs-lookup"><span data-stu-id="af300-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="af300-216">Substitua o endereço `dnsproxy` pelo nome de domínio totalmente qualificado do servidor DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="af300-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="af300-217">Opcional: controlar o tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="af300-217">Optional: Control network traffic</span></span>

<span data-ttu-id="af300-218">Você pode usar NSGs (grupos de segurança de rede) ou UDRs (rotas definidas pelo usuário) para controlar o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="af300-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="af300-219">As NSGs permitem filtrar o tráfego de entrada e de saída e permitem ou negam o tráfego.</span><span class="sxs-lookup"><span data-stu-id="af300-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="af300-220">As UDRs permitem que você controle como o tráfego flui entre os recursos da rede virtual, a Internet e a rede local.</span><span class="sxs-lookup"><span data-stu-id="af300-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="af300-221">O HDInsight requer acesso de entrada de endereços IP específicos na nuvem do Azure e acesso irrestrito de saída.</span><span class="sxs-lookup"><span data-stu-id="af300-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="af300-222">Ao usar as NSGs ou UDRs para controlar o tráfego, você deve executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="af300-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="af300-223">Localize os endereços IP para a localização que contém sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="af300-224">Para obter uma lista de IPs necessários por localização, consulte [Endereços IP necessários](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="af300-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="af300-225">Permitir tráfego de entrada de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="af300-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="af300-226">__NSG__: permitir tráfego de __entrada__ na porta __443__ proveniente da __Internet__.</span><span class="sxs-lookup"><span data-stu-id="af300-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="af300-227">__UDR__: definir o tipo do __Próximo Salto__ da rota para a __Internet__.</span><span class="sxs-lookup"><span data-stu-id="af300-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="af300-228">Para obter um exemplo de como usar o Azure PowerShell ou a CLI do Azure para criar as NSGs, consulte o documento [Estender o HDInsight com Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg).</span><span class="sxs-lookup"><span data-stu-id="af300-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="af300-229">Criar o cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="af300-230">Você deve criar e configurar o servidor DNS personalizado antes de instalar o HDInsight na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="af300-231">Use as etapas no documento [Criar um cluster HDInsight usando o portal do Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) para criar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af300-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="af300-232">Durante a criação do cluster, você deve escolher a localização que contém sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="af300-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="af300-233">Na parte __Configurações avançadas__ da configuração, você deve selecionar a rede virtual e a sub-rede que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="af300-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="af300-234">Conectando-se ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="af300-234">Connecting to HDInsight</span></span>

<span data-ttu-id="af300-235">A maior parte da documentação no HDInsight supõe que você tenha acesso ao cluster via Internet.</span><span class="sxs-lookup"><span data-stu-id="af300-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="af300-236">Por exemplo, você pode se conectar ao cluster em https://NOMEDOCLUSTER.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="af300-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="af300-237">Esse endereço usa o gateway público, que não estará disponível se você tiver usado NSGs ou UDRs para restringir o acesso da Internet.</span><span class="sxs-lookup"><span data-stu-id="af300-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="af300-238">Para conectar-se diretamente ao HDInsight por meio da rede virtual, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="af300-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="af300-239">Para descobrir os nomes de domínio totalmente qualificado internos dos nós do cluster HDInsight, use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="af300-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

2. <span data-ttu-id="af300-240">Para determinar a porta na qual um serviço está disponível, consulte o documento [Portas usadas por serviços do Hadoop no HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="af300-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="af300-241">Alguns serviços hospedados em nós de cabeçalho ficam ativos apenas em um nó por vez.</span><span class="sxs-lookup"><span data-stu-id="af300-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="af300-242">Se você tentar acessar um serviço em um nó de cabeçalho e ele falhar, mude para o outro nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="af300-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="af300-243">Por exemplo, o Ambari só está ativo em um nó de cabeçalho por vez.</span><span class="sxs-lookup"><span data-stu-id="af300-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="af300-244">Se você tentar acessar o Ambari em um nó de cabeçalho e ele retornar um erro 404, então ele estará em execução no outro nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="af300-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af300-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af300-245">Next steps</span></span>

* <span data-ttu-id="af300-246">Para obter mais informações sobre como usar o HDInsight em uma rede virtual, confira [Estender o HDInsight usando Redes Virtuais do Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="af300-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="af300-247">Para obter mais informações sobre redes virtuais do Azure, consulte a [Visão geral da Rede Virtual do Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af300-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="af300-248">Para obter mais informações sobre os Grupos de Segurança de Rede, veja [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="af300-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="af300-249">Para saber mais sobre rotas definidas pelo usuário, confira [Rotas definidas pelo usuário e encaminhamento IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af300-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
