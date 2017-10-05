---
title: "Adicionar bibliotecas Hive durante a criação do cluster HDInsight – Azure | Microsoft Docs"
description: "Saiba como adicionar bibliotecas Hive (arquivos jar) a um cluster HDInsight durante a criação do cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 3412864384961e8820d6700c1bf22a4cae64ba4b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="65765-103">Adicionar bibliotecas Hive personalizadas ao criar seu cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="65765-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="65765-104">Se você tiver bibliotecas que usa frequentemente com Hive no HDInsight, este documento contém informações sobre como usar uma Ação de Script para pré-carregar as bibliotecas durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="65765-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action to pre-load the libraries during cluster creation.</span></span> <span data-ttu-id="65765-105">As bibliotecas adicionadas usando as etapas deste documento estão disponíveis globalmente no Hive — não há necessidade de usar [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) para carregá-las.</span><span class="sxs-lookup"><span data-stu-id="65765-105">Libraries added using the steps in this document are globally available in Hive - there is no need to use [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) to load them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="65765-106">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="65765-106">How it works</span></span>

<span data-ttu-id="65765-107">Ao criar um cluster, se desejar, você pode especificar uma Ação de Script que executa um script nos nós do cluster enquanto ele está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="65765-107">When creating a cluster, you can optionally specify a Script Action that runs a script on the cluster nodes while they are being created.</span></span> <span data-ttu-id="65765-108">O script neste documento aceita um único parâmetro, que é um local WASB que contém as bibliotecas (armazenadas como arquivos jar) a serem pré-carregadas.</span><span class="sxs-lookup"><span data-stu-id="65765-108">The script in this document accepts a single parameter, which is a WASB location that contains the libraries (stored as jar files) to be pre-loaded.</span></span>

<span data-ttu-id="65765-109">Durante a criação do cluster, o script enumera os arquivos, copia-os para o diretório `/usr/lib/customhivelibs/` nos nós de cabeçalho e de trabalho e adiciona-os à propriedade `hive.aux.jars.path` no arquivo `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="65765-109">During cluster creation, the script enumerates the files, copies them to the `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them to the `hive.aux.jars.path` property in the `core-site.xml` file.</span></span> <span data-ttu-id="65765-110">Em clusters baseados em Linux, ele também atualiza o arquivo `hive-env.sh` com o local dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="65765-110">On Linux-based clusters, it also updates the `hive-env.sh` file with the location of the files.</span></span>

> [!NOTE]
> <span data-ttu-id="65765-111">Usar as ações de script neste artigo disponibiliza as bibliotecas nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="65765-111">Using the script actions in this article makes the libraries available in the following scenarios:</span></span>
>
> * <span data-ttu-id="65765-112">**HDInsight baseado em Linux** — ao usar cliente Hive, **WebHCat** e **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="65765-112">**Linux-based HDInsight** - when using the a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="65765-113">**HDInsight baseado em Windows** — ao usar cliente Hive e **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="65765-113">**Windows-based HDInsight** - when using the Hive client and **WebHCat**.</span></span>

## <a name="the-script"></a><span data-ttu-id="65765-114">O script</span><span class="sxs-lookup"><span data-stu-id="65765-114">The script</span></span>

<span data-ttu-id="65765-115">**Local do script**</span><span class="sxs-lookup"><span data-stu-id="65765-115">**Script location**</span></span>

<span data-ttu-id="65765-116">Para os **clusters baseados no Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="65765-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="65765-117">Para os **clusters baseados no Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="65765-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65765-118">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="65765-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="65765-119">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="65765-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="65765-120">**Requisitos**</span><span class="sxs-lookup"><span data-stu-id="65765-120">**Requirements**</span></span>

* <span data-ttu-id="65765-121">Os scripts devem ser aplicados nos**Nós do cabeçalho** e nos **Nós de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="65765-121">The scripts must be applied to both the **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="65765-122">Os jars que você deseja instalar devem estar armazenados no Armazenamento de Blobs do Azure em um **único contêiner**.</span><span class="sxs-lookup"><span data-stu-id="65765-122">The jars you wish to install must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="65765-123">A conta de armazenamento contendo a biblioteca de arquivos jar **deve** ser vinculada ao cluster HDInsight durante a criação.</span><span class="sxs-lookup"><span data-stu-id="65765-123">The storage account containing the library of jar files **must** be linked to the HDInsight cluster during creation.</span></span> <span data-ttu-id="65765-124">Esta deve ser a conta de armazenamento padrão ou uma conta adicionada por meio da __configuração opcional__.</span><span class="sxs-lookup"><span data-stu-id="65765-124">It must either be the default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="65765-125">O caminho WASB para o contêiner deve ser especificado como um parâmetro para a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="65765-125">The WASB path to the container must be specified as a parameter to the Script Action.</span></span> <span data-ttu-id="65765-126">Por exemplo, se os jars estivessem armazenados em um contêiner denominado **libs** em uma conta de armazenamento denominada **mystorage**, o parâmetro seria **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="65765-126">For example, if the jars are stored in a container named **libs** on a storage account named **mystorage**, the parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="65765-127">Este documento supõe que você já criou uma conta de armazenamento, um contêiner de blobs, e carregou os arquivos nela.</span><span class="sxs-lookup"><span data-stu-id="65765-127">This document assumes that you have already create a storage account, blob container, and uploaded the files to it.</span></span>
  >
  > <span data-ttu-id="65765-128">Se você ainda não criou uma conta de armazenamento, faça isso usando o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65765-128">If you have not created a storage account, you can do so through the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="65765-129">Lá, você pode usar um utilitário como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/) para criar um contêiner na conta e carregar arquivo nele.</span><span class="sxs-lookup"><span data-stu-id="65765-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) to create a container in the account and upload files to it.</span></span>

