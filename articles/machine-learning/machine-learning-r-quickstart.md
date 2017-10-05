---
title: "Tutorial de início rápido para a linguagem R para Machine Learning | Microsoft Docs"
description: "Use este tutorial de programação R para começar a usar rapidamente a linguagem R com Studio de Azure Machine Learning para criar uma solução de previsão."
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
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="f12d1-104">Tutorial de início rápido para a linguagem de programação R para o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f12d1-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="f12d1-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="f12d1-105">Introduction</span></span>
<span data-ttu-id="f12d1-106">Este tutorial de início rápido ajuda a iniciar rapidamente estendendo o Azure Machine Learning usando a linguagem de programação R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="f12d1-107">Siga este tutorial de programação R para criar, testar e execute um código R no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="f12d1-108">Ao prosseguir neste tutorial, você criará uma solução completa de previsão usando a linguagem R no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="f12d1-109">O Microsoft Azure Machine Learning contém muitos módulos poderosos de aprendizado de máquina e de manipulação de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="f12d1-110">A poderosa linguagem de R tem sido descrita como a língua franca da análise.</span><span class="sxs-lookup"><span data-stu-id="f12d1-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="f12d1-111">Felizmente, a análise e manipulação de dados no Azure Machine Learning podem ser estendidas com R. Essa combinação fornece a escalabilidade e a facilidade de implantação do Azure Machine Learning com a flexibilidade e análise profunda de R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="f12d1-112">Previsão e conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f12d1-112">Forecasting and the dataset</span></span>
<span data-ttu-id="f12d1-113">A previsão é um método analítico amplamente empregado e bastante útil.</span><span class="sxs-lookup"><span data-stu-id="f12d1-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="f12d1-114">O uso típico varia de previsão de vendas de itens sazonais, determinar níveis de estoque ideal a prever variáveis macroeconômicas.</span><span class="sxs-lookup"><span data-stu-id="f12d1-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="f12d1-115">A previsão normalmente é feita com modelos de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="f12d1-116">Dados de série temporal são dados em que os valores têm um índice de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="f12d1-117">O índice de tempo pode ser regular, por exemplo, a cada mês ou a cada minuto, ou irregulares.</span><span class="sxs-lookup"><span data-stu-id="f12d1-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="f12d1-118">Um modelo de série de tempo se baseia em dados de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-118">A time series model is based on time series data.</span></span> <span data-ttu-id="f12d1-119">A linguagem de programação de R contém uma estrutura flexível e uma análise abrangente para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="f12d1-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="f12d1-120">Neste guia de início rápido, trabalharemos com a produção de derivados de leite e dados de preços na Califórnia.</span><span class="sxs-lookup"><span data-stu-id="f12d1-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="f12d1-121">Esses dados incluem informações mensais sobre a produção de vários produtos derivados do leite e o preço da gordura do leite, uma mercadoria que é um parâmetro de comparação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="f12d1-122">Os dados usados neste artigo, assim como os scripts de R, podem ser [baixados aqui][download].</span><span class="sxs-lookup"><span data-stu-id="f12d1-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="f12d1-123">Esses dados foram originalmente sintetizados a partir das informações disponibilizadas pela Universidade de Wisconsin em http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="f12d1-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="f12d1-124">Organização</span><span class="sxs-lookup"><span data-stu-id="f12d1-124">Organization</span></span>
<span data-ttu-id="f12d1-125">Passaremos por várias etapas enquanto você aprende a criar, testar e executar o código R de manipulação de dados e análises no ambiente do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="f12d1-126">Primeiro, veremos as noções básicas sobre o uso da linguagem R no ambiente do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="f12d1-127">Em seguida, discutiremos os diversos aspectos de entrada/saída de dados, código R e gráficos no ambiente do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="f12d1-128">Então, construiremos a primeira parte de uma solução de previsão criando o código de limpeza de dados e transformação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="f12d1-129">Com nossos dados preparados, executaremos uma análise das correlações entre diversas variáveis de nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="f12d1-130">Por fim, criaremos um modelo de previsão de série de tempos sazonais da produção de leite.</span><span class="sxs-lookup"><span data-stu-id="f12d1-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="f12d1-131">
            <a id="mlstudio">
            </a>Interagir com a linguagem R no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f12d1-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="f12d1-132">Esta seção apresenta algumas noções básicas de interagir com a linguagem de programação R no ambiente do Studio de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="f12d1-133">A linguagem R fornece uma ferramenta poderosa para a criação de análises personalizadas e módulos de manipulação de dados no ambiente do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="f12d1-134">Usarei o RStudio para desenvolver, testar e depurar o código R em pequena escala.</span><span class="sxs-lookup"><span data-stu-id="f12d1-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="f12d1-135">Esse código é, então, recortado e colado em um módulo [Executar Script R][execute-r-script] no Machine Learning Studio, pronto para ser executado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="f12d1-136">O módulo Executar Script R</span><span class="sxs-lookup"><span data-stu-id="f12d1-136">The Execute R Script module</span></span>
<span data-ttu-id="f12d1-137">No Machine Learning Studio, os scripts R são executados no módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-138">Um exemplo do módulo [Executar Script R][execute-r-script] no Machine Learning Studio é ilustrado na Figura 1.</span><span class="sxs-lookup"><span data-stu-id="f12d1-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![A linguagem de programação R: o módulo Executar o Script R selecionado no Studio de Machine Learning][1]

