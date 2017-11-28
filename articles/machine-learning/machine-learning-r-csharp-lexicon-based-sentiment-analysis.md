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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="fd865-103">(preterido) Análise de Sentimento baseada em léxico</span><span class="sxs-lookup"><span data-stu-id="fd865-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="fd865-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="fd865-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="fd865-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="fd865-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="fd865-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="fd865-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="fd865-107">Como medir as opiniões e atitudes dos usuários sobre marcas ou tópicos em redes sociais online, como postagens no Facebook, tweets, análises etc.?</span><span class="sxs-lookup"><span data-stu-id="fd865-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="fd865-108">A análise de sentimento fornece um método para analisar essas questões.</span><span class="sxs-lookup"><span data-stu-id="fd865-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="fd865-109">Em geral, há dois métodos para análise de sentimento.</span><span class="sxs-lookup"><span data-stu-id="fd865-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="fd865-110">Um está usando um algoritmo de aprendizado supervisionado e Olá outros pode ser tratado como aprendizado sem supervisão.</span><span class="sxs-lookup"><span data-stu-id="fd865-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="fd865-111">Um algoritmo de aprendizado supervisionado geralmente cria um modelo de classificação em um grande corpus anotado.</span><span class="sxs-lookup"><span data-stu-id="fd865-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="fd865-112">Sua precisão baseia-se principalmente qualidade Olá anotação hello e geralmente o processo de treinamento de Olá levará um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="fd865-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="fd865-113">Além disso, quando aplicamos tooanother domínio Olá algoritmo Olá resultado geralmente não é válido.</span><span class="sxs-lookup"><span data-stu-id="fd865-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="fd865-114">Em comparação com o aprendizado toosupervised léxico com base em aprendizado sem supervisão usa um dicionário de sentimento, que não exige o armazenamento de um corpo de dados grandes e treinamento - o que torna Olá todo processo muito mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="fd865-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="fd865-115">Nosso [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) se baseia no hello MPQA subjetividade léxico (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), que é um dos dicionários de subjetividade hello mais comumente usada.</span><span class="sxs-lookup"><span data-stu-id="fd865-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="fd865-116">Há 5097 palavras negativas e 2533 palavras positivas em MPQA.</span><span class="sxs-lookup"><span data-stu-id="fd865-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="fd865-117">E todas essas palavras são anotadas como tendo uma polaridade forte ou fraca.</span><span class="sxs-lookup"><span data-stu-id="fd865-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="fd865-118">corpo inteiro da saudação é sob a licença pública geral GNU.</span><span class="sxs-lookup"><span data-stu-id="fd865-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="fd865-119">serviço web de saudação pode ser frases curtas tooany aplicada, como tweets e postagens do Facebook.</span><span class="sxs-lookup"><span data-stu-id="fd865-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="fd865-120">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="fd865-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="fd865-121">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="fd865-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="fd865-122">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="fd865-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="fd865-123">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd865-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="fd865-124">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="fd865-124">Consumption of web service</span></span>
<span data-ttu-id="fd865-125">dados de entrada Hello podem ser qualquer texto, mas o serviço web de saudação funciona melhor com frases curtas.</span><span class="sxs-lookup"><span data-stu-id="fd865-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="fd865-126">saída de Hello é um valor numérico entre -1 e 1.</span><span class="sxs-lookup"><span data-stu-id="fd865-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="fd865-127">Qualquer valor abaixo de 0 indica que o sentimento de saudação do texto de saudação é negativo; Se positivo acima de 0.</span><span class="sxs-lookup"><span data-stu-id="fd865-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="fd865-128">valor absoluto de saudação do resultado Olá denota força de saudação do sentimento Olá associado.</span><span class="sxs-lookup"><span data-stu-id="fd865-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="fd865-129">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="fd865-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="fd865-130">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="fd865-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="fd865-131">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="fd865-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="fd865-132">saudação de entrada é "É um bom dia de hoje."</span><span class="sxs-lookup"><span data-stu-id="fd865-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="fd865-133">saída de Hello é "1", que indica um sentimento positivo associado com a frase de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="fd865-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="fd865-134">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="fd865-134">Creation of web service</span></span>
> <span data-ttu-id="fd865-135">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fd865-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="fd865-136">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="fd865-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="fd865-137">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="fd865-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="fd865-138">De dentro do Azure Machine Learning, um novo teste em branco foi criado.</span><span class="sxs-lookup"><span data-stu-id="fd865-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="fd865-139">Olá figura a seguir mostra o fluxo de teste de saudação de análise de sentimento baseada em dicionário.</span><span class="sxs-lookup"><span data-stu-id="fd865-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="fd865-140">arquivo de "sent_dict.csv" Hello é léxico de subjetividade MPQA hello e é definido como uma das entradas de saudação do [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="fd865-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="fd865-141">Outra entrada é uma revisão de amostra de análise Olá Amazon conjunto de dados para teste, em que é executada a seleção, a modificação do nome de coluna e operações de divisão.</span><span class="sxs-lookup"><span data-stu-id="fd865-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="fd865-142">Usamos um léxico de subjetividade hash pacote toostore Olá na memória hello e acelerar o processo de cálculo de pontuação hello.</span><span class="sxs-lookup"><span data-stu-id="fd865-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="fd865-143">texto de saudação inteiro será indexado por pacote de "tm" e em comparação com a palavra hello no dicionário de sentimento hello.</span><span class="sxs-lookup"><span data-stu-id="fd865-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="fd865-144">Por fim, uma pontuação será calculada com a adição de peso de saudação de cada palavra subjetiva em texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd865-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="fd865-145">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="fd865-145">Experiment flow:</span></span>
![fluxo de teste][2]

#### <a name="module-1"></a><span data-ttu-id="fd865-147">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="fd865-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="fd865-148">Instalar o pacote de hash</span><span class="sxs-lookup"><span data-stu-id="fd865-148">Install hash package</span></span>
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



## <a name="limitations"></a><span data-ttu-id="fd865-149">Limitações</span><span class="sxs-lookup"><span data-stu-id="fd865-149">Limitations</span></span>
<span data-ttu-id="fd865-150">De uma perspectiva de algoritmo, análise de sentimento baseada em dicionário é uma ferramenta de análise de sentimento geral, que não pode executar melhor método de classificação Olá para campos específicos.</span><span class="sxs-lookup"><span data-stu-id="fd865-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="fd865-151">problema de negação Olá não é abordado bem.</span><span class="sxs-lookup"><span data-stu-id="fd865-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="fd865-152">Nós codificamos várias palavras de negação no nosso programa, mas uma maneira melhor é usar um dicionário de negação e criar algumas regras.</span><span class="sxs-lookup"><span data-stu-id="fd865-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="fd865-153">serviço web de saudação melhor em sentenças curtas e simples, como tweets e postagens do Facebook, que em frases longas e complexas, como análises da Amazon.</span><span class="sxs-lookup"><span data-stu-id="fd865-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="fd865-154">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="fd865-154">FAQ</span></span>
<span data-ttu-id="fd865-155">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="fd865-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


