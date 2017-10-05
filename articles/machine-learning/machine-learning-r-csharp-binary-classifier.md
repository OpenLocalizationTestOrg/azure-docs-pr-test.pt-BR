---
title: "(preterido) Classificador Binário — Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="2b799-103">(preterido) Classificador Binário</span><span class="sxs-lookup"><span data-stu-id="2b799-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="2b799-104">O Microsoft DataMarket está sendo desativado e essa API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="2b799-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2b799-105">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2b799-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2b799-106">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2b799-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2b799-107">Suponha que você tenha um conjunto de dados e gostaria de prever uma variável dependente binária com base em variáveis independentes.</span><span class="sxs-lookup"><span data-stu-id="2b799-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="2b799-108">"Regressão logística" é uma técnica estatística popular usada para essas previsões.</span><span class="sxs-lookup"><span data-stu-id="2b799-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="2b799-109">Aqui, a variável dependente é binária ou dicotômica, e p é a probabilidade de presença da característica de interesse.</span><span class="sxs-lookup"><span data-stu-id="2b799-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2b799-110">Um cenário simples poderia ser um pesquisador tentar prever se um aluno em potencial provavelmente aceitará uma oferta de entrada de uma universidade com base em informações (GPA no ensino médio, renda familiar, estado de residência, sexo).</span><span class="sxs-lookup"><span data-stu-id="2b799-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="2b799-111">O resultado previsto é a probabilidade do aluno em potencial aceitar sua oferta de admissão.</span><span class="sxs-lookup"><span data-stu-id="2b799-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="2b799-112">Esse [serviço Web](https://datamarket.azure.com/dataset/aml_labs/log_regression) se ajusta ao modelo de regressão logística para os dados e gera o valor de probabilidade (y) para cada uma das observações nos dados.</span><span class="sxs-lookup"><span data-stu-id="2b799-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="2b799-113">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="2b799-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2b799-114">Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="2b799-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="2b799-115">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2b799-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2b799-116">O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – sem qualquer infraestrutura configurada pelo autor do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2b799-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2b799-117">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="2b799-117">Consumption of web service</span></span>
<span data-ttu-id="2b799-118">O serviço Web dá os valores previstos da variável dependente com base em variáveis independentes para todas as observações.</span><span class="sxs-lookup"><span data-stu-id="2b799-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="2b799-119">O serviço Web espera que o usuário final insira seus dados como cadeias de caracteres em que as linhas são separadas por vírgula (,) e as colunas são separadas por ponto e vírgula (;).</span><span class="sxs-lookup"><span data-stu-id="2b799-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="2b799-120">O serviço Web espera 1 linha por vez e espera que a primeira coluna seja a variável dependente.</span><span class="sxs-lookup"><span data-stu-id="2b799-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="2b799-121">Um conjunto de dados de exemplo poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="2b799-121">An example dataset could look like this:</span></span>

![Dados de amostra][1]

<span data-ttu-id="2b799-123">Observações sem uma variável dependente devem ser inseridas como "NA" para y.</span><span class="sxs-lookup"><span data-stu-id="2b799-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="2b799-124">Os dados de entrada para o conjunto de dados acima seria o seguinte: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span><span class="sxs-lookup"><span data-stu-id="2b799-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="2b799-125">O resultado é o valor previsto para cada uma das linhas com base nas variáveis independentes.</span><span class="sxs-lookup"><span data-stu-id="2b799-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="2b799-126">Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="2b799-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2b799-127">Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo estão [aqui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2b799-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2b799-128">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="2b799-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="2b799-129">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2b799-129">Creation of web service</span></span>
> <span data-ttu-id="2b799-130">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2b799-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2b799-131">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2b799-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2b799-132">Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="2b799-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="2b799-133">De dentro do Azure Machine Learning, um novo teste em branco foi criado e dois módulos [Executar Script R][execute-r-script] foram levados ao espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b799-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="2b799-134">Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente.</span><span class="sxs-lookup"><span data-stu-id="2b799-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="2b799-135">Há 2 partes para esse experimento: a definição de esquema e o modelo de treinamento + pontuação.</span><span class="sxs-lookup"><span data-stu-id="2b799-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="2b799-136">O primeiro módulo define a estrutura esperada do conjunto de entrada, em que a primeira variável é a variável dependente e as variáveis restantes são independentes.</span><span class="sxs-lookup"><span data-stu-id="2b799-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="2b799-137">O segundo módulo se encaixa em um modelo de regressão logística genérico para os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="2b799-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Fluxo de teste][2]

#### <a name="module-1"></a><span data-ttu-id="2b799-139">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="2b799-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="2b799-140">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="2b799-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="2b799-141">Limitações</span><span class="sxs-lookup"><span data-stu-id="2b799-141">Limitations</span></span>
<span data-ttu-id="2b799-142">Este é um exemplo muito simples de um serviço Web de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="2b799-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="2b799-143">Como pode ser visto no código de exemplo acima, nenhuma captura de erro é implementada e o serviço pressupõe que tudo é uma variável binária/contínua (nenhum recurso categórico é permitido), uma vez que o serviço produz apenas valores numéricos no momento da criação do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2b799-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="2b799-144">Além disso, atualmente o serviço lida com um tamanho de dados limitado, devido à natureza da solicitação/resposta da chamada do serviço Web e ao fato de que o modelo é ajustado sempre que o serviço Web é chamado.</span><span class="sxs-lookup"><span data-stu-id="2b799-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="2b799-145">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="2b799-145">FAQ</span></span>
<span data-ttu-id="2b799-146">Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2b799-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

