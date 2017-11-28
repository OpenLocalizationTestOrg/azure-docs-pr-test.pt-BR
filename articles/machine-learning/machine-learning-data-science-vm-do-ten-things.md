---
title: "Olá de aaaTen coisas que você pode fazer na máquina de Virtual de ciência de dados | Microsoft Docs"
description: "Execute várias exploração de dados e tarefas de modelagem em ciência de dados Olá Máquina Virtual."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="d15d6-103">Dez coisas que você pode fazer na ciência de dados Olá Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d15d6-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="d15d6-104">saudação de máquina Virtual de ciência de dados da Microsoft (DSVM) é um ambiente de desenvolvimento de ciência de dados avançados que permite que você tooperform várias tarefas de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="d15d6-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="d15d6-105">Olá ambiente vem já construído e agrupado com dados populares várias ferramentas de análise que tornam mais fácil tooget familiarizar rapidamente com a análise para local, de nuvem ou híbrida implantações.</span><span class="sxs-lookup"><span data-stu-id="d15d6-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="d15d6-106">Olá DSVM trabalha em conjunto com muitos serviços do Azure e é capaz de tooread e processar os dados que já esteja armazenados no Azure, no Azure SQL Data Warehouse, o Azure Data Lake, o armazenamento do Azure ou no banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d15d6-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="d15d6-107">Ela também aproveita outras ferramentas de análise, como o Azure Machine Learning e o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d15d6-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="d15d6-108">Neste artigo, mostrarei como toouse tooperform sua DSVM ciência de dados de várias tarefas e interagir com outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="d15d6-109">Aqui estão algumas das coisas Olá que você pode fazer no hello DSVM:</span><span class="sxs-lookup"><span data-stu-id="d15d6-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="d15d6-110">Explorar dados e desenvolver modelos localmente em Olá DSVM usando o Microsoft R Server, Python</span><span class="sxs-lookup"><span data-stu-id="d15d6-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="d15d6-111">Usar um tooexperiment de notebook Jupyter com seus dados em um navegador usando uma versão pronta enterprise do R criado para escalabilidade e desempenho de Python 2, 3 de Python, Microsoft R</span><span class="sxs-lookup"><span data-stu-id="d15d6-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="d15d6-112">Operacionalizar modelos criados usando R e Python no Azure Machine Learning para que os aplicativos cliente possam acessar seus modelos usando uma interface simples de serviços Web</span><span class="sxs-lookup"><span data-stu-id="d15d6-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="d15d6-113">Administrar os recursos do Azure usando o portal do Azure ou o Powershell</span><span class="sxs-lookup"><span data-stu-id="d15d6-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="d15d6-114">Estender o espaço de armazenamento e compartilhar conjuntos de dados/códigos em grande escala com toda sua equipe criando um armazenamento de Arquivos do Azure como uma unidade montável na DSVM</span><span class="sxs-lookup"><span data-stu-id="d15d6-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="d15d6-115">Compartilhar código com sua equipe usando GitHub e acessar o repositório usando Olá pré-instalados Git clientes - Git Bash GUI do Git.</span><span class="sxs-lookup"><span data-stu-id="d15d6-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="d15d6-116">Acessar vários serviços de análise e dados do Azure, como armazenamento de blobs do Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, SQL Data Warehouse do Azure e bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d15d6-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="d15d6-117">Criar relatórios e painel usando Olá pré-instalado Olá DSVM do Power BI Desktop e implantá-los na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="d15d6-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="d15d6-118">Dimensionar dinamicamente seu toomeet DSVM que precisa de seu projeto</span><span class="sxs-lookup"><span data-stu-id="d15d6-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="d15d6-119">Instalar ferramentas adicionais na sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d15d6-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="d15d6-120">Encargos de uso adicionais se aplicam para muitos dos produtos de serviços de armazenamento e análise de dados adicionais hello listados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d15d6-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="d15d6-121">Consulte toohello [preços do Azure](https://azure.microsoft.com/pricing/) página para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d15d6-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="d15d6-122">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="d15d6-122">**Prerequisites**</span></span>

