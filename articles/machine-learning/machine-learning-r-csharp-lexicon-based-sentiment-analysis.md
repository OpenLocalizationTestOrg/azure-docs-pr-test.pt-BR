---
title: "AAA(deprecated) análise de sentimento baseada léxico - Azure | Microsoft Docs"
description: "(preterido) Análise de Sentimento baseada em léxico"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(preterido) Análise de Sentimento baseada em léxico

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Como medir as opiniões e atitudes dos usuários sobre marcas ou tópicos em redes sociais online, como postagens no Facebook, tweets, análises etc.? A análise de sentimento fornece um método para analisar essas questões.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Em geral, há dois métodos para análise de sentimento. Um está usando um algoritmo de aprendizado supervisionado e Olá outros pode ser tratado como aprendizado sem supervisão. Um algoritmo de aprendizado supervisionado geralmente cria um modelo de classificação em um grande corpus anotado. Sua precisão baseia-se principalmente qualidade Olá anotação hello e geralmente o processo de treinamento de Olá levará um longo tempo. Além disso, quando aplicamos tooanother domínio Olá algoritmo Olá resultado geralmente não é válido. Em comparação com o aprendizado toosupervised léxico com base em aprendizado sem supervisão usa um dicionário de sentimento, que não exige o armazenamento de um corpo de dados grandes e treinamento - o que torna Olá todo processo muito mais rapidamente. 

Nosso [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) se baseia no hello MPQA subjetividade léxico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), que é um dos dicionários de subjetividade hello mais comumente usada. Há 5097 palavras negativas e 2533 palavras positivas em MPQA. E todas essas palavras são anotadas como tendo uma polaridade forte ou fraca. corpo inteiro da saudação é sob a licença pública geral GNU. serviço web de saudação pode ser frases curtas tooany aplicada, como tweets e postagens do Facebook. 

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
dados de entrada Hello podem ser qualquer texto, mas o serviço web de saudação funciona melhor com frases curtas. saída de Hello é um valor numérico entre -1 e 1. Qualquer valor abaixo de 0 indica que o sentimento de saudação do texto de saudação é negativo; Se positivo acima de 0. valor absoluto de saudação do resultado Olá denota força de saudação do sentimento Olá associado. 

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



saudação de entrada é "É um bom dia de hoje." saída de Hello é "1", que indica um sentimento positivo associado com a frase de entrada hello. 

## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

De dentro do Azure Machine Learning, um novo teste em branco foi criado. Olá figura a seguir mostra o fluxo de teste de saudação de análise de sentimento baseada em dicionário. arquivo de "sent_dict.csv" Hello é léxico de subjetividade MPQA hello e é definido como uma das entradas de saudação do [Executar Script R][execute-r-script]. Outra entrada é uma revisão de amostra de análise Olá Amazon conjunto de dados para teste, em que é executada a seleção, a modificação do nome de coluna e operações de divisão. Usamos um léxico de subjetividade hash pacote toostore Olá na memória hello e acelerar o processo de cálculo de pontuação hello. texto de saudação inteiro será indexado por pacote de "tm" e em comparação com a palavra hello no dicionário de sentimento hello. Por fim, uma pontuação será calculada com a adição de peso de saudação de cada palavra subjetiva em texto de saudação. 

### <a name="experiment-flow"></a>Fluxo de teste:
![fluxo de teste][2]

#### <a name="module-1"></a>Módulo 1:
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Instalar o pacote de hash
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Limitações
De uma perspectiva de algoritmo, análise de sentimento baseada em dicionário é uma ferramenta de análise de sentimento geral, que não pode executar melhor método de classificação Olá para campos específicos. problema de negação Olá não é abordado bem. Nós codificamos várias palavras de negação no nosso programa, mas uma maneira melhor é usar um dicionário de negação e criar algumas regras. serviço web de saudação melhor em sentenças curtas e simples, como tweets e postagens do Facebook, que em frases longas e complexas, como análises da Amazon. 

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


