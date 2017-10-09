---
title: "aaaAuthor os módulos R personalizados no aprendizado de máquina do Azure | Microsoft Docs"
description: "Início rápido para a criação de módulos R personalizados no Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="c7378-103">Criar módulos R personalizados no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c7378-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="c7378-104">Este tópico descreve como tooauthor e implantar um módulo personalizado de R no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7378-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="c7378-105">Ele explica o que são módulos R personalizados e quais arquivos são usado toodefine-los.</span><span class="sxs-lookup"><span data-stu-id="c7378-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="c7378-106">Ele ilustra como tooconstruct Olá arquivos que definem um módulo e como tooregister Olá módulo para implantação em um espaço de trabalho do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c7378-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="c7378-107">Olá elementos e atributos usados na definição de saudação do módulo personalizado hello, em seguida, descritos mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="c7378-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="c7378-108">Como a funcionalidade auxiliar toouse arquivos e várias saídas também é abordado.</span><span class="sxs-lookup"><span data-stu-id="c7378-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="c7378-109">O que é um módulo R personalizado?</span><span class="sxs-lookup"><span data-stu-id="c7378-109">What is a custom R module?</span></span>
<span data-ttu-id="c7378-110">Um **módulo personalizado de** é um módulo definido pelo usuário que pode ser carregados tooyour espaço de trabalho e executado como parte de uma experiência de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7378-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="c7378-111">Um **módulo R personalizado** é um módulo personalizado que executa uma função R definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="c7378-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="c7378-112">**R** é uma linguagem de programação para a computação estatística e gráficos que é amplamente usada por cientistas estatísticos e para implementar algoritmos estatísticos.</span><span class="sxs-lookup"><span data-stu-id="c7378-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="c7378-113">No momento, R é o único idioma de saudação tem suportado em módulos personalizados, mas o suporte para idiomas adicionais está programada para versões futuras.</span><span class="sxs-lookup"><span data-stu-id="c7378-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="c7378-114">Módulos personalizados têm **status de primeira classe** no aprendizado de máquina do Azure no sentido de saudação que podem ser usados apenas como qualquer outro módulo.</span><span class="sxs-lookup"><span data-stu-id="c7378-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="c7378-115">Eles podem ser executados com outros módulos, incluídos em visualizações ou em experimentos publicados.</span><span class="sxs-lookup"><span data-stu-id="c7378-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="c7378-116">Tem controle sobre o algoritmo Olá implementado pelo módulo de saudação, Olá toobe portas de entrada e saída usado, Olá parâmetros de modelagem e outros vários comportamentos de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c7378-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="c7378-117">Uma experiência que contém módulos personalizados também pode ser publicada em Olá Cortana Intelligence Galeria para facilitar o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="c7378-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="c7378-118">Arquivos em um módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="c7378-118">Files in a custom R module</span></span>
<span data-ttu-id="c7378-119">Um módulo R personalizado é definido por um arquivo .zip que contém, no mínimo, dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="c7378-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="c7378-120">Um **arquivo de origem** que implementa a função hello R exposta pelo módulo Olá</span><span class="sxs-lookup"><span data-stu-id="c7378-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="c7378-121">Um **arquivo de definição XML** que descreve a interface de módulo personalizado de saudação</span><span class="sxs-lookup"><span data-stu-id="c7378-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="c7378-122">Arquivos auxiliares adicionais também podem ser incluídos no arquivo. zip Olá que fornece a funcionalidade que pode ser acessada pelo módulo personalizado de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="c7378-123">Essa opção é discutida em Olá **argumentos** parte da seção de referência Olá **elementos no arquivo de definição de XML Olá** Olá quickstart exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7378-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="c7378-124">Exemplo de início rápido: definir, empacotar e registrar um módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="c7378-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="c7378-125">Este exemplo ilustra como tooconstruct Olá arquivos necessários para um módulo personalizado de R, empacotá-las em um arquivo zip e, em seguida, registre Olá módulo no seu espaço de trabalho do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c7378-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="c7378-126">Olá arquivos de exemplo e o pacote zip exemplo podem ser baixados do [CustomAddRows.zip baixar arquivo](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="c7378-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="c7378-127">arquivo de origem Olá</span><span class="sxs-lookup"><span data-stu-id="c7378-127">hello source file</span></span>
<span data-ttu-id="c7378-128">Considere o exemplo hello de um **personalizado adicionar linhas** módulo que modifica a implementação padrão de saudação do hello **adicionar linhas** módulo usado tooconcatenate linhas (Observações) de dois conjuntos de dados (quadros de dados).</span><span class="sxs-lookup"><span data-stu-id="c7378-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="c7378-129">saudação padrão **adicionar linhas** módulo acrescenta linhas Olá Olá segundo conjunto de dados de entrada toohello de end da saudação primeira entrada conjunto de dados usando Olá `rbind` algoritmo.</span><span class="sxs-lookup"><span data-stu-id="c7378-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="c7378-130">Olá personalizado `CustomAddRows` função da mesma forma aceita dois conjuntos de dados, mas também aceita um parâmetro booliano de permuta como uma entrada adicional.</span><span class="sxs-lookup"><span data-stu-id="c7378-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="c7378-131">Se o parâmetro de permuta hello está definido muito**FALSE**, ele retorna Olá mesmo conjunto de dados como Olá implementação padrão.</span><span class="sxs-lookup"><span data-stu-id="c7378-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="c7378-132">Mas, se o parâmetro de troca de saudação é **TRUE**, função hello acrescenta linhas do primeiro conjunto de dados de entrada toohello-end do segundo conjunto de dados de saudação em vez disso.</span><span class="sxs-lookup"><span data-stu-id="c7378-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="c7378-133">arquivo de CustomAddRows.R Olá que contém a implementação de saudação do hello R `CustomAddRows` função exposta pelo Olá **personalizado adicionar linhas** módulo tem Olá código R a seguir.</span><span class="sxs-lookup"><span data-stu-id="c7378-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="c7378-134">arquivo de definição de XML Olá</span><span class="sxs-lookup"><span data-stu-id="c7378-134">hello XML definition file</span></span>
<span data-ttu-id="c7378-135">tooexpose isso `CustomAddRows` função como um módulo de aprendizado de máquina do Azure, um arquivo de definição XML deve ser criada toospecify como Olá **personalizado adicionar linhas** módulo deve aparência e o comportamento.</span><span class="sxs-lookup"><span data-stu-id="c7378-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="c7378-136">É toonote crítico que Olá valor Olá **id** atributos de saudação **entrada** e **Arg** elementos no arquivo XML de saudação devem corresponder a nomes de parâmetro de função hello da saudação R o código no arquivo de CustomAddRows.R Olá exatamente: (*dataset1*, *dataset2*, e *permuta* no exemplo hello).</span><span class="sxs-lookup"><span data-stu-id="c7378-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="c7378-137">Olá da mesma forma, o valor de saudação **entryPoint** atributo de saudação **idioma** elemento deve corresponder exatamente Olá nome da função hello no script hello R: (*CustomAddRows* exemplo hello).</span><span class="sxs-lookup"><span data-stu-id="c7378-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="c7378-138">Por outro lado, Olá **id** atributo Olá **saída** elemento não corresponde tooany variáveis no script hello R.</span><span class="sxs-lookup"><span data-stu-id="c7378-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="c7378-139">Quando mais de uma saída é necessária, basta retornar uma lista de função hello R com resultados colocados *em Olá mesma ordem* como **saídas** elementos são declarados no arquivo XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="c7378-140">Pacote e registrar o módulo de saudação</span><span class="sxs-lookup"><span data-stu-id="c7378-140">Package and register hello module</span></span>
<span data-ttu-id="c7378-141">Salvar esses dois arquivos como *CustomAddRows.R* e *CustomAddRows.xml* e, em seguida, zip Olá dois arquivos juntos em uma *CustomAddRows.zip* arquivo.</span><span class="sxs-lookup"><span data-stu-id="c7378-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="c7378-142">tooregistê-los em seu espaço de trabalho do aprendizado de máquina, espaço de trabalho tooyour vá Olá estúdio de aprendizado de máquina, clique em Olá **+ novo** botão na parte inferior do hello e escolha **módulo -> do pacote ZIP** tooupload Olá novo **personalizado adicionar linhas** módulo.</span><span class="sxs-lookup"><span data-stu-id="c7378-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Carregar Zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="c7378-144">Olá **personalizado adicionar linhas** módulo agora está pronto toobe acessado por suas experiências de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c7378-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="c7378-145">Elementos no arquivo de definição de XML Olá</span><span class="sxs-lookup"><span data-stu-id="c7378-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="c7378-146">Elementos de módulo</span><span class="sxs-lookup"><span data-stu-id="c7378-146">Module elements</span></span>
<span data-ttu-id="c7378-147">Olá **módulo** elemento é usado toodefine um módulo personalizado no arquivo XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="c7378-148">Vários módulos podem ser definidos em um arquivo XML usando vários elementos de **módulo** .</span><span class="sxs-lookup"><span data-stu-id="c7378-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="c7378-149">Cada módulo no espaço de trabalho deve ter um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c7378-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="c7378-150">Registrar um módulo personalizado com hello mesmo nome como um módulo personalizado existente e substitui módulo existente Olá com hello uma nova.</span><span class="sxs-lookup"><span data-stu-id="c7378-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="c7378-151">Módulos personalizados no entanto, podem ser registrado com o mesmo nome como um módulo de aprendizado de máquina do Azure existente de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="c7378-152">Se assim, eles aparecem no hello **personalizado** categoria da paleta de módulo hello.</span><span class="sxs-lookup"><span data-stu-id="c7378-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="c7378-153">Dentro de saudação **módulo** elemento, você pode especificar dois elementos opcionais adicionais:</span><span class="sxs-lookup"><span data-stu-id="c7378-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="c7378-154">um **proprietário** elemento que é incorporado em módulo Olá</span><span class="sxs-lookup"><span data-stu-id="c7378-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="c7378-155">um **descrição** elemento que contém o texto que é exibido na ajuda rápida para o módulo de saudação e quando você focaliza o módulo Olá Olá aprendizado de máquina da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7378-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="c7378-156">Regras para limites de caracteres em elementos de módulo hello:</span><span class="sxs-lookup"><span data-stu-id="c7378-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="c7378-157">Olá valor Olá **nome** atributo Olá **módulo** elemento não deve exceder 64 caracteres de comprimento.</span><span class="sxs-lookup"><span data-stu-id="c7378-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="c7378-158">Olá conteúdo de saudação **descrição** elemento não deve exceder 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="c7378-159">Olá conteúdo de saudação **proprietário** elemento não deve exceder 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="c7378-160">Resultados de um módulo podem ser determinísticos ou nondeterministic.* * por padrão, todos os módulos são considerados toobe determinística.</span><span class="sxs-lookup"><span data-stu-id="c7378-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="c7378-161">Ou seja, dado um conjunto imutável de parâmetros de entrada e de dados, módulo Olá deve retornar Olá mesmos resultados eacRAND ou uma hora de functionh que é executado.</span><span class="sxs-lookup"><span data-stu-id="c7378-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="c7378-162">Devido a esse comportamento, o estúdio de aprendizado de máquina do Azure repete somente módulos marcados como determinística se um parâmetro ou dados de entrada hello foi alterado.</span><span class="sxs-lookup"><span data-stu-id="c7378-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="c7378-163">Retornando resultados de saudação em cache também fornece muito execução mais rápida de experimentos.</span><span class="sxs-lookup"><span data-stu-id="c7378-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="c7378-164">Há funções não determinísticas como RAND ou uma função que retorna Olá data ou hora atual.</span><span class="sxs-lookup"><span data-stu-id="c7378-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="c7378-165">Se seu módulo usa uma função não determinística, você pode especificar que o módulo Olá é não determinística pela configuração Olá opcional **isDeterministic** atributo muito**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="c7378-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="c7378-166">Isso assegura que o módulo Olá é executado sempre que a experiência de saudação é executada, mesmo que hello módulo parâmetros de entrada e não foram alterados.</span><span class="sxs-lookup"><span data-stu-id="c7378-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="c7378-167">Definição de linguagem</span><span class="sxs-lookup"><span data-stu-id="c7378-167">Language Definition</span></span>
<span data-ttu-id="c7378-168">Olá **idioma** elemento em seu arquivo de definição XML é o idioma de módulo personalizado de saudação do toospecify usado.</span><span class="sxs-lookup"><span data-stu-id="c7378-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="c7378-169">Atualmente, R é Olá só tem suporte a idioma.</span><span class="sxs-lookup"><span data-stu-id="c7378-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="c7378-170">Olá valor Olá **sourceFile** atributo deve ser o nome de saudação do arquivo de saudação R que contém Olá função toocall quando Olá módulo será executado.</span><span class="sxs-lookup"><span data-stu-id="c7378-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="c7378-171">Esse arquivo deve ser parte do pacote de zip hello.</span><span class="sxs-lookup"><span data-stu-id="c7378-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="c7378-172">Olá valor Olá **entryPoint** atributo é Olá nome da função hello está sendo chamada e deve corresponder a uma função válida definida com no arquivo de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="c7378-173">Portas</span><span class="sxs-lookup"><span data-stu-id="c7378-173">Ports</span></span>
<span data-ttu-id="c7378-174">Olá portas de entrada e saídas para um módulo personalizado são especificadas em elementos filho do hello **portas** seção do arquivo de definição XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="c7378-175">ordem de saudação desses elementos determina Olá layout experiente (UX) por usuários.</span><span class="sxs-lookup"><span data-stu-id="c7378-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="c7378-176">primeiro filho de saudação **entrada** ou **saída** listados no hello **portas** elemento do arquivo XML de saudação torna-se a porta de entrada hello mais à esquerda no hello UX de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="c7378-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="c7378-177">Cada entrada e a porta de saída pode ter um opcional **descrição** elemento filho que especifica o texto de saudação mostrado quando você focaliza cursor do mouse Olá porta Olá Olá aprendizado de máquina da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7378-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="c7378-178">**Regras de portas**:</span><span class="sxs-lookup"><span data-stu-id="c7378-178">**Ports Rules**:</span></span>

* <span data-ttu-id="c7378-179">O número máximo de **portas de entrada e saída** é de 8 para cada.</span><span class="sxs-lookup"><span data-stu-id="c7378-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="c7378-180">Elementos de entrada</span><span class="sxs-lookup"><span data-stu-id="c7378-180">Input elements</span></span>
<span data-ttu-id="c7378-181">Portas de entrada permitem que você espaço de trabalho e a função de tooyour R toopass dados.</span><span class="sxs-lookup"><span data-stu-id="c7378-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="c7378-182">Olá **tipos de dados** que têm suporte para portas de entrada são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c7378-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="c7378-183">**DataTable:** esse tipo é passado a função tooyour R como um data.frame.</span><span class="sxs-lookup"><span data-stu-id="c7378-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="c7378-184">Na verdade, qualquer tipo (por exemplo, arquivos CSV ou arquivos ARFF) que é suportado pelo aprendizado de máquina e que é compatível com **DataTable** são data.frame tooa convertido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c7378-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="c7378-185">Olá **id** atributo associado a cada **DataTable** porta de entrada deve ter um valor exclusivo e esse valor deve corresponder com o parâmetro na função de R nomeado correspondente.</span><span class="sxs-lookup"><span data-stu-id="c7378-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="c7378-186">Opcional **DataTable** portas que não são transmitidas como entrada em um experimento ter valor Olá **nulo** função toohello passado R e portas de zip opcional serão ignoradas se Olá entrada não está conectada.</span><span class="sxs-lookup"><span data-stu-id="c7378-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="c7378-187">Olá **é opcional** atributo é opcional para ambos os Olá **DataTable** e **Zip** tipos e é *false* por padrão.</span><span class="sxs-lookup"><span data-stu-id="c7378-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="c7378-188">**ZIP:** módulos personalizados podem aceitar um arquivo zip como entrada.</span><span class="sxs-lookup"><span data-stu-id="c7378-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="c7378-189">Essa entrada é desempacotada no diretório de trabalho Olá R de sua função</span><span class="sxs-lookup"><span data-stu-id="c7378-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="c7378-190">Para módulos R personalizados, id de saudação para uma porta de Zip não tem toomatch quaisquer parâmetros de função hello R.</span><span class="sxs-lookup"><span data-stu-id="c7378-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="c7378-191">Isso ocorre porque o arquivo zip de saudação é extraído automaticamente toohello R diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c7378-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="c7378-192">**Regras de entrada:**</span><span class="sxs-lookup"><span data-stu-id="c7378-192">**Input Rules:**</span></span>

* <span data-ttu-id="c7378-193">Olá valor Olá **id** atributo de saudação **entrada** elemento deve ser um nome de variável de R válido.</span><span class="sxs-lookup"><span data-stu-id="c7378-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="c7378-194">Olá valor Olá **id** atributo de saudação **entrada** elemento não deve ser maior que 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c7378-195">Olá valor Olá **nome** atributo de saudação **entrada** elemento não deve ser maior que 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c7378-196">Olá conteúdo de saudação **descrição** elemento não deve ter mais de 128 caracteres</span><span class="sxs-lookup"><span data-stu-id="c7378-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="c7378-197">Olá valor Olá **tipo** atributo de saudação **entrada** elemento deve ser *Zip* ou *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c7378-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="c7378-198">Olá valor Olá **é opcional** atributo de saudação **entrada** elemento não é necessário (e é *false* por padrão quando não especificado); mas se for especificado, ele deve ser *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="c7378-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="c7378-199">Elementos de saída</span><span class="sxs-lookup"><span data-stu-id="c7378-199">Output elements</span></span>
<span data-ttu-id="c7378-200">**Portas de saída padrão:** portas de saída são mapeadas toohello valores de retorno de sua função de R, que pode ser usado por módulos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="c7378-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="c7378-201">*DataTable* é o tipo de porta de saída padrão somente Olá com suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="c7378-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="c7378-202">(O suporte para *Aprendizes* e *Transformações* estará disponível em breve.) Uma saída *DataTable* é definida como:</span><span class="sxs-lookup"><span data-stu-id="c7378-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="c7378-203">Para saídas em módulos R personalizados, Olá valor Olá **id** atributo não tem toocorrespond com qualquer coisa no script hello R, mas ele deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c7378-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="c7378-204">Para uma saída de módulo único, o valor de retorno de saudação do função hello R deve ser um *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="c7378-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="c7378-205">Em ordem toooutput mais de um objeto de um tipo de dados com suporte, portas de saída apropriada Olá necessário toobe especificado no arquivo de definição XML de saudação e objetos Olá necessário toobe retornado como uma lista.</span><span class="sxs-lookup"><span data-stu-id="c7378-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="c7378-206">Olá saída objetos são atribuídos a portas toooutput em tooright esquerda, refletindo ordem Olá no qual os objetos de saudação são colocados no Olá retornada lista.</span><span class="sxs-lookup"><span data-stu-id="c7378-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="c7378-207">Por exemplo, se você quiser toomodify Olá **personalizado adicionar linhas** toooutput módulo Olá originais dois conjuntos de dados, *dataset1* e *dataset2*, além disso toohello novo unida conjunto de dados, *conjunto de dados*, (em ordem, da esquerda tooright, como: *dataset*, *dataset1*, *dataset2*), em seguida, defina Olá portas no arquivo de CustomAddRows.xml Olá de saída da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c7378-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="c7378-208">E retornar a lista de saudação de objetos em uma lista na ordem correta, Olá em 'CustomAddRows.R':</span><span class="sxs-lookup"><span data-stu-id="c7378-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="c7378-209">**Saída de visualização:** você também pode especificar uma porta de saída do tipo *visualização*, que exibe a saída de saudação da saída de console e dispositivo gráfico Olá R.</span><span class="sxs-lookup"><span data-stu-id="c7378-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="c7378-210">Esta porta não é parte da saída da função de saudação R e não interfere em ordem de saudação do hello outros tipos de porta de saída.</span><span class="sxs-lookup"><span data-stu-id="c7378-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="c7378-211">tooadd uma visualização porta toohello módulos personalizados, adicione um **saída** elemento com um valor de *visualização* para seus **tipo** atributo:</span><span class="sxs-lookup"><span data-stu-id="c7378-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="c7378-212">**Regras de saída:**</span><span class="sxs-lookup"><span data-stu-id="c7378-212">**Output Rules:**</span></span>

* <span data-ttu-id="c7378-213">Olá valor Olá **id** atributo de saudação **saída** elemento deve ser um nome de variável de R válido.</span><span class="sxs-lookup"><span data-stu-id="c7378-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="c7378-214">Olá valor Olá **id** atributo de saudação **saída** elemento não deve ter mais de 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="c7378-215">Olá valor Olá **nome** atributo de saudação **saída** elemento não deve ser maior que 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c7378-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="c7378-216">Olá valor Olá **tipo** atributo de saudação **saída** elemento deve ser *visualização*.</span><span class="sxs-lookup"><span data-stu-id="c7378-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="c7378-217">Argumentos</span><span class="sxs-lookup"><span data-stu-id="c7378-217">Arguments</span></span>
<span data-ttu-id="c7378-218">Dados adicionais podem ser passados toohello R função por meio de parâmetros do módulo que são definidos no hello **argumentos** elemento.</span><span class="sxs-lookup"><span data-stu-id="c7378-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="c7378-219">Esses parâmetros aparecem no painel de propriedades mais à direita de saudação de saudação da interface do usuário de aprendizado de máquina quando o módulo de saudação é selecionado.</span><span class="sxs-lookup"><span data-stu-id="c7378-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="c7378-220">Os argumentos podem ser qualquer um dos tipos de saudação com suporte ou você pode criar uma enumeração personalizada quando necessário.</span><span class="sxs-lookup"><span data-stu-id="c7378-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="c7378-221">Semelhante toohello **portas** elementos, **argumentos** elementos podem ter um recurso opcional **descrição** elemento que especifica o texto de saudação que aparece quando você passa o mouse Olá em nome do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="c7378-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="c7378-222">Propriedades opcionais para um módulo, como o valor padrão, minValue e maxValue podem ser adicionadas como argumento tooany como atributos tooa **propriedades** elemento.</span><span class="sxs-lookup"><span data-stu-id="c7378-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="c7378-223">Propriedades válidas para Olá **propriedades** elemento dependem do tipo de argumento hello e são descritos com tipos de argumento Olá tem suporte na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="c7378-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="c7378-224">Argumentos com hello **é opcional** propriedade definida muito**"true"** não exigem Olá usuário tooenter um valor.</span><span class="sxs-lookup"><span data-stu-id="c7378-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="c7378-225">Se um valor não for fornecido para o argumento toohello, argumento Olá não for passado a função de ponto de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="c7378-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="c7378-226">Argumentos da função de ponto de entrada hello necessidade opcional toobe explicitamente manipulado pela função hello, por exemplo, atribuído um valor padrão de NULL na definição de função de ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="c7378-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="c7378-227">Um argumento opcional só serão impostas Olá outras restrições de argumento, ou seja, min ou max, se um valor é fornecido pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="c7378-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="c7378-228">Como com as entradas e saídas, é fundamental que cada um dos parâmetros de saudação tenha valores de id exclusivo associados a eles.</span><span class="sxs-lookup"><span data-stu-id="c7378-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="c7378-229">No início rápido do nosso exemplo hello associados/parâmetro de id foi *permuta*.</span><span class="sxs-lookup"><span data-stu-id="c7378-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="c7378-230">Elemento arg</span><span class="sxs-lookup"><span data-stu-id="c7378-230">Arg element</span></span>
<span data-ttu-id="c7378-231">Um parâmetro de módulo é definido usando Olá **Arg** elemento filho do hello **argumentos** seção do arquivo de definição XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="c7378-232">Assim como acontece com os elementos filho de saudação em Olá **portas** seção, Olá a ordem dos parâmetros no hello **argumentos** seção define o layout de saudação em Olá UX.</span><span class="sxs-lookup"><span data-stu-id="c7378-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="c7378-233">Olá parâmetros aparecem de cima para baixo na saudação da interface do usuário em Olá mesma ordem em que elas são definidas no arquivo XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="c7378-234">suporte para o aprendizado de máquina para parâmetros de tipos de saudação são listados aqui.</span><span class="sxs-lookup"><span data-stu-id="c7378-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="c7378-235">**int** – um parâmetro de tipo de número inteiro (32 bits).</span><span class="sxs-lookup"><span data-stu-id="c7378-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="c7378-236">*Propriedades opcionais*: **mín.**, **máx.**, **padrão** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c7378-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="c7378-237">**double** – um parâmetro de tipo duplo.</span><span class="sxs-lookup"><span data-stu-id="c7378-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="c7378-238">*Propriedades opcionais*: **mín.**, **máx.**, **padrão** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c7378-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="c7378-239">**bool** – um parâmetro booliano que é representado por uma caixa de seleção no UX.</span><span class="sxs-lookup"><span data-stu-id="c7378-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="c7378-240">*Propriedades opcionais*: **padrão** -falso se não definido</span><span class="sxs-lookup"><span data-stu-id="c7378-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="c7378-241">**string**: uma cadeia de caracteres padrão</span><span class="sxs-lookup"><span data-stu-id="c7378-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="c7378-242">*Propriedades opcionais*: **padrão** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="c7378-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="c7378-243">**ColumnPickerFor**: um parâmetro de seleção de coluna.</span><span class="sxs-lookup"><span data-stu-id="c7378-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="c7378-244">Esse tipo é renderizado no hello UX como um seletor de coluna.</span><span class="sxs-lookup"><span data-stu-id="c7378-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="c7378-245">Olá **propriedade** elemento é usado toospecify aqui Olá id da porta de saudação do que colunas forem selecionadas, onde o tipo de porta de destino Olá deve ser *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c7378-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="c7378-246">resultado de saudação da seleção de coluna Olá é passado toohello R função como uma lista de cadeias de caracteres que contém os nomes de coluna Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="c7378-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="c7378-247">*Propriedades necessárias*: **portId** -correspondências Olá id de um elemento de entrada com tipo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="c7378-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="c7378-248">*Propriedades opcionais*:</span><span class="sxs-lookup"><span data-stu-id="c7378-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="c7378-249">**allowedTypes** -tipos de coluna de saudação de filtros do qual você pode escolher.</span><span class="sxs-lookup"><span data-stu-id="c7378-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="c7378-250">Os valores válidos incluem:</span><span class="sxs-lookup"><span data-stu-id="c7378-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="c7378-251">Numérico</span><span class="sxs-lookup"><span data-stu-id="c7378-251">Numeric</span></span>
    * <span data-ttu-id="c7378-252">Booliano</span><span class="sxs-lookup"><span data-stu-id="c7378-252">Boolean</span></span>
    * <span data-ttu-id="c7378-253">Categóricos</span><span class="sxs-lookup"><span data-stu-id="c7378-253">Categorical</span></span>
    * <span data-ttu-id="c7378-254">string</span><span class="sxs-lookup"><span data-stu-id="c7378-254">String</span></span>
    * <span data-ttu-id="c7378-255">Rótulo</span><span class="sxs-lookup"><span data-stu-id="c7378-255">Label</span></span>
    * <span data-ttu-id="c7378-256">Recurso</span><span class="sxs-lookup"><span data-stu-id="c7378-256">Feature</span></span>
    * <span data-ttu-id="c7378-257">Pontuação</span><span class="sxs-lookup"><span data-stu-id="c7378-257">Score</span></span>
    * <span data-ttu-id="c7378-258">Todos</span><span class="sxs-lookup"><span data-stu-id="c7378-258">All</span></span>
  * <span data-ttu-id="c7378-259">**padrão** -seleções padrão válido para o seletor de coluna Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="c7378-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="c7378-260">Nenhum</span><span class="sxs-lookup"><span data-stu-id="c7378-260">None</span></span>
    * <span data-ttu-id="c7378-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="c7378-261">NumericFeature</span></span>
    * <span data-ttu-id="c7378-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="c7378-262">NumericLabel</span></span>
    * <span data-ttu-id="c7378-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="c7378-263">NumericScore</span></span>
    * <span data-ttu-id="c7378-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="c7378-264">NumericAll</span></span>
    * <span data-ttu-id="c7378-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="c7378-265">BooleanFeature</span></span>
    * <span data-ttu-id="c7378-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="c7378-266">BooleanLabel</span></span>
    * <span data-ttu-id="c7378-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="c7378-267">BooleanScore</span></span>
    * <span data-ttu-id="c7378-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="c7378-268">BooleanAll</span></span>
    * <span data-ttu-id="c7378-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="c7378-269">CategoricalFeature</span></span>
    * <span data-ttu-id="c7378-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="c7378-270">CategoricalLabel</span></span>
    * <span data-ttu-id="c7378-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="c7378-271">CategoricalScore</span></span>
    * <span data-ttu-id="c7378-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="c7378-272">CategoricalAll</span></span>
    * <span data-ttu-id="c7378-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="c7378-273">StringFeature</span></span>
    * <span data-ttu-id="c7378-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="c7378-274">StringLabel</span></span>
    * <span data-ttu-id="c7378-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="c7378-275">StringScore</span></span>
    * <span data-ttu-id="c7378-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="c7378-276">StringAll</span></span>
    * <span data-ttu-id="c7378-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="c7378-277">AllLabel</span></span>
    * <span data-ttu-id="c7378-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="c7378-278">AllFeature</span></span>
    * <span data-ttu-id="c7378-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="c7378-279">AllScore</span></span>
    * <span data-ttu-id="c7378-280">Todos</span><span class="sxs-lookup"><span data-stu-id="c7378-280">All</span></span>

<span data-ttu-id="c7378-281">**Suspensa**: uma lista (suspensa) enumerada especifica pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="c7378-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="c7378-282">itens de lista suspensa de saudação são especificadas no hello **propriedades** elemento usando um **Item** elemento.</span><span class="sxs-lookup"><span data-stu-id="c7378-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="c7378-283">Olá **id** para cada **Item** deve ser exclusivo e uma variável de R válida.</span><span class="sxs-lookup"><span data-stu-id="c7378-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="c7378-284">Olá valor Olá **nome** de um **Item** serve como o texto de saudação que você vê e o valor de saudação que é passado a função toohello R.</span><span class="sxs-lookup"><span data-stu-id="c7378-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="c7378-285">*Propriedades opcionais*:</span><span class="sxs-lookup"><span data-stu-id="c7378-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="c7378-286">**padrão** - Olá valor de propriedade padrão de saudação deve corresponder com um valor de id de uma saudação **Item** elementos.</span><span class="sxs-lookup"><span data-stu-id="c7378-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="c7378-287">Arquivos auxiliares</span><span class="sxs-lookup"><span data-stu-id="c7378-287">Auxiliary Files</span></span>
<span data-ttu-id="c7378-288">Qualquer arquivo que é colocado no arquivo ZIP módulo personalizado é contínuo toobe disponível para uso durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c7378-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="c7378-289">Qualquer estrutura de diretório presente é preservada.</span><span class="sxs-lookup"><span data-stu-id="c7378-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="c7378-290">Isso significa que funciona de fornecimento de arquivo hello mesmo localmente e na execução de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7378-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="c7378-291">Observe que todos os arquivos são extraídos too'src' directory para que todos os caminhos devem ter ' src /' prefixo.</span><span class="sxs-lookup"><span data-stu-id="c7378-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="c7378-292">Por exemplo, digamos que você deseja tooremove nas todas as linhas do conjunto de dados hello e também remove linhas duplicadas, antes de gerá-lo em CustomAddRows, e você já escreveu uma função do R que faz isso em um arquivo RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="c7378-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="c7378-293">Pode extrair o arquivo auxiliar Olá RemoveDupNARows.R em Olá CustomAddRows função:</span><span class="sxs-lookup"><span data-stu-id="c7378-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="c7378-294">Em seguida, carregue um arquivo zip contendo “CustomAddRows.R”, “CustomAddRows.xml” e “RemoveDupNARows.R” como um módulo R personalizado.</span><span class="sxs-lookup"><span data-stu-id="c7378-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="c7378-295">Ambiente de execução</span><span class="sxs-lookup"><span data-stu-id="c7378-295">Execution Environment</span></span>
<span data-ttu-id="c7378-296">ambiente de execução Olá para script hello R usa Olá a mesma versão do R Olá **Executar Script R** módulo e pode usar Olá mesmo padrão de pacotes.</span><span class="sxs-lookup"><span data-stu-id="c7378-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="c7378-297">Você também pode adicionar adicionais R pacotes tooyour módulo personalizado, incluindo-os no pacote de zip do módulo personalizado de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7378-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="c7378-298">Basta carregá-los no seu script R como faria em seu próprio ambiente R.</span><span class="sxs-lookup"><span data-stu-id="c7378-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="c7378-299">**Limitações do ambiente de execução Olá** incluem:</span><span class="sxs-lookup"><span data-stu-id="c7378-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="c7378-300">Sistema de arquivos não persistente: arquivos gravados quando o módulo personalizado de saudação é executado não são persistidos em várias execuções do hello mesmo módulo.</span><span class="sxs-lookup"><span data-stu-id="c7378-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="c7378-301">Sem acesso à rede</span><span class="sxs-lookup"><span data-stu-id="c7378-301">No network access</span></span>

