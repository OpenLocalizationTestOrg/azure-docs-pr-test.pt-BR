---
title: (preterido) Modelo de cluster - Azure | Microsoft Docs
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="938ff-103">(preterido) Modelo de cluster</span><span class="sxs-lookup"><span data-stu-id="938ff-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="938ff-104">O Microsoft DataMarket está sendo desativado e essa API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="938ff-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="938ff-105">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="938ff-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="938ff-106">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="938ff-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="938ff-107">Como podemos prever grupos de titulares de cartão de crédito para reduzir o risco de cancelamento de uma dívida para os emissores de cartão de crédito?</span><span class="sxs-lookup"><span data-stu-id="938ff-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="938ff-108">Como podemos definir grupos de traços de personalidade de funcionários para melhorar seu desempenho no trabalho?</span><span class="sxs-lookup"><span data-stu-id="938ff-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="938ff-109">Como os médicos podem classificar pacientes em grupos com base nas características de suas doenças?</span><span class="sxs-lookup"><span data-stu-id="938ff-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="938ff-110">A princípio, todas essas perguntas podem ser respondidas por meio da análise de cluster.</span><span class="sxs-lookup"><span data-stu-id="938ff-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="938ff-111">A análise de cluster classifica um conjunto de observações em dois ou mais grupos desconhecidos que se excluem mutuamente com base nas combinações de variáveis.</span><span class="sxs-lookup"><span data-stu-id="938ff-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="938ff-112">O objetivo da análise de cluster é descobrir um sistema de organizar observações, geralmente as pessoas ou suas características, em grupos, em que os membros dos grupos compartilham de propriedades em comum.</span><span class="sxs-lookup"><span data-stu-id="938ff-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="938ff-113">Esse [serviço](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa a metodologia de K-Means, uma técnica de clustering comumente usada, para agrupar dados arbitrários em grupos.</span><span class="sxs-lookup"><span data-stu-id="938ff-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="938ff-114">Esse serviço Web usa os dados e o número de clusters k como entrada e produz previsões de a quais dos grupos k cada observação pertence.</span><span class="sxs-lookup"><span data-stu-id="938ff-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="938ff-115">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="938ff-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="938ff-116">Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="938ff-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="938ff-117">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="938ff-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="938ff-118">O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – sem qualquer infraestrutura configurada pelo autor do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="938ff-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="938ff-119">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="938ff-119">Consumption of web service</span></span>
<span data-ttu-id="938ff-120">Esse serviço Web agrupa os dados em um conjunto de grupos k e gera a atribuição de grupo para cada linha.</span><span class="sxs-lookup"><span data-stu-id="938ff-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="938ff-121">O serviço Web espera que o usuário final insira seus dados como cadeias de caracteres em que as linhas são separadas por vírgula (,) e as colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="938ff-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="938ff-122">O serviço Web espera 1 linha por vez.</span><span class="sxs-lookup"><span data-stu-id="938ff-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="938ff-123">Um conjunto de dados de exemplo poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="938ff-123">An example dataset could look like this:</span></span>

![Dados de amostra][1]

<span data-ttu-id="938ff-125">Suponha que o usuário desejasse separar esses dados em três grupos que se excluam mutuamente.</span><span class="sxs-lookup"><span data-stu-id="938ff-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="938ff-126">Os dados de entrada para o conjunto de dados acima seria o seguinte: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span><span class="sxs-lookup"><span data-stu-id="938ff-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="938ff-127">A saída é a associação a um grupo prevista para cada uma das linhas.</span><span class="sxs-lookup"><span data-stu-id="938ff-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="938ff-128">Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="938ff-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="938ff-129">Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo estão [aqui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="938ff-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="938ff-130">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="938ff-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="938ff-131">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="938ff-131">Creation of web service</span></span>
> <span data-ttu-id="938ff-132">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="938ff-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="938ff-133">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="938ff-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="938ff-134">Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="938ff-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="938ff-135">De dentro do Azure Machine Learning, um novo teste em branco foi criado e dois módulos [Executar Script R][execute-r-script] foram levados ao espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="938ff-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="938ff-136">O esquema de dados foi criado com um [Executar Script R][execute-r-script] simples.</span><span class="sxs-lookup"><span data-stu-id="938ff-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="938ff-137">Em seguida, o esquema de dados foi vinculado à seção de modelo de cluster, criada novamente com um [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="938ff-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="938ff-138">No [Executar Script R][execute-r-script] usado para o modelo de cluster, o serviço Web utiliza a função "k-means", que é predefinida no [Executar Script R][execute-r-script] do Machine Learning do Azure.</span><span class="sxs-lookup"><span data-stu-id="938ff-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Fluxo de teste][3]

#### <a name="module-1"></a><span data-ttu-id="938ff-140">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="938ff-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="938ff-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="938ff-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="938ff-142">Limitações</span><span class="sxs-lookup"><span data-stu-id="938ff-142">Limitations</span></span>
<span data-ttu-id="938ff-143">Este é um exemplo muito simples de um serviço Web de clustering.</span><span class="sxs-lookup"><span data-stu-id="938ff-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="938ff-144">Como pode ser visto no código de exemplo acima, nenhuma captura de erro é implementada e o serviço pressupõe que tudo é uma variável contínua (nenhum recurso categórico é permitido), uma vez que o serviço apenas produz valores números no momento da criação do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="938ff-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="938ff-145">Além disso, atualmente o serviço lida com um tamanho de dados limitado, devido à natureza da solicitação/resposta da chamada do serviço Web e ao fato de que o modelo é ajustado sempre que o serviço Web é chamado.</span><span class="sxs-lookup"><span data-stu-id="938ff-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="938ff-146">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="938ff-146">FAQ</span></span>
<span data-ttu-id="938ff-147">Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="938ff-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

