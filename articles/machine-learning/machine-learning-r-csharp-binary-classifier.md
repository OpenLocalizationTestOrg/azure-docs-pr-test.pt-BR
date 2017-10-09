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
# <a name="deprecated-binary-classifier"></a>(preterido) Classificador Binário

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Suponha que você tenha um conjunto de dados e deseje toopredict uma variável dependente binária com base em variáveis independentes de saudação. "Regressão logística" é uma técnica estatística popular usada para essas previsões. Eis variável dependente de saudação binário ou dicotômicas e p é a probabilidade de saudação da presença de característica de saudação de interesse. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Um cenário simples pode ser onde um pesquisador está tentando toopredict se um aluno em potencial é provavelmente tooaccept uma universidade de tooa de oferta de admissão com base nas informações (GPA no ensino médio, família renda, estado residente, sexo). resultado previsto Olá é a probabilidade de saudação do aluno potencial de saudação aceitar a oferta de admissão hello. Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/log_regression) se ajusta Olá dados de toohello do modelo de regressão logística e saídas Olá valor de probabilidade (y) para cada uma das observações Olá nos dados de saudação.  

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Essa saudação do web service oferece prevista valores de variável dependente de saudação com base em variáveis independentes de saudação para todas as observações de saudação. serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgula (,) e as colunas são separadas por ponto e vírgula (;). serviço web de saudação espera 1 linha por vez e espera Olá primeira coluna toobe Olá variável dependente. Um conjunto de dados de exemplo poderia ser assim:

![Dados de amostra][1]

Observações sem uma variável dependente devem ser inseridas como "NA" para y. Olá dados de entrada para Olá acima de conjunto de dados deve ser Olá a seguir cadeia de caracteres: "1; 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, NA; 3; 4". saudação de saída é hello valor previsto para cada uma das linhas de saudação com base em variáveis independentes de saudação. 

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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

De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] extraída de módulos no espaço de trabalho de saudação. Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente. Há 2 partes toothis experimentar: definição de esquema e o modelo de treinamento + de pontuação. módulo primeiro Olá define a estrutura de saudação esperada de dataset entrada hello, onde Olá primeira variável é variável dependente de saudação e variáveis restantes Olá são independentes. segundo módulo de saudação se ajusta a um modelo de regressão logística genérico para dados de entrada hello.    

![Fluxo de teste][2]

#### <a name="module-1"></a>Módulo 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Módulo 2:
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


## <a name="limitations"></a>Limitações
Este é um exemplo muito simples de um serviço Web de classificação binária. Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável binário/contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação deste serviço da Web. Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado. 

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

