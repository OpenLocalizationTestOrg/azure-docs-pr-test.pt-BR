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
# <a name="deprecated-survival-analysis"></a>(preterido) Análise de Sobrevivência

> [!NOTE]
> Olá Microsoft DataMarket está sendo desativado e esta API foi preterida. 
> 
> Você pode encontrar várias APIs e experiências de exemplo útil no hello [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com). Para obter mais informações sobre Olá galeria, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](machine-learning-gallery-how-to-use-contribute-publish.md).

Em muitos cenários, o resultado principal de saudação em avaliação é Olá tooan evento de interesse. Em outras palavras, pergunta de hello "quando esse evento ocorrerá?" é feita. Como exemplo, considere situações em que dados saudação descrevem o tempo decorrido de saudação (dias, anos, quilometragem, etc.) até Olá ocorre o evento de interesse (relapse doença, grau PhD recebida, falha de freio preenchimento). Cada instância em dados saudação representa um objeto específico (um paciente um aluno, um carro, etc.).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Isso [serviço web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) responde a pergunta de hello "qual é a probabilidade de Olá Olá eventos de interesse ocorrerá por tempo n para objeto x?" Ao fornecer um modelo de análise de sobrevivência, esse serviço da web permite que os usuários toosupply dados tootrain Olá modelo e testá-lo. tema principal de saudação do experimento Olá toomodel Olá de é Olá decorrido tempo até que ocorra o evento de saudação de interesse. 

> Este serviço Web poderia ser consumido por usuários – potencialmente por meio de um aplicativo móvel, de um site ou até mesmo em um computador local, por exemplo. Mas finalidade de saudação do serviço web de saudação também é tooserve como um exemplo de como o aprendizado de máquina do Azure pode ser usado toocreate os serviços da web sobre o código R. Com apenas algumas linhas de código R e cliques de botão dentro do Azure Machine Learning Studio, um experimento pode ser criado com código R e publicado como um serviço Web. serviço web de saudação pode ser publicado toohello Azure Marketplace e consumido por usuários e dispositivos em Olá, mundo com nenhuma configuração de infraestrutura pelo autor de saudação do serviço web de saudação.  
> 
> 

## <a name="consumption-of-web-service"></a>Consumo do serviço Web
esquema de dados de entrada de saudação do serviço web de saudação é mostrada no Olá a tabela a seguir. Seis informações são necessárias como entrada hello: dados de treinamento, dados de teste, tempo de interesse, o índice de saudação da dimensão "Hora" Olá, índice e dimensão "evento" e os tipos de variáveis de saudação (contínua ou o fator). dados de treinamento de saudação são representados com uma cadeia de caracteres, em que linhas de saudação são separadas por vírgula e Olá colunas são separadas por ponto e vírgula. número de saudação de recursos de dados de saudação é flexível. Todos os elementos de saudação na cadeia de caracteres de entrada hello devem ser numéricos. Nos dados de treinamento Olá, a dimensão de tempo"hello" indica número Olá de unidades de tempo (dias, anos, quilometragem, etc.) decorrido desde que o ponto de partida de saudação da saudação estudar (um paciente programas de tratamento de droga, um estudo de PhD aluno inicial, um carro iniciando toobe controlado por, etc.) Após hello eventos de interesse (paciente Olá retornando toodrug uso, grau Olá PhD hello, obtenção dos alunos, car Olá ter falha de preenchimento de freio, etc.). dimensão de "evento" Olá indica se o evento Olá de interesse ocorre no final de saudação do estudo hello. Um valor de "evento = 1" significa que eventos de interesse de Olá ocorre em tempo de saudação indicado pela dimensão de "tempo" hello; "evento = 0" significa que Olá eventos de interesse não ocorreu por tempo Olá indicado pela dimensão de "tempo" hello.

