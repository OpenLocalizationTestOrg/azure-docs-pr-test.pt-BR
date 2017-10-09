---
title: aaaGet iniciada com o servidor do R no HDInsight - Azure | Microsoft Docs
description: Saiba como toocreate um Apache despertar no cluster HDInsight que inclui o R Server e enviar um script R no cluster hello.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a><span data-ttu-id="e8f2a-103">Aprenda a usar o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8f2a-103">Get started using R Server on HDInsight</span></span>

<span data-ttu-id="e8f2a-104">HDInsight inclui um toobe de opção R Server integrado ao seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-104">HDInsight includes an R Server option toobe integrated into your HDInsight cluster.</span></span> <span data-ttu-id="e8f2a-105">Essa opção permite que scripts R toouse Spark e MapReduce cálculos de toorun distribuído.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-105">This option allows R scripts toouse Spark and MapReduce toorun distributed computations.</span></span> <span data-ttu-id="e8f2a-106">Neste documento, você aprenderá como toocreate um R Server no cluster HDInsight e, em seguida, executar um R script que demonstra o uso do Spark para distribuídos cálculos de R.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-106">In this document, you learn how toocreate an R Server on HDInsight cluster and then run an R script that demonstrates using Spark for distributed R computations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e8f2a-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e8f2a-107">Prerequisites</span></span>

* <span data-ttu-id="e8f2a-108">**Uma assinatura do Azure**: antes de começar este tutorial, você deve ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-108">**An Azure subscription**: Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="e8f2a-109">Artigo vá toohello [avaliação gratuita do Microsoft Azure obter](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-109">Go toohello article [Get Microsoft Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) for more information.</span></span>
* <span data-ttu-id="e8f2a-110">**Um cliente do Secure Shell (SSH)**: um SSH cliente é usado tooremotely conectar o cluster do HDInsight toohello e executar comandos diretamente no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-110">**A Secure Shell (SSH) client**: An SSH client is used tooremotely connect toohello HDInsight cluster and run commands directly on hello cluster.</span></span> <span data-ttu-id="e8f2a-111">Para obter mais informações, confira [Usar SSH com HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="e8f2a-111">For more information, see [Use SSH with HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
* <span data-ttu-id="e8f2a-112">**As chaves de SSH (opcionais)**: você pode proteger a saudação SSH conta usada tooconnect toohello cluster usando uma senha ou uma chave pública.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-112">**SSH keys (optional)**: You can secure hello SSH account used tooconnect toohello cluster using either a password or a public key.</span></span> <span data-ttu-id="e8f2a-113">Usando uma senha é mais fácil e permite que você tooget iniciado sem toocreate um par de chaves pública/privada.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-113">Using a password is easier, and allows you tooget started without having toocreate a public/private key pair.</span></span> <span data-ttu-id="e8f2a-114">No entanto, usar uma chave é mais seguro.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-114">However, using a key is more secure.</span></span>

> [!NOTE]
> <span data-ttu-id="e8f2a-115">etapas de saudação neste documento pressupõem que você está usando uma senha.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-115">hello steps in this document assume that you are using a password.</span></span>


## <a name="automated-cluster-creation"></a><span data-ttu-id="e8f2a-116">Criação de cluster automatizada</span><span class="sxs-lookup"><span data-stu-id="e8f2a-116">Automated cluster creation</span></span>

<span data-ttu-id="e8f2a-117">Você pode automatizar a criação de saudação do HDInsight R Servers usando o Gerenciador de recursos do Azure modelos, Olá SDK e também PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-117">You can automate hello creation of HDInsight R Servers using Azure Resource Manager templates, hello SDK, and also PowerShell.</span></span>

