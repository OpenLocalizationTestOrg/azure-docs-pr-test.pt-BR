---
title: "(preterido) Pacote de distribuição binomial — Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="29313-103">(preterido) Pacote de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="29313-104">O Microsoft DataMarket está sendo desativado e essa API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="29313-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="29313-105">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="29313-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="29313-106">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="29313-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="29313-107">O Pacote de Distribuição Binomial é um conjunto de serviços Web de exemplo ([Gerador Binomial](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Calculadora de probabilidade](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Calculadora de Quantil](https://datamarket.azure.com/dataset/aml_labs/bdq5)) que ajuda a gerar e lidar com distribuições binomiais.</span><span class="sxs-lookup"><span data-stu-id="29313-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="29313-108">Os serviços permitem gerar uma sequência de distribuição binomial de qualquer tamanho, calcular quantidades a partir de uma determinada probabilidade e calcular probabilidade a partir de um determinado quantil.</span><span class="sxs-lookup"><span data-stu-id="29313-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="29313-109">Cada um dos serviços emite saídas diferentes com base no serviço selecionado (consulte a descrição abaixo).</span><span class="sxs-lookup"><span data-stu-id="29313-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="29313-110">O Pacote de Distribuição Binomial baseia-se nas funções R qbinom, rbinom e pbinom, que são incluídas no pacote de estatísticas de R.</span><span class="sxs-lookup"><span data-stu-id="29313-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="29313-111">Esses serviços Web podem ser consumidos por usuários – potencialmente de forma direta no marketplace, por meio de um aplicativo móvel, um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="29313-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="29313-112">Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="29313-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="29313-113">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="29313-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="29313-114">O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – não é necessária nenhuma configuração de infraestrutura feita pelo autor do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="29313-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="29313-115">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="29313-115">Consumption of web service</span></span>
<span data-ttu-id="29313-116">O pacote de Distribuição Binomial inclui os três serviços a seguir.</span><span class="sxs-lookup"><span data-stu-id="29313-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="29313-117">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="29313-118">Esse serviço aceita quatro argumentos de uma distribuição normal e calcula o quantil associado.</span><span class="sxs-lookup"><span data-stu-id="29313-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="29313-119">Os argumentos de entrada são:</span><span class="sxs-lookup"><span data-stu-id="29313-119">The input arguments are:</span></span>

* <span data-ttu-id="29313-120">p - uma única probabilidade agregada de várias tentativas.</span><span class="sxs-lookup"><span data-stu-id="29313-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="29313-121">tamanho – o número de tentativas.</span><span class="sxs-lookup"><span data-stu-id="29313-121">size - The number of trials.</span></span>
* <span data-ttu-id="29313-122">prob – a probabilidade de sucesso em uma tentativa.</span><span class="sxs-lookup"><span data-stu-id="29313-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="29313-123">Lado – L para o lado inferior da distribuição, U para o lado superior da distribuição.</span><span class="sxs-lookup"><span data-stu-id="29313-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="29313-124">A saída do serviço é o quantil calculado associado à probabilidade determinada.</span><span class="sxs-lookup"><span data-stu-id="29313-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="29313-125">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="29313-126">Esse serviço aceita quatro argumentos de uma distribuição binominal e calcula a probabilidade associada.</span><span class="sxs-lookup"><span data-stu-id="29313-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="29313-127">Os argumentos de entrada são:</span><span class="sxs-lookup"><span data-stu-id="29313-127">The input arguments are:</span></span>

* <span data-ttu-id="29313-128">q - um único quantil de um evento com distribuição binomial.</span><span class="sxs-lookup"><span data-stu-id="29313-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="29313-129">tamanho – o número de tentativas.</span><span class="sxs-lookup"><span data-stu-id="29313-129">size - The number of trials.</span></span>
* <span data-ttu-id="29313-130">prob – a probabilidade de sucesso em uma tentativa.</span><span class="sxs-lookup"><span data-stu-id="29313-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="29313-131">lado – L para o lado inferior da distribuição, U para o lado superior da distribuição ou E, que é igual a um único número de sucessos.</span><span class="sxs-lookup"><span data-stu-id="29313-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="29313-132">A saída do serviço é a probabilidade calculada associada ao quantil determinado.</span><span class="sxs-lookup"><span data-stu-id="29313-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="29313-133">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="29313-134">Este serviço aceita três argumentos de uma distribuição binomial e gera uma sequência aleatória de números distribuídos binomialmente.</span><span class="sxs-lookup"><span data-stu-id="29313-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="29313-135">Os argumentos a seguir devem ser fornecidos a ele na solicitação:</span><span class="sxs-lookup"><span data-stu-id="29313-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="29313-136">n - número de observações.</span><span class="sxs-lookup"><span data-stu-id="29313-136">n - Number of observations.</span></span> 
* <span data-ttu-id="29313-137">tamanho – número de tentativas.</span><span class="sxs-lookup"><span data-stu-id="29313-137">size - Number of trials.</span></span>
* <span data-ttu-id="29313-138">prob – probabilidade de sucesso.</span><span class="sxs-lookup"><span data-stu-id="29313-138">prob - Probability of success.</span></span>

<span data-ttu-id="29313-139">A saída do serviço é uma sequência de tamanho n com uma distribuição binomial com base no tamanho e em argumentos prob.</span><span class="sxs-lookup"><span data-stu-id="29313-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="29313-140">Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="29313-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="29313-141">Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo são: [Gerador](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Calculadora de probabilidade](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Calculadora de quantil](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="29313-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="29313-142">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="29313-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="29313-143">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="29313-144">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="29313-145">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="29313-146">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="29313-146">Creation of web service</span></span>
> <span data-ttu-id="29313-147">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="29313-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="29313-148">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="29313-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="29313-149">Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="29313-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="29313-150">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-150">Binomial Distribution Quantile Calculator</span></span>
![Criar espaço de trabalho][4]

#### <a name="module-1"></a><span data-ttu-id="29313-152">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="29313-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="29313-153">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="29313-153">Module 2:</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="29313-154">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-154">Binomial Distribution Probability Calculator</span></span>
![Criar espaço de trabalho][5]

#### <a name="module-1"></a><span data-ttu-id="29313-156">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="29313-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="29313-157">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="29313-157">Module 2:</span></span>
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="29313-158">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="29313-158">Binomial Distribution Generator</span></span>
![Criar espaço de trabalho][6]

#### <a name="module-1"></a><span data-ttu-id="29313-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="29313-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="29313-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="29313-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="29313-162">Limitações</span><span class="sxs-lookup"><span data-stu-id="29313-162">Limitations</span></span>
<span data-ttu-id="29313-163">Estes são exemplos muito simples de Distribuição Binomial.</span><span class="sxs-lookup"><span data-stu-id="29313-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="29313-164">Como se pode ver no exemplo de código acima, pouca captura de erro é implantada.</span><span class="sxs-lookup"><span data-stu-id="29313-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="29313-165">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="29313-165">FAQ</span></span>
<span data-ttu-id="29313-166">Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="29313-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

