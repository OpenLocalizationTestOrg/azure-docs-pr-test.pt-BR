---
title: "(preterido) Previsão: ARIMA (média de movimentação integrada de regressão automática) – Azure | Microsoft Docs"
description: "(preterido) Previsão - Média de Movimentação Integrada de Regressão Automática (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 4f3af41fd8873fdf75c6426fd395351cb41db190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a><span data-ttu-id="87441-103">(preterido) Previsão - Média de Movimentação Integrada de Regressão Automática (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="87441-103">(deprecated) Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>

> [!NOTE]
> <span data-ttu-id="87441-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="87441-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="87441-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="87441-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="87441-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="87441-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>


<span data-ttu-id="87441-107">Isso [service](https://datamarket.azure.com/dataset/aml_labs/arima) implementa previsões de tooproduce de regressão automática integrado movendo médio (ARIMA) com base em dados históricos de saudação fornecidos pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="87441-107">This [service](https://datamarket.azure.com/dataset/aml_labs/arima) implements Autoregressive Integrated Moving Average (ARIMA) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="87441-108">Será Olá demanda para um aumento de produto específico deste ano?</span><span class="sxs-lookup"><span data-stu-id="87441-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="87441-109">Pode, prever Minhas vendas de produto para Olá Natal, para que eu efetivamente pode planejar o inventário do meu?</span><span class="sxs-lookup"><span data-stu-id="87441-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="87441-110">Modelos de previsão são tooaddress apt essas perguntas.</span><span class="sxs-lookup"><span data-stu-id="87441-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="87441-111">Considerando Olá após os dados, esses modelos examinar tendências ocultas e tendências do futuro periodicidade toopredict.</span><span class="sxs-lookup"><span data-stu-id="87441-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="87441-112">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="87441-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="87441-113">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="87441-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="87441-114">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="87441-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="87441-115">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="87441-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="87441-116">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="87441-116">Consumption of web service</span></span>
<span data-ttu-id="87441-117">Este serviço aceita 4 argumentos e calcula as previsões ARIMA hello.</span><span class="sxs-lookup"><span data-stu-id="87441-117">This service accepts 4 arguments and calculates hello ARIMA forecasts.</span></span>
<span data-ttu-id="87441-118">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="87441-118">hello input arguments are:</span></span>

* <span data-ttu-id="87441-119">Frequência – indica a frequência de saudação de dados brutos de saudação (diariamente/semanalmente/mês/trimestre/anual).</span><span class="sxs-lookup"><span data-stu-id="87441-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="87441-120">Horizonte - período de tempo de previsão do futuro.</span><span class="sxs-lookup"><span data-stu-id="87441-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="87441-121">Data - adicionar na nova série de tempo Olá dados de tempo.</span><span class="sxs-lookup"><span data-stu-id="87441-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="87441-122">Valor - adicionar em valores de dados de série de tempo novo de saudação.</span><span class="sxs-lookup"><span data-stu-id="87441-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="87441-123">saída de saudação do serviço de saudação é Olá calculados os valores de previsão.</span><span class="sxs-lookup"><span data-stu-id="87441-123">hello output of hello service is hello calculated forecast values.</span></span> 

<span data-ttu-id="87441-124">A amostrada de entrada poderia ser:</span><span class="sxs-lookup"><span data-stu-id="87441-124">Sample input could be:</span></span> 

* <span data-ttu-id="87441-125">Frequência - 12</span><span class="sxs-lookup"><span data-stu-id="87441-125">Frequency - 12</span></span>
* <span data-ttu-id="87441-126">Horizonte - 12</span><span class="sxs-lookup"><span data-stu-id="87441-126">Horizon - 12</span></span>
* <span data-ttu-id="87441-127">Data - 15/1/2012;15/2/2012;15/3/2012;15/4/2012;15/5/2012;15/6/2012;15/7/2012;15/8/2012;15/9/2012;15/10/2012;15/11/2012;15/12/2012; 15/1/2013;15/2/2013;15/3/2013;15/4/2013;15/5/2013;15/6/2013;15/7/2013;15/8/2013;15/9/2013;15/10/2013;15/11/2013;15/12/2013; 15/1/2014;15/2/2014;15/3/2014;15/4/2014;15/5/2014;15/6/2014;15/7/2014;15/8/2014;15/9/2014</span><span class="sxs-lookup"><span data-stu-id="87441-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="87441-128">Valor - 3.479;3,68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3,51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="87441-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="87441-129">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="87441-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="87441-130">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="87441-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="87441-131">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="87441-131">Starting C# code for web service consumption:</span></span>
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
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a><span data-ttu-id="87441-132">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="87441-132">Creation of web service</span></span>
> <span data-ttu-id="87441-133">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="87441-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="87441-134">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="87441-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="87441-135">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="87441-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="87441-136">De dentro do Azure Machine Learning, um novo teste em branco foi criado.</span><span class="sxs-lookup"><span data-stu-id="87441-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="87441-137">Os dados de entrada de amostra foram carregados com um esquema de dados predefinido.</span><span class="sxs-lookup"><span data-stu-id="87441-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="87441-138">Esquema de dados toohello vinculado é um [Executar Script R] [ execute-r-script] módulo, que gera o modelo de previsão de ARIMA hello usando 'auto.arima' e 'previsão' funções de R.</span><span class="sxs-lookup"><span data-stu-id="87441-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module, which generates hello ARIMA forecasting model by using ‘auto.arima’ and ‘forecast’ functions from R.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="87441-139">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="87441-139">Experiment flow:</span></span>
![Criar espaço de trabalho][2]

#### <a name="module-1"></a><span data-ttu-id="87441-141">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="87441-141">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Criar espaço de trabalho][3]    

#### <a name="module-2"></a><span data-ttu-id="87441-143">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="87441-143">Module 2:</span></span>
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="87441-144">Limitações</span><span class="sxs-lookup"><span data-stu-id="87441-144">Limitations</span></span>
<span data-ttu-id="87441-145">Este é um exemplo muito simples para a previsão ARIMA.</span><span class="sxs-lookup"><span data-stu-id="87441-145">This is a very simple example for ARIMA forecasting.</span></span> <span data-ttu-id="87441-146">Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e serviço Olá presume que todas as variáveis de saudação são valores contínuos positivo e frequência Olá deve ser um inteiro maior que 1.</span><span class="sxs-lookup"><span data-stu-id="87441-146">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="87441-147">comprimento de saudação de vetores de valor de data e Olá deve Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="87441-147">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="87441-148">variável de data de saudação deve aderir toohello formato "mm/dd/aaaa'.</span><span class="sxs-lookup"><span data-stu-id="87441-148">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="87441-149">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="87441-149">FAQ</span></span>
<span data-ttu-id="87441-150">Para perguntas frequentes sobre o consumo do serviço web de saudação ou toomarketplace de publicação, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="87441-150">For frequently asked questions on consumption of hello web service or publishing toomarketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