## <a name="create-a-cluster-using-the-script"></a><span data-ttu-id="65765-130">Criar um cluster usando o script</span><span class="sxs-lookup"><span data-stu-id="65765-130">Create a cluster using the script</span></span>

> [!NOTE]
> <span data-ttu-id="65765-131">As etapas a seguir criam um cluster HDInsight baseado no Linux.</span><span class="sxs-lookup"><span data-stu-id="65765-131">The following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="65765-132">Para criar um cluster baseado no Windows, escolha **Windows** como o SO do cluster ao criar o cluster e use o script do Windows (PowerShell) em vez do script bash.</span><span class="sxs-lookup"><span data-stu-id="65765-132">To create a Windows-based cluster, select **Windows** as the cluster OS when creating the cluster, and use the Windows (PowerShell) script instead of the bash script.</span></span>
>
> <span data-ttu-id="65765-133">Você também pode usar o Azure PowerShell ou o SDK do .NET do HDInsight para criar um cluster usando esse script.</span><span class="sxs-lookup"><span data-stu-id="65765-133">You can also use Azure PowerShell or the HDInsight .NET SDK to create a cluster using this script.</span></span> <span data-ttu-id="65765-134">Para obter mais informações sobre como usar esses métodos, consulte [Personalizar clusters HDInsight com Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65765-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="65765-135">Inicie provisionando um cluster com as etapas em [Provisionar clusters HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não conclua o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="65765-135">Start provisioning a cluster by using the steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="65765-136">Na folha **Configuração Opcional**, escolha **Ações de Script** e forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="65765-136">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="65765-137">**NOME**: insira um nome amigável para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="65765-137">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="65765-138">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="65765-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="65765-139">**CABEÇALHO**: marque esta opção.</span><span class="sxs-lookup"><span data-stu-id="65765-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="65765-140">**TRABALHO**: marque esta opção.</span><span class="sxs-lookup"><span data-stu-id="65765-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="65765-141">**ZOOKEEPER**: deixe essa opção em branco.</span><span class="sxs-lookup"><span data-stu-id="65765-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="65765-142">**PARÂMETROS**: insira o endereço WASB para o contêiner e a conta de armazenamento que contém os jars.</span><span class="sxs-lookup"><span data-stu-id="65765-142">**PARAMETERS**: Enter the WASB address to the container and storage account that contains the jars.</span></span> <span data-ttu-id="65765-143">Por exemplo, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="65765-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="65765-144">Na parte inferior das **Ações de Script**, use o botão **Selecionar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="65765-144">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span>

4. <span data-ttu-id="65765-145">Na folha **Configuração Opcional**, selecione **Contas de Armazenamento vinculadas** e selecione o link **Adicionar uma chave de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="65765-145">On the **Optional Configuration** blade, select **Linked Storage Accounts** and select the **Add a storage key** link.</span></span> <span data-ttu-id="65765-146">Selecione a conta de armazenamento que contém os jars, em seguida, use os botões de **seleção** para salvar as configurações e retornar para a folha **Configuração Opcional**.</span><span class="sxs-lookup"><span data-stu-id="65765-146">Select the storage account that contains the jars, and then use the **select** buttons to save settings and return the **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="65765-147">Use o botão **Selecionar** na parte inferior da folha **Configuração Opcional** para salvar as informações da configuração opcional.</span><span class="sxs-lookup"><span data-stu-id="65765-147">Use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

6. <span data-ttu-id="65765-148">Continue a provisionar o cluster como descrito em [Provisionar clusters HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="65765-148">Continue provisioning the cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="65765-149">Assim que a criação do cluster for concluída, você poderá usar os jars adicionados do Hive por meio desse script sem precisar usar a instrução `ADD JAR`.</span><span class="sxs-lookup"><span data-stu-id="65765-149">Once cluster creation finishes, you are able to use the jars added through this script from Hive without having to use the `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65765-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65765-150">Next steps</span></span>

<span data-ttu-id="65765-151">Para saber mais sobre como trabalhar com o Hive, confira [Usar o Hive com o HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="65765-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
