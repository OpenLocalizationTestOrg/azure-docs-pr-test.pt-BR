---
title: "tutorial aaaQuickstart linguagem R para o aprendizado de máquina | Microsoft Docs"
description: "Use este tutorial tooget iniciado rapidamente usando o idioma Olá R com o estúdio de aprendizado de máquina do Azure toocreate uma solução de previsão de programação de R."
keywords: "guia de início rápido, linguagem r, linguagem de programação r, tutorial de programação r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="93573-104">Tutorial de início rápido para a linguagem de programação Olá R para o aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="93573-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="93573-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="93573-105">Introduction</span></span>
<span data-ttu-id="93573-106">Este tutorial de início rápido ajuda você a iniciar rapidamente estendendo o aprendizado de máquina do Azure usando a linguagem de programação Olá R.</span><span class="sxs-lookup"><span data-stu-id="93573-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="93573-107">Siga este tutorial toocreate de programação de R, teste e execute o código R no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="93573-108">Conforme você trabalha com tutorial, você criará uma solução completa de previsão usando linguagem Olá R no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="93573-109">O Microsoft Azure Machine Learning contém muitos módulos poderosos de aprendizado de máquina e de manipulação de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="93573-110">linguagem R avançada de saudação tem sido descrita como Olá linguagem internacional de análise.</span><span class="sxs-lookup"><span data-stu-id="93573-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="93573-111">Felizmente, análise e manipulação de dados no aprendizado de máquina do Azure pode ser estendida por meio de R. Essa combinação fornece escalabilidade hello e facilidade de implantação de aprendizado de máquina do Azure com flexibilidade hello e análise detalhada do R.</span><span class="sxs-lookup"><span data-stu-id="93573-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="93573-112">Conjunto de dados de previsão e hello</span><span class="sxs-lookup"><span data-stu-id="93573-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="93573-113">A previsão é um método analítico amplamente empregado e bastante útil.</span><span class="sxs-lookup"><span data-stu-id="93573-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="93573-114">Intervalo de prever vendas sazonais, determinar níveis de estoque ideal variáveis macroeconomic toopredicting de usos comuns.</span><span class="sxs-lookup"><span data-stu-id="93573-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="93573-115">A previsão normalmente é feita com modelos de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="93573-116">Dados de série temporal são a data em que os valores hello tem um índice de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="93573-117">índice de tempo de saudação pode ser normal, por exemplo, a cada mês ou a cada minuto, ou irregulares.</span><span class="sxs-lookup"><span data-stu-id="93573-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="93573-118">Um modelo de série de tempo se baseia em dados de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-118">A time series model is based on time series data.</span></span> <span data-ttu-id="93573-119">linguagem de programação Olá R contém uma estrutura flexível e análise abrangente para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="93573-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="93573-120">Neste guia de início rápido, trabalharemos com a produção de derivados de leite e dados de preços na Califórnia.</span><span class="sxs-lookup"><span data-stu-id="93573-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="93573-121">Esses dados incluem informações mensais na produção de hello de vários Laticínios e preço Olá fat leite mercadoria um parâmetro de comparação.</span><span class="sxs-lookup"><span data-stu-id="93573-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="93573-122">Olá usados neste artigo, juntamente com scripts de R, os dados podem ser [baixado em][download].</span><span class="sxs-lookup"><span data-stu-id="93573-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="93573-123">Esses dados foi originalmente sintetizados das informações disponíveis da saudação Universidade de Wisconsin em http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="93573-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="93573-124">Organização</span><span class="sxs-lookup"><span data-stu-id="93573-124">Organization</span></span>
<span data-ttu-id="93573-125">Podemos será andamento por meio de várias etapas, você aprenderá como toocreate, testar e executar análises e dados de código de manipulação de R no ambiente de aprendizado de máquina do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="93573-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="93573-126">Primeiro, exploraremos Olá Noções básicas sobre usando linguagem de saudação R no ambiente do hello estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="93573-127">Em seguida, podemos progresso toodiscussing vários aspectos de e/s de dados, o código R e elementos gráficos no ambiente de aprendizado de máquina do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="93573-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="93573-128">É, em seguida, criará a primeira parte Olá da nossa solução previsão criando código para limpeza de dados e a transformação.</span><span class="sxs-lookup"><span data-stu-id="93573-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="93573-129">Com nossos dados preparados vamos realizar uma análise de correlações Olá entre várias variáveis de saudação em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="93573-130">Por fim, criaremos um modelo de previsão de série de tempos sazonais da produção de leite.</span><span class="sxs-lookup"><span data-stu-id="93573-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="93573-131">
            <a id="mlstudio">
            </a>Interagir com a linguagem R no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93573-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="93573-132">Esta seção descreve alguns aspectos de interação com a linguagem de programação Olá R no ambiente do estúdio de aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="93573-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="93573-133">linguagem de saudação R fornece uma ferramenta poderosa toocreate personalizado análises e dados de manipulação módulos no ambiente de aprendizado de máquina do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93573-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="93573-134">Vou usar RStudio toodevelop, testar e depurar código de R em pequena escala.</span><span class="sxs-lookup"><span data-stu-id="93573-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="93573-135">Esse código é, em seguida, recortar e colar em um [Executar Script R] [ execute-r-script] módulo no toorun pronto do estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="93573-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="93573-136">módulo de executar Script R Olá</span><span class="sxs-lookup"><span data-stu-id="93573-136">hello Execute R Script module</span></span>
<span data-ttu-id="93573-137">No estúdio de aprendizado de máquina, scripts de R são executados dentro de saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-138">Um exemplo de hello [Executar Script R] [ execute-r-script] módulo no estúdio de aprendizado de máquina é mostrado na Figura 1.</span><span class="sxs-lookup"><span data-stu-id="93573-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Linguagem de programação R: módulo Executar Script R de saudação selecionado no estúdio de aprendizado de máquina][1]

