---
title: "AAA(deprecated) distribuição Normal Suite de serviço Web - Azure | Microsoft Docs"
description: "(preterido) Pacote de serviço Web de distribuição normal"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="86794-103">(preterido) Pacote de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="86794-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="86794-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="86794-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="86794-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="86794-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="86794-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="86794-107">Olá Suite distribuição Normal é um conjunto de serviços da web de exemplo ([gerador](https://datamarket.azure.com/dataset/aml_labs/ndg7), [quantil Calculadora](https://datamarket.azure.com/dataset/aml_labs/ndq5), [probabilidade Calculadora](https://datamarket.azure.com/dataset/aml_labs/ndp5)) que ajudam na geração e manipulação distribuições normais.</span><span class="sxs-lookup"><span data-stu-id="86794-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="86794-108">Serviços de saudação permitem gerar uma sequência de distribuição normal de qualquer tamanho, calculando quantis de uma determinada probabilidade e calcular a probabilidade de um determinado quantil.</span><span class="sxs-lookup"><span data-stu-id="86794-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="86794-109">Cada um dos serviços de saudação emite saídas diferentes com base no serviço de saudação selecionado (consulte a descrição abaixo).</span><span class="sxs-lookup"><span data-stu-id="86794-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="86794-110">Olá distribuição Normal Suite baseia-se em Olá R funções qnorm, rnorm e pnorm, que são incluídos no pacote de estatísticas de R.</span><span class="sxs-lookup"><span data-stu-id="86794-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="86794-111">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="86794-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="86794-112">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="86794-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="86794-113">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="86794-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="86794-114">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="86794-115">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="86794-115">Consumption of web service</span></span>
<span data-ttu-id="86794-116">Olá distribuição Normal Suite inclui Olá 3 serviços a seguir.</span><span class="sxs-lookup"><span data-stu-id="86794-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86794-117">Calculadora de quantil de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="86794-118">Este serviço aceita 4 argumentos de uma distribuição normal e calcula o quantil Olá associado.</span><span class="sxs-lookup"><span data-stu-id="86794-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="86794-119">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="86794-119">hello input arguments are:</span></span>

* <span data-ttu-id="86794-120">p - uma única probabilidade de um evento com distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="86794-121">Média - média de uma distribuição normal de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86794-122">SD - Olá desvio padrão da distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="86794-123">Lado - L para o lado inferior de saudação da distribuição hello e U para o lado superior de saudação da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="86794-124">saída de saudação do serviço de saudação é quantil Olá calculado que está associado a saudação considerando a probabilidade.</span><span class="sxs-lookup"><span data-stu-id="86794-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86794-125">Calculadora de probabilidade de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="86794-126">Este serviço aceita 4 argumentos de uma distribuição normal e calcula a probabilidade de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="86794-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="86794-127">argumentos de entrada Hello são:</span><span class="sxs-lookup"><span data-stu-id="86794-127">hello input arguments are:</span></span>

* <span data-ttu-id="86794-128">q - um único quantil de um evento com distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="86794-129">Média - média de uma distribuição normal de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86794-130">SD - Olá desvio padrão da distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="86794-131">Lado - L para o lado inferior de saudação da distribuição hello e U para o lado superior de saudação da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="86794-132">saída de saudação do serviço de saudação é a probabilidade de Olá calculado que está associada a saudação fornecida quantil.</span><span class="sxs-lookup"><span data-stu-id="86794-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="86794-133">Gerador de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-133">Normal Distribution Generator</span></span>
<span data-ttu-id="86794-134">Este serviço aceita três argumentos de uma distribuição normal e gera uma sequência aleatória de números distribuídos normalmente.</span><span class="sxs-lookup"><span data-stu-id="86794-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="86794-135">Olá argumentos a seguir devem ser fornecidos tooit na solicitação de saudação:</span><span class="sxs-lookup"><span data-stu-id="86794-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="86794-136">n - número de Olá de observações.</span><span class="sxs-lookup"><span data-stu-id="86794-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="86794-137">Média - média de uma distribuição normal de saudação.</span><span class="sxs-lookup"><span data-stu-id="86794-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="86794-138">SD - Olá desvio padrão da distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="86794-139">saída de saudação do serviço de saudação é uma sequência de comprimento de n com uma distribuição normal com base nos argumentos de média e sd hello.</span><span class="sxs-lookup"><span data-stu-id="86794-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="86794-140">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="86794-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="86794-141">Há várias maneiras de consumo de serviço de saudação de forma automática (aplicativos de exemplo estão aqui: [gerador](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [probabilidade Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [quantil Calculadora](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="86794-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="86794-142">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="86794-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86794-143">Calculadora de quantil de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86794-144">Calculadora de probabilidade de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="86794-145">Gerador de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="86794-146">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="86794-146">Creation of web service</span></span>
> <span data-ttu-id="86794-147">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="86794-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="86794-148">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="86794-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="86794-149">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="86794-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="86794-150">Calculadora de quantil de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="86794-151">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="86794-151">Experiment flow:</span></span>

![Fluxo de teste][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="86794-153">Calculadora de probabilidade de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="86794-154">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="86794-154">Experiment flow:</span></span>

![Fluxo de teste][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="86794-156">Gerador de distribuição normal</span><span class="sxs-lookup"><span data-stu-id="86794-156">Normal Distribution Generator</span></span>
<span data-ttu-id="86794-157">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="86794-157">Experiment flow:</span></span>

![Fluxo de teste][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="86794-159">Limitações</span><span class="sxs-lookup"><span data-stu-id="86794-159">Limitations</span></span>
<span data-ttu-id="86794-160">Estes são exemplos muito simples ao redor Olá uma distribuição normal.</span><span class="sxs-lookup"><span data-stu-id="86794-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="86794-161">Como pode ser visto no código de exemplo hello acima, capturando pouco de erro é implementado.</span><span class="sxs-lookup"><span data-stu-id="86794-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="86794-162">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="86794-162">FAQ</span></span>
<span data-ttu-id="86794-163">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="86794-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

