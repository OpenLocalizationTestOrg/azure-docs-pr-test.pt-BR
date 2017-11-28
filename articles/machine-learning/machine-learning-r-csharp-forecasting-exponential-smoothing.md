---
title: "(preterido) Previsão — Ajuste exponencial — Azure | Microsoft Docs"
description: "(preterido) Serviço Web: Suavização exponencial da previsão"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 736d5d4adb8ecfd1e3372d273b64917f4a2e76ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="24d34-103">(preterido) Previsão — Ajuste exponencial</span><span class="sxs-lookup"><span data-stu-id="24d34-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="24d34-104">O Microsoft DataMarket está sendo desativado e essa API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="24d34-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="24d34-105">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="24d34-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="24d34-106">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="24d34-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="24d34-107">Este [serviço Web](https://datamarket.azure.com/dataset/aml_labs/ets) implementa o Modelo de ajuste exponencial (ETS) para produzir previsões com base nos dados históricos fornecidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="24d34-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements the Exponential Smoothing model (ETS) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="24d34-108">A demanda de um produto específico aumentará neste ano?</span><span class="sxs-lookup"><span data-stu-id="24d34-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="24d34-109">Posso prever as vendas do meu produto para a temporada de Natal para que eu possa planejar efetivamente meu estoque?</span><span class="sxs-lookup"><span data-stu-id="24d34-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="24d34-110">Modelos de previsão são adequados para responder a essas perguntas.</span><span class="sxs-lookup"><span data-stu-id="24d34-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="24d34-111">Considerando os dados passados, esses modelos examinam tendências ocultas e a sazonalidade para prever tendências futuras.</span><span class="sxs-lookup"><span data-stu-id="24d34-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="24d34-112">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="24d34-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="24d34-113">Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="24d34-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="24d34-114">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="24d34-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="24d34-115">O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – sem qualquer infraestrutura configurada pelo autor do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="24d34-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="24d34-116">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="24d34-116">Consumption of web service</span></span>
<span data-ttu-id="24d34-117">Este serviço aceita quatro argumentos e calcula as previsões ETS.</span><span class="sxs-lookup"><span data-stu-id="24d34-117">This service accepts 4 arguments and calculates the ETS forecasts.</span></span>
<span data-ttu-id="24d34-118">Os argumentos de entrada são:</span><span class="sxs-lookup"><span data-stu-id="24d34-118">The input arguments are:</span></span>

* <span data-ttu-id="24d34-119">Frequência - indica a frequência dos dados brutos (diários/semanais/mensais/trimestrais/anuais).</span><span class="sxs-lookup"><span data-stu-id="24d34-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="24d34-120">Horizonte - período de tempo de previsão do futuro.</span><span class="sxs-lookup"><span data-stu-id="24d34-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="24d34-121">Data - adicionar novos dados de série de tempo para o tempo.</span><span class="sxs-lookup"><span data-stu-id="24d34-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="24d34-122">Valor - adicionar os novos valores de dados de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="24d34-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="24d34-123">A saída do serviço são os valores de previsão calculados.</span><span class="sxs-lookup"><span data-stu-id="24d34-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="24d34-124">A amostrada de entrada poderia ser:</span><span class="sxs-lookup"><span data-stu-id="24d34-124">Sample input could be:</span></span> 

* <span data-ttu-id="24d34-125">Frequência - 12</span><span class="sxs-lookup"><span data-stu-id="24d34-125">Frequency - 12</span></span>
* <span data-ttu-id="24d34-126">Horizonte - 12</span><span class="sxs-lookup"><span data-stu-id="24d34-126">Horizon - 12</span></span>
* <span data-ttu-id="24d34-127">Data - 15/1/2012;15/2/2012;15/3/2012;15/4/2012;15/5/2012;15/6/2012;15/7/2012;15/8/2012;15/9/2012;15/10/2012;15/11/2012;15/12/2012; 15/1/2013;15/2/2013;15/3/2013;15/4/2013;15/5/2013;15/6/2013;15/7/2013;15/8/2013;15/9/2013;15/10/2013;15/11/2013;15/12/2013; 15/1/2014;15/2/2014;15/3/2014;15/4/2014;15/5/2014;15/6/2014;15/7/2014;15/8/2014;15/9/2014</span><span class="sxs-lookup"><span data-stu-id="24d34-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="24d34-128">Valor - 3.479;3,68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3,51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="24d34-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="24d34-129">Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="24d34-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="24d34-130">Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo estão [aqui](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="24d34-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="24d34-131">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="24d34-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="24d34-132">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="24d34-132">Creation of web service</span></span>
> <span data-ttu-id="24d34-133">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="24d34-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="24d34-134">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="24d34-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="24d34-135">Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="24d34-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="24d34-136">De dentro do Azure Machine Learning, um novo teste em branco foi criado.</span><span class="sxs-lookup"><span data-stu-id="24d34-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="24d34-137">Os dados de entrada de amostra foram carregados com um esquema de dados predefinido.</span><span class="sxs-lookup"><span data-stu-id="24d34-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="24d34-138">Vinculado ao esquema de dados está um módulo de [Executar Script R][execute-r-script] que gera o modelo de previsão ETS usando as funções “ets” e “forecast” de R.</span><span class="sxs-lookup"><span data-stu-id="24d34-138">Linked to the data schema is an [Execute R Script][execute-r-script] module that generates the ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Fluxo de teste][2]

#### <a name="module-1"></a><span data-ttu-id="24d34-140">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="24d34-140">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Exemplo de dados][3]    

#### <a name="module-2"></a><span data-ttu-id="24d34-142">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="24d34-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="24d34-143">Limitações</span><span class="sxs-lookup"><span data-stu-id="24d34-143">Limitations</span></span>
<span data-ttu-id="24d34-144">Este é um exemplo muito simples para a previsão ETS.</span><span class="sxs-lookup"><span data-stu-id="24d34-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="24d34-145">Como se pode ver no código de exemplo acima, nenhuma captura de erro é implementada e o serviço presume que todas as variáveis são valores contínuos/positivos e a frequência deve ser um inteiro maior que 1.</span><span class="sxs-lookup"><span data-stu-id="24d34-145">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="24d34-146">Os vetores de data e valor devem ter o mesmo tamanho.</span><span class="sxs-lookup"><span data-stu-id="24d34-146">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="24d34-147">A variável de data deve seguir o formato 'mm/dd/aaaa'.</span><span class="sxs-lookup"><span data-stu-id="24d34-147">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="24d34-148">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="24d34-148">FAQ</span></span>
<span data-ttu-id="24d34-149">Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="24d34-149">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

