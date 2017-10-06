---
title: "ciência aaaData em Olá máquina de Virtual de ciência de dados do Linux | Microsoft Docs"
description: "Como tooperform ciência de dados comum várias tarefas com hello VM de ciência de dados do Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Ciência de dados em Olá máquina de Virtual de ciência de dados do Linux
Este passo a passo mostra como tooperform ciência de dados comum várias tarefas com hello VM de ciência de dados do Linux. saudação de máquina Virtual de ciência de dados de Linux (DSVM) é uma imagem de máquina virtual disponível no Azure que é instalado com uma coleção de ferramentas usadas para análise de dados e aprendizado de máquina. componentes de software chave Olá são discriminados em Olá [Olá provisionar máquina de Virtual de ciência de dados do Linux](machine-learning-data-science-linux-dsvm-intro.md) tópico. Olá imagem VM torna fácil tooget iniciado fazendo ciência de dados em minutos, sem ter que tooinstall e configurar cada uma das ferramentas de saudação individualmente. Você pode facilmente aumentar Olá VM, se necessário e interrompê-lo quando não estiver em uso. Portanto, esse recurso é elástico e econômico.

Hello, demonstradas neste passo a passo de tarefas de ciência de dados siga etapas de saudação descritas em Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Esse processo fornece uma ciência toodata abordagem sistemática que permite às equipes de tooeffectively colaborar Olá ciclo de vida de criação de aplicativos inteligentes os cientistas de dados. o processo de ciência de dados Olá também fornece uma estrutura iterativa para ciência de dados que pode ser seguida por um indivíduo.

