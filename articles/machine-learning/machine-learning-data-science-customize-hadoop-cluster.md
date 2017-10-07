---
title: "clusters de aaaCustomize Hadoop para Olá processo de ciência de dados do Team | Microsoft Docs"
description: "Módulos de Python populares disponibilizados em clusters do Hadoop do Azure HDInsight personalizados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="a698c-103">Personalizar os clusters de Hadoop de HDInsight do Azure para Olá processo de ciência de dados de equipe</span><span class="sxs-lookup"><span data-stu-id="a698c-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="a698c-104">Este artigo descreve como toocustomize uma HDInsight Hadoop cluster instalando Anaconda de 64 bits (Python 2.7) em cada nó ao cluster Olá é provisionado como um serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a698c-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="a698c-105">Ele também mostra como tooaccess Olá cluster do nó principal toosubmit trabalhos personalizados toohello.</span><span class="sxs-lookup"><span data-stu-id="a698c-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="a698c-106">Essa personalização faz muitos módulos Python populares, que são incluídos no Anaconda, projetado definidas UDFs (funções) que estão convenientemente disponíveis para uso em usuário tooprocess registros de Hive no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a698c-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="a698c-107">Para obter instruções sobre procedimentos Olá usadas neste cenário, consulte [como consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="a698c-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="a698c-108">menu a seguir Hello links tootopics que descrevem como tooset backup Olá vários ambientes de ciência de dados usado pelo Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="a698c-109"><a name="customize"></a>Personalizar o cluster do Hadoop do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a698c-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="a698c-110">Iniciar toocreate um cluster HDInsight Hadoop personalizado, efetuando logon muito[**portal clássico do Azure**](https://manage.windowsazure.com/), clique em **novo** no hello esquerda inferior do canto e, em seguida, selecione os serviços de dados -> HDINSIGHT -> **criação personalizada** toobring backup Olá **detalhes do Cluster** janela.</span><span class="sxs-lookup"><span data-stu-id="a698c-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="a698c-112">Nome de saudação do hello cluster toobe criado na página de configuração 1 e aceitar valores padrão para Olá outros campos.</span><span class="sxs-lookup"><span data-stu-id="a698c-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="a698c-113">Clique em Olá seta toogo toohello próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="a698c-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="a698c-115">Na página de configuração 2, insira o número de saudação do **nós de dados**, selecione Olá **região/rede VIRTUAL**e selecione tamanhos Olá Olá **nó de cabeçalho** e hello **o nó de dados**.</span><span class="sxs-lookup"><span data-stu-id="a698c-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="a698c-116">Clique em Olá seta toogo toohello próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="a698c-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="a698c-117">Olá **região/rede VIRTUAL** tem toobe Olá mesmo como região Olá Olá da conta de armazenamento que será usado para o cluster HDInsight Hadoop de saudação do toobe.</span><span class="sxs-lookup"><span data-stu-id="a698c-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a698c-118">Caso contrário, na página de configuração quarta Olá, conta de armazenamento de saudação não serão exibidos na lista suspensa de saudação do **nome da conta**.</span><span class="sxs-lookup"><span data-stu-id="a698c-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="a698c-120">Na página de configuração 3, forneça um nome de usuário e senha para Olá cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a698c-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a698c-121">**Não** Olá selecione *Enter Olá Hive/Oozie Metastore*.</span><span class="sxs-lookup"><span data-stu-id="a698c-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="a698c-122">Em seguida, clique em Olá seta toogo toohello próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="a698c-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="a698c-124">Na página de configuração 4, especifique o nome de conta de armazenamento hello, contêiner de padrão de saudação do hello cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a698c-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="a698c-125">Se você selecionar *criar contêiner padrão* em Olá **CONTÊINER padrão** lista suspensa, um contêiner com hello mesmo nome como Olá cluster será criado.</span><span class="sxs-lookup"><span data-stu-id="a698c-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="a698c-126">Clique em Olá seta toogo toohello última página de configuração.</span><span class="sxs-lookup"><span data-stu-id="a698c-126">Click hello arrow toogo toohello last configuration page.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="a698c-128">No final da saudação **ações de Script** página de configuração, clique em **Adicionar ação de script** botão e, em seguida, preencha os campos de texto de saudação com hello valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="a698c-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="a698c-129">**NOME** -qualquer cadeia de caracteres como nome hello dessa ação de script</span><span class="sxs-lookup"><span data-stu-id="a698c-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="a698c-130">**TIPO DE NÓ** – selecione **Todos os nós**</span><span class="sxs-lookup"><span data-stu-id="a698c-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="a698c-131">**URI do SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="a698c-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="a698c-132">*publicscripts* é um contêiner público na conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="a698c-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="a698c-133">*getgoing* usamos tooshare PowerShell script arquivos toofacilitate trabalho dos usuários no Azure</span><span class="sxs-lookup"><span data-stu-id="a698c-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="a698c-134">**PARÂMETROS** - (deixe em branco)</span><span class="sxs-lookup"><span data-stu-id="a698c-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="a698c-135">Por fim, clique em Olá marca de seleção toostart Olá a criação do cluster de Hadoop de HDInsight Olá personalizado.</span><span class="sxs-lookup"><span data-stu-id="a698c-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="a698c-137"><a name="headnode"></a>Olá acesso cabeçotes de nó de Hadoop Cluster</span><span class="sxs-lookup"><span data-stu-id="a698c-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="a698c-138">Você deve habilitar o cluster de Hadoop toohello acesso remoto no Azure antes de poder acessar o nó principal de saudação do cluster de Hadoop de saudação via RDP.</span><span class="sxs-lookup"><span data-stu-id="a698c-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="a698c-139">Faça logon no toohello [ **portal clássico do Azure**](https://manage.windowsazure.com/), selecione **HDInsight** Olá esquerda, selecione o cluster Hadoop Olá lista de clusters, clique em Olá  **CONFIGURAÇÃO** guia e, em seguida, clique em Olá **habilitar remoto** ícone final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="a698c-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="a698c-141">Em Olá **configurar área de trabalho remota** janela, insira hello nome de usuário e os campos de senha e selecione a data de validade Olá para acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="a698c-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="a698c-142">Clique em Olá marca de seleção tooenable Olá acesso remoto toohello nó principal do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="a698c-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="a698c-144">nome de usuário de saudação e a senha para acesso remoto Olá não são Olá nome usuário e senha que você usa ao criar o cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="a698c-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="a698c-145">Eles são um conjunto separado de credenciais.</span><span class="sxs-lookup"><span data-stu-id="a698c-145">This is a separate set of credentials.</span></span> <span data-ttu-id="a698c-146">Além disso, a data de expiração de saudação do acesso remoto Olá tem toobe dentro de 7 dias de saudação data atual.</span><span class="sxs-lookup"><span data-stu-id="a698c-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="a698c-147">Após a habilitação do acesso remoto, clique em **conectar** final Olá Olá página tooremote no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="a698c-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="a698c-148">Logon toohello o nó principal do cluster de Hadoop Olá inserindo credenciais de saudação do usuário de acesso remoto de saudação que você especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a698c-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="a698c-150">Olá próximas etapas no hello avançado do processo de análise são mapeadas em Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas para movem dados para HDInsight, em seguida, processam e exemplo-lo na preparação para aprender com dados saudação com o aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="a698c-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="a698c-151">Consulte [como consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) para obter instruções sobre como tooaccess Olá módulos Python que estão incluídos no Anaconda do nó principal de saudação do cluster de saudação em funções definidas pelo usuário (UDFs) que são usados tooprocess Hive registros armazenados no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="a698c-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

