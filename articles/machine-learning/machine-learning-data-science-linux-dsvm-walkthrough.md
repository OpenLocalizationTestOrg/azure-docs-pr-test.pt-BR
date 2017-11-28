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
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="23298-103">Ciência de dados em Olá máquina de Virtual de ciência de dados do Linux</span><span class="sxs-lookup"><span data-stu-id="23298-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="23298-104">Este passo a passo mostra como tooperform ciência de dados comum várias tarefas com hello VM de ciência de dados do Linux.</span><span class="sxs-lookup"><span data-stu-id="23298-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="23298-105">saudação de máquina Virtual de ciência de dados de Linux (DSVM) é uma imagem de máquina virtual disponível no Azure que é instalado com uma coleção de ferramentas usadas para análise de dados e aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="23298-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="23298-106">componentes de software chave Olá são discriminados em Olá [Olá provisionar máquina de Virtual de ciência de dados do Linux](machine-learning-data-science-linux-dsvm-intro.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="23298-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="23298-107">Olá imagem VM torna fácil tooget iniciado fazendo ciência de dados em minutos, sem ter que tooinstall e configurar cada uma das ferramentas de saudação individualmente.</span><span class="sxs-lookup"><span data-stu-id="23298-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="23298-108">Você pode facilmente aumentar Olá VM, se necessário e interrompê-lo quando não estiver em uso.</span><span class="sxs-lookup"><span data-stu-id="23298-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="23298-109">Portanto, esse recurso é elástico e econômico.</span><span class="sxs-lookup"><span data-stu-id="23298-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="23298-110">Hello, demonstradas neste passo a passo de tarefas de ciência de dados siga etapas de saudação descritas em Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="23298-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="23298-111">Esse processo fornece uma ciência toodata abordagem sistemática que permite às equipes de tooeffectively colaborar Olá ciclo de vida de criação de aplicativos inteligentes os cientistas de dados.</span><span class="sxs-lookup"><span data-stu-id="23298-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="23298-112">o processo de ciência de dados Olá também fornece uma estrutura iterativa para ciência de dados que pode ser seguida por um indivíduo.</span><span class="sxs-lookup"><span data-stu-id="23298-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="23298-113">Analisamos Olá [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de dados neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="23298-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="23298-114">Este é um conjunto de endereços de email que são marcados como spam ou ham (ou seja, eles não são spam), e também contém algumas estatísticas sobre conteúdo Olá Olá emails.</span><span class="sxs-lookup"><span data-stu-id="23298-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="23298-115">estatísticas de saudação incluídas são discutidas em Olá lado mas uma seção.</span><span class="sxs-lookup"><span data-stu-id="23298-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23298-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="23298-116">Prerequisites</span></span>
<span data-ttu-id="23298-117">Antes de usar uma máquina Virtual de ciência de dados de Linux, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="23298-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="23298-118">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="23298-118">An **Azure subscription**.</span></span> <span data-ttu-id="23298-119">Se você não tiver uma, consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="23298-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="23298-120">Uma [**VM da ciência de dados do Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="23298-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="23298-121">Para obter informações sobre o provisionamento essa VM, consulte [Olá provisionar máquina de Virtual de ciência de dados do Linux](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="23298-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="23298-122">[X2Go](http://wiki.x2go.org/doku.php) instalado em seu computador e aberto em uma sessão XFCE.</span><span class="sxs-lookup"><span data-stu-id="23298-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="23298-123">Para obter informações sobre como instalar e configurar um **cliente X2Go**, confira [Instalando e configurando o cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="23298-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="23298-124">Uma **conta do AzureML**.</span><span class="sxs-lookup"><span data-stu-id="23298-124">An **AzureML account**.</span></span> <span data-ttu-id="23298-125">Se você ainda não tiver uma, inscreva-se para uma nova no hello [home page do AzureML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="23298-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="23298-126">Há um toohelp de nível de uso livre começar.</span><span class="sxs-lookup"><span data-stu-id="23298-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="23298-127">Baixar o conjunto de dados do hello spambase</span><span class="sxs-lookup"><span data-stu-id="23298-127">Download hello spambase dataset</span></span>
<span data-ttu-id="23298-128">Olá [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de dados é um conjunto de dados que contém somente 4601 exemplos relativamente pequeno.</span><span class="sxs-lookup"><span data-stu-id="23298-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="23298-129">Este é um tamanho conveniente toouse quando demonstrando que alguns dos recursos chave Olá Olá VM de ciência de dados que mantém os requisitos de recursos de saudação modesto.</span><span class="sxs-lookup"><span data-stu-id="23298-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-130">Este passo a passo foi criado em Máquina Virtual da Ciência de Dados do Linux de tamanho D2 v2.</span><span class="sxs-lookup"><span data-stu-id="23298-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="23298-131">Esse tamanho DSVM é capaz de manipular procedimentos Olá neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="23298-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="23298-132">Se você precisar de mais espaço de armazenamento, você pode criar discos adicionais e anexá-los tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="23298-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="23298-133">Esses discos usam armazenamento persistente do Azure, para que seus dados são preservados mesmo quando o servidor de saudação for reprovisionada vencimento tooresizing ou está desligado.</span><span class="sxs-lookup"><span data-stu-id="23298-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="23298-134">tooadd um disco e anexá-lo tooyour VM, siga as instruções de saudação em [adicionar um disco tooa VM Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23298-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="23298-135">Essas etapas usam hello Azure de linha de comando CLI (Interface do Azure), que já está instalado no hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="23298-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="23298-136">Para esses procedimentos podem ser feitos inteiramente do hello própria máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23298-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="23298-137">Outra opção de armazenamento de tooincrease é toouse [arquivos do Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="23298-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="23298-138">dados de saudação toodownload, abra uma janela do terminal e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="23298-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="23298-139">o arquivo baixado Olá não tem uma linha de cabeçalho, vamos criar outro arquivo que tem um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="23298-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="23298-140">Execute este comando toocreate um arquivo com cabeçalhos apropriados Olá:</span><span class="sxs-lookup"><span data-stu-id="23298-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="23298-141">Em seguida, concatene dois arquivos Olá junto com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="23298-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="23298-142">Olá dataset tem vários tipos de estatísticas sobre cada email:</span><span class="sxs-lookup"><span data-stu-id="23298-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="23298-143">Colunas como ***word\_freq\_WORD*** indicar porcentagem Olá de palavras no email de saudação que correspondem *WORD*.</span><span class="sxs-lookup"><span data-stu-id="23298-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="23298-144">Por exemplo, se *word\_freq\_fazer* for 1, 1% de todas as palavras no email Olá foram *fazer*.</span><span class="sxs-lookup"><span data-stu-id="23298-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="23298-145">Colunas como ***char\_freq\_CHAR*** indicar porcentagem Olá de todos os caracteres no email Olá foram *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="23298-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="23298-146">***capital\_executar\_comprimento\_mais longa*** é Olá o período mais longo de uma sequência de letras maiusculas.</span><span class="sxs-lookup"><span data-stu-id="23298-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="23298-147">***capital\_executar\_comprimento\_médio*** é Olá médio de todas as sequências de letras maiusculas.</span><span class="sxs-lookup"><span data-stu-id="23298-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="23298-148">***capital\_executar\_comprimento\_total*** é Olá o comprimento total de todas as sequências de letras maiusculas.</span><span class="sxs-lookup"><span data-stu-id="23298-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="23298-149">***spam*** indica se o email de saudação foi considerado spam ou não (1 = spam, 0 = não spam).</span><span class="sxs-lookup"><span data-stu-id="23298-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="23298-150">Explorar Olá conjunto de dados com o Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="23298-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="23298-151">Vamos examinar dados hello e faça o aprendizado de máquina básica com r. Olá VM de ciência de dados vem com [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pré-instalado.</span><span class="sxs-lookup"><span data-stu-id="23298-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="23298-152">Hello bibliotecas matemáticas multithread nesta versão do R oferecem melhor desempenho de várias versões de thread único.</span><span class="sxs-lookup"><span data-stu-id="23298-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="23298-153">Microsoft R Open também fornece reprodução usando um instantâneo do repositório de pacotes CRAN hello.</span><span class="sxs-lookup"><span data-stu-id="23298-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="23298-154">exemplos usados neste passo a passo, Olá clone de código de tooget cópias de saudação **Azure-Machine-aprendizado--ciência de dados** repositório usando o git, que é instalado em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="23298-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="23298-155">Na linha de comando git hello, execute:</span><span class="sxs-lookup"><span data-stu-id="23298-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="23298-156">Abra uma janela do terminal e iniciar uma nova sessão de R com um console interativo Olá R.</span><span class="sxs-lookup"><span data-stu-id="23298-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-157">Você também pode usar o RStudio para Olá procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="23298-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="23298-158">tooinstall RStudio, execute este comando em um terminal:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="23298-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="23298-159">dados de saudação tooimport e configure o ambiente hello, execute:</span><span class="sxs-lookup"><span data-stu-id="23298-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="23298-160">toosee estatísticas de resumo sobre cada coluna:</span><span class="sxs-lookup"><span data-stu-id="23298-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="23298-161">Para obter uma exibição diferente dos dados saudação:</span><span class="sxs-lookup"><span data-stu-id="23298-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="23298-162">Isso mostra Olá tipo de cada variável e primeiro Olá alguns valores no conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="23298-163">Olá *spam* coluna foi lido como um número inteiro, mas é realmente um categóricos variável (ou fator).</span><span class="sxs-lookup"><span data-stu-id="23298-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="23298-164">tooset seu tipo:</span><span class="sxs-lookup"><span data-stu-id="23298-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="23298-165">toodo algumas análises EXPLORATÓRIAS, use Olá [ggplot2](http://ggplot2.org/) do pacote, uma biblioteca de gráfica popular para R Olá VM já está instalado.</span><span class="sxs-lookup"><span data-stu-id="23298-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="23298-166">Observe que, de dados resumidos Olá exibida anteriormente, que temos as estatísticas de resumo sobre a frequência de saudação do caractere de ponto de exclamação hello.</span><span class="sxs-lookup"><span data-stu-id="23298-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="23298-167">Vamos plotar as frequências aqui com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="23298-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="23298-168">Desde que a barra de saudação zero é inclinação plotagem Olá, vamos eliminá-lo:</span><span class="sxs-lookup"><span data-stu-id="23298-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="23298-169">Há uma densidade não trivial acima de 1 parece interessante.</span><span class="sxs-lookup"><span data-stu-id="23298-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="23298-170">Vejamos apenas os dados:</span><span class="sxs-lookup"><span data-stu-id="23298-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="23298-171">Em seguida, divida por ham vs. spam:</span><span class="sxs-lookup"><span data-stu-id="23298-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="23298-172">Estes exemplos devem permitir que você plotagens semelhante de toomake da saudação tooexplore outras colunas Olá dados neles contidos.</span><span class="sxs-lookup"><span data-stu-id="23298-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="23298-173">Treinar e testar um modelo de AM</span><span class="sxs-lookup"><span data-stu-id="23298-173">Train and test an ML model</span></span>
<span data-ttu-id="23298-174">Agora vamos treinar um par de aprendizado de máquina modelos de emails de saudação tooclassify no conjunto de dados hello como contendo um span ou ham.</span><span class="sxs-lookup"><span data-stu-id="23298-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="23298-175">Treinamos um modelo da árvore de decisão e um modelo de floresta aleatória nesta seção, então, testamos sua precisão das previsões.</span><span class="sxs-lookup"><span data-stu-id="23298-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-176">pacote de rpart (particionamento recursivo e árvores de regressão) de saudação usado em Olá código a seguir já está instalado em Olá VM de ciência de dados.</span><span class="sxs-lookup"><span data-stu-id="23298-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="23298-177">Primeiro, vamos dividir o conjunto de dados de saudação em conjuntos de treinamento e teste:</span><span class="sxs-lookup"><span data-stu-id="23298-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="23298-178">E, em seguida, crie uma saudação de tooclassify de árvore de decisão emails.</span><span class="sxs-lookup"><span data-stu-id="23298-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="23298-179">Este é o resultado de saudação:</span><span class="sxs-lookup"><span data-stu-id="23298-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="23298-181">toodetermine como ele executa no treinamento de saudação definido, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="23298-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="23298-182">toodetermine como ele executa no conjunto de teste de saudação:</span><span class="sxs-lookup"><span data-stu-id="23298-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="23298-183">Também tentaremos um modelo de floresta aleatória.</span><span class="sxs-lookup"><span data-stu-id="23298-183">Let's also try a random forest model.</span></span> <span data-ttu-id="23298-184">Florestas aleatórias treinar uma infinidade de árvores de decisão e de saída de uma classe que é o modo de saudação do classificações Olá todas Olá individuais de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="23298-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="23298-185">Eles fornecem uma abordagem de aprendizado conforme eles corrigir para tendência de saudação de um toooverfit de modelo de árvore de decisão um conjunto de dados de treinamento de máquina mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="23298-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="23298-186">Implantar um modelo tooAzure ML</span><span class="sxs-lookup"><span data-stu-id="23298-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="23298-187">[O estúdio de aprendizado de máquina do Azure](https://studio.azureml.net/) (AzureML) é um serviço de nuvem que torna fácil toobuild e implanta modelos de análise de previsão.</span><span class="sxs-lookup"><span data-stu-id="23298-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="23298-188">Um dos recursos interessantes de saudação do AzureML é seu toopublish capacidade qualquer R funcionar como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="23298-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="23298-189">Olá pacote AzureML R faz toodo fácil implantação diretamente do nosso sessão R Olá DSVM.</span><span class="sxs-lookup"><span data-stu-id="23298-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="23298-190">toodeploy o código de árvore de decisão de Olá da seção anterior Olá, é necessário toosign em tooAzure estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="23298-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="23298-191">É necessário o ID do espaço de trabalho e um toosign de token de autorização no.</span><span class="sxs-lookup"><span data-stu-id="23298-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="23298-192">toofind esses valores e inicializar Olá AzureML variáveis com eles:</span><span class="sxs-lookup"><span data-stu-id="23298-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="23298-193">Selecione **configurações** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="23298-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="23298-194">Observe a **ID do ESPAÇO DE TRABALHO**.</span><span class="sxs-lookup"><span data-stu-id="23298-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="23298-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="23298-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="23298-196">Selecione **Tokens de autorização** de menu sobrecarga hello e anote seu **primário Token de autorização**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="23298-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="23298-197">Saudação de carga **AzureML** do pacote e, em seguida, definir valores de variáveis de saudação com sua ID de token e o espaço de trabalho em sua sessão de R em Olá DSVM:</span><span class="sxs-lookup"><span data-stu-id="23298-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="23298-198">Vamos simplificar Olá modelo toomake este tooimplement mais fácil de demonstração.</span><span class="sxs-lookup"><span data-stu-id="23298-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="23298-199">Escolha Olá três variáveis em Olá decisão mais próximo toohello raiz da árvore e criar uma nova árvore usando apenas as três variáveis:</span><span class="sxs-lookup"><span data-stu-id="23298-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="23298-200">Precisamos de uma função de previsão que usa recursos hello como entrada e retorna Olá valores previstos:</span><span class="sxs-lookup"><span data-stu-id="23298-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="23298-201">Publicar Olá predictSpam função tooAzureML usando Olá **publishWebService** função:</span><span class="sxs-lookup"><span data-stu-id="23298-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="23298-202">Essa função usa Olá **predictSpam** funcionar, cria um serviço web denominado **spamWebService** com definido entradas e saídas e retorna informações sobre o novo ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="23298-203">Exibir detalhes da saudação publicado serviço da web, incluindo suas chaves de acesso e o ponto de extremidade de API com o comando hello:</span><span class="sxs-lookup"><span data-stu-id="23298-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="23298-204">tootry-out em Olá primeiras 10 linhas do conjunto de teste de saudação:</span><span class="sxs-lookup"><span data-stu-id="23298-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="23298-205">Usar outras ferramentas disponíveis</span><span class="sxs-lookup"><span data-stu-id="23298-205">Use other tools available</span></span>
<span data-ttu-id="23298-206">seções restantes Olá mostram como toouse algumas ferramentas Olá instaladas em Olá VM de ciência de dados do Linux. Aqui está a lista de saudação de ferramentas abordadas:</span><span class="sxs-lookup"><span data-stu-id="23298-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="23298-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="23298-207">XGBoost</span></span>
* <span data-ttu-id="23298-208">Python</span><span class="sxs-lookup"><span data-stu-id="23298-208">Python</span></span>
* <span data-ttu-id="23298-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="23298-209">Jupyterhub</span></span>
* <span data-ttu-id="23298-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="23298-210">Rattle</span></span>
* <span data-ttu-id="23298-211">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="23298-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="23298-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="23298-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="23298-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="23298-213">XGBoost</span></span>
<span data-ttu-id="23298-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) : uma ferramenta que fornece implementação de árvore aumentada rápida e precisa.</span><span class="sxs-lookup"><span data-stu-id="23298-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="23298-215">O XGBoost também pode chamar a partir do python ou de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="23298-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="23298-216">Python</span><span class="sxs-lookup"><span data-stu-id="23298-216">Python</span></span>
<span data-ttu-id="23298-217">Para o desenvolvimento com Python, distribuições de Python Anaconda Olá 2.7 e 3.5 foram instaladas em Olá DSVM.</span><span class="sxs-lookup"><span data-stu-id="23298-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-218">Olá distribuição Anaconda inclui [Condas](http://conda.pydata.org/docs/index.html), que pode ser usado toocreate ambientes personalizados para Python com versões diferentes e/ou pacotes instalados.</span><span class="sxs-lookup"><span data-stu-id="23298-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="23298-219">Vamos leitura em algumas Olá spambase dataset e classificar emails Olá com máquinas de vetor de suporte em scikit-Saiba mais:</span><span class="sxs-lookup"><span data-stu-id="23298-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="23298-220">previsões de toomake:</span><span class="sxs-lookup"><span data-stu-id="23298-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="23298-221">tooshow como toopublish um ponto de extremidade AzureML, vamos criar um modelo mais simples Olá três variáveis como fizemos quando publicamos modelo Olá R anteriormente.</span><span class="sxs-lookup"><span data-stu-id="23298-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="23298-222">toopublish Olá modelo tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="23298-222">toopublish hello model tooAzureML:</span></span>

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
> <span data-ttu-id="23298-223">Isso só está disponível para o python 2.7 e ainda não é suportado na versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="23298-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="23298-224">Execute com **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="23298-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="23298-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="23298-225">Jupyterhub</span></span>
<span data-ttu-id="23298-226">distribuição da Anaconda Olá no hello DSVM vem com um bloco de anotações do Jupyter, um ambiente de plataforma cruzada tooshare Python, R ou Julia código e análise.</span><span class="sxs-lookup"><span data-stu-id="23298-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="23298-227">anotações do Jupyter Olá é acessada por meio de JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="23298-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="23298-228">Você entra usando seu nome de usuário local do Linux e a senha em ***https://\<nome DNS da VM ou Endereço IP\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="23298-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="23298-229">Todos os arquivos de configuração para o JupyterHub são encontrados no diretório **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="23298-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="23298-230">Vários blocos de anotações de exemplo já estão instalados no hello VM:</span><span class="sxs-lookup"><span data-stu-id="23298-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="23298-231">Consulte Olá [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) para um bloco de anotações do Python de exemplo.</span><span class="sxs-lookup"><span data-stu-id="23298-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="23298-232">Consulte o [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para obter um bloco de anotações do **R** de exemplo.</span><span class="sxs-lookup"><span data-stu-id="23298-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="23298-233">Consulte Olá [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para obter outro exemplo **Python** notebook.</span><span class="sxs-lookup"><span data-stu-id="23298-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-234">Olá idioma Julia também está disponível na linha de comando Olá Olá VM de ciência de dados do Linux.</span><span class="sxs-lookup"><span data-stu-id="23298-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="23298-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="23298-235">Rattle</span></span>
<span data-ttu-id="23298-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (Olá ferramenta analíticos R tooLearn facilmente) é uma ferramenta gráfica de R para mineração de dados.</span><span class="sxs-lookup"><span data-stu-id="23298-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="23298-237">Ele tem uma interface intuitiva que torna mais fácil tooload, explorar e transformar dados e criar e avaliar modelos.</span><span class="sxs-lookup"><span data-stu-id="23298-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="23298-238">artigo Olá [Rattle: A Data Mining GUI para R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fornece um passo a passo que demonstre seus recursos.</span><span class="sxs-lookup"><span data-stu-id="23298-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="23298-239">Instale e inicie chocalho com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="23298-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="23298-240">Instalação não é necessária em Olá DSVM.</span><span class="sxs-lookup"><span data-stu-id="23298-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="23298-241">Mas chocalho pode solicitar pacotes adicionais tooinstall ao ser carregado.</span><span class="sxs-lookup"><span data-stu-id="23298-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="23298-242">O Rattle usa uma interface baseada em guias.</span><span class="sxs-lookup"><span data-stu-id="23298-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="23298-243">A maioria das guias Olá corresponde toosteps em Olá [processo de ciência de dados](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como o carregamento de dados ou explorá-la.</span><span class="sxs-lookup"><span data-stu-id="23298-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="23298-244">processo de ciência de dados Olá flui da esquerda tooright pelas guias de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="23298-245">Mas a guia última Olá contém um log de comandos Olá R executando chocalho.</span><span class="sxs-lookup"><span data-stu-id="23298-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="23298-246">tooload e configurar o conjunto de dados hello:</span><span class="sxs-lookup"><span data-stu-id="23298-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="23298-247">arquivo de saudação tooload, selecione Olá **dados** guia, em seguida,</span><span class="sxs-lookup"><span data-stu-id="23298-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="23298-248">Escolha o seletor de saudação Avançar muito**Filename** e escolha **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="23298-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="23298-249">arquivo de saudação tooload.</span><span class="sxs-lookup"><span data-stu-id="23298-249">tooload hello file.</span></span> <span data-ttu-id="23298-250">Selecione **Execute** linha superior de saudação de botões.</span><span class="sxs-lookup"><span data-stu-id="23298-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="23298-251">Você deve ver um resumo de cada coluna, incluindo seu tipo de dados identificado, se ele é uma entrada, um destino ou outro tipo de variável e o número de saudação de valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="23298-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="23298-252">Chocalho identificar corretamente Olá **spam** coluna como destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="23298-253">Coluna de spam selecione hello, em seguida, Olá conjunto **tipo de dados de destino** muito**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="23298-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="23298-254">dados de saudação tooexplore:</span><span class="sxs-lookup"><span data-stu-id="23298-254">tooexplore hello data:</span></span>

* <span data-ttu-id="23298-255">Selecione Olá **explorar** guia.</span><span class="sxs-lookup"><span data-stu-id="23298-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="23298-256">Clique em **resumo**, em seguida, **Execute**, toosee algumas informações sobre os tipos de variáveis hello e algumas estatísticas de resumo.</span><span class="sxs-lookup"><span data-stu-id="23298-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="23298-257">tooview outros tipos de estatísticas sobre cada variável, selecione outras opções como **descrever** ou **Noções básicas de**.</span><span class="sxs-lookup"><span data-stu-id="23298-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="23298-258">Olá **explorar** guia também permite que você toogenerate muitos criteriosos plota.</span><span class="sxs-lookup"><span data-stu-id="23298-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="23298-259">tooplot um histograma dos dados saudação:</span><span class="sxs-lookup"><span data-stu-id="23298-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="23298-260">Selecione **Distribuições**.</span><span class="sxs-lookup"><span data-stu-id="23298-260">Select **Distributions**.</span></span>
* <span data-ttu-id="23298-261">Verifique o **Histograma** quanto a **word_freq_remove** e **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="23298-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="23298-262">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="23298-262">Select **Execute**.</span></span> <span data-ttu-id="23298-263">Você deverá ver que dois densidade plota em uma janela de gráfico único, onde ele está criptografado palavra hello "você" é exibido com mais frequência nos emails de "remover".</span><span class="sxs-lookup"><span data-stu-id="23298-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="23298-264">gráficos de correlação Olá também são interessantes.</span><span class="sxs-lookup"><span data-stu-id="23298-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="23298-265">toocreate um:</span><span class="sxs-lookup"><span data-stu-id="23298-265">toocreate one:</span></span>

* <span data-ttu-id="23298-266">Escolha **correlação** como Olá **tipo**, em seguida,</span><span class="sxs-lookup"><span data-stu-id="23298-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="23298-267">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="23298-267">Select **Execute**.</span></span>
* <span data-ttu-id="23298-268">O Rattle avisa que ele recomenda um máximo de 40 variáveis.</span><span class="sxs-lookup"><span data-stu-id="23298-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="23298-269">Selecione **Sim** tooview plotagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="23298-270">Há alguns correlações interessantes que surgirem: "tecnologia" é fortemente correlacionada muito "HP" e "laboratórios", por exemplo.</span><span class="sxs-lookup"><span data-stu-id="23298-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="23298-271">Ele é também fortemente correlacionado muito "650", como código de área de saudação de doadores de conjunto de dados de saudação é 650.</span><span class="sxs-lookup"><span data-stu-id="23298-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="23298-272">valores numéricos Olá correlações Olá entre palavras estão disponíveis na janela de explorar hello.</span><span class="sxs-lookup"><span data-stu-id="23298-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="23298-273">É interessante toonote, por exemplo, se "tecnologia" negativamente correlacionada com "a" e "money".</span><span class="sxs-lookup"><span data-stu-id="23298-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="23298-274">Chocalho pode transformar Olá dataset toohandle alguns problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="23298-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="23298-275">Por exemplo, ele permite que você toorescale recursos, imputar valores ausentes, manipular exceções e remova variáveis ou observações com dados ausentes.</span><span class="sxs-lookup"><span data-stu-id="23298-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="23298-276">O Rattle também pode identificar regras de associação entre as observações e/ou variáveis.</span><span class="sxs-lookup"><span data-stu-id="23298-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="23298-277">Essas guias estão fora do escopo deste passo a passo de introdução.</span><span class="sxs-lookup"><span data-stu-id="23298-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="23298-278">O Rattle também pode executar a análise de cluster.</span><span class="sxs-lookup"><span data-stu-id="23298-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="23298-279">Vamos excluir alguns recursos toomake Olá saída mais fácil tooread.</span><span class="sxs-lookup"><span data-stu-id="23298-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="23298-280">Em Olá **dados** guia, escolha **ignorar** tooeach próximo de variáveis de saudação exceto esses dez itens:</span><span class="sxs-lookup"><span data-stu-id="23298-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="23298-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="23298-281">word_freq_hp</span></span>
* <span data-ttu-id="23298-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="23298-282">word_freq_technology</span></span>
* <span data-ttu-id="23298-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="23298-283">word_freq_george</span></span>
* <span data-ttu-id="23298-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="23298-284">word_freq_remove</span></span>
* <span data-ttu-id="23298-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="23298-285">word_freq_your</span></span>
* <span data-ttu-id="23298-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="23298-286">word_freq_dollar</span></span>
* <span data-ttu-id="23298-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="23298-287">word_freq_money</span></span>
* <span data-ttu-id="23298-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="23298-288">capital_run_length_longest</span></span>
* <span data-ttu-id="23298-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="23298-289">word_freq_business</span></span>
* <span data-ttu-id="23298-290">spam</span><span class="sxs-lookup"><span data-stu-id="23298-290">spam</span></span>

<span data-ttu-id="23298-291">Vá toohello **Cluster** guia, escolha **KMeans**e conjunto hello *número de clusters* too4.</span><span class="sxs-lookup"><span data-stu-id="23298-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="23298-292">Então, **Executar**.</span><span class="sxs-lookup"><span data-stu-id="23298-292">Then **Execute**.</span></span> <span data-ttu-id="23298-293">Olá resultados são exibidos na janela de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="23298-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="23298-294">Um cluster tem alta frequência de "george" e "hp", e provavelmente é um email corporativo legítimo.</span><span class="sxs-lookup"><span data-stu-id="23298-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="23298-295">toobuild um modelo de aprendizado de máquina de árvore de decisão simples:</span><span class="sxs-lookup"><span data-stu-id="23298-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="23298-296">Selecione Olá **modelo** guia</span><span class="sxs-lookup"><span data-stu-id="23298-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="23298-297">Escolha **árvore** como Olá **tipo**.</span><span class="sxs-lookup"><span data-stu-id="23298-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="23298-298">Selecione **Execute** toodisplay árvore de saudação em formato de texto de saudação de janela de saída.</span><span class="sxs-lookup"><span data-stu-id="23298-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="23298-299">Selecione Olá **desenhar** botão tooview uma versão de gráfica.</span><span class="sxs-lookup"><span data-stu-id="23298-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="23298-300">Isso é bastante semelhante árvore toohello são obtidos anteriormente usando *rpart*.</span><span class="sxs-lookup"><span data-stu-id="23298-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="23298-301">Um dos recursos interessantes de saudação do chocalho é toorun sua capacidade de aprendizado de máquina vários métodos e avaliá-los rapidamente.</span><span class="sxs-lookup"><span data-stu-id="23298-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="23298-302">Aqui está o procedimento hello:</span><span class="sxs-lookup"><span data-stu-id="23298-302">Here is hello procedure:</span></span>

* <span data-ttu-id="23298-303">Escolha **todos os** para Olá **tipo**.</span><span class="sxs-lookup"><span data-stu-id="23298-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="23298-304">Selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="23298-304">Select **Execute**.</span></span>
* <span data-ttu-id="23298-305">Depois de concluir a você pode clicar em qualquer único **tipo**, como **SVM**e exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="23298-306">Você também pode comparar o desempenho de saudação dos modelos de saudação na validação de saudação definido usando Olá **avaliar** guia. Por exemplo, Olá **erro matriz** seleção mostra matriz de confusão hello, erro geral e erro de média de classe para cada modelo no conjunto de validação de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="23298-307">Você também pode plotar as curvas ROC, executar a análise de sensibilidade e fazer outros tipos de avaliações do modelo.</span><span class="sxs-lookup"><span data-stu-id="23298-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="23298-308">Quando você terminar de criar modelos, selecione Olá **Log** guia tooview código de saudação R executando chocalho durante a sessão.</span><span class="sxs-lookup"><span data-stu-id="23298-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="23298-309">Você pode selecionar Olá **exportar** botão toosave-lo.</span><span class="sxs-lookup"><span data-stu-id="23298-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="23298-310">Há um bug na versão atual do Rattle.</span><span class="sxs-lookup"><span data-stu-id="23298-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="23298-311">toomodify Olá script ou usá-lo toorepeat suas etapas mais tarde, você deve inserir um caractere # na frente do * exportar este log... * no texto de saudação do log de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="23298-312">PostgreSQL e Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="23298-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="23298-313">Olá DSVM vem com PostgreSQL instalado.</span><span class="sxs-lookup"><span data-stu-id="23298-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="23298-314">O PostgreSQL é um banco de dados relacional sofisticado de fonte aberta.</span><span class="sxs-lookup"><span data-stu-id="23298-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="23298-315">Esta seção mostra como tooload nosso conjunto de dados de spam em PostgreSQL e, em seguida, consultá-los.</span><span class="sxs-lookup"><span data-stu-id="23298-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="23298-316">Antes de carregar dados Olá, é necessário tooallow de autenticação de senha de saudação localhost.</span><span class="sxs-lookup"><span data-stu-id="23298-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="23298-317">Em um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="23298-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="23298-318">Inferior Olá Olá do arquivo de configuração são várias linhas que detalham Olá conexões permitida:</span><span class="sxs-lookup"><span data-stu-id="23298-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="23298-319">Alterar hello "IPv4 conexões locais" linha toouse md5 em vez de ident, para que possa se conectar usando um nome de usuário e senha:</span><span class="sxs-lookup"><span data-stu-id="23298-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="23298-320">E reiniciar o serviço de postgres hello:</span><span class="sxs-lookup"><span data-stu-id="23298-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="23298-321">toolaunch psql, um terminal interativo para PostgreSQL, como usuário de postgres internos Olá, execute Olá comando a seguir em um prompt:</span><span class="sxs-lookup"><span data-stu-id="23298-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="23298-322">Criar uma nova conta de usuário, usando Olá o mesmo nome de usuário como Olá conta Linux que você está conectado no momento como e atribua a ele uma senha:</span><span class="sxs-lookup"><span data-stu-id="23298-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="23298-323">Faça logon toopsql como usuário:</span><span class="sxs-lookup"><span data-stu-id="23298-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="23298-324">E importar dados de saudação para um novo banco de dados:</span><span class="sxs-lookup"><span data-stu-id="23298-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="23298-325">Agora, vamos explorar dados hello e execute algumas consultas usando **SQL esquilo**, uma ferramenta gráfica que permite interagir com bancos de dados por meio de um driver JDBC.</span><span class="sxs-lookup"><span data-stu-id="23298-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="23298-326">tooget iniciado, inicie o SQL esquilo no menu de aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23298-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="23298-327">tooset driver hello:</span><span class="sxs-lookup"><span data-stu-id="23298-327">tooset up hello driver:</span></span>

* <span data-ttu-id="23298-328">Selecione **Windows** e **Exibir Drivers**.</span><span class="sxs-lookup"><span data-stu-id="23298-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="23298-329">Clique com o botão direito do mouse em **PostgreSQL** e selecione **Modificar Driver**.</span><span class="sxs-lookup"><span data-stu-id="23298-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="23298-330">Selecione **Caminho de classe Extra** e **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="23298-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="23298-331">Digite ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para Olá **nome de arquivo** e</span><span class="sxs-lookup"><span data-stu-id="23298-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="23298-332">Selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="23298-332">Select **Open**.</span></span>
* <span data-ttu-id="23298-333">Escolha Listar Drivers e selecione **org.postgresql.Driver** no **Nome da Classe** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="23298-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="23298-334">tooset o servidor local do toohello Olá conexão:</span><span class="sxs-lookup"><span data-stu-id="23298-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="23298-335">Selecione **Windows** e **Exibir Aliases.**</span><span class="sxs-lookup"><span data-stu-id="23298-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="23298-336">Escolha Olá  **+**  toomake botão um novo alias.</span><span class="sxs-lookup"><span data-stu-id="23298-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="23298-337">Nomeie- *banco de dados de Spam*, escolha **PostgreSQL** em Olá **Driver** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="23298-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="23298-338">Definir a URL de saudação muito*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="23298-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="23298-339">Insira seu *nome de usuário* e *senha*.</span><span class="sxs-lookup"><span data-stu-id="23298-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="23298-340">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="23298-340">Click **OK**.</span></span>
* <span data-ttu-id="23298-341">Olá tooopen **Conexão** janela, clique duas vezes em Olá ***banco de dados de Spam*** alias.</span><span class="sxs-lookup"><span data-stu-id="23298-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="23298-342">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="23298-342">Select **Connect**.</span></span>

<span data-ttu-id="23298-343">toorun algumas consultas:</span><span class="sxs-lookup"><span data-stu-id="23298-343">toorun some queries:</span></span>

* <span data-ttu-id="23298-344">Selecione Olá **SQL** guia.</span><span class="sxs-lookup"><span data-stu-id="23298-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="23298-345">Insira uma consulta simples como `SELECT * from data;` na caixa de texto de consulta de saudação na parte superior de saudação do guia SQL hello.</span><span class="sxs-lookup"><span data-stu-id="23298-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="23298-346">Pressione **Ctrl-Enter** toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="23298-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="23298-347">Por padrão SQL esquilo retorna Olá primeiras 100 linhas de sua consulta.</span><span class="sxs-lookup"><span data-stu-id="23298-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="23298-348">Há muitas consultas mais que você pode executar tooexplore esses dados.</span><span class="sxs-lookup"><span data-stu-id="23298-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="23298-349">Por exemplo, como faz Olá frequência da palavra hello *fazer* diferem spam ham?</span><span class="sxs-lookup"><span data-stu-id="23298-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="23298-350">Ou quais são as características de saudação do email que normalmente contêm *3d*?</span><span class="sxs-lookup"><span data-stu-id="23298-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="23298-351">A maioria dos emails que têm uma ocorrência alta *3d* aparentemente são spam, poderia ser um recurso útil para a criação de uma saudação do modelo de previsão tooclassify emails.</span><span class="sxs-lookup"><span data-stu-id="23298-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="23298-352">Se você quisesse tooperform aprendizado de máquina com dados armazenados em um banco de dados PostgreSQL, considere o uso de [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="23298-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="23298-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="23298-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="23298-354">O SQL Data Warehouse do Azure é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="23298-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="23298-355">Para obter mais informações, consulte [O que é Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="23298-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="23298-356">tooconnect toohello data warehouse e cria tabela hello, comando a seguir Olá execução de um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="23298-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="23298-357">No prompt de sqlcmd hello:</span><span class="sxs-lookup"><span data-stu-id="23298-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="23298-358">Copie os dados com o bcp:</span><span class="sxs-lookup"><span data-stu-id="23298-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="23298-359">terminações de linha de saudação no arquivo baixado Olá são estilo do Windows, mas bcp espera estilo UNIX, por isso, precisamos bcp tootell que com hello sinalizador - r.</span><span class="sxs-lookup"><span data-stu-id="23298-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="23298-360">E consulte com o sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="23298-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="23298-361">Você também pode consultar com o Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="23298-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="23298-362">Siga as etapas semelhantes para PostgreSQL, usando Olá Microsoft MSSQL Server JDBC Driver, que pode ser encontrado em ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="23298-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23298-363">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="23298-363">Next steps</span></span>
<span data-ttu-id="23298-364">Para obter uma visão geral dos tópicos que orientam você pelas tarefas de saudação que compõem o processo de ciência de dados Olá no Azure, consulte [processo de ciência de dados de equipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="23298-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="23298-365">Para obter uma descrição de outras orientações de ponta a ponta que demonstram etapas Olá Olá processo de ciência de dados de equipe para cenários específicos, consulte [explicações passo a passo do processo de ciência de dados de equipe](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="23298-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="23298-366">Olá explicações passo a passo também ilustra como toocombine de nuvem e ferramentas no local e serviços em um fluxo de trabalho ou pipeline toocreate um aplicativo inteligente.</span><span class="sxs-lookup"><span data-stu-id="23298-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