<span data-ttu-id="f12d1-140">*Figura 1. O ambiente do Machine Learning Studio mostrando o módulo Executar Script R selecionado.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="f12d1-141">Consultando a Figura 1, vejamos algumas das principais partes do ambiente do Machine Learning Studio para trabalhar com o módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="f12d1-142">Os módulos do teste são mostrados no painel central.</span><span class="sxs-lookup"><span data-stu-id="f12d1-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="f12d1-143">A parte superior do painel direito contém uma janela para exibir e editar seus scripts de R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="f12d1-144">A parte inferior do painel direito mostra algumas propriedades de [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="f12d1-145">Você pode exibir os logs de erro e de saída clicando nos pontos apropriados deste painel.</span><span class="sxs-lookup"><span data-stu-id="f12d1-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="f12d1-146">Naturalmente, abordaremos o módulo [Executar Script R][execute-r-script] com mais detalhes no restante deste documento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="f12d1-147">Ao trabalhar com funções R complexas, é recomendável que você edite, teste e depure no RStudio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="f12d1-148">Assim como acontece com qualquer desenvolvimento de software, estenda o código de forma incremental e teste-o em pequenos casos de teste simples.</span><span class="sxs-lookup"><span data-stu-id="f12d1-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="f12d1-149">Em seguida, recorte e cole suas funções na janela de script R do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-150">Essa abordagem permite aproveitar o IDE (ambiente de desenvolvimento integrado) do RStudio e a capacidade do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="f12d1-151">Executar código R</span><span class="sxs-lookup"><span data-stu-id="f12d1-151">Execute R code</span></span>
<span data-ttu-id="f12d1-152">Qualquer código R no módulo [Executar Script R][execute-r-script] será executado quando você clicar no botão **Executar** para iniciar o experimento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="f12d1-153">Quando a execução for concluída, uma marca de seleção aparecerá no ícone [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="f12d1-154">Codificação R defensiva para o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f12d1-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="f12d1-155">Se, por exemplo, estiver desenvolvendo código R para um serviço Web que usa o Azure Machine Learning, você definitivamente deverá planejar como seu código lidará com exceções e com entrada de dados inesperados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="f12d1-156">Para ficar claro, eu não incluí muito em relação a verificação ou a manipulação de exceção na maioria dos exemplos de código mostrados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="f12d1-157">No entanto, ao prosseguirmos, darei vários exemplos de funções usando o recurso de tratamento de exceção do R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="f12d1-158">Se for necessário um entendimento mais completo do tratamento de exceção do R, recomendo a leitura das seções aplicáveis do livro de Wickham listado no [Apêndice B - Leitura adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="f12d1-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="f12d1-159">Depurar e testar R no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f12d1-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="f12d1-160">Para reiterar, é recomendável testar e depurar seu código R em pequena escala no RStudio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="f12d1-161">No entanto, há casos em que você precisará detectar problemas de código R no próprio módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="f12d1-162">Além disso, é recomendável verificar os resultados no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="f12d1-163">A saída da execução do código R e na plataforma do Estúdio de Azure Machine Learning é encontrada principalmente em output.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="f12d1-164">Algumas informações adicionais serão vistas no arquivo error.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="f12d1-165">Se ocorrer um erro no Machine Learning Studio durante a execução do código R, a primeira ação deverá ser verificar error.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="f12d1-166">Esse arquivo pode conter mensagens de erro úteis para ajudá-lo a entender e corrigir o erro.</span><span class="sxs-lookup"><span data-stu-id="f12d1-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="f12d1-167">Para exibir error.log, clique em **Exibir log de erros** no **painel de propriedades** de [Executar Script R][execute-r-script] que contém o erro.</span><span class="sxs-lookup"><span data-stu-id="f12d1-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="f12d1-168">Por exemplo, executei o seguinte código R, com uma variável y indefinida, em um módulo [Executar Script R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="f12d1-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="f12d1-169">Esse código não foi executado resultando em uma condição de erro.</span><span class="sxs-lookup"><span data-stu-id="f12d1-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="f12d1-170">Ao clicar em **Exibir log de erro** no **painel de propriedades** é produzido o modo de exibição mostrado na Figura 2.</span><span class="sxs-lookup"><span data-stu-id="f12d1-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![A mensagem de erro é exibida][2]

<span data-ttu-id="f12d1-172">*Figura 2. Mensagem de erro pop-up.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="f12d1-173">Parece que precisamos examinar output.g para ver a mensagem de erro de R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="f12d1-174">Clique em [Executar Script R][execute-r-script] e, em seguida, clique no item **Exibir output.log** no **painel de propriedades** à direita.</span><span class="sxs-lookup"><span data-stu-id="f12d1-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="f12d1-175">Uma nova janela do navegador é aberta e vejo o item a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="f12d1-176">Essa mensagem de erro contém surpresas e claramente identifica o problema.</span><span class="sxs-lookup"><span data-stu-id="f12d1-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="f12d1-177">Para inspecionar o valor de qualquer objeto em R, você pode imprimir esses valores no arquivo output.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="f12d1-178">As regras para examinar os valores de objeto são essencialmente as mesmas de uma sessão interativa de R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="f12d1-179">Por exemplo, se você digitar um nome de variável em uma linha, o valor do objeto será impresso no arquivo de output.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="f12d1-180">Pacotes no Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="f12d1-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="f12d1-181">O Azure Machine Learning vem com mais de 350 pacotes de linguagem R pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="f12d1-182">Você pode usar o código a seguir no módulo [Executar Script R][execute-r-script] para recuperar uma lista dos pacotes pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="f12d1-183">Se você não entender a última linha do código no momento, continue lendo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="f12d1-184">No restante deste documento, discutiremos amplamente o uso de R no ambiente do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="f12d1-185">Introdução ao RStudio</span><span class="sxs-lookup"><span data-stu-id="f12d1-185">Introduction to RStudio</span></span>
<span data-ttu-id="f12d1-186">O RStudio é um IDE amplamente utilizado para R. Usarei o RStudio para editar, testar e depurar parte do código R usado neste guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="f12d1-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="f12d1-187">Depois que o código R for testado e estiver pronto, basta recortar do editor do RStudio e colar no módulo [Executar Script R][execute-r-script] do Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="f12d1-188">Se você não tiver a linguagem de programação R instalada em seu computador desktop, recomendo que você faça isso agora.</span><span class="sxs-lookup"><span data-stu-id="f12d1-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="f12d1-189">Downloads gratuitos da linguagem R de software livre estão disponíveis na rede de arquivamento abrangente R (CRAN) em [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="f12d1-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="f12d1-190">Há downloads disponíveis para Windows, Mac OS e Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="f12d1-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="f12d1-191">Escolha um espelho próximo e siga as instruções de download.</span><span class="sxs-lookup"><span data-stu-id="f12d1-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="f12d1-192">Além disso, CRAN contém uma grande quantidade de pacotes de manipulação de dados e análise úteis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="f12d1-193">Se você for novo no RStudio, você deve baixar e instalar a versão para desktop.</span><span class="sxs-lookup"><span data-stu-id="f12d1-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="f12d1-194">Você pode encontrar os downloads do RStudio para Windows, Mac OS e Linux/UNIX em http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="f12d1-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="f12d1-195">Siga as instruções fornecidas para instalar o RStudio em seu computador desktop.</span><span class="sxs-lookup"><span data-stu-id="f12d1-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="f12d1-196">Uma tutorial de introdução no RStudio está disponível em https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="f12d1-197">Forneço algumas informações adicionais sobre como usar o RStudio no [Apêndice A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="f12d1-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="f12d1-198"><a id="scriptmodule"></a>Obter dados de entrada e saída no módulo Executar Script R</span><span class="sxs-lookup"><span data-stu-id="f12d1-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="f12d1-199">Nesta seção, discutiremos como você obtém dados de entrada e saída no módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-200">Analisaremos como lidar com vários tipos de dados de leitura de entrada e saída do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="f12d1-201">O código completo para esta seção está no arquivo zip baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="f12d1-202">Carregar e verificar dados no Studio de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f12d1-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="f12d1-203"><a id="loading"></a>Carregar o conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f12d1-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="f12d1-204">Vamos começar carregando o arquivo **csdairydata.csv** no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="f12d1-205">Inicie seu ambiente do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="f12d1-206">Clique em **+ NOVO** no canto inferior esquerdo da tela e selecione **Conjunto de dados**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="f12d1-207">Selecione **Do Arquivo Local**, e **Procurar** para selecionar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="f12d1-208">Verifique se você selecionou **Arquivo CSV genérico com cabeçalho (.csv)** como o tipo do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="f12d1-209">Clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="f12d1-209">Click the check mark.</span></span>
* <span data-ttu-id="f12d1-210">Depois que o conjunto de dados tiver sido carregado, você deve ver o novo conjunto de dados clicando na guia **Conjuntos de Dados** .</span><span class="sxs-lookup"><span data-stu-id="f12d1-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="f12d1-211">Criar uma experiência</span><span class="sxs-lookup"><span data-stu-id="f12d1-211">Create an experiment</span></span>
<span data-ttu-id="f12d1-212">Agora que temos alguns dados no Machine Learning Studio, precisamos criar um teste para fazer a análise.</span><span class="sxs-lookup"><span data-stu-id="f12d1-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="f12d1-213">Clique em **+ NOVO** na parte inferior esquerda e selecione **Testar** e **Teste em branco**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="f12d1-214">Você pode nomear o seu teste selecionando e modificando o título **Teste criado em...** no início da página.</span><span class="sxs-lookup"><span data-stu-id="f12d1-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="f12d1-215">Por exemplo, alterando-o para **Análise da AC**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="f12d1-216">À esquerda da página de teste, expanda **Conjuntos de Dados Salvos** e **Meus Conjuntos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="f12d1-217">Você deve ver o **cadairydata.csv** que carregou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="f12d1-218">Arraste e solte o **conjunto de dados csdairydata.csv** no teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="f12d1-219">Na caixa **Pesquisar itens de teste** na parte superior do painel à esquerda, digite [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="f12d1-220">O módulo irá aparecer na lista de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f12d1-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="f12d1-221">Arraste e solte o módulo [Executar Script R][execute-r-script] em seu palete.</span><span class="sxs-lookup"><span data-stu-id="f12d1-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="f12d1-222">Conecte a saída do **conjunto de dados csdairydata.csv** à entrada à esquerda (**Dataset1**) de [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="f12d1-223">**Não se esqueça de clicar em 'Salvar'!**</span><span class="sxs-lookup"><span data-stu-id="f12d1-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="f12d1-224">Agora seu teste deve ser similar a Figura 3.</span><span class="sxs-lookup"><span data-stu-id="f12d1-224">At this point your experiment should look something like Figure 3.</span></span>

![O teste de Análise de Produtos Derivados do Leite da Califórnia, com o conjunto de dados e o módulo Executar Script R][3]

<span data-ttu-id="f12d1-226">*Figura 3. O teste Análise de produtos derivados de leite da Califórnia com o conjunto de dados e o módulo Executar Script R.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="f12d1-227">Verificar os dados</span><span class="sxs-lookup"><span data-stu-id="f12d1-227">Check on the data</span></span>
<span data-ttu-id="f12d1-228">Vamos dar uma olhada nos dados que carregou em nosso teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="f12d1-229">No teste, clique duas vezes na saída do **conjunto de dados cadairydata.csv** e selecione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="f12d1-230">Você deve ver algo semelhante à Figura 4.</span><span class="sxs-lookup"><span data-stu-id="f12d1-230">You should see something like Figure 4.</span></span>  

![Resumo do conjunto de dados cadairydata.csv][4]

<span data-ttu-id="f12d1-232">*Figura 4. Resumo de conjunto de dados cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="f12d1-233">Nessa exibição, vemos muitas informações úteis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="f12d1-234">Podemos ver as primeiras linhas do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="f12d1-235">Se selecionarmos uma coluna, a seção Estatísticas mostra mais informações sobre a coluna.</span><span class="sxs-lookup"><span data-stu-id="f12d1-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="f12d1-236">Por exemplo, a linha Tipo de Recurso mostra quais tipos de dados o Azure Machine Learning Studio atribuiu à coluna.</span><span class="sxs-lookup"><span data-stu-id="f12d1-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="f12d1-237">Dar uma olhada rápida como esta é boa uma verificação de integridade para ser feita antes de começar qualquer trabalho sério.</span><span class="sxs-lookup"><span data-stu-id="f12d1-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="f12d1-238">Primeiro script R</span><span class="sxs-lookup"><span data-stu-id="f12d1-238">First R script</span></span>
<span data-ttu-id="f12d1-239">Vamos criar um primeiro script R simples para testar no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="f12d1-240">Criei e testei o seguinte script no RStudio:</span><span class="sxs-lookup"><span data-stu-id="f12d1-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="f12d1-241">Agora preciso transferir esse script para meu Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="f12d1-242">Eu poderia simplesmente recortar e colar.</span><span class="sxs-lookup"><span data-stu-id="f12d1-242">I could simply cut and paste.</span></span> <span data-ttu-id="f12d1-243">No entanto, nesse caso, eu vou transferir o meu script R por meio de um arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="f12d1-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="f12d1-244">Entrada de dados para o módulo Executar Script R</span><span class="sxs-lookup"><span data-stu-id="f12d1-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="f12d1-245">Vejamos as entradas do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-246">Neste exemplo, vamos ler dados de laticínios da Califórnia no módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="f12d1-247">Há três entradas possíveis para o módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-248">Você pode usar qualquer uma ou todas essas entradas, dependendo do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="f12d1-249">Também é totalmente aceitável usar um script R que não receba entrada.</span><span class="sxs-lookup"><span data-stu-id="f12d1-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="f12d1-250">Vamos examinar cada uma dessa entradas, da esquerda para a direita.</span><span class="sxs-lookup"><span data-stu-id="f12d1-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="f12d1-251">Você pode ver os nomes de cada uma das entradas colocando o cursor sobre a entrada e lendo a dica de ferramenta.</span><span class="sxs-lookup"><span data-stu-id="f12d1-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="f12d1-252">Pacote de script</span><span class="sxs-lookup"><span data-stu-id="f12d1-252">Script Bundle</span></span>
<span data-ttu-id="f12d1-253">A entrada de Pacote de Script permite que você passe o conteúdo de um arquivo zip para o módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-254">Você pode usar um dos comandos a seguir para ler o conteúdo do arquivo zip em seu código R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="f12d1-255">O Azure Machine Learning trata arquivos zip como se eles estivessem no diretório src/. Portanto, é necessário prefixar seus nomes de arquivo com esse nome de diretório.</span><span class="sxs-lookup"><span data-stu-id="f12d1-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="f12d1-256">Por exemplo, se o zip contiver os arquivos `yourfile.R` e `yourData.rdata` na raiz, aborde-os como `src/yourfile.R` e `src/yourData.rdata` ao usar `source` e `load`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="f12d1-257">Já discutimos o carregamento de conjuntos de dados em [Carregando o conjunto de dados](#loading).</span><span class="sxs-lookup"><span data-stu-id="f12d1-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="f12d1-258">Após criar e testar o script R mostrado na seção anterior, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f12d1-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="f12d1-259">Salve o script R em um arquivo .R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-259">Save the R script into a .R file.</span></span> <span data-ttu-id="f12d1-260">Eu chamo meu arquivo script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="f12d1-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="f12d1-261">Este é o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="f12d1-262">Crie um arquivo zip e copie o script no arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="f12d1-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="f12d1-263">No Windows, clique com o botão direito do mouse no arquivo e selecione **Enviar para** e em **Pasta compactada**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="f12d1-264">Isso criará um novo arquivo zip contendo o arquivo "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="f12d1-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="f12d1-265">Adicione o arquivo aos **conjuntos de dados** no Machine Learning Studio, especificando o tipo como **zip**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="f12d1-266">Agora você deve ver o arquivo zip em seus conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="f12d1-267">Arraste e solte o arquivo zip dos **conjuntos de dados** para as **telas do Estúdio AM**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="f12d1-268">Conecte a saída do ícone **dados de zip** à entrada do **Pacote de Scripts** do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="f12d1-269">Digite a função `source()` com o nome do arquivo zip na janela de código do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-270">No meu caso, digitei `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="f12d1-271">Lembre-se de clicar em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="f12d1-272">Uma vez concluídas essas etapas, o módulo [Executar Script R][execute-r-script] executará o script R no arquivo zip quando o experimento for executado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="f12d1-273">Agora seu teste deve ser semelhante à Figura 5.</span><span class="sxs-lookup"><span data-stu-id="f12d1-273">At this point your experiment should look something like Figure 5.</span></span>

![Teste usando o script de R compactado][6]

<span data-ttu-id="f12d1-275">*Figura 5. Experimente usar o R script compactado.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="f12d1-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="f12d1-276">Dataset1</span></span>
<span data-ttu-id="f12d1-277">Você pode passar uma tabela retangular de dados para seu código R usando a entrada Dataset1.</span><span class="sxs-lookup"><span data-stu-id="f12d1-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="f12d1-278">Em nosso script simples, a função `maml.mapInputPort(1)` lê os dados da porta 1.</span><span class="sxs-lookup"><span data-stu-id="f12d1-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="f12d1-279">Esses dados são então atribuídos a um nome de variável de quadro de dados em seu código.</span><span class="sxs-lookup"><span data-stu-id="f12d1-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="f12d1-280">Em nosso script simples a primeira linha de código realiza a atribuição.</span><span class="sxs-lookup"><span data-stu-id="f12d1-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="f12d1-281">Execute seu teste clicando no botão **Executar** .</span><span class="sxs-lookup"><span data-stu-id="f12d1-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="f12d1-282">Quando a execução for concluída, clique no módulo [Executar Script R][execute-r-script] e clique em **Exibir log de saída** no painel de propriedades.</span><span class="sxs-lookup"><span data-stu-id="f12d1-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="f12d1-283">Uma nova página deve aparecer em seu navegador, exibindo o conteúdo do arquivo output.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="f12d1-284">Ao rolar para baixo, você deve ver algo como o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f12d1-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="f12d1-285">Mais adiante na página, há informações mais detalhadas sobre as colunas, que parecerão com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="f12d1-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

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

<span data-ttu-id="f12d1-286">Esses resultados são como o esperado, com 228 observações e 9 colunas no dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="f12d1-287">Podemos ver os nomes de coluna, o tipo de dados R e um exemplo de cada coluna.</span><span class="sxs-lookup"><span data-stu-id="f12d1-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="f12d1-288">Essa mesma saída impressa está convenientemente disponível na saída do Dispositivo R do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-289">Discutiremos as saídas do módulo [Executar Script R][execute-r-script] na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="f12d1-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="f12d1-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="f12d1-290">Dataset2</span></span>
<span data-ttu-id="f12d1-291">O comportamento da entrada do Dataset2 é idêntico ao do Dataset1.</span><span class="sxs-lookup"><span data-stu-id="f12d1-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="f12d1-292">Usando essa entrada, você pode passar uma segunda tabela retangular de dados para o seu código R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="f12d1-293">A função `maml.mapInputPort(2)`, com o argumento 2, é usada para passar esses dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="f12d1-294">Execute as saídas do Script R</span><span class="sxs-lookup"><span data-stu-id="f12d1-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="f12d1-295">Exibir um dataframe</span><span class="sxs-lookup"><span data-stu-id="f12d1-295">Output a dataframe</span></span>
<span data-ttu-id="f12d1-296">Você pode exibir o conteúdo de um dataframe R como tabela retangular por meio da porta de resultados do Dataset1 usando a função `maml.mapOutputPort()` .</span><span class="sxs-lookup"><span data-stu-id="f12d1-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="f12d1-297">Em nosso script R simples, isso é realizado pela seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="f12d1-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="f12d1-298">Depois de executar o teste, clique na porta de saída do Dataset1 de Resultado e clique em **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="f12d1-299">Você deve ver algo como na Figura 6.</span><span class="sxs-lookup"><span data-stu-id="f12d1-299">You should see something like Figure 6.</span></span>

![A visualização da saída dos dados de derivados do leite da Califórnia][7]

<span data-ttu-id="f12d1-301">*Figura 6. A visualização da saída dos dados dos derivados de leite da Califórnia.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="f12d1-302">Esta saída parece idêntica à entrada, exatamente como se esperava.</span><span class="sxs-lookup"><span data-stu-id="f12d1-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="f12d1-303">Saída do Dispositivo R</span><span class="sxs-lookup"><span data-stu-id="f12d1-303">R Device output</span></span>
<span data-ttu-id="f12d1-304">A saída do Dispositivo do módulo [Executar Script R][execute-r-script] contém mensagens e saída de gráficos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="f12d1-305">As duas mensagens de erro padrão e de saída padrão de R são enviadas para a porta de saída do dispositivo R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="f12d1-306">Para exibir a saída do dispositivo R, clique na porta e, em seguida, em **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="f12d1-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="f12d1-307">Podemos ver a saída padrão e o erro padrão do script R na Figura 7.</span><span class="sxs-lookup"><span data-stu-id="f12d1-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Saída padrão e erro padrão da porta do Dispositivo R][8]

<span data-ttu-id="f12d1-309">*Figura 7. Saída padrão e erro padrão da porta do Dispositivo R.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="f12d1-310">Rolando para baixo podemos ver a saída de gráficos do nosso script R na Figura 8.</span><span class="sxs-lookup"><span data-stu-id="f12d1-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Saída de gráficos da porta do Dispositivo R][9]

<span data-ttu-id="f12d1-312">*Figura 8. Saída de gráficos da porta do Dispositivo R.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="f12d1-313"><a id="filtering"></a>Filtragem de dados e transformação</span><span class="sxs-lookup"><span data-stu-id="f12d1-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="f12d1-314">Nesta seção, vamos executar alguns dados básicos de filtragem e operações de transformação nos dados de produtos derivados de leite da Califórnia.</span><span class="sxs-lookup"><span data-stu-id="f12d1-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="f12d1-315">No final desta seção, teremos dados em um formato adequado para a criação de um modelo de análise.</span><span class="sxs-lookup"><span data-stu-id="f12d1-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="f12d1-316">Mais especificamente, nesta seção vamos executar várias tarefas de transformação e de limpeza de dados comuns: transformação de tipo, filtragem por dataframes, adição de novas colunas computadas e transformações de valor.</span><span class="sxs-lookup"><span data-stu-id="f12d1-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="f12d1-317">Este histórioco deve ajudá-lo a lidar com as diversas variações encontradas em problemas do mundo real.</span><span class="sxs-lookup"><span data-stu-id="f12d1-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="f12d1-318">O código completo R para esta seção está disponível no arquivo zip baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="f12d1-319">Transformações de tipo</span><span class="sxs-lookup"><span data-stu-id="f12d1-319">Type transformations</span></span>
<span data-ttu-id="f12d1-320">Agora que podemos ler os dados dos laticínios da Califórnia no código R no módulo [Executar Script R][execute-r-script], precisamos garantir que os dados nas colunas tenham o tipo e o formato desejados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="f12d1-321">R é uma linguagem tipificada dinamicamente, o que significa que os tipos de dados são forçados entre si quando necessário.</span><span class="sxs-lookup"><span data-stu-id="f12d1-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="f12d1-322">Os tipos de dados atômicos em R incluem numérico, lógico e de caractere.</span><span class="sxs-lookup"><span data-stu-id="f12d1-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="f12d1-323">O fator de tipo é usado para o armazenamento de dados categóricos de forma compacta.</span><span class="sxs-lookup"><span data-stu-id="f12d1-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="f12d1-324">Você pode obter mais informações sobre tipos de dados nas referências no [Apêndice B - Leitura adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="f12d1-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="f12d1-325">Quando dados tabulares são lidos em R de a partir de uma fonte externa, é sempre uma boa idéia verificar os tipos resultantes nas colunas.</span><span class="sxs-lookup"><span data-stu-id="f12d1-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="f12d1-326">Você pode desejar uma coluna de tipo de caractere, mas em muitos casos isso aparecerá como fator ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="f12d1-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="f12d1-327">Em outros casos, uma coluna que você acha que deve ser numérica é representada por dados de caracteres, por exemplo, '1,23' em vez de 1,23 como número de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="f12d1-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="f12d1-328">Felizmente, é fácil converter de um tipo para outro, desde que o mapeamento seja possível.</span><span class="sxs-lookup"><span data-stu-id="f12d1-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="f12d1-329">Por exemplo, você não pode converter “Nevada” para um valor numérico, mas você pode convertê-la em um fator (variável categórica).</span><span class="sxs-lookup"><span data-stu-id="f12d1-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="f12d1-330">Um outro exemplo, você pode converter um numérico 1 em um caractere “1” ou um fator.</span><span class="sxs-lookup"><span data-stu-id="f12d1-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="f12d1-331">A sintaxe para qualquer uma dessas conversões é simples: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="f12d1-332">Essas funções de conversão de tipo incluem os itens a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="f12d1-333">Observando os tipos de dados das colunas usadas como entrada na seção anterior: todas as colunas são do tipo numérico, exceto a coluna rotulada como 'Month', que é do tipo de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f12d1-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="f12d1-334">Vamos converter isso em um fator e os resultados do teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="f12d1-335">Excluí a linha que criou a matriz de dispersão e adicionei uma linha para converter a coluna 'Month' em um fator.</span><span class="sxs-lookup"><span data-stu-id="f12d1-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="f12d1-336">Em meu teste, vou simplesmente recortar e colar o código R na janela de código do módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="f12d1-337">Você também pode atualizar o arquivo zip e carregá-lo no Azure Machine Learning Studio, mas isso requer várias etapas.</span><span class="sxs-lookup"><span data-stu-id="f12d1-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="f12d1-338">Vamos executar esse código e examinar o log de saída para o script R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="f12d1-339">Os dados relevantes do log são mostrados na Figura 9.</span><span class="sxs-lookup"><span data-stu-id="f12d1-339">The relevant data from the log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="f12d1-340">*Figura 9. Resumo do dataframe com uma variável de fator.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="f12d1-341">O tipo de Mês deve agora indicar '**Fator c/ 14 níveis**'.</span><span class="sxs-lookup"><span data-stu-id="f12d1-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="f12d1-342">Isso é um problema, pois há apenas 12 meses no ano.</span><span class="sxs-lookup"><span data-stu-id="f12d1-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="f12d1-343">Você também pode verificar se o tipo em **Visualizar** da porta do Conjunto de dados de resultado é “**Categórico**”.</span><span class="sxs-lookup"><span data-stu-id="f12d1-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="f12d1-344">O problema é que a coluna “Month” não foi codificada sistematicamente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="f12d1-345">Em alguns casos, um mês é chamado de abril e, em outros, é abreviado como abril. Podemos pode resolver esse problema cortando a cadeia de caracteres para três caracteres.</span><span class="sxs-lookup"><span data-stu-id="f12d1-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="f12d1-346">Agora, a linha de código deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="f12d1-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="f12d1-347">Execute novamente o teste e exiba o log de saída.</span><span class="sxs-lookup"><span data-stu-id="f12d1-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="f12d1-348">Os resultados esperados são mostrados na Figura 10.</span><span class="sxs-lookup"><span data-stu-id="f12d1-348">The expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="f12d1-349">*Figura 10. Resumo do dataframe com o número correto de níveis de fator.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="f12d1-350">Nossa variável fator agora tem os 12 níveis desejados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="f12d1-351">Filtragem de dataframe básico</span><span class="sxs-lookup"><span data-stu-id="f12d1-351">Basic data frame filtering</span></span>
<span data-ttu-id="f12d1-352">Os dataframes R oferecem suporte a recursos avançados de filtragem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="f12d1-353">Conjuntos de dados podem ser subdivididos usando filtros lógicos em linhas ou colunas.</span><span class="sxs-lookup"><span data-stu-id="f12d1-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="f12d1-354">Em muitos casos, serão necessários critérios complexos de filtro.</span><span class="sxs-lookup"><span data-stu-id="f12d1-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="f12d1-355">As referências no [Apêndice B - leitura adicional](#appendixb) contêm exemplos extensivos de filtragem de dataframes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="f12d1-356">Há algumas filtragens que devemos fazer em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="f12d1-357">Se examinar as colunas no dataframe cadariydata, você verá duas colunas desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="f12d1-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="f12d1-358">A primeira coluna contém apenas um número de linha que não é muito útil.</span><span class="sxs-lookup"><span data-stu-id="f12d1-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="f12d1-359">A segunda coluna, Year.Month, contém informações redundantes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="f12d1-360">Podemos facilmente excluir essas colunas usando o código R a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="f12d1-361">De agora em diante nesta seção, só mostrarei o código adicional que estou adicionando ao módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="f12d1-362">Adicionarei cada nova linha **antes** da função `str()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="f12d1-363">Posso usar essa função para verificar os resultados no Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="f12d1-364">Adiciono a linha a seguir a meu código R no módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="f12d1-365">Execute esse código em seu teste e verifique o resultado no log de saída.</span><span class="sxs-lookup"><span data-stu-id="f12d1-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="f12d1-366">Esses resultados são mostrados na Figura 11.</span><span class="sxs-lookup"><span data-stu-id="f12d1-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="f12d1-367">*Figura 11. Resumo do dataframe com duas colunas removidas.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="f12d1-368">Boas notícias!</span><span class="sxs-lookup"><span data-stu-id="f12d1-368">Good news!</span></span> <span data-ttu-id="f12d1-369">Podemos obter os resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="f12d1-370">Adicionar uma nova coluna</span><span class="sxs-lookup"><span data-stu-id="f12d1-370">Add a new column</span></span>
<span data-ttu-id="f12d1-371">Para criar modelos de série de tempo é conveniente ter uma coluna que contenha os meses desde o início da série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="f12d1-372">Criaremos uma nova coluna “Month.Count”.</span><span class="sxs-lookup"><span data-stu-id="f12d1-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="f12d1-373">Para ajudar a organizar o código, vamos criar nossa primeira função simples, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="f12d1-374">Em seguida, aplicaremos essa função para criar uma nova coluna no dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="f12d1-375">O novo código é indicado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="f12d1-376">Agora execute o teste atualizado e use o log de saída para exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="f12d1-377">Esses resultados são mostrados na Figura 12.</span><span class="sxs-lookup"><span data-stu-id="f12d1-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="f12d1-378">*Figura 12. Resumo do dataframe com a coluna adicional.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="f12d1-379">Parece que tudo está funcionando.</span><span class="sxs-lookup"><span data-stu-id="f12d1-379">It looks like everything is working.</span></span> <span data-ttu-id="f12d1-380">Temos a nova coluna com os valores esperados em nosso dataframe</span><span class="sxs-lookup"><span data-stu-id="f12d1-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="f12d1-381">Transformações de valor</span><span class="sxs-lookup"><span data-stu-id="f12d1-381">Value transformations</span></span>
<span data-ttu-id="f12d1-382">Nesta seção, vamos executar algumas transformações simples nos valores de algumas das colunas de nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="f12d1-383">A linguagem R suporta transformações de valor quase que de forma arbitrária.</span><span class="sxs-lookup"><span data-stu-id="f12d1-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="f12d1-384">As referências no [Apêndice B - leitura adicional](#appendixb) contêm exemplos extensivos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="f12d1-385">Se examinar os valores nos resumos de nosso datafame, você notará algo estranho.</span><span class="sxs-lookup"><span data-stu-id="f12d1-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="f12d1-386">Há mais sorvetes do que leite produzido na Califórnia?</span><span class="sxs-lookup"><span data-stu-id="f12d1-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="f12d1-387">Não, certamente não, pois isso não faz sentido, além de triste pois alguns de nós amam sorvetes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="f12d1-388">As unidades são diferentes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-388">The units are different.</span></span> <span data-ttu-id="f12d1-389">O preço está em unidades de libras dos EUA, o leite está em unidades de um milhão de libras dos EUA, o sorvete está em unidades de 1.000 galões dos EUA e o queijo cottage está em unidades de 1.000 libras dos EUA.</span><span class="sxs-lookup"><span data-stu-id="f12d1-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="f12d1-390">Supondo que o sorvete pese aproximadamente 6,5 libras por galão, podemos facilmente fazer a multiplicação a fim de converter esses valores para que eles estejam todos em unidades iguais de 1.000 libras.</span><span class="sxs-lookup"><span data-stu-id="f12d1-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="f12d1-391">Para nosso modelo de previsão, usamos um modelo de multiplicação para tendência e ajuste sazonal desses dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="f12d1-392">Uma transformação de log nos permite usar um modelo linear, simplificando esse processo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="f12d1-393">Podemos aplicar a transformação de log na mesma função em que o multiplicador será aplicado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="f12d1-394">No código a seguir, defino uma nova função, `log.transform()`, e a aplico às linhas que contêm os valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="f12d1-395">A função R `Map()` é usada para aplicar a função `log.transform()` às colunas selecionadas do dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="f12d1-396">`Map()` é semelhante a `apply()` mas permite mais de uma lista de argumentos para a função.</span><span class="sxs-lookup"><span data-stu-id="f12d1-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="f12d1-397">Observe que uma lista de multiplicadores fornece o segundo argumento para a função `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="f12d1-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="f12d1-398">A função `na.omit()` é usada como um pouco de limpeza, para garantir que não haja valores ausentes ou indefinidos no dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="f12d1-399">Muitas coisas estão acontecendo na função `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="f12d1-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="f12d1-400">A maior parte do código verifica se há possíveis problemas com os argumentos ou lida com exceções, que ainda podem surgir durante os cálculos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="f12d1-401">Apenas algumas linhas desse código realmente fazem os cálculos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="f12d1-402">O objetivo da programação de defesa é evitar a falha de uma única função que impeça que o processamento continue.</span><span class="sxs-lookup"><span data-stu-id="f12d1-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="f12d1-403">Uma falha abrupta de uma análise de execução longa pode ser muito frustrante para os usuários.</span><span class="sxs-lookup"><span data-stu-id="f12d1-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="f12d1-404">Para evitar essa situação, devem ser escolhidos valores de retorno padrão que limitem os danos ao processamento downstream.</span><span class="sxs-lookup"><span data-stu-id="f12d1-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="f12d1-405">Uma mensagem também é emitida para alertar os usuários que algo deu errado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="f12d1-406">Se você não está acostumado à programação defensiva em R, todo esse código pode parecer um pouco sobrecarregado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="f12d1-407">Eu o orientarei durante as etapas principais:</span><span class="sxs-lookup"><span data-stu-id="f12d1-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="f12d1-408">Um vetor de quatro mensagens é definido.</span><span class="sxs-lookup"><span data-stu-id="f12d1-408">A vector of four messages is defined.</span></span> <span data-ttu-id="f12d1-409">Essas mensagens são usadas para comunicar informações sobre alguns dos possíveis erros e exceções que podem ocorrer com esse código.</span><span class="sxs-lookup"><span data-stu-id="f12d1-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="f12d1-410">Posso retornar um valor NA para cada caso.</span><span class="sxs-lookup"><span data-stu-id="f12d1-410">I return a value of NA for each case.</span></span> <span data-ttu-id="f12d1-411">Há muitas outras possibilidades que podem ter menos efeitos colaterais.</span><span class="sxs-lookup"><span data-stu-id="f12d1-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="f12d1-412">Eu poderia retornar um vetor de zeros ou o vetor de entrada original, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="f12d1-413">As verificações são executadas nos argumentos para a função.</span><span class="sxs-lookup"><span data-stu-id="f12d1-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="f12d1-414">Em cada caso, se for detectado um erro, será retornado um valor padrão, e uma mensagem será produzida pela função `warning()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="f12d1-415">Estou usando `warning()` em vez de `stop()`, pois essa segunda opção encerrará a execução, justamente o que estou tentando evitar.</span><span class="sxs-lookup"><span data-stu-id="f12d1-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="f12d1-416">Observe que eu escrevi este código em um estilo de procedimento, pois nesse caso uma abordagem funcional me parece complexa e obscura.</span><span class="sxs-lookup"><span data-stu-id="f12d1-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="f12d1-417">As computações de log são encapsuladas em `tryCatch()` para que as exceções não causem uma interrupção abrupta no processamento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="f12d1-418">Sem `tryCatch()` , a maioria dos erros gerada pelas funções de R resulta em um sinal de interrupção, que faz exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="f12d1-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="f12d1-419">Executar esse código R em seu teste e veja a saída impressa no output.log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="f12d1-420">Agora, você verá os valores transformados das quatro colunas no log, conforme mostrado na Figura 13.</span><span class="sxs-lookup"><span data-stu-id="f12d1-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="f12d1-421">*Figura 13. Resumo dos valores transformados no dataframe.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="f12d1-422">Vemos que os valores foram transformados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-422">We see the values have been transformed.</span></span> <span data-ttu-id="f12d1-423">Agora, a produção de leite excede bastante a produção de todos os outros produtos derivados do leite, lembrando que agora estamos analisando uma escala logarítmica.</span><span class="sxs-lookup"><span data-stu-id="f12d1-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="f12d1-424">Neste momento, os dados são limpos e estamos prontos para a modelagem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="f12d1-425">Observando o resumo da visualização para a saída do Conjunto de Dados de Resultado de nosso módulo [Executar Script R][execute-r-script], você verá que a coluna “Month” é “Categorical”, com 12 valores exclusivos, novamente, como desejávamos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="f12d1-426"><a id="timeseries"></a>Análise de correlação e objetos de série temporal</span><span class="sxs-lookup"><span data-stu-id="f12d1-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="f12d1-427">Nesta seção vamos explorar alguns objetos básicos de série de tempo de R e vamos analisar as correlações entre algumas das variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="f12d1-428">Nosso objetivo é obter um dataframe de saída que contenha as informações de correlação de pares em várias defasagens.</span><span class="sxs-lookup"><span data-stu-id="f12d1-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="f12d1-429">O código R completo para esta seção está disponível no arquivo zip baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="f12d1-430">Objetos de série temporal em R</span><span class="sxs-lookup"><span data-stu-id="f12d1-430">Time series objects in R</span></span>
<span data-ttu-id="f12d1-431">Como já mencionado, as série de tempo são uma série de valores de dados indexados por tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="f12d1-432">Objetos de série de tempo R são usados para criar e gerenciar o índice de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="f12d1-433">Há diversas vantagens em usar objetos de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="f12d1-434">Os objetos de série temporal evitam que você tenha que lidar com os vários detalhes do gerenciamento dos valores de índice da série temporal que são encapsulados no objeto.</span><span class="sxs-lookup"><span data-stu-id="f12d1-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="f12d1-435">Além disso, os objetos de série de tempo permitem que você use vários métodos de série de tempo para plotar, imprimir, modelar etc.</span><span class="sxs-lookup"><span data-stu-id="f12d1-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="f12d1-436">A classe de série de tempo POSIXct é comumente usada e é relativamente simples.</span><span class="sxs-lookup"><span data-stu-id="f12d1-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="f12d1-437">Essa classe de série de tempo mede o tempo a partir do início da época, 1º de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="f12d1-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="f12d1-438">Vamos usar objetos de série de tempo POSIXct neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="f12d1-439">Outras classes de objeto de série de tempo amplamente utilizados em R incluem zoo e xts, série temporal extensível.</span><span class="sxs-lookup"><span data-stu-id="f12d1-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="f12d1-440">Exemplo de objeto de série temporal</span><span class="sxs-lookup"><span data-stu-id="f12d1-440">Time series object example</span></span>
<span data-ttu-id="f12d1-441">Vamos começar com o nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-441">Let's get started with our example.</span></span> <span data-ttu-id="f12d1-442">Arraste e solte um **novo** módulo [Executar Script R][execute-r-script] em seu experimento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="f12d1-443">Conecte a porta de saída do Conjunto de Dados de Resultado 1 do módulo [Executar Script R][execute-r-script] existente à porta de entrada do Conjunto de Dados de Resultado 1 do novo módulo [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="f12d1-444">Como fiz nos primeiros exemplos, ao progredirmos no exemplo, em alguns pontos vou mostrar apenas as linhas adicionais incrementais do código R em cada etapa.</span><span class="sxs-lookup"><span data-stu-id="f12d1-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="f12d1-445">Lendo o dataframe</span><span class="sxs-lookup"><span data-stu-id="f12d1-445">Reading the dataframe</span></span>
<span data-ttu-id="f12d1-446">Como primeira etapa, vamos ler um dataframe e verificar se obtemos os resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="f12d1-447">O código a seguir deve ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="f12d1-448">Agora, execute o teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-448">Now, run the experiment.</span></span> <span data-ttu-id="f12d1-449">O log da nova forma Executar Script R deve parecer com a Figura 14.</span><span class="sxs-lookup"><span data-stu-id="f12d1-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="f12d1-450">*Figura 14. Resumo do dataframe no módulo Executar Script R.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="f12d1-451">Esses dados são dos tipos e formato esperados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-451">This data is of the expected types and format.</span></span> <span data-ttu-id="f12d1-452">Observe que a coluna “Month” é do fator tipo e tem o número esperado de níveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="f12d1-453">Criando um objeto de série temporal</span><span class="sxs-lookup"><span data-stu-id="f12d1-453">Creating a time series object</span></span>
<span data-ttu-id="f12d1-454">Precisamos adicionar um objeto de série de tempo ao nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="f12d1-455">Substitua o código atual pelo exemplo a seguir, que adiciona uma nova coluna da classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="f12d1-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="f12d1-456">Agora, verifique o log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-456">Now, check the log.</span></span> <span data-ttu-id="f12d1-457">Deve se parecer com a Figura 15.</span><span class="sxs-lookup"><span data-stu-id="f12d1-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="f12d1-458">*Figura 15. Resumo do dataframe com um objeto de série temporal.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="f12d1-459">Podemos ver o resumo a nova coluna é de fato da classe POSIXct.</span><span class="sxs-lookup"><span data-stu-id="f12d1-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="f12d1-460">Explorando e transformando os dados</span><span class="sxs-lookup"><span data-stu-id="f12d1-460">Exploring and transforming the data</span></span>
<span data-ttu-id="f12d1-461">Vamos explorar algumas das variáveis deste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f12d1-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="f12d1-462">Uma matriz de scatterplot é uma boa maneira para darmos uma olhada rápida.</span><span class="sxs-lookup"><span data-stu-id="f12d1-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="f12d1-463">Estou substituindo a função `str()` no código R anterior pela linha a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="f12d1-464">Execute esse código e veja o que acontece.</span><span class="sxs-lookup"><span data-stu-id="f12d1-464">Run this code and see what happens.</span></span> <span data-ttu-id="f12d1-465">A plotagem produzida na porta do dispositivo R deve parecer com a Figura 16.</span><span class="sxs-lookup"><span data-stu-id="f12d1-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Matriz de dispersão de variáveis selecionadas][17]

<span data-ttu-id="f12d1-467">*Figura 16. Matriz de dispersão de variáveis selecionadas.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="f12d1-468">Há alguma estrutura estranha nas relações entre essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="f12d1-469">Talvez isso surja de tendências nos dados e do fato de que não padronizamos as variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="f12d1-470">Análise de correlação</span><span class="sxs-lookup"><span data-stu-id="f12d1-470">Correlation analysis</span></span>
<span data-ttu-id="f12d1-471">Para executar análise de correlação, precisamos padronizar e eliminar tendências das variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="f12d1-472">Poderíamos simplesmente usar a função `scale()` de R, que centraliza e dimensiona variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="f12d1-473">Essa função também pode ser executada mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-473">This function might well run faster.</span></span> <span data-ttu-id="f12d1-474">No entanto, eu quero mostrar um exemplo de programação defensiva em R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="f12d1-475">A função `ts.detrend()` abaixo executa ambas essas operações.</span><span class="sxs-lookup"><span data-stu-id="f12d1-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="f12d1-476">As duas linhas de código a seguir eliminam os dados de tendência e, em seguida, padronizam os valores.</span><span class="sxs-lookup"><span data-stu-id="f12d1-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="f12d1-477">Muitas coisas estão acontecendo na função `ts.detrend()` .</span><span class="sxs-lookup"><span data-stu-id="f12d1-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="f12d1-478">A maior parte do código verifica se há possíveis problemas com os argumentos ou lida com exceções, que ainda podem surgir durante os cálculos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="f12d1-479">Apenas algumas linhas desse código realmente fazem os cálculos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="f12d1-480">Já abordamos a um exemplo de programação defensiva em [Transformações de valor](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="f12d1-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="f12d1-481">Os dois blocos de computação estão encapsulados em `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="f12d1-482">Para alguns erros, faz sentido retornar ao vetor original de entrada e, em outros casos, retornar a um vetor de zeros.</span><span class="sxs-lookup"><span data-stu-id="f12d1-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="f12d1-483">Observe que a regressão linear usada para a eliminação de tendência é uma regressão de uma série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="f12d1-484">A variável preditora é um objeto de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="f12d1-485">Quando `ts.detrend()` é definido, aplicamos as variáveis de interesse em nosso dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="f12d1-486">Devemos forçar a lista resultante criada por `lapply()` nos dados do dataframe usando `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="f12d1-487">Devido aos aspectos defensivos de `ts.detrend()`, se uma das variáveis não for processada, isso não impedirá o processamento correto das outras.</span><span class="sxs-lookup"><span data-stu-id="f12d1-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="f12d1-488">A última linha do código cria um par scatterplot.</span><span class="sxs-lookup"><span data-stu-id="f12d1-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="f12d1-489">Após a execução do código R, os resultados da dispersão são mostrados na Figura 17.</span><span class="sxs-lookup"><span data-stu-id="f12d1-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Emparelhar a dispersão da série temporal padronizada e sem tendências][18]

<span data-ttu-id="f12d1-491">*Figura 17. Emparelhe o scatterplot da séries de tempo padronizada e sem tendências.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="f12d1-492">Você pode comparar esses resultados aos mostrados na Figura 16.</span><span class="sxs-lookup"><span data-stu-id="f12d1-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="f12d1-493">Com a tendência removida e as variáveis padronizadas, vemos muito menos estrutura nas relações entre essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="f12d1-494">O código para calcular as correlações como objetos ccf R é indicado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="f12d1-495">Executar esse código produz o log mostrado na Figura 18.</span><span class="sxs-lookup"><span data-stu-id="f12d1-495">Running this code produces the log shown in Figure 18.</span></span>

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

<span data-ttu-id="f12d1-496">*Figura 18. Lista de objetos ccf de análise de correlação emparelhados.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="f12d1-497">Há um valor de correlação para cada intervalo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="f12d1-498">Nenhum desses valores de correlação é grande o suficiente para ser significativo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="f12d1-499">Podemos, portanto, concluir que é possível modelar cada variável de forma independente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="f12d1-500">Exibir um dataframe</span><span class="sxs-lookup"><span data-stu-id="f12d1-500">Output a dataframe</span></span>
<span data-ttu-id="f12d1-501">Podemos ter calculado as correlações emparelhadas como uma lista de objetos ccf R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="f12d1-502">Isso apresenta um pequeno problema, pois a porta de saída do conjunto de dados resultado exige um dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="f12d1-503">Além disso, o objeto ccf é uma lista e queremos apenas os valores no primeiro elemento dessa lista, as correlações em vários intervalos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="f12d1-504">O código a seguir extrai os valores de intervalo da lista de objetos ccf, que também são listas.</span><span class="sxs-lookup"><span data-stu-id="f12d1-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="f12d1-505">A primeira linha de código é um pouco complicada, e algumas explicações podem ajudá-lo a entendê-la.</span><span class="sxs-lookup"><span data-stu-id="f12d1-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="f12d1-506">Trabalhando de dentro para fora, temos o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f12d1-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="f12d1-507">O operador '**[[**' com o argumento '**1**' seleciona o vetor de correlações nas defasagens do primeiro elemento da lista de objetos ccf.</span><span class="sxs-lookup"><span data-stu-id="f12d1-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="f12d1-508">A função `do.call()` aplica-se à função `rbind()` nos elementos de lista retornados por `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="f12d1-509">A função `data.frame()` converte o resultado produzido por `do.call()` em um dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="f12d1-510">Observe que os nomes das linhas estão na coluna do dataframe.</span><span class="sxs-lookup"><span data-stu-id="f12d1-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="f12d1-511">Fazer isso preserva os nomes de linha quando eles são a saída de [Executar Script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="f12d1-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="f12d1-512">A execução do código produz o resultado mostrado na Figura 19 quando eu **Visualizar** a saída da porta do conjunto de dados do resultado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="f12d1-513">Os nomes de linha estão na primeira coluna, conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-513">The row names are in the first column, as intended.</span></span>

![Resultados da saída da análise de correlação][20]

<span data-ttu-id="f12d1-515">*Figura 19. Saída de resultados da análise de correlação.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="f12d1-516"><a id="seasonalforecasting"></a>Exemplo de série temporal: previsão sazonal</span><span class="sxs-lookup"><span data-stu-id="f12d1-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="f12d1-517">Nossos dados agora estão em um formato adequado para análise, e determinamos que não há correlação significativa entre as variáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="f12d1-518">Vamos continuar e criar um modelo de previsão de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="f12d1-519">Usando esse modelo vamos prever a produção de leite da Califórnia para os 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="f12d1-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="f12d1-520">Nosso modelo de previsão terá dois componentes, um componente de tendência e um componente sazonal.</span><span class="sxs-lookup"><span data-stu-id="f12d1-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="f12d1-521">A previsão concluída é o produto desses dois componentes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="f12d1-522">Esse tipo de modelo é conhecido como modelo de multiplicação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="f12d1-523">A alternativa é um modelo de adição.</span><span class="sxs-lookup"><span data-stu-id="f12d1-523">The alternative is an additive model.</span></span> <span data-ttu-id="f12d1-524">Já aplicamos uma transformação logarítmica às variáveis de interesse, o que torna essa análise manejável.</span><span class="sxs-lookup"><span data-stu-id="f12d1-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="f12d1-525">O código R completo para esta seção está disponível no arquivo zip baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="f12d1-526">Criando o dataframe para análise</span><span class="sxs-lookup"><span data-stu-id="f12d1-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="f12d1-527">Comece adicionando um **novo** módulo [Executar Script R][execute-r-script] ao seu experimento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="f12d1-528">Conecte a saída do **Conjunto de Dados de Resultado** do módulo [Executar Script R][execute-r-script] existente à entrada do **Conjunto de Dados 1** do novo módulo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="f12d1-529">O resultado deve ser semelhante a Figura 20.</span><span class="sxs-lookup"><span data-stu-id="f12d1-529">The result should look something like Figure 20.</span></span>

![O teste com o novo módulo Executar Script R adicionado][21]

<span data-ttu-id="f12d1-531">*Figura 20. O teste com o novo módulo Executar Script R adicionado.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="f12d1-532">Como a análise de correlação que acabamos de concluir, precisamos adicionar uma coluna com um objeto de série de tempo POSIXct.</span><span class="sxs-lookup"><span data-stu-id="f12d1-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="f12d1-533">O código a seguir fará exatamente isso.</span><span class="sxs-lookup"><span data-stu-id="f12d1-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="f12d1-534">Execute esse código e examine o log.</span><span class="sxs-lookup"><span data-stu-id="f12d1-534">Run this code and look at the log.</span></span> <span data-ttu-id="f12d1-535">O resultado deve ser semelhante a Figura 21.</span><span class="sxs-lookup"><span data-stu-id="f12d1-535">The result should look like Figure 21.</span></span>

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

<span data-ttu-id="f12d1-536">*Figura 21. Resumo do dataframe.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="f12d1-537">Com esse resultado, você está pronto para iniciar nossa análise.</span><span class="sxs-lookup"><span data-stu-id="f12d1-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="f12d1-538">Criar um conjunto de dados de treinamento</span><span class="sxs-lookup"><span data-stu-id="f12d1-538">Create a training dataset</span></span>
<span data-ttu-id="f12d1-539">Com o dataframe construído, precisamos criar um conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="f12d1-540">Esses dados incluirão todas as observações exceto as últimas 12, do ano de 2013, as quais são o nosso conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="f12d1-541">O seguinte código subagrupa o dataframe e cria plotagens de produção de derivados de leite e de as variáveis de preço.</span><span class="sxs-lookup"><span data-stu-id="f12d1-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="f12d1-542">Então, eu crio plotagens das quatro produções e variáveis de preços.</span><span class="sxs-lookup"><span data-stu-id="f12d1-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="f12d1-543">Uma função anônima é usada para definir alguns argumentos para a plotagem e, em seguida, para iterar a lista dos outros dois argumentos com `Map()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="f12d1-544">Se você estiver pensando que um loop funcionaria bem aqui, você está certo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="f12d1-545">Mas, como R é uma linguagem funcional, estou lhe mostrando uma abordagem funcional.</span><span class="sxs-lookup"><span data-stu-id="f12d1-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="f12d1-546">Executar o código produz séries de plotagens de série de tempo da saída do dispositivo R mostrada na Figura 22.</span><span class="sxs-lookup"><span data-stu-id="f12d1-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="f12d1-547">Observe que o eixo de tempo é em unidades de datas, uma bela vantagem do método de plotagem de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![Primeira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segunda das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terceira das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarta das plotagens de série temporal dos dados de produção e preço de derivados de leite da Califórnia](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="f12d1-552">*Figura 22. Plotagens de série temporal dos dados de produção e preço de derivados do leite da Califórnia.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="f12d1-553">Um modelo de tendência</span><span class="sxs-lookup"><span data-stu-id="f12d1-553">A trend model</span></span>
<span data-ttu-id="f12d1-554">Depois de criar um objeto de série de tempo e de ter examinado os dados, vamos começar a construir um modelo de tendência para os dados de produção leite da Califórnia.</span><span class="sxs-lookup"><span data-stu-id="f12d1-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="f12d1-555">Podemos fazer isso com uma regressão da série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-555">We can do this with a time series regression.</span></span> <span data-ttu-id="f12d1-556">No entanto, fica claro na plotagem que é necessário mais do que uma inclinação e uma interceptação para modelar com precisão a tendência observada nos dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="f12d1-557">Dada uma pequena escala de dados, vou criar o modelo para a tendência no RStudio e, em seguida, vou recortar e colar o modelo resultante no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="f12d1-558">O RStudio fornece um ambiente adequado para esse tipo de análise interativa.</span><span class="sxs-lookup"><span data-stu-id="f12d1-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="f12d1-559">Como primeira tentativa, tentarei uma regressão polinomial com poderes de até 3.</span><span class="sxs-lookup"><span data-stu-id="f12d1-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="f12d1-560">Existe um perigo real de sobreajuste desses tipos de modelos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="f12d1-561">Portanto, é melhor evitar condições de ordem mais alta.</span><span class="sxs-lookup"><span data-stu-id="f12d1-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="f12d1-562">A função `I()` inibe a interpretação do conteúdo (interpreta o conteúdo 'como está') e permite que você grave uma função interpretada literalmente em uma equação de regressão.</span><span class="sxs-lookup"><span data-stu-id="f12d1-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="f12d1-563">Isso gera o resultado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-563">This generates the following.</span></span>

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

<span data-ttu-id="f12d1-564">Dos valores de P (Pr(>|t|)) nessa saída, podemos ver que o termo ao quadrado pode não ser significativo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="f12d1-565">Vou usar a função `update()` para modificar esse modelo eliminado o termo ao quadrado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="f12d1-566">Isso gera o resultado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-566">This generates the following.</span></span>

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

<span data-ttu-id="f12d1-567">Assim parece melhor.</span><span class="sxs-lookup"><span data-stu-id="f12d1-567">This looks better.</span></span> <span data-ttu-id="f12d1-568">Todos os termos são significativos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-568">All of the terms are significant.</span></span> <span data-ttu-id="f12d1-569">No entanto, o valor de 2e-16 é um valor padrão e não deve ser levado muito a sério.</span><span class="sxs-lookup"><span data-stu-id="f12d1-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="f12d1-570">Para teste de sensatez, vamos criar uma plotagem de série de tempo dos dados da produção de derivados de leite da Califórnia com a curva de tendência mostrada.</span><span class="sxs-lookup"><span data-stu-id="f12d1-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="f12d1-571">Adicionei o código a seguir ao modelo [Executar Script R][execute-r-script] do Azure Machine Learning (não o RStudio) para criar o modelo e fazer uma plotagem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="f12d1-572">O resultado é mostrado na Figura 23.</span><span class="sxs-lookup"><span data-stu-id="f12d1-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dados de produção de leite da Califórnia com o modelo de tendência mostrado](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="f12d1-574">*Figura 23. Dados de produção leite da Califórnia com o modelo de tendência mostrado.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="f12d1-575">Parece que o modelo de tendência se ajusta aos dados muito bem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="f12d1-576">Além disso, não parece ter evidência de ajuste excessivo, como agitações estranhas na curva de modelo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="f12d1-577">Modelo sazonal</span><span class="sxs-lookup"><span data-stu-id="f12d1-577">Seasonal model</span></span>
<span data-ttu-id="f12d1-578">Com um modelo de tendência em mãos, precisamos continuar e incluir efeitos sazonais.</span><span class="sxs-lookup"><span data-stu-id="f12d1-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="f12d1-579">Usaremos o mês do ano como uma variável fictícia no modelo linear para capturar o efeito de mês a mês.</span><span class="sxs-lookup"><span data-stu-id="f12d1-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="f12d1-580">Observe que quando você introduz variáveis fator em um modelo, a interceptação não deve ser computada.</span><span class="sxs-lookup"><span data-stu-id="f12d1-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="f12d1-581">Se você não fizer isso, a fórmula será muito especificada e R descartará um dos fatores desejados, mas manterá o termo de interceptação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="f12d1-582">Como temos um modelo de tendência satisfatório, podemos usar a função `update()` para adicionar novos termos ao modelo existente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="f12d1-583">-1 na atualização da fórmula descarta o termo de interceptação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="f12d1-584">Continuando em RStudio:</span><span class="sxs-lookup"><span data-stu-id="f12d1-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="f12d1-585">Isso gera o resultado a seguir.</span><span class="sxs-lookup"><span data-stu-id="f12d1-585">This generates the following.</span></span>

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

<span data-ttu-id="f12d1-586">Vemos que o modelo não tem um termo de interceptação e tem 12 fatores mês significativos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="f12d1-587">Isso é exatamente o que queremos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="f12d1-588">Vamos fazer outra plotagem de série de tempo dos dados de produção de derivados de leite da Califórnia para ver até que ponto o modelo sazonal está funcionando.</span><span class="sxs-lookup"><span data-stu-id="f12d1-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="f12d1-589">Adicionei o seguinte código ao modelo [Executar Script R][execute-r-script] Azure Machine Learning para criar o modelo e fazer uma plotagem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="f12d1-590">Executar esse código no Azure Machine Learning produz a plotagem mostrada na Figura 24.</span><span class="sxs-lookup"><span data-stu-id="f12d1-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![Produção de leite da Califórnia com o modelo, incluindo efeitos sazonais](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="f12d1-592">*Figura 24. Produção de leite na Califórnia com o modelo dos efeitos sazonais.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="f12d1-593">O ajuste para os dados mostrados na Figura 24 é bastante encorajador.</span><span class="sxs-lookup"><span data-stu-id="f12d1-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="f12d1-594">A tendência e o efeito sazonal (variação mensal) parecem razoáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="f12d1-595">Como outra verificação em nosso modelo, vamos dar uma olhada nos resíduos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="f12d1-596">O código a seguir calcula os valores previstos de nossos dois modelos, calcula os resíduos para o modelo sazonal e, então, plota esses resíduos nos dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="f12d1-597">A plotagem restante é mostrada na Figura 25.</span><span class="sxs-lookup"><span data-stu-id="f12d1-597">The residual plot is shown in Figure 25.</span></span>

![Resíduos do modelo sazonal para os dados de treinamento](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="f12d1-599">*Figura 25. Resíduos do modelo sazonal para os dados de treinamento.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="f12d1-600">Esses resíduos parecem razoáveis.</span><span class="sxs-lookup"><span data-stu-id="f12d1-600">These residuals look reasonable.</span></span> <span data-ttu-id="f12d1-601">Não há nenhuma estrutura em particular, exceto o efeito da recessão de 2008 e 2009, que nosso modelo não leva em conta bem.</span><span class="sxs-lookup"><span data-stu-id="f12d1-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="f12d1-602">A plotagem mostrada na Figura 25 é útil para detectar qualquer padrão dependente de tempo nos resíduos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="f12d1-603">A abordagem explícita de computação e plotagem residual que eu sei coloca os resíduos na ordem de tempo no gráfico.</span><span class="sxs-lookup"><span data-stu-id="f12d1-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="f12d1-604">Se, por outro lado, eu tivesse plotado `milk.lm$residuals`, a plotagem não estaria em ordem de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="f12d1-605">Também é possível usar `plot.lm()` para produzir uma série de gráficos de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="f12d1-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="f12d1-606">Esse código gera uma série de gráficos de diagnóstico mostrados na Figura 26.</span><span class="sxs-lookup"><span data-stu-id="f12d1-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Primeira das plotagens de diagnóstico do modelo sazonal](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segunda das plotagens de diagnóstico do modelo sazonal](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terceira das plotagens de diagnóstico do modelo sazonal](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarta das plotagens de diagnóstico do modelo sazonal](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="f12d1-611">*Figura 26. Gráficos de diagnóstico de gráficos para o modelo sazonal.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="f12d1-612">Há alguns pontos de grande influencia identificados nessas representações gráficas, mas eles não causam muita preocupação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="f12d1-613">Além disso, podemos ver pela plotagem Q-Q Normal que os resíduos são próximos ao normalmente distribuídos, uma suposição importante para os modelos lineares.</span><span class="sxs-lookup"><span data-stu-id="f12d1-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="f12d1-614">Avaliação de previsão e modelo</span><span class="sxs-lookup"><span data-stu-id="f12d1-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="f12d1-615">Tem só mais uma coisa para concluir o nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="f12d1-616">Precisamos calcular as previsões e medir o erro em relação aos dados reais.</span><span class="sxs-lookup"><span data-stu-id="f12d1-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="f12d1-617">Nossa previsão será para os 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="f12d1-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="f12d1-618">Podemos calcular uma medida de erro para essa previsão para os dados reais que não fazem parte de nosso conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="f12d1-619">Além disso, podemos comparar o desempenho em 18 anos de dados de treinamento com os 12 meses de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="f12d1-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="f12d1-620">Um número de métricas é usado para medir o desempenho dos modelos de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="f12d1-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="f12d1-621">Em nosso caso, usaremos o erro de RMS (raiz quadrada média).</span><span class="sxs-lookup"><span data-stu-id="f12d1-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="f12d1-622">A função a seguir calcula o erro RMS entre duas séries.</span><span class="sxs-lookup"><span data-stu-id="f12d1-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
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

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="f12d1-623">Assim como na função `log.transform()` , discutida na seção "Transformações de valor", há muitas verificações de erros e exceções de código de recuperação nessa função.</span><span class="sxs-lookup"><span data-stu-id="f12d1-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="f12d1-624">Os princípios empregados são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-624">The principles employed are the same.</span></span> <span data-ttu-id="f12d1-625">O trabalho é feito em dois lugares ajustados em `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="f12d1-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="f12d1-626">Em primeiro lugar, a série de tempo é de exponenciação, pois temos trabalhado com os valores dos logarítmos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="f12d1-627">Em segundo lugar, o erro real do RMS é computado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="f12d1-628">Equipado com uma função para medir o erro RMS, vamos criar e exibir um dataframe que contenha os erros de RMS.</span><span class="sxs-lookup"><span data-stu-id="f12d1-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="f12d1-629">Incluiremos termos para o modelo de tendência sozinho e o modelo completo com fatores sazonais.</span><span class="sxs-lookup"><span data-stu-id="f12d1-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="f12d1-630">O código a seguir faz o trabalho usando os dois modelos lineares que construímos.</span><span class="sxs-lookup"><span data-stu-id="f12d1-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
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

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="f12d1-631">Executar esse código produz a saída mostrada na Figura 27 na porta de saída de conjunto de dados do resultado.</span><span class="sxs-lookup"><span data-stu-id="f12d1-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Comparação de erro do RMS para os modelos][26]

<span data-ttu-id="f12d1-633">*Figura 27. Comparação de erro do RMS com os modelos.*</span><span class="sxs-lookup"><span data-stu-id="f12d1-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="f12d1-634">Com base nesses resultados, podemos ver que a adição dos fatores sazonais ao modelo reduz o erro RMS significativamente.</span><span class="sxs-lookup"><span data-stu-id="f12d1-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="f12d1-635">Não é muito surpreendente, o erro RMS para os dados de treinamento é um pouco menor que para a previsão.</span><span class="sxs-lookup"><span data-stu-id="f12d1-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="f12d1-636"><a id="appendixa"></a>APÊNDICE A: Guia do RStudio</span><span class="sxs-lookup"><span data-stu-id="f12d1-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="f12d1-637">O RStudio é muito bem documentado, portanto neste apêndice fornecerei alguns links para as seções principais da documentação RStudio para você começar.</span><span class="sxs-lookup"><span data-stu-id="f12d1-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="f12d1-638">Criando projetos</span><span class="sxs-lookup"><span data-stu-id="f12d1-638">Creating projects</span></span>
   
   <span data-ttu-id="f12d1-639">Você pode organizar e gerenciar seu código R em projetos usando o RStudio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="f12d1-640">A documentação que usa projetos pode ser encontrada em https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="f12d1-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="f12d1-641">Eu recomendo que você siga estas instruções e crie um projeto para os exemplos de código R neste documento.</span><span class="sxs-lookup"><span data-stu-id="f12d1-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="f12d1-642">Editar e executar código R</span><span class="sxs-lookup"><span data-stu-id="f12d1-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="f12d1-643">O RStudio fornece um ambiente integrado para editar e executar código R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="f12d1-644">A documentação pode ser encontrada em https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="f12d1-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="f12d1-645">Depurando</span><span class="sxs-lookup"><span data-stu-id="f12d1-645">Debugging</span></span>
   
   <span data-ttu-id="f12d1-646">O RStudio inclui recursos avançados de depuração.</span><span class="sxs-lookup"><span data-stu-id="f12d1-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="f12d1-647">A documentação para esses recursos estão em https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="f12d1-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="f12d1-648">Os recursos de solução de problemas do ponto de interrupção estão em https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="f12d1-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="f12d1-649"><a id="appendixb"></a>APÊNDICE B: Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="f12d1-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="f12d1-650">Este tutorial de programação R aborda os conceitos básicos de que você precisa para usar a linguagem R com o Studio de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f12d1-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="f12d1-651">Se você não estiver familiarizado com R, duas introduções estão disponíveis no CRAN:</span><span class="sxs-lookup"><span data-stu-id="f12d1-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="f12d1-652">R para iniciantes de Emmanuel Paradis é um bom ponto de partida em http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="f12d1-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="f12d1-653">An Introduction to R, por W. N.</span><span class="sxs-lookup"><span data-stu-id="f12d1-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="f12d1-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="f12d1-654">Venables et.</span></span> <span data-ttu-id="f12d1-655">al.</span><span class="sxs-lookup"><span data-stu-id="f12d1-655">al.</span></span> <span data-ttu-id="f12d1-656">se aprofunda um pouco mais em http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="f12d1-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="f12d1-657">Existem muitos livros sobre R que podem ajudá-lo a começar.</span><span class="sxs-lookup"><span data-stu-id="f12d1-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="f12d1-658">Aqui estão alguns que considero úteis:</span><span class="sxs-lookup"><span data-stu-id="f12d1-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="f12d1-659">The Art of R Programming; A Tour of Statistical Software Design, de Norman Matloff, é uma excelente introdução à programação em R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="f12d1-660">R Cookbook, de Paul Teetor, fornece uma abordagem de problemas e soluções usando R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="f12d1-661">R in Action, por Robert Kabacoff, é outro livro introdutório útil.</span><span class="sxs-lookup"><span data-stu-id="f12d1-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="f12d1-662">O site Quick R é um recurso útil em http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="f12d1-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="f12d1-663">R Inferno, de Patrick Burns, é um livro surpreendentemente bem-humorado que lida com inúmeros tópicos complicados e difíceis que podem ser encontrados ao programar em R. O livro está disponível gratuitamente em http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="f12d1-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="f12d1-664">Se você quiser se aprofundar em tópicos avançados em R, consulte o livro Advanced R, de Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="f12d1-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="f12d1-665">A versão online deste livro está disponível gratuitamente em http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="f12d1-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="f12d1-666">Um catálogo de pacotes de série temporal de R pode ser encontrado no CRAN Task View para análise de série temporal: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="f12d1-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="f12d1-667">Para obter informações sobre pacotes de objetos de série temporal específicos, consulte a documentação do pacote.</span><span class="sxs-lookup"><span data-stu-id="f12d1-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="f12d1-668">O livro Introductory Time Series with R, de Paul Cowpertwait e Andrew Metcalfe, fornece uma introdução ao uso de R para análise de série temporal.</span><span class="sxs-lookup"><span data-stu-id="f12d1-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="f12d1-669">Muitos textos mais teóricos fornecem exemplos de R.</span><span class="sxs-lookup"><span data-stu-id="f12d1-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="f12d1-670">Alguns ótimos recursos na Internet:</span><span class="sxs-lookup"><span data-stu-id="f12d1-670">Some great internet resources:</span></span>

* <span data-ttu-id="f12d1-671">DataCamp: DataCamp ensina R no conforto de seu navegador, com lições em vídeo e exercícios de codificação.</span><span class="sxs-lookup"><span data-stu-id="f12d1-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="f12d1-672">Há tutoriais interativos sobre as técnicas de R e os pacotes mais recentes.</span><span class="sxs-lookup"><span data-stu-id="f12d1-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="f12d1-673">Obtenha o tutorial de R interativo gratuitamente em https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="f12d1-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="f12d1-674">Um guia de Introdução ao R de Programiz https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="f12d1-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="f12d1-675">A quick R tutorial, por Kelly Black, da Clarkson University, http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="f12d1-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="f12d1-676">Mais de 60 recursos de R listados em http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="f12d1-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
