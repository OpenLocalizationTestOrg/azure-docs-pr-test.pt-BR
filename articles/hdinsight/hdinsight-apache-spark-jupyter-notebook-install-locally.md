---
title: Instalar o Jupyter localmente e conectar-se a um cluster do Spark do Azure HDInsight | Microsoft Docs
description: "Saiba mais sobre como instalar o bloco de anotações do Jupyter localmente em seu computador e se conectar a um cluster Apache Spark no Azure HDInsight."
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
ms.openlocfilehash: fe9dcdb643aa6a8ee5d55738b7a446e4b0153986
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-to-apache-spark-on-hdinsight"></a><span data-ttu-id="7eea0-103">Instalar o bloco de anotações do Jupyter em seu computador e conectar-se ao Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-103">Install Jupyter notebook on your computer and connect to Apache Spark on HDInsight</span></span>

<span data-ttu-id="7eea0-104">Neste artigo, você aprende como instalar blocos de notas Jupyter, com o PySpark personalizado (para o Python) e kernels Spark (para Scala) com a mágica de Spark, e conectar o bloco de notas a um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7eea0-104">In this article you learn how to install Jupyter notebook, with the custom PySpark (for Python) and Spark (for Scala) kernels with Spark magic, and connect the notebook to an HDInsight cluster.</span></span> <span data-ttu-id="7eea0-105">Pode haver inúmeros motivos para instalar o Jupyter no computador local e alguns desafios também.</span><span class="sxs-lookup"><span data-stu-id="7eea0-105">There can be a number of reasons to install Jupyter on your local computer, and there can be some challenges as well.</span></span> <span data-ttu-id="7eea0-106">Para saber mais sobre isso, confira a seção [Por que devo instalar o Jupyter no meu computador](#why-should-i-install-jupyter-on-my-computer) no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7eea0-106">For more on this, see the section [Why should I install Jupyter on my computer](#why-should-i-install-jupyter-on-my-computer) at the end of this article.</span></span>

<span data-ttu-id="7eea0-107">Há três etapas principais envolvidas na instalação do Jupyter e da mágica do Spark em seu computador.</span><span class="sxs-lookup"><span data-stu-id="7eea0-107">There are three key steps involved in installing Jupyter and the Spark magic on your computer.</span></span>

* <span data-ttu-id="7eea0-108">Instalar bloco de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="7eea0-108">Install Jupyter notebook</span></span>
* <span data-ttu-id="7eea0-109">Instalar os kernels PySpark e Spark com a mágica do Spark</span><span class="sxs-lookup"><span data-stu-id="7eea0-109">Install the PySpark and Spark kernels with the Spark magic</span></span>
* <span data-ttu-id="7eea0-110">Configure a mágica do Spark para acessar o cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-110">Configure Spark magic to access Spark cluster on HDInsight</span></span>

<span data-ttu-id="7eea0-111">Para saber mais sobre os kernels personalizados e a sobre a mágica Spark disponível para blocos de notas Jupyter com o cluster HDInsight, confira [Kernels disponíveis para blocos de notas Jupyter com clusters do Apache Spark Linux no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7eea0-111">For more information about the custom kernels and the Spark magic available for Jupyter notebooks with HDInsight cluster, see [Kernels available for Jupyter notebooks with Apache Spark Linux clusters on HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7eea0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7eea0-112">Prerequisites</span></span>
<span data-ttu-id="7eea0-113">Os pré-requisitos listados aqui não são para a instalação do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7eea0-113">The prerequisites listed here are not for installing Jupyter.</span></span> <span data-ttu-id="7eea0-114">Eles são para conectar o bloco de notas Jupyter a um cluster HDInsight depois que o bloco de notas está instalado.</span><span class="sxs-lookup"><span data-stu-id="7eea0-114">These are for connecting the Jupyter notebook to an HDInsight cluster once the notebook is installed.</span></span>

* <span data-ttu-id="7eea0-115">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eea0-115">An Azure subscription.</span></span> <span data-ttu-id="7eea0-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7eea0-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7eea0-117">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7eea0-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7eea0-118">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7eea0-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="install-jupyter-notebook-on-your-computer"></a><span data-ttu-id="7eea0-119">Instalar bloco de notas Jupyter em seu computador</span><span class="sxs-lookup"><span data-stu-id="7eea0-119">Install Jupyter notebook on your computer</span></span>

<span data-ttu-id="7eea0-120">Você deve instalar o Python antes de instalar notebooks do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7eea0-120">You  must install Python before you can install Jupyter notebooks.</span></span> <span data-ttu-id="7eea0-121">Ambos o Python e o Jupyter estão disponíveis como parte da [distribuição do Anaconda](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="7eea0-121">Both Python and Jupyter are available as part of the [Anaconda distribution](https://www.continuum.io/downloads).</span></span> <span data-ttu-id="7eea0-122">Quando instala o Anaconda, você instala uma distribuição do Python.</span><span class="sxs-lookup"><span data-stu-id="7eea0-122">When you install Anaconda, you install a distribution of Python.</span></span> <span data-ttu-id="7eea0-123">Quando o Anaconda é instalado, você adiciona a instalação do Jupyter executando comandos apropriados.</span><span class="sxs-lookup"><span data-stu-id="7eea0-123">Once Anaconda is installed, you add the Jupyter installation by running appropriate commands.</span></span>

1. <span data-ttu-id="7eea0-124">Baixe o [instalador do Anaconda](https://www.continuum.io/downloads) para sua plataforma e execute a instalação.</span><span class="sxs-lookup"><span data-stu-id="7eea0-124">Download the [Anaconda installer](https://www.continuum.io/downloads) for your platform and run the setup.</span></span> <span data-ttu-id="7eea0-125">Ao executar o assistente de instalação, não deixe de selecionar a opção de adicionar o Anaconda à variável PATH.</span><span class="sxs-lookup"><span data-stu-id="7eea0-125">While running the setup wizard, make sure you select the option to add Anaconda to your PATH variable.</span></span>
2. <span data-ttu-id="7eea0-126">Execute o comando a seguir para instalar o Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7eea0-126">Run the following command to install Jupyter.</span></span>

        conda install jupyter

    <span data-ttu-id="7eea0-127">Para obter mais informações sobre a instalação do Jupyter, confira [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Instalando o Jupyter usando o Anaconda).</span><span class="sxs-lookup"><span data-stu-id="7eea0-127">For more information on installing Jupyter, see [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html).</span></span>

## <a name="install-the-kernels-and-spark-magic"></a><span data-ttu-id="7eea0-128">Instalar os kernels e a mágica do Spark</span><span class="sxs-lookup"><span data-stu-id="7eea0-128">Install the kernels and Spark magic</span></span>

<span data-ttu-id="7eea0-129">Para obter instruções sobre como instalar a mágica do Spark, os kernels PySpark e Spark, siga as instruções da instalação na [documentação do sparkmagic](https://github.com/jupyter-incubator/sparkmagic#installation) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7eea0-129">For instructions on how to install the Spark magic, the PySpark and Spark kernels, follow the installation instructions in the [sparkmagic documentation](https://github.com/jupyter-incubator/sparkmagic#installation) on GitHub.</span></span> <span data-ttu-id="7eea0-130">A primeira etapa na documentação da mágica do Spark solicita a instalação da mágica do Spark.</span><span class="sxs-lookup"><span data-stu-id="7eea0-130">The first step in the Spark magic documentation asks you to install Spark magic.</span></span> <span data-ttu-id="7eea0-131">Substitua essa primeira etapa no link com os seguintes comandos, dependendo da versão do cluster do HDInsight de conexão.</span><span class="sxs-lookup"><span data-stu-id="7eea0-131">Replace that first step in the link with the following commands, depending on the version of the HDInsight cluster you will connect to.</span></span> <span data-ttu-id="7eea0-132">Depois disso, siga as etapas restantes na documentação da mágica do Spark.</span><span class="sxs-lookup"><span data-stu-id="7eea0-132">After that, follow the remaining steps in the Spark magic documentation.</span></span> <span data-ttu-id="7eea0-133">Se quiser instalar os kernels diferentes, você deverá executar a Etapa 3 na seção de instruções da instalação da mágica do Spark.</span><span class="sxs-lookup"><span data-stu-id="7eea0-133">If you want to install the different kernels, you must perform Step 3 in the Spark magic installation instructions section.</span></span>

* <span data-ttu-id="7eea0-134">Para clusters v3.4, instale sparkmagic 0.2.3 executando `pip install sparkmagic==0.2.3`</span><span class="sxs-lookup"><span data-stu-id="7eea0-134">For clusters v3.4, install sparkmagic 0.2.3 by executing `pip install sparkmagic==0.2.3`</span></span>

* <span data-ttu-id="7eea0-135">Para clusters v3.5 e v3.6, instale sparkmagic 0.11.2 executando `pip install sparkmagic==0.11.2`</span><span class="sxs-lookup"><span data-stu-id="7eea0-135">For clusters v3.5 and v3.6, install sparkmagic 0.11.2 by executing `pip install sparkmagic==0.11.2`</span></span>

## <a name="configure-spark-magic-to-connect-to-hdinsight-spark-cluster"></a><span data-ttu-id="7eea0-136">Configurar a mágica do Spark para se conectar ao cluster do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="7eea0-136">Configure Spark magic to connect to HDInsight Spark cluster</span></span>

<span data-ttu-id="7eea0-137">Nesta seção, você configura a mágica do Spark instalada anteriormente para se conectar a um cluster Apache Spark que já deve ter criado no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7eea0-137">In this section you configure the Spark magic that you installed earlier to connect to an Apache Spark cluster that you must have already created in Azure HDInsight.</span></span>

1. <span data-ttu-id="7eea0-138">As informações de configuração do Jupyter normalmente são armazenadas no diretório base dos usuários.</span><span class="sxs-lookup"><span data-stu-id="7eea0-138">The Jupyter configuration information is typically stored in the users home directory.</span></span> <span data-ttu-id="7eea0-139">Para localizar seu diretório base em qualquer plataforma de sistema operacional, digite os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7eea0-139">To locate your home directory on any OS platform, type the following commands.</span></span>

    <span data-ttu-id="7eea0-140">Inicie o shell do Python.</span><span class="sxs-lookup"><span data-stu-id="7eea0-140">Start the Python shell.</span></span> <span data-ttu-id="7eea0-141">Em uma janela de comando, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7eea0-141">On a command window, type the following:</span></span>

        python

    <span data-ttu-id="7eea0-142">No shell do Python, digite o comando a seguir para localizar o diretório base.</span><span class="sxs-lookup"><span data-stu-id="7eea0-142">On the Python shell, enter the following command to find out the home directory.</span></span>

        import os
        print(os.path.expanduser('~'))

2. <span data-ttu-id="7eea0-143">Navegue até o diretório base e crie uma pasta chamada **.sparkmagic** , caso ela ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="7eea0-143">Navigate to the home directory and create a folder called **.sparkmagic** if it does not already exist.</span></span>
3. <span data-ttu-id="7eea0-144">Dentro da pasta, crie um arquivo chamado **config.json** e adicione o trecho de código JSON a seguir dentro dele.</span><span class="sxs-lookup"><span data-stu-id="7eea0-144">Within the folder, create a file called **config.json** and add the following JSON snippet inside it.</span></span>

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

4. <span data-ttu-id="7eea0-145">Substitua **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** pelos valores apropriados.</span><span class="sxs-lookup"><span data-stu-id="7eea0-145">Substitute **{USERNAME}**, **{CLUSTERDNSNAME}**, and **{BASE64ENCODEDPASSWORD}** with appropriate values.</span></span> <span data-ttu-id="7eea0-146">Você pode usar vários utilitários em sua linguagem de programação favorita ou online para gerar uma senha codificada em base64 para sua senha real.</span><span class="sxs-lookup"><span data-stu-id="7eea0-146">You can use a number of utilities in your favorite programming language or online to generate a base64 encoded password for your actual password.</span></span>

5. <span data-ttu-id="7eea0-147">Defina as configurações corretas de Pulsação em `config.json`.</span><span class="sxs-lookup"><span data-stu-id="7eea0-147">Configure the right Heartbeat settings in `config.json`.</span></span> <span data-ttu-id="7eea0-148">Você deve adicionar essas configurações no mesmo nível que os trechos `kernel_python_credentials` e `kernel_scala_credentials` adicionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7eea0-148">You should add these settings at the same level as the `kernel_python_credentials` and `kernel_scala_credentials` snippets your added earlier.</span></span> <span data-ttu-id="7eea0-149">Para obter um exemplo de como e onde adicionar as configurações de pulsação, consulte este [exemplo de config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span><span class="sxs-lookup"><span data-stu-id="7eea0-149">For an example on how and where to add the heartbeat settings, see this [sample config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).</span></span>

    * <span data-ttu-id="7eea0-150">Para `sparkmagic 0.2.3` (clusters v3.4), incluem:</span><span class="sxs-lookup"><span data-stu-id="7eea0-150">For `sparkmagic 0.2.3` (clusters v3.4), include:</span></span>

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * <span data-ttu-id="7eea0-151">Para `sparkmagic 0.11.2` (clusters v3.5 e v3.6), inclua:</span><span class="sxs-lookup"><span data-stu-id="7eea0-151">For `sparkmagic 0.11.2` (clusters v3.5 and v3.6), include:</span></span>

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    ><span data-ttu-id="7eea0-152">As pulsações são enviadas para garantir que as sessões não sejam perdidas.</span><span class="sxs-lookup"><span data-stu-id="7eea0-152">Heartbeats are sent to ensure that sessions are not leaked.</span></span> <span data-ttu-id="7eea0-153">Quando um computador entra em suspensão ou está desligado, a pulsação não é enviada e, como resultado, a sessão é limpa.</span><span class="sxs-lookup"><span data-stu-id="7eea0-153">When a computer goes to sleep or is shut down, the heartbeat is not sent, resulting in the session being cleaned up.</span></span> <span data-ttu-id="7eea0-154">Para clusters v3.4, se desejar desabilitar esse comportamento, você poderá definir a configuração Livy `livy.server.interactive.heartbeat.timeout` para `0` da interface do usuário do Ambari.</span><span class="sxs-lookup"><span data-stu-id="7eea0-154">For clusters v3.4, if you wish to disable this behavior, you can set the Livy config `livy.server.interactive.heartbeat.timeout` to `0` from the Ambari UI.</span></span> <span data-ttu-id="7eea0-155">Para clusters v3.5, se você não definir a configuração de 3.5 ou acima, a sessão não será excluída.</span><span class="sxs-lookup"><span data-stu-id="7eea0-155">For clusters v3.5, if you do not set the 3.5 configuration above, the session will not be deleted.</span></span>

6. <span data-ttu-id="7eea0-156">Inicie o Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7eea0-156">Start Jupyter.</span></span> <span data-ttu-id="7eea0-157">Use o comando do prompt de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7eea0-157">Use the following command from the command prompt.</span></span>

        jupyter notebook

7. <span data-ttu-id="7eea0-158">Verifique se você pode se conectar ao cluster usando o bloco de notas Jupyter e se você pode usar a mágica Spark disponível com os kernels.</span><span class="sxs-lookup"><span data-stu-id="7eea0-158">Verify that you can connect to the cluster using the Jupyter notebook and that you can use the Spark magic available with the kernels.</span></span> <span data-ttu-id="7eea0-159">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7eea0-159">Perform the following steps.</span></span>

    <span data-ttu-id="7eea0-160">a.</span><span class="sxs-lookup"><span data-stu-id="7eea0-160">a.</span></span> <span data-ttu-id="7eea0-161">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="7eea0-161">Create a new notebook.</span></span> <span data-ttu-id="7eea0-162">Do canto direito, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="7eea0-162">From the right-hand corner, click **New**.</span></span> <span data-ttu-id="7eea0-163">Você deve ver o kernel padrão **Python2** e os dois kernels novos instalados, **PySpark** e **Spark**.</span><span class="sxs-lookup"><span data-stu-id="7eea0-163">You should see the default kernel **Python2** and the two new kernels that you install, **PySpark** and **Spark**.</span></span> <span data-ttu-id="7eea0-164">Clique em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="7eea0-164">Click **PySpark**.</span></span>

    <span data-ttu-id="7eea0-165">![Kernels no bloco de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels no bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="7eea0-165">![Kernels in Jupyter notebook](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels in Jupyter notebook")</span></span>

    <span data-ttu-id="7eea0-166">b.</span><span class="sxs-lookup"><span data-stu-id="7eea0-166">b.</span></span> <span data-ttu-id="7eea0-167">Execute o trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7eea0-167">Run the following code snippet.</span></span>

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    <span data-ttu-id="7eea0-168">Se você puder recuperar a saída com êxito, a conexão com o cluster HDInsight será testada.</span><span class="sxs-lookup"><span data-stu-id="7eea0-168">If you can successfully retrieve the output, your connection to the HDInsight cluster is tested.</span></span>

    >[!TIP]
    ><span data-ttu-id="7eea0-169">Se você quiser atualizar a configuração do bloco de notas para se conectar a um cluster diferente, atualize o config.json com o novo conjunto de valores, conforme mostrado na Etapa 3 acima.</span><span class="sxs-lookup"><span data-stu-id="7eea0-169">If you want to update the notebook configuration to connect to a different cluster, update the config.json with the new set of values, as shown in Step 3 above.</span></span>

## <a name="why-should-i-install-jupyter-on-my-computer"></a><span data-ttu-id="7eea0-170">Por que devo instalar o Jupyter no meu computador?</span><span class="sxs-lookup"><span data-stu-id="7eea0-170">Why should I install Jupyter on my computer?</span></span>
<span data-ttu-id="7eea0-171">Pode haver vários motivos pelos quais você possa querer instalar o Jupyter no computador e conectá-lo a um cluster Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7eea0-171">There can be a number of reasons why you might want to install Jupyter on your computer and then connect it to a Spark cluster on HDInsight.</span></span>

* <span data-ttu-id="7eea0-172">Mesmo que os blocos de notas Jupyter já estejam disponíveis no cluster Spark no Azure HDInsight, a instalação do Jupyter no seu computador fornece a opção de criar os blocos de notas localmente, de testar o aplicativo em um cluster em execução e de carregar os blocos de notas no cluster.</span><span class="sxs-lookup"><span data-stu-id="7eea0-172">Even though Jupyter notebooks are already available on the Spark cluster in Azure HDInsight, installing Jupyter on your computer provides you the option to create your notebooks locally, test your application against a running cluster, and then upload the notebooks to the cluster.</span></span> <span data-ttu-id="7eea0-173">Para carregar os blocos de notas no cluster, você pode carregá-los usando o bloco de notas Jupyter que está em execução ou o cluster, ou salvá-los na pasta /HdiNotebooks na conta de armazenamento associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="7eea0-173">To upload the notebooks to the cluster, you can either upload them using the Jupyter notebook that is running or the cluster, or save them to the /HdiNotebooks folder in the storage account associated with the cluster.</span></span> <span data-ttu-id="7eea0-174">Para saber mais sobre como os blocos de notas são armazenados no cluster, confira [Onde os blocos de notas Jupyter são armazenados](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span><span class="sxs-lookup"><span data-stu-id="7eea0-174">For more information on how notebooks are stored on the cluster, see [Where are Jupyter notebooks stored](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?</span></span>
* <span data-ttu-id="7eea0-175">Com os blocos de notas disponíveis localmente, você pode se conectar a clusters Spark diferentes com base nos requisitos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7eea0-175">With the notebooks available locally, you can connect to different Spark clusters based on your application requirement.</span></span>
* <span data-ttu-id="7eea0-176">É possível usar o GitHub para implementar um sistema de controle de origem e ter o controle de versão para os blocos de notas.</span><span class="sxs-lookup"><span data-stu-id="7eea0-176">You can use GitHub to implement a source control system and have version control for the notebooks.</span></span> <span data-ttu-id="7eea0-177">Você também pode ter um ambiente colaborativo, onde vários usuários podem trabalhar com o mesmo bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="7eea0-177">You can also have a collaborative environment where multiple users can work with the same notebook.</span></span>
* <span data-ttu-id="7eea0-178">Você pode trabalhar com blocos de notas localmente sem sequer ter um cluster em operação.</span><span class="sxs-lookup"><span data-stu-id="7eea0-178">You can work with notebooks locally without even having a cluster up.</span></span> <span data-ttu-id="7eea0-179">É preciso apenas um cluster no qual testar seus blocos de notas, e não para gerenciar manualmente os blocos de notas ou um ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7eea0-179">You only need a cluster to test your notebooks against, not to manually manage your notebooks or a development environment.</span></span>
* <span data-ttu-id="7eea0-180">Pode ser mais fácil configurar seu próprio ambiente de desenvolvimento local que configurar a instalação do Jupyter no cluster.</span><span class="sxs-lookup"><span data-stu-id="7eea0-180">It may be easier to configure your own local development environment than it is to configure the Jupyter installation on the cluster.</span></span>  <span data-ttu-id="7eea0-181">É possível aproveitar todo o software que você tem instalado localmente sem configurar um ou mais clusters remotos.</span><span class="sxs-lookup"><span data-stu-id="7eea0-181">You can take advantage of all the software you have installed locally without configuring one or more remote clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="7eea0-182">Com o Jupyter instalado no computador local, vários usuários podem executar o mesmo bloco de notas no mesmo cluster Spark ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="7eea0-182">With Jupyter installed on your local computer, multiple users can run the same notebook on the same Spark cluster at the same time.</span></span> <span data-ttu-id="7eea0-183">Nessa situação, várias sessões Livy são criadas.</span><span class="sxs-lookup"><span data-stu-id="7eea0-183">In such a situation, multiple Livy sessions are created.</span></span> <span data-ttu-id="7eea0-184">Se você tiver um problema e desejar depurá-lo, será uma tarefa complexa rastrear qual sessão Livy pertence a qual usuário.</span><span class="sxs-lookup"><span data-stu-id="7eea0-184">If you run into an issue and want to debug that, it will be a complex task to track which Livy session belongs to which user.</span></span>
>
>

## <span data-ttu-id="7eea0-185"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="7eea0-185"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="7eea0-186">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-186">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7eea0-187">Cenários</span><span class="sxs-lookup"><span data-stu-id="7eea0-187">Scenarios</span></span>
* [<span data-ttu-id="7eea0-188">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="7eea0-188">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7eea0-189">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="7eea0-189">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7eea0-190">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para prever resultados da inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="7eea0-190">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7eea0-191">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="7eea0-191">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7eea0-192">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-192">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="7eea0-193">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="7eea0-193">Create and run applications</span></span>
* [<span data-ttu-id="7eea0-194">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="7eea0-194">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7eea0-195">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="7eea0-195">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7eea0-196">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="7eea0-196">Tools and extensions</span></span>
* [<span data-ttu-id="7eea0-197">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="7eea0-197">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7eea0-198">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="7eea0-198">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7eea0-199">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-199">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7eea0-200">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-200">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7eea0-201">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="7eea0-201">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a><span data-ttu-id="7eea0-202">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="7eea0-202">Manage resources</span></span>
* [<span data-ttu-id="7eea0-203">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-203">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7eea0-204">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7eea0-204">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
