---
title: "(preterido) Regressão Linear Multivariada - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>(preterido) Regressão Linear Multivariada

> [!NOTE]
> O Microsoft DataMarket está sendo desativado e essa API foi preterida. 
> 
> Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com). Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).

Suponha que você tenha um conjunto de dados e gostaria de prever rapidamente uma variável dependente (y) para cada indivíduo (i) com base em outras variáveis independentes. A regressão linear é uma técnica estatística popular usada para essas previsões. Aqui, a variável dependente y é considerada um valor contínuo.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Um cenário simples poderia ser um em que o pesquisador estivesse tentando prever o peso de um indivíduo (y) com base em sua altura (x). Um cenário mais avançado poderia ser um em que o Pesquisador tivesse informações adicionais para a pessoa (como peso, sexo, raça) e tentasse prever o peso dessa pessoa. Esse [serviço Web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) se ajusta ao modelo de regressão linear para os dados e gera o valor previsto (y) para cada uma das observações nos dados.

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – sem qualquer infraestrutura configurada pelo autor do serviço Web.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
O serviço Web dá os valores previstos da variável dependente com base em variáveis independentes para todas as observações. O serviço Web espera que o usuário final insira seus dados como cadeias de caracteres em que as linhas são separadas por vírgula (,) e as colunas são separadas por ponto e vírgula (;). O serviço Web espera 1 linha por vez e espera que a primeira coluna seja a variável dependente. Um conjunto de dados de exemplo poderia ser assim:

![Dados de amostra][1]

Observações sem uma variável dependente devem ser inseridas como "NA" para y. Os dados de entrada para o conjunto de dados acima seria o seguinte: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”. O resultado é o valor previsto para cada uma das linhas com base nas variáveis independentes. 

> Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo estão [aqui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

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
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.
> 
> 

De dentro do Azure Machine Learning, um novo teste em branco foi criado e dois módulos [Executar Scripts R][execute-r-script] foram levados ao espaço de trabalho. Esse serviço Web executa um teste de Azure Machine Learning com script R subjacente. Há 2 partes para esse experimento: a definição de esquema e o modelo de treinamento + pontuação. O primeiro módulo define a estrutura esperada do conjunto de entrada, em que a primeira variável é a variável dependente e as variáveis restantes são independentes. O segundo módulo se encaixa em um modelo de regressão linear genérico para os dados de entrada.  

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
Este é um exemplo muito simples de um serviço Web de regressão linear múltipla. Como pode ser visto no código de exemplo acima, nenhuma captura de erro é implementada e o serviço pressupõe que tudo é uma variável contínua (nenhum recurso categórico é permitido), uma vez que o serviço apenas produz valores números no momento da criação do serviço Web. Além disso, atualmente o serviço lida com um tamanho de dados limitado, devido à natureza da solicitação/resposta da chamada do serviço Web e ao fato de que o modelo é ajustado sempre que o serviço Web é chamado. 

## <a name="faq"></a>Perguntas frequentes
Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

