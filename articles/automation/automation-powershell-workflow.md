---
title: "aaaLearning fluxo de trabalho do PowerShell para automação do Azure | Microsoft Docs"
description: "Este artigo destina-se como uma lição rápida de autores familiarizados com PowerShell toounderstand Olá diferenças entre o PowerShell e o fluxo de trabalho do PowerShell e conceitos tooAutomation aplicável runbooks."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="2821f-103">Aprender sobre os principais conceitos de Fluxo de Trabalho do Windows PowerShell para runbooks de Automação</span><span class="sxs-lookup"><span data-stu-id="2821f-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="2821f-104">Os runbooks na Automação do Azure são implementados como Fluxos de Trabalho do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2821f-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="2821f-105">Um fluxo de trabalho do Windows PowerShell é o script do Windows PowerShell tooa semelhante, mas tem algumas diferenças importantes que podem ser confusas tooa novo usuário.</span><span class="sxs-lookup"><span data-stu-id="2821f-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="2821f-106">Enquanto este artigo é pretendido toohelp escrever runbooks usando o fluxo de trabalho do PowerShell, é recomendável que você escreve runbooks usando o PowerShell, a menos que você precisa de pontos de verificação.</span><span class="sxs-lookup"><span data-stu-id="2821f-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="2821f-107">Há várias diferenças de sintaxe, quando se cria runbooks do fluxo de trabalho do PowerShell e essas diferenças requerem um pouco mais trabalho toowrite efetivo fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="2821f-108">Um fluxo de trabalho é uma sequência de etapas programadas e conectadas que executam tarefas de execução longa ou exigem a coordenação de saudação de várias etapas em vários dispositivos ou nós gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2821f-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="2821f-109">Olá, benefícios de um fluxo de trabalho em um script normal incluem a capacidade de saudação toosimultaneously executar uma ação em vários dispositivos e Olá capacidade tooautomatically recuperar de falhas.</span><span class="sxs-lookup"><span data-stu-id="2821f-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="2821f-110">Um Fluxo de Trabalho do Windows PowerShell é um script do Windows PowerShell que usa o Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="2821f-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="2821f-111">Enquanto o fluxo de trabalho de saudação é escrito com sintaxe do Windows PowerShell e lançado pelo Windows PowerShell, ela é processada pelo Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="2821f-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="2821f-112">Para obter detalhes completos sobre tópicos Olá neste artigo, consulte [guia de Introdução ao fluxo de trabalho do Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="2821f-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="2821f-113">Estrutura básica de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="2821f-113">Basic structure of a workflow</span></span>
<span data-ttu-id="2821f-114">Olá primeira etapa tooconverting um fluxo de trabalho do PowerShell script tooa PowerShell é envolve com hello **fluxo de trabalho** palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="2821f-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="2821f-115">Inicia um fluxo de trabalho com hello **fluxo de trabalho** palavra-chave seguida pelo corpo de saudação do script hello entre chaves.</span><span class="sxs-lookup"><span data-stu-id="2821f-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="2821f-116">nome de saudação do fluxo de trabalho Olá segue Olá **fluxo de trabalho** conforme Olá segue a sintaxe da palavra-chave:</span><span class="sxs-lookup"><span data-stu-id="2821f-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="2821f-117">nome de saudação do fluxo de trabalho de saudação deve corresponder o nome de Olá de runbook da automação hello.</span><span class="sxs-lookup"><span data-stu-id="2821f-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="2821f-118">Se Olá runbook está sendo importado, nome de arquivo hello deve corresponder ao nome do fluxo de trabalho hello e deve terminar em *. ps1*.</span><span class="sxs-lookup"><span data-stu-id="2821f-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="2821f-119">tooadd parâmetros toohello fluxo de trabalho, use Olá **Param** exatamente como você faria tooa script de palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="2821f-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="2821f-120">Alterações de código</span><span class="sxs-lookup"><span data-stu-id="2821f-120">Code changes</span></span>
<span data-ttu-id="2821f-121">Código de fluxo de trabalho do PowerShell analisa o código de script tooPowerShell quase idênticos, exceto algumas alterações significativas.</span><span class="sxs-lookup"><span data-stu-id="2821f-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="2821f-122">Olá seções a seguir descreve as alterações que você precisa toomake tooa de script do PowerShell para ele toorun em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="2821f-123">Atividades</span><span class="sxs-lookup"><span data-stu-id="2821f-123">Activities</span></span>
<span data-ttu-id="2821f-124">Uma atividade é uma tarefa específica em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="2821f-125">Assim como um script é composto de um ou mais comandos, um fluxo de trabalho é composto de uma ou mais atividades que são executadas em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="2821f-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="2821f-126">O fluxo de trabalho do Windows PowerShell converte automaticamente muitos dos Olá tooactivities de cmdlets do Windows PowerShell quando ele é executado em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="2821f-127">Quando você especificar um desses cmdlets em seu runbook, atividade correspondente Olá é executada pelo Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="2821f-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="2821f-128">Para os cmdlets sem uma atividade correspondente, o fluxo de trabalho do Windows PowerShell executa automaticamente cmdlet hello dentro um [InlineScript](#inlinescript) atividade.</span><span class="sxs-lookup"><span data-stu-id="2821f-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="2821f-129">Há um conjunto de cmdlets que são excluídos e não podem ser usados em um fluxo de trabalho, a menos que você o inclua explicitamente em um bloco de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="2821f-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="2821f-130">Para obter mais detalhes sobre esses conceitos, confira [Usando atividades em fluxos de trabalho de script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="2821f-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="2821f-131">Atividades de fluxo de trabalho compartilham um conjunto de tooconfigure de parâmetros comuns de sua operação.</span><span class="sxs-lookup"><span data-stu-id="2821f-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="2821f-132">Para obter detalhes sobre os parâmetros comuns de fluxo de trabalho hello, consulte [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="2821f-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="2821f-133">Parâmetros posicionais</span><span class="sxs-lookup"><span data-stu-id="2821f-133">Positional parameters</span></span>
<span data-ttu-id="2821f-134">Você não pode usar parâmetros posicionais com atividades e cmdlets em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="2821f-135">Tudo o que isso significa é que você deve usar nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2821f-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="2821f-136">Por exemplo, considere Olá código que obtém todos os serviços em execução a seguir.</span><span class="sxs-lookup"><span data-stu-id="2821f-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="2821f-137">Se você tentar toorun esse mesmo código em um fluxo de trabalho, você receberá uma mensagem como "Conjunto não pode ser resolvido Olá especificado do parâmetro nomeado parâmetros."</span><span class="sxs-lookup"><span data-stu-id="2821f-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="2821f-138">toocorrect, fornecer o nome do parâmetro hello seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="2821f-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="2821f-139">Objetos desserializados</span><span class="sxs-lookup"><span data-stu-id="2821f-139">Deserialized objects</span></span>
<span data-ttu-id="2821f-140">Os objetos em fluxos de trabalho são desserializados.</span><span class="sxs-lookup"><span data-stu-id="2821f-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="2821f-141">Isso significa que suas propriedades ainda estão disponíveis, mas não seus métodos.</span><span class="sxs-lookup"><span data-stu-id="2821f-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="2821f-142">Por exemplo, considere Olá código do PowerShell que interrompe um serviço usando o método de parada Olá Olá do objeto de serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="2821f-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="2821f-143">Se você tentar toorun isso em um fluxo de trabalho, você receberá um erro informando que "invocação de método não é suportada em um fluxo de trabalho do Windows PowerShell."</span><span class="sxs-lookup"><span data-stu-id="2821f-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="2821f-144">Uma opção é toowrap estas duas linhas de código em um [InlineScript](#inlinescript) bloquear em caso $Service seria um objeto de serviço no bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="2821f-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="2821f-145">Outra opção é toouse outro cmdlet que executa Olá a mesma funcionalidade que o método hello, se houver um disponível.</span><span class="sxs-lookup"><span data-stu-id="2821f-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="2821f-146">Em nosso exemplo, o cmdlet Stop-Service de saudação fornece Olá mesma funcionalidade que o método de parada Olá e você pode usar o seguinte Olá para um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="2821f-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="2821f-147">InlineScript</span></span>
<span data-ttu-id="2821f-148">Olá **InlineScript** atividade é útil quando você precisa toorun um ou mais comandos como tradicional script do PowerShell em vez de fluxo de trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2821f-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="2821f-149">Enquanto os comandos em um fluxo de trabalho são enviados tooWindows Workflow Foundation para processamento, os comandos em um bloco InlineScript são processados pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2821f-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="2821f-150">O InlineScript utiliza Olá seguindo a sintaxe mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="2821f-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="2821f-151">Você pode retornar a saída de um InlineScript atribuindo Olá saída tooa variável.</span><span class="sxs-lookup"><span data-stu-id="2821f-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="2821f-152">Olá exemplo a seguir interrompe um serviço e, em seguida, gera o nome do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="2821f-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="2821f-153">Você pode passar valores para um bloco InlineScript, mas deve usar o modificador de escopo **$Using** .</span><span class="sxs-lookup"><span data-stu-id="2821f-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="2821f-154">Olá exemplo a seguir é exemplo anterior toohello idênticos exceto hello nome do serviço é fornecido por uma variável.</span><span class="sxs-lookup"><span data-stu-id="2821f-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="2821f-155">Atividades InlineScript podem ser essenciais para alguns fluxos de trabalho, eles não oferecem suporte a construções de fluxo de trabalho e devem ser usados somente quando necessário para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2821f-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="2821f-156">Não é possível usar [pontos de verificação](#checkpoints) dentro de um bloco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="2821f-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="2821f-157">Se ocorrer uma falha em bloco Olá, ele deverá ser retomado do início de saudação do bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="2821f-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="2821f-158">Não é possível usar a [execução paralela](#parallel-processing) dentro de um InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="2821f-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="2821f-159">InlineScript afeta a escalabilidade de fluxo de trabalho hello, uma vez que retém a sessão do Windows PowerShell Olá para todo o comprimento do bloco de InlineScript Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="2821f-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="2821f-160">Para obter mais informações sobre como usar o InlineScript, consulte [Executando comandos do Windows PowerShell em um fluxo de trabalho](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="2821f-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="2821f-161">Processamento paralelo</span><span class="sxs-lookup"><span data-stu-id="2821f-161">Parallel processing</span></span>
<span data-ttu-id="2821f-162">Uma vantagem dos fluxos de trabalho do Windows PowerShell é Olá capacidade tooperform um conjunto de comandos em paralelo, em vez de sequencialmente como com um script típico.</span><span class="sxs-lookup"><span data-stu-id="2821f-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="2821f-163">Você pode usar o hello **paralela** palavra-chave toocreate um bloco de script com vários comandos que são executados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2821f-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="2821f-164">Isso usa Olá seguindo a sintaxe mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="2821f-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="2821f-165">Nesse caso, a atividade1 e da atividade2 inicia em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2821f-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="2821f-166">A Activity3 começará somente após a conclusão da Activity1 e da Activity2.</span><span class="sxs-lookup"><span data-stu-id="2821f-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="2821f-167">Por exemplo, considere Olá seguintes comandos do PowerShell que vários arquivos tooa rede destino da cópia.</span><span class="sxs-lookup"><span data-stu-id="2821f-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="2821f-168">Esses comandos são executados sequencialmente para que um arquivo deve concluir a cópia antes de saudação é iniciada.</span><span class="sxs-lookup"><span data-stu-id="2821f-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="2821f-169">Olá seguinte fluxo de trabalho executa esses mesmos comandos em paralelo, para que todos eles iniciarem a cópia no hello mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="2821f-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="2821f-170">Somente depois que todas elas sejam copiados é Olá conclusão mensagem exibida.</span><span class="sxs-lookup"><span data-stu-id="2821f-170">Only after they are all copied is hello completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="2821f-171">Você pode usar o hello **ForEach-Parallel** construir tooprocess comandos para cada item em uma coleção simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2821f-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="2821f-172">itens de saudação na coleção de saudação são processados em paralelo, enquanto Olá comandos no bloco de script hello são executados sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="2821f-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="2821f-173">Isso usa Olá seguindo a sintaxe mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="2821f-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="2821f-174">Nesse caso, atividade1 inicia em Olá a mesma hora para todos os itens na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="2821f-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="2821f-175">Para cada item, a Activity2 será iniciada após a conclusão da Activity1.</span><span class="sxs-lookup"><span data-stu-id="2821f-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="2821f-176">A Activity3 começará somente depois da conclusão da Activity1 e Activity2 para todos os itens.</span><span class="sxs-lookup"><span data-stu-id="2821f-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="2821f-177">saudação de exemplo a seguir é semelhante exemplo anterior toohello copiando arquivos em paralelo.</span><span class="sxs-lookup"><span data-stu-id="2821f-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="2821f-178">Nesse caso, uma mensagem é exibida para cada arquivo depois de copiar.</span><span class="sxs-lookup"><span data-stu-id="2821f-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="2821f-179">Somente depois que todos estejam completamente copiado é mensagem de saudação do final de conclusão exibida.</span><span class="sxs-lookup"><span data-stu-id="2821f-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="2821f-180">Não é recomendável executar runbooks filho em paralelo, porque isso mostrou resultados não confiáveis toogive.</span><span class="sxs-lookup"><span data-stu-id="2821f-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="2821f-181">Hello saída do runbook filho de hello, às vezes, não aparece e configurações no runbook de um filho podem afetar Olá outros runbooks filho paralela</span><span class="sxs-lookup"><span data-stu-id="2821f-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="2821f-182">Pontos de verificação</span><span class="sxs-lookup"><span data-stu-id="2821f-182">Checkpoints</span></span>
<span data-ttu-id="2821f-183">Um *ponto de verificação* é um instantâneo do estado atual de saudação do fluxo de trabalho de saudação que inclui o valor atual de saudação para variáveis e qualquer saída gerada toothat ponto.</span><span class="sxs-lookup"><span data-stu-id="2821f-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="2821f-184">Se um fluxo de trabalho termina em erro ou está suspenso, em seguida, Olá próxima vez que ele é executado será iniciado de seu último ponto de verificação, em vez de início de saudação do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2821f-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="2821f-185">Você pode definir um ponto de verificação em um fluxo de trabalho com hello **Checkpoint-Workflow** atividade.</span><span class="sxs-lookup"><span data-stu-id="2821f-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="2821f-186">Olá código de exemplo a seguir, uma exceção ocorre após a atividade2 causando Olá tooend de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2821f-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="2821f-187">Quando o fluxo de trabalho de saudação for executado novamente, ele começa pela execução da atividade2, já que isso estava logo após o último ponto de verificação de saudação definido.</span><span class="sxs-lookup"><span data-stu-id="2821f-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="2821f-188">Você deve definir pontos de verificação em um fluxo de trabalho depois que as atividades que podem estar sujeito a tooexception e não devem ser repetida se o fluxo de trabalho Olá será retomado.</span><span class="sxs-lookup"><span data-stu-id="2821f-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="2821f-189">Por exemplo, o fluxo de trabalho pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2821f-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="2821f-190">Você pode definir um ponto de verificação antes e depois da máquina virtual do hello comandos toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2821f-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="2821f-191">Se a falha na criação do hello, comandos Olá seriam repetidos se o fluxo de trabalho de saudação for iniciado novamente.</span><span class="sxs-lookup"><span data-stu-id="2821f-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="2821f-192">Se Olá trabalho falhar após a criação de saudação terá êxito, em seguida, Olá máquina virtual será não ser criada novamente quando o fluxo de trabalho de saudação é retomado.</span><span class="sxs-lookup"><span data-stu-id="2821f-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="2821f-193">saudação de exemplo a seguir copia o local da rede tooa vários arquivos e define um ponto de verificação após cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="2821f-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="2821f-194">Se o local de rede Olá for perdido, o fluxo de trabalho de saudação termina em erro.</span><span class="sxs-lookup"><span data-stu-id="2821f-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="2821f-195">Quando ele for iniciado novamente, ele será retomado no hello último ponto de verificação que significa que somente os arquivos de saudação que já foram copiados são ignorados.</span><span class="sxs-lookup"><span data-stu-id="2821f-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="2821f-196">Como as credenciais de nome de usuário não são mantidas após chamar hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) atividade ou após o último ponto de verificação de saudação, você precisa tooset Olá credenciais toonull e, em seguida, recuperá-los novamente do armazenamento de ativos de saudação após  **Fluxo de trabalho Suspender** ou ponto de verificação é chamado.</span><span class="sxs-lookup"><span data-stu-id="2821f-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="2821f-197">Caso contrário, você pode receber Olá a seguinte mensagem de erro: *não é possível continuar o fluxo de trabalho hello, ou porque os dados de persistência podem não ser completamente salvos ou salva dados de persistência estão corrompidos. Você deve reiniciar o fluxo de trabalho de saudação.*</span><span class="sxs-lookup"><span data-stu-id="2821f-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="2821f-198">Olá mesmo código a seguir demonstra como toohandle isso em seus runbooks do fluxo de trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2821f-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="2821f-199">Isso não é necessário se você estiver autenticando usando uma conta Executar como configurada com uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="2821f-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="2821f-200">Para obter mais informações sobre pontos de verificação, consulte [tooa de pontos de verificação de adição de fluxo de trabalho de Script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="2821f-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2821f-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2821f-201">Next steps</span></span>
* <span data-ttu-id="2821f-202">tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="2821f-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
