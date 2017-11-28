---
title: "AAA(deprecated) Multivariada de regressão Linear - Azure | Microsoft Docs"
description: "(preterido) Regressão Linear Multivariada"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="84881-103">(preterido) Regressão Linear Multivariada</span><span class="sxs-lookup"><span data-stu-id="84881-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="84881-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="84881-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="84881-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="84881-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="84881-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="84881-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="84881-107">Suponha que você tem um conjunto de dados e seria como tooquickly prever uma variável dependente (y) para cada indivíduo (i) com base em variáveis independentes.</span><span class="sxs-lookup"><span data-stu-id="84881-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="84881-108">A regressão linear é uma técnica estatística popular usada para essas previsões.</span><span class="sxs-lookup"><span data-stu-id="84881-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="84881-109">Aqui Olá variável dependente y é considerado toobe um valor contínuo.</span><span class="sxs-lookup"><span data-stu-id="84881-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="84881-110">Um cenário simples pode ser onde Pesquisador hello está tentando toopredict peso de saudação de um indivíduo (y) com base em sua altura (x).</span><span class="sxs-lookup"><span data-stu-id="84881-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="84881-111">Um cenário mais avançado pode ser onde o Pesquisador de saudação tem informações adicionais para Olá individual (como o peso, sexo, corrida) e tentativas toopredict peso Olá Olá individuais.</span><span class="sxs-lookup"><span data-stu-id="84881-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="84881-112">Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) se ajusta Olá dados de toohello do modelo de regressão linear e saídas Olá valor previsto (y) para cada uma das observações Olá nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="84881-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="84881-113">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="84881-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="84881-114">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="84881-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="84881-115">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="84881-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="84881-116">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="84881-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="84881-117">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="84881-117">Consumption of web service</span></span>
<span data-ttu-id="84881-118">Essa saudação do web service oferece prevista valores de variável dependente de saudação com base em variáveis independentes de saudação para todas as observações de saudação.</span><span class="sxs-lookup"><span data-stu-id="84881-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="84881-119">serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgulas (,) e as colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="84881-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="84881-120">serviço web de saudação espera 1 linha por vez e espera Olá primeira coluna toobe Olá variável dependente.</span><span class="sxs-lookup"><span data-stu-id="84881-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="84881-121">Um conjunto de dados de exemplo poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="84881-121">An example dataset could look like this:</span></span>

![Dados de amostra][1]

<span data-ttu-id="84881-123">Observações sem uma variável dependente devem ser inseridas como "NA" para y.</span><span class="sxs-lookup"><span data-stu-id="84881-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="84881-124">Olá dados de entrada para Olá acima de conjunto de dados deve ser Olá a seguir cadeia de caracteres: "10; 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2: 1, 4, 3; NA".</span><span class="sxs-lookup"><span data-stu-id="84881-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="84881-125">saudação de saída é hello valor previsto para cada uma das linhas de saudação com base em variáveis independentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="84881-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="84881-126">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="84881-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="84881-127">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="84881-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="84881-128">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="84881-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="84881-129">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="84881-129">Creation of web service</span></span>
> <span data-ttu-id="84881-130">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84881-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="84881-131">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="84881-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="84881-132">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="84881-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="84881-133">De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] módulos foram recebidos no espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="84881-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="84881-134">Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente.</span><span class="sxs-lookup"><span data-stu-id="84881-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="84881-135">Há 2 partes toothis experimentar: definição de esquema e o modelo de treinamento + de pontuação.</span><span class="sxs-lookup"><span data-stu-id="84881-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="84881-136">módulo primeiro Olá define a estrutura de saudação esperada de dataset entrada hello, onde Olá primeira variável é variável dependente de saudação e variáveis restantes Olá são independentes.</span><span class="sxs-lookup"><span data-stu-id="84881-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="84881-137">segundo módulo de saudação se ajusta a um modelo de regressão linear genérico para dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="84881-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Fluxo de teste][3]

#### <a name="module-1"></a><span data-ttu-id="84881-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="84881-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="84881-140">Definição de esquema</span><span class="sxs-lookup"><span data-stu-id="84881-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="84881-141">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="84881-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="84881-142">Modelagem de LM</span><span class="sxs-lookup"><span data-stu-id="84881-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="84881-143">Limitações</span><span class="sxs-lookup"><span data-stu-id="84881-143">Limitations</span></span>
<span data-ttu-id="84881-144">Este é um exemplo muito simples de um serviço Web de regressão linear múltipla.</span><span class="sxs-lookup"><span data-stu-id="84881-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="84881-145">Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação desta Web serviço.</span><span class="sxs-lookup"><span data-stu-id="84881-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="84881-146">Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado.</span><span class="sxs-lookup"><span data-stu-id="84881-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="84881-147">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="84881-147">FAQ</span></span>
<span data-ttu-id="84881-148">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="84881-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

