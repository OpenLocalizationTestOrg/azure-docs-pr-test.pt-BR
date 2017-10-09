---
title: "AAA(deprecated) classificador binário - Azure | Microsoft Docs"
description: "(preterido) Classificador Binário"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="a7685-103">(preterido) Classificador Binário</span><span class="sxs-lookup"><span data-stu-id="a7685-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="a7685-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="a7685-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a7685-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a7685-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a7685-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a7685-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a7685-107">Suponha que você tenha um conjunto de dados e deseje toopredict uma variável dependente binária com base em variáveis independentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="a7685-108">"Regressão logística" é uma técnica estatística popular usada para essas previsões.</span><span class="sxs-lookup"><span data-stu-id="a7685-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="a7685-109">Eis variável dependente de saudação binário ou dicotômicas e p é a probabilidade de saudação da presença de característica de saudação de interesse.</span><span class="sxs-lookup"><span data-stu-id="a7685-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a7685-110">Um cenário simples pode ser onde um pesquisador está tentando toopredict se um aluno em potencial é provavelmente tooaccept uma universidade de tooa de oferta de admissão com base nas informações (GPA no ensino médio, família renda, estado residente, sexo).</span><span class="sxs-lookup"><span data-stu-id="a7685-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="a7685-111">resultado previsto Olá é a probabilidade de saudação do aluno potencial de saudação aceitar a oferta de admissão hello.</span><span class="sxs-lookup"><span data-stu-id="a7685-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="a7685-112">Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/log_regression) se ajusta Olá dados de toohello do modelo de regressão logística e saídas Olá valor de probabilidade (y) para cada uma das observações Olá nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="a7685-113">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="a7685-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a7685-114">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="a7685-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="a7685-115">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="a7685-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a7685-116">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a7685-117">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="a7685-117">Consumption of web service</span></span>
<span data-ttu-id="a7685-118">Essa saudação do web service oferece prevista valores de variável dependente de saudação com base em variáveis independentes de saudação para todas as observações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="a7685-119">serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgula (,) e as colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="a7685-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="a7685-120">serviço web de saudação espera 1 linha por vez e espera Olá primeira coluna toobe Olá variável dependente.</span><span class="sxs-lookup"><span data-stu-id="a7685-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="a7685-121">Um conjunto de dados de exemplo poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="a7685-121">An example dataset could look like this:</span></span>

![Dados de amostra][1]

<span data-ttu-id="a7685-123">Observações sem uma variável dependente devem ser inseridas como "NA" para y.</span><span class="sxs-lookup"><span data-stu-id="a7685-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="a7685-124">Olá dados de entrada para Olá acima de conjunto de dados deve ser Olá a seguir cadeia de caracteres: "1; 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="a7685-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="a7685-125">saudação de saída é hello valor previsto para cada uma das linhas de saudação com base em variáveis independentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="a7685-126">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="a7685-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a7685-127">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a7685-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a7685-128">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="a7685-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="a7685-129">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="a7685-129">Creation of web service</span></span>
> <span data-ttu-id="a7685-130">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a7685-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a7685-131">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a7685-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a7685-132">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="a7685-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="a7685-133">De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] extraída de módulos no espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a7685-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="a7685-134">Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente.</span><span class="sxs-lookup"><span data-stu-id="a7685-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="a7685-135">Há 2 partes toothis experimentar: definição de esquema e o modelo de treinamento + de pontuação.</span><span class="sxs-lookup"><span data-stu-id="a7685-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="a7685-136">módulo primeiro Olá define a estrutura de saudação esperada de dataset entrada hello, onde Olá primeira variável é variável dependente de saudação e variáveis restantes Olá são independentes.</span><span class="sxs-lookup"><span data-stu-id="a7685-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="a7685-137">segundo módulo de saudação se ajusta a um modelo de regressão logística genérico para dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="a7685-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Fluxo de teste][2]

#### <a name="module-1"></a><span data-ttu-id="a7685-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="a7685-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="a7685-140">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="a7685-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="a7685-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="a7685-141">Limitations</span></span>
<span data-ttu-id="a7685-142">Este é um exemplo muito simples de um serviço Web de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="a7685-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="a7685-143">Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável binário/contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação deste serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="a7685-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="a7685-144">Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado.</span><span class="sxs-lookup"><span data-stu-id="a7685-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="a7685-145">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="a7685-145">FAQ</span></span>
<span data-ttu-id="a7685-146">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a7685-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

