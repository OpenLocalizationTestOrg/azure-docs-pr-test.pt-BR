---
title: "AAA(deprecated) distribuição Binomial Suite - Azure | Microsoft Docs"
description: "(preterido) Pacote de distribuição binomial"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
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
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a>(preterido) Pacote de distribuição binomial

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Olá Suite distribuição Binomial é um conjunto de serviços da web de exemplo ([Binomial gerador](https://datamarket.azure.com/dataset/aml_labs/bdg5), [probabilidade Calculadora](https://datamarket.azure.com/dataset/aml_labs/bdp4), [quantil Calculadora](https://datamarket.azure.com/dataset/aml_labs/bdq5)) que ajudam a gerar e Lidando com distribuições binomial. Olá serviços permitem gerar uma sequência de distribuição binomial de qualquer tamanho, calculando quantis de dado probabilidade e a probabilidade de cálculo de um determinado quantil. Cada um dos serviços de saudação emite saídas diferentes com base no serviço de saudação selecionado (consulte a descrição abaixo). Olá distribuição Binomial Suite baseia-se em Olá R funções qbinom, rbinom e pbinom, que são incluídos no pacote de estatísticas de R hello. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Esses serviços da web podem ser consumidos por usuários – potencialmente diretamente no marketplace hello, por meio de um aplicativo móvel, por meio de um site, ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo – nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação é necessária.
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Olá distribuição Binomial Suite inclui Olá 3 serviços a seguir.

### <a name="binomial-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição binomial
Este serviço aceita 4 argumentos de uma distribuição normal e calcula o quantil Olá associado.
argumentos de entrada Hello são:

* p - uma única probabilidade agregada de várias tentativas.  
* tamanho - número de saudação de tentativas.
* PROB - probabilidade de saudação de sucesso em uma versão de avaliação.
* Lado - L para o lado inferior de saudação da distribuição hello, U para o lado superior de saudação da distribuição de saudação. 

saída de saudação do serviço de saudação é quantil Olá calculado que está associado a saudação considerando a probabilidade.

### <a name="binomial-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição binomial
Este serviço aceita 4 argumentos de uma distribuição binomial e calcula a probabilidade de saudação associada.
argumentos de entrada Hello são:

* q - um único quantil de um evento com distribuição binomial. 
* tamanho - número de saudação de tentativas.
* PROB - probabilidade de saudação de sucesso em uma versão de avaliação.
* lado - L para o lado inferior de saudação da distribuição hello, U lado superior Olá distribuição Olá da ou E que seja igual tooa único número de sucessos.

saída de saudação do serviço de saudação é a probabilidade de Olá calculado que está associada a saudação fornecida quantil.

### <a name="binomial-distribution-generator"></a>Gerador de distribuição binomial
Este serviço aceita três argumentos de uma distribuição binomial e gera uma sequência aleatória de números distribuídos binomialmente. Olá argumentos a seguir devem ser fornecidos tooit na solicitação de saudação:

* n - número de observações. 
* tamanho – número de tentativas.
* prob – probabilidade de sucesso.

saída de saudação do serviço de saudação é uma sequência de comprimento de n com uma distribuição binomial com base nos argumentos de tamanho e prob hello.

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (aplicativos de exemplo estão aqui: [gerador](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [probabilidade Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [quantil Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
### <a name="binomial-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição binomial
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição binomial
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a>Gerador de distribuição binomial
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
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
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a>Calculadora de quantil de distribuição binomial
![Criar espaço de trabalho][4]

#### <a name="module-1"></a>Módulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>Módulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a>Calculadora de probabilidade de distribuição binomial
![Criar espaço de trabalho][5]

#### <a name="module-1"></a>Módulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>Módulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a>Gerador de distribuição binomial
![Criar espaço de trabalho][6]

#### <a name="module-1"></a>Módulo 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>Módulo 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Limitações
Estes são exemplos muito simples em torno de distribuição binomial de saudação. Como pode ser visto no código de exemplo hello acima, capturando pouco de erro é implementado.

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

