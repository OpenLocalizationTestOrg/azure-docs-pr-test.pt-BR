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
# <a name="deprecated-difference-in-proportions-test"></a>(preterido) Diferença no teste de proporções

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Duas proporções são estatisticamente diferentes? Suponha que um usuário deseja toocompare dois filmes toodetermine se um filme tem uma impacto significativamente maior proporção de 'gosta' quando comparado a outros toohello. Com um grande exemplo, pode haver uma diferença estatisticamente significativa entre as proporções de saudação 0,50 e 0.51. Com uma pequena amostra, pode não haver suficiente toodetermine dados se essas proporções são realmente diferentes. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/prop_test) conduz um teste de hipóteses de diferença de saudação em dois proporções com base na entrada do usuário do número de saudação de êxitos e número total de saudação de tentativas para grupos de comparação de saudação 2. Em uma situação, esse serviço da web poderia ser chamado de dentro de um aplicativo de comparação de filme, informando ao usuário Olá se um dos filmes Olá é 'gostou' com mais frequência do que outros, Olá com base na classificação de filme.

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Esse serviço aceita quatro argumentos e forma uma hipótese de teste de proporções.

argumentos de entrada Hello são:

* Successes1 - número de eventos de sucesso na amostra 1.
* Successes2 - número de eventos de sucesso na amostra 2.
* Total1 - tamanho da amostra 1.
* Total2 - tamanho da amostra 2.

saída de saudação do serviço de saudação é resultado de saudação da hipótese Olá juntamente com hello chi-square estatística, df, p-valor de teste e proporção em limites de 1/2 e o intervalo de confiança de exemplo.

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
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


## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

De dentro do Azure Machine Learning, uma nova experiência em branco foi criada com dois módulos [Executar Script R][execute-r-script]. Módulo primeiro Olá Olá esquema de dados é definido, enquanto o segundo módulo de saudação usa o comando de prop.test Olá no teste de hipóteses R tooperform Olá para 2 proporções. 

### <a name="experiment-flow"></a>Fluxo de teste:
![Fluxo de teste][2]

#### <a name="module-1"></a>Módulo 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Módulo 2:
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


## <a name="limitations"></a>Limitações
Este é um exemplo muito simples para um teste de diferença em duas proporções. Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e serviço Olá pressupõe que todas as variáveis de saudação são contínuas.

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

