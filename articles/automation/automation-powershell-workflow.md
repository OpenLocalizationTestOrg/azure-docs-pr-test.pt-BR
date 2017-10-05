---
title: "Aprender sobre o Fluxo de Trabalho do PowerShell para Automação do Azure | Microsoft Docs"
description: "Este artigo é concebido como uma lição rápida para autores familiarizados com o PowerShell para entender as diferenças entre o PowerShell e o fluxo de trabalho do PowerShell e conceitos aplicáveis aos runbooks de Automação."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="0847e-103">Aprender sobre os principais conceitos de Fluxo de Trabalho do Windows PowerShell para runbooks de Automação</span><span class="sxs-lookup"><span data-stu-id="0847e-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="0847e-104">Os runbooks na Automação do Azure são implementados como Fluxos de Trabalho do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0847e-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="0847e-105">Um fluxo de trabalho do Windows PowerShell é semelhante a um script do Windows PowerShell, mas tem algumas diferenças significativas que podem ser confusas para um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="0847e-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="0847e-106">Embora este artigo sirva para ajudar você a escrever runbooks usando o Fluxo de Trabalho do PowerShell, recomendamos que você escreva os runbooks usando o PowerShell, a menos que você precise de pontos de verificação.</span><span class="sxs-lookup"><span data-stu-id="0847e-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="0847e-107">Há diversas diferenças de sintaxe quando se cria runbooks de Fluxo de trabalho do PowerShell, e essas diferenças exigem um pouco mais de trabalho para escrever fluxos de trabalho efetivos.</span><span class="sxs-lookup"><span data-stu-id="0847e-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="0847e-108">Um fluxo de trabalho é uma sequência de etapas programadas e conectadas que executam tarefas de longa duração ou exigem a coordenação de várias etapas em vários dispositivos ou nós gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0847e-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="0847e-109">Os benefícios de um fluxo de trabalho comparado com um script normal incluem a capacidade de realizar simultaneamente uma ação em vários dispositivos e a capacidade de se recuperar automaticamente de falhas.</span><span class="sxs-lookup"><span data-stu-id="0847e-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="0847e-110">Um Fluxo de Trabalho do Windows PowerShell é um script do Windows PowerShell que usa o Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="0847e-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="0847e-111">Embora o fluxo de trabalho seja escrito com a sintaxe do Windows PowerShell e inicializado pelo Windows PowerShell, ele é processado pelo Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="0847e-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="0847e-112">Para obter detalhes completos sobre os tópicos nesse artigo, consulte [Introdução ao fluxo de trabalho do Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="0847e-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="0847e-113">Estrutura básica de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="0847e-113">Basic structure of a workflow</span></span>
<span data-ttu-id="0847e-114">A primeira etapa para converter um script do PowerShell para um fluxo de trabalho do PowerShell é circunscrevê-lo com a palavra-chave **Workflow** .</span><span class="sxs-lookup"><span data-stu-id="0847e-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="0847e-115">Um fluxo de trabalho começa com a palavra-chave **Workflow** seguida do corpo do script entre chaves.</span><span class="sxs-lookup"><span data-stu-id="0847e-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="0847e-116">O nome do fluxo de trabalho segue a palavra-chave **Workflow**, conforme mostra a sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="0847e-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="0847e-117">O nome do fluxo de trabalho deve corresponder ao nome do runbook de automação.</span><span class="sxs-lookup"><span data-stu-id="0847e-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="0847e-118">Se o runbook está sendo importado, o nome do arquivo deve corresponder ao nome do fluxo de trabalho e deve terminar em *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="0847e-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="0847e-119">Para adicionar parâmetros ao fluxo de trabalho, use a palavra-chave **Param** , exatamente como faria para um script.</span><span class="sxs-lookup"><span data-stu-id="0847e-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="0847e-120">Alterações de código</span><span class="sxs-lookup"><span data-stu-id="0847e-120">Code changes</span></span>
<span data-ttu-id="0847e-121">O código de fluxo de trabalho do PowerShell é praticamente idêntico ao código de script do PowerShell, exceto por algumas alterações significativas.</span><span class="sxs-lookup"><span data-stu-id="0847e-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="0847e-122">As seções a seguir descrevem as alterações que você precisa fazer em um script do PowerShell para ele para executar em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="0847e-123">Atividades</span><span class="sxs-lookup"><span data-stu-id="0847e-123">Activities</span></span>
<span data-ttu-id="0847e-124">Uma atividade é uma tarefa específica em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="0847e-125">Assim como um script é composto de um ou mais comandos, um fluxo de trabalho é composto de uma ou mais atividades que são executadas em uma sequência.</span><span class="sxs-lookup"><span data-stu-id="0847e-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="0847e-126">O fluxo de trabalho do Windows PowerShell converte automaticamente muitos dos cmdlets do Windows PowerShell para atividades ao executar um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="0847e-127">Quando você especifica um desses cmdlets em seu runbook, a atividade correspondente é executada pelo Windows Workflow Foundation.</span><span class="sxs-lookup"><span data-stu-id="0847e-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="0847e-128">Para esses cmdlets sem uma atividade correspondente, o Fluxo de Trabalho do Windows PowerShell executa o cmdlet automaticamente dentro de uma atividade de [InlineScript](#inlinescript) .</span><span class="sxs-lookup"><span data-stu-id="0847e-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="0847e-129">Há um conjunto de cmdlets que são excluídos e não podem ser usados em um fluxo de trabalho, a menos que você o inclua explicitamente em um bloco de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="0847e-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="0847e-130">Para obter mais detalhes sobre esses conceitos, confira [Usando atividades em fluxos de trabalho de script](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="0847e-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="0847e-131">As atividades de fluxo de trabalho compartilham um conjunto de parâmetros comuns para configurar suas operações.</span><span class="sxs-lookup"><span data-stu-id="0847e-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="0847e-132">Para obter detalhes sobre os parâmetros comuns do fluxo de trabalho, consulte [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="0847e-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="0847e-133">Parâmetros posicionais</span><span class="sxs-lookup"><span data-stu-id="0847e-133">Positional parameters</span></span>
<span data-ttu-id="0847e-134">Você não pode usar parâmetros posicionais com atividades e cmdlets em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="0847e-135">Tudo o que isso significa é que você deve usar nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0847e-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="0847e-136">Por exemplo, considere o código a seguir que obtém todos os serviços em execução.</span><span class="sxs-lookup"><span data-stu-id="0847e-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="0847e-137">Se você tentar executar esse mesmo código em um fluxo de trabalho, receberá uma mensagem como "O conjunto de parâmetros não pode ser resolvido usando os parâmetros nomeados especificados".</span><span class="sxs-lookup"><span data-stu-id="0847e-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="0847e-138">Para corrigir isso, basta fornecer o nome do parâmetro como demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="0847e-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="0847e-139">Objetos desserializados</span><span class="sxs-lookup"><span data-stu-id="0847e-139">Deserialized objects</span></span>
<span data-ttu-id="0847e-140">Os objetos em fluxos de trabalho são desserializados.</span><span class="sxs-lookup"><span data-stu-id="0847e-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="0847e-141">Isso significa que suas propriedades ainda estão disponíveis, mas não seus métodos.</span><span class="sxs-lookup"><span data-stu-id="0847e-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="0847e-142">Por exemplo, considere código do PowerShell a seguir que para um serviço usando o método Stop do objeto Service.</span><span class="sxs-lookup"><span data-stu-id="0847e-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="0847e-143">Se você tentar executá-lo em um fluxo de trabalho, receberá um erro dizendo "Não há suporte para a invocação de método em um Fluxo de Trabalho do Windows PowerShell".</span><span class="sxs-lookup"><span data-stu-id="0847e-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="0847e-144">Uma opção é encapsular essas duas linhas de código em um bloco [InlineScript](#inlinescript); neste caso, $Service seria um objeto de serviço dentro do bloco.</span><span class="sxs-lookup"><span data-stu-id="0847e-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="0847e-145">Outra opção é usar outro cmdlet que executa a mesma funcionalidade que o método, se houver um disponível.</span><span class="sxs-lookup"><span data-stu-id="0847e-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="0847e-146">No nosso exemplo, o cmdlet Stop-Service fornece a mesma funcionalidade que o método Stop, sendo que você pode usar o demonstrado a seguir para um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="0847e-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="0847e-147">InlineScript</span></span>
<span data-ttu-id="0847e-148">A atividade **InlineScript** é útil quando você precisa executar um ou mais comandos como um script do PowerShell tradicional em vez do fluxo de trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0847e-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="0847e-149">Enquanto os comandos em um fluxo de trabalho são enviados ao Windows Workflow Foundation para processamento, os comandos em um bloco de InlineScript são processados pelo Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0847e-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="0847e-150">O InlineScript usa a sintaxe mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="0847e-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="0847e-151">Você pode retornar a saída de um InlineScript atribuindo a saída a uma variável.</span><span class="sxs-lookup"><span data-stu-id="0847e-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="0847e-152">O exemplo a seguir para um serviço e, em seguida, gera o nome do serviço.</span><span class="sxs-lookup"><span data-stu-id="0847e-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="0847e-153">Você pode passar valores para um bloco InlineScript, mas deve usar o modificador de escopo **$Using** .</span><span class="sxs-lookup"><span data-stu-id="0847e-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="0847e-154">O exemplo a seguir é idêntico ao exemplo anterior, exceto que o nome do serviço é fornecido por uma variável.</span><span class="sxs-lookup"><span data-stu-id="0847e-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="0847e-155">Embora as atividades InlineScript possam ser essenciais em determinados fluxos de trabalho, elas não dão suporte a construtores de fluxo de trabalho e devem ser usadas somente quando necessário pelos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="0847e-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="0847e-156">Não é possível usar [pontos de verificação](#checkpoints) dentro de um bloco InlineScript.</span><span class="sxs-lookup"><span data-stu-id="0847e-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="0847e-157">Se uma falha ocorre dentro do bloco, ele deve ser retomado desde o início do bloco.</span><span class="sxs-lookup"><span data-stu-id="0847e-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="0847e-158">Não é possível usar a [execução paralela](#parallel-processing) dentro de um InlineScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="0847e-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="0847e-159">O InlineScript afeta a escalabilidade do fluxo de trabalho, uma vez que retém a sessão do Windows PowerShell por toda a duração do bloco de InlineScript.</span><span class="sxs-lookup"><span data-stu-id="0847e-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="0847e-160">Para obter mais informações sobre como usar o InlineScript, consulte [Executando comandos do Windows PowerShell em um fluxo de trabalho](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="0847e-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="0847e-161">Processamento paralelo</span><span class="sxs-lookup"><span data-stu-id="0847e-161">Parallel processing</span></span>
<span data-ttu-id="0847e-162">Uma vantagem dos Fluxos de Trabalho do Windows PowerShell é a capacidade de executar um conjunto de comandos em paralelo em vez de sequencialmente como com um script típico.</span><span class="sxs-lookup"><span data-stu-id="0847e-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="0847e-163">Você pode usar a palavra-chave **Parallel** para criar um bloco de script com vários comandos que são executados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0847e-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="0847e-164">Isso usa a sintaxe a seguir, mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="0847e-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="0847e-165">Nesse caso, Activity1 e a Activity2 começarão simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0847e-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="0847e-166">A Activity3 começará somente após a conclusão da Activity1 e da Activity2.</span><span class="sxs-lookup"><span data-stu-id="0847e-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="0847e-167">Por exemplo, considere os seguintes comandos do PowerShell que copiam vários arquivos para um destino de rede.</span><span class="sxs-lookup"><span data-stu-id="0847e-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="0847e-168">Esses comandos são executados em sequência, de forma que a cópia de um arquivo deve terminar antes que a do próximo seja iniciada.</span><span class="sxs-lookup"><span data-stu-id="0847e-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="0847e-169">O fluxo de trabalho a seguir executa esses mesmos comandos em paralelo para que todos eles comecem a copiar ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0847e-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="0847e-170">A mensagem de conclusão será exibida somente depois que todos eles tiverem sido copiados.</span><span class="sxs-lookup"><span data-stu-id="0847e-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="0847e-171">Você pode usar o construct **ForEach-Parallel** para processar comandos de cada item em uma coleção simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0847e-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="0847e-172">Os itens na coleção são processados em paralelo, enquanto os comandos no bloco de script são executados em sequência.</span><span class="sxs-lookup"><span data-stu-id="0847e-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="0847e-173">Isso usa a sintaxe a seguir, mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="0847e-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="0847e-174">Nesse caso, Activity1 será iniciada simultaneamente para todos os itens na coleção.</span><span class="sxs-lookup"><span data-stu-id="0847e-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="0847e-175">Para cada item, a Activity2 será iniciada após a conclusão da Activity1.</span><span class="sxs-lookup"><span data-stu-id="0847e-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="0847e-176">A Activity3 começará somente depois da conclusão da Activity1 e Activity2 para todos os itens.</span><span class="sxs-lookup"><span data-stu-id="0847e-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="0847e-177">O exemplo a seguir é semelhante ao exemplo anterior copiando os arquivos em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0847e-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="0847e-178">Nesse caso, uma mensagem é exibida para cada arquivo depois de copiar.</span><span class="sxs-lookup"><span data-stu-id="0847e-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="0847e-179">Somente depois que todos estiverem completamente copiados a mensagem de conclusão final é exibida.</span><span class="sxs-lookup"><span data-stu-id="0847e-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="0847e-180">Não recomendamos a execução de runbooks filho em paralelo, uma vez que isso demonstrou fornecer resultados não confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0847e-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="0847e-181">Às vezes, a saída do runbook filho não é exibida e as configurações em um runbook filho podem afetar os outros runbooks filho paralelos</span><span class="sxs-lookup"><span data-stu-id="0847e-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="0847e-182">pontos de verificação</span><span class="sxs-lookup"><span data-stu-id="0847e-182">Checkpoints</span></span>
<span data-ttu-id="0847e-183">Um *ponto de verificação* é um instantâneo do estado atual do fluxo de trabalho que inclui o valor atual de variáveis e as saídas geradas para aquele ponto.</span><span class="sxs-lookup"><span data-stu-id="0847e-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="0847e-184">Se um fluxo de trabalho terminar em erro ou se for suspenso, na próxima vez que ele for executado, iniciará no seu último ponto de verificação e não no início do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0847e-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="0847e-185">Você pode definir um ponto de verificação em um fluxo de trabalho com a atividade **Checkpoint-Workflow** .</span><span class="sxs-lookup"><span data-stu-id="0847e-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="0847e-186">No código de exemplo a seguir, uma exceção ocorre após Activity2, fazendo com que o fluxo de trabalho seja encerrado.</span><span class="sxs-lookup"><span data-stu-id="0847e-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="0847e-187">Quando o fluxo de trabalho é executado novamente, ele começa pela execução de Activity2, já que isso foi logo após o último ponto de verificação definido.</span><span class="sxs-lookup"><span data-stu-id="0847e-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="0847e-188">Você deve definir pontos de verificação em um fluxo de trabalho para depois de atividades que possam estar sujeitas a exceção e não devam ser repetidas se o fluxo de trabalho for retomado.</span><span class="sxs-lookup"><span data-stu-id="0847e-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="0847e-189">Por exemplo, o fluxo de trabalho pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0847e-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="0847e-190">Você pode definir um ponto de verificação antes e depois dos comandos para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0847e-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="0847e-191">Se a criação falhar, os comandos serão repetidos se o fluxo de trabalho for iniciado novamente.</span><span class="sxs-lookup"><span data-stu-id="0847e-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="0847e-192">Se o fluxo de trabalho falhar após a criação ser bem-sucedida, a máquina virtual não será criada novamente quando o fluxo de trabalho for retomado.</span><span class="sxs-lookup"><span data-stu-id="0847e-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="0847e-193">O exemplo a seguir copia vários arquivos para um local de rede e define um ponto de verificação depois de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="0847e-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="0847e-194">Se o local de rede for perdido, o fluxo de trabalho terminará em erro.</span><span class="sxs-lookup"><span data-stu-id="0847e-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="0847e-195">Quando ele for iniciado novamente, ele retomará do último ponto de verificação, o que significa que somente os arquivos que já tiverem sido copiados serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="0847e-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="0847e-196">Como as credenciais do nome de usuário não são mantidas depois de chamar a atividade [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) ou após o último ponto de verificação, você precisa definir as credenciais para null e recuperá-las novamente no armazenamento de ativos após **Suspend-Workflow** ou o ponto de verificação ser chamado.</span><span class="sxs-lookup"><span data-stu-id="0847e-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="0847e-197">Caso contrário, você pode receber a seguinte mensagem de erro: *não é possível continuar o fluxo de trabalho, ou porque não foi possível salvar completamente os dados de persistência, ou porque os dados de persistência salvos estão corrompidos. Você deve reiniciar o fluxo de trabalho.*</span><span class="sxs-lookup"><span data-stu-id="0847e-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="0847e-198">O mesmo código a seguir demonstra como lidar com isso em seus runbooks do Fluxo de Trabalho do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0847e-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="0847e-199">Isso não é necessário se você estiver autenticando usando uma conta Executar como configurada com uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0847e-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="0847e-200">Para saber mais sobre pontos de verificação, confira [Adicionando pontos de verificação a um Fluxo de Trabalho de script](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="0847e-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0847e-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0847e-201">Next steps</span></span>
* <span data-ttu-id="0847e-202">Para começar a usar runbooks de fluxo de trabalho do PowerShell, veja [Meu primeiro runbook de Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="0847e-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