<span data-ttu-id="93573-140">*Figura 1. ambiente de estúdio de aprendizado de máquina Olá mostrando Olá Executar Script R módulo selecionado.*</span><span class="sxs-lookup"><span data-stu-id="93573-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="93573-141">Consultando tooFigure 1, vamos examinar algumas das partes principais de saudação do ambiente do estúdio de aprendizado de máquina Olá para trabalhar com hello [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="93573-142">módulos Olá experimento Olá são mostrados no painel de centro de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="93573-143">parte superior de saudação do painel direito da saudação contém um tooview de janela e editar seus scripts de R.</span><span class="sxs-lookup"><span data-stu-id="93573-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="93573-144">parte inferior de saudação do painel direito mostra algumas propriedades de saudação [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="93573-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="93573-145">Você pode exibir os logs de erro e a saída de hello clicando em pontos de saudação apropriado deste painel.</span><span class="sxs-lookup"><span data-stu-id="93573-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="93573-146">Obviamente, abordaremos Olá [Executar Script R] [ execute-r-script] mais detalhadamente no restante deste documento hello.</span><span class="sxs-lookup"><span data-stu-id="93573-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="93573-147">Ao trabalhar com funções R complexas, é recomendável que você edite, teste e depure no RStudio.</span><span class="sxs-lookup"><span data-stu-id="93573-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="93573-148">Assim como acontece com qualquer desenvolvimento de software, estenda o código de forma incremental e teste-o em pequenos casos de teste simples.</span><span class="sxs-lookup"><span data-stu-id="93573-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="93573-149">Recorte e cole as funções na janela de script hello R de saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-150">Essa abordagem permite que você tooharness Olá RStudio ambiente de desenvolvimento integrado (IDE) tanto Olá potência de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="93573-151">Executar código R</span><span class="sxs-lookup"><span data-stu-id="93573-151">Execute R code</span></span>
<span data-ttu-id="93573-152">Qualquer código de R Olá [Executar Script R] [ execute-r-script] módulo será executado quando você executar o teste de saudação clicando em Olá **executar** botão.</span><span class="sxs-lookup"><span data-stu-id="93573-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="93573-153">Quando a execução for concluída, uma marca de seleção aparecerá em Olá [Executar Script R] [ execute-r-script] ícone.</span><span class="sxs-lookup"><span data-stu-id="93573-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="93573-154">Codificação R defensiva para o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93573-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="93573-155">Se, por exemplo, estiver desenvolvendo código R para um serviço Web que usa o Azure Machine Learning, você definitivamente deverá planejar como seu código lidará com exceções e com entrada de dados inesperados.</span><span class="sxs-lookup"><span data-stu-id="93573-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="93573-156">toomaintain clareza, não incluí quase Olá forma de verificação ou a maioria dos exemplos de código Olá mostrados de tratamento de exceção.</span><span class="sxs-lookup"><span data-stu-id="93573-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="93573-157">No entanto, ao prosseguirmos, darei vários exemplos de funções usando o recurso de tratamento de exceção do R.</span><span class="sxs-lookup"><span data-stu-id="93573-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="93573-158">Se for necessário um tratamento mais completo de tratamento de exceção de R, recomendo ler seções aplicáveis de saudação de livro de saudação do Wickham listada na [Apêndice B - leitura adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="93573-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="93573-159">Depurar e testar R no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93573-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="93573-160">tooreiterate, é recomendável testar e depurar seu código R em pequena escala no RStudio.</span><span class="sxs-lookup"><span data-stu-id="93573-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="93573-161">No entanto, há casos em que você precisará tootrack problemas de código R no hello [Executar Script R] [ execute-r-script] em si.</span><span class="sxs-lookup"><span data-stu-id="93573-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="93573-162">Além disso, é uma boa prática toocheck os resultados no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="93573-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="93573-163">Saída da execução de saudação do seu código R e na plataforma de aprendizado de máquina do Azure Olá encontra-se principalmente na saída. log.</span><span class="sxs-lookup"><span data-stu-id="93573-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="93573-164">Algumas informações adicionais serão vistas no arquivo error.log.</span><span class="sxs-lookup"><span data-stu-id="93573-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="93573-165">Se ocorrer um erro no estúdio de aprendizado de máquina durante a execução do seu código R, o primeiro curso de ação deve ser toolook em Error.</span><span class="sxs-lookup"><span data-stu-id="93573-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="93573-166">Esse arquivo pode conter toohelp de mensagens de erro útil compreender e corrija o erro.</span><span class="sxs-lookup"><span data-stu-id="93573-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="93573-167">Error tooview, clique em **Exibir log do erro** em Olá **painel propriedades** para Olá [Executar Script R] [ execute-r-script] que contém o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="93573-168">Por exemplo, executei Olá seguinte código R, com uma variável y indefinido, em um [Executar Script R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="93573-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="93573-169">Este código falhará tooexecute, resultando em uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="93573-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="93573-170">Clicando em **Exibir log do erro** em Olá **painel propriedades** produz Olá exibição mostrada na Figura 2.</span><span class="sxs-lookup"><span data-stu-id="93573-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![A mensagem de erro é exibida][2]

<span data-ttu-id="93573-172">*Figura 2. Mensagem de erro pop-up.*</span><span class="sxs-lookup"><span data-stu-id="93573-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="93573-173">Parece que precisamos toolook na mensagem de erro la toosee Olá R.</span><span class="sxs-lookup"><span data-stu-id="93573-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="93573-174">Clique em Olá [Executar Script R] [ execute-r-script] e, em seguida, clique em Olá **exibi-la** item Olá **painel propriedades** toohello direita.</span><span class="sxs-lookup"><span data-stu-id="93573-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="93573-175">Abre uma nova janela do navegador e consulte o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="93573-176">Essa mensagem de erro contém sem surpresas e identifica claramente o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="93573-177">valor de saudação tooinspect de qualquer objeto em R, você pode imprimir o arquivo de saída. log esses valores toohello.</span><span class="sxs-lookup"><span data-stu-id="93573-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="93573-178">regras de saudação para examinar o objeto valores são essencialmente Olá mesmo como em uma sessão interativa de R.</span><span class="sxs-lookup"><span data-stu-id="93573-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="93573-179">Por exemplo, se você digitar um nome de variável em uma linha, o valor de saudação do objeto Olá será impressa toohello la arquivo.</span><span class="sxs-lookup"><span data-stu-id="93573-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="93573-180">Pacotes no Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="93573-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="93573-181">O Azure Machine Learning vem com mais de 350 pacotes de linguagem R pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="93573-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="93573-182">Você pode usar Olá Olá código a seguir [Executar Script R] [ execute-r-script] módulo tooretrieve uma lista de saudação pré-instalado pacotes.</span><span class="sxs-lookup"><span data-stu-id="93573-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="93573-183">Se você não entender a última linha hello deste código momento Olá, leia sobre.</span><span class="sxs-lookup"><span data-stu-id="93573-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="93573-184">No restante deste documento hello, discutiremos extensivamente usando R no ambiente de aprendizado de máquina do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93573-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="93573-185">Introdução tooRStudio</span><span class="sxs-lookup"><span data-stu-id="93573-185">Introduction tooRStudio</span></span>
<span data-ttu-id="93573-186">RStudio é um IDE amplamente utilizado para R. Vou usar RStudio para editar, testar e depurar algum código Olá R usado neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="93573-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="93573-187">Depois que o código de R é testado e pronto, você simplesmente recortar e colar do editor de RStudio Olá em um estúdio de aprendizado de máquina [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="93573-188">Se você não tiver a linguagem de programação Olá R instalada em seu computador desktop, é recomendável que você faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="93573-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="93573-189">Downloads gratuitos da linguagem R de software livre estão disponíveis em Olá rede de arquivamento abrangente de R (CRAN) em [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="93573-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="93573-190">Há downloads disponíveis para Windows, Mac OS e Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="93573-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="93573-191">Escolha um espelho próximo e siga as instruções de download de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="93573-192">Além disso, CRAN contém uma grande quantidade de pacotes de manipulação de dados e análise úteis.</span><span class="sxs-lookup"><span data-stu-id="93573-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="93573-193">Se você for novo tooRStudio, deve baixar e instalar a versão de área de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="93573-194">Você pode encontrar hello que rstudio downloads do Windows, Mac OS e UNIX/Linux em http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="93573-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="93573-195">Siga as direções de saudação fornecidas tooinstall RStudio em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="93573-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="93573-196">Uma introdução ao tutorial tooRStudio está disponível em https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="93573-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="93573-197">Forneço algumas informações adicionais sobre como usar o RStudio no [Apêndice A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="93573-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="93573-198"><a id="scriptmodule"></a>Obter dados dentro e fora do módulo Executar Script R de saudação</span><span class="sxs-lookup"><span data-stu-id="93573-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="93573-199">Nesta seção, discutiremos como obter dados dentro e fora de saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-200">Analisaremos como toohandle vários tipos de dados de leitura dentro e fora de saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="93573-201">código completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93573-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="93573-202">Carregar e verificar dados no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="93573-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="93573-203"><a id="loading"></a>Carregar conjunto de dados Olá</span><span class="sxs-lookup"><span data-stu-id="93573-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="93573-204">Começaremos Carregando Olá **csdairydata.csv** arquivo no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="93573-205">Inicie seu ambiente do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="93573-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="93573-206">Clique em **+ novo** em Olá inferior esquerdo da tela e selecione **conjunto de dados**.</span><span class="sxs-lookup"><span data-stu-id="93573-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="93573-207">Selecione **do arquivo Local**e, em seguida, **procurar** tooselect arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="93573-208">Verifique se você selecionou **arquivo CSV genérico com cabeçalho (. csv)** como tipo Olá Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="93573-209">Clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-209">Click hello check mark.</span></span>
* <span data-ttu-id="93573-210">Após Olá conjunto de dados foi carregado, você deve ver Olá novo conjunto de dados clicando em Olá **conjuntos de dados** guia.</span><span class="sxs-lookup"><span data-stu-id="93573-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="93573-211">Criar uma experiência</span><span class="sxs-lookup"><span data-stu-id="93573-211">Create an experiment</span></span>
<span data-ttu-id="93573-212">Agora que temos alguns dados no estúdio de aprendizado de máquina, é preciso toocreate uma análise de saudação do experimento toodo.</span><span class="sxs-lookup"><span data-stu-id="93573-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="93573-213">Clique em **+ novo** em Olá inferior esquerda e selecione **experimento**, em seguida, **experiência em branco**.</span><span class="sxs-lookup"><span data-stu-id="93573-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="93573-214">Você pode nomear sua experiência selecionando e modificando, Olá **experimento criado em...**  título na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="93573-215">Por exemplo, a alteração muito**AC Laticínios Analysis**.</span><span class="sxs-lookup"><span data-stu-id="93573-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="93573-216">Esquerda de saudação da página de teste hello, expanda **conjuntos de dados salvos**e, em seguida, **Meus conjuntos de dados**.</span><span class="sxs-lookup"><span data-stu-id="93573-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="93573-217">Você deve ver Olá **cadairydata.csv** que você carregou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93573-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="93573-218">Saudação de arrastar e soltar **csdairydata.csv dataset** no experimento hello.</span><span class="sxs-lookup"><span data-stu-id="93573-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="93573-219">Em Olá **pesquisa experimentar itens** caixa na parte superior de saudação do painel esquerdo hello, tipo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="93573-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="93573-220">Você verá o módulo de saudação aparecem na lista de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="93573-221">Saudação de arrastar e soltar [Executar Script R] [ execute-r-script] módulo na sua paleta.</span><span class="sxs-lookup"><span data-stu-id="93573-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="93573-222">Conecte a saída de saudação do hello **csdairydata.csv dataset** entrada mais à esquerda do toohello (**Dataset1**) de saudação [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="93573-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="93573-223">**Não se esqueça de tooclick em 'Salvar'!**</span><span class="sxs-lookup"><span data-stu-id="93573-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="93573-224">Agora seu teste deve ser similar a Figura 3.</span><span class="sxs-lookup"><span data-stu-id="93573-224">At this point your experiment should look something like Figure 3.</span></span>

![Olá AC Laticínios análise fazer experiências com o conjunto de dados e o módulo Executar Script R][3]

<span data-ttu-id="93573-226">*Figura 3. Olá AC Laticínios análise fazer experiências com o conjunto de dados e o módulo Executar Script R.*</span><span class="sxs-lookup"><span data-stu-id="93573-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="93573-227">Verificar dados saudação</span><span class="sxs-lookup"><span data-stu-id="93573-227">Check on hello data</span></span>
<span data-ttu-id="93573-228">Vamos dar uma olhada nos dados de saudação que carregou em nossa experiência.</span><span class="sxs-lookup"><span data-stu-id="93573-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="93573-229">Na experiência de hello, clique em saída Olá Olá **cadairydata.csv dataset** e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="93573-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="93573-230">Você deve ver algo semelhante à Figura 4.</span><span class="sxs-lookup"><span data-stu-id="93573-230">You should see something like Figure 4.</span></span>  

![Resumo do conjunto de dados de cadairydata.csv Olá][4]

<span data-ttu-id="93573-232">*Figura 4. Resumo do conjunto de dados de cadairydata.csv hello.*</span><span class="sxs-lookup"><span data-stu-id="93573-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="93573-233">Nessa exibição, vemos muitas informações úteis.</span><span class="sxs-lookup"><span data-stu-id="93573-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="93573-234">Podemos ver Olá primeiro várias linhas de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="93573-235">Se selecionamos uma coluna, Olá seção de estatísticas mostra mais informações sobre a coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="93573-236">Por exemplo, linha de tipo de recurso Olá mostra quais tipos de dados no estúdio de aprendizado de máquina do Azure atribuída toohello coluna.</span><span class="sxs-lookup"><span data-stu-id="93573-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="93573-237">É ter uma olhada rápida assim uma verificação de integridade válida antes de começar toodo qualquer trabalho sério.</span><span class="sxs-lookup"><span data-stu-id="93573-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="93573-238">Primeiro script R</span><span class="sxs-lookup"><span data-stu-id="93573-238">First R script</span></span>
<span data-ttu-id="93573-239">Vamos criar um simple tooexperiment de script R primeiro no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="93573-240">Posso ter criado e testado Olá RStudio script a seguir.</span><span class="sxs-lookup"><span data-stu-id="93573-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="93573-241">Agora, preciso tootransfer tooAzure esse script estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="93573-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="93573-242">Eu poderia simplesmente recortar e colar.</span><span class="sxs-lookup"><span data-stu-id="93573-242">I could simply cut and paste.</span></span> <span data-ttu-id="93573-243">No entanto, nesse caso, eu vou transferir o meu script R por meio de um arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="93573-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="93573-244">Módulo de executar Script R de toohello de entrada de dados</span><span class="sxs-lookup"><span data-stu-id="93573-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="93573-245">Vamos dar uma olhada nos Olá entradas toohello [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-246">Neste exemplo, lê dados Laticínios do hello Califórnia em Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="93573-247">Há três entradas possíveis para Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-248">Você pode usar qualquer uma ou todas essas entradas, dependendo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93573-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="93573-249">Também é perfeitamente razoável toouse um R script que não precisa de entrada em todos os.</span><span class="sxs-lookup"><span data-stu-id="93573-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="93573-250">Vamos dar uma olhada em cada um desses inputs, indo de tooright à esquerda.</span><span class="sxs-lookup"><span data-stu-id="93573-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="93573-251">Você pode ver os nomes de saudação de cada uma das entradas de saudação colocando o cursor sobre entrada hello e lendo a dica de ferramenta hello.</span><span class="sxs-lookup"><span data-stu-id="93573-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="93573-252">Pacote de script</span><span class="sxs-lookup"><span data-stu-id="93573-252">Script Bundle</span></span>
<span data-ttu-id="93573-253">Olá entrada de pacote de Script permite que você toopass Olá conteúdo de um arquivo zip em [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-254">Você pode usar uma saudação comandos tooread Olá conteúdo Olá zip arquivo a seguir em seu código R.</span><span class="sxs-lookup"><span data-stu-id="93573-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="93573-255">O aprendizado de máquina do Azure trata arquivos ZIP hello como se eles estão em Olá src / diretório, portanto, você precisa tooprefix nomeia o arquivo com este nome de diretório.</span><span class="sxs-lookup"><span data-stu-id="93573-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="93573-256">Por exemplo, se hello zip contém arquivos Olá `yourfile.R` e `yourData.rdata` na raiz de saudação do zip hello, endereço como `src/yourfile.R` e `src/yourData.rdata` ao usar `source` e `load`.</span><span class="sxs-lookup"><span data-stu-id="93573-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="93573-257">Já discutimos conjuntos de dados de carregamento no [Carregando conjunto de dados Olá](#loading).</span><span class="sxs-lookup"><span data-stu-id="93573-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="93573-258">Depois de ter criado e testado o script hello R mostrado na seção anterior hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="93573-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="93573-259">Salve o script hello R em um. Arquivo de R.</span><span class="sxs-lookup"><span data-stu-id="93573-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="93573-260">Eu chamo meu arquivo script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="93573-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="93573-261">Aqui está o conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="93573-262">Crie um arquivo zip e copie o script no arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="93573-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="93573-263">No Windows, clique com botão direito no arquivo hello e selecione **enviar para**e, em seguida, **pasta compactada**.</span><span class="sxs-lookup"><span data-stu-id="93573-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="93573-264">Isso criará um novo arquivo zip que contém hello "simpleplot. Arquivo de R".</span><span class="sxs-lookup"><span data-stu-id="93573-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="93573-265">Adicionar seu arquivo toohello **conjuntos de dados** no estúdio de aprendizado de máquina, especificando o tipo hello como **zip**.</span><span class="sxs-lookup"><span data-stu-id="93573-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="93573-266">Agora você deve ver o arquivo zip de saudação em seus conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="93573-267">Arrastar e soltar Olá zip no **conjuntos de dados** para Olá **tela ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="93573-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="93573-268">Conecte a saída de saudação do hello **zip dados** ícone toohello **pacote de Script** entrada de saudação [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="93573-269">Saudação de tipo `source()` função com o nome do arquivo zip na janela de código Olá para Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-270">No meu caso, digitei `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="93573-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="93573-271">Lembre-se de clicar em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="93573-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="93573-272">Quando essas etapas forem concluídas, Olá [Executar Script R] [ execute-r-script] módulo executará Olá R script no arquivo zip de saudação quando experimento Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="93573-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="93573-273">Agora seu teste deve ser semelhante à Figura 5.</span><span class="sxs-lookup"><span data-stu-id="93573-273">At this point your experiment should look something like Figure 5.</span></span>

![Teste usando o script de R compactado][6]

<span data-ttu-id="93573-275">*Figura 5. Experimente usar o R script compactado.*</span><span class="sxs-lookup"><span data-stu-id="93573-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="93573-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="93573-276">Dataset1</span></span>
<span data-ttu-id="93573-277">Você pode passar uma tabela retangular de código de tooyour R dados usando entrada hello Dataset1.</span><span class="sxs-lookup"><span data-stu-id="93573-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="93573-278">Em nosso Olá script simples `maml.mapInputPort(1)` função lê dados saudação da porta 1.</span><span class="sxs-lookup"><span data-stu-id="93573-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="93573-279">Esses dados, em seguida, são atribuídos o nome da variável dataframe tooa em seu código.</span><span class="sxs-lookup"><span data-stu-id="93573-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="93573-280">Em nosso script simple a primeira linha hello de código executa atribuição hello.</span><span class="sxs-lookup"><span data-stu-id="93573-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="93573-281">Execute seu teste clicando no hello **executar** botão.</span><span class="sxs-lookup"><span data-stu-id="93573-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="93573-282">Ao término da execução de saudação, clique em Olá [Executar Script R] [ execute-r-script] módulo e depois clique em **Exibir log de saída** no painel de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="93573-283">Uma nova página deve aparecer em seu navegador mostrando o conteúdo de saudação do arquivo de saída. log hello.</span><span class="sxs-lookup"><span data-stu-id="93573-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="93573-284">Quando você rolar para baixo, você verá algo parecido com hello seguinte.</span><span class="sxs-lookup"><span data-stu-id="93573-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="93573-285">Mais para baixo Olá página é informações mais detalhadas sobre colunas de saudação, que será parecida com a seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="93573-286">Esses resultados são principalmente conforme o esperado, com 228 observações e 9 colunas no dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="93573-287">Podemos ver os nomes de coluna hello, tipo de dados de saudação R e um exemplo de cada coluna.</span><span class="sxs-lookup"><span data-stu-id="93573-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="93573-288">Essa mesma impressão há convenientemente da saudação saída dispositivo R Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-289">Vamos discutir as saídas de saudação do hello [Executar Script R] [ execute-r-script] módulo na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="93573-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="93573-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="93573-290">Dataset2</span></span>
<span data-ttu-id="93573-291">Olá, comportamento de entrada hello Dataset2 é idêntico toothat de Dataset1.</span><span class="sxs-lookup"><span data-stu-id="93573-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="93573-292">Usando essa entrada, você pode passar uma segunda tabela retangular de dados para o seu código R.</span><span class="sxs-lookup"><span data-stu-id="93573-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="93573-293">Olá função `maml.mapInputPort(2)`, com argumento Olá 2, é usado toopass esses dados.</span><span class="sxs-lookup"><span data-stu-id="93573-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="93573-294">Execute as saídas do Script R</span><span class="sxs-lookup"><span data-stu-id="93573-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="93573-295">Exibir um dataframe</span><span class="sxs-lookup"><span data-stu-id="93573-295">Output a dataframe</span></span>
<span data-ttu-id="93573-296">Você pode extrair conteúdo de saudação de um dataframe de R como uma tabela retangular pela porta Olá Dataset1 resultado usando Olá `maml.mapOutputPort()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="93573-297">Em nosso script R simple, isso é feito por Olá linha a seguir.</span><span class="sxs-lookup"><span data-stu-id="93573-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="93573-298">Após a experiência de saudação em execução, clique em Olá porta de saída de resultado Dataset1 e, em seguida, clique em **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="93573-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="93573-299">Você deve ver algo como na Figura 6.</span><span class="sxs-lookup"><span data-stu-id="93573-299">You should see something like Figure 6.</span></span>

![visualização de saudação da saída de saudação do hello dados Laticínios Califórnia][7]

<span data-ttu-id="93573-301">*Figura 6. visualização de saudação da saída de saudação do hello dados Laticínios Califórnia.*</span><span class="sxs-lookup"><span data-stu-id="93573-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="93573-302">Esta saída é entrada toohello idênticos, exatamente como esperado.</span><span class="sxs-lookup"><span data-stu-id="93573-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="93573-303">Saída do Dispositivo R</span><span class="sxs-lookup"><span data-stu-id="93573-303">R Device output</span></span>
<span data-ttu-id="93573-304">Olá saída de dispositivo de hello [Executar Script R] [ execute-r-script] módulo contém a saída de mensagens e elementos gráficos.</span><span class="sxs-lookup"><span data-stu-id="93573-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="93573-305">As duas mensagens de erro padrão e de saída padrão de R são enviadas toohello dispositivo R porta de saída.</span><span class="sxs-lookup"><span data-stu-id="93573-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="93573-306">Olá tooview R dispositivo de saída, clique na porta hello e, em seguida, em **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="93573-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="93573-307">Podemos ver a saída de saudação padrão e erro padrão do script hello R na Figura 7.</span><span class="sxs-lookup"><span data-stu-id="93573-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Saída padrão e erro padrão de saudação porta dispositivo R][8]

<span data-ttu-id="93573-309">*Figura 7. Saída padrão e erro padrão de saudação porta do dispositivo de R.*</span><span class="sxs-lookup"><span data-stu-id="93573-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="93573-310">Rolando para baixo, consulte a saída de gráficos de saudação do nosso script R na Figura 8.</span><span class="sxs-lookup"><span data-stu-id="93573-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Saída de elementos gráficos da saudação porta dispositivo R][9]

<span data-ttu-id="93573-312">*Figura 8. Gráficos de saída de hello porta do dispositivo de R.*</span><span class="sxs-lookup"><span data-stu-id="93573-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="93573-313"><a id="filtering"></a>Filtragem de dados e transformação</span><span class="sxs-lookup"><span data-stu-id="93573-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="93573-314">Nesta seção vamos realizar algumas filtragem básica de dados e operações de transformação em Olá dados Laticínios Califórnia.</span><span class="sxs-lookup"><span data-stu-id="93573-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="93573-315">Ao final desta seção Olá teremos dados em um formato adequado para a criação de um modelo analítico.</span><span class="sxs-lookup"><span data-stu-id="93573-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="93573-316">Mais especificamente, nesta seção vamos executar várias tarefas de transformação e de limpeza de dados comuns: transformação de tipo, filtragem por dataframes, adição de novas colunas computadas e transformações de valor.</span><span class="sxs-lookup"><span data-stu-id="93573-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="93573-317">Este plano de fundo deve ajudá-lo a lidar com hello muitas variações em problemas do mundo real.</span><span class="sxs-lookup"><span data-stu-id="93573-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="93573-318">código de R completo Olá para essa seção está disponível no arquivo zip de saudação que você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93573-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="93573-319">Transformações de tipo</span><span class="sxs-lookup"><span data-stu-id="93573-319">Type transformations</span></span>
<span data-ttu-id="93573-320">Agora que nós pode ler dados de laticínios de Califórnia de Olá em código Olá Olá R [Executar Script R] [ execute-r-script] módulo, precisamos tooensure que dados Olá nas colunas de saudação tem tipo hello pretendido e o formato.</span><span class="sxs-lookup"><span data-stu-id="93573-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="93573-321">R é uma linguagem tipada dinamicamente, o que significa que os tipos de dados são forçados de um tooanother conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="93573-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="93573-322">tipos de dados atômico de saudação em R incluem numérica, lógica e de caractere.</span><span class="sxs-lookup"><span data-stu-id="93573-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="93573-323">tipo de fator de saudação é toocompactly usado armazenar dados categóricos.</span><span class="sxs-lookup"><span data-stu-id="93573-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="93573-324">Você pode encontrar mais informações sobre tipos de dados em referências de saudação em [Apêndice B - leituras](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="93573-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="93573-325">Quando dados de tabela é lido em R de uma fonte externa, é sempre uma saudação de toocheck boa ideia resultante tipos nas colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="93573-326">Você pode desejar uma coluna de tipo de caractere, mas em muitos casos isso aparecerá como fator ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="93573-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="93573-327">Em outros casos, uma coluna que você acha que deve ser numérica é representada por dados de caracteres, por exemplo, '1,23' em vez de 1,23 como número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="93573-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="93573-328">Felizmente, é fácil tooconvert um tipo tooanother, desde que o mapeamento é possível.</span><span class="sxs-lookup"><span data-stu-id="93573-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="93573-329">Por exemplo, não é possível converter 'Nevada' em um valor numérico, mas você pode converter tooa fator (variável categórica).</span><span class="sxs-lookup"><span data-stu-id="93573-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="93573-330">Um outro exemplo, você pode converter um numérico 1 em um caractere “1” ou um fator.</span><span class="sxs-lookup"><span data-stu-id="93573-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="93573-331">sintaxe de saudação para qualquer uma dessas conversões é simple: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="93573-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="93573-332">Essas funções de conversão de tipo incluem o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="93573-333">Observando os tipos de dados Olá Olá de colunas de nós entrada na seção anterior Olá: todas as colunas são do tipo numérico, exceto Olá coluna rotulada 'Month', que é o caractere de tipo.</span><span class="sxs-lookup"><span data-stu-id="93573-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="93573-334">Vamos converter esse fator tooa e Olá resultados de teste.</span><span class="sxs-lookup"><span data-stu-id="93573-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="93573-335">Posso ter excluído linha hello que criou a matriz de scatterplot hello e adicionou uma linha convertendo o fator de tooa de coluna de 'Month' hello.</span><span class="sxs-lookup"><span data-stu-id="93573-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="93573-336">Em minha experiência, apenas será recortar e colar o código Olá R na janela de código de saudação do hello [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="93573-337">Você também pode atualizar o arquivo zip de saudação e carregá-lo tooAzure estúdio de aprendizado de máquina, mas isso leva várias etapas.</span><span class="sxs-lookup"><span data-stu-id="93573-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="93573-338">Vamos executar esse código e examinar o log de saída Olá para Olá script R.</span><span class="sxs-lookup"><span data-stu-id="93573-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="93573-339">dados relevantes de saudação do log de saudação são mostrados na Figura 9.</span><span class="sxs-lookup"><span data-stu-id="93573-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="93573-340">*Figura 9. Resumo de dataframe de saudação com uma variável de fator.*</span><span class="sxs-lookup"><span data-stu-id="93573-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="93573-341">tipo de saudação do mês deve agora dizer '**fator com 14 níveis**'.</span><span class="sxs-lookup"><span data-stu-id="93573-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="93573-342">Este é um problema, já que há somente 12 meses no ano de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="93573-343">Você também pode verificar toosee que Olá tipo em **visualizar** de conjunto de dados de resultado de hello porta é '**categórico**'.</span><span class="sxs-lookup"><span data-stu-id="93573-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="93573-344">problema de saudação é que hello 'Month', coluna sistematicamente não foi codificada.</span><span class="sxs-lookup"><span data-stu-id="93573-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="93573-345">Em alguns casos, um mês é chamado de abril e, em outros, é abreviado como abril. É possível resolver esse problema, cortar caracteres de too3 de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="93573-346">linha de saudação de código agora Olá seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="93573-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="93573-347">Execute novamente o teste de saudação e exibir o log de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="93573-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="93573-348">Olá esperado de resultados são mostrados na Figura 10.</span><span class="sxs-lookup"><span data-stu-id="93573-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="93573-349">*Figura 10. Resumo de dataframe de saudação com o número correto de níveis de fator.*</span><span class="sxs-lookup"><span data-stu-id="93573-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="93573-350">Nossa variável fator agora tem 12 níveis de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="93573-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="93573-351">Filtragem de dataframe básico</span><span class="sxs-lookup"><span data-stu-id="93573-351">Basic data frame filtering</span></span>
<span data-ttu-id="93573-352">Os dataframes R oferecem suporte a recursos avançados de filtragem.</span><span class="sxs-lookup"><span data-stu-id="93573-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="93573-353">Conjuntos de dados podem ser subdivididos usando filtros lógicos em linhas ou colunas.</span><span class="sxs-lookup"><span data-stu-id="93573-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="93573-354">Em muitos casos, serão necessários critérios complexos de filtro.</span><span class="sxs-lookup"><span data-stu-id="93573-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="93573-355">Olá referências em [Apêndice B - leituras](#appendixb) contêm exemplos abrangentes de filtragem de quadros de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="93573-356">Há algumas filtragens que devemos fazer em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="93573-357">Se você observar colunas Olá Olá cadairydata dataframe, você verá duas colunas desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="93573-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="93573-358">coluna primeiro Olá contém apenas um número de linha, que não é muito útil.</span><span class="sxs-lookup"><span data-stu-id="93573-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="93573-359">Olá segunda coluna, Year.Month, contém informações redundantes.</span><span class="sxs-lookup"><span data-stu-id="93573-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="93573-360">Podemos facilmente pode excluir essas colunas usando Olá código R a seguir.</span><span class="sxs-lookup"><span data-stu-id="93573-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="93573-361">De agora nesta seção, vou apenas Mostrar você Olá código adicional que estou adicionando Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="93573-362">Vou adicionar cada nova linha **antes de** Olá `str()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="93573-363">Posso usar esta função tooverify os resultados no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="93573-364">Adicionar Olá após linha toomy R código em Olá [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="93573-365">Executar esse código em sua experiência e verificar o resultado de saudação do log de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="93573-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="93573-366">Esses resultados são mostrados na Figura 11.</span><span class="sxs-lookup"><span data-stu-id="93573-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="93573-367">*Figura 11. Resumo de dataframe de saudação com duas colunas é removido.*</span><span class="sxs-lookup"><span data-stu-id="93573-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="93573-368">Boas notícias!</span><span class="sxs-lookup"><span data-stu-id="93573-368">Good news!</span></span> <span data-ttu-id="93573-369">Podemos obter resultados Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="93573-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="93573-370">Adicionar uma nova coluna</span><span class="sxs-lookup"><span data-stu-id="93573-370">Add a new column</span></span>
<span data-ttu-id="93573-371">modelos de série temporal toocreate será conveniente toohave uma coluna que contém Olá meses desde o início de saudação do MTS hello.</span><span class="sxs-lookup"><span data-stu-id="93573-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="93573-372">Criaremos uma nova coluna “Month.Count”.</span><span class="sxs-lookup"><span data-stu-id="93573-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="93573-373">toohelp organizar código Olá vamos criar nossa primeira função simple, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="93573-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="93573-374">Em seguida, aplicaremos toocreate essa função uma nova coluna em dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="93573-375">Olá novo código é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="93573-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="93573-376">Agora execute experimento Olá atualizado e use Olá log tooview Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="93573-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="93573-377">Esses resultados são mostrados na Figura 12.</span><span class="sxs-lookup"><span data-stu-id="93573-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="93573-378">*Figura 12. Resumo de dataframe de saudação com coluna adicional hello.*</span><span class="sxs-lookup"><span data-stu-id="93573-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="93573-379">Parece que tudo está funcionando.</span><span class="sxs-lookup"><span data-stu-id="93573-379">It looks like everything is working.</span></span> <span data-ttu-id="93573-380">Temos a nova coluna Olá com valores esperados de saudação em nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="93573-381">Transformações de valor</span><span class="sxs-lookup"><span data-stu-id="93573-381">Value transformations</span></span>
<span data-ttu-id="93573-382">Nesta seção vamos realizar algumas transformações simples nos valores hello algumas das colunas de saudação do nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="93573-383">idioma Olá R suporta transformações de valor quase arbitrário.</span><span class="sxs-lookup"><span data-stu-id="93573-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="93573-384">Olá referências em [Apêndice B - leitura adicional](#appendixb) contêm exemplos extensivos.</span><span class="sxs-lookup"><span data-stu-id="93573-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="93573-385">Se você examinar os valores hello em resumos de saudação do nosso dataframe você verá algo ímpar aqui.</span><span class="sxs-lookup"><span data-stu-id="93573-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="93573-386">Há mais sorvetes do que leite produzido na Califórnia?</span><span class="sxs-lookup"><span data-stu-id="93573-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="93573-387">Não, claro não, pois isso faz sentido, sad como esse fato pode ser toosome de nós amantes sorvete.</span><span class="sxs-lookup"><span data-stu-id="93573-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="93573-388">unidades de saudação são diferentes.</span><span class="sxs-lookup"><span data-stu-id="93573-388">hello units are different.</span></span> <span data-ttu-id="93573-389">preço Hello está em unidades de nós libras, leite é em unidades de 1 milhão libras dos EUA, sorvete é em unidades de 1.000 nos galões e madeira de casa cheese está em unidades de libra de 1.000 dos EUA.</span><span class="sxs-lookup"><span data-stu-id="93573-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="93573-390">Supondo que sorvete pondera cerca de 6,5 libras por galão, podemos facilmente Olá multiplicação tooconvert esses valores para que eles estão todos em unidades iguais de libra 1.000.</span><span class="sxs-lookup"><span data-stu-id="93573-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="93573-391">Para nosso modelo de previsão, usamos um modelo de multiplicação para tendência e ajuste sazonal desses dados.</span><span class="sxs-lookup"><span data-stu-id="93573-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="93573-392">Uma transformação de log nos permite toouse um modelo linear, simplificar esse processo.</span><span class="sxs-lookup"><span data-stu-id="93573-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="93573-393">É possível aplicar transformação de log Olá no hello mesma função onde multiplicador Olá é aplicado.</span><span class="sxs-lookup"><span data-stu-id="93573-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="93573-394">Em Olá código a seguir, definir uma nova função, `log.transform()`e aplicá-lo toohello linhas contendo valores numéricos de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="93573-395">Olá R `Map()` função é usada tooapply Olá `log.transform()` função toohello selecionar colunas de dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="93573-396">`Map()`é muito semelhante`apply()` , mas permite que mais de uma lista de função de toohello de argumentos.</span><span class="sxs-lookup"><span data-stu-id="93573-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="93573-397">Observe que uma lista de multiplicadores fornece Olá segundo argumento toohello `log.transform()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="93573-398">Olá `na.omit()` função é usada como um pouco de limpeza tooensure não temos ausente ou indefinidos valores hello dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="93573-399">Há bastante aconteça bit no hello `log.transform()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="93573-400">A maioria desse código está verificando problemas potenciais com argumentos de saudação ou lidar com exceções, que ainda podem surgir durante os cálculos de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="93573-401">Apenas algumas linhas do código realmente Olá cálculos.</span><span class="sxs-lookup"><span data-stu-id="93573-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="93573-402">Olá objetivo programação defesa Olá é falha de saudação tooprevent de uma única função que impede o processamento de continuar.</span><span class="sxs-lookup"><span data-stu-id="93573-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="93573-403">Uma falha abrupta de uma análise de execução longa pode ser muito frustrante para os usuários.</span><span class="sxs-lookup"><span data-stu-id="93573-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="93573-404">tooavoid nessa situação, o padrão de valores de retorno devem ser escolhidos que limitará danificar toodownstream processamento.</span><span class="sxs-lookup"><span data-stu-id="93573-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="93573-405">Uma mensagem também é produzido tooalert usuários que algo deu errado.</span><span class="sxs-lookup"><span data-stu-id="93573-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="93573-406">Se você não estiver programação toodefensive usados em R, todo esse código pode parecer um pouco difícil.</span><span class="sxs-lookup"><span data-stu-id="93573-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="93573-407">Eu orientará você pelas etapas principais hello:</span><span class="sxs-lookup"><span data-stu-id="93573-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="93573-408">Um vetor de quatro mensagens é definido.</span><span class="sxs-lookup"><span data-stu-id="93573-408">A vector of four messages is defined.</span></span> <span data-ttu-id="93573-409">Essas mensagens são usadas toocommunicate informações sobre alguns Olá possíveis erros e exceções que podem ocorrer com este código.</span><span class="sxs-lookup"><span data-stu-id="93573-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="93573-410">Posso retornar um valor NA para cada caso.</span><span class="sxs-lookup"><span data-stu-id="93573-410">I return a value of NA for each case.</span></span> <span data-ttu-id="93573-411">Há muitas outras possibilidades que podem ter menos efeitos colaterais.</span><span class="sxs-lookup"><span data-stu-id="93573-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="93573-412">Pode retornar um vetor de zeros ou vetor de entrada original hello, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="93573-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="93573-413">Verificações são executadas na função de toohello hello argumentos.</span><span class="sxs-lookup"><span data-stu-id="93573-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="93573-414">Em cada caso, se for detectado um erro, será retornado um valor padrão e uma mensagem é produzida pelo Olá `warning()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="93573-415">Estou usando `warning()` em vez de `stop()` como Olá último terminará em execução, exatamente o que estou tentando tooavoid.</span><span class="sxs-lookup"><span data-stu-id="93573-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="93573-416">Observe que eu escrevi este código em um estilo de procedimento, pois nesse caso uma abordagem funcional me parece complexa e obscura.</span><span class="sxs-lookup"><span data-stu-id="93573-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="93573-417">cálculos de log Olá são encapsulados em `tryCatch()` para que as exceções não causará uma interrupção abrupto tooprocessing.</span><span class="sxs-lookup"><span data-stu-id="93573-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="93573-418">Sem `tryCatch()` , a maioria dos erros gerada pelas funções de R resulta em um sinal de interrupção, que faz exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="93573-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="93573-419">Execute esse código R em sua experiência e examinar Olá impressas saída no arquivo de saída. log hello.</span><span class="sxs-lookup"><span data-stu-id="93573-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="93573-420">Agora você verá valores hello transformado Olá quatro colunas na saudação de log, conforme mostrado na Figura 13.</span><span class="sxs-lookup"><span data-stu-id="93573-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="93573-421">*Figura 13. Resumo da saudação transformados valores hello dataframe.*</span><span class="sxs-lookup"><span data-stu-id="93573-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="93573-422">Podemos ver que foram transformados valores hello.</span><span class="sxs-lookup"><span data-stu-id="93573-422">We see hello values have been transformed.</span></span> <span data-ttu-id="93573-423">Agora, a produção de leite excede bastante a produção de todos os outros produtos derivados do leite, lembrando que agora estamos analisando uma escala logarítmica.</span><span class="sxs-lookup"><span data-stu-id="93573-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="93573-424">Neste momento, os dados são limpos e estamos prontos para a modelagem.</span><span class="sxs-lookup"><span data-stu-id="93573-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="93573-425">Observando a visualização de saudação resumida de Olá saído do conjunto de dados de resultado de nossa [Executar Script R] [ execute-r-script] módulo, você verá a coluna de 'Mês' hello é 'Categórico' com 12 valores exclusivos, novamente, assim como queremos .</span><span class="sxs-lookup"><span data-stu-id="93573-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="93573-426"><a id="timeseries"></a>Análise de correlação e objetos de série temporal</span><span class="sxs-lookup"><span data-stu-id="93573-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="93573-427">Nesta seção explorar alguns objetos básicos de série de tempo de R e analisar correlações Olá entre algumas das variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="93573-428">Nosso objetivo é toooutput um dataframe contendo Olá correlação emparelhadas informações em vários atrasos.</span><span class="sxs-lookup"><span data-stu-id="93573-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="93573-429">código de R completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93573-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="93573-430">Objetos de série temporal em R</span><span class="sxs-lookup"><span data-stu-id="93573-430">Time series objects in R</span></span>
<span data-ttu-id="93573-431">Como já mencionado, as série de tempo são uma série de valores de dados indexados por tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="93573-432">Objetos de série de tempo de R são usada toocreate e gerenciar o índice de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="93573-433">Há várias vantagens toousing tempo série objetos.</span><span class="sxs-lookup"><span data-stu-id="93573-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="93573-434">Objetos de série de tempo de liberá-lo da saudação muitos detalhes de gerenciamento Olá série índice valores de hora são encapsulados no objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="93573-435">Além disso, objetos de série de tempo permitem que você toouse Olá muitos métodos de série de tempo para plotar, impressão, modelagem, etc.</span><span class="sxs-lookup"><span data-stu-id="93573-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="93573-436">Olá POSIXct classe de série de tempo é comumente usado e é relativamente simple.</span><span class="sxs-lookup"><span data-stu-id="93573-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="93573-437">Essa classe de série de tempo mede o tempo do início de saudação da época hello, 1º de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="93573-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="93573-438">Vamos usar objetos de série de tempo POSIXct neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="93573-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="93573-439">Outras classes de objeto de série de tempo amplamente utilizados em R incluem zoo e xts, série temporal extensível.</span><span class="sxs-lookup"><span data-stu-id="93573-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="93573-440">Exemplo de objeto de série temporal</span><span class="sxs-lookup"><span data-stu-id="93573-440">Time series object example</span></span>
<span data-ttu-id="93573-441">Vamos começar com o nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="93573-441">Let's get started with our example.</span></span> <span data-ttu-id="93573-442">Arraste e solte um **novo** módulo [Executar Script R][execute-r-script] em seu experimento.</span><span class="sxs-lookup"><span data-stu-id="93573-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="93573-443">Conectar porta de saída Olá Dataset1 de resultado de saudação existentes [Executar Script R] [ execute-r-script] Olá nova porta de entrada do módulo toohello Dataset1 [Executar Script R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="93573-444">Como fiz exemplos primeiro Olá, como podemos andamento por meio do exemplo hello, alguns momentos, vou mostrar apenas Olá incrementais mais linhas de código R em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="93573-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="93573-445">Olá dataframe de leitura</span><span class="sxs-lookup"><span data-stu-id="93573-445">Reading hello dataframe</span></span>
<span data-ttu-id="93573-446">Como uma primeira etapa, vamos um dataframe de leitura e assegure-se de que podemos obter resultados de saudação esperado.</span><span class="sxs-lookup"><span data-stu-id="93573-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="93573-447">Olá código a seguir deve fazer o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="93573-448">Agora, execute o teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-448">Now, run hello experiment.</span></span> <span data-ttu-id="93573-449">log de saudação da nova forma de executar Script R Olá deve parecer com a Figura 14.</span><span class="sxs-lookup"><span data-stu-id="93573-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="93573-450">*Figura 14. Resumo de dataframe de saudação no módulo Executar Script R de saudação.*</span><span class="sxs-lookup"><span data-stu-id="93573-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="93573-451">Esses dados são de formato e tipos de saudação esperado.</span><span class="sxs-lookup"><span data-stu-id="93573-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="93573-452">Observe que a coluna de 'Month' hello é do fator de tipo e tem Olá esperado um número de níveis.</span><span class="sxs-lookup"><span data-stu-id="93573-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="93573-453">Criando um objeto de série temporal</span><span class="sxs-lookup"><span data-stu-id="93573-453">Creating a time series object</span></span>
<span data-ttu-id="93573-454">Precisamos tooadd um dataframe de tooour de objeto de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="93573-455">Substitua o código de atual de saudação pelo seguinte hello, que adiciona uma nova coluna de classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="93573-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="93573-456">Agora, verifique o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-456">Now, check hello log.</span></span> <span data-ttu-id="93573-457">Deve se parecer com a Figura 15.</span><span class="sxs-lookup"><span data-stu-id="93573-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="93573-458">*Figura 15. Resumo de dataframe de saudação com um objeto de série de tempo.*</span><span class="sxs-lookup"><span data-stu-id="93573-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="93573-459">Podemos ver da saudação resumida que coluna nova Olá na verdade é da classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="93573-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="93573-460">Explorar e transformar dados Olá</span><span class="sxs-lookup"><span data-stu-id="93573-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="93573-461">Vamos explorar algumas das variáveis de saudação deste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93573-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="93573-462">Uma matriz de scatterplot é uma boa maneira tooproduce uma olhada rápida.</span><span class="sxs-lookup"><span data-stu-id="93573-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="93573-463">Eu estou substituindo Olá `str()` função no código de R anterior Olá com a seguinte linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="93573-464">Execute esse código e veja o que acontece.</span><span class="sxs-lookup"><span data-stu-id="93573-464">Run this code and see what happens.</span></span> <span data-ttu-id="93573-465">plotagem Olá produzida em Olá porta dispositivo R deve parecer com a Figura 16.</span><span class="sxs-lookup"><span data-stu-id="93573-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Matriz de dispersão de variáveis selecionadas][17]

<span data-ttu-id="93573-467">*Figura 16. Matriz de dispersão de variáveis selecionadas.*</span><span class="sxs-lookup"><span data-stu-id="93573-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="93573-468">Há algumas estruturas estranha em relações de saudação entre essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="93573-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="93573-469">Talvez isso surge de tendências nos dados de saudação e de fato Olá que não adotaram variáveis hello.</span><span class="sxs-lookup"><span data-stu-id="93573-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="93573-470">Análise de correlação</span><span class="sxs-lookup"><span data-stu-id="93573-470">Correlation analysis</span></span>
<span data-ttu-id="93573-471">análise de correlação tooperform precisamos tooboth eliminação de tendência e padronizar variáveis hello.</span><span class="sxs-lookup"><span data-stu-id="93573-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="93573-472">Podemos simplesmente usar Olá R `scale()` função, que centraliza tanto dimensiona variáveis.</span><span class="sxs-lookup"><span data-stu-id="93573-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="93573-473">Essa função também pode ser executada mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="93573-473">This function might well run faster.</span></span> <span data-ttu-id="93573-474">No entanto, quero tooshow é um exemplo de programação defesa em R.</span><span class="sxs-lookup"><span data-stu-id="93573-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="93573-475">Olá `ts.detrend()` função abaixo executa ambas essas operações.</span><span class="sxs-lookup"><span data-stu-id="93573-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="93573-476">Hello seguintes duas linhas de código da tendência dados saudação e, em seguida, padronizar valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="93573-477">Há bastante aconteça bit no hello `ts.detrend()` função.</span><span class="sxs-lookup"><span data-stu-id="93573-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="93573-478">A maioria desse código está verificando problemas potenciais com argumentos de saudação ou lidar com exceções, que ainda podem surgir durante os cálculos de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="93573-479">Apenas algumas linhas do código realmente Olá cálculos.</span><span class="sxs-lookup"><span data-stu-id="93573-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="93573-480">Já abordamos a um exemplo de programação defensiva em [Transformações de valor](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="93573-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="93573-481">Os dois blocos de computação estão encapsulados em `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="93573-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="93573-482">Para alguns erros faz sentido tooreturn Olá entrada vetor original e em outros casos, retornar um vetor de zeros.</span><span class="sxs-lookup"><span data-stu-id="93573-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="93573-483">Observe que a regressão linear de saudação usado para eliminação de tendência é uma regressão de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="93573-484">variável de indicador de saudação é um objeto de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="93573-485">Uma vez `ts.detrend()` definido aplicá-lo toohello variáveis de interesse em nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="93573-486">Nós deve forçar a lista resultante de saudação criada pelo `lapply()` dataframe toodata usando `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="93573-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="93573-487">Devido a defesa aspectos de `ts.detrend()`, processamento de saudação de corrigir a tooprocess falha uma das variáveis de saudação não impedirá que outros.</span><span class="sxs-lookup"><span data-stu-id="93573-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="93573-488">a linha final Olá de código cria um par scatterplot.</span><span class="sxs-lookup"><span data-stu-id="93573-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="93573-489">Depois de executar código Olá R, resultados Olá Olá scatterplot são mostrados na Figura 17.</span><span class="sxs-lookup"><span data-stu-id="93573-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Emparelhar a dispersão da série temporal padronizada e sem tendências][18]

<span data-ttu-id="93573-491">*Figura 17. Emparelhe o scatterplot da séries de tempo padronizada e sem tendências.*</span><span class="sxs-lookup"><span data-stu-id="93573-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="93573-492">Você pode comparar esses toothose resultados mostrado na Figura 16.</span><span class="sxs-lookup"><span data-stu-id="93573-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="93573-493">Com hello tendência removido e Olá variáveis padronizados, podemos ver muito menos estrutura em relações de saudação entre essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="93573-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="93573-494">correlações de saudação do Hello código toocompute como objetos de R ccf é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="93573-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="93573-495">Executar esse código produz log Olá mostrado na Figura 18.</span><span class="sxs-lookup"><span data-stu-id="93573-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="93573-496">*Figura 18. Lista de ccf objetos da análise de correlação de pares de saudação.*</span><span class="sxs-lookup"><span data-stu-id="93573-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="93573-497">Há um valor de correlação para cada intervalo.</span><span class="sxs-lookup"><span data-stu-id="93573-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="93573-498">Nenhum desses valores de correlação é grande o suficiente toobe significativa.</span><span class="sxs-lookup"><span data-stu-id="93573-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="93573-499">Podemos, portanto, concluir que é possível modelar cada variável de forma independente.</span><span class="sxs-lookup"><span data-stu-id="93573-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="93573-500">Exibir um dataframe</span><span class="sxs-lookup"><span data-stu-id="93573-500">Output a dataframe</span></span>
<span data-ttu-id="93573-501">Podemos ter computada correlações emparelhadas hello como uma lista de objetos de R ccf.</span><span class="sxs-lookup"><span data-stu-id="93573-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="93573-502">Isso apresenta um pequeno problema como Olá porta de saída do conjunto de dados de resultado realmente requer um dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="93573-503">Além disso, Olá ccf próprio objeto for uma lista e queremos apenas os valores hello no primeiro elemento Olá desta lista, correlações Olá no hello atrasos vários.</span><span class="sxs-lookup"><span data-stu-id="93573-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="93573-504">Olá código extrai Olá latência valores a seguir da lista de saudação de objetos de ccf, que são listas.</span><span class="sxs-lookup"><span data-stu-id="93573-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="93573-505">Olá primeira linha de código é um pouco confusa e alguma explicação pode ajudá-lo a entender a ele.</span><span class="sxs-lookup"><span data-stu-id="93573-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="93573-506">Trabalhando dentro para fora da saudação temos seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="93573-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="93573-507">Olá '**[[**'operator com argumento de saudação'**1**' selecionará Olá vetor de correlações em atrasos de saudação do primeiro elemento de saudação da lista de objetos ccf hello.</span><span class="sxs-lookup"><span data-stu-id="93573-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="93573-508">Olá `do.call()` função se aplica a saudação `rbind()` função sobre os elementos de saudação da lista de saudação retorna ao `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="93573-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="93573-509">Olá `data.frame()` função converte o resultado de saudação produzido por `do.call()` tooa dataframe.</span><span class="sxs-lookup"><span data-stu-id="93573-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="93573-510">Observe que os nomes de linha de saudação em uma coluna de dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="93573-511">Isso preserva a nomes de linha hello quando eles são produzidos por Olá [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="93573-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="93573-512">A execução de código Olá produz saída de hello mostrada na Figura 19 quando eu **visualizar** Olá saída em Olá porta do conjunto de dados de resultado.</span><span class="sxs-lookup"><span data-stu-id="93573-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="93573-513">nomes de linha de saudação estão na primeira coluna de hello, conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="93573-513">hello row names are in hello first column, as intended.</span></span>

![Resultados da análise de correlação de saudação][20]

<span data-ttu-id="93573-515">*Figura 19. Resultados da análise de correlação de saudação de saída.*</span><span class="sxs-lookup"><span data-stu-id="93573-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="93573-516"><a id="seasonalforecasting"></a>Exemplo de série temporal: previsão sazonal</span><span class="sxs-lookup"><span data-stu-id="93573-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="93573-517">Nossos dados agora estão em um formato adequado para análise e determinamos que não há nenhum significativas correlações entre variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="93573-518">Vamos continuar e criar um modelo de previsão de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="93573-519">Usando esse modelo preveja a produção de leite Califórnia para Olá 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="93573-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="93573-520">Nosso modelo de previsão terá dois componentes, um componente de tendência e um componente sazonal.</span><span class="sxs-lookup"><span data-stu-id="93573-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="93573-521">Previsão concluída Olá é produto Olá esses dois componentes.</span><span class="sxs-lookup"><span data-stu-id="93573-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="93573-522">Esse tipo de modelo é conhecido como modelo de multiplicação.</span><span class="sxs-lookup"><span data-stu-id="93573-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="93573-523">alternativa de saudação é um modelo aditivo.</span><span class="sxs-lookup"><span data-stu-id="93573-523">hello alternative is an additive model.</span></span> <span data-ttu-id="93573-524">Nós já aplicou um variáveis de toohello de transformação de log de interesse, o que torna essa análise manejável.</span><span class="sxs-lookup"><span data-stu-id="93573-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="93573-525">código de R completo Olá desta seção é no arquivo zip de saudação que você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="93573-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="93573-526">Criando dataframe Olá para análise</span><span class="sxs-lookup"><span data-stu-id="93573-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="93573-527">Comece adicionando um **novo** [Executar Script R] [ execute-r-script] experimento de tooyour do módulo.</span><span class="sxs-lookup"><span data-stu-id="93573-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="93573-528">Conectar Olá **conjunto de dados de resultado** saída de hello existentes [Executar Script R] [ execute-r-script] módulo toohello **Dataset1** entrada do novo módulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="93573-529">resultado de saudação deve ser semelhante a Figura 20.</span><span class="sxs-lookup"><span data-stu-id="93573-529">hello result should look something like Figure 20.</span></span>

![Olá experimentar Olá novo Executar Script R módulo adicionado][21]

<span data-ttu-id="93573-531">*Figura 20. Olá experimentar Olá novo Executar Script R módulo adicionado.*</span><span class="sxs-lookup"><span data-stu-id="93573-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="93573-532">Como com a análise de correlação de saudação que acabou de concluir, é preciso tooadd uma coluna com um objeto de série de tempo de POSIXct.</span><span class="sxs-lookup"><span data-stu-id="93573-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="93573-533">saudação de código a seguir vai fazer exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="93573-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="93573-534">Execute este código e examinar o log de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-534">Run this code and look at hello log.</span></span> <span data-ttu-id="93573-535">resultado de saudação deve parecer com a Figura 21.</span><span class="sxs-lookup"><span data-stu-id="93573-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="93573-536">*Figura 21. Um resumo de dataframe de saudação.*</span><span class="sxs-lookup"><span data-stu-id="93573-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="93573-537">Com esse resultado, estamos pronto toostart nossa análise.</span><span class="sxs-lookup"><span data-stu-id="93573-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="93573-538">Criar um conjunto de dados de treinamento</span><span class="sxs-lookup"><span data-stu-id="93573-538">Create a training dataset</span></span>
<span data-ttu-id="93573-539">Com o dataframe de saudação construída, é preciso toocreate um conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="93573-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="93573-540">Esses dados incluirá todas observações Olá exceto Olá últimas 12, do ano Olá 2013, o que é o nosso conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="93573-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="93573-541">seguir Olá subconjuntos Olá dataframe de código e cria gráficos de variáveis de produção e preço Laticínios hello.</span><span class="sxs-lookup"><span data-stu-id="93573-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="93573-542">Em seguida, criar gráficos de saudação quatro variáveis de produção e preço.</span><span class="sxs-lookup"><span data-stu-id="93573-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="93573-543">Uma função anônima é usado toodefine alguns amplia a plotagem e, em seguida, iterar pela lista de saudação de saudação outros dois argumentos com `Map()`.</span><span class="sxs-lookup"><span data-stu-id="93573-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="93573-544">Se você estiver pensando que um loop funcionaria bem aqui, você está certo.</span><span class="sxs-lookup"><span data-stu-id="93573-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="93573-545">Mas, como R é uma linguagem funcional, estou lhe mostrando uma abordagem funcional.</span><span class="sxs-lookup"><span data-stu-id="93573-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="93573-546">Executar código Olá produz Olá plota série de série temporal da saída de dispositivo R Olá mostrada na Figura 22.</span><span class="sxs-lookup"><span data-stu-id="93573-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="93573-547">Observe que eixo de tempo de saudação em unidades de datas, um benefício interessante do tempo de saudação série plotar método.</span><span class="sxs-lookup"><span data-stu-id="93573-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Primeira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segunda das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terceira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarta das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="93573-552">*Figura 22. Plotagens de série temporal dos dados de produção e preço de derivados do leite da Califórnia.*</span><span class="sxs-lookup"><span data-stu-id="93573-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="93573-553">Um modelo de tendência</span><span class="sxs-lookup"><span data-stu-id="93573-553">A trend model</span></span>
<span data-ttu-id="93573-554">Tendo criado um objeto de série de tempo e tendo uma olhada em dados Olá, vamos começar tooconstruct um modelo de tendência para Olá dados de produção leite Califórnia.</span><span class="sxs-lookup"><span data-stu-id="93573-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="93573-555">Podemos fazer isso com uma regressão da série de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-555">We can do this with a time series regression.</span></span> <span data-ttu-id="93573-556">No entanto, é claro de plotagem Olá que iremos precisa de mais de um coeficiente e interceptar tooaccurately modelar Olá observado tendências nos dados de treinamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="93573-557">Considerando pequena escala Olá dos dados hello, será criar modelo Olá tendência em RStudio e, em seguida, recorte e cole o modelo resultante Olá em aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="93573-558">O RStudio fornece um ambiente adequado para esse tipo de análise interativa.</span><span class="sxs-lookup"><span data-stu-id="93573-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="93573-559">Como a primeira tentativa, tentarei uma regressão polinomial com too3 é inicializado.</span><span class="sxs-lookup"><span data-stu-id="93573-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="93573-560">Existe um perigo real de sobreajuste desses tipos de modelos.</span><span class="sxs-lookup"><span data-stu-id="93573-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="93573-561">Portanto, é melhor termos de ordem alta tooavoid.</span><span class="sxs-lookup"><span data-stu-id="93573-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="93573-562">Olá `I()` função inibe a interpretação de conteúdo da saudação (interpreta conteúdo Olá 'como está') e permite que você toowrite uma função interpretada literalmente em uma equação de regressão.</span><span class="sxs-lookup"><span data-stu-id="93573-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="93573-563">Isso gera o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="93573-564">Dos valores de P (Pr (> | t |)) na saída, podemos ver que Olá quadrado termo não pode ser significativo.</span><span class="sxs-lookup"><span data-stu-id="93573-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="93573-565">Vou usar Olá `update()` função toomodify esse modelo por descartar Olá quadrado termo.</span><span class="sxs-lookup"><span data-stu-id="93573-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="93573-566">Isso gera o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="93573-567">Assim parece melhor.</span><span class="sxs-lookup"><span data-stu-id="93573-567">This looks better.</span></span> <span data-ttu-id="93573-568">Todos os termos de saudação são significativos.</span><span class="sxs-lookup"><span data-stu-id="93573-568">All of hello terms are significant.</span></span> <span data-ttu-id="93573-569">No entanto, o valor de 2e-16 de saudação é um valor padrão e não deve ser tomada muito sério.</span><span class="sxs-lookup"><span data-stu-id="93573-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="93573-570">Como um teste de integridade, vamos fazer um gráfico de série de tempo de saudação dados de produção Laticínios Califórnia com curva de tendência Olá mostrada.</span><span class="sxs-lookup"><span data-stu-id="93573-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="93573-571">Adicionei Olá código Olá aprendizado de máquina a seguir [Executar Script R] [ execute-r-script] toocreate de modelo (não RStudio) Olá modelo e faça um gráfico.</span><span class="sxs-lookup"><span data-stu-id="93573-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="93573-572">Olá resultado é mostrado na Figura 23.</span><span class="sxs-lookup"><span data-stu-id="93573-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dados de produção de leite da Califórnia com o modelo de tendência mostrado](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="93573-574">*Figura 23. Dados de produção leite da Califórnia com o modelo de tendência mostrado.*</span><span class="sxs-lookup"><span data-stu-id="93573-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="93573-575">Parece que o modelo de tendência Olá se adapta a saudação dados muito bem.</span><span class="sxs-lookup"><span data-stu-id="93573-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="93573-576">Além disso, não parece toobe evidência de ajuste excessivo, como ímpar wiggles na curva do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="93573-577">Modelo sazonal</span><span class="sxs-lookup"><span data-stu-id="93573-577">Seasonal model</span></span>
<span data-ttu-id="93573-578">Com um modelo de tendência em mãos, precisamos toopush em e incluir efeitos sazonais hello.</span><span class="sxs-lookup"><span data-stu-id="93573-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="93573-579">Usaremos o mês de saudação do ano de saudação como uma variável fictícia em vigor do hello modelo linear toocapture Olá mês a mês.</span><span class="sxs-lookup"><span data-stu-id="93573-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="93573-580">Observe que quando você introduzir variáveis fator em um modelo, interceptação Olá não deve computada.</span><span class="sxs-lookup"><span data-stu-id="93573-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="93573-581">Se você não fizer isso, fórmula Olá é excessivamente especificada e R descartará uma saudação desejado fatores, mas manter o termo de interceptação hello.</span><span class="sxs-lookup"><span data-stu-id="93573-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="93573-582">Como temos um modelo de tendência satisfatório podemos usar Olá `update()` Olá de tooadd função novo modelo existente toohello de termos.</span><span class="sxs-lookup"><span data-stu-id="93573-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="93573-583">Olá -1 na fórmula de atualização Olá descarta o termo de interceptação hello.</span><span class="sxs-lookup"><span data-stu-id="93573-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="93573-584">Continuar em RStudio momento hello:</span><span class="sxs-lookup"><span data-stu-id="93573-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="93573-585">Isso gera o seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="93573-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="93573-586">Podemos ver o modelo Olá não tem um termo de interceptação e tem 12 fatores significativos mês.</span><span class="sxs-lookup"><span data-stu-id="93573-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="93573-587">Isso é exatamente o que queremos toosee.</span><span class="sxs-lookup"><span data-stu-id="93573-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="93573-588">Vamos fazer outra plotagem de série de tempo de saudação Califórnia produção Laticínios dados toosee como modelo sazonais hello está funcionando.</span><span class="sxs-lookup"><span data-stu-id="93573-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="93573-589">Adicionei Olá código Olá aprendizado de máquina a seguir [Executar Script R] [ execute-r-script] toocreate Olá modelo e faça um gráfico.</span><span class="sxs-lookup"><span data-stu-id="93573-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="93573-590">Executar esse código no aprendizado de máquina do Azure produz plotagem Olá mostrada na Figura 24.</span><span class="sxs-lookup"><span data-stu-id="93573-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Produção de leite da Califórnia com o modelo, incluindo efeitos sazonais](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="93573-592">*Figura 24. Produção de leite na Califórnia com o modelo dos efeitos sazonais.*</span><span class="sxs-lookup"><span data-stu-id="93573-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="93573-593">Olá, ajustar toohello dados mostrados na Figura 24 são incentivando em vez disso.</span><span class="sxs-lookup"><span data-stu-id="93573-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="93573-594">Tendência de saudação e efeito sazonais de saudação (variação mensal) procure razoáveis.</span><span class="sxs-lookup"><span data-stu-id="93573-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="93573-595">Como outra verificação em nosso modelo, vamos dar uma olhada em restos Olá.</span><span class="sxs-lookup"><span data-stu-id="93573-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="93573-596">Olá exemplo código a seguir calcula Olá valores previstos de nosso dois modelos, calcula restos Olá para modelo sazonais hello e plota, em seguida, dos resíduos para dados de treinamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="93573-597">plotagem residual Olá é mostrada na Figura 25.</span><span class="sxs-lookup"><span data-stu-id="93573-597">hello residual plot is shown in Figure 25.</span></span>

![Restos de modelo de sazonais Olá para dados de treinamento Olá](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="93573-599">*Figura 25. Restos de modelo de sazonais Olá para dados de treinamento de saudação.*</span><span class="sxs-lookup"><span data-stu-id="93573-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="93573-600">Esses resíduos parecem razoáveis.</span><span class="sxs-lookup"><span data-stu-id="93573-600">These residuals look reasonable.</span></span> <span data-ttu-id="93573-601">Não há nenhuma estrutura específica, exceto o efeito de saudação do recessão Olá 2008 e 2009, o que nosso modelo não leva em conta particularmente bem.</span><span class="sxs-lookup"><span data-stu-id="93573-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="93573-602">plotagem de saudação mostrada na Figura 25 é útil para detectar qualquer padrões dependentes de tempo em restos Olá.</span><span class="sxs-lookup"><span data-stu-id="93573-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="93573-603">abordagem de saudação explícita de computação e plotar resíduos Olá usei coloca restos Olá na ordem de tempo no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="93573-604">Se, em Olá outro lado, tinha plotados `milk.lm$residuals`, plotagem Olá não teria sido na ordem de tempo.</span><span class="sxs-lookup"><span data-stu-id="93573-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="93573-605">Você também pode usar `plot.lm()` tooproduce uma série de gráficos de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="93573-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="93573-606">Esse código gera uma série de gráficos de diagnóstico mostrados na Figura 26.</span><span class="sxs-lookup"><span data-stu-id="93573-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Primeiro de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segundo de gráficos de diagnósticos para o modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terceiros de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarto de diagnósticos gráficos para modelo sazonais Olá](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="93573-611">*Figura 26. Diagnóstico plota para modelo sazonais hello.*</span><span class="sxs-lookup"><span data-stu-id="93573-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="93573-612">Há alguns pontos altamente influentes identificados nesses gráficos, mas nada toocause grande preocupação.</span><span class="sxs-lookup"><span data-stu-id="93573-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="93573-613">Além disso, podemos ver de plotagem de Q-Q Normal Olá restos Olá são toonormally fechar distribuído, uma suposição importante para os modelos lineares.</span><span class="sxs-lookup"><span data-stu-id="93573-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="93573-614">Avaliação de previsão e modelo</span><span class="sxs-lookup"><span data-stu-id="93573-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="93573-615">Há apenas um toocomplete de toodo coisa mais nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="93573-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="93573-616">Precisamos toocompute previsões e medir o erro de saudação em relação aos dados reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="93573-617">Nossa previsão será usado para Olá 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="93573-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="93573-618">Podemos pode computar uma medida de erro para essa previsão toohello real de dados que não faz parte de nosso conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="93573-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="93573-619">Além disso, é possível comparar o desempenho em Olá 18 anos de toohello de dados de treinamento 12 meses de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="93573-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="93573-620">São usadas várias métricas de desempenho de saudação toomeasure de modelos de série temporal.</span><span class="sxs-lookup"><span data-stu-id="93573-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="93573-621">Em nosso caso, usaremos erro de raiz quadrada média (RMS) hello.</span><span class="sxs-lookup"><span data-stu-id="93573-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="93573-622">Olá função a seguir calcula o hello RMS erro entre duas séries.</span><span class="sxs-lookup"><span data-stu-id="93573-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="93573-623">Assim como acontece com hello `log.transform()` função discutimos em hello "Valor transformações" seção, há muito código de recuperação a verificação e a exceção de erro nesta função.</span><span class="sxs-lookup"><span data-stu-id="93573-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="93573-624">Princípios de saudação empregados são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="93573-624">hello principles employed are hello same.</span></span> <span data-ttu-id="93573-625">Olá o trabalho é realizado em dois lugares encapsulados em `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="93573-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="93573-626">Primeiro, série de tempo de saudação é exponentiated, já que temos trabalhado com logs de saudação de valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="93573-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="93573-627">Segundo, o erro real RMS Olá é computado.</span><span class="sxs-lookup"><span data-stu-id="93573-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="93573-628">Vamos equipado com uma saudação de toomeasure função erro RMS, compilação e um dataframe contendo Olá RMS erros de saída.</span><span class="sxs-lookup"><span data-stu-id="93573-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="93573-629">Podemos incluirá termos de modelo de tendência Olá sozinho e modelo completo de saudação com fatores sazonais.</span><span class="sxs-lookup"><span data-stu-id="93573-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="93573-630">Olá código a seguir Olá trabalho usando modelos lineares dois Olá construímos.</span><span class="sxs-lookup"><span data-stu-id="93573-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="93573-631">Executando este código produz saída de hello mostrada na Figura 27 no hello porta de saída do conjunto de dados de resultado.</span><span class="sxs-lookup"><span data-stu-id="93573-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Comparação de erros do RMS para modelos de saudação][26]

<span data-ttu-id="93573-633">*Figura 27. Comparação de erros do RMS para modelos de saudação.*</span><span class="sxs-lookup"><span data-stu-id="93573-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="93573-634">A partir desses resultados, podemos ver que adicionando Olá fatores sazonais toohello modelo reduz o erro de RMS Olá significativamente.</span><span class="sxs-lookup"><span data-stu-id="93573-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="93573-635">Não é muito surpreendente, erro Olá RMS para Olá dados de treinamento é um pouco menor que para saudação de previsão.</span><span class="sxs-lookup"><span data-stu-id="93573-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="93573-636"><a id="appendixa"></a>Apêndice a: Guia tooRStudio</span><span class="sxs-lookup"><span data-stu-id="93573-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="93573-637">RStudio muito bem documentada, portanto neste apêndice fornecerei alguns links toohello seções principais da saudação RStudio documentação tooget que é iniciado.</span><span class="sxs-lookup"><span data-stu-id="93573-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="93573-638">Criando projetos</span><span class="sxs-lookup"><span data-stu-id="93573-638">Creating projects</span></span>
   
   <span data-ttu-id="93573-639">Você pode organizar e gerenciar seu código R em projetos usando o RStudio.</span><span class="sxs-lookup"><span data-stu-id="93573-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="93573-640">documentação de saudação que usa projetos pode ser encontrada em https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="93573-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="93573-641">É recomendável que você siga estas instruções e cria um projeto para obter exemplos de código Olá R neste documento.</span><span class="sxs-lookup"><span data-stu-id="93573-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="93573-642">Editar e executar código R</span><span class="sxs-lookup"><span data-stu-id="93573-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="93573-643">O RStudio fornece um ambiente integrado para editar e executar código R.</span><span class="sxs-lookup"><span data-stu-id="93573-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="93573-644">A documentação pode ser encontrada em https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="93573-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="93573-645">Depurando</span><span class="sxs-lookup"><span data-stu-id="93573-645">Debugging</span></span>
   
   <span data-ttu-id="93573-646">O RStudio inclui recursos avançados de depuração.</span><span class="sxs-lookup"><span data-stu-id="93573-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="93573-647">A documentação para esses recursos estão em https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="93573-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="93573-648">recursos de solução de problemas de ponto de interrupção de saudação são documentados em https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="93573-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="93573-649"><a id="appendixb"></a>APÊNDICE B: Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="93573-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="93573-650">Este tutorial aborda Olá básico da programação de R de que você precisa toouse Olá linguagem R com o estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="93573-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="93573-651">Se você não estiver familiarizado com R, duas introduções estão disponíveis no CRAN:</span><span class="sxs-lookup"><span data-stu-id="93573-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="93573-652">R para iniciantes por Emmanuel Paradis é toostart um bom lugar no http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="93573-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="93573-653">Um tooR Introdução por W. N.</span><span class="sxs-lookup"><span data-stu-id="93573-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="93573-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="93573-654">Venables et.</span></span> <span data-ttu-id="93573-655">al.</span><span class="sxs-lookup"><span data-stu-id="93573-655">al.</span></span> <span data-ttu-id="93573-656">se aprofunda um pouco mais em http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="93573-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="93573-657">Existem muitos livros sobre R que podem ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="93573-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="93573-658">Aqui estão alguns que considero úteis:</span><span class="sxs-lookup"><span data-stu-id="93573-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="93573-659">Olá arte de programação R: um Tour de estatística Design de Software por Norman Matloff é tooprogramming uma excelente introdução em R.</span><span class="sxs-lookup"><span data-stu-id="93573-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="93573-660">Livro de receitas R por Paul Teetor fornece toousing uma abordagem problema e a solução R.</span><span class="sxs-lookup"><span data-stu-id="93573-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="93573-661">R in Action, por Robert Kabacoff, é outro livro introdutório útil.</span><span class="sxs-lookup"><span data-stu-id="93573-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="93573-662">site do Hello complementar R rápida é um recurso útil em http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="93573-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="93573-663">R Inferno por Patrick Burns é surpreendentemente divertido livros que lida com uma série de tópicos complicados e difícil que podem ser encontrados durante a programação no catálogo de r. hello estão disponível gratuitamente em http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="93573-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="93573-664">Se você quiser um mergulho no tópicos avançados em R, dê uma olhada no catálogo Olá avançado R por Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="93573-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="93573-665">a versão online Olá deste livro está disponível gratuitamente em http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="93573-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="93573-666">Um catálogo de pacotes de série de tempo de R pode ser encontrado no hello CRAN modo de exibição de tarefa para análise de série temporal: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="93573-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="93573-667">Para obter informações sobre pacotes de objeto de série de tempo específico, consulte a documentação toohello para que o pacote.</span><span class="sxs-lookup"><span data-stu-id="93573-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="93573-668">Catálogo de Olá MTS introdutório R por Paul Cowpertwait e Andrew Metcalfe fornece uma introdução toousing R para análise de série temporal.</span><span class="sxs-lookup"><span data-stu-id="93573-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="93573-669">Muitos textos mais teóricos fornecem exemplos de R.</span><span class="sxs-lookup"><span data-stu-id="93573-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="93573-670">Alguns ótimos recursos na Internet:</span><span class="sxs-lookup"><span data-stu-id="93573-670">Some great internet resources:</span></span>

* <span data-ttu-id="93573-671">DataCamp: DataCamp ensina R no conforto de saudação do seu navegador com vídeos lições e exercícios de codificação.</span><span class="sxs-lookup"><span data-stu-id="93573-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="93573-672">Há interativos tutoriais sobre técnicas de R mais recentes hello e pacotes.</span><span class="sxs-lookup"><span data-stu-id="93573-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="93573-673">Consulte o tutorial de R livre interativo para o hello em https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="93573-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="93573-674">Um guia de Introdução ao R de Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="93573-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="93573-675">A quick R tutorial, por Kelly Black, da Clarkson University, http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="93573-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="93573-676">Mais de 60 recursos de R listados em http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="93573-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
