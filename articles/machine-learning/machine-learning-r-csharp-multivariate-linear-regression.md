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
# <a name="deprecated-multivariate-linear-regression"></a>(preterido) Regressão Linear Multivariada

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Suponha que você tem um conjunto de dados e seria como tooquickly prever uma variável dependente (y) para cada indivíduo (i) com base em variáveis independentes. A regressão linear é uma técnica estatística popular usada para essas previsões. Aqui Olá variável dependente y é considerado toobe um valor contínuo.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Um cenário simples pode ser onde Pesquisador hello está tentando toopredict peso de saudação de um indivíduo (y) com base em sua altura (x). Um cenário mais avançado pode ser onde o Pesquisador de saudação tem informações adicionais para Olá individual (como o peso, sexo, corrida) e tentativas toopredict peso Olá Olá individuais. Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) se ajusta Olá dados de toohello do modelo de regressão linear e saídas Olá valor previsto (y) para cada uma das observações Olá nos dados de saudação.

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Essa saudação do web service oferece prevista valores de variável dependente de saudação com base em variáveis independentes de saudação para todas as observações de saudação. serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgulas (,) e as colunas são separadas por ponto e vírgula (;). serviço web de saudação espera 1 linha por vez e espera Olá primeira coluna toobe Olá variável dependente. Um conjunto de dados de exemplo poderia ser assim:

![Dados de amostra][1]

Observações sem uma variável dependente devem ser inseridas como "NA" para y. Olá dados de entrada para Olá acima de conjunto de dados deve ser Olá a seguir cadeia de caracteres: "10; 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2: 1, 4, 3; NA". saudação de saída é hello valor previsto para cada uma das linhas de saudação com base em variáveis independentes de saudação. 

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
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




## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] módulos foram recebidos no espaço de trabalho de saudação. Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente. Há 2 partes toothis experimentar: definição de esquema e o modelo de treinamento + de pontuação. módulo primeiro Olá define a estrutura de saudação esperada de dataset entrada hello, onde Olá primeira variável é variável dependente de saudação e variáveis restantes Olá são independentes. segundo módulo de saudação se ajusta a um modelo de regressão linear genérico para dados de entrada hello.  

![Fluxo de teste][3]

#### <a name="module-1"></a>Módulo 1:
#### <a name="schema-definition"></a>Definição de esquema
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>Módulo 2:
#### <a name="lm-modeling"></a>Modelagem de LM
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

## <a name="limitations"></a>Limitações
Este é um exemplo muito simples de um serviço Web de regressão linear múltipla. Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação desta Web serviço. Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado. 

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