Analisamos Olá [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de dados neste passo a passo. Este é um conjunto de endereços de email que são marcados como spam ou ham (ou seja, eles não são spam), e também contém algumas estatísticas sobre conteúdo Olá Olá emails. estatísticas de saudação incluídas são discutidas em Olá lado mas uma seção.

## <a name="prerequisites"></a>Pré-requisitos
Antes de usar uma máquina Virtual de ciência de dados de Linux, você deve ter o seguinte hello:

* Uma **assinatura do Azure**. Se você não tiver uma, consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free/).
* Uma [**VM da ciência de dados do Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Para obter informações sobre o provisionamento essa VM, consulte [Olá provisionar máquina de Virtual de ciência de dados do Linux](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) instalado em seu computador e aberto em uma sessão XFCE. Para obter informações sobre como instalar e configurar um **cliente X2Go**, confira [Instalando e configurando o cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Uma **conta do AzureML**. Se você ainda não tiver uma, inscreva-se para uma nova no hello [home page do AzureML](https://studio.azureml.net/). Há um toohelp de nível de uso livre começar.

## <a name="download-hello-spambase-dataset"></a>Baixar o conjunto de dados do hello spambase
Olá [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de dados é um conjunto de dados que contém somente 4601 exemplos relativamente pequeno. Este é um tamanho conveniente toouse quando demonstrando que alguns dos recursos chave Olá Olá VM de ciência de dados que mantém os requisitos de recursos de saudação modesto.

> [!NOTE]
> Este passo a passo foi criado em Máquina Virtual da Ciência de Dados do Linux de tamanho D2 v2. Esse tamanho DSVM é capaz de manipular procedimentos Olá neste passo a passo.
>
>

Se você precisar de mais espaço de armazenamento, você pode criar discos adicionais e anexá-los tooyour VM. Esses discos usam armazenamento persistente do Azure, para que seus dados são preservados mesmo quando o servidor de saudação for reprovisionada vencimento tooresizing ou está desligado. tooadd um disco e anexá-lo tooyour VM, siga as instruções de saudação em [adicionar um disco tooa VM Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Essas etapas usam hello Azure de linha de comando CLI (Interface do Azure), que já está instalado no hello DSVM. Para esses procedimentos podem ser feitos inteiramente do hello própria máquina virtual. Outra opção de armazenamento de tooincrease é toouse [arquivos do Azure](../storage/files/storage-how-to-use-files-linux.md).

dados de saudação toodownload, abra uma janela do terminal e execute este comando:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

o arquivo baixado Olá não tem uma linha de cabeçalho, vamos criar outro arquivo que tem um cabeçalho. Execute este comando toocreate um arquivo com cabeçalhos apropriados Olá:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Em seguida, concatene dois arquivos Olá junto com o comando hello:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Olá dataset tem vários tipos de estatísticas sobre cada email:

* Colunas como ***word\_freq\_WORD*** indicar porcentagem Olá de palavras no email de saudação que correspondem *WORD*. Por exemplo, se *word\_freq\_fazer* for 1, 1% de todas as palavras no email Olá foram *fazer*.
* Colunas como ***char\_freq\_CHAR*** indicar porcentagem Olá de todos os caracteres no email Olá foram *CHAR*.
* ***capital\_executar\_comprimento\_mais longa*** é Olá o período mais longo de uma sequência de letras maiusculas.
* ***capital\_executar\_comprimento\_médio*** é Olá médio de todas as sequências de letras maiusculas.
* ***capital\_executar\_comprimento\_total*** é Olá o comprimento total de todas as sequências de letras maiusculas.
* ***spam*** indica se o email de saudação foi considerado spam ou não (1 = spam, 0 = não spam).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Explorar Olá conjunto de dados com o Microsoft R Open
Vamos examinar dados hello e faça o aprendizado de máquina básica com r. Olá VM de ciência de dados vem com [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pré-instalado. Hello bibliotecas matemáticas multithread nesta versão do R oferecem melhor desempenho de várias versões de thread único. Microsoft R Open também fornece reprodução usando um instantâneo do repositório de pacotes CRAN hello.

exemplos usados neste passo a passo, Olá clone de código de tooget cópias de saudação **Azure-Machine-aprendizado--ciência de dados** repositório usando o git, que é instalado em Olá VM. Na linha de comando git hello, execute:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Abra uma janela do terminal e iniciar uma nova sessão de R com um console interativo Olá R.

> [!NOTE]
> Você também pode usar o RStudio para Olá procedimentos a seguir. tooinstall RStudio, execute este comando em um terminal:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

dados de saudação tooimport e configure o ambiente hello, execute:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee estatísticas de resumo sobre cada coluna:

    summary(data)

Para obter uma exibição diferente dos dados saudação:

    str(data)

Isso mostra Olá tipo de cada variável e primeiro Olá alguns valores no conjunto de dados de saudação.

Olá *spam* coluna foi lido como um número inteiro, mas é realmente um categóricos variável (ou fator). tooset seu tipo:

    data$spam <- as.factor(data$spam)

toodo algumas análises EXPLORATÓRIAS, use Olá [ggplot2](http://ggplot2.org/) do pacote, uma biblioteca de gráfica popular para R Olá VM já está instalado. Observe que, de dados resumidos Olá exibida anteriormente, que temos as estatísticas de resumo sobre a frequência de saudação do caractere de ponto de exclamação hello. Vamos plotar as frequências aqui com hello comandos a seguir:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Desde que a barra de saudação zero é inclinação plotagem Olá, vamos eliminá-lo:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Há uma densidade não trivial acima de 1 parece interessante. Vejamos apenas os dados:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Em seguida, divida por ham vs. spam:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Estes exemplos devem permitir que você plotagens semelhante de toomake da saudação tooexplore outras colunas Olá dados neles contidos.

## <a name="train-and-test-an-ml-model"></a>Treinar e testar um modelo de AM
Agora vamos treinar um par de aprendizado de máquina modelos de emails de saudação tooclassify no conjunto de dados hello como contendo um span ou ham. Treinamos um modelo da árvore de decisão e um modelo de floresta aleatória nesta seção, então, testamos sua precisão das previsões.

> [!NOTE]
> pacote de rpart (particionamento recursivo e árvores de regressão) de saudação usado em Olá código a seguir já está instalado em Olá VM de ciência de dados.
>
>

Primeiro, vamos dividir o conjunto de dados de saudação em conjuntos de treinamento e teste:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

E, em seguida, crie uma saudação de tooclassify de árvore de decisão emails.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Este é o resultado de saudação:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

toodetermine como ele executa no treinamento de saudação definido, use Olá código a seguir:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

toodetermine como ele executa no conjunto de teste de saudação:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Também tentaremos um modelo de floresta aleatória. Florestas aleatórias treinar uma infinidade de árvores de decisão e de saída de uma classe que é o modo de saudação do classificações Olá todas Olá individuais de árvores de decisão. Eles fornecem uma abordagem de aprendizado conforme eles corrigir para tendência de saudação de um toooverfit de modelo de árvore de decisão um conjunto de dados de treinamento de máquina mais eficiente.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Implantar um modelo tooAzure ML
[O estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/) (AzureML) é um serviço de nuvem que torna fácil toobuild e implanta modelos de análise de previsão. Um dos recursos interessantes de saudação do AzureML é seu toopublish capacidade qualquer R funcionar como um serviço web. Olá pacote AzureML R faz toodo fácil implantação diretamente do nosso sessão R Olá DSVM.

toodeploy o código de árvore de decisão de Olá da seção anterior Olá, é necessário toosign em tooAzure estúdio de aprendizado de máquina. É necessário o ID do espaço de trabalho e um toosign de token de autorização no. toofind esses valores e inicializar Olá AzureML variáveis com eles:

Selecione **configurações** no menu esquerdo hello. Observe a **ID do ESPAÇO DE TRABALHO**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Selecione **Tokens de autorização** de menu sobrecarga hello e anote seu **primário Token de autorização**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Saudação de carga **AzureML** do pacote e, em seguida, definir valores de variáveis de saudação com sua ID de token e o espaço de trabalho em sua sessão de R em Olá DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Vamos simplificar Olá modelo toomake este tooimplement mais fácil de demonstração. Escolha Olá três variáveis em Olá decisão mais próximo toohello raiz da árvore e criar uma nova árvore usando apenas as três variáveis:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Precisamos de uma função de previsão que usa recursos hello como entrada e retorna Olá valores previstos:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Publicar Olá predictSpam função tooAzureML usando Olá **publishWebService** função:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Essa função usa Olá **predictSpam** funcionar, cria um serviço web denominado **spamWebService** com definido entradas e saídas e retorna informações sobre o novo ponto de extremidade de saudação.

Exibir detalhes da saudação publicado serviço da web, incluindo suas chaves de acesso e o ponto de extremidade de API com o comando hello:

    spamWebService[[2]]

tootry-out em Olá primeiras 10 linhas do conjunto de teste de saudação:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Usar outras ferramentas disponíveis
seções restantes Olá mostram como toouse algumas ferramentas Olá instaladas em Olá VM de ciência de dados do Linux. Aqui está a lista de saudação de ferramentas abordadas:

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL e Squirrel SQL
* SQL Server Data Warehouse

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) : uma ferramenta que fornece implementação de árvore aumentada rápida e precisa.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

O XGBoost também pode chamar a partir do python ou de uma linha de comando.

## <a name="python"></a>Python
Para o desenvolvimento com Python, distribuições de Python Anaconda Olá 2.7 e 3.5 foram instaladas em Olá DSVM.

> [!NOTE]
> Olá distribuição Anaconda inclui [Condas](http://conda.pydata.org/docs/index.html), que pode ser usado toocreate ambientes personalizados para Python com versões diferentes e/ou pacotes instalados.
>
>

Vamos leitura em algumas Olá spambase dataset e classificar emails Olá com máquinas de vetor de suporte em scikit-Saiba mais:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

previsões de toomake:

    clf.predict(X.ix[0:20, :])

tooshow como toopublish um ponto de extremidade AzureML, vamos criar um modelo mais simples Olá três variáveis como fizemos quando publicamos modelo Olá R anteriormente.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish Olá modelo tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Isso só está disponível para o python 2.7 e ainda não é suportado na versão 3.5. Execute com **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
distribuição da Anaconda Olá no hello DSVM vem com um bloco de anotações do Jupyter, um ambiente de plataforma cruzada tooshare Python, R ou Julia código e análise. anotações do Jupyter Olá é acessada por meio de JupyterHub. Você entra usando seu nome de usuário local do Linux e a senha em ***https://\<nome DNS da VM ou Endereço IP\>:8000/***. Todos os arquivos de configuração para o JupyterHub são encontrados no diretório **/etc/jupyterhub**.

Vários blocos de anotações de exemplo já estão instalados no hello VM:

* Consulte Olá [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) para um bloco de anotações do Python de exemplo.
* Consulte o [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para obter um bloco de anotações do **R** de exemplo.
* Consulte Olá [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para obter outro exemplo **Python** notebook.

> [!NOTE]
> Olá idioma Julia também está disponível na linha de comando Olá Olá VM de ciência de dados do Linux.
>
>

## <a name="rattle"></a>Rattle
[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (Olá ferramenta analíticos R tooLearn facilmente) é uma ferramenta gráfica de R para mineração de dados. Ele tem uma interface intuitiva que torna mais fácil tooload, explorar e transformar dados e criar e avaliar modelos.  artigo Olá [Rattle: A Data Mining GUI para R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fornece um passo a passo que demonstre seus recursos.

Instale e inicie chocalho com hello comandos a seguir:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Instalação não é necessária em Olá DSVM. Mas chocalho pode solicitar pacotes adicionais tooinstall ao ser carregado.
>
>

O Rattle usa uma interface baseada em guias. A maioria das guias Olá corresponde toosteps em Olá [processo de ciência de dados](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como o carregamento de dados ou explorá-la. processo de ciência de dados Olá flui da esquerda tooright pelas guias de saudação. Mas a guia última Olá contém um log de comandos Olá R executando chocalho.

tooload e configurar o conjunto de dados hello:

* arquivo de saudação tooload, selecione Olá **dados** guia, em seguida,
* Escolha o seletor de saudação Avançar muito**Filename** e escolha **spambaseHeaders.data**.
* arquivo de saudação tooload. Selecione **Execute** linha superior de saudação de botões. Você deve ver um resumo de cada coluna, incluindo seu tipo de dados identificado, se ele é uma entrada, um destino ou outro tipo de variável e o número de saudação de valores exclusivos.
* Chocalho identificar corretamente Olá **spam** coluna como destino de saudação. Coluna de spam selecione hello, em seguida, Olá conjunto **tipo de dados de destino** muito**Categoric**.

dados de saudação tooexplore:

* Selecione Olá **explorar** guia.
* Clique em **resumo**, em seguida, **Execute**, toosee algumas informações sobre os tipos de variáveis hello e algumas estatísticas de resumo.
* tooview outros tipos de estatísticas sobre cada variável, selecione outras opções como **descrever** ou **Noções básicas de**.

Olá **explorar** guia também permite que você toogenerate muitos criteriosos plota. tooplot um histograma dos dados saudação:

* Selecione **Distribuições**.
* Verifique o **Histograma** quanto a **word_freq_remove** e **word_freq_you**.
* Selecione **Executar**. Você deverá ver que dois densidade plota em uma janela de gráfico único, onde ele está criptografado palavra hello "você" é exibido com mais frequência nos emails de "remover".

gráficos de correlação Olá também são interessantes. toocreate um:

* Escolha **correlação** como Olá **tipo**, em seguida,
* Selecione **Executar**.
* O Rattle avisa que ele recomenda um máximo de 40 variáveis. Selecione **Sim** tooview plotagem de saudação.

Há alguns correlações interessantes que surgirem: "tecnologia" é fortemente correlacionada muito "HP" e "laboratórios", por exemplo. Ele é também fortemente correlacionado muito "650", como código de área de saudação de doadores de conjunto de dados de saudação é 650.

valores numéricos Olá correlações Olá entre palavras estão disponíveis na janela de explorar hello. É interessante toonote, por exemplo, se "tecnologia" negativamente correlacionada com "a" e "money".

Chocalho pode transformar Olá dataset toohandle alguns problemas comuns. Por exemplo, ele permite que você toorescale recursos, imputar valores ausentes, manipular exceções e remova variáveis ou observações com dados ausentes. O Rattle também pode identificar regras de associação entre as observações e/ou variáveis. Essas guias estão fora do escopo deste passo a passo de introdução.

O Rattle também pode executar a análise de cluster. Vamos excluir alguns recursos toomake Olá saída mais fácil tooread. Em Olá **dados** guia, escolha **ignorar** tooeach próximo de variáveis de saudação exceto esses dez itens:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

Vá toohello **Cluster** guia, escolha **KMeans**e conjunto hello *número de clusters* too4. Então, **Executar**. Olá resultados são exibidos na janela de saída de hello. Um cluster tem alta frequência de "george" e "hp", e provavelmente é um email corporativo legítimo.

toobuild um modelo de aprendizado de máquina de árvore de decisão simples:

* Selecione Olá **modelo** guia
* Escolha **árvore** como Olá **tipo**.
* Selecione **Execute** toodisplay árvore de saudação em formato de texto de saudação de janela de saída.
* Selecione Olá **desenhar** botão tooview uma versão de gráfica. Isso é bastante semelhante árvore toohello são obtidos anteriormente usando *rpart*.

Um dos recursos interessantes de saudação do chocalho é toorun sua capacidade de aprendizado de máquina vários métodos e avaliá-los rapidamente. Aqui está o procedimento hello:

* Escolha **todos os** para Olá **tipo**.
* Selecione **Executar**.
* Depois de concluir a você pode clicar em qualquer único **tipo**, como **SVM**e exibir resultados de saudação.
* Você também pode comparar o desempenho de saudação dos modelos de saudação na validação de saudação definido usando Olá **avaliar** guia. Por exemplo, Olá **erro matriz** seleção mostra matriz de confusão hello, erro geral e erro de média de classe para cada modelo no conjunto de validação de saudação.
* Você também pode plotar as curvas ROC, executar a análise de sensibilidade e fazer outros tipos de avaliações do modelo.

Quando você terminar de criar modelos, selecione Olá **Log** guia tooview código de saudação R executando chocalho durante a sessão. Você pode selecionar Olá **exportar** botão toosave-lo.

> [!NOTE]
> Há um bug na versão atual do Rattle. toomodify Olá script ou usá-lo toorepeat suas etapas mais tarde, você deve inserir um caractere # na frente do * exportar este log... * no texto de saudação do log de saudação.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL e Squirrel SQL
Olá DSVM vem com PostgreSQL instalado. O PostgreSQL é um banco de dados relacional sofisticado de fonte aberta. Esta seção mostra como tooload nosso conjunto de dados de spam em PostgreSQL e, em seguida, consultá-los.

Antes de carregar dados Olá, é necessário tooallow de autenticação de senha de saudação localhost. Em um prompt de comando:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Inferior Olá Olá do arquivo de configuração são várias linhas que detalham Olá conexões permitida:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Alterar hello "IPv4 conexões locais" linha toouse md5 em vez de ident, para que possa se conectar usando um nome de usuário e senha:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

E reiniciar o serviço de postgres hello:

    sudo systemctl restart postgresql

toolaunch psql, um terminal interativo para PostgreSQL, como usuário de postgres internos Olá, execute Olá comando a seguir em um prompt:

    sudo -u postgres psql

Criar uma nova conta de usuário, usando Olá o mesmo nome de usuário como Olá conta Linux que você está conectado no momento como e atribua a ele uma senha:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Faça logon toopsql como usuário:

    psql

E importar dados de saudação para um novo banco de dados:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Agora, vamos explorar dados hello e execute algumas consultas usando **SQL esquilo**, uma ferramenta gráfica que permite interagir com bancos de dados por meio de um driver JDBC.

tooget iniciado, inicie o SQL esquilo no menu de aplicativos de saudação. tooset driver hello:

* Selecione **Windows** e **Exibir Drivers**.
* Clique com o botão direito do mouse em **PostgreSQL** e selecione **Modificar Driver**.
* Selecione **Caminho de classe Extra** e **Adicionar**.
* Digite ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para Olá **nome de arquivo** e
* Selecione **Abrir**.
* Escolha Listar Drivers e selecione **org.postgresql.Driver** no **Nome da Classe** e **OK**.

tooset o servidor local do toohello Olá conexão:

* Selecione **Windows** e **Exibir Aliases.**
* Escolha Olá  **+**  toomake botão um novo alias.
* Nomeie- *banco de dados de Spam*, escolha **PostgreSQL** em Olá **Driver** lista suspensa.
* Definir a URL de saudação muito*jdbc:postgresql://localhost/spam*.
* Insira seu *nome de usuário* e *senha*.
* Clique em **OK**.
* Olá tooopen **Conexão** janela, clique duas vezes em Olá ***banco de dados de Spam*** alias.
* Selecione **Conectar**.

toorun algumas consultas:

* Selecione Olá **SQL** guia.
* Insira uma consulta simples como `SELECT * from data;` na caixa de texto de consulta de saudação na parte superior de saudação do guia SQL hello.
* Pressione **Ctrl-Enter** toorun-lo. Por padrão SQL esquilo retorna Olá primeiras 100 linhas de sua consulta.

Há muitas consultas mais que você pode executar tooexplore esses dados. Por exemplo, como faz Olá frequência da palavra hello *fazer* diferem spam ham?

    SELECT avg(word_freq_make), spam from data group by spam;

Ou quais são as características de saudação do email que normalmente contêm *3d*?

    SELECT * from data order by word_freq_3d desc;

A maioria dos emails que têm uma ocorrência alta *3d* aparentemente são spam, poderia ser um recurso útil para a criação de uma saudação do modelo de previsão tooclassify emails.

Se você quisesse tooperform aprendizado de máquina com dados armazenados em um banco de dados PostgreSQL, considere o uso de [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server Data Warehouse
O SQL Data Warehouse do Azure é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais. Para obter mais informações, consulte [O que é Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello data warehouse e cria tabela hello, comando a seguir Olá execução de um prompt de comando:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

No prompt de sqlcmd hello:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Copie os dados com o bcp:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> terminações de linha de saudação no arquivo baixado Olá são estilo do Windows, mas bcp espera estilo UNIX, por isso, precisamos bcp tootell que com hello sinalizador - r.
>
>

E consulte com o sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

Você também pode consultar com o Squirrel SQL. Siga as etapas semelhantes para PostgreSQL, usando Olá Microsoft MSSQL Server JDBC Driver, que pode ser encontrado em ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral dos tópicos que orientam você pelas tarefas de saudação que compõem o processo de ciência de dados Olá no Azure, consulte [processo de ciência de dados de equipe](http://aka.ms/datascienceprocess).

Para obter uma descrição de outras orientações de ponta a ponta que demonstram etapas Olá Olá processo de ciência de dados de equipe para cenários específicos, consulte [explicações passo a passo do processo de ciência de dados de equipe](data-science-process-walkthroughs.md). Olá explicações passo a passo também ilustra como toocombine de nuvem e ferramentas no local e serviços em um fluxo de trabalho ou pipeline toocreate um aplicativo inteligente.