* <span data-ttu-id="e8f2a-118">toocreate um servidor de R usando um modelo de gerenciamento de recursos do Azure, consulte [implantar um cluster de HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-118">toocreate an R Server using an Azure Resource Management template, see [Deploy an R server HDInsight cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).</span></span>
* <span data-ttu-id="e8f2a-119">toocreate um servidor de R usando Olá .NET SDK, consulte [criar clusters baseados em Linux em HDInsight usando Olá .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e8f2a-119">toocreate an R Server using hello .NET SDK, see [create Linux-based clusters in HDInsight using hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>
* <span data-ttu-id="e8f2a-120">toodeploy R Server usando o powershell, consulte o artigo de saudação em [criação de um servidor de R no HDInsight com o PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-120">toodeploy R Server using powershell, see hello article on [creating an R Server on HDInsight with PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).</span></span>


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a><span data-ttu-id="e8f2a-121">Criar cluster hello usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e8f2a-121">Create hello cluster using hello Azure portal</span></span>

1. <span data-ttu-id="e8f2a-122">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e8f2a-123">Selecione **NOVO** -> **Intelligence + Análises**, -> **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-123">Select **NEW** -> **Intelligence + Analytics**, -> **HDInsight**.</span></span>

    ![Imagem da criação de um novo cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. <span data-ttu-id="e8f2a-125">Em Olá **criação rápida** experiência, insira um nome para o cluster de saudação em Olá **nome do Cluster** campo.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-125">In hello **Quick create** experience, enter a name for hello cluster in hello **Cluster Name** field.</span></span> <span data-ttu-id="e8f2a-126">Se você tiver várias assinaturas do Azure, use Olá **assinatura** entrada tooselect Olá um toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-126">If you have multiple Azure subscriptions, use hello **Subscription** entry tooselect hello one you want toouse.</span></span>

    ![Nome do cluster e seleções de assinatura](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. <span data-ttu-id="e8f2a-128">Selecione **tipo de Cluster** tooopen Olá **configuração de Cluster** folha.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-128">Select **Cluster type** tooopen hello **Cluster configuration** blade.</span></span> <span data-ttu-id="e8f2a-129">Em Olá **configuração de Cluster** folha, selecione Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-129">On hello **Cluster Configuration** blade, select hello following options:</span></span>

    * <span data-ttu-id="e8f2a-130">**Tipo de Cluster**: Servidor R</span><span class="sxs-lookup"><span data-stu-id="e8f2a-130">**Cluster Type**: R Server</span></span>
    * <span data-ttu-id="e8f2a-131">**Versão**: versão select Olá tooinstall R Server no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-131">**Version**: select hello version of R Server tooinstall on hello cluster.</span></span> <span data-ttu-id="e8f2a-132">Olá versão disponível no momento é ***R Server 9.1 (HDI 3.6)***.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-132">hello version currently available is ***R Server 9.1 (HDI 3.6)***.</span></span> <span data-ttu-id="e8f2a-133">Notas de versão para versões disponíveis de saudação do servidor do R estão disponíveis [aqui](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-133">Release notes for hello available versions of R Server are available [here](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).</span></span>
    * <span data-ttu-id="e8f2a-134">**Edição de comunidade do estúdio R para R Server**: o IDE baseada em navegador é instalado por padrão no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-134">**R Studio community edition for R Server**: this browser-based IDE is installed by default on hello edge node.</span></span> <span data-ttu-id="e8f2a-135">Se você preferir toonot que ele seja instalado, em seguida, desmarque a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-135">If you would prefer toonot have it installed, then uncheck hello check box.</span></span> <span data-ttu-id="e8f2a-136">Se você escolher toohave-lo instalado, Olá URL para acessar Olá logon de servidor RStudio é encontrado em uma folha de aplicativo de portal para o cluster quando ela é criada.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-136">If you choose toohave it installed, hello URL for accessing hello RStudio Server login is found on a portal application blade for your cluster once it’s been created.</span></span>
    * <span data-ttu-id="e8f2a-137">Deixe Olá outras opções com valores padrão de saudação e usar Olá **selecione** toosave Olá cluster tipo de botão.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-137">Leave hello other options at hello default values and use hello **Select** button toosave hello cluster type.</span></span>

        ![Captura de tela do tipo de folha do cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. <span data-ttu-id="e8f2a-139">Insira um **Nome de usuário de logon do cluster** e uma **Senha de logon do cluster**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-139">Enter a **Cluster login username** and **Cluster login password**.</span></span>

    <span data-ttu-id="e8f2a-140">Especifique um **Nome de Usuário SSH**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-140">Specify an **SSH Username**.</span></span> <span data-ttu-id="e8f2a-141">SSH é usado tooremotely conectar toohello cluster usando um **Secure Shell (SSH)** cliente.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-141">SSH is used tooremotely connect toohello cluster using a **Secure Shell (SSH)** client.</span></span> <span data-ttu-id="e8f2a-142">Você pode especificar usuário SSH Olá nesta caixa de diálogo ou após Olá cluster foi criado (na guia de configuração de saudação para cluster Olá).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-142">You can either specify hello SSH user in this dialog or after hello cluster has been created (in hello Configuration tab for hello cluster).</span></span> <span data-ttu-id="e8f2a-143">R Server está configurado tooexpect um **nome de usuário SSH** de "remoteuser".</span><span class="sxs-lookup"><span data-stu-id="e8f2a-143">R Server is configured tooexpect an **SSH username** of “remoteuser”.</span></span>  <span data-ttu-id="e8f2a-144">**Se você usar um nome de usuário diferente, você deve executar uma etapa adicional após Olá cluster é criado.**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-144">**If you use a different username, you must perform an additional step after hello cluster is created.**</span></span>

    <span data-ttu-id="e8f2a-145">Caixa de saudação deixe marcada para **usar a mesma senha de logon de cluster** toouse **senha** como hello tipo de autenticação, a menos que você preferir que o uso de uma chave pública.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-145">Leave hello box checked for **Use same password as cluster login** toouse **PASSWORD** as hello authentication type unless you prefer use of a public key.</span></span>  <span data-ttu-id="e8f2a-146">Você precisa de um par de chaves pública/privada de tooaccess R Server no cluster Olá por meio de um cliente remoto como, por exemplo, RTVS, RStudio ou outro IDE de área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-146">You need a public/private key pair tooaccess R Server on hello cluster via a remote client as, for example, RTVS, RStudio or another desktop IDE.</span></span> <span data-ttu-id="e8f2a-147">Se você instalar Olá edição do servidor RStudio community, será necessário toochoose uma senha SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-147">If you install hello RStudio Server community edition, you need toochoose an SSH password.</span></span>     

    <span data-ttu-id="e8f2a-148">toocreate e use um par de chaves pública/privada, desmarque **usar a mesma senha de logon de cluster** e, em seguida, selecione **chave pública** e faça o seguinte.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-148">toocreate and use a public/private key pair, uncheck **Use same password as cluster login** and then select **PUBLIC KEY** and proceed as follows.</span></span> <span data-ttu-id="e8f2a-149">Estas instruções pressupõem que você tenha o Cygwin com ssh-keygen ou equivalente instalado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-149">These instructions assume that you have Cygwin with ssh-keygen or an equivalent installed.</span></span>

    * <span data-ttu-id="e8f2a-150">Gere um par de chaves pública/privada do prompt de comando de saudação em seu laptop:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-150">Generate a public/private key pair from hello command prompt on your laptop:</span></span>

        <span data-ttu-id="e8f2a-151">ssh-keygen -t rsa -b 2048</span><span class="sxs-lookup"><span data-stu-id="e8f2a-151">ssh-keygen -t rsa -b 2048</span></span>

    * <span data-ttu-id="e8f2a-152">Siga Olá prompt tooname um arquivo de chave e, em seguida, insira uma frase secreta para aumentar a segurança.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-152">Follow hello prompt tooname a key file and then enter a passphrase for added security.</span></span> <span data-ttu-id="e8f2a-153">Sua tela deve ser semelhante a saudação a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-153">Your screen should look something like hello following image:</span></span>

        ![Linha de comando SSH no Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * <span data-ttu-id="e8f2a-155">Este comando cria um arquivo de chave privada e um arquivo de chave pública em pub de nome < arquivo de chave privada > Olá, por exemplo, furiosa e furiosa.pub.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-155">This command creates a private key file and a public key file under hello name <private-key-filename>.pub, for example furiosa and furiosa.pub.</span></span>

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * <span data-ttu-id="e8f2a-157">Em seguida, especifique o arquivo de chave pública de saudação (&#42;. pub) quando atribuir HDI credenciais de cluster e, por fim, confirme a grupo de recursos e região e selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-157">Then specify hello public key file (&#42;.pub) when assigning HDI cluster credentials and finally confirm your resource group and region and select **Next**.</span></span>

        ![Folha Credenciais](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * <span data-ttu-id="e8f2a-159">Alterar as permissões no arquivo de chave privada em seu laptop hello:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-159">Change permissions on hello private keyfile on your laptop:</span></span>

        <span data-ttu-id="e8f2a-160">chmod 600 <private-key-filename></span><span class="sxs-lookup"><span data-stu-id="e8f2a-160">chmod 600 <private-key-filename></span></span>

   * <span data-ttu-id="e8f2a-161">Use o arquivo de chave privada Olá com SSH para logon remoto:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-161">Use hello private key file with SSH for remote login:</span></span>

        <span data-ttu-id="e8f2a-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span><span class="sxs-lookup"><span data-stu-id="e8f2a-162">ssh –i <private-key-filename> remoteuser@<hostname public ip></span></span>

      <span data-ttu-id="e8f2a-163">Ou, como definição de saudação de parte de seu Hadoop Spark contexto de computação para o servidor do R no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-163">Or, as part hello definition of your Hadoop Spark compute context for R Server on hello client.</span></span> <span data-ttu-id="e8f2a-164">Consulte Olá **usando o Microsoft R Server como um cliente de Hadoop** subseção em [criar um contexto de computação para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-164">See hello **Using Microsoft R Server as a Hadoop Client** subsection in [Create a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).</span></span>

6. <span data-ttu-id="e8f2a-165">criação rápida de saudação faz transição toohello **armazenamento** conta de armazenamento blade tooselect Olá toobe configurações usado para local primário de saudação do hello usado pelo cluster Olá de sistema de arquivos do HDFS.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-165">hello quick create transitions you toohello **Storage** blade tooselect hello storage account settings toobe used for hello primary location of hello HDFS file system used by hello cluster.</span></span> <span data-ttu-id="e8f2a-166">Selecione uma conta nova ou existente do Armazenamento do Azure ou uma conta existente de armazenamento do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-166">Select either a new or existing Azure Storage account or an existing Data Lake Storage account.</span></span>

    - <span data-ttu-id="e8f2a-167">Se você selecionar uma conta de armazenamento do Azure, uma conta de armazenamento existente é selecionada, escolhendo **selecionar uma conta de armazenamento** e, em seguida, selecionando conta relevante hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-167">If you select an Azure Storage account, an existing storage account is selected by choosing **Select a storage account** and then selecting hello relevant account.</span></span> <span data-ttu-id="e8f2a-168">Criar uma nova conta usando Olá **criar novo** link no hello **selecionar uma conta de armazenamento** seção.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-168">Create a new account using hello **Create New** link in hello **Select a storage account** section.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e8f2a-169">Se você selecionar **novo** você deve inserir um nome para a nova conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-169">If you select **New** you must enter a name for hello new storage account.</span></span> <span data-ttu-id="e8f2a-170">Uma marca de seleção verde é exibida se o nome da saudação é aceito.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-170">A green check appears if hello name is accepted.</span></span>

      <span data-ttu-id="e8f2a-171">Olá **contêiner padrão** nome de toohello padrões de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-171">hello **Default Container** defaults toohello name of hello cluster.</span></span> <span data-ttu-id="e8f2a-172">Deixe o padrão como valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-172">Leave this default as hello value.</span></span>

      <span data-ttu-id="e8f2a-173">Se uma nova opção de conta de armazenamento foi selecionada um prompt tooselect **local** é determinada tooselect toocreate qual região Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-173">If a new storage account option was selected a prompt tooselect **Location** is given tooselect which region toocreate hello storage account.</span></span>  

         ![Folha de fonte de dados](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > <span data-ttu-id="e8f2a-175">Também selecionando Olá local para a fonte de dados padrão de saudação define o local de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-175">Selecting hello location for hello default data source  also sets hello location of hello HDInsight cluster.</span></span> <span data-ttu-id="e8f2a-176">Olá fonte de dados padrão e de cluster deve estar no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-176">hello cluster and default data source must be in hello same region.</span></span>

    - <span data-ttu-id="e8f2a-177">Se você quiser toouse um repositório do Data Lake existente, selecione Olá ADLS toouse de conta de armazenamento e adicionar cluster Olá *adicionar* identidade tooyour cluster tooallow acessar toohello o repositório.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-177">If you want toouse an existing Data Lake Store, then select hello ADLS storage account toouse and add hello cluster *ADD* identity tooyour cluster tooallow access toohello store.</span></span> <span data-ttu-id="e8f2a-178">Para obter mais informações sobre este processo, consulte [Criar um cluster do HDInsight com o Data Lake Store usando o Portal do Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-178">For more information on this process, see [Creating HDInsight cluster with Data Lake Store using Azure portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).</span></span>

    <span data-ttu-id="e8f2a-179">Saudação de uso **selecione** configuração de fontes de dados do botão toosave hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-179">Use hello **Select** button toosave hello data source configuration.</span></span>


7. <span data-ttu-id="e8f2a-180">Olá **resumo** folha, em seguida, exibe toovalidate todas as suas configurações.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-180">hello **Summary** blade then displays toovalidate all your settings.</span></span> <span data-ttu-id="e8f2a-181">Aqui você pode alterar sua **tamanho do Cluster** toomodify Olá o número de servidores no cluster e também especificar qualquer **ações de Script** toorun desejado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-181">Here you can change your **Cluster size** toomodify hello number of servers in your cluster and also specify any **Script actions** you want toorun.</span></span> <span data-ttu-id="e8f2a-182">A menos que você sabe que precisa de um cluster maior, deixe o número de saudação de nós de trabalho com o padrão de saudação do `4`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-182">Unless you know that you need a larger cluster, leave hello number of worker nodes at hello default of `4`.</span></span> <span data-ttu-id="e8f2a-183">Olá estimativa de custo de cluster Olá é mostrado na folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-183">hello estimated cost of hello cluster is shown within hello blade.</span></span>

    ![resumo do cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > <span data-ttu-id="e8f2a-185">Se necessário, você pode redimensionar o cluster mais tarde por meio de saudação Portal (**Cluster** -> **configurações** -> **Cluster de escala**) tooincrease ou Diminua o número de saudação de nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-185">If needed, you can resize your cluster later through hello Portal (**Cluster** -> **Settings** -> **Scale Cluster**) tooincrease or decrease hello number of worker nodes.</span></span>  <span data-ttu-id="e8f2a-186">Este redimensionamento pode ser útil para quando ocioso cluster hello quando não estiver em uso, ou para adicionar as necessidades de saudação do toomeet de capacidade de tarefas maior.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-186">This resizing can be useful for idling down hello cluster when not in use, or for adding capacity toomeet hello needs of larger tasks.</span></span>
   >
   >

   <span data-ttu-id="e8f2a-187">Tookeep alguns fatores em mente ao dimensionar seu cluster, nós de dados hello e nó de borda Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-187">Some factors tookeep in mind when sizing your cluster, hello data nodes, and hello edge node include:</span></span>  

   * <span data-ttu-id="e8f2a-188">desempenho Olá de análises de R Server distribuídos no Spark é proporcional toohello número de nós de trabalho quando dados saudação forem grandes.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-188">hello performance of distributed R Server analyses on Spark is proportional toohello number of worker nodes when hello data is large.</span></span>  

   * <span data-ttu-id="e8f2a-189">desempenho de saudação de análises de R Server é linear no tamanho de saudação dos dados que está sendo analisados.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-189">hello performance of R Server analyses is linear in hello size of data being analyzed.</span></span> <span data-ttu-id="e8f2a-190">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-190">For example:</span></span>  

     * <span data-ttu-id="e8f2a-191">Para dados toomodest pequenos, o desempenho é melhor quando analisada em um contexto de computação local no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-191">For small toomodest data, performance is best when analyzed in a local compute context on hello edge node.</span></span>  <span data-ttu-id="e8f2a-192">Para obter mais informações sobre cenários de saudação sob a qual hello local e o Spark contextos de computação funcionam melhor, consulte Opções de contexto de computação para o servidor do R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-192">For more information on hello scenarios under which hello local and Spark compute contexts work best, see  Compute context options for R Server on HDInsight.</span></span><br>
     * <span data-ttu-id="e8f2a-193">Se você fazer logon no nó de borda toohello e executa o script R, mas Olá funções de rx ScaleR são executadas <strong>localmente</strong> no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-193">If you log in toohello edge node and run your R script, then all but hello ScaleR rx-functions are executed <strong>locally</strong> on hello edge node.</span></span> <span data-ttu-id="e8f2a-194">Olá para memória e número de núcleos de nó de borda Olá sejam dimensionado adequadamente.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-194">So hello memory and number of cores of hello edge node should be sized accordingly.</span></span> <span data-ttu-id="e8f2a-195">Olá que mesmo se aplica se você usar R Server em HDI como um contexto de computação remota de seu laptop.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-195">hello same applies if you use R Server on HDI as a remote compute context from your laptop.</span></span>

     ![Folha de camadas de preços de nó](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     <span data-ttu-id="e8f2a-197">Saudação de uso **selecione** nó de saudação do botão toosave preços de configuração.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-197">Use hello **Select** button toosave hello node pricing configuration.</span></span>

   <span data-ttu-id="e8f2a-198">Também há um link para **Baixar modelo e parâmetros**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-198">There is also a link for **Download template and parameters**.</span></span> <span data-ttu-id="e8f2a-199">Clique em scripts de toodisplay esse link podem ser usado tooautomate Olá criação de um cluster com a configuração selecionada hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-199">Click on this link toodisplay scripts that can be used tooautomate hello creation of a cluster with hello selected configuration.</span></span> <span data-ttu-id="e8f2a-200">Esses scripts também estão disponíveis no hello entrada portal do Azure para seu cluster quando ele tiver sido criado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-200">These scripts are also available from hello Azure portal entry for your cluster once it has been created.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e8f2a-201">Levará algum tempo para Olá cluster toobe criado, normalmente em torno de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-201">It takes some time for hello cluster toobe created, usually around 20 minutes.</span></span> <span data-ttu-id="e8f2a-202">Use o bloco Olá Olá quadro inicial ou Olá **notificações** entrada hello à esquerda do hello página toocheck no processo de criação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-202">Use hello tile on hello Startboard, or hello **Notifications** entry on hello left of hello page toocheck on hello creation process.</span></span>
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a><span data-ttu-id="e8f2a-203">Conecte-se tooRStudio Server</span><span class="sxs-lookup"><span data-stu-id="e8f2a-203">Connect tooRStudio Server</span></span>

<span data-ttu-id="e8f2a-204">Se você tiver escolhido tooinclude edição do servidor RStudio community em sua instalação, você pode acessar o logon de RStudio Olá por meio de dois métodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-204">If you’ve chosen tooinclude RStudio Server community edition in your installation, then you can access hello RStudio login via two different methods.</span></span>

1. <span data-ttu-id="e8f2a-205">Vá toohello URL a seguir (onde **CLUSTERNAME** é Olá nome do cluster de saudação que você criou):</span><span class="sxs-lookup"><span data-stu-id="e8f2a-205">Go toohello following URL (where **CLUSTERNAME** is hello name of hello cluster you've created):</span></span>

    <span data-ttu-id="e8f2a-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span><span class="sxs-lookup"><span data-stu-id="e8f2a-206">https://**CLUSTERNAME**.azurehdinsight.net/rstudio/</span></span>

2. <span data-ttu-id="e8f2a-207">Abrir a entrada de Olá para seu cluster em Olá portal do Azure, selecione Olá **R Server painéis** link rápido e, em seguida, selecionando Olá **R Studio painel**:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-207">Open hello entry for your cluster in hello Azure portal, select hello **R Server Dashboards** quick link and then selecting hello **R Studio Dashboard**:</span></span>

     ![Painel de controle do acesso Olá R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Painel de controle do acesso Olá R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > <span data-ttu-id="e8f2a-210">Independentemente do método hello usado, hello primeira vez que você efetuar logon é necessário tooauthenticate duas vezes.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-210">Regardless of hello method used, hello first time you log in you need tooauthenticate twice.</span></span>  <span data-ttu-id="e8f2a-211">Na primeira autenticação de hello, fornecem Olá *ID de usuário do administrador de cluster* e *senha*.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-211">At hello first authentication, provide hello *cluster Admin userid* and *password*.</span></span> <span data-ttu-id="e8f2a-212">No prompt de segundo hello, fornecer Olá *SSH userid* e *senha*.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-212">At hello second prompt, provide hello *SSH userid* and *password*.</span></span> <span data-ttu-id="e8f2a-213">Log subsequentes ins exigem apenas Olá *senha SSH* e *userid*.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-213">Subsequent log ins only require hello *SSH password* and *userid*.</span></span>

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a><span data-ttu-id="e8f2a-214">Conecte-se o nó de borda de R Server toohello</span><span class="sxs-lookup"><span data-stu-id="e8f2a-214">Connect toohello R Server edge node</span></span>

<span data-ttu-id="e8f2a-215">Conecte-se tooR nó de borda do servidor do cluster do HDInsight hello usando o SSH com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-215">Connect tooR Server edge node of hello HDInsight cluster using SSH with hello command:</span></span>

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> <span data-ttu-id="e8f2a-216">Você pode encontrar hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` endereço no hello portal do Azure, selecionando o cluster, em seguida, **todas as configurações** -> **aplicativos** -> **RServer**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-216">You can find hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` address in hello Azure portal by selecting your cluster then **All Settings** -> **Apps** -> **RServer**.</span></span> <span data-ttu-id="e8f2a-217">Isso exibe Olá informações de ponto de extremidade SSH para nó de borda de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-217">This displays hello SSH Endpoint information for hello edge node.</span></span>
>
> ![Imagem de saudação de ponto de extremidade SSH para o nó de borda Olá](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

<span data-ttu-id="e8f2a-219">Se você usou uma senha toosecure sua conta de usuário SSH, é solicitada tooentê-lo.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-219">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="e8f2a-220">Se você usou uma chave pública, você pode ter toouse Olá `-i` toospecify parâmetro hello chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-220">If you used a public key, you may have toouse hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="e8f2a-221">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-221">For example:</span></span>

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="e8f2a-222">Para obter mais informações, consulte [conectar tooHDInsight (Hadoop) usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-222">For more information, see [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="e8f2a-223">Uma vez conectado, você chega em uma prompt toohello a seguir semelhante:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-223">Once connected, you arrive at a prompt similar toohello following:</span></span>

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a><span data-ttu-id="e8f2a-224">Habilitar múltiplos usuário simultâneos</span><span class="sxs-lookup"><span data-stu-id="e8f2a-224">Enable multiple concurrent users</span></span>

<span data-ttu-id="e8f2a-225">Você pode habilitar vários usuários simultâneos adicionando mais usuários para o nó de borda Olá no qual Olá comunidade RStudio versão é executado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-225">You can enable multiple concurrent users by adding more users for hello edge node on which hello RStudio community version runs.</span></span>

<span data-ttu-id="e8f2a-226">Quando você cria um cluster HDInsight, deve fornecer dois usuários, um usuário HTTP e um usuário SSH:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-226">When you create an HDInsight cluster, you must provide two users, an HTTP user and an SSH user:</span></span>

![Usuários simultâneos 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- <span data-ttu-id="e8f2a-228">**Nome de usuário de logon de cluster**: um usuário HTTP para autenticação por meio do gateway de HDInsight Olá que é usado tooprotect hello HDInsight clusters que você criou.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-228">**Cluster login username**: an HTTP user for authentication through hello HDInsight gateway that is used tooprotect hello HDInsight clusters you created.</span></span> <span data-ttu-id="e8f2a-229">Este usuário HTTP é usado tooaccess Olá Ambari UI, YARN da interface do usuário, bem como outros componentes de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-229">This HTTP user is used tooaccess hello Ambari UI, YARN UI, as well as other UI components.</span></span>
- <span data-ttu-id="e8f2a-230">**Nome de usuário de Shell (SSH) segura**: um cluster de saudação do SSH usuário tooaccess por meio do secure shell.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-230">**Secure Shell (SSH) username**: an SSH user tooaccess hello cluster through secure shell.</span></span> <span data-ttu-id="e8f2a-231">Este usuário é um usuário em Olá sistema Linux para todos os nós de cabeçalho hello, nós de trabalho e nós de borda.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-231">This user is a user in hello Linux system for all hello head nodes, worker nodes, and edge nodes.</span></span> <span data-ttu-id="e8f2a-232">Então você pode usar do secure shell tooaccess qualquer um de nós de saudação em um cluster remoto.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-232">So you can use secure shell tooaccess any of hello nodes in a remote cluster.</span></span>

<span data-ttu-id="e8f2a-233">Olá R Studio Server Community na versão usada Olá Microsoft R Server no cluster do HDInsight tipo aceita apenas o nome de usuário do Linux e a senha como um mecanismo de logon.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-233">hello R Studio Server Community version used in hello Microsoft R Server on HDInsight type cluster accepts only Linux username and password as a login mechanism.</span></span> <span data-ttu-id="e8f2a-234">Ele não dá suporte a tokens de passagem.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-234">It does not support passing tokens.</span></span> <span data-ttu-id="e8f2a-235">Portanto, se você tiver criado um novo cluster e deseja toouse Studio R tooaccess-lo, você precisa toolog em duas vezes.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-235">So if you have created a new cluster and want toouse R Studio tooaccess it, you need toolog in twice.</span></span>

- <span data-ttu-id="e8f2a-236">Primeiro, faça logon usando credenciais de usuário de saudação HTTP por meio de saudação HDInsight Gateway:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-236">First log in using hello HTTP user credentials through hello HDInsight Gateway:</span></span> 

    ![Usuário simultâneo 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- <span data-ttu-id="e8f2a-238">Em seguida, use Olá toolog de credenciais de usuário SSH no tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-238">Then use hello SSH user credentials toolog in tooRStudio:</span></span>
  
    ![Usuário simultâneo 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

<span data-ttu-id="e8f2a-240">Atualmente, apenas uma conta de usuário SSH pode ser criada durante o provisionamento de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-240">Currently, only one SSH user account can be created when provisioning an HDInsight cluster.</span></span> <span data-ttu-id="e8f2a-241">Para clusters de vários usuários tooaccess Microsoft R Server no HDInsight tooenable, precisamos toocreate mais usuários em Olá sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-241">So tooenable multiple users tooaccess Microsoft R Server on HDInsight clusters, we need toocreate additional users in hello Linux system.</span></span>

<span data-ttu-id="e8f2a-242">Como RStudio Server Community está em execução no nó de borda do cluster hello, há várias etapas aqui:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-242">Because RStudio Server Community is running on hello cluster’s edge node, there are several steps here:</span></span>

1. <span data-ttu-id="e8f2a-243">Usar toolog de usuário SSH Olá criada no nó de borda toohello</span><span class="sxs-lookup"><span data-stu-id="e8f2a-243">Use hello created SSH user toolog in toohello edge node</span></span>
2. <span data-ttu-id="e8f2a-244">Adicionar mais usuários do Linux ao nó de borda</span><span class="sxs-lookup"><span data-stu-id="e8f2a-244">Add more Linux users in edge node</span></span>
3. <span data-ttu-id="e8f2a-245">Use a versão de comunidade RStudio com usuário Olá criado</span><span class="sxs-lookup"><span data-stu-id="e8f2a-245">Use RStudio Community version with hello user created</span></span>

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a><span data-ttu-id="e8f2a-246">Etapa 1: Usar toolog de usuário SSH Olá criada no nó de borda toohello</span><span class="sxs-lookup"><span data-stu-id="e8f2a-246">Step 1: Use hello created SSH user toolog in toohello edge node</span></span>

<span data-ttu-id="e8f2a-247">Baixar qualquer ferramenta SSH (como o Putty) e usar o hello existente SSH usuário toolog no.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-247">Download any SSH tool (such as Putty) and use hello existing SSH user toolog in.</span></span> <span data-ttu-id="e8f2a-248">Siga instruções Olá fornecidas no [conectar tooHDInsight (Hadoop) usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Olá nó de borda.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-248">Then follow hello instructions provided in [Connect tooHDInsight (Hadoop) using SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello edge node.</span></span> <span data-ttu-id="e8f2a-249">endereço de nó de borda Olá para R Server no cluster HDInsight é: *clustername-ed-ssh.azurehdinsight.net*</span><span class="sxs-lookup"><span data-stu-id="e8f2a-249">hello edge node address for R Server on HDInsight cluster is: *clustername-ed-ssh.azurehdinsight.net*</span></span>


### <a name="step-2-add-more-linux-users-in-edge-node"></a><span data-ttu-id="e8f2a-250">Etapa 2: adicionar mais usuários do Linux ao nó de borda</span><span class="sxs-lookup"><span data-stu-id="e8f2a-250">Step 2: Add more Linux users in edge node</span></span>

<span data-ttu-id="e8f2a-251">tooadd um nó de borda de toohello de usuário, execute os comandos de saudação:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-251">tooadd a user toohello edge node, execute hello commands:</span></span>

    sudo useradd yournewusername -m
    sudo passwd yourusername

<span data-ttu-id="e8f2a-252">Você deve ver Olá itens retornados a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-252">You should see hello following items returned:</span></span> 

![Usuários simultâneos 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

<span data-ttu-id="e8f2a-254">Quando solicitado para "senha Kerberos atual:", basta pressionar **Enter** tooignore-lo.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-254">When prompted for “Current Kerberos password:”, just press **Enter** tooignore it.</span></span> <span data-ttu-id="e8f2a-255">Olá `-m` opção `useradd` comando indica que o sistema Olá criará uma pasta base para usuário hello, que é necessário para a versão da comunidade de RStudio.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-255">hello `-m` option in `useradd` command indicates that hello system will create a home folder for hello user, which is required for RStudio Community version.</span></span>


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a><span data-ttu-id="e8f2a-256">Etapa 3: Versão de uso RStudio comunidade com usuário Olá criado</span><span class="sxs-lookup"><span data-stu-id="e8f2a-256">Step 3: Use RStudio Community version with hello user created</span></span>

<span data-ttu-id="e8f2a-257">Use Olá criado pelo usuário toolog tooRStudio:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-257">Use hello user created toolog in tooRStudio:</span></span>

![Usuários simultâneos 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

<span data-ttu-id="e8f2a-259">Observe que RStudio indica que você está usando o novo usuário de saudação (aqui, por exemplo, *sshuser6*) toolog em cluster hello:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-259">Notice that RStudio indicates that you are using hello new user (here, for example, *sshuser6*) toolog in hello cluster:</span></span> 

![Usuários simultâneos 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

<span data-ttu-id="e8f2a-261">Você também pode fazer logon usando credenciais de saudação original (por padrão, ele é *sshuser*) simultaneamente a partir de outra janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-261">You can also log in using hello original credentials (by default, it is *sshuser*) concurrently from another browser window.</span></span>

<span data-ttu-id="e8f2a-262">Você pode enviar um trabalho usando funções scaleR.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-262">You can submit a job using scaleR functions.</span></span> <span data-ttu-id="e8f2a-263">Aqui está um exemplo de hello comandos usados toorun um trabalho:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-263">Here is an example of hello commands used toorun a job:</span></span>

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


<span data-ttu-id="e8f2a-264">Observe que os trabalhos de saudação enviados são em nomes de usuário diferente na interface do usuário do YARN:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-264">Notice that hello jobs submitted are under different user names in YARN UI:</span></span>

![Usuários simultâneos 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

<span data-ttu-id="e8f2a-266">Observe também que Olá recém-adicionado usuários não têm privilégios de raiz no sistema Linux, mas eles têm Olá mesmo acessar arquivos de saudação do tooall no armazenamento remoto Olá HDFS e WASB.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-266">Note also that hello newly added users do not have root privileges in Linux system, but they do have hello same access tooall hello files in hello remote HDFS and WASB storage.</span></span>


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a><span data-ttu-id="e8f2a-267">Use o console Olá R</span><span class="sxs-lookup"><span data-stu-id="e8f2a-267">Use hello R console</span></span>

1. <span data-ttu-id="e8f2a-268">Da sessão SSH hello, use Olá console do comando toostart Olá R a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-268">From hello SSH session, use hello following command toostart hello R console:</span></span>  

        R

2. <span data-ttu-id="e8f2a-269">Você deve ver o seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-269">You should see output similar toohello following:</span></span>
    
    <span data-ttu-id="e8f2a-270">R versão 3.2.2 (2015-08-14) – "Segurança de incêndio" Copyright (C) 2015 hello R Foundation para a plataforma de computação de estatísticas: x86_64 pc linux-gnu (64 bits)</span><span class="sxs-lookup"><span data-stu-id="e8f2a-270">R version 3.2.2 (2015-08-14) -- "Fire Safety"  Copyright (C) 2015 hello R Foundation for Statistical Computing  Platform: x86_64-pc-linux-gnu (64-bit)</span></span>

    <span data-ttu-id="e8f2a-271">R é um software livre e vem com ABSOLUTAMENTE NENHUMA GARANTIA.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-271">R is free software and comes with ABSOLUTELY NO WARRANTY.</span></span>
    <span data-ttu-id="e8f2a-272">São boas-vinda tooredistribute sob determinadas condições.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-272">You are welcome tooredistribute it under certain conditions.</span></span>
    <span data-ttu-id="e8f2a-273">Digite 'license()' ou 'licence()' para obter detalhes de distribuição.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-273">Type 'license()' or 'licence()' for distribution details.</span></span>

    <span data-ttu-id="e8f2a-274">Suporte de linguagem natural, mas em execução em uma localidade com idioma inglês</span><span class="sxs-lookup"><span data-stu-id="e8f2a-274">Natural language support but running in an English locale</span></span>

    <span data-ttu-id="e8f2a-275">R é um projeto de colaboração com muitos colaboradores.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-275">R is a collaborative project with many contributors.</span></span>
    <span data-ttu-id="e8f2a-276">Digite 'contributors()' para obter mais informações e 'citation()' em como toocite R ou R pacotes em publicações.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-276">Type 'contributors()' for more information and 'citation()' on how toocite R or R packages in publications.</span></span>

    <span data-ttu-id="e8f2a-277">Digite 'demo()' para algumas demonstrações, help() para obter ajuda online ou help.start() para um toohelp de interface do navegador HTML.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-277">Type 'demo()' for some demos, 'help()' for on-line help, or 'help.start()' for an HTML browser interface toohelp.</span></span>
    <span data-ttu-id="e8f2a-278">Digite 'chamar' tooquit R.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-278">Type 'q()' tooquit R.</span></span>

    <span data-ttu-id="e8f2a-279">Microsoft R Server versão 8.0: uma distribuição avançada de pacotes Microsoft R Copyright (C) 2016 Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="e8f2a-279">Microsoft R Server version 8.0: an enhanced distribution of R  Microsoft packages Copyright (C) 2016 Microsoft Corporation</span></span>

    <span data-ttu-id="e8f2a-280">Digite readme() para notas de versão.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-280">Type 'readme()' for release notes.</span></span>
    >

3. <span data-ttu-id="e8f2a-281">De saudação `>` prompt, você pode inserir o código R.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-281">From hello `>` prompt, you can enter R code.</span></span> <span data-ttu-id="e8f2a-282">Servidor de R inclui pacotes que permitem que você tooeasily interagir com Hadoop e executar cálculos distribuídos.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-282">R server includes packages that allow you tooeasily interact with Hadoop and run distributed computations.</span></span> <span data-ttu-id="e8f2a-283">Por exemplo, use Olá raiz de saudação do comando tooview saudação padrão do sistema de arquivos para o cluster do HDInsight Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-283">For example, use hello following command tooview hello root of hello default file system for hello HDInsight cluster:</span></span>

    <span data-ttu-id="e8f2a-284">rxHadoopListFiles("/")</span><span class="sxs-lookup"><span data-stu-id="e8f2a-284">rxHadoopListFiles("/")</span></span>

4. <span data-ttu-id="e8f2a-285">Você também pode usar o hello WASB estilo endereçamento.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-285">You can also use hello WASB style addressing.</span></span>

    <span data-ttu-id="e8f2a-286">rxHadoopListFiles("wasb:///")</span><span class="sxs-lookup"><span data-stu-id="e8f2a-286">rxHadoopListFiles("wasb:///")</span></span>


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a><span data-ttu-id="e8f2a-287">Usando o Servidor R no HDI de uma instância remota do Microsoft R Server ou Microsoft R Client</span><span class="sxs-lookup"><span data-stu-id="e8f2a-287">Using R Server on HDI from a remote instance of Microsoft R Server or Microsoft R Client</span></span>

<span data-ttu-id="e8f2a-288">É possível tooset o contexto de computação do acesso toohello HDI Hadoop Spark de uma instância remota do Microsoft R Server ou o cliente do Microsoft R em execução em um desktop ou laptop.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-288">It is possible tooset up access toohello HDI Hadoop Spark compute context from a remote instance of Microsoft R Server or Microsoft R Client running on a desktop or laptop.</span></span> <span data-ttu-id="e8f2a-289">Consulte **usando o Microsoft R Server como um cliente de Hadoop** subseção Olá [criando um contexto de computação para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-289">See **Using Microsoft R Server as a Hadoop Client** subsection in hello [Creating a Compute Context for Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md).</span></span> <span data-ttu-id="e8f2a-290">toodo assim, você precisa toospecify Olá as opções a seguir ao definir o contexto de computação RxSpark Olá em seu laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-290">toodo so, you need toospecify hello following options when defining hello RxSpark compute context on your laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches, and sshProfileScript.</span></span> <span data-ttu-id="e8f2a-291">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-291">For example:</span></span>


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a><span data-ttu-id="e8f2a-292">Use um contexto de computação</span><span class="sxs-lookup"><span data-stu-id="e8f2a-292">Use a compute context</span></span>

<span data-ttu-id="e8f2a-293">Um contexto de computação permite toocontrol se a computação é executada localmente no nó de borda de saudação ou distribuída entre nós Olá no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-293">A compute context allows you toocontrol whether computation is performed locally on hello edge node or distributed across hello nodes in hello HDInsight cluster.</span></span>

1. <span data-ttu-id="e8f2a-294">Servidor RStudio ou console Olá R (em uma sessão SSH), use Olá dados de exemplo de tooload de código a seguir no armazenamento padrão da saudação para HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-294">From RStudio Server or hello R console (in an SSH session), use hello following code tooload example data into hello default storage for HDInsight:</span></span>

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. <span data-ttu-id="e8f2a-295">Em seguida, vamos criar algumas informações de dados e definir duas fontes de dados para que possamos trabalhar com dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-295">Next, let's create some data info and define two data sources so that we can work with hello data.</span></span>

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. <span data-ttu-id="e8f2a-296">Vamos executar uma regressão logística em dados de saudação usando o contexto de computação local hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-296">Let's run a logistic regression over hello data using hello local compute context.</span></span>

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    <span data-ttu-id="e8f2a-297">Você deve ver a saída que termina com linhas toohello semelhante a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-297">You should see output that ends with lines similar toohello following:</span></span>

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. <span data-ttu-id="e8f2a-298">Em seguida, vamos executar Olá mesmo Regressão logística usando Olá Spark contexto.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-298">Next, let's run hello same logistic regression using hello Spark context.</span></span> <span data-ttu-id="e8f2a-299">contexto do Spark Olá distribui Olá processamento em todos os nós de trabalho Olá no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-299">hello Spark context distributes hello processing over all hello worker nodes in hello HDInsight cluster.</span></span>

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > <span data-ttu-id="e8f2a-300">Você também pode usar o cálculo de toodistribute MapReduce em nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-300">You can also use MapReduce toodistribute computation across cluster nodes.</span></span> <span data-ttu-id="e8f2a-301">Para saber mais sobre o contexto de computação, confira [Opções de contexto de computação para o Servidor R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-301">For more information on compute context, see [Compute context options for R Server on HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).</span></span>


## <a name="distribute-r-code-toomultiple-nodes"></a><span data-ttu-id="e8f2a-302">Distribuir nós de toomultiple código R</span><span class="sxs-lookup"><span data-stu-id="e8f2a-302">Distribute R code toomultiple nodes</span></span>

<span data-ttu-id="e8f2a-303">Com o servidor de R, você pode facilmente executar código R existente e executá-lo em vários nós no cluster hello usando `rxExec`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-303">With R Server, you can easily take existing R code and run it across multiple nodes in hello cluster by using `rxExec`.</span></span> <span data-ttu-id="e8f2a-304">Essa função é útil ao fazer uma limpeza de parâmetro ou simulações.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-304">This function is useful when doing a parameter sweep or simulations.</span></span> <span data-ttu-id="e8f2a-305">Olá, código a seguir é um exemplo de como toouse `rxExec`:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-305">hello following code is an example of how toouse `rxExec`:</span></span>

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

<span data-ttu-id="e8f2a-306">Se você ainda estiver usando Olá Spark ou contexto de MapReduce, esse comando retorna valor de nodename Olá para nós de trabalho Olá código Olá `(Sys.info()["nodename"])` é executado no.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-306">If you are still using hello Spark or MapReduce context, this  command returns hello nodename value for hello worker nodes that hello code `(Sys.info()["nodename"])` is run on.</span></span> <span data-ttu-id="e8f2a-307">Por exemplo, em um cluster de quatro nós, você espera que tooreceive de saída a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-307">For example, on a four node cluster, you expect tooreceive output similar toohello following:</span></span>

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a><span data-ttu-id="e8f2a-308">Acessando dados no Hive e no Parquet</span><span class="sxs-lookup"><span data-stu-id="e8f2a-308">Accessing Data in Hive and Parquet</span></span>

<span data-ttu-id="e8f2a-309">Um recurso disponível em R Server 9.1 permite toodata acesso direto no Hive e Parquet para uso por funções ScaleR no contexto de computação Olá Spark.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-309">A feature available in R Server 9.1 allows direct access toodata in Hive and Parquet for use by ScaleR functions in hello Spark compute context.</span></span> <span data-ttu-id="e8f2a-310">Esses recursos estão disponíveis por meio de novos dados fonte funções ScaleR chamadas RxHiveData e RxParquetData que funcionam com o uso de dados do Spark SQL tooload diretamente em um DataFrame Spark para análise pelo ScaleR.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-310">These capabilities are available through new ScaleR data source functions called RxHiveData and RxParquetData that work through use of Spark SQL tooload data directly into a Spark DataFrame for analysis by ScaleR.</span></span>  

<span data-ttu-id="e8f2a-311">saudação de código a seguir fornece um exemplo de código sobre o uso de novas funções de saudação:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-311">hello following code provides some sample code on use of hello new functions:</span></span>

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


<span data-ttu-id="e8f2a-312">Para obter informações adicionais sobre o uso dessas novas funções consulte a Ajuda online Olá no R Server através do uso de saudação `?RxHivedata` e `?RxParquetData` comandos.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-312">For additional info on use of these new functions see hello online help in R Server through use of hello `?RxHivedata` and `?RxParquetData` commands.</span></span>  


## <a name="install-additional-r-packages-on-hello-edge-node"></a><span data-ttu-id="e8f2a-313">Instalar pacotes R adicionais no nó de borda Olá</span><span class="sxs-lookup"><span data-stu-id="e8f2a-313">Install additional R packages on hello edge node</span></span>

<span data-ttu-id="e8f2a-314">Se você quiser tooinstall pacotes de R adicionais no nó de borda hello, você pode usar `install.packages()` diretamente de dentro Olá console R quando conectado toohello borda nó por meio do SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-314">If you would like tooinstall additional R packages on hello edge node, you can use `install.packages()` directly from within hello R console when connected toohello edge node through SSH.</span></span> <span data-ttu-id="e8f2a-315">No entanto, se você precisar tooinstall pacotes de R em nós de trabalho de saudação do cluster de saudação, você deve usar uma ação de Script.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-315">However, if you need tooinstall R packages on hello worker nodes of hello cluster, you must use a Script Action.</span></span>

<span data-ttu-id="e8f2a-316">Ações de script são scripts de Bash que são usadas toomake configuração alterações toohello HDInsight cluster ou tooinstall software adicional, como pacotes R adicionais.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-316">Script Actions are Bash scripts that are used toomake configuration changes toohello HDInsight cluster or tooinstall additional software, such as additional R packages.</span></span> <span data-ttu-id="e8f2a-317">tooinstall pacotes adicionais usando uma ação de Script, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-317">tooinstall additional packages using a Script Action, use hello following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8f2a-318">Usar pacotes de R adicionais tooinstall ações de Script só pode ser usado depois Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-318">Using Script Actions tooinstall additional R packages can only be used after hello cluster has been created.</span></span> <span data-ttu-id="e8f2a-319">Não use esse procedimento durante a criação do cluster, como o script hello se baseia em R Server sendo completamente instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-319">Do not use this procedure during cluster creation, as hello script relies on R Server being completely installed and configured.</span></span>
>
>

1. <span data-ttu-id="e8f2a-320">De saudação [portal do Azure](https://portal.azure.com), selecione o servidor do R no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-320">From hello [Azure portal](https://portal.azure.com), select your R Server on HDInsight cluster.</span></span>

2. <span data-ttu-id="e8f2a-321">De saudação **configurações** folha, selecione **ações de Script** e **Enviar nova** toosubmit uma nova ação de Script.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-321">From hello **Settings** blade, select **Script Actions** and then **Submit New** toosubmit a new Script Action.</span></span>

   ![Imagem da folha de ações do script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. <span data-ttu-id="e8f2a-323">De saudação **enviar ação de script** folha, fornecer Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-323">From hello **Submit script action** blade, provide hello following information:</span></span>

   * <span data-ttu-id="e8f2a-324">**Nome**: amigável para um nome tooidentify este script</span><span class="sxs-lookup"><span data-stu-id="e8f2a-324">**Name**: A friendly name tooidentify this script</span></span>

   * <span data-ttu-id="e8f2a-325">**URI do script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span><span class="sxs-lookup"><span data-stu-id="e8f2a-325">**Bash script URI**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`</span></span>

   * <span data-ttu-id="e8f2a-326">**Cabeçalho**: esse item deve estar **desmarcado**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-326">**Head**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="e8f2a-327">**Trabalho**: esse item deve estar **marcado**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-327">**Worker**: This item should be **checked**</span></span>

   * <span data-ttu-id="e8f2a-328">**Nós de borda**: esse item deve estar **desmarcado**.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-328">**Edge nodes**: This item should be **unchecked**.</span></span>

   * <span data-ttu-id="e8f2a-329">**Zookeeper**: esse item deve estar **desmarcado**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-329">**Zookeeper**: This item should be **unchecked**</span></span>

   * <span data-ttu-id="e8f2a-330">**Parâmetros**: Olá R pacotes toobe instalado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-330">**Parameters**: hello R packages toobe installed.</span></span> <span data-ttu-id="e8f2a-331">Por exemplo, `bitops stringr arules`</span><span class="sxs-lookup"><span data-stu-id="e8f2a-331">For example, `bitops stringr arules`</span></span>

   * <span data-ttu-id="e8f2a-332">**Persistir esse script...**: esse item estar **marcado**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-332">**Persist this script...**: This item should be **Checked**</span></span>  

   > [!NOTE]
   > 1. <span data-ttu-id="e8f2a-333">Por padrão, todos os pacotes de R são instalados de um instantâneo do repositório de MRAN Microsoft hello consistente com a versão de saudação do servidor de R que foi instalado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-333">By default, all R packages are installed from a snapshot of hello Microsoft MRAN repository consistent with hello version of R Server that has been installed.</span></span> <span data-ttu-id="e8f2a-334">Se você quiser tooinstall de versões mais recentes dos pacotes, há alguns riscos de incompatibilidade.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-334">If you want tooinstall newer versions of packages, then there is some risk of incompatibility.</span></span> <span data-ttu-id="e8f2a-335">No entanto esse tipo de instalação é possível especificando `useCRAN` como Olá primeiro elemento do pacote de saudação de lista, por exemplo `useCRAN bitops, stringr, arules`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-335">However this kind of install is possible by specifying `useCRAN` as hello first element of hello package list, for example `useCRAN bitops, stringr, arules`.</span></span>  
   > 2. <span data-ttu-id="e8f2a-336">Alguns pacotes R exigem outras bibliotecas do sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-336">Some R packages require additional Linux system libraries.</span></span> <span data-ttu-id="e8f2a-337">Para sua conveniência, podemos ter pré-instalado dependências Olá necessárias por Olá top 100 pacotes R mais populares.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-337">For convenience, we have pre-installed hello dependencies needed by hello top 100 most popular R packages.</span></span> <span data-ttu-id="e8f2a-338">No entanto, se precisam de pacotes de R Olá que instalar bibliotecas além esses, em seguida, você deve baixar Olá script base usado aqui e adicionar etapas tooinstall Olá sistema bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-338">However, if hello R package(s) you install require libraries beyond these then you must download hello base script used here and add steps tooinstall hello system libraries.</span></span> <span data-ttu-id="e8f2a-339">Você deve carregar Olá modificado script tooa público blob contêiner no armazenamento do Azure e usar pacotes de saudação do hello modificado script tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-339">You must then upload hello modified script tooa public blob container in Azure storage and use hello modified script tooinstall hello packages.</span></span>
   >    <span data-ttu-id="e8f2a-340">Para saber mais sobre como desenvolver as Ações de Script, confira [Desenvolvimento de ação de script](hdinsight-hadoop-script-actions-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-340">For more information on developing Script Actions, see [Script Action development](hdinsight-hadoop-script-actions-linux.md).</span></span>  
   >
   >

   ![Adicionando uma ação do script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. <span data-ttu-id="e8f2a-342">Selecione **criar** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-342">Select **Create** toorun hello script.</span></span> <span data-ttu-id="e8f2a-343">Após a conclusão do script hello, pacotes de saudação R estão disponíveis em todos os nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-343">Once hello script completes, hello R packages are available on all worker nodes.</span></span>


## <a name="using-microsoft-r-server-operationalization"></a><span data-ttu-id="e8f2a-344">Usando a operacionalização do Microsoft R Server</span><span class="sxs-lookup"><span data-stu-id="e8f2a-344">Using Microsoft R Server Operationalization</span></span>

<span data-ttu-id="e8f2a-345">Quando a modelagem de dados for concluída, você pode colocar previsões de toomake modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-345">When your data modeling is complete, you can operationalize hello model toomake predictions.</span></span> <span data-ttu-id="e8f2a-346">tooconfigure para operacionalização do Microsoft R Server, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-346">tooconfigure for Microsoft R Server operationalization, perform hello following steps:</span></span>

<span data-ttu-id="e8f2a-347">Primeiro, ssh no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-347">First, ssh into hello Edge node.</span></span> <span data-ttu-id="e8f2a-348">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="e8f2a-348">For example,</span></span> 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="e8f2a-349">Depois de usar ssh, altere o diretório para versão relevantes hello e sudo Olá dotnet dll:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-349">After using ssh, change directory for hello relevant version and sudo hello dotnet dll:</span></span> 

- <span data-ttu-id="e8f2a-350">Para o Microsoft R Server 9.1:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-350">For Microsoft R Server 9.1:</span></span>

    <span data-ttu-id="e8f2a-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="e8f2a-351">cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll</span></span>

- <span data-ttu-id="e8f2a-352">Para o Microsoft R Server 9.0:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-352">For Microsoft R Server 9.0:</span></span>

    <span data-ttu-id="e8f2a-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span><span class="sxs-lookup"><span data-stu-id="e8f2a-353">cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll</span></span>

<span data-ttu-id="e8f2a-354">operacionalização do Microsoft R Server tooconfigure com uma configuração de uma caixa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-354">tooconfigure Microsoft R Server operationalization with a One-box configuration do hello following:</span></span>

1. <span data-ttu-id="e8f2a-355">Selecione “Configurar o R Server para operacionalização”</span><span class="sxs-lookup"><span data-stu-id="e8f2a-355">Select “Configure R Server for Operationalization”</span></span>
2. <span data-ttu-id="e8f2a-356">Selecione "A.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-356">Select “A.</span></span> <span data-ttu-id="e8f2a-357">Uma caixa (web + nós de computação)"</span><span class="sxs-lookup"><span data-stu-id="e8f2a-357">One-box (web + compute nodes)”</span></span>
3. <span data-ttu-id="e8f2a-358">Digite uma senha para Olá **admin** usuário</span><span class="sxs-lookup"><span data-stu-id="e8f2a-358">Enter a password for hello **admin** user</span></span>

![operações de uma caixa](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

<span data-ttu-id="e8f2a-360">Como uma etapa opcional, você pode executar verificações de diagnóstico com um teste de diagnóstico da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-360">As an optional step you can perform Diagnostic checks by running a diagnostic test as follows:</span></span>

1. <span data-ttu-id="e8f2a-361">Selecione "6.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-361">Select “6.</span></span> <span data-ttu-id="e8f2a-362">Executar testes de diagnóstico”</span><span class="sxs-lookup"><span data-stu-id="e8f2a-362">Run diagnostic tests”</span></span>
2. <span data-ttu-id="e8f2a-363">Selecione "A.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-363">Select “A.</span></span> <span data-ttu-id="e8f2a-364">Configuração de teste”</span><span class="sxs-lookup"><span data-stu-id="e8f2a-364">Test configuration”</span></span>
3. <span data-ttu-id="e8f2a-365">Insira o nome de usuário = "admin" e a senha da etapa de configuração anterior</span><span class="sxs-lookup"><span data-stu-id="e8f2a-365">Enter Username = “admin” and password from previous configuration step</span></span>
4. <span data-ttu-id="e8f2a-366">Confirme a integridade geral = aprovado</span><span class="sxs-lookup"><span data-stu-id="e8f2a-366">Confirm Overall Health = pass</span></span>
5. <span data-ttu-id="e8f2a-367">Utilitário de administração de saudação de saída</span><span class="sxs-lookup"><span data-stu-id="e8f2a-367">Exit hello Admin Utility</span></span>
6. <span data-ttu-id="e8f2a-368">Sair do SSH</span><span class="sxs-lookup"><span data-stu-id="e8f2a-368">Exit SSH</span></span>

![Diagnóstico para operações](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
><span data-ttu-id="e8f2a-370">**Atrasos longos ao consumir um serviço web no Spark**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-370">**Long delays when consuming web service on Spark**</span></span>
>
><span data-ttu-id="e8f2a-371">Se você encontrar longos atrasos ao tentar tooconsume um serviço web criado com as funções de mrsdeploy em um contexto de computação Spark, talvez seja necessário tooadd algumas pastas ausentes.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-371">If you encounter long delays when trying tooconsume a web service created with mrsdeploy functions in a Spark compute context, you may need tooadd some missing folders.</span></span> <span data-ttu-id="e8f2a-372">Olá aplicativo Spark pertence a usuário tooa chamado '*rserve2*' sempre que ele é chamado de um serviço web usando funções mrsdeploy.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-372">hello Spark application belongs tooa user called '*rserve2*' whenever it is invoked from a web service using mrsdeploy functions.</span></span> <span data-ttu-id="e8f2a-373">toowork esse problema:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-373">toowork around this issue:</span></span>

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


<span data-ttu-id="e8f2a-374">Neste estágio, a configuração de saudação para operacionalização foi concluída.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-374">At this stage, hello configuration for Operationalization is complete.</span></span> <span data-ttu-id="e8f2a-375">Agora você pode usar o hello 'mrsdeploy' o pacote em seu toohello de tooconnect RClient operacionalização no nó de borda e começar a usar seus recursos, como [execução remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e [serviços web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-375">Now you can use hello ‘mrsdeploy’ package on your RClient tooconnect toohello Operationalization on edge node and start using its features like [remote execution](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) and [web-services](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette).</span></span> <span data-ttu-id="e8f2a-376">Dependendo se o cluster é configurado em uma rede virtual ou não, talvez seja necessário tooset a porta direta túnel por meio de logon SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-376">Depending on whether your cluster is set up on a virtual network or not, you may need tooset up port forward tunneling through SSH login.</span></span> <span data-ttu-id="e8f2a-377">Olá seções a seguir explicam como tooset backup esse túnel.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-377">hello following sections explain how tooset up this tunnel.</span></span>

### <a name="rserver-cluster-on-virtual-network"></a><span data-ttu-id="e8f2a-378">Cluster do RServer em Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="e8f2a-378">RServer Cluster on virtual network</span></span>

<span data-ttu-id="e8f2a-379">Verifique se que você permitir o tráfego por meio do nó de borda toohello 12800 de porta.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-379">Make sure you allow traffic through port 12800 toohello edge node.</span></span> <span data-ttu-id="e8f2a-380">Dessa forma, você pode usar o recurso do hello borda nó tooconnect toohello operacionalização.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-380">That way, you can use hello edge node tooconnect toohello Operationalization feature.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


<span data-ttu-id="e8f2a-381">Se hello `remoteLogin()` não é possível conectar-se o nó de borda toohello, mas é possível que o nó de borda toohello SSH, você precisará tooverify se o tráfego na porta 12800 tooallow de regra de saudação foi configurado corretamente ou não.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-381">If hello `remoteLogin()` cannot connect toohello edge node, but you can SSH toohello edge node, then you need tooverify whether hello rule tooallow traffic on port 12800 has been set properly or not.</span></span> <span data-ttu-id="e8f2a-382">Se você continuar problema de saudação tooface, você pode trabalhar ao redor dele com a configuração de porta direta túnel por meio do SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-382">If you continue tooface hello issue, you can work around it by setting up port forward tunneling through SSH.</span></span> <span data-ttu-id="e8f2a-383">Para obter instruções, consulte Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-383">For instructions, see hello following section.</span></span>

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a><span data-ttu-id="e8f2a-384">Cluster do RServer não configurado em rede virtual</span><span class="sxs-lookup"><span data-stu-id="e8f2a-384">RServer Cluster not set up on virtual network</span></span>

<span data-ttu-id="e8f2a-385">Se o cluster não estiver configurado na rede virtual ou se você estiver tendo problemas com a conectividade por meio da rede virtual, use o túnel SSH de encaminhamento da porta:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-385">If your cluster is not set up on vnet or if you are having troubles with connectivity through vnet, you can use SSH port forward tunneling:</span></span>

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

<span data-ttu-id="e8f2a-386">Você também pode configurá-la em Putty.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-386">On Putty, you can set it up as well.</span></span>

![conexão SSH em putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

<span data-ttu-id="e8f2a-388">Depois que sua sessão SSH está ativa, o tráfego de saudação da porta do computador 12800 é encaminhado porta do nó de borda toohello 12800 por meio de sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-388">Once your SSH session is active, hello traffic from your machine’s port 12800 is forwarded toohello edge node’s port 12800 through SSH session.</span></span> <span data-ttu-id="e8f2a-389">Use `127.0.0.1:12800` no seu método `remoteLogin()`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-389">Make sure you use `127.0.0.1:12800` in your `remoteLogin()` method.</span></span> <span data-ttu-id="e8f2a-390">Isso registra no operacionalização do nó de borda toohello por meio de encaminhamento de porta.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-390">This logs in toohello edge node’s operationalization through port forwarding.</span></span>


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a><span data-ttu-id="e8f2a-391">Como o tooscale Microsoft R Server operacionalização nós em nós de trabalho HDInsight de computação</span><span class="sxs-lookup"><span data-stu-id="e8f2a-391">How tooscale Microsoft R Server Operationalization compute nodes on HDInsight worker nodes</span></span>

### <a name="decommission-hello-worker-nodes"></a><span data-ttu-id="e8f2a-392">Encerrar Olá nó (s) de trabalho</span><span class="sxs-lookup"><span data-stu-id="e8f2a-392">Decommission hello worker node(s)</span></span>

<span data-ttu-id="e8f2a-393">Atualmente, o Microsoft R Server não é gerenciado por meio de Yarn.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-393">Microsoft R Server is currently not managed through Yarn.</span></span> <span data-ttu-id="e8f2a-394">Se nós de trabalho Olá não estiverem encerrados, Olá Yarn Gerenciador de recursos não funcionará conforme esperado, pois ele não estar ciente recursos Olá consumidos pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-394">If hello worker nodes are not decommissioned, hello Yarn Resource Manager will not work as expected because it will not be aware of hello resources being taken up by hello server.</span></span> <span data-ttu-id="e8f2a-395">Em ordem tooavoid nessa situação, é recomendável encerramento nós de trabalho Olá antes de você expandir nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-395">In order tooavoid this situation, we recommend decommissioning hello worker nodes before you scale out hello compute nodes.</span></span>

<span data-ttu-id="e8f2a-396">Nós de trabalho toodecommissioning etapas:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-396">Steps toodecommissioning worker nodes:</span></span>

* <span data-ttu-id="e8f2a-397">Faça logon no console do Ambari tooHDI do cluster e clique na guia "hosts"</span><span class="sxs-lookup"><span data-stu-id="e8f2a-397">Log in tooHDI cluster's Ambari console and click on "hosts" tab</span></span>
* <span data-ttu-id="e8f2a-398">Selecione nós de trabalho (toobe encerrado), clique em "Ações" > "Hosts selecionados" > "Hosts" > clique em "Ativar o modo de manutenção ON".</span><span class="sxs-lookup"><span data-stu-id="e8f2a-398">Select worker nodes (toobe decommissioned), Click on "Actions" > "Selected Hosts" > "Hosts" > click on "Turn ON Maintenance Mode".</span></span> <span data-ttu-id="e8f2a-399">Por exemplo, Olá a imagem a seguir nós selecionamos toodecommission wn3 e wn4.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-399">For example, in hello following image we have selected wn3 and wn4 toodecommission.</span></span>  

   ![encerrar nós de trabalho](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* <span data-ttu-id="e8f2a-401">Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > clique em **Desativar**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-401">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Decommission**</span></span>
* <span data-ttu-id="e8f2a-402">Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > clique em **Desativar**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-402">Select **Actions** > **Selected Hosts** > **NodeManagers** > click **Decommission**</span></span>
* <span data-ttu-id="e8f2a-403">Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > clique em **Parar**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-403">Select **Actions** > **Selected Hosts** > **DataNodes** > click **Stop**</span></span>
* <span data-ttu-id="e8f2a-404">Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > clique em **Parar**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-404">Select **Actions** > **Selected Hosts** > **NodeManagers** > click on **Stop**</span></span>
* <span data-ttu-id="e8f2a-405">Selecione **Ações** > **Hosts Selecionados** > **Hosts** > clique em **Parar Todos os Componentes**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-405">Select **Actions** > **Selected Hosts** > **Hosts** > click **Stop All Components**</span></span>
* <span data-ttu-id="e8f2a-406">Cancele a seleção de nós de trabalho hello e selecione nós de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="e8f2a-406">Unselect hello worker nodes and select hello head nodes</span></span>
* <span data-ttu-id="e8f2a-407">Selecione **Ações** > **Hosts selecionados** > "**Hosts** > **Reiniciar Todos os Componentes**</span><span class="sxs-lookup"><span data-stu-id="e8f2a-407">Select **Actions** > **Selected Hosts** > "**Hosts** > **Restart All Components**</span></span>

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a><span data-ttu-id="e8f2a-408">Configurar nós de computação em cada nó de trabalho encerrado</span><span class="sxs-lookup"><span data-stu-id="e8f2a-408">Configure Compute nodes on each decommissioned worker node(s)</span></span>

1. <span data-ttu-id="e8f2a-409">SSH em cada nó de trabalho desativado.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-409">SSH into each decommissioned worker node.</span></span>
2. <span data-ttu-id="e8f2a-410">Executar o utilitário Administrador usando `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-410">Run admin utility using `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.</span></span>
3. <span data-ttu-id="e8f2a-411">Insira "1" tooselect opção "Configurar o servidor de R para operacionalização".</span><span class="sxs-lookup"><span data-stu-id="e8f2a-411">Enter "1" tooselect option "Configure R Server for Operationalization".</span></span>
4. <span data-ttu-id="e8f2a-412">Insira a opção tooselect "c" "c.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-412">Enter "c" tooselect option "C.</span></span> <span data-ttu-id="e8f2a-413">Nó de computação”.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-413">Compute node".</span></span> <span data-ttu-id="e8f2a-414">Isso configura o nó de computação Olá no nó do operador hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-414">This configures hello compute node on hello worker node.</span></span>
5. <span data-ttu-id="e8f2a-415">Utilitário de administração de saudação de saída.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-415">Exit hello Admin Utility.</span></span>

### <a name="add-compute-nodes-details-on-web-node"></a><span data-ttu-id="e8f2a-416">Adicionar detalhes de nós de computação no nó da Web</span><span class="sxs-lookup"><span data-stu-id="e8f2a-416">Add compute nodes details on Web Node</span></span>

<span data-ttu-id="e8f2a-417">Depois que todos os nós de trabalho encerrado foram configurados toorun nó de computação, volte no nó de borda hello e adicionar endereços IP de nós de trabalho encerrado na configuração do nó de web do Microsoft R Server hello:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-417">Once all decommissioned worker nodes have been configured toorun compute node, come back on hello edge node and add decommissioned worker nodes' IP addresses in hello Microsoft R Server web node's configuration:</span></span>

* <span data-ttu-id="e8f2a-418">SSH no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-418">SSH into hello edge node.</span></span>
* <span data-ttu-id="e8f2a-419">Execute `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-419">Run `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.</span></span>
* <span data-ttu-id="e8f2a-420">Procure Olá seção "URIs" e adicionar IP do nó do operador e detalhes de porta.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-420">Look for hello "URIs" section, and add worker node's IP and port details.</span></span>

    ![encerrar nós de trabalho cmdline](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a><span data-ttu-id="e8f2a-422">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e8f2a-422">Troubleshoot</span></span>

<span data-ttu-id="e8f2a-423">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="e8f2a-423">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8f2a-424">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8f2a-424">Next steps</span></span>

<span data-ttu-id="e8f2a-425">Agora você deve entender como um novo cluster HDInsight que inclui as Noções básicas de R Server e hello de saudação do uso de toocreate Olá console de R em uma sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="e8f2a-425">Now you should understand how toocreate a new HDInsight cluster that includes hello R Server and hello basics of using hello R console from an SSH session.</span></span> <span data-ttu-id="e8f2a-426">Olá tópicos seguintes explicam outras maneiras de gerenciar e trabalhar com R Server no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e8f2a-426">hello following topics explain other ways of managing and working with R Server on HDInsight:</span></span>

* [<span data-ttu-id="e8f2a-427">Adicionar servidor RStudio tooHDInsight (se não é instalado durante a criação do cluster)</span><span class="sxs-lookup"><span data-stu-id="e8f2a-427">Add RStudio Server tooHDInsight (if not installed during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="e8f2a-428">Opções de contexto de computação para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8f2a-428">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)
* [<span data-ttu-id="e8f2a-429">Opções de Armazenamento do Azure para o Servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e8f2a-429">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)