* <span data-ttu-id="d15d6-123">É necessária uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-123">You need an Azure subscription.</span></span> <span data-ttu-id="d15d6-124">Você pode se inscrever para uma avaliação gratuita [aqui](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="d15d6-125">Instruções para o provisionamento de uma máquina Virtual de ciência de dados Olá portal do Azure estão disponíveis em [criar uma máquina virtual](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="d15d6-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="d15d6-126">1. Explorar dados e desenvolver modelos usando o Microsoft R Server ou Python</span><span class="sxs-lookup"><span data-stu-id="d15d6-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="d15d6-127">Você pode usar linguagens como R e Python toodo sua análise de dados à direita na Olá DSVM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="d15d6-128">Para R, você pode usar um IDE chamado "Revolution R Enterprise 8.0" que pode ser encontrado no menu de início de saudação ou área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="d15d6-129">A Microsoft forneceu bibliotecas adicionais sobre os Olá abrir tooenable de fonte/CRAN-R escalonáveis análise e hello capacidade tooanalyze dados maior do que o tamanho da memória Olá permitido ao fazer a análise em paralelo.</span><span class="sxs-lookup"><span data-stu-id="d15d6-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="d15d6-130">Você também pode instalar um IDE do R que quiser, por exemplo, [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="d15d6-131">Para Python, você pode usar um IDE como Visual Studio Community Edition que tem Olá ferramentas Python para a extensão do Visual Studio (PTVS) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="d15d6-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="d15d6-132">Por padrão, somente um Python 2.7 básico está configurado no PTVS (sem nenhuma biblioteca de análise como SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="d15d6-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="d15d6-133">Em ordem tooenable Anaconda Python 2.7 e 3.5, você precisa fazer toodo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d15d6-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="d15d6-134">Criar ambientes personalizados para cada versão navegando muito**ferramentas** -> **ferramentas Python** -> **Python ambientes** e, em seguida, clicando em " **+ Personalizado**"em Olá Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="d15d6-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="d15d6-135">Forneça uma descrição e definir caminhos de prefixo, como o ambiente de saudação *c:\anaconda* Anaconda Python 2.7 ou *c:\anaconda\envs\py35* Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="d15d6-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="d15d6-136">Clique em **detecção automática** e **aplicar** toosave ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="d15d6-137">É aqui que configuração de ambiente personalizado Olá aparência no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d15d6-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Configuração do PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="d15d6-139">Consulte Olá [documentação PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para obter detalhes adicionais sobre como toocreate ambientes de Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="d15d6-140">Agora você está pronto toocreate um novo projeto de Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="d15d6-141">Navegue muito**arquivo** -> **novo** -> **projeto** -> **Python** e selecione o tipo de saudação do Você está criando um aplicativo de Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="d15d6-142">Você pode definir o ambiente de Python Olá Olá projeto toohello desejado versão atual (Anaconda 2.7 ou 3.5): Olá do botão direito do mouse **ambiente Python**, selecione **Adicionar/remover Python ambientes**, e em seguida, selecione Olá desejado ambiente tooassociate com projeto hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="d15d6-143">Você pode encontrar mais informações sobre como trabalhar com PTVS no produto Olá [documentação](https://github.com/Microsoft/PTVS/wiki) página.</span><span class="sxs-lookup"><span data-stu-id="d15d6-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="d15d6-144">2. Usando um modelo e anotações do Jupyter tooexplore seus dados com Python ou R</span><span class="sxs-lookup"><span data-stu-id="d15d6-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="d15d6-145">saudação de anotações do Jupyter é um ambiente poderoso que fornece um baseado em navegador "IDE" para modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="d15d6-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="d15d6-146">Você pode usar o Python 2, 3 de Python ou R (código-fonte aberto e Olá Microsoft R Server) em um bloco de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d15d6-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="d15d6-147">Olá toolaunch Jupyter Notebook clique no ícone do menu Iniciar Olá / ícone da área de trabalho denominada **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="d15d6-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="d15d6-148">Em Olá DSVM você também pode procurar muito "https://localhost:9999 /" tooaccess Olá Jupiter Notebook.</span><span class="sxs-lookup"><span data-stu-id="d15d6-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="d15d6-149">Se ele solicitará a senha, use instruções fornecidas na Olá ***como toocreate uma senha forte no servidor de notebook Jupyter Olá*** seção Olá [Olá provisionar máquina de Virtual de ciência de dados da Microsoft](machine-learning-data-science-provision-vm.md)toocreate de tópico de anotações do Jupyter uma senha forte tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="d15d6-150">Depois de abrir o bloco de anotações hello, você deverá ver um diretório que contém alguns blocos de anotações de exemplo que são predefinidos no hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="d15d6-151">Agora você pode:</span><span class="sxs-lookup"><span data-stu-id="d15d6-151">Now you can:</span></span>

* <span data-ttu-id="d15d6-152">Clique no código de Olá Olá notebook toosee.</span><span class="sxs-lookup"><span data-stu-id="d15d6-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="d15d6-153">executar cada célula pressionando **SHIFT-ENTER**.</span><span class="sxs-lookup"><span data-stu-id="d15d6-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="d15d6-154">Execute o bloco de anotações inteiro Olá clicando no **célula** -> **executar**</span><span class="sxs-lookup"><span data-stu-id="d15d6-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="d15d6-155">Crie um novo bloco clicando na Olá Jupyter ícone (canto superior esquerdo) e, em seguida, clicando em **novo** botão hello à direita e, em seguida, escolher o idioma de bloco de anotações de saudação (também conhecido como kernels).</span><span class="sxs-lookup"><span data-stu-id="d15d6-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="d15d6-156">Atualmente suportamos Python 2.7, kernel de saudação R 3.5 Python e R. dá suporte à programação no R de software livre como enterprise Olá escalonável Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="d15d6-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="d15d6-157">Quando estiver no bloco de anotações de saudação pode explorar seus dados, criar modelo hello, testar Olá modelo usando a opção de bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="d15d6-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="d15d6-158">3. Compilar os modelos usando R e Python e operacionalizá-los usando o Machine Learning do Azure</span><span class="sxs-lookup"><span data-stu-id="d15d6-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="d15d6-159">Quando você tiver criado e validado a próxima etapa do modelo Olá geralmente é toodeploy-lo em produção.</span><span class="sxs-lookup"><span data-stu-id="d15d6-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="d15d6-160">Isso permite que o cliente de previsões de modelo aplicativos tooinvoke Olá em um tempo real ou em uma base de modo de lote.</span><span class="sxs-lookup"><span data-stu-id="d15d6-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="d15d6-161">O aprendizado de máquina do Azure fornece um mecanismo toooperationalize um modelo incorporado em R ou Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="d15d6-162">Quando você colocar o modelo no aprendizado de máquina do Azure, um serviço web é exposto que permite que os clientes toomake chamadas REST que passam parâmetros de entrada e receber previsões do modelo hello como saídas.</span><span class="sxs-lookup"><span data-stu-id="d15d6-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="d15d6-163">Se você não ainda inscreveram para o aprendizado de máquina do Azure, você pode obter um espaço de trabalho livre ou um espaço de trabalho padrão visitando Olá [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/) home page e clicar em "Introdução".</span><span class="sxs-lookup"><span data-stu-id="d15d6-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="d15d6-164">Compilar e operacionalizar modelos em Python</span><span class="sxs-lookup"><span data-stu-id="d15d6-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="d15d6-165">Aqui está um trecho de código desenvolvido em um bloco de anotações do Jupyter de Python cria um modelo simple usando Olá Saiba SciKit biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d15d6-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="d15d6-166">método Hello usado toodeploy seu modelos de python tooAzure aprendizado de máquina encapsula Olá previsão do modelo de saudação em uma função e decora-lo com os atributos fornecidos pela biblioteca de python de aprendizado de máquina do Azure pré-instalado Olá que indicam sua máquina do Azure ID do espaço de trabalho de aprendizado, chave de API e saudação de entrada e retornam parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d15d6-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="d15d6-167">Um cliente pode agora fazer chamadas toohello web service.</span><span class="sxs-lookup"><span data-stu-id="d15d6-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="d15d6-168">Existem wrappers de conveniência que constroem Olá solicitações da API REST.</span><span class="sxs-lookup"><span data-stu-id="d15d6-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="d15d6-169">Aqui está um exemplo código tooconsume Olá web de serviço.</span><span class="sxs-lookup"><span data-stu-id="d15d6-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="d15d6-170">biblioteca de aprendizado de máquina do Azure Olá só tem suporte em Python 2.7 no momento.</span><span class="sxs-lookup"><span data-stu-id="d15d6-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="d15d6-171">Criar e operacionalizar modelos R</span><span class="sxs-lookup"><span data-stu-id="d15d6-171">Build and Operationalize R models</span></span>
<span data-ttu-id="d15d6-172">Você pode implantar os modelos de R criados no hello máquina de Virtual de ciência de dados ou em outro lugar no aprendizado de máquina do Azure de forma que seja semelhante toohow que é feito para Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="d15d6-173">O hello etapas:</span><span class="sxs-lookup"><span data-stu-id="d15d6-173">Her are hello steps:</span></span>

* <span data-ttu-id="d15d6-174">Crie um tooprovide de arquivo settings.json a ID do espaço de trabalho e a autenticação de token conforme Olá exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d15d6-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="d15d6-175">grave um wrapper para a função de previsão do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="d15d6-176">chamar ```publishWebService``` em Olá toopass de biblioteca de aprendizado de máquina do Azure no wrapper de função hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="d15d6-177">Aqui está a saudação procedimento e trechos de código que podem ser usado tooset up, criar, publicar e consumir um modelo como um serviço web no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="d15d6-178">Configuração</span><span class="sxs-lookup"><span data-stu-id="d15d6-178">Setup</span></span>
1. <span data-ttu-id="d15d6-179">Instalar o pacote de R de aprendizado de máquina Olá digitando ```install.packages("AzureML")``` no IDE do Revolution R Enterprise 8.0 ou seu IDE de R.</span><span class="sxs-lookup"><span data-stu-id="d15d6-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="d15d6-180">Baixe o RTools [daqui](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="d15d6-181">Você precisa Olá zip utilitário no caminho de saudação (e nomeado zip.exe) toooperationalize seu pacote de R no aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d15d6-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="d15d6-182">Criar um arquivo settings.json em um diretório chamado ```.azureml``` em seu diretório base e insira parâmetros de saudação do seu espaço de trabalho do aprendizado de máquina do Azure:</span><span class="sxs-lookup"><span data-stu-id="d15d6-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="d15d6-183">Estrutura do arquivo settings.json:</span><span class="sxs-lookup"><span data-stu-id="d15d6-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="d15d6-184">Compilar um modelo em R e publicá-lo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d15d6-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="d15d6-185">Consumir Olá modelo implantado no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="d15d6-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="d15d6-186">tooconsume o modelo de saudação de um aplicativo cliente, usamos Olá toolook de biblioteca de aprendizado de máquina do Azure backup Olá publicado o serviço web por nome usando Olá `services` ponto de extremidade Olá toodetermine de chamada de API.</span><span class="sxs-lookup"><span data-stu-id="d15d6-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="d15d6-187">Em seguida, você simplesmente chama hello `consume` de função e passar Olá toobe de quadro de dados previsto.</span><span class="sxs-lookup"><span data-stu-id="d15d6-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="d15d6-188">saudação de código a seguir é o modelo de saudação de tooconsume usado publicado como um serviço web de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="d15d6-189">Para obter mais informações sobre a biblioteca de R de aprendizado de máquina do Azure Olá podem ser encontradas [aqui](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="d15d6-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="d15d6-190">4. Administrar os recursos do Azure usando o portal do Azure ou o Powershell</span><span class="sxs-lookup"><span data-stu-id="d15d6-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="d15d6-191">Olá DSVM não só permite que você toobuild sua solução de análise localmente no Olá a máquina virtual, mas também permite que você tooaccess serviços em nuvem do Azure da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d15d6-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="d15d6-192">O Azure fornece vários serviços de análise de dados, armazenamento e computação, além de outros serviços que você pode administrar e acessar da DSVM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="d15d6-193">tooadminister seus recursos de assinatura e na nuvem do Azure, você pode usar o navegador e o ponto toothe [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d15d6-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d15d6-194">Você também pode usar o Azure Powershell tooadminister sua assinatura do Azure e seus recursos por meio de um script.</span><span class="sxs-lookup"><span data-stu-id="d15d6-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="d15d6-195">Você pode executar o Powershell do Azure de um atalho na área de trabalho de saudação ou de saudação iniciar menu intitulada "Microsoft Azure Powershell".</span><span class="sxs-lookup"><span data-stu-id="d15d6-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="d15d6-196">Consulte a [documentação do Microsoft Azure Powershell](../powershell-azure-resource-manager.md) para obter mais informações sobre como você pode administrar seus recursos e assinatura do Azure usando os scripts do Windows Powershell.</span><span class="sxs-lookup"><span data-stu-id="d15d6-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="d15d6-197">5. Estender o espaço de armazenamento com um sistema de arquivos compartilhado</span><span class="sxs-lookup"><span data-stu-id="d15d6-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="d15d6-198">Os cientistas de dados podem compartilhar grandes conjuntos de dados, código ou outros recursos em equipe hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="d15d6-199">Olá DSVM em si tem cerca de 70GB de espaço disponível.</span><span class="sxs-lookup"><span data-stu-id="d15d6-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="d15d6-200">tooextend seu armazenamento, você pode usar o hello Azure File Service e montá-lo em Olá DSVM ou acessá-lo por meio de uma API REST.</span><span class="sxs-lookup"><span data-stu-id="d15d6-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="d15d6-201">máximo de espaço de compartilhamento do Azure File Service Olá Olá é 5TB e limite de tamanho de arquivo individual é 1TB.</span><span class="sxs-lookup"><span data-stu-id="d15d6-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="d15d6-202">Você pode usar o Azure Powershell toocreate um compartilhamento de serviço de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="d15d6-203">Aqui está o hello script toorun no Azure PowerShell toocreate um compartilhamento de serviço de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="d15d6-204">Agora que você criou um compartilhamento de arquivos do Azure, é possível montá-lo em qualquer máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="d15d6-205">É altamente recomendável que Olá VM está no mesmo data center do Azure como latência de tooavoid de conta de armazenamento hello e dados de encargos de transferência.</span><span class="sxs-lookup"><span data-stu-id="d15d6-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="d15d6-206">Aqui estão as unidade de Olá Olá comandos toomount em Olá DSVM que pode ser executado no Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="d15d6-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="d15d6-207">Agora você pode acessar essa unidade como faria com qualquer unidade normal Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="d15d6-208">6. Compartilhar código com sua equipe usando o GitHub</span><span class="sxs-lookup"><span data-stu-id="d15d6-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="d15d6-209">O GitHub é um repositório de código onde você pode encontrar muitas fontes e código de exemplo para diferentes ferramentas usando diversas tecnologias compartilhadas pela comunidade de desenvolvedores de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="d15d6-210">Ele usa o Git como Olá versões tootrack e repositório de tecnologia Olá de arquivos de código.</span><span class="sxs-lookup"><span data-stu-id="d15d6-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="d15d6-211">O GitHub é também uma plataforma de onde você pode criar seu próprio repositório toostore código compartilhado e a documentação da sua equipe implementar o controle de versão e também controlar quem tem acesso tooview e colaboração de código.</span><span class="sxs-lookup"><span data-stu-id="d15d6-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="d15d6-212">Visite Olá [páginas de Ajuda do GitHub](https://help.github.com/) para obter mais informações sobre como usar o Git.</span><span class="sxs-lookup"><span data-stu-id="d15d6-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="d15d6-213">Você pode usar GitHub como uma saudação maneiras toocollaborate com sua equipe, em seguida, use o código desenvolvido pela comunidade Olá e colaboração da comunidade do código toohello back.</span><span class="sxs-lookup"><span data-stu-id="d15d6-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="d15d6-214">Olá DSVM já vem carregado com ferramentas de cliente em linha de comando como bem GUI tooaccess repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="d15d6-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="d15d6-215">Olá ferramenta de linha de comando toowork com Git e GitHub é chamado de Git Bash.</span><span class="sxs-lookup"><span data-stu-id="d15d6-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="d15d6-216">Visual Studio instalado Olá DSVM tem extensões de Git hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="d15d6-217">Você pode encontrar ícones de inicialização para essas ferramentas no menu de início do hello e área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="d15d6-218">código de toodownload de um repositório GitHub é usar Olá ```git clone``` comando.</span><span class="sxs-lookup"><span data-stu-id="d15d6-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="d15d6-219">Por exemplo repositório de ciência de dados toodownload publicado pela Microsoft no diretório atual Olá você pode executar Olá comando a seguir quando estiver no ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="d15d6-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="d15d6-220">No Visual Studio, você pode fazer Olá a mesma operação de clonagem.</span><span class="sxs-lookup"><span data-stu-id="d15d6-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="d15d6-221">Olá captura de tela a seguir mostra como tooaccess Git e GitHub ferramentas no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d15d6-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Git no Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="d15d6-223">Você pode encontrar mais informações sobre como usar o Git toowork com o repositório do GitHub de vários recursos disponíveis em github.com. Olá [roteiro](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) é uma referência útil.</span><span class="sxs-lookup"><span data-stu-id="d15d6-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="d15d6-224">7. Acessar vários serviços de análise e dados do Azure</span><span class="sxs-lookup"><span data-stu-id="d15d6-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="d15d6-225">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d15d6-225">Azure Blob</span></span>
<span data-ttu-id="d15d6-226">O blob do Azure é um armazenamento em nuvem confiável e econômico para pequenos e grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="d15d6-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="d15d6-227">Vamos dar uma olhada em como você pode mover dados tooAzure Blob e acessar dados armazenados em um Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="d15d6-228">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="d15d6-228">**Prerequisite**</span></span>

* <span data-ttu-id="d15d6-229">**Crie sua conta de Armazenamento de Blobs do Azure no [portal do Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="d15d6-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="d15d6-231">Confirmar essa ferramenta de linha de comando pré-instalados AzCopy do hello é encontrada em ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="d15d6-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="d15d6-232">Ao executar essa ferramenta, você pode adicionar Olá contendo Olá azcopy.exe tooyour caminho ambiente tooavoid variável digitando Olá completo comando caminho do diretório.</span><span class="sxs-lookup"><span data-stu-id="d15d6-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="d15d6-233">Para obter mais informações sobre a ferramenta AzCopy, consulte muito[AzCopy documentação](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="d15d6-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="d15d6-234">Inicie a ferramenta de Gerenciador de armazenamento do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="d15d6-235">Ele pode ser baixado em [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="d15d6-237">**Mover dados de VM tooAzure Blob: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="d15d6-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="d15d6-238">dados de toomove entre seus arquivos locais e o armazenamento de blob, você pode usar o AzCopy na linha de comando ou o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d15d6-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="d15d6-239">Substituir **C:\myfolder** toohello caminho onde o arquivo está armazenado, **mystorageaccount** nome de conta de armazenamento de blob tooyour, **mycontainer** toohello o nome do contêiner, **chave da conta de armazenamento** tooyour chave de acesso de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="d15d6-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="d15d6-240">Você pode encontrar as credenciais da conta de armazenamento no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d15d6-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="d15d6-242">Execute o comando AzCopy no PowerShell ou em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="d15d6-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="d15d6-243">Veja um exemplo de uso do comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="d15d6-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="d15d6-244">Depois que você executar o tooan de toocopy AzCopy comando BLOBs do Azure, consulte o arquivo aparece no Gerenciador de armazenamento do Azure em breve.</span><span class="sxs-lookup"><span data-stu-id="d15d6-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="d15d6-246">**Mover dados de VM tooAzure Blob: Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="d15d6-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="d15d6-247">Você também pode carregar dados de arquivo local Olá em sua VM usando o Gerenciador de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="d15d6-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="d15d6-248">contêiner de tooa tooupload dados, selecione Olá Olá de contêiner e clique em do destino **carregar** botão.![ Carregar no Gerenciador de armazenamento](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="d15d6-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="d15d6-249">Clique em Olá **...**  toohello direito da saudação **arquivos** caixa, selecione um ou vários tooupload de arquivos do sistema de arquivos hello e clique em **carregar** toobegin carregando arquivos hello.![ Carregar arquivos tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="d15d6-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="d15d6-250">**Ler dados de Blobs do Azure: módulo de leitor do Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="d15d6-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="d15d6-251">No estúdio de aprendizado de máquina do Azure, você pode usar um **módulo de importação de dados** tooread dados do seu blob.</span><span class="sxs-lookup"><span data-stu-id="d15d6-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="d15d6-253">**Ler dados do Blob do Azure: ODBC do Python**</span><span class="sxs-lookup"><span data-stu-id="d15d6-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="d15d6-254">Você pode usar **BlobService** dados da biblioteca tooread diretamente do blob em um programa de anotações do Jupyter ou Python.</span><span class="sxs-lookup"><span data-stu-id="d15d6-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="d15d6-255">Primeiro, importe os pacotes necessários:</span><span class="sxs-lookup"><span data-stu-id="d15d6-255">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="d15d6-256">Em seguida, conecte suas credenciais de conta do Blob do Azure e leia os dados no Blob:</span><span class="sxs-lookup"><span data-stu-id="d15d6-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="d15d6-257">dados de saudação é lido em um quadro de dados:</span><span class="sxs-lookup"><span data-stu-id="d15d6-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="d15d6-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d15d6-259">Azure Data Lake</span></span>
<span data-ttu-id="d15d6-260">O Armazenamento do Azure Data Lake é um repositório de grande escala para cargas de trabalho de análise de big data e é compatível com HDFS (Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="d15d6-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="d15d6-261">Ele funciona com o ecossistema de Hadoop hello e Olá análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d15d6-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="d15d6-262">Vamos mostrar como você pode mover dados para Olá repositório Azure Data Lake e executar análise usando a análise do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d15d6-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="d15d6-263">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="d15d6-263">**Prerequisite**</span></span>

* <span data-ttu-id="d15d6-264">Crie seu Azure Data Lake Analytics no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d15d6-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="d15d6-266">Olá **ferramentas do Azure Data Lake** na **Visual Studio** encontrada nesse [link](https://www.microsoft.com/download/details.aspx?id=49504) já está instalado no Visual Studio Community Edition que está na máquina virtual de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="d15d6-267">Depois de iniciar o Visual Studio e log em sua assinatura do Azure, você verá a sua conta de análise de dados do Azure e armazenamento no painel esquerdo de saudação do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d15d6-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="d15d6-269">**Mover dados de VM tooData Lake: Azure Data Lake Explorer**</span><span class="sxs-lookup"><span data-stu-id="d15d6-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="d15d6-270">Você pode usar **Azure Data Lake Explorer** dados tooupload de arquivos locais de saudação em seu armazenamento de máquina Virtual tooData Lake.</span><span class="sxs-lookup"><span data-stu-id="d15d6-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="d15d6-272">Você também pode criar um tooproductionize de pipeline de dados o tooor de movimentação de dados do Azure Data Lake usando Olá [Factory(ADF) de dados do Azure](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="d15d6-273">Nós nos referimos toothis [artigo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide você por meio de dados de saudação do hello etapas toobuild pipelines.</span><span class="sxs-lookup"><span data-stu-id="d15d6-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="d15d6-274">**Ler dados do Azure Blob tooData Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="d15d6-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="d15d6-275">Se os dados residirem no Armazenamento de Blobs, você poderá lê-los diretamente no blob do armazenamento do Azure na consulta U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d15d6-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="d15d6-276">Antes de escrever a consulta U-SQL, certifique-se de que sua conta de armazenamento de blob é tooyour vinculado do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d15d6-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="d15d6-277">Vá muito**portal do Azure**, localizar seu painel de análise do Azure Data Lake, clique em **adicionar fonte de dados**, selecione o tipo de armazenamento muito**armazenamento do Azure** e conecte o armazenamento do Azure Nome da conta e chave.</span><span class="sxs-lookup"><span data-stu-id="d15d6-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="d15d6-278">Você estará tooreference capaz de dados de saudação armazenados na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Insira a conta de armazenamento e a chave](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="d15d6-280">No Visual Studio, você pode ler dados de armazenamento de blob, que algumas manipulação de dados, a engenharia de recurso e a saída Olá resultante dados tooeither Azure Data Lake ou o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="d15d6-281">Ao fazer referência a dados Olá no armazenamento de blob, use **wasb: / /**; quando você faz referência a dados hello Azure Data Lake, use **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="d15d6-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Quadro de dados](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="d15d6-283">Você pode usar o hello consultas U-SQL no Visual Studio a seguir:</span><span class="sxs-lookup"><span data-stu-id="d15d6-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="d15d6-284">Depois de sua consulta é enviada toohello server, um diagrama que mostra o status de saudação do seu trabalho será exibido.</span><span class="sxs-lookup"><span data-stu-id="d15d6-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Diagrama de status do trabalho](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="d15d6-286">**Dados da consulta no Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="d15d6-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="d15d6-287">Depois que o dataset Olá é incluído no Azure Data Lake, você pode usar [linguagem U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery e explorar dados saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="d15d6-288">Linguagem U-SQL é tooT-SQL semelhante, mas combina alguns recursos do c# para que os usuários possam gravar módulos personalizados, funções definidas pelo usuário e etc. Você pode usar scripts de saudação na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="d15d6-289">Após a consulta Olá tooserver enviado, tripdata_summary. CSV pode ser encontrado em breve **Azure Data Lake Explorer**, você pode visualizar dados de saudação pelo arquivo de saudação do botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="d15d6-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Arquivo no Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="d15d6-291">informações do arquivo hello toosee:</span><span class="sxs-lookup"><span data-stu-id="d15d6-291">toosee hello file information:</span></span>

![Resumo do arquivo](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="d15d6-293">Clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="d15d6-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="d15d6-294">HDInsight do Azure é um serviço gerenciado de Apache Hadoop, Spark, HBase e Storm na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="d15d6-295">Você pode trabalhar facilmente com clusters de HDInsight do Azure de saudação máquina de virtual de ciência de dados.</span><span class="sxs-lookup"><span data-stu-id="d15d6-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="d15d6-296">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="d15d6-296">**Prerequisite**</span></span>

* <span data-ttu-id="d15d6-297">Crie sua conta de Armazenamento de Blobs do Azure no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d15d6-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d15d6-298">Esta conta de armazenamento é dados toostore usada para clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d15d6-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Criar uma conta de Armazenamento de Blobs do Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="d15d6-300">Personalize os Clusters do Azure HDInsight Hadoop no [portal do Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="d15d6-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="d15d6-301">Você deve vincular a conta de armazenamento Olá criada com o cluster HDInsight quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="d15d6-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="d15d6-302">Esta conta de armazenamento é usada para acessar os dados que podem ser processados em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Vincular toostorage conta criada com o cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="d15d6-304">Você deve habilitar **acesso remoto** toohello o nó principal do cluster Olá depois que ele é criado.</span><span class="sxs-lookup"><span data-stu-id="d15d6-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="d15d6-305">Lembre-se de credenciais de acesso remoto Olá você especificar aqui (diferentes das especificadas para cluster Olá em sua criação): necessário no procedimento subsequente hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Habilitar o acesso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="d15d6-307">Criar um Espaço de Trabalho do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d15d6-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="d15d6-308">Seus Testes de Machine Learning são armazenados neste espaço de trabalho do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d15d6-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="d15d6-309">Selecione opções de saudação realçada no Portal, conforme mostrado na Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="d15d6-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Criar um espaço de trabalho de Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="d15d6-311">Em seguida, digite os parâmetros de saudação do seu espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="d15d6-311">Then enter hello parameters for your workspace</span></span>

![Insira os parâmetros do Espaço de Trabalho do Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="d15d6-313">Carregue os dados usando o IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d15d6-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="d15d6-314">Primeiro importar pacotes necessários, plug-in de credenciais, crie um banco de dados em sua conta de armazenamento e dados tooHDI clusters de carga.</span><span class="sxs-lookup"><span data-stu-id="d15d6-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="d15d6-315">Como alternativa, você pode seguir esta [passo a passo](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster do táxi NYC dados tooHDI.</span><span class="sxs-lookup"><span data-stu-id="d15d6-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="d15d6-316">As principais etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="d15d6-316">Major steps include:</span></span>
  
  * <span data-ttu-id="d15d6-317">AzCopy: download compactado CSV na pasta local do blob público tooyour</span><span class="sxs-lookup"><span data-stu-id="d15d6-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="d15d6-318">AzCopy: carregar descompactado CSV do cluster de tooHDI de pasta local</span><span class="sxs-lookup"><span data-stu-id="d15d6-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="d15d6-319">Faça logon no nó principal de saudação do cluster de Hadoop e preparar para análise de dados exploratório</span><span class="sxs-lookup"><span data-stu-id="d15d6-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="d15d6-320">Após dados saudação cluster tooHDI carregado, você pode verificar seus dados no Gerenciador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d15d6-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="d15d6-321">Um banco de dados nyctaxidb é criado no cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="d15d6-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="d15d6-322">**Exploração de dados: consultas Hive no Python**</span><span class="sxs-lookup"><span data-stu-id="d15d6-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="d15d6-323">Como dados de saudação são em cluster Hadoop, você pode usar o hello pyodbc pacote tooconnect tooHadoop Clusters e banco de dados de consulta usando Hive toodo exploração e engenharia de recurso.</span><span class="sxs-lookup"><span data-stu-id="d15d6-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="d15d6-324">Você pode exibir as tabelas existentes Olá criada na etapa de pré-requisito hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Exibir tabelas existentes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="d15d6-326">Vamos dar uma olhada no número de saudação de registros em cada mês e hello o frequências de Oblíquo ou não na tabela de viagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="d15d6-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Gráfico do número de registros a cada mês](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Gráfico das frequências de dicas](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="d15d6-329">Podemos também distância Olá entre o local de recebimento e o local de redução de computação e, em seguida, compare-toohello trip distância.</span><span class="sxs-lookup"><span data-stu-id="d15d6-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabela de coleta e entrega](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Plotagem de distância de tootrip de distância de entrega/redução](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="d15d6-332">Agora, vamos preparar uma conjunto reduzido de dados (1%) para modelagem.</span><span class="sxs-lookup"><span data-stu-id="d15d6-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="d15d6-333">Podemos usar esses dados no módulo de leitor do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d15d6-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="d15d6-334">Após alguns instantes, você pode ver dados saudação foi carregados em clusters de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="d15d6-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabela de dados](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="d15d6-336">**Ler dados do HDI usando o Machine Learning: módulo de leitor**</span><span class="sxs-lookup"><span data-stu-id="d15d6-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="d15d6-337">Você também pode usar o hello **leitor** módulo no banco de dados do estúdio de aprendizado de máquina tooaccess Olá no cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d15d6-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="d15d6-338">Plug-in credenciais Olá seus clusters de HDI e conta de armazenamento do Azure tooenable criar modelos usando o banco de dados em clusters HDI do aprendizado de máquina usando o.</span><span class="sxs-lookup"><span data-stu-id="d15d6-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Propriedades do módulo de leitor](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="d15d6-340">Olá conjunto de dados pode ser exibido:</span><span class="sxs-lookup"><span data-stu-id="d15d6-340">hello scored dataset can then be viewed:</span></span>

![Exibir o conjunto de dados pontuado](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="d15d6-342">Azure SQL Data Warehouse e bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d15d6-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="d15d6-343">O SQL Data Warehouse do Azure é um data warehouse elástico como um serviço, com experiência em SQL Server de nível corporativo.</span><span class="sxs-lookup"><span data-stu-id="d15d6-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="d15d6-344">Você pode provisionar o SQL Data Warehouse do Azure seguindo Olá instruções fornecidas neste [artigo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d15d6-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="d15d6-345">Depois de provisionar o SQL Data Warehouse do Azure, você pode usar isso [passo a passo](machine-learning-data-science-process-sqldw-walkthrough.md) toodo para carregar dados, exploração e modelagem de dados dentro de saudação do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d15d6-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="d15d6-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d15d6-346">Azure Cosmos DB</span></span>
<span data-ttu-id="d15d6-347">Banco de dados do Azure Cosmos é um banco de dados NoSQL na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="d15d6-348">Ele permite que você toowork com documentos como JSON e permite que os documentos de saudação toostore e consulta.</span><span class="sxs-lookup"><span data-stu-id="d15d6-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="d15d6-349">Você precisa de saudação toodo seguir por requisitos etapas tooaccess Azure Cosmos DB de saudação DSVM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="d15d6-350">Instalar o SDK do Python para DocumentDB (Execute ```pip install pydocumentdb``` no prompt de comando)</span><span class="sxs-lookup"><span data-stu-id="d15d6-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="d15d6-351">Criar uma conta do Azure Cosmos DB e um banco de dados no [Portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d15d6-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="d15d6-352">Baixar "Ferramenta de migração de banco de dados do Azure Cosmos" de [aqui](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) e extrair tooa diretório de sua escolha</span><span class="sxs-lookup"><span data-stu-id="d15d6-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="d15d6-353">Importar dados JSON (dados vulcões) armazenados em um [blob público](https://cahandson.blob.core.windows.net/samples/volcano.json) no banco de dados do Cosmos com o seguinte comando parâmetros toohello ferramenta de migração (dtui.exe do diretório Olá onde você instalou Olá, ferramenta de migração de banco de dados do Cosmos).</span><span class="sxs-lookup"><span data-stu-id="d15d6-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="d15d6-354">Insira o local de origem e destino de saudação com estes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d15d6-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="d15d6-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="d15d6-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="d15d6-356">Quando você importa dados hello, você pode ir tooJupyter e notebook Olá abrir intitulada *DocumentDBSample* que contém o python tooaccess documentos de código e fazer algumas consultas básicas.</span><span class="sxs-lookup"><span data-stu-id="d15d6-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="d15d6-357">Você pode aprender mais sobre o banco de dados do Cosmos visitando o serviço Olá [página de documentação](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="d15d6-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="d15d6-358">8. Criar relatórios e painel usando Olá Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d15d6-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="d15d6-359">Vamos visualize arquivos de JSON vulcões Olá que vimos no hello precedem Cosmos banco de dados de exemplo em informações visuais do Power BI toogain nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="d15d6-360">Etapas detalhadas estão disponíveis no hello [artigo do Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="d15d6-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="d15d6-361">Aqui estão as etapas de alto nível hello:</span><span class="sxs-lookup"><span data-stu-id="d15d6-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="d15d6-362">Abra o Power BI Desktop e execute "Obter Dados".</span><span class="sxs-lookup"><span data-stu-id="d15d6-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="d15d6-363">Especifique a URL hello como: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="d15d6-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="d15d6-364">Você deve ver os registros JSON de saudação importados como uma lista</span><span class="sxs-lookup"><span data-stu-id="d15d6-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="d15d6-365">Converter a tabela de tooa de lista de saudação para que Power BI possa trabalhar com hello mesmo</span><span class="sxs-lookup"><span data-stu-id="d15d6-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="d15d6-366">Expanda colunas Olá clicando em Olá expanda ícone (Olá um com ícone "seta para a esquerda e uma seta à direita" Olá Olá à direita da coluna de saudação)</span><span class="sxs-lookup"><span data-stu-id="d15d6-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="d15d6-367">Perceba que o local é um campo "Registro".</span><span class="sxs-lookup"><span data-stu-id="d15d6-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="d15d6-368">Expanda registro hello e selecione apenas as coordenadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="d15d6-369">A coordenada é uma coluna de lista</span><span class="sxs-lookup"><span data-stu-id="d15d6-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="d15d6-370">Adicionar uma nova coluna tooconvert Olá lista coordenada de colunas em uma coluna de LatLong separada por vírgulas concatenando elementos Olá dois no campo de coordenada lista hello usando a fórmula de saudação ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="d15d6-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="d15d6-371">Por fim, converter Olá ```Elevation``` tooDecimal de coluna e selecione Olá **fechar** e **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d15d6-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="d15d6-372">Em vez de etapas anteriores, você pode colar Olá após código scripts Olá etapas usadas em Olá Editor Avançado no Power BI que permite transformações de dados Olá toowrite em uma linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="d15d6-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="d15d6-373">Agora você tem dados saudação em seu modelo de dados do Power BI.</span><span class="sxs-lookup"><span data-stu-id="d15d6-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="d15d6-374">A área de trabalho do Power BI deve aparecer da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d15d6-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="d15d6-376">Você pode iniciar a criação de relatórios e visualizações usando o modelo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="d15d6-377">Você pode seguir as etapas de saudação neste [artigo do Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild um relatório.</span><span class="sxs-lookup"><span data-stu-id="d15d6-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="d15d6-378">resultado final de saudação é um relatório semelhante ao seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="d15d6-378">hello end result is a report that looks like hello following.</span></span>

![Exibição de relatório do Power BI Desktop — conector do Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="d15d6-380">9. Dimensionar dinamicamente seu toomeet DSVM que precisa de seu projeto</span><span class="sxs-lookup"><span data-stu-id="d15d6-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="d15d6-381">Você pode dimensionar para cima e Olá DSVM toomeet que precisa de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d15d6-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="d15d6-382">Se não precisar Olá toouse VM em finais de semana ou saudação da noite, você pode desligar Olá VM de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d15d6-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="d15d6-383">Incorre em encargos de computação se você usar apenas Olá botão de desligamento de sistema operacional em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d15d6-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="d15d6-384">Se você precisar toohandle algumas análises de grande escala e precisa de mais capacidade de CPU ou memória ou disco, você pode encontrar uma grande variedade de tamanhos VM em termos de núcleos de CPU, capacidade de memória e tipos de disco (incluindo unidades de estado sólido) que atendem suas necessidades de orçamento e de computação.</span><span class="sxs-lookup"><span data-stu-id="d15d6-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="d15d6-385">Olá lista completa de VMs junto com seus preços por hora de computação está disponível em Olá [preços de máquinas virtuais do Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) página.</span><span class="sxs-lookup"><span data-stu-id="d15d6-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="d15d6-386">Da mesma forma, se reduz a necessidade de capacidade de processamento de VM (por exemplo: você moveu tooa uma grande carga de trabalho Hadoop ou um cluster Spark), você pode reduzir o cluster de saudação do hello [portal do Azure](https://portal.azure.com) e toohello configurações da VM instância.</span><span class="sxs-lookup"><span data-stu-id="d15d6-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="d15d6-387">Veja uma captura de tela.</span><span class="sxs-lookup"><span data-stu-id="d15d6-387">Here is a screenshot.</span></span>

![Configurações da instância VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="d15d6-389">10. Instalar ferramentas adicionais na sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d15d6-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="d15d6-390">Podemos empacotar várias ferramentas que acreditamos que são tooaddress capaz de muitas das necessidades de análise de dados comuns hello e que devem economizar tempo, evitando a necessidade de tooinstall configurar ambientes de uma e economizar dinheiro por pagar apenas para os recursos que você Use.</span><span class="sxs-lookup"><span data-stu-id="d15d6-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="d15d6-391">Você pode aproveitar os outros dados do Azure e serviços de análise descritos neste artigo tooenhance seu ambiente de análise.</span><span class="sxs-lookup"><span data-stu-id="d15d6-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="d15d6-392">Entendemos que, em alguns casos, suas necessidades podem exigir ferramentas adicionais, incluindo algumas ferramentas de terceiros.</span><span class="sxs-lookup"><span data-stu-id="d15d6-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="d15d6-393">Você tem acesso administrativo completo em Olá máquina virtual tooinstall novas ferramentas que você precisa.</span><span class="sxs-lookup"><span data-stu-id="d15d6-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="d15d6-394">Também é possível instalar pacotes adicionais no Python e no R que não foram pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="d15d6-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="d15d6-395">Para Python, você pode usar ```conda``` ou ```pip```.</span><span class="sxs-lookup"><span data-stu-id="d15d6-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="d15d6-396">Para R, você pode usar o hello ```install.packages()``` na Olá R console ou usar Olá IDE e escolha "**pacotes** -> **pacotes de instalação...** ".</span><span class="sxs-lookup"><span data-stu-id="d15d6-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="d15d6-397">Resumo</span><span class="sxs-lookup"><span data-stu-id="d15d6-397">Summary</span></span>
<span data-ttu-id="d15d6-398">Essas são apenas algumas das coisas Olá que você pode fazer no hello máquina de Virtual de ciência de dados do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d15d6-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="d15d6-399">Há muitas outras coisas que você pode fazer toomake-lo um ambiente de análise efetiva.</span><span class="sxs-lookup"><span data-stu-id="d15d6-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

