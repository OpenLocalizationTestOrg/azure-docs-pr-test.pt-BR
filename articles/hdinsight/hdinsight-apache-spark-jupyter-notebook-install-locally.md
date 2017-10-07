---
title: aaaInstall Jupyter localmente & conectar-se o cluster do Spark no HDInsight tooan | Microsoft Docs
description: "Saiba como anotações do Jupyter tooinstall localmente no seu computador e conecte-o cluster do tooan Apache Spark no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a><span data-ttu-id="daa53-103">Instalar o bloco de anotações do Jupyter em seu computador e conecte-se tooApache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-103">Install Jupyter notebook on your computer and connect tooApache Spark on HDInsight</span></span>

<span data-ttu-id="daa53-104">Neste artigo, você aprenderá como anotações do Jupyter tooinstall, com hello PySpark personalizado (para Python) e kernels Spark (para Scala) com despertar magic e conecte-se o cluster do HDInsight Olá notebook tooan.</span><span class="sxs-lookup"><span data-stu-id="daa53-104">In this article you learn how tooinstall Jupyter notebook, with hello custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect hello notebook tooan HDInsight cluster.</span></span> <span data-ttu-id="daa53-105">Pode haver um número de motivos tooinstall Jupyter no computador local, e pode haver alguns desafios também.</span><span class="sxs-lookup"><span data-stu-id="daa53-105">There can be a number of reasons tooinstall Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="daa53-106">Para obter mais informações sobre isso, consulte a seção de saudação [por que devo instalar Jupyter no meu computador](#why-should-i-install-jupyter-on-my-computer) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="daa53-106">For more on this, see hello section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at hello end of this article.</span></span>

<span data-ttu-id="daa53-107">Há três etapas principais envolvidas na instalação Jupyter e hello magic Spark no seu computador.</span><span class="sxs-lookup"><span data-stu-id="daa53-107">There are three key steps involved in installing Jupyter and hello Spark magic on your computer.</span></span>

* <span data-ttu-id="daa53-108">Instalar bloco de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="daa53-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="daa53-109">Instalar hello PySpark e kernels Spark com hello magic Spark</span><span class="sxs-lookup"><span data-stu-id="daa53-109">Install hello PySpark and Spark kernels with hello Spark magic</span></span>
* <span data-ttu-id="daa53-110">Configurar Spark magic tooaccess cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-110">Configure Spark magic tooaccess Spark cluster on HDInsight</span></span>

<span data-ttu-id="daa53-111">Para obter mais informações sobre kernels personalizado hello e mágico de Spark Olá disponível para blocos de anotações do Jupyter com o cluster HDInsight, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="daa53-111">For more information about hello custom kernels and hello Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daa53-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="daa53-112">Prerequisites</span></span>
<span data-ttu-id="daa53-113">pré-requisitos de saudação listados aqui não são para a instalação do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="daa53-113">hello prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="daa53-114">Esses são para cluster de HDInsight do conexão Olá Jupyter notebook tooan quando notebook hello está instalado.</span><span class="sxs-lookup"><span data-stu-id="daa53-114">These are for connecting hello Jupyter notebook tooan HDInsight cluster once hello notebook is installed.</span></span>

* <span data-ttu-id="daa53-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="daa53-115">An Azure subscription.</span></span> <span data-ttu-id="daa53-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="daa53-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="daa53-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="daa53-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="daa53-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="daa53-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="daa53-119">Instalar bloco de notas Jupyter em seu computador</span><span class="sxs-lookup"><span data-stu-id="daa53-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="daa53-120">Você deve instalar o Python antes de instalar notebooks do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="daa53-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="daa53-121">Python e Jupyter estão disponíveis como parte da saudação [distribuição Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="daa53-121">Both Python and Jupyter are available as part of hello [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="daa53-122">Quando instala o Anaconda, você instala uma distribuição do Python.</span><span class="sxs-lookup"><span data-stu-id="daa53-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="daa53-123">Quando Anaconda estiver instalado, você adiciona instalação de Jupyter Olá executando comandos apropriados.</span><span class="sxs-lookup"><span data-stu-id="daa53-123">Once Anaconda is installed, you add hello Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="daa53-124">Baixar Olá [instalador Anaconda](https://www.continuum.io/downloads) para sua plataforma e a configuração de execução hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-124">Download hello [Anaconda installer](https://www.continuum.io/downloads) for your platform and run hello setup.</span></span> <span data-ttu-id="daa53-125">Ao Assistente de instalação de saudação em execução, verifique se que você selecionar a variável de caminho Olá opção tooadd Anaconda tooyour.</span><span class="sxs-lookup"><span data-stu-id="daa53-125">While running hello setup wizard, make sure you select hello option tooadd Anaconda tooyour PATH variable.</span></span>
2. <span data-ttu-id="daa53-126">Execute Olá comando tooinstall Jupyter a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-126">Run hello following command tooinstall Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="daa53-127">Para obter mais informações sobre a instalação do Jupyter, confira [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Instalando o Jupyter usando o Anaconda).</span><span class="sxs-lookup"><span data-stu-id="daa53-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-hello-kernels-and-spark-magic"></a><span data-ttu-id="daa53-128">Instalar kernels hello e magic Spark</span><span class="sxs-lookup"><span data-stu-id="daa53-128">Install hello kernels and Spark magic</span></span>

<span data-ttu-id="daa53-129">Para obter instruções sobre como mágica do tooinstall Olá Spark, Olá PySpark e kernels Spark, siga instruções de instalação de saudação em Olá [sparkmagic documentação](https://github.com/jupyter-incubator/sparkmagic#installation) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="daa53-129">For instructions on how tooinstall hello Spark magic, hello PySpark and Spark kernels, follow hello installation instructions in hello [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="daa53-130">Olá primeira etapa na documentação do hello Spark magic solicitará que você tooinstall mágico de Spark.</span><span class="sxs-lookup"><span data-stu-id="daa53-130">hello first step in hello Spark magic documentation asks you tooinstall Spark magic.</span></span> <span data-ttu-id="daa53-131">Substitua essa primeira etapa no link Olá Olá comandos, dependendo da versão de saudação do cluster do HDInsight Olá que você se conectará a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-131">Replace that first step in hello link with hello following commands, depending on hello version of hello HDInsight cluster you will connect to.</span></span> <span data-ttu-id="daa53-132">Depois disso, siga Olá restantes etapas descritas na documentação mágica do hello Spark.</span><span class="sxs-lookup"><span data-stu-id="daa53-132">After that, follow hello remaining steps in hello Spark magic documentation.</span></span> <span data-ttu-id="daa53-133">Se você quiser kernels diferentes do tooinstall Olá, você deve executar a etapa 3 no hello seção de instruções de instalação magic Spark.</span><span class="sxs-lookup"><span data-stu-id="daa53-133">If you want tooinstall hello different kernels, you must perform Step 3 in hello Spark magic installation instructions section.</span></span>

* <span data-ttu-id="daa53-134">Para clusters v3.4, instale sparkmagic 0.2.3 executando `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="daa53-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="daa53-135">Para clusters v3.5 e v3.6, instale sparkmagic 0.11.2 executando `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="daa53-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a><span data-ttu-id="daa53-136">Configurar o cluster do Spark tooconnect magic tooHDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="daa53-136">Configure Spark magic tooconnect tooHDInsight Spark cluster</span></span>

<span data-ttu-id="daa53-137">Nesta seção você configurar mágico do Spark Olá que você instalou o cluster do Apache Spark de tooan tooconnect anterior você já deve ter criado no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="daa53-137">In this section you configure hello Spark magic that you installed earlier tooconnect tooan Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="daa53-138">Olá Jupyter informações de configuração é normalmente armazenado no diretório base de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="daa53-138">hello Jupyter configuration information is typically stored in hello users home directory.</span></span> <span data-ttu-id="daa53-139">toolocate comandos de seu diretório base em qualquer plataforma de sistema operacional, Olá tipo a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-139">toolocate your home directory on any OS platform, type hello following commands.</span></span>

    <span data-ttu-id="daa53-140">Inicie o shell de Python hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-140">Start hello Python shell.</span></span> <span data-ttu-id="daa53-141">Em uma janela de comando, digite o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="daa53-141">On a command window, type hello following:</span></span>

        python

    <span data-ttu-id="daa53-142">Na Olá shell Python, digite Olá toofind comando diretório base Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-142">On hello Python shell, enter hello following command toofind out hello home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="daa53-143">Navegue diretório base toohello e crie uma pasta chamada **.sparkmagic** se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="daa53-143">Navigate toohello home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="daa53-144">Na pasta hello, crie um arquivo chamado **config. JSON** e adicione Olá seguindo o trecho JSON dentro dele.</span><span class="sxs-lookup"><span data-stu-id="daa53-144">Within hello folder, create a file called **config.json** and add hello following JSON snippet inside it.</span></span>

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. <span data-ttu-id="daa53-145">Substitua **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** pelos valores apropriados.</span><span class="sxs-lookup"><span data-stu-id="daa53-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="daa53-146">Você pode usar um número de utilitários em sua linguagem de programação favorita ou senha codificada em base64 de toogenerate online para sua senha real.</span><span class="sxs-lookup"><span data-stu-id="daa53-146">You can use a number of utilities in your favorite programming language or online toogenerate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="daa53-147">Definir configurações de pulsação direita Olá no `config.json`.</span><span class="sxs-lookup"><span data-stu-id="daa53-147">Configure hello right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="daa53-148">Você deve adicionar essas configurações em Olá mesmo nível como Olá `kernel_python_credentials` e `kernel_scala_credentials` trechos seu adicionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="daa53-148">You should add these settings at hello same level as hello `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="daa53-149">Para obter um exemplo sobre como e onde tooadd Olá configurações de pulsação, consulte [config. JSON de exemplo](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="daa53-149">For an example on how and where tooadd hello heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="daa53-150">Para `sparkmagic 0.2.3` (clusters v3.4), incluem:</span><span class="sxs-lookup"><span data-stu-id="daa53-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="daa53-151">Para `sparkmagic 0.11.2` (clusters v3.5 e v3.6), inclua:</span><span class="sxs-lookup"><span data-stu-id="daa53-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="daa53-152">As pulsações são enviadas tooensure que não vazam sessões.</span><span class="sxs-lookup"><span data-stu-id="daa53-152">Heartbeats are sent tooensure that sessions are not leaked.</span></span> <span data-ttu-id="daa53-153">Quando um computador fica toosleep ou está desligado, pulsação Olá não for enviada, resultando em Olá sessão sendo limpo.</span><span class="sxs-lookup"><span data-stu-id="daa53-153">When a computer goes toosleep or is shut down, hello heartbeat is not sent, resulting in hello session being cleaned up.</span></span> <span data-ttu-id="daa53-154">Para clusters v3.4, se desejar toodisable esse comportamento, você pode definir Olá Livy config `livy.server.interactive.heartbeat.timeout` muito`0` de saudação Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="daa53-154">For clusters v3.4, if you wish toodisable this behavior, you can set hello Livy config `livy.server.interactive.heartbeat.timeout` too`0` from hello Ambari UI.</span></span> <span data-ttu-id="daa53-155">Para v 3.5 de clusters, se você não definir a configuração de saudação 3.5 acima, sessão de saudação não será excluído.</span><span class="sxs-lookup"><span data-stu-id="daa53-155">For clusters v3.5, if you do not set hello 3.5 configuration above, hello session will not be deleted.</span></span>

6. <span data-ttu-id="daa53-156">Inicie o Jupyter.</span><span class="sxs-lookup"><span data-stu-id="daa53-156">Start Jupyter.</span></span> <span data-ttu-id="daa53-157">Use Olá comando a seguir no prompt de comando hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-157">Use hello following command from hello command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="daa53-158">Verifique se você pode se conectar a cluster toohello usando anotações do Jupyter hello e que você pode usar mágico de Spark Olá disponível com kernels hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-158">Verify that you can connect toohello cluster using hello Jupyter notebook and that you can use hello Spark magic available with hello kernels.</span></span> <span data-ttu-id="daa53-159">Execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-159">Perform hello following steps.</span></span>

    <span data-ttu-id="daa53-160">a.</span><span class="sxs-lookup"><span data-stu-id="daa53-160">a.</span></span> <span data-ttu-id="daa53-161">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="daa53-161">Create a new notebook.</span></span> <span data-ttu-id="daa53-162">No canto superior direito da saudação, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="daa53-162">From hello right-hand corner, click **New**.</span></span> <span data-ttu-id="daa53-163">Você deve ver o kernel do padrão de saudação **Python2** e Olá dois kernels nova instalação, **PySpark** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="daa53-163">You should see hello default kernel **Python2** and hello two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="daa53-164">Clique em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="daa53-164">Click **PySpark**.</span></span>

    <span data-ttu-id="daa53-165">![Kernels no bloco de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels no bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="daa53-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="daa53-166">b.</span><span class="sxs-lookup"><span data-stu-id="daa53-166">b.</span></span> <span data-ttu-id="daa53-167">Execute Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="daa53-167">Run hello following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="daa53-168">Se você pode recuperar com êxito saída hello, seu cluster de HDInsight toohello conexão é testada.</span><span class="sxs-lookup"><span data-stu-id="daa53-168">If you can successfully retrieve hello output, your connection toohello HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="daa53-169">Se você quiser tooupdate Olá notebook configuração tooconnect tooa cluster diferente, atualize Olá config. JSON com o novo conjunto de saudação de valores, conforme mostrado na etapa 3 acima.</span><span class="sxs-lookup"><span data-stu-id="daa53-169">If you want tooupdate hello notebook configuration tooconnect tooa different cluster, update hello config.json with hello new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="daa53-170">Por que devo instalar o Jupyter no meu computador?</span><span class="sxs-lookup"><span data-stu-id="daa53-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="daa53-171">Pode haver um número de motivos pelos quais você pode desejar tooinstall Jupyter em seu computador e, em seguida, conecte-se de cluster tooa Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="daa53-171">There can be a number of reasons why you might want tooinstall Jupyter on your computer and then connect it tooa Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="daa53-172">Embora os blocos de anotações do Jupyter já estão disponíveis no cluster do hello Spark no HDInsight do Azure, instalando Jupyter no seu computador fornece Olá opção toocreate seus blocos de anotações localmente, testar o aplicativo em um cluster em execução e, em seguida, carregar Olá cluster de toohello blocos de anotações.</span><span class="sxs-lookup"><span data-stu-id="daa53-172">Even though Jupyter notebooks are already available on hello Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you hello option toocreate your notebooks locally, test your application against a running cluster, and then upload hello notebooks toohello cluster.</span></span> <span data-ttu-id="daa53-173">cluster de toohello blocos de anotações do hello tooupload, você pode carregá-los usando anotações do Jupyter Olá que está em execução ou saudação do cluster ou salvá-las toohello /HdiNotebooks pasta na conta de armazenamento Olá associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="daa53-173">tooupload hello notebooks toohello cluster, you can either upload them using hello Jupyter notebook that is running or hello cluster, or save them toohello /HdiNotebooks folder in hello storage account associated with hello cluster.</span></span> <span data-ttu-id="daa53-174">Para obter mais informações sobre como os blocos de anotações são armazenados no cluster hello, consulte [blocos de anotações do Jupyter armazenamento](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="daa53-174">For more information on how notebooks are stored on hello cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="daa53-175">Com blocos de anotações Olá disponíveis localmente, você pode conectar clusters do Spark toodifferent com base em suas necessidades de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daa53-175">With hello notebooks available locally, you can connect toodifferent Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="daa53-176">Você pode usar GitHub tooimplement um sistema de controle de origem e ter controle de versão para notebooks hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-176">You can use GitHub tooimplement a source control system and have version control for hello notebooks.</span></span> <span data-ttu-id="daa53-177">Você também pode ter um ambiente de colaboração em que vários usuários podem trabalhar com hello mesmo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="daa53-177">You can also have a collaborative environment where multiple users can work with hello same notebook.</span></span>
* <span data-ttu-id="daa53-178">Você pode trabalhar com blocos de notas localmente sem sequer ter um cluster em operação.</span><span class="sxs-lookup"><span data-stu-id="daa53-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="daa53-179">Você só precisa de um cluster tootest seus blocos de anotações em, não toomanually gerenciar seus blocos de anotações ou em um ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="daa53-179">You only need a cluster tootest your notebooks against, not toomanually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="daa53-180">Ele pode ser mais fácil tooconfigure seu próprio ambiente de desenvolvimento local que a instalação de Jupyter tooconfigure Olá no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="daa53-180">It may be easier tooconfigure your own local development environment than it is tooconfigure hello Jupyter installation on hello cluster.</span></span>  <span data-ttu-id="daa53-181">Você pode tirar proveito de todos os softwares de saudação instalado localmente sem configurar um ou mais clusters remotos.</span><span class="sxs-lookup"><span data-stu-id="daa53-181">You can take advantage of all hello software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="daa53-182">Com Jupyter instalado no computador local, vários usuários podem executar Olá mesmo bloco de anotações Olá Spark mesmo cluster em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="daa53-182">With Jupyter installed on your local computer, multiple users can run hello same notebook on hello same Spark cluster at hello same time.</span></span> <span data-ttu-id="daa53-183">Nessa situação, várias sessões Livy são criadas.</span><span class="sxs-lookup"><span data-stu-id="daa53-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="daa53-184">Se você tiver um problema e deseja toodebug que, ele será um tootrack tarefa complexa que sessão Livy pertence toowhich usuário.</span><span class="sxs-lookup"><span data-stu-id="daa53-184">If you run into an issue and want toodebug that, it will be a complex task tootrack which Livy session belongs toowhich user.</span></span>
>
>

## <span data-ttu-id="daa53-185"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="daa53-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="daa53-186">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="daa53-187">Cenários</span><span class="sxs-lookup"><span data-stu-id="daa53-187">Scenarios</span></span>
* [<span data-ttu-id="daa53-188">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="daa53-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="daa53-189">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="daa53-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="daa53-190">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="daa53-190">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="daa53-191">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="daa53-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="daa53-192">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="daa53-193">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="daa53-193">Create and run applications</span></span>
* [<span data-ttu-id="daa53-194">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="daa53-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="daa53-195">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="daa53-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="daa53-196">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="daa53-196">Tools and extensions</span></span>
* [<span data-ttu-id="daa53-197">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="daa53-197">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="daa53-198">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="daa53-198">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="daa53-199">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="daa53-200">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="daa53-201">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="daa53-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="daa53-202">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="daa53-202">Manage resources</span></span>
* [<span data-ttu-id="daa53-203">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="daa53-203">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="daa53-204">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="daa53-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
