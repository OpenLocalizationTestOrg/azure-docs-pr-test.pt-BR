---
title: "bibliotecas de Hive aaaAdd durante HDInsight cluster criação - Azure | Microsoft Docs"
description: "Saiba como bibliotecas de Hive tooadd (arquivos jar), tooan HDInsight cluster durante a criação do cluster."
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
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="29b74-103">Adicionar bibliotecas Hive personalizadas ao criar seu cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="29b74-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="29b74-104">Se você tiver bibliotecas que você usa com frequência com Hive no HDInsight, este documento contém informações sobre como usar bibliotecas de Olá de toopre carga uma ação de Script durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="29b74-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="29b74-105">Bibliotecas adicionadas usando etapas Olá neste documento estão disponíveis globalmente no Hive - não há nenhuma necessidade toouse [Adicionar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload-los.</span><span class="sxs-lookup"><span data-stu-id="29b74-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="29b74-106">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="29b74-106">How it works</span></span>

<span data-ttu-id="29b74-107">Ao criar um cluster, você pode opcionalmente especificar uma ação de Script que executa um script em nós de cluster Olá enquanto estão sendo criados.</span><span class="sxs-lookup"><span data-stu-id="29b74-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="29b74-108">script Hello neste documento aceita um único parâmetro, que é um local de WASB que contém a saudação bibliotecas (armazenadas como arquivos jar) toobe pré-carregado.</span><span class="sxs-lookup"><span data-stu-id="29b74-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="29b74-109">Durante a criação do cluster, o script hello enumera arquivos hello, copia toohello `/usr/lib/customhivelibs/` diretório em nós de cabeçalho e de trabalho, em seguida, adiciona toohello `hive.aux.jars.path` propriedade Olá `core-site.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="29b74-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="29b74-110">Em clusters baseados em Linux, ela também atualiza Olá `hive-env.sh` arquivo com hello local dos arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="29b74-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="29b74-111">Usar ações de script hello neste artigo disponibiliza bibliotecas Olá no hello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="29b74-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="29b74-112">**HDInsight baseados em Linux** - quando usando Olá um cliente de Hive, **WebHCat**, e **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="29b74-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="29b74-113">**HDInsight baseados em Windows** - ao usar o cliente de Hive hello e **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="29b74-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="29b74-114">script Hello</span><span class="sxs-lookup"><span data-stu-id="29b74-114">hello script</span></span>

<span data-ttu-id="29b74-115">**Local do script**</span><span class="sxs-lookup"><span data-stu-id="29b74-115">**Script location**</span></span>

<span data-ttu-id="29b74-116">Para os **clusters baseados no Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="29b74-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="29b74-117">Para os **clusters baseados no Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="29b74-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29b74-118">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="29b74-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="29b74-119">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="29b74-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="29b74-120">**Requisitos**</span><span class="sxs-lookup"><span data-stu-id="29b74-120">**Requirements**</span></span>

* <span data-ttu-id="29b74-121">scripts de saudação devem ser aplicada tooboth Olá **nós de cabeçalho** e **nós de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="29b74-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="29b74-122">Olá jars desejar tooinstall devem ser armazenados no armazenamento de BLOBs do Azure em um **único contêiner**.</span><span class="sxs-lookup"><span data-stu-id="29b74-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="29b74-123">conta de armazenamento Olá que contém a biblioteca de saudação arquivos jar **deve** ser vinculada toohello HDInsight cluster durante a criação.</span><span class="sxs-lookup"><span data-stu-id="29b74-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="29b74-124">Ele deve ser conta de armazenamento saudação padrão ou uma conta adicionada por meio de __configuração opcional__.</span><span class="sxs-lookup"><span data-stu-id="29b74-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="29b74-125">contêiner de toohello Olá WASB caminho deve ser especificado como uma ação de Script de toohello do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="29b74-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="29b74-126">Por exemplo, se hello jars são armazenados em um contêiner chamado **bibliotecas** em uma conta de armazenamento denominada **mystorage**, parâmetro hello seria  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="29b74-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="29b74-127">Este documento assume que você já crie uma conta de armazenamento, contêiner de blob e carregado Olá arquivos tooit.</span><span class="sxs-lookup"><span data-stu-id="29b74-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="29b74-128">Se você não tiver criado uma conta de armazenamento, você pode fazer isso por meio de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29b74-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="29b74-129">Você pode usar um utilitário como [Azure Storage Explorer](http://storageexplorer.com/) toocreate um contêiner na conta de saudação e carregar arquivos tooit.</span><span class="sxs-lookup"><span data-stu-id="29b74-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="29b74-130">Criar um cluster usando o script hello</span><span class="sxs-lookup"><span data-stu-id="29b74-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="29b74-131">Olá etapas a seguir cria um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="29b74-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="29b74-132">toocreate um cluster baseado no Windows, selecione **Windows** como Olá cluster sistema operacional durante a criação de cluster hello e usar script de saudação do Windows (PowerShell) em vez de scripts de bash Olá.</span><span class="sxs-lookup"><span data-stu-id="29b74-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="29b74-133">Você também pode usar o Azure PowerShell ou Olá HDInsight .NET SDK toocreate um cluster usando esse script.</span><span class="sxs-lookup"><span data-stu-id="29b74-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="29b74-134">Para obter mais informações sobre como usar esses métodos, consulte [Personalizar clusters HDInsight com Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="29b74-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="29b74-135">Iniciar o provisionamento de um cluster usando as etapas de saudação em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não conclua o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="29b74-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="29b74-136">Em Olá **configuração opcional** folha, selecione **ações de Script**e fornecer Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="29b74-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="29b74-137">**NOME**: insira um nome amigável para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="29b74-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="29b74-138">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="29b74-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="29b74-139">**CABEÇALHO**: marque esta opção.</span><span class="sxs-lookup"><span data-stu-id="29b74-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="29b74-140">**TRABALHO**: marque esta opção.</span><span class="sxs-lookup"><span data-stu-id="29b74-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="29b74-141">**ZOOKEEPER**: deixe essa opção em branco.</span><span class="sxs-lookup"><span data-stu-id="29b74-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="29b74-142">**PARÂMETROS**: insira Olá WASB endereço toohello contêiner e conta de armazenamento que contém os jars hello.</span><span class="sxs-lookup"><span data-stu-id="29b74-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="29b74-143">Por exemplo, **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="29b74-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="29b74-144">Na parte inferior de saudação do hello **ações de Script**, use Olá **selecione** configuração de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="29b74-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="29b74-145">Em Olá **configuração opcional** folha, selecione **contas de armazenamento vinculadas** e selecione hello **adicionar uma chave de armazenamento** link.</span><span class="sxs-lookup"><span data-stu-id="29b74-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="29b74-146">Selecionar conta de armazenamento Olá que contém os jars hello e use Olá **selecione** configurações de toosave de botões e hello retorno **configuração opcional** folha.</span><span class="sxs-lookup"><span data-stu-id="29b74-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="29b74-147">Saudação de uso **selecione** botão na parte inferior de saudação do hello **configuração opcional** informações de configuração opcional de saudação de toosave de folha.</span><span class="sxs-lookup"><span data-stu-id="29b74-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="29b74-148">Continuar o provisionamento de cluster Olá conforme descrito em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="29b74-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="29b74-149">Depois de termina a criação do cluster, você está jars do hello capaz de toouse adicionadas por este script de Hive sem ter que toouse Olá `ADD JAR` instrução.</span><span class="sxs-lookup"><span data-stu-id="29b74-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29b74-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29b74-150">Next steps</span></span>

<span data-ttu-id="29b74-151">Para saber mais sobre como trabalhar com o Hive, confira [Usar o Hive com o HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="29b74-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
