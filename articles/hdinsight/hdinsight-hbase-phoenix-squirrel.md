---
title: aaaUse Phoenix Apache e esquilo com baseados no Windows Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Phoenix Apache no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="45ae8-103">Usar Apache Phoenix e SQuirreL com clusters do HBase baseados em Windows no HDInsight</span><span class="sxs-lookup"><span data-stu-id="45ae8-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="45ae8-104">Saiba como toouse [Apache Phoenix](http://phoenix.apache.org/) no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45ae8-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="45ae8-105">Para obter mais informações sobre o Phoenix, consulte [Phoenix em 15 minutos ou menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="45ae8-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="45ae8-106">Para Olá gramática Phoenix, consulte [Phoenix gramática](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="45ae8-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="45ae8-107">Para Olá informações de versão de Phoenix no HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="45ae8-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="45ae8-108">Olá etapas para esse trabalho de documento somente para clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="45ae8-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="45ae8-109">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="45ae8-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="45ae8-110">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="45ae8-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="45ae8-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="45ae8-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="45ae8-112">Para obter informações sobre como usar o Phoenix no HDInsight baseado em Linux, consulte [Usar o Apache Phoenix com clusters HBase baseados em Linux no HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="45ae8-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="45ae8-113">Usar o SQLLine</span><span class="sxs-lookup"><span data-stu-id="45ae8-113">Use SQLLine</span></span>
<span data-ttu-id="45ae8-114">[SQLLine](http://sqlline.sourceforge.net/) é um utilitário de linha de comando tooexecute SQL.</span><span class="sxs-lookup"><span data-stu-id="45ae8-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="45ae8-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45ae8-115">Prerequisites</span></span>
<span data-ttu-id="45ae8-116">Antes de usar SQLLine, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="45ae8-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="45ae8-117">**Um cluster HBase no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="45ae8-118">Para obter informações sobre como provisionar o cluster HBase, consulte [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="45ae8-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="45ae8-119">**Conecte toohello HBase cluster por meio do protocolo de área de trabalho remota Olá**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="45ae8-120">Para obter instruções, consulte [Hadoop gerenciar clusters de HDInsight usando Olá Portal clássico do Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="45ae8-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="45ae8-121">**toofind nome de host Olá**</span><span class="sxs-lookup"><span data-stu-id="45ae8-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="45ae8-122">Abra **linha de comando do Hadoop** na área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="45ae8-123">Execute Olá sufixo DNS do comando tooget Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="45ae8-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="45ae8-124">Execute **Connection-specific DNS Suffix**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="45ae8-125">Por exemplo, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="45ae8-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="45ae8-126">Quando você conectar tooan HBase cluster, você precisará tooone tooconnect de Zookeepers hello usando o FQDN.</span><span class="sxs-lookup"><span data-stu-id="45ae8-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="45ae8-127">Cada cluster HDInsight possui 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="45ae8-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="45ae8-128">São eles: *zookeeper0*, *zookeeper1* e *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="45ae8-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="45ae8-129">Olá FQDN será algo como *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="45ae8-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="45ae8-130">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="45ae8-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="45ae8-131">Abra **linha de comando do Hadoop** na área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="45ae8-132">Execute Olá comandos tooopen SQLLine a seguir:</span><span class="sxs-lookup"><span data-stu-id="45ae8-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="45ae8-134">comandos de saudação usados no exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="45ae8-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="45ae8-135">Para obter mais informações, consulte o [Manual SQLLine](http://sqlline.sourceforge.net/#manual) e [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="45ae8-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="45ae8-136">Usar o SQuirreL</span><span class="sxs-lookup"><span data-stu-id="45ae8-136">Use SQuirreL</span></span>
<span data-ttu-id="45ae8-137">[Esquilo SQL Client](http://squirrel-sql.sourceforge.net/) é um programa Java gráfico que permitem que você tooview estrutura de saudação do banco de dados compatível com JDBC, procurar Olá dados nas tabelas, emitir comandos SQL etc. Ele pode ser usado tooconnect tooApache Phoenix no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45ae8-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="45ae8-138">Esta seção mostra como tooinstall e configurar esquilo em sua estação de trabalho tooconnect tooan cluster HBase em HDInsight por meio de VPN.</span><span class="sxs-lookup"><span data-stu-id="45ae8-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="45ae8-139">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45ae8-139">Prerequisites</span></span>
<span data-ttu-id="45ae8-140">Antes de seguir os procedimentos de hello, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="45ae8-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="45ae8-141">Um cluster HBase implantado tooan rede virtual do Azure com uma máquina virtual DNS.</span><span class="sxs-lookup"><span data-stu-id="45ae8-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="45ae8-142">Para obter instruções, consulte [Criar clusters HBase na Rede Virtual do Azure][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="45ae8-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="45ae8-143">Obtém o sufixo DNS específico da Conexão do hello HBase cluster cluster.</span><span class="sxs-lookup"><span data-stu-id="45ae8-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="45ae8-144">tooget-lo, RDP em cluster Olá, e, em seguida, executar esse comando.</span><span class="sxs-lookup"><span data-stu-id="45ae8-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="45ae8-145">sufixo DNS Olá é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="45ae8-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="45ae8-146">Baixe e instale o [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="45ae8-147">Você precisará makecert da saudação pacote toocreate seu certificado.</span><span class="sxs-lookup"><span data-stu-id="45ae8-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="45ae8-148">Baixe e instale o [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="45ae8-149">O SQuirreL SQL client versão 3.0 e superior requer JRE versão 1.6 ou superior.</span><span class="sxs-lookup"><span data-stu-id="45ae8-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="45ae8-150">Configurar uma conexão de VPN ponto a Site toohello rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="45ae8-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="45ae8-151">Há três etapas envolvidas na configuração de uma conexão VPN ponto a site:</span><span class="sxs-lookup"><span data-stu-id="45ae8-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="45ae8-152">Configurar uma rede virtual e um gateway de roteamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="45ae8-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="45ae8-153">Criar seus certificados</span><span class="sxs-lookup"><span data-stu-id="45ae8-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="45ae8-154">Configurar o seu cliente VPN</span><span class="sxs-lookup"><span data-stu-id="45ae8-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="45ae8-155">Consulte [configurar uma conexão de VPN ponto a Site tooan rede Virtual do Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="45ae8-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="45ae8-156">Configurar uma rede virtual e um gateway de roteamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="45ae8-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="45ae8-157">Garantir que você possua um cluster HBase em uma rede virtual do Azure (consulte Olá pré-requisitos para essa seção).</span><span class="sxs-lookup"><span data-stu-id="45ae8-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="45ae8-158">Olá próxima etapa é tooconfigure uma conexão ponto a site.</span><span class="sxs-lookup"><span data-stu-id="45ae8-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="45ae8-159">**conectividade de ponto para site Olá tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="45ae8-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="45ae8-160">Entrar toohello [Portal clássico do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="45ae8-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="45ae8-161">Olá esquerda, clique em **redes**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="45ae8-162">Clique em criar a rede virtual Olá (consulte [HBase provisionar clusters na rede Virtual do Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="45ae8-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="45ae8-163">Clique em **configurar** da parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="45ae8-164">Em Olá **conectividade ponto a site** seção, selecione **configurar conectividade ponto a site**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="45ae8-165">Configurar **IP inicial** e **CIDR** endereço de intervalo de endereços toospecify Olá IP do qual os clientes VPN receberão um IP quando conectados.</span><span class="sxs-lookup"><span data-stu-id="45ae8-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="45ae8-166">intervalo de saudação não pode sobrepor qualquer Olá intervalos localizados em seus locais de rede e Olá rede virtual do Azure, que você irá se conectar.</span><span class="sxs-lookup"><span data-stu-id="45ae8-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="45ae8-167">Por exemplo.</span><span class="sxs-lookup"><span data-stu-id="45ae8-167">For example.</span></span> <span data-ttu-id="45ae8-168">Se você selecionou 10.0.0.0/20 para rede virtual hello, você pode selecionar 10.1.0.0/24 para o espaço de endereço de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="45ae8-169">Consulte Olá [conectividadepontoaSite] [ vnet-point-to-site-connectivity] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="45ae8-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="45ae8-170">Na seção de espaços de endereço de rede virtual hello, clique em **Adicionar sub-rede de gateway**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="45ae8-171">Clique em **salvar** na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="45ae8-172">Clique em **Sim** tooconfirm alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="45ae8-173">Aguarde até que o sistema de saudação terminou tornando Olá alterar antes de prosseguir toohello próximo procedimento.</span><span class="sxs-lookup"><span data-stu-id="45ae8-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="45ae8-174">**toocreate um gateway de roteamento dinâmico**</span><span class="sxs-lookup"><span data-stu-id="45ae8-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="45ae8-175">De Olá Portal clássico do Azure, clique em **painel** da parte superior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="45ae8-176">Clique em **criar GATEWAY** Olá página de baixo hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="45ae8-177">Clique em **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="45ae8-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="45ae8-178">Aguarde até que o gateway de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="45ae8-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="45ae8-179">Clique em **painel** da parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="45ae8-180">Você verá um diagrama visual de rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="45ae8-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Diagrama virtual de ponto para site de rede virtual do Azure][img-vnet-diagram]

    <span data-ttu-id="45ae8-182">diagrama de saudação mostra 0 conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="45ae8-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="45ae8-183">Depois de fazer uma rede virtual de toohello de conexão, o número de saudação será atualizado tooone.</span><span class="sxs-lookup"><span data-stu-id="45ae8-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="45ae8-184">Criar seus certificados</span><span class="sxs-lookup"><span data-stu-id="45ae8-184">Create your certificates</span></span>
<span data-ttu-id="45ae8-185">Toocreate unidirecional é um certificado x. 509 usando Olá ferramenta de criação de certificado (makecert.exe) que vem com [Microsoft Visual Studio Express para Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="45ae8-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="45ae8-186">**toocreate um certificado raiz autoassinado**</span><span class="sxs-lookup"><span data-stu-id="45ae8-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="45ae8-187">Na estação de trabalho, abra uma janela de prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="45ae8-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="45ae8-188">Navegue toohello pasta de ferramentas do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45ae8-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="45ae8-189">Olá comando no exemplo hello abaixo a seguir criar e instalar um certificado raiz no repositório de certificados pessoal Olá na estação de trabalho e também criar um arquivo. cer correspondente que você posteriormente carregará toohello Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="45ae8-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="45ae8-190">Altere o diretório de toohello que você deseja Olá toobe do arquivo. cer localizado, onde o HBaseVnetVPNRootCertificate é o nome de saudação que você deseja toouse certificado hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="45ae8-191">Não feche o prompt de comando hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="45ae8-192">Você precisará no procedimento a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="45ae8-193">Porque você criou um certificado raiz do qual os certificados de cliente serão gerados, você pode desejar tooexport esse certificado junto com sua chave privada e salvá-lo tooa local seguro onde possa ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="45ae8-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="45ae8-194">**toocreate um certificado de cliente**</span><span class="sxs-lookup"><span data-stu-id="45ae8-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="45ae8-195">De saudação mesmo prompt de comando (tem toobe em Olá mesmo computador em que você criou o certificado de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="45ae8-196">certificado de cliente Olá deve ser gerado do certificado de raiz de saudação), execução hello seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="45ae8-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="45ae8-197">HBaseVnetVPNRootCertificate é o nome do certificado raiz hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="45ae8-198">Ele tem o nome do certificado de raiz toomatch hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="45ae8-199">Certificado de raiz hello e certificado de saudação do cliente são armazenadas no repositório de certificados pessoais no computador.</span><span class="sxs-lookup"><span data-stu-id="45ae8-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="45ae8-200">Use certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="45ae8-200">Use certmgr.msc tooverify.</span></span>

    ![Certificado VPN de ponto para site de rede virtual do Azure][img-certificate]

    <span data-ttu-id="45ae8-202">Um certificado de cliente deve ser instalado em cada computador que deseja que a rede virtual do tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="45ae8-203">É recomendável que você crie cliente exclusivo certificados para cada computador que deseja que a rede virtual do tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="45ae8-204">certificados de cliente de saudação tooexport, use certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="45ae8-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="45ae8-205">**toohello do certificado raiz do tooupload Olá Portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="45ae8-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="45ae8-206">De Olá Portal clássico do Azure, clique em **rede** Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="45ae8-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="45ae8-207">Clique em rede virtual hello, onde o cluster HBase é implantado.</span><span class="sxs-lookup"><span data-stu-id="45ae8-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="45ae8-208">Clique em **certificados** da parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="45ae8-209">Clique em **carregar** de saudação baixo e especifique o arquivo do certificado raiz Olá você criou no procedimento Olá antes da última.</span><span class="sxs-lookup"><span data-stu-id="45ae8-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="45ae8-210">Aguarde até que o certificado de saudação foi importado.</span><span class="sxs-lookup"><span data-stu-id="45ae8-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="45ae8-211">Clique em **painel** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="45ae8-212">diagrama de virtual Olá mostra o status de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="45ae8-213">Configurar o seu cliente VPN</span><span class="sxs-lookup"><span data-stu-id="45ae8-213">Configure your VPN client</span></span>
<span data-ttu-id="45ae8-214">**toodownload e instale o pacote VPN de cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="45ae8-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="45ae8-215">Na página de painel Olá da rede virtual hello, na seção de visão rápida hello, clique em **Download Olá pacote de VPN de cliente de 64 bits** ou **Download Olá pacote de VPN de cliente de 32 bits** com base em seu versão do sistema operacional da estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="45ae8-216">Clique em **executar** tooinstall pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="45ae8-217">No prompt de segurança hello, clique em **obter mais informações**e, em seguida, clique em **executar assim mesmo**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="45ae8-218">Clique em **Sim** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="45ae8-218">Click **Yes** twice.</span></span>

<span data-ttu-id="45ae8-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="45ae8-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="45ae8-220">Na área de trabalho de saudação de sua estação de trabalho, clique o ícone de redes de saudação na barra de tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="45ae8-221">Você deverá ver uma conexão VPN com o seu nome de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="45ae8-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="45ae8-222">Clique no nome de conexão de VPN hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="45ae8-223">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-223">Click **Connect**.</span></span>

<span data-ttu-id="45ae8-224">**Olá tootest resolução de nome de domínio e a conexão VPN**</span><span class="sxs-lookup"><span data-stu-id="45ae8-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="45ae8-225">Na estação de trabalho Olá, abra um prompt de comando e ping de saudação nomes de sufixo DNS do cluster do HBase Olá a seguir é myhbase.b7.internal.cloudapp.net:</span><span class="sxs-lookup"><span data-stu-id="45ae8-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="45ae8-226">Instalar e configurar o SQuirreL em sua estação de trabalho</span><span class="sxs-lookup"><span data-stu-id="45ae8-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="45ae8-227">**tooinstall esquilo**</span><span class="sxs-lookup"><span data-stu-id="45ae8-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="45ae8-228">Baixar arquivo do hello esquilo SQL client jar do [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="45ae8-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="45ae8-229">Arquivo jar Olá Abrir/executar.</span><span class="sxs-lookup"><span data-stu-id="45ae8-229">Open/run hello jar file.</span></span> <span data-ttu-id="45ae8-230">Ele requer Olá [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="45ae8-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="45ae8-231">Clique em **Avançar** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="45ae8-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="45ae8-232">Especifique um caminho onde Olá você tem permissão de gravação e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="45ae8-233">pasta de instalação padrão Hello está na pasta de C:\Program Files\squirrel sql 3.6 de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="45ae8-234">No caminho de toothis de toowrite de ordem, instalador Olá deve ter o privilégio de administrador hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="45ae8-235">Você pode abrir um prompt de comando como administrador, navegue pasta bin do tooJava e, em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="45ae8-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="45ae8-236">Java.exe-jar [caminho de saudação do arquivo jar do hello esquilo]</span><span class="sxs-lookup"><span data-stu-id="45ae8-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="45ae8-237">Clique em **Okey** tooconfirm criando Olá diretório de destino.</span><span class="sxs-lookup"><span data-stu-id="45ae8-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="45ae8-238">configuração padrão de saudação é tooinstall Olá Base e pacotes padrão.</span><span class="sxs-lookup"><span data-stu-id="45ae8-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="45ae8-239">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-239">Click **Next**.</span></span>
7. <span data-ttu-id="45ae8-240">Clique em **Próximo** duas vezes e, em seguida, clique em **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="45ae8-241">**driver de Phoenix Olá tooinstall**</span><span class="sxs-lookup"><span data-stu-id="45ae8-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="45ae8-242">arquivo jar do Hello phoenix driver está localizado em um cluster HBase de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="45ae8-243">caminho de saudação é semelhante seguinte toohello baseados em versões de saudação:</span><span class="sxs-lookup"><span data-stu-id="45ae8-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="45ae8-244">Você precisa toocopy-tooyour estação de trabalho em Olá [pasta de instalação esquilo] /lib caminho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="45ae8-245">Olá, a maneira mais fácil é tooRDP cluster hello e, em seguida, use arquivo copiar/colar (CTRL + C e CTRL + V) toocopy-tooyour estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="45ae8-246">**tooadd um tooSQuirreL de driver Phoenix**</span><span class="sxs-lookup"><span data-stu-id="45ae8-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="45ae8-247">Abra o SQuirreL SQL Client em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="45ae8-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="45ae8-248">Clique em Olá **Driver** guia Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="45ae8-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="45ae8-249">De saudação **Drivers** menu, clique em **novo Driver**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="45ae8-250">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="45ae8-250">Enter hello following information:</span></span>

   * <span data-ttu-id="45ae8-251">**Nome**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="45ae8-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="45ae8-252">**URL de exemplo**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="45ae8-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="45ae8-253">**Nome da classe**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="45ae8-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="45ae8-254">Usuário todas as letras minúsculas Olá exemplo de URL.</span><span class="sxs-lookup"><span data-stu-id="45ae8-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="45ae8-255">Você pode usar o quorum zookeeper completo no caso de um deles estar inativo.</span><span class="sxs-lookup"><span data-stu-id="45ae8-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="45ae8-256">saudação de nomes de host são zookeeper0, zookeeper1 e zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="45ae8-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-driver]
5. <span data-ttu-id="45ae8-258">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-258">Click **OK**.</span></span>

<span data-ttu-id="45ae8-259">**toocreate um cluster do alias toohello HBase**</span><span class="sxs-lookup"><span data-stu-id="45ae8-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="45ae8-260">De esquilo, clique em Olá **Aliases** guia Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="45ae8-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="45ae8-261">De saudação **Aliases** menu, clique em **novo Alias**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="45ae8-262">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="45ae8-262">Enter hello following information:</span></span>

   * <span data-ttu-id="45ae8-263">**Nome**: nome de saudação do cluster HBase de saudação ou qualquer nome que você preferir.</span><span class="sxs-lookup"><span data-stu-id="45ae8-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="45ae8-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="45ae8-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="45ae8-265">Isso deve corresponder a nome do driver Olá criada no procedimento última hello.</span><span class="sxs-lookup"><span data-stu-id="45ae8-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="45ae8-266">**URL**: Olá URL é copiada da configuração do driver.</span><span class="sxs-lookup"><span data-stu-id="45ae8-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="45ae8-267">Verifique se toouser todas as letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="45ae8-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="45ae8-268">**Nome de usuário**: pode ser qualquer texto.</span><span class="sxs-lookup"><span data-stu-id="45ae8-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="45ae8-269">Como você usar a conectividade VPN aqui, o nome de usuário de saudação não é usado em todos os.</span><span class="sxs-lookup"><span data-stu-id="45ae8-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="45ae8-270">**Senha**: pode ser qualquer texto.</span><span class="sxs-lookup"><span data-stu-id="45ae8-270">**Password**: It can be any text.</span></span>

     ![HDInsight HBase Phoenix SQuirreL driver][img-squirrel-alias]
4. <span data-ttu-id="45ae8-272">Clique em **Testar**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-272">Click **Test**.</span></span>
5. <span data-ttu-id="45ae8-273">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-273">Click **Connect**.</span></span> <span data-ttu-id="45ae8-274">Quando faz conexão hello, esquilo é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="45ae8-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="45ae8-276">**toorun um teste**</span><span class="sxs-lookup"><span data-stu-id="45ae8-276">**toorun a test**</span></span>

1. <span data-ttu-id="45ae8-277">Clique em Olá **SQL** guia direito próximo toohello **objetos** guia.</span><span class="sxs-lookup"><span data-stu-id="45ae8-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="45ae8-278">Copie e cole a saudação de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="45ae8-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="45ae8-279">Clique o botão de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="45ae8-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="45ae8-281">Alternar back toohello **objetos** guia.</span><span class="sxs-lookup"><span data-stu-id="45ae8-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="45ae8-282">Expanda o nome do alias hello e, em seguida, expanda **tabela**.</span><span class="sxs-lookup"><span data-stu-id="45ae8-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="45ae8-283">Você deverá ver a nova tabela de hello listada em.</span><span class="sxs-lookup"><span data-stu-id="45ae8-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45ae8-284">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45ae8-284">Next steps</span></span>
<span data-ttu-id="45ae8-285">Neste artigo, você aprendeu como toouse Phoenix Apache no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45ae8-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="45ae8-286">toolearn mais, consulte</span><span class="sxs-lookup"><span data-stu-id="45ae8-286">toolearn more, see</span></span>

* <span data-ttu-id="45ae8-287">[Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.</span><span class="sxs-lookup"><span data-stu-id="45ae8-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="45ae8-288">[Provisionar clusters HBase na rede Virtual do Azure][hdinsight-hbase-provision-vnet]: com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que os aplicativos podem se comunicar com o HBase diretamente.</span><span class="sxs-lookup"><span data-stu-id="45ae8-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="45ae8-289">[Configurar a replicação do HBase em HDInsight](hdinsight-hbase-replication.md): Saiba como tooconfigure HBase replicação entre dois datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="45ae8-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="45ae8-290">[Analisar o sentimento do Twitter com HBase em HDInsight][hbase-twitter-sentiment]: Saiba como toodo em tempo real [análise de sentimento](http://en.wikipedia.org/wiki/Sentiment_analysis) de big data usando HBase em um cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45ae8-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
