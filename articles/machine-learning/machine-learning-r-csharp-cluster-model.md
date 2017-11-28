---
title: AAA(deprecated) modelo de Cluster - Azure | Microsoft Docs
description: (preterido) Modelo de cluster
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="15852-103">(preterido) Modelo de cluster</span><span class="sxs-lookup"><span data-stu-id="15852-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="15852-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="15852-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="15852-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="15852-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="15852-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="15852-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="15852-107">Como podemos prever grupos comportamentos dos sistema crédito em ordem tooreduce Olá custos off risco de emissores de cartão de crédito?</span><span class="sxs-lookup"><span data-stu-id="15852-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="15852-108">Como pode podemos definir grupos de características de identificação de funcionários em ordem tooimprove seu desempenho no trabalho?</span><span class="sxs-lookup"><span data-stu-id="15852-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="15852-109">Como o médicos podem classificar pacientes em grupos com base nas características de saudação do seus infecciosas?</span><span class="sxs-lookup"><span data-stu-id="15852-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="15852-110">A princípio, todas essas perguntas podem ser respondidas por meio da análise de cluster.</span><span class="sxs-lookup"><span data-stu-id="15852-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="15852-111">A análise de cluster classifica um conjunto de observações em dois ou mais grupos desconhecidos que se excluem mutuamente com base nas combinações de variáveis.</span><span class="sxs-lookup"><span data-stu-id="15852-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="15852-112">finalidade de saudação da análise de cluster é toodiscover um sistema de organizar observações, geralmente as pessoas ou suas características em grupos, onde os membros de grupos de saudação compartilham propriedades em comum.</span><span class="sxs-lookup"><span data-stu-id="15852-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="15852-113">Isso [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa Olá metodologia de K-Means, uma técnica normalmente usada de clustering, dados arbitrários de toocluster em grupos.</span><span class="sxs-lookup"><span data-stu-id="15852-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="15852-114">Esse serviço da web usa dados de saudação e número de saudação de k clusters como entrada e produz previsões que Olá k grupos toowhich cada observações pertence.</span><span class="sxs-lookup"><span data-stu-id="15852-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="15852-115">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="15852-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="15852-116">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="15852-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="15852-117">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="15852-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="15852-118">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="15852-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="15852-119">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="15852-119">Consumption of web service</span></span>
<span data-ttu-id="15852-120">Esse serviço da web agrupa dados saudação em um conjunto de k grupos e saídas Olá atribuição de grupo para cada linha.</span><span class="sxs-lookup"><span data-stu-id="15852-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="15852-121">serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgulas (,) e as colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="15852-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="15852-122">serviço web de saudação espera 1 linha por vez.</span><span class="sxs-lookup"><span data-stu-id="15852-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="15852-123">Um conjunto de dados de exemplo poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="15852-123">An example dataset could look like this:</span></span>

![Dados de amostra][1]

<span data-ttu-id="15852-125">Suponha que Olá usuário quisesse tooseparate esses dados em grupos mutuamente 3.</span><span class="sxs-lookup"><span data-stu-id="15852-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="15852-126">Olá dados de entrada para Olá acima de conjunto de dados seria a seguinte Olá: valor = "10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3".</span><span class="sxs-lookup"><span data-stu-id="15852-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="15852-127">saída de Hello é Olá associação de grupo previsto para cada uma das linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="15852-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="15852-128">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="15852-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="15852-129">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="15852-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="15852-130">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="15852-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="15852-131">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="15852-131">Creation of web service</span></span>
> <span data-ttu-id="15852-132">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15852-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="15852-133">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="15852-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="15852-134">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="15852-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="15852-135">De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] extraída de módulos no espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="15852-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="15852-136">esquema de saudação de dados foi criada com um simples [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="15852-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="15852-137">Em seguida, o esquema de dados Olá foi vinculado toohello do cluster modelo, criado novamente com um [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="15852-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="15852-138">Em Olá [Executar Script R] [ execute-r-script] usado para o modelo de cluster Olá, serviço da web de saudação, em seguida, utiliza a função hello "k-means", que é predefinida no hello [Executar Script R] [ execute-r-script] de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="15852-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Fluxo de teste][3]

#### <a name="module-1"></a><span data-ttu-id="15852-140">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="15852-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="15852-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="15852-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="15852-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="15852-142">Limitations</span></span>
<span data-ttu-id="15852-143">Este é um exemplo muito simples de um serviço Web de clustering.</span><span class="sxs-lookup"><span data-stu-id="15852-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="15852-144">Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação desta Web serviço.</span><span class="sxs-lookup"><span data-stu-id="15852-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="15852-145">Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado.</span><span class="sxs-lookup"><span data-stu-id="15852-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="15852-146">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="15852-146">FAQ</span></span>
<span data-ttu-id="15852-147">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="15852-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

