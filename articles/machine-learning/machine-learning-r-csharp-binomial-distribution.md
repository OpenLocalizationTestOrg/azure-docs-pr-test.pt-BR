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
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="3b845-103">(preterido) Pacote de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="3b845-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="3b845-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3b845-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3b845-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3b845-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3b845-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3b845-107">Olá Suite distribuição Binomial é um conjunto de serviços da web de exemplo ([Binomial gerador](https://datamarket.azure.com/dataset/aml_labs/bdg5), [probabilidade Calculadora](https://datamarket.azure.com/dataset/aml_labs/bdp4), [quantil Calculadora](https://datamarket.azure.com/dataset/aml_labs/bdq5)) que ajudam a gerar e Lidando com distribuições binomial.</span><span class="sxs-lookup"><span data-stu-id="3b845-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="3b845-108">Olá serviços permitem gerar uma sequência de distribuição binomial de qualquer tamanho, calculando quantis de dado probabilidade e a probabilidade de cálculo de um determinado quantil.</span><span class="sxs-lookup"><span data-stu-id="3b845-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="3b845-109">Cada um dos serviços de saudação emite saídas diferentes com base no serviço de saudação selecionado (consulte a descrição abaixo).</span><span class="sxs-lookup"><span data-stu-id="3b845-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="3b845-110">Olá distribuição Binomial Suite baseia-se em Olá R funções qbinom, rbinom e pbinom, que são incluídos no pacote de estatísticas de R hello.</span><span class="sxs-lookup"><span data-stu-id="3b845-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="3b845-111">Esses serviços da web podem ser consumidos por usuários – potencialmente diretamente no marketplace hello, por meio de um aplicativo móvel, por meio de um site, ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="3b845-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3b845-112">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="3b845-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="3b845-113">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3b845-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3b845-114">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo – nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação é necessária.</span><span class="sxs-lookup"><span data-stu-id="3b845-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3b845-115">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="3b845-115">Consumption of web service</span></span>
<span data-ttu-id="3b845-116">Olá distribuição Binomial Suite inclui Olá 3 serviços a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b845-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3b845-117">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="3b845-118">Este serviço aceita 4 argumentos de uma distribuição normal e calcula o quantil Olá associado.</span><span class="sxs-lookup"><span data-stu-id="3b845-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="3b845-119">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="3b845-119">hello input arguments are:</span></span>

* <span data-ttu-id="3b845-120">p - uma única probabilidade agregada de várias tentativas.</span><span class="sxs-lookup"><span data-stu-id="3b845-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="3b845-121">tamanho - número de saudação de tentativas.</span><span class="sxs-lookup"><span data-stu-id="3b845-121">size - hello number of trials.</span></span>
* <span data-ttu-id="3b845-122">PROB - probabilidade de saudação de sucesso em uma versão de avaliação.</span><span class="sxs-lookup"><span data-stu-id="3b845-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3b845-123">Lado - L para o lado inferior de saudação da distribuição hello, U para o lado superior de saudação da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b845-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="3b845-124">saída de saudação do serviço de saudação é quantil Olá calculado que está associado a saudação considerando a probabilidade.</span><span class="sxs-lookup"><span data-stu-id="3b845-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3b845-125">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="3b845-126">Este serviço aceita 4 argumentos de uma distribuição binomial e calcula a probabilidade de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="3b845-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="3b845-127">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="3b845-127">hello input arguments are:</span></span>

* <span data-ttu-id="3b845-128">q - um único quantil de um evento com distribuição binomial.</span><span class="sxs-lookup"><span data-stu-id="3b845-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="3b845-129">tamanho - número de saudação de tentativas.</span><span class="sxs-lookup"><span data-stu-id="3b845-129">size - hello number of trials.</span></span>
* <span data-ttu-id="3b845-130">PROB - probabilidade de saudação de sucesso em uma versão de avaliação.</span><span class="sxs-lookup"><span data-stu-id="3b845-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3b845-131">lado - L para o lado inferior de saudação da distribuição hello, U lado superior Olá distribuição Olá da ou E que seja igual tooa único número de sucessos.</span><span class="sxs-lookup"><span data-stu-id="3b845-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="3b845-132">saída de saudação do serviço de saudação é a probabilidade de Olá calculado que está associada a saudação fornecida quantil.</span><span class="sxs-lookup"><span data-stu-id="3b845-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3b845-133">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="3b845-134">Este serviço aceita três argumentos de uma distribuição binomial e gera uma sequência aleatória de números distribuídos binomialmente.</span><span class="sxs-lookup"><span data-stu-id="3b845-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="3b845-135">Olá argumentos a seguir devem ser fornecidos tooit na solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="3b845-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="3b845-136">n - número de observações.</span><span class="sxs-lookup"><span data-stu-id="3b845-136">n - Number of observations.</span></span> 
* <span data-ttu-id="3b845-137">tamanho – número de tentativas.</span><span class="sxs-lookup"><span data-stu-id="3b845-137">size - Number of trials.</span></span>
* <span data-ttu-id="3b845-138">prob – probabilidade de sucesso.</span><span class="sxs-lookup"><span data-stu-id="3b845-138">prob - Probability of success.</span></span>

<span data-ttu-id="3b845-139">saída de saudação do serviço de saudação é uma sequência de comprimento de n com uma distribuição binomial com base nos argumentos de tamanho e prob hello.</span><span class="sxs-lookup"><span data-stu-id="3b845-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="3b845-140">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="3b845-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3b845-141">Há várias maneiras de consumo de serviço de saudação de forma automática (aplicativos de exemplo estão aqui: [gerador](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [probabilidade Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [quantil Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="3b845-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3b845-142">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="3b845-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3b845-143">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3b845-144">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="3b845-145">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="3b845-146">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="3b845-146">Creation of web service</span></span>
> <span data-ttu-id="3b845-147">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3b845-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3b845-148">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3b845-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3b845-149">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="3b845-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3b845-150">Calculadora de quantil de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-150">Binomial Distribution Quantile Calculator</span></span>
![Criar espaço de trabalho][4]

#### <a name="module-1"></a><span data-ttu-id="3b845-152">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="3b845-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="3b845-153">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="3b845-153">Module 2:</span></span>
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


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3b845-154">Calculadora de probabilidade de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-154">Binomial Distribution Probability Calculator</span></span>
![Criar espaço de trabalho][5]

#### <a name="module-1"></a><span data-ttu-id="3b845-156">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="3b845-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="3b845-157">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="3b845-157">Module 2:</span></span>
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

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3b845-158">Gerador de distribuição binomial</span><span class="sxs-lookup"><span data-stu-id="3b845-158">Binomial Distribution Generator</span></span>
![Criar espaço de trabalho][6]

#### <a name="module-1"></a><span data-ttu-id="3b845-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="3b845-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="3b845-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="3b845-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="3b845-162">Limitações</span><span class="sxs-lookup"><span data-stu-id="3b845-162">Limitations</span></span>
<span data-ttu-id="3b845-163">Estes são exemplos muito simples em torno de distribuição binomial de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b845-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="3b845-164">Como pode ser visto no código de exemplo hello acima, capturando pouco de erro é implementado.</span><span class="sxs-lookup"><span data-stu-id="3b845-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="3b845-165">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="3b845-165">FAQ</span></span>
<span data-ttu-id="3b845-166">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3b845-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

