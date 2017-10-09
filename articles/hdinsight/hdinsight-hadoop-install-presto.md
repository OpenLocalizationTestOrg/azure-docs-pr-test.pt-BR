---
title: clusters de pronto no Azure HDInsight Linux aaaInstall | Microsoft Docs
description: "Saiba como tooinstall pronto e Airpal no Hadoop de HDInsight baseados em Linux clusters usando ações de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="5002e-103">Instalar e usar Presto em clusters Hadoop do HDInsight</span><span class="sxs-lookup"><span data-stu-id="5002e-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="5002e-104">Neste tópico, você aprenderá como tooinstall pronto no Hadoop de HDInsight clusters usando a ação de Script.</span><span class="sxs-lookup"><span data-stu-id="5002e-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="5002e-105">Você também aprenderá como tooinstall Airpal em um cluster HDInsight Presto existente.</span><span class="sxs-lookup"><span data-stu-id="5002e-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5002e-106">Olá etapas neste documento exigem um **cluster HDInsight Hadoop de 3.5** que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="5002e-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="5002e-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5002e-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5002e-108">Para obter mais informações, consulte [Versões do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="5002e-109">O que é o Presto?</span><span class="sxs-lookup"><span data-stu-id="5002e-109">What is Presto?</span></span>
<span data-ttu-id="5002e-110">[Presto](https://prestodb.io/overview.html) é um mecanismo de consulta SQL distribuído rápido para big data.</span><span class="sxs-lookup"><span data-stu-id="5002e-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="5002e-111">O Presto é ideal para consultas interativas de petabytes de dados.</span><span class="sxs-lookup"><span data-stu-id="5002e-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="5002e-112">Para obter mais informações sobre componentes de saudação pronto e como eles funcionam juntos, consulte [conceitos Presto](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="5002e-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="5002e-113">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="5002e-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="5002e-114">Componentes personalizados, como pronto, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5002e-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5002e-115">Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado.</span><span class="sxs-lookup"><span data-stu-id="5002e-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="5002e-116">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5002e-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="5002e-117">Instalar o Presto usando a ação de script</span><span class="sxs-lookup"><span data-stu-id="5002e-117">Install Presto using script action</span></span>

<span data-ttu-id="5002e-118">Esta seção fornece instruções sobre como o script de exemplo de hello toouse ao criar um novo cluster usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5002e-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="5002e-119">Iniciar o provisionamento de um cluster usando as etapas de saudação em [clusters HDInsight baseados em Linux provisionar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="5002e-120">Certifique-se de criar cluster hello usando Olá **personalizado** fluxo de criação de cluster.</span><span class="sxs-lookup"><span data-stu-id="5002e-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="5002e-121">Certifique-se de cluster Olá que criar atende Olá requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5002e-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="5002e-122">a.</span><span class="sxs-lookup"><span data-stu-id="5002e-122">a.</span></span> <span data-ttu-id="5002e-123">Ele deve ser um cluster Hadoop com o HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="5002e-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="5002e-124">b.</span><span class="sxs-lookup"><span data-stu-id="5002e-124">b.</span></span> <span data-ttu-id="5002e-125">Ele deve usar o armazenamento do Azure como armazenamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5002e-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="5002e-126">Usando Presto em um cluster que usa o repositório Azure Data Lake como opção de armazenamento Olá ainda não é suportado.</span><span class="sxs-lookup"><span data-stu-id="5002e-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Criação do cluster HDInsight usando opções personalizadas](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="5002e-128">Em Olá **configurações avançadas** folha, selecione **ações de Script**e forneça as informações de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="5002e-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="5002e-129">**NOME**: insira um nome amigável para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="5002e-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="5002e-130">**URI do script Bash**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="5002e-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="5002e-131">**CABEÇALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="5002e-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="5002e-132">**TRABALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="5002e-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="5002e-133">**ZOOKEEPER**: desmarque essa caixa de seleção</span><span class="sxs-lookup"><span data-stu-id="5002e-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="5002e-134">**PARÂMETROS**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="5002e-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="5002e-135">Na parte inferior de saudação do hello **ações de Script** folha, clique em Olá **selecione** configuração de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="5002e-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="5002e-136">Por fim, clique em hello **selecione** botão na parte inferior de saudação do hello **configurações avançadas** informações de configuração de saudação de toosave de folha.</span><span class="sxs-lookup"><span data-stu-id="5002e-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="5002e-137">Continuar o provisionamento de cluster Olá conforme descrito em [clusters HDInsight baseados em Linux provisionar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5002e-138">PowerShell do Azure, Olá CLI do Azure, Olá HDInsight .NET SDK ou modelos do Azure Resource Manager também podem ser usado tooapply ações de script.</span><span class="sxs-lookup"><span data-stu-id="5002e-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="5002e-139">Você também pode aplicar o script ações tooalready clusters em execução.</span><span class="sxs-lookup"><span data-stu-id="5002e-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="5002e-140">Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="5002e-141">Usar o Presto com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="5002e-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="5002e-142">Execute Olá etapas toouse pronto em um cluster do HDInsight a seguir depois que ele foi instalado usando Olá etapas descritas acima.</span><span class="sxs-lookup"><span data-stu-id="5002e-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="5002e-143">Conecte o cluster do HDInsight toohello usando SSH:</span><span class="sxs-lookup"><span data-stu-id="5002e-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5002e-144">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="5002e-145">Inicie o shell Presto hello, usando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="5002e-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="5002e-146">Execute uma consulta em uma tabela de exemplo, **hivesampletable**, que está disponível em todos os clusters do HDInsight por padrão.</span><span class="sxs-lookup"><span data-stu-id="5002e-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="5002e-147">Por padrão, os conectores [Hive](https://prestodb.io/docs/current/connector/hive.html) e [TPCH](https://prestodb.io/docs/current/connector/tpch.html) já vêm configurados.</span><span class="sxs-lookup"><span data-stu-id="5002e-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="5002e-148">Conector de hive é configurado toouse saudação padrão instalado Hive instalação, para que todas as tabelas de saudação do Hive serão automaticamente visíveis no pronto.</span><span class="sxs-lookup"><span data-stu-id="5002e-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="5002e-149">Para obter uma descrição detalhada de como você pode usar o Presto, confira a [documentação do Presto](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="5002e-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="5002e-150">Usar o Airpal com o Presto</span><span class="sxs-lookup"><span data-stu-id="5002e-150">Use Airpal with Presto</span></span>

<span data-ttu-id="5002e-151">O [Airpal](https://github.com/airbnb/airpal#airpal) é uma interface de consulta baseada na Web de código-fonte aberto para o Presto.</span><span class="sxs-lookup"><span data-stu-id="5002e-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="5002e-152">Para saber mais sobre o Airpal, confira a [documentação do Airpal](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="5002e-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="5002e-153">Nesta seção, vamos examinar etapas Olá muito**instalar Airpal em Olá edgenode** de um cluster HDInsight Hadoop, que já tem pronto instalado.</span><span class="sxs-lookup"><span data-stu-id="5002e-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="5002e-154">Isso garante que essa interface de consulta Olá Airpal web está disponível por Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="5002e-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="5002e-155">Usando SSH, conecte-se toohello um nó principal do cluster HDInsight Olá Presto instalados:</span><span class="sxs-lookup"><span data-stu-id="5002e-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5002e-156">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5002e-157">Quando você estiver conectado, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5002e-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="5002e-158">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5002e-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="5002e-159">Da saída de hello, observe o valor de saudação para Olá **valor** propriedade.</span><span class="sxs-lookup"><span data-stu-id="5002e-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="5002e-160">Você precisará dela durante a instalação Airpal no hello edgenode de cluster.</span><span class="sxs-lookup"><span data-stu-id="5002e-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="5002e-161">Da saída de hello acima, o valor de saudação que você precisará **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="5002e-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="5002e-162">Usar o modelo de saudação  **[aqui](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate um HDInsight edgenode do cluster e forneça valores hello, conforme mostrado na Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="5002e-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![Instalação do Airpal no cluster Presto pelo HDInsight](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="5002e-164">Clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="5002e-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="5002e-165">Assim que as alterações de saudação forem aplicadas toohello configuração de cluster, você pode acessar a interface Olá Airpal da web usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="5002e-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="5002e-166">a.</span><span class="sxs-lookup"><span data-stu-id="5002e-166">a.</span></span> <span data-ttu-id="5002e-167">Na folha de cluster hello, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5002e-167">From hello cluster blade, click **Applications**.</span></span>

    ![O HDInsight inicia o Airpal no cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="5002e-169">b.</span><span class="sxs-lookup"><span data-stu-id="5002e-169">b.</span></span> <span data-ttu-id="5002e-170">De saudação **aplicativos instalados** folha, clique em **Portal** contra airpal.</span><span class="sxs-lookup"><span data-stu-id="5002e-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![O HDInsight inicia o Airpal no cluster Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="5002e-172">c.</span><span class="sxs-lookup"><span data-stu-id="5002e-172">c.</span></span> <span data-ttu-id="5002e-173">Quando solicitado, insira as credenciais de administrador de saudação que você especificou ao criar o cluster HDInsight Hadoop de saudação.</span><span class="sxs-lookup"><span data-stu-id="5002e-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="5002e-174">Personalizar uma instalação do Presto no cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="5002e-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="5002e-175">Depois que você instalou uma pronto em um cluster HDInsight Hadoop, você pode personalizar toomake alterações na instalação da saudação como atualizar as configurações de memória, alterar conectores, etc. Execute Olá toodo as etapas a seguir assim.</span><span class="sxs-lookup"><span data-stu-id="5002e-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="5002e-176">Usando SSH, conecte-se toohello um nó principal do cluster HDInsight Olá Presto instalados:</span><span class="sxs-lookup"><span data-stu-id="5002e-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="5002e-177">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5002e-178">Faça as alterações de configuração no arquivo hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="5002e-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="5002e-179">Para saber mais sobre a configuração do Presto, confira [Configuração do Presto para clusters baseados em YARN](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="5002e-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="5002e-180">Parar e interrompa a instância de execução atual de saudação do pronto.</span><span class="sxs-lookup"><span data-stu-id="5002e-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="5002e-181">Inicie uma nova instância de pronto com a personalização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5002e-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="5002e-182">Aguarde Olá nova instância toobe pronto e observe o endereço do coordenador presto.</span><span class="sxs-lookup"><span data-stu-id="5002e-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="5002e-183">Gerar dados de avaliação de desempenho para clusters do HDInsight que executam o Presto</span><span class="sxs-lookup"><span data-stu-id="5002e-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="5002e-184">DS TPC é saudação padrão da indústria para medir o desempenho de saudação de muitos sistemas de suporte de decisão, incluindo sistemas grandes de dados.</span><span class="sxs-lookup"><span data-stu-id="5002e-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="5002e-185">Você pode usar Presto nos dados de toogenerate clusters HDInsight e avaliar como ele se compara com seus próprios dados de referência do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5002e-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="5002e-186">Para saber mais, clique [aqui](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="5002e-187">Consulte também</span><span class="sxs-lookup"><span data-stu-id="5002e-187">See also</span></span>
* <span data-ttu-id="5002e-188">[Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="5002e-189">O matiz é uma interface que torna mais fácil toocreate, executar da web e salvar os trabalhos de Pig e Hive, bem como procurar saudação padrão armazenamento para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5002e-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="5002e-190">[Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="5002e-191">Use cluster personalização tooinstall que giraph no Hadoop de HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5002e-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5002e-192">Giraph permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5002e-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="5002e-193">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5002e-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="5002e-194">Use cluster personalização tooinstall que solr no Hadoop de HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5002e-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5002e-195">Solr permite operações de pesquisa poderoso tooperform nos dados armazenados.</span><span class="sxs-lookup"><span data-stu-id="5002e-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
