---
title: "AAA(deprecated) distribuição Normal Suite de serviço Web - Azure | Microsoft Docs"
description: "(preterido) Pacote de serviço Web de distribuição normal"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a>(preterido) Pacote de distribuição normal

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Olá Suite distribuição Normal é um conjunto de serviços da web de exemplo ([gerador](https://datamarket.azure.com/dataset/aml_labs/ndg7), [quantil Calculadora](https://datamarket.azure.com/dataset/aml_labs/ndq5), [probabilidade Calculadora](https://datamarket.azure.com/dataset/aml_labs/ndp5)) que ajudam na geração e manipulação distribuições normais. Serviços de saudação permitem gerar uma sequência de distribuição normal de qualquer tamanho, calculando quantis de uma determinada probabilidade e calcular a probabilidade de um determinado quantil. Cada um dos serviços de saudação emite saídas diferentes com base no serviço de saudação selecionado (consulte a descrição abaixo). Olá distribuição Normal Suite baseia-se em Olá R funções qnorm, rnorm e pnorm, que são incluídos no pacote de estatísticas de R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Olá distribuição Normal Suite inclui Olá 3 serviços a seguir.

### <a name="normal-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição normal
Este serviço aceita 4 argumentos de uma distribuição normal e calcula o quantil Olá associado.

argumentos de entrada Hello são:

* p - uma única probabilidade de um evento com distribuição normal. 
* Média - média de uma distribuição normal de saudação.
* SD - Olá desvio padrão da distribuição normal. 
* Lado - L para o lado inferior de saudação da distribuição hello e U para o lado superior de saudação da distribuição de saudação.

saída de saudação do serviço de saudação é quantil Olá calculado que está associado a saudação considerando a probabilidade.

### <a name="normal-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição normal
Este serviço aceita 4 argumentos de uma distribuição normal e calcula a probabilidade de saudação associada.

argumentos de entrada Hello são:

* q - um único quantil de um evento com distribuição normal. 
* Média - média de uma distribuição normal de saudação.
* SD - Olá desvio padrão da distribuição normal. 
* Lado - L para o lado inferior de saudação da distribuição hello e U para o lado superior de saudação da distribuição de saudação.

saída de saudação do serviço de saudação é a probabilidade de Olá calculado que está associada a saudação fornecida quantil.

### <a name="normal-distribution-generator"></a>Gerador de distribuição normal
Este serviço aceita três argumentos de uma distribuição normal e gera uma sequência aleatória de números distribuídos normalmente. Olá argumentos a seguir devem ser fornecidos tooit na solicitação de saudação:

* n - número de Olá de observações. 
* Média - média de uma distribuição normal de saudação.
* SD - Olá desvio padrão da distribuição normal. 

saída de saudação do serviço de saudação é uma sequência de comprimento de n com uma distribuição normal com base nos argumentos de média e sd hello.

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (aplicativos de exemplo estão aqui: [gerador](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [probabilidade Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [quantil Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
### <a name="normal-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição normal
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição normal
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a>Gerador de distribuição normal
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). 
> 
> 

Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.

### <a name="normal-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição normal
Fluxo de teste:

![Fluxo de teste][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição normal
Fluxo de teste:

![Fluxo de teste][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a>Gerador de distribuição normal
Fluxo de teste:

![Fluxo de teste][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Limitações
Estes são exemplos muito simples ao redor Olá uma distribuição normal. Como pode ser visto no código de exemplo hello acima, capturando pouco de erro é implementado.

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

