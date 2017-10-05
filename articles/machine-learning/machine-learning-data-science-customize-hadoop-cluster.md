---
title: "Personalizar clusters Hadoop para o Processo de Ciência de Dados de Equipe | Microsoft Docs"
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="8460a-103">Personalizar clusters Hadoop do Azure HDInsight para o Processo de Ciência de Dados de Equipe</span><span class="sxs-lookup"><span data-stu-id="8460a-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="8460a-104">Este artigo descreve como personalizar um cluster Hadoop do HDInsight instalando o Anaconda de 64 bits (Python 2.7) em cada nó quando o cluster for provisionado como um serviço do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8460a-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="8460a-105">Ele também mostra como acessar o nó principal para enviar trabalhos personalizados para o cluster.</span><span class="sxs-lookup"><span data-stu-id="8460a-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="8460a-106">Essa personalização disponibiliza muitos módulos Python populares incluídos no Anaconda para uso em UDFs (Funções Definidas pelo Usuário) projetadas para processar registros Hive no cluster.</span><span class="sxs-lookup"><span data-stu-id="8460a-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="8460a-107">Para obter instruções sobre os procedimentos usados neste cenário, veja [Como enviar consultas do Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="8460a-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="8460a-108">Este menu leva a tópicos que descrevem como configurar os diversos ambientes de ciência de dados usados pelo [TDSP (Processo de Ciência de Dados de Equipe)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8460a-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="8460a-109"><a name="customize"></a>Personalizar o cluster do Hadoop do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8460a-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="8460a-110">Para criar um cluster personalizado Hadoop do HDInsight, faça logon no [**Portal Clássico do Azure**](https://manage.windowsazure.com/), clique em **Novo** no canto inferior esquerdo e selecione SERVIÇOS DE DADOS -> HDINSIGHT -> **CRIAÇÃO PERSONALIZADA** para abrir a janela **Detalhes do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="8460a-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="8460a-112">Insira o nome do cluster a ser criado na página de configuração 1 e aceite os valores padrão para os outros campos.</span><span class="sxs-lookup"><span data-stu-id="8460a-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="8460a-113">Clique na seta para ir para a próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="8460a-113">Click the arrow to go to the next configuration page.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="8460a-115">Na página de configuração 2, insira o número dos **NÓS DE DADOS**, selecione a **REGIÃO/REDE VIRTUAL** e selecione os tamanhos do **NÓ PRINCIPAL** e **NÓ DE DADOS**.</span><span class="sxs-lookup"><span data-stu-id="8460a-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="8460a-116">Clique na seta para ir para a próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="8460a-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="8460a-117">A **REGIÃO/REDE VIRTUAL** precisa ser a mesma que a região da conta de armazenamento que será usada para o cluster do Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8460a-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="8460a-118">Caso contrário, na quarta página de configuração, a conta de armazenamento não aparecerá na lista suspensa de **NOME DA CONTA**.</span><span class="sxs-lookup"><span data-stu-id="8460a-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="8460a-120">Na página de configuração 3, forneça um nome de usuário e senha para o cluster do Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8460a-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="8460a-121">**Não** selecione *Inserir o Hive/Oozie Metastore*.</span><span class="sxs-lookup"><span data-stu-id="8460a-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="8460a-122">Clique na seta para ir para a próxima página de configuração.</span><span class="sxs-lookup"><span data-stu-id="8460a-122">Then, click the arrow to go to the next configuration page.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="8460a-124">Na página de configuração 4, especifique o nome da conta de armazenamento, o contêiner padrão do cluster do Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8460a-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="8460a-125">Se você selecionar *Criar contêiner padrão* na lista suspensa **CONTÊINER PADRÃO**, será criado um contêiner com um nome igual ao do cluster.</span><span class="sxs-lookup"><span data-stu-id="8460a-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="8460a-126">Clique na seta para ir para a última página de configuração.</span><span class="sxs-lookup"><span data-stu-id="8460a-126">Click the arrow to go to the last configuration page.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="8460a-128">Na página de configuração **Ações de Script** final, clique no botão **adicionar ação de script** e preencha os campos de texto com os valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="8460a-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="8460a-129">**NOME** – qualquer cadeia de caracteres como o nome dessa ação de script</span><span class="sxs-lookup"><span data-stu-id="8460a-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="8460a-130">**TIPO DE NÓ** – selecione **Todos os nós**</span><span class="sxs-lookup"><span data-stu-id="8460a-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="8460a-131">**URI do SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="8460a-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="8460a-132">*publicscripts* é um contêiner público na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8460a-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="8460a-133">*getgoing* é usado para compartilhar arquivos de script do PowerShell a fim de facilitar o trabalho dos usuários no Azure</span><span class="sxs-lookup"><span data-stu-id="8460a-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="8460a-134">**PARÂMETROS** - (deixe em branco)</span><span class="sxs-lookup"><span data-stu-id="8460a-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="8460a-135">Por fim, clique na marca de seleção para iniciar a criação do cluster personalizado do Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8460a-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="8460a-137"><a name="headnode"></a> Acessar o nó principal do Cluster do Hadoop</span><span class="sxs-lookup"><span data-stu-id="8460a-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="8460a-138">É necessário habilitar o acesso remoto ao cluster do Hadoop no Azure para acessar o nó principal do cluster do Hadoop via RDP.</span><span class="sxs-lookup"><span data-stu-id="8460a-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="8460a-139">Faça logon no [**Portal Clássico do Azure**](https://manage.windowsazure.com/), selecione **HDInsight** à esquerda, selecione o cluster Hadoop na lista de clusters, clique na guia **CONFIGURAÇÃO** e, em seguida, clique no ícone **HABILITAR CONEXÃO REMOTA** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8460a-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="8460a-141">Na janela **Configurar Área de Trabalho Remota** , insira os campos NOME DE USUÁRIO e SENHA e selecione a data de validade para o acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="8460a-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="8460a-142">Em seguida, clique na marca de seleção para habilitar o acesso remoto ao nó principal do cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8460a-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="8460a-144">O nome de usuário e senha para o acesso remoto não são os mesmos usados ao criar o cluster do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8460a-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="8460a-145">Eles são um conjunto separado de credenciais.</span><span class="sxs-lookup"><span data-stu-id="8460a-145">This is a separate set of credentials.</span></span> <span data-ttu-id="8460a-146">Além disso, a data de validade do acesso remoto deve estar dentro de 7 dias a partir da data atual.</span><span class="sxs-lookup"><span data-stu-id="8460a-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="8460a-147">Após habilitar o acesso remoto, clique em **CONECTAR** na parte inferior da página para iniciar a conexão remota com o nó principal.</span><span class="sxs-lookup"><span data-stu-id="8460a-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="8460a-148">Faça logon no nó principal do cluster do Hadoop inserindo as credenciais do usuário de acesso remoto que você especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8460a-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="8460a-150">As próximas etapas do processo de análise avançada são mapeadas no [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas que movem dados para o HDInsight, que os processa e que obtém amostras deles como parte da preparação para o aprendizado baseado em dados com o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8460a-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="8460a-151">Veja [Como enviar consultas do Hive](machine-learning-data-science-move-hive-tables.md#submit) para obter instruções sobre como acessar os módulos Python incluídos no Anaconda por meio do nó principal do cluster em UDFs (funções definidas pelo usuário) usadas para processar registros do Hive armazenados no cluster.</span><span class="sxs-lookup"><span data-stu-id="8460a-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

