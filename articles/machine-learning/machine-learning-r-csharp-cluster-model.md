---
title: AAA(deprecated) modelo de Cluster - Azure | Microsoft Docs
description: (preterido) Modelo de cluster
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a>(preterido) Modelo de cluster

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Como podemos prever grupos comportamentos dos sistema crédito em ordem tooreduce Olá custos off risco de emissores de cartão de crédito? Como pode podemos definir grupos de características de identificação de funcionários em ordem tooimprove seu desempenho no trabalho? Como o médicos podem classificar pacientes em grupos com base nas características de saudação do seus infecciosas? A princípio, todas essas perguntas podem ser respondidas por meio da análise de cluster.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

A análise de cluster classifica um conjunto de observações em dois ou mais grupos desconhecidos que se excluem mutuamente com base nas combinações de variáveis. finalidade de saudação da análise de cluster é toodiscover um sistema de organizar observações, geralmente as pessoas ou suas características em grupos, onde os membros de grupos de saudação compartilham propriedades em comum. Isso [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) usa Olá metodologia de K-Means, uma técnica normalmente usada de clustering, dados arbitrários de toocluster em grupos. Esse serviço da web usa dados de saudação e número de saudação de k clusters como entrada e produz previsões que Olá k grupos toowhich cada observações pertence. 

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
Esse serviço da web agrupa dados saudação em um conjunto de k grupos e saídas Olá atribuição de grupo para cada linha. serviço web de saudação espera Olá tooinput dados como uma cadeia de caracteres em que linhas são separadas por vírgulas (,) e as colunas são separadas por ponto e vírgula (;). serviço web de saudação espera 1 linha por vez. Um conjunto de dados de exemplo poderia ser assim:

![Dados de amostra][1]

Suponha que Olá usuário quisesse tooseparate esses dados em grupos mutuamente 3. Olá dados de entrada para Olá acima de conjunto de dados seria a seguinte Olá: valor = "10; 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3". saída de Hello é Olá associação de grupo previsto para cada uma das linhas de saudação.

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
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

De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] extraída de módulos no espaço de trabalho de saudação. esquema de saudação de dados foi criada com um simples [Executar Script R][execute-r-script]. Em seguida, o esquema de dados Olá foi vinculado toohello do cluster modelo, criado novamente com um [Executar Script R][execute-r-script]. Em Olá [Executar Script R] [ execute-r-script] usado para o modelo de cluster Olá, serviço da web de saudação, em seguida, utiliza a função hello "k-means", que é predefinida no hello [Executar Script R] [ execute-r-script] de aprendizado de máquina do Azure.    

![Fluxo de teste][3]

#### <a name="module-1"></a>Módulo 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Módulo 2:
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a>Limitações
Este é um exemplo muito simples de um serviço Web de clustering. Como pode ser visto no código de exemplo hello acima, nenhum erro capturando é implementado e Olá serviço considera tudo o que é uma variável contínua (não há recursos categóricos permitidos), como Olá serviço apenas entradas valores numéricos na Olá Olá criação desta Web serviço. Além disso, o serviço Olá atualmente lida com tamanho de dados limitada, devido a natureza de solicitação/resposta toohello do serviço web de saudação do fato de chamada e Olá Olá modelo está sendo ajustar sempre que o serviço web de saudação é chamado. 

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