* trainingdata - uma cadeia de caracteres. As linhas são separadas por vírgulas; as colunas são separadas por ponto e vírgula. Cada linha inclui a dimensão de "tempo", a dimensão de "evento" e as variáveis do preditor.
* testingdata - Uma linha de dados que contém variáveis de previsão para um determinado objeto.
* time_of_interest - Olá tempo de interesse n.
* index_time - índice de coluna de saudação da dimensão de "Hora" hello (começando em 1).
* index_event - índice de coluna de saudação da dimensão de "evento" hello (começando em 1).
* variable_types - Uma cadeia de caracteres com ponto e vírgula como separador. 0 representa variáveis contínuas e 1 representa variáveis de fator.

saída de Hello é a probabilidade de saudação de um evento que ocorre em uma hora específica. 

> Esse serviço, como hospedado em hello Azure Marketplace é um serviço OData; Esses podem ser chamados por meio de métodos POST ou GET. 
> 
> 

Há várias maneiras de consumo de serviço de saudação de forma automática (um aplicativo de exemplo é [aqui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Iniciando o código C# para consumo de serviço Web:
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




interpretação de saudação desse teste é o seguinte. Supondo que objetivo Olá dados saudação é toomodel Olá tempo até Olá retornar toodrug uso para pacientes Olá que receberam um dos programas de tratamento de saudação dois. Olá saída de leituras de serviço da web hello: para pacientes sendo 35 anos, tendo anterior medicamento tratamento 2 vezes, levando o programa de tratamento de tempo residencial Olá, e com o uso de heroin e cocaine, a probabilidade de saudação de retorno de uso de droga toohello é 95.64% por dia 500.

## <a name="creation-of-web-service"></a>Criação de serviço Web
> Este serviço Web foi criado usando o Azure Machine Learning. Para obter uma avaliação gratuita, bem como vídeos introdutórios sobre a criação de testes e [publicação de serviços Web](machine-learning-publish-a-machine-learning-web-service.md), consulte [azure.com/ml](http://azure.com/ml). Abaixo está uma captura de tela do experimento Olá que criou o código de exemplo e o serviço da web hello para cada um dos módulos Olá experimento hello.
> 
> 

De dentro de aprendizado de máquina do Azure, uma nova experiência em branco foi criada e dois [Executar Script R] [ execute-r-script] módulos foram recebidos no espaço de trabalho de saudação. Olá esquema de dados foi criada com um simples [Executar Script R][execute-r-script], que define o esquema de dados de entrada hello para serviço web de saudação. Esse módulo é vinculado toohello segundo [Executar Script R] [ execute-r-script] módulo, que major o trabalho. Esse módulo faz o pré-processamento de dados, a criação de modelo e as previsões. Na etapa de pré-processamento de dados hello, dados de entrada hello representados por uma cadeia de caracteres longa são transformados e convertidos em um quadro de dados. Na etapa de criação de modelo hello, um pacote R externo "survival_2.37 7.zip" é instalado para realizar a análise de sobrevivência. Em seguida, função de "coxph" hello é executada após um tarefas de processamento de dados da série. detalhes de saudação da função de "coxph" Olá para análise de sobrevivência podem ser lidos na documentação de saudação R. Na etapa de previsão hello, uma instância de teste é fornecida em treinado Olá com função de "surfit" hello e curva de sobrevivência Olá para esta instância de teste é produzida como variável "curva". Por fim, a probabilidade de saudação do tempo de saudação de interesse é obtida. 

### <a name="experiment-flow"></a>Fluxo de teste:
![fluxo de teste][1]

#### <a name="module-1"></a>Módulo 1:
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

#### <a name="module-2"></a>Módulo 2:
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




## <a name="limitations"></a>Limitações
Este serviço Web aceita apenas valores numéricos como variáveis de recurso (colunas). coluna de "evento" Hello pode levar apenas o valor 0 ou 1. coluna de "Hora" Hello precisa toobe um número inteiro positivo.

## <a name="faq"></a>Perguntas frequentes
Para perguntas frequentes sobre o consumo do serviço web de saudação ou publicação toohello Azure Marketplace, consulte [aqui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

