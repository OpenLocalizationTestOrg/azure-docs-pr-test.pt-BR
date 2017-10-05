---
title: "(preterido) Análise de Sobrevivência com o Azure Machine Learning | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="1557b-103">(preterido) Análise de Sobrevivência</span><span class="sxs-lookup"><span data-stu-id="1557b-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="1557b-104">O Microsoft DataMarket está sendo desativado e essa API foi preterida.</span><span class="sxs-lookup"><span data-stu-id="1557b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="1557b-105">Você pode encontrar muitos testes de exemplo úteis e APIs na [Galeria do Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1557b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1557b-106">Para saber mais sobre a Galeria, confira [Compartilhar e descobrir soluções na Galeria do Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="1557b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="1557b-107">Em muitos cenários, o resultado principal em avaliação é o momento de um evento de interesse.</span><span class="sxs-lookup"><span data-stu-id="1557b-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="1557b-108">Em outras palavras, a pergunta “quando esse evento ocorrerá?”</span><span class="sxs-lookup"><span data-stu-id="1557b-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="1557b-109">é feita.</span><span class="sxs-lookup"><span data-stu-id="1557b-109">is asked.</span></span> <span data-ttu-id="1557b-110">Como exemplo, considere situações em que os dados descrevem o tempo decorrido (dias, anos, quilometragem, etc.) até o evento de interesse (recidiva da doença, recebimento de grau PhD, falha nas pastilhas de freio) ocorrer.</span><span class="sxs-lookup"><span data-stu-id="1557b-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="1557b-111">Cada instância nos dados representa um objeto específico (um paciente, uma estudante, um carro, etc.).</span><span class="sxs-lookup"><span data-stu-id="1557b-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="1557b-112">Esse [serviço Web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) responde à pergunta “qual é a probabilidade de o evento de interesse ocorrer no tempo n para o objeto x?”</span><span class="sxs-lookup"><span data-stu-id="1557b-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="1557b-113">Ao fornecer um modelo de análise de sobrevivência, esse serviço Web permite aos usuários fornecer dados para treinar o modelo e testá-lo.</span><span class="sxs-lookup"><span data-stu-id="1557b-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="1557b-114">O tema principal do teste é modelar a extensão do tempo decorrido até que ocorra o evento de interesse.</span><span class="sxs-lookup"><span data-stu-id="1557b-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="1557b-115">Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="1557b-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="1557b-116">Mas a finalidade do serviço Web é também servir como um exemplo de como o Azure Machine Learning pode ser usado para criar serviços Web sobre o código R.</span><span class="sxs-lookup"><span data-stu-id="1557b-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="1557b-117">Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="1557b-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="1557b-118">O serviço Web pode ser publicado no Azure Marketplace e consumido por dispositivos e usuários em todo o mundo – sem qualquer infraestrutura configurada pelo autor do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="1557b-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="1557b-119">Consumo do serviço Web</span><span class="sxs-lookup"><span data-stu-id="1557b-119">Consumption of web service</span></span>
<span data-ttu-id="1557b-120">O esquema de dados de entrada do serviço Web é mostrado na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="1557b-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="1557b-121">São necessárias seis informações como entrada: dados de treinamento, dados de teste, tempo de interesse, o índice da dimensão de "tempo", o índice da dimensão de "evento" e os tipos de variáveis (contínua ou fator).</span><span class="sxs-lookup"><span data-stu-id="1557b-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="1557b-122">Os dados de treinamento são representados por uma sequência, em que as linhas são separadas por vírgulas e as colunas são separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="1557b-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="1557b-123">O número de recursos de dados é flexível.</span><span class="sxs-lookup"><span data-stu-id="1557b-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="1557b-124">Todos os elementos na cadeia de caracteres de entrada devem ser numéricos.</span><span class="sxs-lookup"><span data-stu-id="1557b-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="1557b-125">Nos dados de treinamento, a dimensão de "tempo" indica o número de unidades de tempo (dias, anos, quilometragem, etc.) decorridas desde o ponto de partida do estudo (o recebimento de programas de tratamento de drogas pelo paciente, o início do doutorado de um aluno, o início do uso de um carro, etc.) até o evento de interesse (o paciente voltar a usar drogas, o aluno obter o grau de PhD, as pastilhas do freio do carro falharem, etc.) ocorrer.</span><span class="sxs-lookup"><span data-stu-id="1557b-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="1557b-126">A dimensão de "evento" indica se o evento de interesse ocorre no final do estudo.</span><span class="sxs-lookup"><span data-stu-id="1557b-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="1557b-127">Um valor de "evento=1" significa que o evento de interesse ocorre no período indicado pela dimensão de "tempo"; "evento=0" significa que o evento de interesse não ocorreu até o momento indicado pela dimensão de "tempo".</span><span class="sxs-lookup"><span data-stu-id="1557b-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="1557b-128">trainingdata - uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1557b-128">trainingdata - A character string.</span></span> <span data-ttu-id="1557b-129">As linhas são separadas por vírgulas; as colunas são separadas por ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="1557b-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="1557b-130">Cada linha inclui a dimensão de "tempo", a dimensão de "evento" e as variáveis do preditor.</span><span class="sxs-lookup"><span data-stu-id="1557b-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="1557b-131">testingdata - Uma linha de dados que contém variáveis de previsão para um determinado objeto.</span><span class="sxs-lookup"><span data-stu-id="1557b-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="1557b-132">time_of_interest - O tempo de interesse decorrido n.</span><span class="sxs-lookup"><span data-stu-id="1557b-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="1557b-133">index_time - O índice da coluna da dimensão de "tempo" (a partir de 1).</span><span class="sxs-lookup"><span data-stu-id="1557b-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="1557b-134">index_event - O índice da coluna da dimensão de "evento" (a partir de 1).</span><span class="sxs-lookup"><span data-stu-id="1557b-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="1557b-135">variable_types - Uma cadeia de caracteres com ponto e vírgula como separador.</span><span class="sxs-lookup"><span data-stu-id="1557b-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="1557b-136">0 representa variáveis contínuas e 1 representa variáveis de fator.</span><span class="sxs-lookup"><span data-stu-id="1557b-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="1557b-137">A saída é a probabilidade de um evento ocorrer em um determinado tempo.</span><span class="sxs-lookup"><span data-stu-id="1557b-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="1557b-138">Esse serviço, conforme hospedado no Azure Marketplace é um serviço OData; ele pode ser chamado por meio de métodos POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="1557b-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="1557b-139">Há várias maneiras de consumir o serviço de forma automática (os aplicativos de exemplo estão [aqui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1557b-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="1557b-140">Iniciando o código C# para consumo de serviço Web:</span><span class="sxs-lookup"><span data-stu-id="1557b-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="1557b-141">A interpretação desse teste é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="1557b-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="1557b-142">Supondo que o objetivo dos dados seja modelar o tempo decorrido até o retorno para o uso de drogas para os pacientes que receberam um dos dois programas de tratamento.</span><span class="sxs-lookup"><span data-stu-id="1557b-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="1557b-143">O resultado das leituras do serviço Web: para pacientes com 35 anos, dois tratamentos anteriores para drogas, recebendo o programa de tratamento residencial longo e com o uso de heroína e cocaína, a probabilidade de voltar a usar drogas é de 95,64% até o dia 500.</span><span class="sxs-lookup"><span data-stu-id="1557b-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="1557b-144">Criação de serviço Web</span><span class="sxs-lookup"><span data-stu-id="1557b-144">Creation of web service</span></span>
> <span data-ttu-id="1557b-145">Este serviço Web foi criado usando o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1557b-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="1557b-146">Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="1557b-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="1557b-147">Abaixo está uma captura de tela do teste que criou o serviço Web e o exemplo de código para cada um dos módulos dentro do teste.</span><span class="sxs-lookup"><span data-stu-id="1557b-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="1557b-148">De dentro do Azure Machine Learning, um novo teste em branco foi criado e dois módulos [Executar Scripts R][execute-r-script] foram levados ao espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1557b-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="1557b-149">O esquema de dados foi criado com um [Executar Script R][execute-r-script] simples, que define o esquema de dados de entrada para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="1557b-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="1557b-150">Esse módulo é, então, vinculado ao segundo módulo [Executar Script R][execute-r-script], que faz a maior parte do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1557b-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="1557b-151">Esse módulo faz o pré-processamento de dados, a criação de modelo e as previsões.</span><span class="sxs-lookup"><span data-stu-id="1557b-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="1557b-152">Na etapa de pré-processamento de dados, os dados de entrada representados por uma cadeia de caracteres longa são transformados e convertidos em uma estrutura de dados.</span><span class="sxs-lookup"><span data-stu-id="1557b-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="1557b-153">Na etapa de construção do modelo, um pacote R externo "survival_2.37-7.zip" é instalado para realizar a análise de sobrevivência.</span><span class="sxs-lookup"><span data-stu-id="1557b-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="1557b-154">Em seguida, a função de "coxph" é executada após uma série de tarefas de processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="1557b-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="1557b-155">Os detalhes da função "coxph" para a análise de sobrevivência podem ser lidos na documentação de R.</span><span class="sxs-lookup"><span data-stu-id="1557b-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="1557b-156">Na etapa de previsão, uma instância de teste é fornecida para o modelo treinado com a função "surfit" e a curva de sobrevivência para esta instância de teste é produzida como a variável "curva".</span><span class="sxs-lookup"><span data-stu-id="1557b-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="1557b-157">Por fim, a probabilidade do tempo de interesse é obtida.</span><span class="sxs-lookup"><span data-stu-id="1557b-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="1557b-158">Fluxo de teste:</span><span class="sxs-lookup"><span data-stu-id="1557b-158">Experiment flow:</span></span>
![fluxo de teste][1]

#### <a name="module-1"></a><span data-ttu-id="1557b-160">Módulo 1:</span><span class="sxs-lookup"><span data-stu-id="1557b-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="1557b-161">Módulo 2:</span><span class="sxs-lookup"><span data-stu-id="1557b-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="1557b-162">Limitações</span><span class="sxs-lookup"><span data-stu-id="1557b-162">Limitations</span></span>
<span data-ttu-id="1557b-163">Este serviço Web aceita apenas valores numéricos como variáveis de recurso (colunas).</span><span class="sxs-lookup"><span data-stu-id="1557b-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="1557b-164">A coluna "evento" pode ter apenas o valor 0 ou 1.</span><span class="sxs-lookup"><span data-stu-id="1557b-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="1557b-165">A coluna "hora" precisa ser um inteiro positivo.</span><span class="sxs-lookup"><span data-stu-id="1557b-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="1557b-166">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="1557b-166">FAQ</span></span>
<span data-ttu-id="1557b-167">Para obter as perguntas frequentes sobre o consumo do serviço Web ou a publicação no Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1557b-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

