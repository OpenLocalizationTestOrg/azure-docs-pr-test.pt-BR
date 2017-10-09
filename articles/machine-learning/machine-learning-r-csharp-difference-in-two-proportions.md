---
title: "AAA(deprecated) diferença proporções teste - o Azure | Microsoft Docs"
description: "(preterido) Diferença no teste de proporções"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="65ca9-103">(preterido) Diferença no teste de proporções</span><span class="sxs-lookup"><span data-stu-id="65ca9-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="65ca9-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="65ca9-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="65ca9-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="65ca9-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="65ca9-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="65ca9-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="65ca9-107">Duas proporções são estatisticamente diferentes?</span><span class="sxs-lookup"><span data-stu-id="65ca9-107">Are two proportions statistically different?</span></span> <span data-ttu-id="65ca9-108">Suponha que um usuário deseja toocompare dois filmes toodetermine se um filme tem uma impacto significativamente maior proporção de 'gosta' quando comparado a outros toohello.</span><span class="sxs-lookup"><span data-stu-id="65ca9-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="65ca9-109">Com um grande exemplo, pode haver uma diferença estatisticamente significativa entre as proporções de saudação 0,50 e 0.51.</span><span class="sxs-lookup"><span data-stu-id="65ca9-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="65ca9-110">Com uma pequena amostra, pode não haver suficiente toodetermine dados se essas proporções são realmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="65ca9-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="65ca9-111">Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/prop_test) conduz um teste de hipóteses de diferença de saudação em dois proporções com base na entrada do usuário do número de saudação de êxitos e número total de saudação de tentativas para grupos de comparação de saudação 2.</span><span class="sxs-lookup"><span data-stu-id="65ca9-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="65ca9-112">Em uma situação, esse serviço da web poderia ser chamado de dentro de um aplicativo de comparação de filme, informando ao usuário Olá se um dos filmes Olá é 'gostou' com mais frequência do que outros, Olá com base na classificação de filme.</span><span class="sxs-lookup"><span data-stu-id="65ca9-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="65ca9-113">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="65ca9-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="65ca9-114">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="65ca9-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="65ca9-115">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="65ca9-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="65ca9-116">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="65ca9-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="65ca9-117">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="65ca9-117">Consumption of web service</span></span>
<span data-ttu-id="65ca9-118">Esse serviço aceita quatro argumentos e forma uma hipótese de teste de proporções.</span><span class="sxs-lookup"><span data-stu-id="65ca9-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="65ca9-119">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="65ca9-119">hello input arguments are:</span></span>

* <span data-ttu-id="65ca9-120">Successes1 - número de eventos de sucesso na amostra 1.</span><span class="sxs-lookup"><span data-stu-id="65ca9-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="65ca9-121">Successes2 - número de eventos de sucesso na amostra 2.</span><span class="sxs-lookup"><span data-stu-id="65ca9-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="65ca9-122">Total1 - tamanho da amostra 1.</span><span class="sxs-lookup"><span data-stu-id="65ca9-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="65ca9-123">Total2 - tamanho da amostra 2.</span><span class="sxs-lookup"><span data-stu-id="65ca9-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="65ca9-124">saída de saudação do serviço de saudação é resultado de saudação da hipótese Olá juntamente com hello chi-square estatística, df, p-valor de teste e proporção em limites de 1/2 e o intervalo de confiança de exemplo.</span><span class="sxs-lookup"><span data-stu-id="65ca9-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="65ca9-125">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="65ca9-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="65ca9-126">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="65ca9-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="65ca9-127">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="65ca9-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="65ca9-128">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="65ca9-128">Creation of web service</span></span>
> <span data-ttu-id="65ca9-129">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="65ca9-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="65ca9-130">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="65ca9-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="65ca9-131">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="65ca9-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="65ca9-132">De dentro do Azure Machine Learning, uma nova experiência em branco foi criada com dois módulos [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="65ca9-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="65ca9-133">Módulo primeiro Olá Olá esquema de dados é definido, enquanto o segundo módulo de saudação usa o comando de prop.test Olá no teste de hipóteses R tooperform Olá para 2 proporções.</span><span class="sxs-lookup"><span data-stu-id="65ca9-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="65ca9-134">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="65ca9-134">Experiment flow:</span></span>
![Fluxo de teste][2]

#### <a name="module-1"></a><span data-ttu-id="65ca9-136">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="65ca9-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="65ca9-137">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="65ca9-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="65ca9-138">Limitações</span><span class="sxs-lookup"><span data-stu-id="65ca9-138">Limitations</span></span>
<span data-ttu-id="65ca9-139">Este é um exemplo muito simples para um teste de diferença em duas proporções.</span><span class="sxs-lookup"><span data-stu-id="65ca9-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="65ca9-140">Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e serviço Olá pressupõe que todas as variáveis de saudação são contínuas.</span><span class="sxs-lookup"><span data-stu-id="65ca9-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="65ca9-141">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="65ca9-141">FAQ</span></span>
<span data-ttu-id="65ca9-142">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="65ca9-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

