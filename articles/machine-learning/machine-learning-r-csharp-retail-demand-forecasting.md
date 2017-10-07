---
title: "AAA(deprecated) previsão - ETS + STL - Azure | Microsoft Docs"
description: "(preterido) Previsão – ETS + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
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
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>(preterido) Previsão – ETS + STL

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implementa Decomposição de tendência sazonais (STL) e suavização exponencial (ETS) previsões de tooproduce modelos com base em dados de histórico Olá fornecidos pelo usuário hello. Será Olá demanda para um aumento de produto específico deste ano? Pode, prever Minhas vendas de produto para Olá Natal, para que eu efetivamente pode planejar o inventário do meu? Modelos de previsão são tooaddress apt essas perguntas. Considerando Olá após os dados, esses modelos examinar tendências ocultas e tendências do futuro periodicidade toopredict. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Este serviço aceita 4 argumentos e calcula as previsões de saudação.
argumentos de entrada Hello são:

* Frequência – indica a frequência de saudação de dados brutos de saudação (diariamente/semanalmente/mês/trimestre/anual).
* Horizonte - período de tempo de previsão do futuro.
* Data - adicionar na nova série de tempo Olá dados de tempo.
* Valor - adicionar em valores de dados de série de tempo novo de saudação.

saída de saudação do serviço de saudação é Olá calculados os valores de previsão.

A amostrada de entrada poderia ser: 

* Frequência - 12
* Horizonte - 12
* Data - 15/1/2012;15/2/2012;15/3/2012;15/4/2012;15/5/2012;15/6/2012;15/7/2012;15/8/2012;15/9/2012;15/10/2012;15/11/2012;15/12/2012; 15/1/2013;15/2/2013;15/3/2013;15/4/2013;15/5/2013;15/6/2013;15/7/2013;15/8/2013;15/9/2013;15/10/2013;15/11/2013;15/12/2013; 15/1/2014;15/2/2014;15/3/2014;15/4/2014;15/5/2014;15/6/2014;15/7/2014;15/8/2014;15/9/2014
* Valor - 3.479;3,68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3,51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
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
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

De dentro do Azure Machine Learning, um novo teste em branco foi criado. Os dados de entrada de amostra foram carregados com um esquema de dados predefinido. Esquema de dados toohello vinculado é um [Executar Script R] [ execute-r-script] módulo, que gera STL e ETS modelos de previsão usando 'stl', 'ets' e 'previsão' funções de R. 

### <a name="experiment-flow"></a>Fluxo de teste:
![Fluxo de teste][2]

#### <a name="module-1"></a>Módulo 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Dados de amostra][3]    

#### <a name="module-2"></a>Módulo 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Limitações
Este é um exemplo muito simples para a previsão ETS + STL. Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e serviço Olá presume que todas as variáveis de saudação são valores contínuos positivo e frequência Olá deve ser um inteiro maior que 1. Hello comprimento dos vetores de valor de data e Olá deve ser Olá mesmo e comprimento de saudação do MTS Olá deve ser maior que 2 * frequência. variável de data de saudação deve aderir toohello formato "mm/dd/aaaa'.

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

