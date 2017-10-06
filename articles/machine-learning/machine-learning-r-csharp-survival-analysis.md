---
title: "AAA(deprecated) análise de sobrevivência com o aprendizado de máquina do Azure | Microsoft Docs"
description: "(preterido) Probabilidade de ocorrência de evento de Análise de Sobrevivência"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="8d07b-103">(preterido) Análise de Sobrevivência</span><span class="sxs-lookup"><span data-stu-id="8d07b-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="8d07b-104">Olá Microsoft DataMarket está sendo desativado e esta API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="8d07b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="8d07b-105">Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="8d07b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="8d07b-106">Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="8d07b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="8d07b-107">Em muitos cenários, o resultado principal de saudação em avaliação é Olá tooan evento de interesse.</span><span class="sxs-lookup"><span data-stu-id="8d07b-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="8d07b-108">Em outras palavras, pergunta de hello "quando esse evento ocorrerá?"</span><span class="sxs-lookup"><span data-stu-id="8d07b-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="8d07b-109">é feita.</span><span class="sxs-lookup"><span data-stu-id="8d07b-109">is asked.</span></span> <span data-ttu-id="8d07b-110">Como exemplo, considere situações em que dados saudação descrevem o tempo decorrido de saudação (dias, anos, quilometragem, etc.) até Olá ocorre o evento de interesse (relapse doença, grau PhD recebida, falha de freio preenchimento).</span><span class="sxs-lookup"><span data-stu-id="8d07b-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="8d07b-111">Cada instância em dados saudação representa um objeto específico (um paciente um aluno, um carro, etc.).</span><span class="sxs-lookup"><span data-stu-id="8d07b-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="8d07b-112">Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) responde a pergunta de hello "qual é a probabilidade de Olá Olá eventos de interesse ocorrerá por tempo n para objeto x?"</span><span class="sxs-lookup"><span data-stu-id="8d07b-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="8d07b-113">Ao fornecer um modelo de análise de sobrevivência, esse serviço da web permite que os usuários toosupply dados tootrain Olá modelo e testá-lo.</span><span class="sxs-lookup"><span data-stu-id="8d07b-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="8d07b-114">tema principal de saudação do experimento Olá toomodel Olá de é Olá decorrido tempo até que ocorra o evento de saudação de interesse.</span><span class="sxs-lookup"><span data-stu-id="8d07b-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="8d07b-115">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="8d07b-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="8d07b-116">Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="8d07b-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="8d07b-117">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="8d07b-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="8d07b-118">serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d07b-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="8d07b-119">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="8d07b-119">Consumption of web service</span></span>
<span data-ttu-id="8d07b-120">esquema de dados de entrada de saudação do serviço web de saudação é mostrada no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d07b-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="8d07b-121">Seis informações são necessárias como entrada hello: dados de treinamento, dados de teste, tempo de interesse, o índice de saudação da dimensão "Hora" Olá, índice e dimensão "evento" e os tipos de variáveis de saudação (contínua ou o fator).</span><span class="sxs-lookup"><span data-stu-id="8d07b-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="8d07b-122">dados de treinamento de saudação são representados com uma cadeia de caracteres, em que linhas de saudação são separadas por vírgula e Olá colunas são separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d07b-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="8d07b-123">número de saudação de recursos de dados de saudação é flexível.</span><span class="sxs-lookup"><span data-stu-id="8d07b-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="8d07b-124">Todos os elementos de saudação na cadeia de caracteres de entrada hello devem ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="8d07b-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="8d07b-125">Nos dados de treinamento Olá, a dimensão de tempo"hello" indica número Olá de unidades de tempo (dias, anos, quilometragem, etc.) decorrido desde que o ponto de partida de saudação da saudação estudar (um paciente programas de tratamento de droga, um estudo de PhD aluno inicial, um carro iniciando toobe controlado por, etc.) Após hello eventos de interesse (paciente Olá retornando toodrug uso, grau Olá PhD hello, obtenção dos alunos, car Olá ter falha de preenchimento de freio, etc.).</span><span class="sxs-lookup"><span data-stu-id="8d07b-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="8d07b-126">dimensão de "evento" Olá indica se o evento Olá de interesse ocorre no final de saudação do estudo hello.</span><span class="sxs-lookup"><span data-stu-id="8d07b-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="8d07b-127">Um valor de "evento = 1" significa que eventos de interesse de Olá ocorre em tempo de saudação indicado pela dimensão de "tempo" hello; "evento = 0" significa que Olá eventos de interesse não ocorreu por tempo Olá indicado pela dimensão de "tempo" hello.</span><span class="sxs-lookup"><span data-stu-id="8d07b-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="8d07b-128">trainingdata - uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d07b-128">trainingdata - A character string.</span></span> <span data-ttu-id="8d07b-129">As linhas são separadas por vírgulas; as colunas são separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="8d07b-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="8d07b-130">Cada linha inclui a dimensão de "tempo", a dimensão de "evento" e as variáveis do preditor.</span><span class="sxs-lookup"><span data-stu-id="8d07b-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="8d07b-131">testingdata - Uma linha de dados que contém variáveis de previsão para um determinado objeto.</span><span class="sxs-lookup"><span data-stu-id="8d07b-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="8d07b-132">time_of_interest - Olá tempo de interesse n.</span><span class="sxs-lookup"><span data-stu-id="8d07b-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="8d07b-133">index_time - índice de coluna de saudação da dimensão de "Hora" hello (começando em 1).</span><span class="sxs-lookup"><span data-stu-id="8d07b-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="8d07b-134">index_event - índice de coluna de saudação da dimensão de "evento" hello (começando em 1).</span><span class="sxs-lookup"><span data-stu-id="8d07b-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="8d07b-135">variable_types - Uma cadeia de caracteres com ponto e vírgula como separador.</span><span class="sxs-lookup"><span data-stu-id="8d07b-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="8d07b-136">0 representa variáveis contínuas e 1 representa variáveis de fator.</span><span class="sxs-lookup"><span data-stu-id="8d07b-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="8d07b-137">saída de Hello é a probabilidade de saudação de um evento que ocorre em uma hora específica.</span><span class="sxs-lookup"><span data-stu-id="8d07b-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="8d07b-138">Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="8d07b-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="8d07b-139">Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="8d07b-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="8d07b-140">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="8d07b-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="8d07b-141">interpretação de saudação desse teste é o seguinte.</span><span class="sxs-lookup"><span data-stu-id="8d07b-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="8d07b-142">Supondo que objetivo Olá dados saudação é toomodel Olá tempo até Olá retornar toodrug uso para pacientes Olá que receberam um dos programas de tratamento de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="8d07b-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="8d07b-143">Olá saída de leituras de serviço da web hello: para pacientes sendo 35 anos, tendo anterior medicamento tratamento 2 vezes, levando o programa de tratamento de tempo residencial Olá, e com o uso de heroin e cocaine, a probabilidade de saudação de retorno de uso de droga toohello é 95.64% por dia 500.</span><span class="sxs-lookup"><span data-stu-id="8d07b-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="8d07b-144">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="8d07b-144">Creation of web service</span></span>
> <span data-ttu-id="8d07b-145">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8d07b-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="8d07b-146">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="8d07b-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="8d07b-147">Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.</span><span class="sxs-lookup"><span data-stu-id="8d07b-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="8d07b-148">De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] módulos foram recebidos no espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d07b-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="8d07b-149">Olá esquema de dados foi criada com um simples [Executar Script R][execute-r-script], que define o esquema de dados de entrada hello para serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d07b-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="8d07b-150">Esse módulo é vinculado toohello segundo [Executar Script R] [ execute-r-script] módulo, que major o trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d07b-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="8d07b-151">Esse módulo faz o pré-processamento de dados, a criação de modelo e as previsões.</span><span class="sxs-lookup"><span data-stu-id="8d07b-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="8d07b-152">Na etapa de pré-processamento de dados hello, dados de entrada hello representados por uma cadeia de caracteres longa são transformados e convertidos em um quadro de dados.</span><span class="sxs-lookup"><span data-stu-id="8d07b-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="8d07b-153">Na etapa de criação de modelo hello, um pacote R externo "survival_2.37 7.zip" é instalado para realizar a análise de sobrevivência.</span><span class="sxs-lookup"><span data-stu-id="8d07b-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="8d07b-154">Em seguida, função de "coxph" hello é executada após um tarefas de processamento de dados da série.</span><span class="sxs-lookup"><span data-stu-id="8d07b-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="8d07b-155">detalhes de saudação da função de "coxph" Olá para análise de sobrevivência podem ser lidos na documentação de saudação R.</span><span class="sxs-lookup"><span data-stu-id="8d07b-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="8d07b-156">Na etapa de previsão hello, uma instância de teste é fornecida em treinado Olá com função de "surfit" hello e curva de sobrevivência Olá para esta instância de teste é produzida como variável "curva".</span><span class="sxs-lookup"><span data-stu-id="8d07b-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="8d07b-157">Por fim, a probabilidade de saudação do tempo de saudação de interesse é obtida.</span><span class="sxs-lookup"><span data-stu-id="8d07b-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="8d07b-158">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="8d07b-158">Experiment flow:</span></span>
![fluxo de teste][1]

#### <a name="module-1"></a><span data-ttu-id="8d07b-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="8d07b-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="8d07b-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="8d07b-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="8d07b-162">Limitações</span><span class="sxs-lookup"><span data-stu-id="8d07b-162">Limitations</span></span>
<span data-ttu-id="8d07b-163">Este serviço Web aceita apenas valores numéricos como variáveis de recurso (colunas).</span><span class="sxs-lookup"><span data-stu-id="8d07b-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="8d07b-164">coluna de "evento" Hello pode levar apenas o valor 0 ou 1.</span><span class="sxs-lookup"><span data-stu-id="8d07b-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="8d07b-165">coluna de "Hora" Hello precisa toobe um número inteiro positivo.</span><span class="sxs-lookup"><span data-stu-id="8d07b-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="8d07b-166">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="8d07b-166">FAQ</span></span>
<span data-ttu-id="8d07b-167">Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8d07b-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

