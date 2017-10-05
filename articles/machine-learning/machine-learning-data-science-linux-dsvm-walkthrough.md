---
title: "Ciência de dados na Máquina Virtual da Ciência de Dados do Linux | Microsoft Docs"
description: "Como executar várias tarefas comuns da ciência de dados com a VM da Ciência de Dados do Linux."
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
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="85130-103">Ciência de dados na Máquina Virtual da Ciência de Dados do Linux</span><span class="sxs-lookup"><span data-stu-id="85130-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="85130-104">Este passo a passo mostra como executar várias tarefas comuns da ciência de dados com a VM da Ciência de Dados do Linux.</span><span class="sxs-lookup"><span data-stu-id="85130-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="85130-105">A Máquina Virtual da Ciência de Dados do Linux (DSVM) é uma imagem da máquina virtual disponível no Azure pré-instalada com uma coleção de ferramentas usadas comumente para a análise de dados e o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="85130-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="85130-106">Os principais componentes do software são detalhados no tópico [Provisionar a Máquina Virtual da Ciência de Dados do Linux](machine-learning-data-science-linux-dsvm-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="85130-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="85130-107">A imagem da VM facilita começar a fazer a ciência de dados em minutos, sem precisar instalar e configurar cada uma das ferramentas individualmente.</span><span class="sxs-lookup"><span data-stu-id="85130-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="85130-108">Você pode dimensionar facilmente a VM, se necessário, e parar quando não estiver em uso.</span><span class="sxs-lookup"><span data-stu-id="85130-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="85130-109">Portanto, esse recurso é elástico e econômico.</span><span class="sxs-lookup"><span data-stu-id="85130-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="85130-110">As tarefas da ciência de dados demonstradas neste passo a passo seguem as etapas descritas no [Processo da Ciência de Dados de Equipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="85130-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="85130-111">Esse processo fornece uma abordagem sistemática para a ciência de dados que permite às equipes de cientistas de dados colaborarem de maneira eficiente no ciclo de vida da criação de aplicativos inteligentes.</span><span class="sxs-lookup"><span data-stu-id="85130-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="85130-112">O processo da ciência de dados também fornece uma estrutura iterativa para a ciência de dados que pode ser seguida por uma pessoa.</span><span class="sxs-lookup"><span data-stu-id="85130-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="85130-113">Analisamos o conjunto de dados [baseado em spam](https://archive.ics.uci.edu/ml/datasets/spambase) neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="85130-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="85130-114">Este é um conjunto de emails marcados como spam ou ham (ou seja, não são spam) e também contém algumas estatísticas sobre o conteúdo dos emails.</span><span class="sxs-lookup"><span data-stu-id="85130-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="85130-115">As estatísticas incluídas serão analisadas na próxima seção, exceto uma.</span><span class="sxs-lookup"><span data-stu-id="85130-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85130-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="85130-116">Prerequisites</span></span>
<span data-ttu-id="85130-117">Antes de criar uma Máquina Virtual da Ciência de Dados do Linux, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="85130-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="85130-118">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="85130-118">An **Azure subscription**.</span></span> <span data-ttu-id="85130-119">Se você não tiver uma, consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="85130-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="85130-120">Uma [**VM da ciência de dados do Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="85130-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="85130-121">Para obter informações sobre como provisionar essa VM, consulte [Provisionar a Máquina Virtual da Ciência de Dados do Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="85130-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="85130-122">[X2Go](http://wiki.x2go.org/doku.php) instalado em seu computador e aberto em uma sessão XFCE.</span><span class="sxs-lookup"><span data-stu-id="85130-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="85130-123">Para obter informações sobre como instalar e configurar um **cliente X2Go**, confira [Instalando e configurando o cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="85130-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="85130-124">Uma **conta do AzureML**.</span><span class="sxs-lookup"><span data-stu-id="85130-124">An **AzureML account**.</span></span> <span data-ttu-id="85130-125">Se você ainda não tiver, inscreva-se para ter uma nova na [home page do AzureML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="85130-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="85130-126">Há uma camada de uso gratuita para ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="85130-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="85130-127">Baixar o conjunto de dados baseado em spam</span><span class="sxs-lookup"><span data-stu-id="85130-127">Download the spambase dataset</span></span>
<span data-ttu-id="85130-128">O conjunto de dados [baseado em spam](https://archive.ics.uci.edu/ml/datasets/spambase) é um conjunto de dados relativamente pequeno que contém somente 4.601 exemplos.</span><span class="sxs-lookup"><span data-stu-id="85130-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="85130-129">Esse é um tamanho conveniente usado ao demonstrar alguns dos principais recursos da VM da Ciência de Dados, quando ela mantém os requisitos de recursos modestos.</span><span class="sxs-lookup"><span data-stu-id="85130-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-130">Este passo a passo foi criado em Máquina Virtual da Ciência de Dados do Linux de tamanho D2 v2.</span><span class="sxs-lookup"><span data-stu-id="85130-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="85130-131">Esse tamanho da DSVM é capaz de lidar com os procedimentos neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="85130-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="85130-132">Se você precisar de mais espaço de armazenamento, poderá criar discos adicionais e anexá-los à sua VM.</span><span class="sxs-lookup"><span data-stu-id="85130-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="85130-133">Esses discos usam o armazenamento persistente do Azure para que seus dados sejam preservados mesmo quando o servidor é provisionado novamente devido ao redimensionamento ou é desligado.</span><span class="sxs-lookup"><span data-stu-id="85130-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="85130-134">Para adicionar um disco e anexá-lo à sua VM, siga as instruções em [Adicionar um disco a uma VM do Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85130-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="85130-135">Essas etapas usam a Interface de Linha de Comando do Azure (Azure CLI), que já está instalada na DSVM.</span><span class="sxs-lookup"><span data-stu-id="85130-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="85130-136">Então, esses procedimentos podem ser feitos inteiramente na própria VM.</span><span class="sxs-lookup"><span data-stu-id="85130-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="85130-137">Outra opção para aumentar o armazenamento é usar os [arquivos do Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="85130-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="85130-138">Para baixar os dados, abra uma janela do terminal e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="85130-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="85130-139">O arquivo baixado não tem uma linha de cabeçalho, portamos, iremos criar outro arquivo com um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="85130-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="85130-140">Execute este comando para criar um arquivo com os devidos cabeçalhos:</span><span class="sxs-lookup"><span data-stu-id="85130-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="85130-141">Então, concatene os dois arquivos com o comando:</span><span class="sxs-lookup"><span data-stu-id="85130-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="85130-142">O conjunto de dados tem vários tipos de estatísticas em cada email:</span><span class="sxs-lookup"><span data-stu-id="85130-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="85130-143">Colunas como ***word\_freq\_WORD*** indicam a porcentagem de palavras no email que correspondem a *WORD*.</span><span class="sxs-lookup"><span data-stu-id="85130-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="85130-144">Por exemplo, se *word\_freq\_make* for 1, 1% de todas as palavras no email foi *make*.</span><span class="sxs-lookup"><span data-stu-id="85130-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="85130-145">Colunas como ***char\_freq\_CHAR*** indicam a porcentagem de todos os caracteres no email que foram *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="85130-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="85130-146">***capital\_run\_length\_longest*** é o maior comprimento de uma sequência de letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="85130-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="85130-147">***capital\_run\_length\_average*** é a duração média de todas as sequências de letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="85130-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="85130-148">***capital\_run\_length\_total*** é o comprimento total de todas as sequências de letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="85130-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="85130-149">***spam*** indica se o email foi considerado spam ou não (1 = spam, 0 = não spam).</span><span class="sxs-lookup"><span data-stu-id="85130-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="85130-150">Explorar o conjunto de dados com o Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="85130-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="85130-151">Vamos examinar os dados e fazer um aprendizado de máquina básico com R. A VM da Ciência de Dados vem com o [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="85130-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="85130-152">As bibliotecas matemáticas multithread nesta versão do R oferecem melhor desempenho que diversas versões de thread único.</span><span class="sxs-lookup"><span data-stu-id="85130-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="85130-153">O Microsoft R Open também fornece a capacidade de reprodução usando um instantâneo do repositório de pacotes CRAN.</span><span class="sxs-lookup"><span data-stu-id="85130-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="85130-154">Para obter cópias dos exemplos de código usados neste passo a passo, clone o repositório **Azure-Machine-Learning-Data-Science** usando o git, que é pré-instalado na VM.</span><span class="sxs-lookup"><span data-stu-id="85130-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="85130-155">Na linha de comando do git, execute:</span><span class="sxs-lookup"><span data-stu-id="85130-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="85130-156">Abra uma janela de terminal e inicie uma nova sessão de R com o console interativo de R.</span><span class="sxs-lookup"><span data-stu-id="85130-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-157">Você também pode usar o RStudio para os procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="85130-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="85130-158">Para instalar o RStudio, execute este comando em um terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="85130-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="85130-159">Para importar os dados e configurar o ambiente, execute:</span><span class="sxs-lookup"><span data-stu-id="85130-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="85130-160">Para ver as estatísticas de resumo sobre cada coluna:</span><span class="sxs-lookup"><span data-stu-id="85130-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="85130-161">Para obter uma exibição diferente dos dados:</span><span class="sxs-lookup"><span data-stu-id="85130-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="85130-162">Isso mostra o tipo de cada variável e os primeiros valores no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="85130-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="85130-163">A coluna *spam* foi lida como um número inteiro, mas é realmente uma variável categórica (ou fator).</span><span class="sxs-lookup"><span data-stu-id="85130-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="85130-164">Para definir seu tipo:</span><span class="sxs-lookup"><span data-stu-id="85130-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="85130-165">Para fazer algumas análises exploratórias, use o pacote [ggplot2](http://ggplot2.org/) , uma biblioteca de gráficos popular para R já está instalada na VM.</span><span class="sxs-lookup"><span data-stu-id="85130-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="85130-166">Observe, dos dados de resumo exibidos anteriormente, temos as estatísticas de resumo sobre a frequência do caractere de ponto de exclamação.</span><span class="sxs-lookup"><span data-stu-id="85130-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="85130-167">Iremos plotar as frequências aqui com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="85130-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="85130-168">Como a barra zero está distorcendo a plotagem, iremos nos livrar dela:</span><span class="sxs-lookup"><span data-stu-id="85130-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="85130-169">Há uma densidade não trivial acima de 1 parece interessante.</span><span class="sxs-lookup"><span data-stu-id="85130-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="85130-170">Vejamos apenas os dados:</span><span class="sxs-lookup"><span data-stu-id="85130-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="85130-171">Em seguida, divida por ham vs. spam:</span><span class="sxs-lookup"><span data-stu-id="85130-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="85130-172">Esses exemplos devem permitir fazer plotagens semelhante das outras colunas para explorar os dados contidos nelas.</span><span class="sxs-lookup"><span data-stu-id="85130-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="85130-173">Treinar e testar um modelo de AM</span><span class="sxs-lookup"><span data-stu-id="85130-173">Train and test an ML model</span></span>
<span data-ttu-id="85130-174">Agora, iremos treinar alguns modelos de aprendizado de máquina para classificar os emails no conjunto de dados como contendo span ou ham.</span><span class="sxs-lookup"><span data-stu-id="85130-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="85130-175">Treinamos um modelo da árvore de decisão e um modelo de floresta aleatória nesta seção, então, testamos sua precisão das previsões.</span><span class="sxs-lookup"><span data-stu-id="85130-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-176">O pacote rpart (particionamento recursivo e árvores de regressão) usado no código a seguir já está instalado na VM da Ciência de Dados.</span><span class="sxs-lookup"><span data-stu-id="85130-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="85130-177">Primeiro, dividiremos o conjunto de dados em conjuntos de treinamento e teste:</span><span class="sxs-lookup"><span data-stu-id="85130-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="85130-178">Em seguida, crie uma árvore de decisão para classificar os emails.</span><span class="sxs-lookup"><span data-stu-id="85130-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="85130-179">Aqui está o resultado:</span><span class="sxs-lookup"><span data-stu-id="85130-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="85130-181">Para determinar a execução no conjunto de treinamento, use o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="85130-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="85130-182">Para determinar a execução no conjunto de teste:</span><span class="sxs-lookup"><span data-stu-id="85130-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="85130-183">Também tentaremos um modelo de floresta aleatória.</span><span class="sxs-lookup"><span data-stu-id="85130-183">Let's also try a random forest model.</span></span> <span data-ttu-id="85130-184">As florestas aleatórias treinam uma infinidade de árvores de decisão e geram uma classe que é o modo das classificações a partir de todas as árvores de decisão individuais.</span><span class="sxs-lookup"><span data-stu-id="85130-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="85130-185">Fornecem uma abordagem do aprendizado de máquina mais potente à medida que corrigem a tendência de um modelo de árvore de decisão de sobreajustar um conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="85130-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="85130-186">Implantar um modelo para o AzureML</span><span class="sxs-lookup"><span data-stu-id="85130-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="85130-187">
            [Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) é um serviço de nuvem que facilita criar e implantar modelos de análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="85130-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="85130-188">Um dos recursos interessantes do AzureML é sua capacidade de publicar qualquer função R como um serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="85130-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="85130-189">O pacote AzureML R facilita a implantação correta a partir de nossa sessão R na DSVM.</span><span class="sxs-lookup"><span data-stu-id="85130-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="85130-190">Para implantar o código da árvore de decisão da seção anterior, você precisa entrar no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="85130-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="85130-191">Você precisa de sua ID do espaço de trabalho e de um token de autorização para entrar.</span><span class="sxs-lookup"><span data-stu-id="85130-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="85130-192">Para localizar esses valores e inicializar as variáveis do AzureML com eles:</span><span class="sxs-lookup"><span data-stu-id="85130-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="85130-193">Selecione **Configurações** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="85130-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="85130-194">Observe a **ID do ESPAÇO DE TRABALHO**.</span><span class="sxs-lookup"><span data-stu-id="85130-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="85130-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="85130-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="85130-196">Selecione **Tokens de Autorização** no menu de sobrecarga e observe o **Token de Autorização Primário**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="85130-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="85130-197">Carregue o pacote **AzureML** e defina os valores das variáveis com seu token e ID do espaço de trabalho na sessão R da DSVM:</span><span class="sxs-lookup"><span data-stu-id="85130-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="85130-198">Iremos simplificar o modelo para tornar esta demonstração mais fácil de implementar.</span><span class="sxs-lookup"><span data-stu-id="85130-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="85130-199">Selecione as três variáveis na árvore de decisão mais próximas da raiz e compile uma nova árvore usando apenas essas três variáveis:</span><span class="sxs-lookup"><span data-stu-id="85130-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="85130-200">Precisamos de uma função de previsão que usa os recursos como uma entrada e retorna os valores previstos:</span><span class="sxs-lookup"><span data-stu-id="85130-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="85130-201">Publique a função predictSpam para o AzureML usando a função **publishWebService** :</span><span class="sxs-lookup"><span data-stu-id="85130-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="85130-202">Essa função usa a **predictSpam**, cria um serviço Web denominado **spamWebService** com entradas e saídas definidas e retorna informações sobre o novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="85130-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="85130-203">Exiba os detalhes do serviço Web publicado, incluindo seu ponto de extremidade de API e acesse as chaves com o comando:</span><span class="sxs-lookup"><span data-stu-id="85130-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="85130-204">Para experimentar nas primeiras 10 linhas do conjunto de teste:</span><span class="sxs-lookup"><span data-stu-id="85130-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="85130-205">Usar outras ferramentas disponíveis</span><span class="sxs-lookup"><span data-stu-id="85130-205">Use other tools available</span></span>
<span data-ttu-id="85130-206">As seções restantes mostram como usar algumas das ferramentas instaladas na VM da Ciência de Dados do Linux. Aqui está a lista das ferramentas analisadas:</span><span class="sxs-lookup"><span data-stu-id="85130-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="85130-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="85130-207">XGBoost</span></span>
* <span data-ttu-id="85130-208">Python</span><span class="sxs-lookup"><span data-stu-id="85130-208">Python</span></span>
* <span data-ttu-id="85130-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="85130-209">Jupyterhub</span></span>
* <span data-ttu-id="85130-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="85130-210">Rattle</span></span>
* <span data-ttu-id="85130-211">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="85130-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="85130-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="85130-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="85130-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="85130-213">XGBoost</span></span>
<span data-ttu-id="85130-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) : uma ferramenta que fornece implementação de árvore aumentada rápida e precisa.</span><span class="sxs-lookup"><span data-stu-id="85130-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="85130-215">O XGBoost também pode chamar a partir do python ou de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="85130-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="85130-216">Python</span><span class="sxs-lookup"><span data-stu-id="85130-216">Python</span></span>
<span data-ttu-id="85130-217">Para o desenvolvimento com o Python, as distribuições do Anaconda Python 2.7 e 3.5 foram instaladas na DSVM.</span><span class="sxs-lookup"><span data-stu-id="85130-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-218">A distribuição Anaconda inclui o [Condas](http://conda.pydata.org/docs/index.html), que pode ser usado para criar ambientes personalizados para o Python com versões diferentes e/ou pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="85130-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="85130-219">Iremos transmitir o conjunto de dados baseado em spam e classificar os emails com máquinas do vetor de suporte no scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="85130-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="85130-220">Para fazer previsões:</span><span class="sxs-lookup"><span data-stu-id="85130-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="85130-221">Para mostrar como publicar um ponto de extremidade do AzureML, criaremos um modelo mais simples das três variáveis como fizemos quando publicamos o modelo R anteriormente.</span><span class="sxs-lookup"><span data-stu-id="85130-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="85130-222">Para publicar o modelo para o AzureML:</span><span class="sxs-lookup"><span data-stu-id="85130-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="85130-223">Isso só está disponível para o python 2.7 e ainda não é suportado na versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="85130-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="85130-224">Execute com **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="85130-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="85130-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="85130-225">Jupyterhub</span></span>
<span data-ttu-id="85130-226">A distribuição Anaconda na DSVM vem com um bloco de anotações do Jupyter, um ambiente de plataforma cruzada para compartilhar o Python, R ou o código Julia e a análise.</span><span class="sxs-lookup"><span data-stu-id="85130-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="85130-227">O notebook Jupyter é acessado com o JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="85130-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="85130-228">Você entra usando seu nome de usuário local do Linux e a senha em ***https://\<nome DNS da VM ou Endereço IP\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="85130-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="85130-229">Todos os arquivos de configuração para o JupyterHub são encontrados no diretório **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="85130-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="85130-230">Vários blocos de anotações de exemplo já estão instalados na VM:</span><span class="sxs-lookup"><span data-stu-id="85130-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="85130-231">Consulte o [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) para ver um bloco de anotações do Python de exemplo.</span><span class="sxs-lookup"><span data-stu-id="85130-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="85130-232">Consulte o [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para obter um bloco de anotações do **R** de exemplo.</span><span class="sxs-lookup"><span data-stu-id="85130-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="85130-233">Consulte o [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para obter outro bloco de anotações do **Python** de exemplo.</span><span class="sxs-lookup"><span data-stu-id="85130-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-234">O idioma Julia também está disponível na linha de comando na VM da Ciência de Dados do Linux.</span><span class="sxs-lookup"><span data-stu-id="85130-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="85130-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="85130-235">Rattle</span></span>
<span data-ttu-id="85130-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (a Ferramenta Analítica do R Fácil de Aprender) é uma ferramenta gráfica do R para a mineração de dados.</span><span class="sxs-lookup"><span data-stu-id="85130-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="85130-237">Ela tem uma interface simples que facilita carregar, explorar e transformar os dados, compilar e avaliar os modelos.</span><span class="sxs-lookup"><span data-stu-id="85130-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="85130-238">O artigo [Rattle: Uma GUI da Mineração de Dados para o R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fornece um passo a passo que demonstre seus recursos.</span><span class="sxs-lookup"><span data-stu-id="85130-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="85130-239">Instale e inicie o Rattle com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="85130-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="85130-240">A instalação não é necessária na DSVM.</span><span class="sxs-lookup"><span data-stu-id="85130-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="85130-241">Mas o Rattle pode solicitar que você instale pacotes adicionais ao ser carregado.</span><span class="sxs-lookup"><span data-stu-id="85130-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="85130-242">O Rattle usa uma interface baseada em guias.</span><span class="sxs-lookup"><span data-stu-id="85130-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="85130-243">A maioria das guias corresponde às etapas no [Processo da Ciência de Dados](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como carregar os dados ou explorá-los.</span><span class="sxs-lookup"><span data-stu-id="85130-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="85130-244">O processo da ciência de dados flui da esquerda para a direita nas guias.</span><span class="sxs-lookup"><span data-stu-id="85130-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="85130-245">Mas a última guia contém um log dos comandos do R executados pelo Rattle.</span><span class="sxs-lookup"><span data-stu-id="85130-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="85130-246">Para carregar e configurar o conjunto de dados:</span><span class="sxs-lookup"><span data-stu-id="85130-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="85130-247">Para carregar o arquivo, selecione a guia **Dados** , em seguida,</span><span class="sxs-lookup"><span data-stu-id="85130-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="85130-248">Escolha o seletor ao lado do **Nome de arquivo** e escolha **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="85130-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="85130-249">Para carregar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="85130-249">To load the file.</span></span> <span data-ttu-id="85130-250">selecione **Executar** na linha superior de botões.</span><span class="sxs-lookup"><span data-stu-id="85130-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="85130-251">Você deve ver um resumo de cada coluna, incluindo o tipo de dados identificado, se é uma entrada, um destino ou outro tipo de variável, e o número de valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="85130-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="85130-252">O Rattle identifica corretamente a coluna de **spam** como o destino.</span><span class="sxs-lookup"><span data-stu-id="85130-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="85130-253">Selecione a coluna de spam e defina o **Tipo de Dados de Destino** para **Categórico**.</span><span class="sxs-lookup"><span data-stu-id="85130-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="85130-254">Para explorar os dados:</span><span class="sxs-lookup"><span data-stu-id="85130-254">To explore the data:</span></span>

* <span data-ttu-id="85130-255">Selecione a guia **Explorar** .</span><span class="sxs-lookup"><span data-stu-id="85130-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="85130-256">Clique em **Resumo** e em **Executar** para ver algumas informações sobre os tipos de variáveis e algumas estatísticas resumidas.</span><span class="sxs-lookup"><span data-stu-id="85130-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="85130-257">Para exibir os outros tipos de estatísticas sobre cada variável, selecione outras opções, como **Descrever** ou **Básico**.</span><span class="sxs-lookup"><span data-stu-id="85130-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="85130-258">A guia **Explorar** também permite gerar várias plotagens criteriosas.</span><span class="sxs-lookup"><span data-stu-id="85130-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="85130-259">Para plotar um histograma dos dados:</span><span class="sxs-lookup"><span data-stu-id="85130-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="85130-260">Selecione **Distribuições**.</span><span class="sxs-lookup"><span data-stu-id="85130-260">Select **Distributions**.</span></span>
* <span data-ttu-id="85130-261">Verifique o **Histograma** quanto a **word_freq_remove** e **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="85130-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="85130-262">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="85130-262">Select **Execute**.</span></span> <span data-ttu-id="85130-263">Você deverá ver duas plotagens de densidade em uma janela de gráfico, na qual fica claro que a palavra "you" aparece com muito mais frequência nos emails que "remove".</span><span class="sxs-lookup"><span data-stu-id="85130-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="85130-264">As plotagens de correlação também são interessantes.</span><span class="sxs-lookup"><span data-stu-id="85130-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="85130-265">Para criar uma:</span><span class="sxs-lookup"><span data-stu-id="85130-265">To create one:</span></span>

* <span data-ttu-id="85130-266">Escolha **Correlação** como o **Tipo** e</span><span class="sxs-lookup"><span data-stu-id="85130-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="85130-267">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="85130-267">Select **Execute**.</span></span>
* <span data-ttu-id="85130-268">O Rattle avisa que ele recomenda um máximo de 40 variáveis.</span><span class="sxs-lookup"><span data-stu-id="85130-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="85130-269">Selecione **Sim** para exibir a plotagem.</span><span class="sxs-lookup"><span data-stu-id="85130-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="85130-270">Há algumas correlações interessantes que surgem: "tecnologia" é muito correlacionado a "HP" e "laboratórios", por exemplo.</span><span class="sxs-lookup"><span data-stu-id="85130-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="85130-271">Também está muito correlacionado a "650", porque o código de área dos doadores do conjunto de dados é 650.</span><span class="sxs-lookup"><span data-stu-id="85130-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="85130-272">Os valores numéricos para as correlações entre as palavras estão disponíveis na janela Explorar.</span><span class="sxs-lookup"><span data-stu-id="85130-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="85130-273">É interessante observar, por exemplo, que "tecnologia" está negativamente correlacionado a "seu" e "dinheiro".</span><span class="sxs-lookup"><span data-stu-id="85130-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="85130-274">O Rattle pode transformar o conjunto de dados para lidar com alguns problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="85130-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="85130-275">Por exemplo, ele permite que você redimensione os recursos, atribua os valores ausentes, lide com os valores atípicos e remova as variáveis ou observações sem dados.</span><span class="sxs-lookup"><span data-stu-id="85130-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="85130-276">O Rattle também pode identificar regras de associação entre as observações e/ou variáveis.</span><span class="sxs-lookup"><span data-stu-id="85130-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="85130-277">Essas guias estão fora do escopo deste passo a passo de introdução.</span><span class="sxs-lookup"><span data-stu-id="85130-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="85130-278">O Rattle também pode executar a análise de cluster.</span><span class="sxs-lookup"><span data-stu-id="85130-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="85130-279">Iremos excluir alguns recursos para facilitar a leitura da saída.</span><span class="sxs-lookup"><span data-stu-id="85130-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="85130-280">Na guia **Dados**, escolha **Ignorar** ao lado de cada uma das variáveis, exceto esses 10 itens:</span><span class="sxs-lookup"><span data-stu-id="85130-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="85130-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="85130-281">word_freq_hp</span></span>
* <span data-ttu-id="85130-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="85130-282">word_freq_technology</span></span>
* <span data-ttu-id="85130-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="85130-283">word_freq_george</span></span>
* <span data-ttu-id="85130-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="85130-284">word_freq_remove</span></span>
* <span data-ttu-id="85130-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="85130-285">word_freq_your</span></span>
* <span data-ttu-id="85130-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="85130-286">word_freq_dollar</span></span>
* <span data-ttu-id="85130-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="85130-287">word_freq_money</span></span>
* <span data-ttu-id="85130-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="85130-288">capital_run_length_longest</span></span>
* <span data-ttu-id="85130-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="85130-289">word_freq_business</span></span>
* <span data-ttu-id="85130-290">spam</span><span class="sxs-lookup"><span data-stu-id="85130-290">spam</span></span>

<span data-ttu-id="85130-291">Em seguida, vá para a guia **Cluster**, escolha **KMeans** e defina o *Número de clusters* para 4.</span><span class="sxs-lookup"><span data-stu-id="85130-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="85130-292">Então, **Executar**.</span><span class="sxs-lookup"><span data-stu-id="85130-292">Then **Execute**.</span></span> <span data-ttu-id="85130-293">Os resultados são exibidos na janela de saída.</span><span class="sxs-lookup"><span data-stu-id="85130-293">The results are displayed in the output window.</span></span> <span data-ttu-id="85130-294">Um cluster tem alta frequência de "george" e "hp", e provavelmente é um email corporativo legítimo.</span><span class="sxs-lookup"><span data-stu-id="85130-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="85130-295">Para compilar um modelo de aprendizado de máquina da árvore de decisão simples:</span><span class="sxs-lookup"><span data-stu-id="85130-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="85130-296">Selecione a guia **Modelo** ,</span><span class="sxs-lookup"><span data-stu-id="85130-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="85130-297">Escolha **Árvore** como o **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="85130-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="85130-298">Selecione **Executar** para exibir a árvore em formato de texto na janela de saída.</span><span class="sxs-lookup"><span data-stu-id="85130-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="85130-299">Selecione o botão **Desenhar** para exibir uma versão gráfica.</span><span class="sxs-lookup"><span data-stu-id="85130-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="85130-300">Isto é bastante semelhante à árvore obtida anteriormente usando *rpart*.</span><span class="sxs-lookup"><span data-stu-id="85130-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="85130-301">Um dos recursos interessantes do Rattle é sua capacidade de executar vários métodos de aprendizado de máquina e avaliá-los rapidamente.</span><span class="sxs-lookup"><span data-stu-id="85130-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="85130-302">Este é o procedimento:</span><span class="sxs-lookup"><span data-stu-id="85130-302">Here is the procedure:</span></span>

* <span data-ttu-id="85130-303">Escolha **Todos** para o **Tipo**.</span><span class="sxs-lookup"><span data-stu-id="85130-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="85130-304">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="85130-304">Select **Execute**.</span></span>
* <span data-ttu-id="85130-305">Depois de concluir, você pode clicar em qualquer **Tipo**, como **SVM**, e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="85130-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="85130-306">Você também pode comparar o desempenho dos modelos no conjunto de validação usando a guia **Avaliar** . Por exemplo, a seleção **Matriz do Erro** mostra a matriz de confusão, erro geral e erro de classe média para cada modelo no conjunto de validação.</span><span class="sxs-lookup"><span data-stu-id="85130-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="85130-307">Você também pode plotar as curvas ROC, executar a análise de sensibilidade e fazer outros tipos de avaliações do modelo.</span><span class="sxs-lookup"><span data-stu-id="85130-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="85130-308">Após terminar de compilar os modelos, selecione a guia **Log** para exibir o código do R executado pelo Rattle durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="85130-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="85130-309">Você pode selecionar o botão **Exportar** para salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="85130-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="85130-310">Há um bug na versão atual do Rattle.</span><span class="sxs-lookup"><span data-stu-id="85130-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="85130-311">Para modificar o script ou usá-lo para repetir as etapas posteriormente, você deve inserir um caractere # na frente de *Exportar este log... * no texto do log.</span><span class="sxs-lookup"><span data-stu-id="85130-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="85130-312">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="85130-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="85130-313">A DSVM vem com o PostgreSQL instalado.</span><span class="sxs-lookup"><span data-stu-id="85130-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="85130-314">O PostgreSQL é um banco de dados relacional sofisticado de fonte aberta.</span><span class="sxs-lookup"><span data-stu-id="85130-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="85130-315">Esta seção mostra como carregar nosso conjunto de dados de spam no PostgreSQL e consultá-lo.</span><span class="sxs-lookup"><span data-stu-id="85130-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="85130-316">Antes de carregar os dados, você precisa permitir a autenticação de senha a partir do host local.</span><span class="sxs-lookup"><span data-stu-id="85130-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="85130-317">Em um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="85130-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="85130-318">Na parte inferior do arquivo de configuração, há várias linhas que detalham as conexões permitidas:</span><span class="sxs-lookup"><span data-stu-id="85130-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="85130-319">Altere a linha "conexões locais IPv4" para usar md5 em vez de ident, para que possamos fazer logon usando um nome de usuário e senha:</span><span class="sxs-lookup"><span data-stu-id="85130-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="85130-320">E reinicie o serviço postgres:</span><span class="sxs-lookup"><span data-stu-id="85130-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="85130-321">Para iniciar o psql, um terminal interativo do PostgreSQL, como o usuário postgres interno, execute o seguinte comando em um prompt:</span><span class="sxs-lookup"><span data-stu-id="85130-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="85130-322">Crie uma nova conta de usuário, usando o mesmo nome de usuário da conta do Linux com a qual você está conectado no momento, e atribua uma senha:</span><span class="sxs-lookup"><span data-stu-id="85130-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="85130-323">Então, faça logon no psql como seu usuário:</span><span class="sxs-lookup"><span data-stu-id="85130-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="85130-324">E importe os dados para um novo banco de dados:</span><span class="sxs-lookup"><span data-stu-id="85130-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="85130-325">Agora, iremos explorar os dados e executar algumas consultas usando o **Squirrel SQL**, uma ferramenta gráfica que permite interagir com os bancos de dados por meio de um driver JDBC.</span><span class="sxs-lookup"><span data-stu-id="85130-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="85130-326">Para começar, inicie o Squirrel SQL no menu Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="85130-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="85130-327">Para configurar o driver:</span><span class="sxs-lookup"><span data-stu-id="85130-327">To set up the driver:</span></span>

* <span data-ttu-id="85130-328">Selecione **Windows** e **Exibir Drivers**.</span><span class="sxs-lookup"><span data-stu-id="85130-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="85130-329">Clique com o botão direito do mouse em **PostgreSQL** e selecione **Modificar Driver**.</span><span class="sxs-lookup"><span data-stu-id="85130-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="85130-330">Selecione **Caminho de classe Extra** e **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="85130-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="85130-331">Digite ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para o **Nome de Arquivo** e</span><span class="sxs-lookup"><span data-stu-id="85130-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="85130-332">Selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="85130-332">Select **Open**.</span></span>
* <span data-ttu-id="85130-333">Escolha Listar Drivers e selecione **org.postgresql.Driver** no **Nome da Classe** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="85130-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="85130-334">Para configurar a conexão com o servidor local:</span><span class="sxs-lookup"><span data-stu-id="85130-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="85130-335">Selecione **Windows** e **Exibir Aliases.**</span><span class="sxs-lookup"><span data-stu-id="85130-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="85130-336">Escolha o botão **+** para criar um novo alias.</span><span class="sxs-lookup"><span data-stu-id="85130-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="85130-337">Nomeie-o como *Banco de dados de spam* e escolha **PostgreSQL** na lista suspensa **Driver**.</span><span class="sxs-lookup"><span data-stu-id="85130-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="85130-338">Define a URL como *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="85130-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="85130-339">Insira seu *nome de usuário* e *senha*.</span><span class="sxs-lookup"><span data-stu-id="85130-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="85130-340">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="85130-340">Click **OK**.</span></span>
* <span data-ttu-id="85130-341">Para abrir a janela **Conexão**, clique duas vezes no alias do ***Banco de dados de spam***.</span><span class="sxs-lookup"><span data-stu-id="85130-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="85130-342">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="85130-342">Select **Connect**.</span></span>

<span data-ttu-id="85130-343">Para executar algumas consultas:</span><span class="sxs-lookup"><span data-stu-id="85130-343">To run some queries:</span></span>

* <span data-ttu-id="85130-344">Selecione a guia **SQL** .</span><span class="sxs-lookup"><span data-stu-id="85130-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="85130-345">Insira uma consulta simples, como `SELECT * from data;` , na caixa de texto da consulta na parte superior da guia SQL.</span><span class="sxs-lookup"><span data-stu-id="85130-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="85130-346">Pressione **Ctrl-Enter** para executá-la.</span><span class="sxs-lookup"><span data-stu-id="85130-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="85130-347">Por padrão, o Squirrel SQL retorna as primeiras 100 linhas de sua consulta.</span><span class="sxs-lookup"><span data-stu-id="85130-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="85130-348">Há muito mais consultas que você pode executar para explorar esses dados.</span><span class="sxs-lookup"><span data-stu-id="85130-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="85130-349">Por exemplo, como a frequência da palavra *make* difere entre o spam e o ham?</span><span class="sxs-lookup"><span data-stu-id="85130-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="85130-350">Ou quais são as características de email que geralmente contêm *3º*?</span><span class="sxs-lookup"><span data-stu-id="85130-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="85130-351">A maioria dos emails com uma alta ocorrência de *3º* aparentemente é spam, portanto, pode ser um recurso útil para compilar um modelo de previsão para classificar os emails.</span><span class="sxs-lookup"><span data-stu-id="85130-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="85130-352">Se você quiser executar o aprendizado de máquina com os dados armazenados em um banco de dados PostgreSQL, considere usar o [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="85130-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="85130-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="85130-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="85130-354">O SQL Data Warehouse do Azure é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="85130-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="85130-355">Para obter mais informações, consulte [O que é Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="85130-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="85130-356">Para conectar o data warehouse e criar a tabela, execute o seguinte comando em um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="85130-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="85130-357">Em seguida, no prompt do sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="85130-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="85130-358">Copie os dados com o bcp:</span><span class="sxs-lookup"><span data-stu-id="85130-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="85130-359">As terminações de linha no arquivo baixado estão no estilo Windows, mas o bcp espera o estilo UNIX, portanto, precisamos informar isso ao bcp com o sinalizador -r.</span><span class="sxs-lookup"><span data-stu-id="85130-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="85130-360">E consulte com o sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="85130-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="85130-361">Você também pode consultar com o Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="85130-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="85130-362">Siga as etapas semelhantes para o PostgreSQL, usando o Driver JDBC do Microsoft MSSQL Server, que pode ser encontrado em ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="85130-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85130-363">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85130-363">Next steps</span></span>
<span data-ttu-id="85130-364">Para obter uma visão geral dos tópicos que explicam as tarefas que compõem o processo de Ciência de dados no Azure, confira [Processo de Ciência de Dados de Equipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="85130-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="85130-365">Para obter uma descrição de outras orientações de ponta a ponta que demonstram as etapas no Processo da Ciência de Dados de Equipe para cenários específicos, consulte [Explicações Passo a Passo do Processo da Ciência de Dados de Equipe](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="85130-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="85130-366">As orientações também mostram como combinar ferramentas e serviços de nuvem e locais em um fluxo de trabalho ou pipeline para criar um aplicativo inteligente.</span><span class="sxs-lookup"><span data-stu-id="85130-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
