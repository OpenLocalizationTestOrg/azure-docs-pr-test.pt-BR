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
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Aprender sobre os principais conceitos de Fluxo de Trabalho do Windows PowerShell para runbooks de Automação 
Os runbooks na Automação do Azure são implementados como Fluxos de Trabalho do Windows PowerShell.  Um fluxo de trabalho do Windows PowerShell é o script do Windows PowerShell tooa semelhante, mas tem algumas diferenças importantes que podem ser confusas tooa novo usuário.  Enquanto este artigo é pretendido toohelp escrever runbooks usando o fluxo de trabalho do PowerShell, é recomendável que você escreve runbooks usando o PowerShell, a menos que você precisa de pontos de verificação.  Há várias diferenças de sintaxe, quando se cria runbooks do fluxo de trabalho do PowerShell e essas diferenças requerem um pouco mais trabalho toowrite efetivo fluxos de trabalho.  

Um fluxo de trabalho é uma sequência de etapas programadas e conectadas que executam tarefas de execução longa ou exigem a coordenação de saudação de várias etapas em vários dispositivos ou nós gerenciados. Olá, benefícios de um fluxo de trabalho em um script normal incluem a capacidade de saudação toosimultaneously executar uma ação em vários dispositivos e Olá capacidade tooautomatically recuperar de falhas. Um Fluxo de Trabalho do Windows PowerShell é um script do Windows PowerShell que usa o Windows Workflow Foundation. Enquanto o fluxo de trabalho de saudação é escrito com sintaxe do Windows PowerShell e lançado pelo Windows PowerShell, ela é processada pelo Windows Workflow Foundation.

Para obter detalhes completos sobre tópicos Olá neste artigo, consulte [guia de Introdução ao fluxo de trabalho do Windows PowerShell](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Estrutura básica de um fluxo de trabalho
Olá primeira etapa tooconverting um fluxo de trabalho do PowerShell script tooa PowerShell é envolve com hello **fluxo de trabalho** palavra-chave.  Inicia um fluxo de trabalho com hello **fluxo de trabalho** palavra-chave seguida pelo corpo de saudação do script hello entre chaves. nome de saudação do fluxo de trabalho Olá segue Olá **fluxo de trabalho** conforme Olá segue a sintaxe da palavra-chave:

    Workflow Test-Workflow
    {
       <Commands>
    }

nome de saudação do fluxo de trabalho de saudação deve corresponder o nome de Olá de runbook da automação hello. Se Olá runbook está sendo importado, nome de arquivo hello deve corresponder ao nome do fluxo de trabalho hello e deve terminar em *. ps1*.

tooadd parâmetros toohello fluxo de trabalho, use Olá **Param** exatamente como você faria tooa script de palavra-chave.

## <a name="code-changes"></a>Alterações de código
Código de fluxo de trabalho do PowerShell analisa o código de script tooPowerShell quase idênticos, exceto algumas alterações significativas.  Olá seções a seguir descreve as alterações que você precisa toomake tooa de script do PowerShell para ele toorun em um fluxo de trabalho.

### <a name="activities"></a>Atividades
Uma atividade é uma tarefa específica em um fluxo de trabalho. Assim como um script é composto de um ou mais comandos, um fluxo de trabalho é composto de uma ou mais atividades que são executadas em uma sequência. O fluxo de trabalho do Windows PowerShell converte automaticamente muitos dos Olá tooactivities de cmdlets do Windows PowerShell quando ele é executado em um fluxo de trabalho. Quando você especificar um desses cmdlets em seu runbook, atividade correspondente Olá é executada pelo Windows Workflow Foundation. Para os cmdlets sem uma atividade correspondente, o fluxo de trabalho do Windows PowerShell executa automaticamente cmdlet hello dentro um [InlineScript](#inlinescript) atividade. Há um conjunto de cmdlets que são excluídos e não podem ser usados em um fluxo de trabalho, a menos que você o inclua explicitamente em um bloco de InlineScript. Para obter mais detalhes sobre esses conceitos, confira [Usando atividades em fluxos de trabalho de script](http://technet.microsoft.com/library/jj574194.aspx).

Atividades de fluxo de trabalho compartilham um conjunto de tooconfigure de parâmetros comuns de sua operação. Para obter detalhes sobre os parâmetros comuns de fluxo de trabalho hello, consulte [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Parâmetros posicionais
Você não pode usar parâmetros posicionais com atividades e cmdlets em um fluxo de trabalho.  Tudo o que isso significa é que você deve usar nomes de parâmetro.

Por exemplo, considere Olá código que obtém todos os serviços em execução a seguir.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Se você tentar toorun esse mesmo código em um fluxo de trabalho, você receberá uma mensagem como "Conjunto não pode ser resolvido Olá especificado do parâmetro nomeado parâmetros."  toocorrect, fornecer o nome do parâmetro hello seguinte hello.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Objetos desserializados
Os objetos em fluxos de trabalho são desserializados.  Isso significa que suas propriedades ainda estão disponíveis, mas não seus métodos.  Por exemplo, considere Olá código do PowerShell que interrompe um serviço usando o método de parada Olá Olá do objeto de serviço a seguir.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Se você tentar toorun isso em um fluxo de trabalho, você receberá um erro informando que "invocação de método não é suportada em um fluxo de trabalho do Windows PowerShell."  

Uma opção é toowrap estas duas linhas de código em um [InlineScript](#inlinescript) bloquear em caso $Service seria um objeto de serviço no bloco de saudação.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Outra opção é toouse outro cmdlet que executa Olá a mesma funcionalidade que o método hello, se houver um disponível.  Em nosso exemplo, o cmdlet Stop-Service de saudação fornece Olá mesma funcionalidade que o método de parada Olá e você pode usar o seguinte Olá para um fluxo de trabalho.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
Olá **InlineScript** atividade é útil quando você precisa toorun um ou mais comandos como tradicional script do PowerShell em vez de fluxo de trabalho do PowerShell.  Enquanto os comandos em um fluxo de trabalho são enviados tooWindows Workflow Foundation para processamento, os comandos em um bloco InlineScript são processados pelo Windows PowerShell.

O InlineScript utiliza Olá seguindo a sintaxe mostrada abaixo.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Você pode retornar a saída de um InlineScript atribuindo Olá saída tooa variável. Olá exemplo a seguir interrompe um serviço e, em seguida, gera o nome do serviço de saudação.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Você pode passar valores para um bloco InlineScript, mas deve usar o modificador de escopo **$Using** .  Olá exemplo a seguir é exemplo anterior toohello idênticos exceto hello nome do serviço é fornecido por uma variável.

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


Atividades InlineScript podem ser essenciais para alguns fluxos de trabalho, eles não oferecem suporte a construções de fluxo de trabalho e devem ser usados somente quando necessário para Olá motivos a seguir:

* Não é possível usar [pontos de verificação](#checkpoints) dentro de um bloco InlineScript. Se ocorrer uma falha em bloco Olá, ele deverá ser retomado do início de saudação do bloco de saudação.
* Não é possível usar a [execução paralela](#parallel-processing) dentro de um InlineScriptBlock.
* InlineScript afeta a escalabilidade de fluxo de trabalho hello, uma vez que retém a sessão do Windows PowerShell Olá para todo o comprimento do bloco de InlineScript Olá Olá.

Para obter mais informações sobre como usar o InlineScript, consulte [Executando comandos do Windows PowerShell em um fluxo de trabalho](http://technet.microsoft.com/library/jj574197.aspx) e [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Processamento paralelo
Uma vantagem dos fluxos de trabalho do Windows PowerShell é Olá capacidade tooperform um conjunto de comandos em paralelo, em vez de sequencialmente como com um script típico.

Você pode usar o hello **paralela** palavra-chave toocreate um bloco de script com vários comandos que são executados simultaneamente. Isso usa Olá seguindo a sintaxe mostrada abaixo. Nesse caso, a atividade1 e da atividade2 inicia em Olá simultaneamente. A Activity3 começará somente após a conclusão da Activity1 e da Activity2.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Por exemplo, considere Olá seguintes comandos do PowerShell que vários arquivos tooa rede destino da cópia.  Esses comandos são executados sequencialmente para que um arquivo deve concluir a cópia antes de saudação é iniciada.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Olá seguinte fluxo de trabalho executa esses mesmos comandos em paralelo, para que todos eles iniciarem a cópia no hello mesmo tempo.  Somente depois que todas elas sejam copiados é Olá conclusão mensagem exibida.

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


Você pode usar o hello **ForEach-Parallel** construir tooprocess comandos para cada item em uma coleção simultaneamente. itens de saudação na coleção de saudação são processados em paralelo, enquanto Olá comandos no bloco de script hello são executados sequencialmente. Isso usa Olá seguindo a sintaxe mostrada abaixo. Nesse caso, atividade1 inicia em Olá a mesma hora para todos os itens na coleção de saudação. Para cada item, a Activity2 será iniciada após a conclusão da Activity1. A Activity3 começará somente depois da conclusão da Activity1 e Activity2 para todos os itens.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

saudação de exemplo a seguir é semelhante exemplo anterior toohello copiando arquivos em paralelo.  Nesse caso, uma mensagem é exibida para cada arquivo depois de copiar.  Somente depois que todos estejam completamente copiado é mensagem de saudação do final de conclusão exibida.

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
> Não é recomendável executar runbooks filho em paralelo, porque isso mostrou resultados não confiáveis toogive.  Hello saída do runbook filho de hello, às vezes, não aparece e configurações no runbook de um filho podem afetar Olá outros runbooks filho paralela
>

## <a name="checkpoints"></a>Pontos de verificação
Um *ponto de verificação* é um instantâneo do estado atual de saudação do fluxo de trabalho de saudação que inclui o valor atual de saudação para variáveis e qualquer saída gerada toothat ponto. Se um fluxo de trabalho termina em erro ou está suspenso, em seguida, Olá próxima vez que ele é executado será iniciado de seu último ponto de verificação, em vez de início de saudação do fluxo de trabalho de saudação.  Você pode definir um ponto de verificação em um fluxo de trabalho com hello **Checkpoint-Workflow** atividade.

Olá código de exemplo a seguir, uma exceção ocorre após a atividade2 causando Olá tooend de fluxo de trabalho. Quando o fluxo de trabalho de saudação for executado novamente, ele começa pela execução da atividade2, já que isso estava logo após o último ponto de verificação de saudação definido.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Você deve definir pontos de verificação em um fluxo de trabalho depois que as atividades que podem estar sujeito a tooexception e não devem ser repetida se o fluxo de trabalho Olá será retomado. Por exemplo, o fluxo de trabalho pode criar uma máquina virtual. Você pode definir um ponto de verificação antes e depois da máquina virtual do hello comandos toocreate hello. Se a falha na criação do hello, comandos Olá seriam repetidos se o fluxo de trabalho de saudação for iniciado novamente. Se Olá trabalho falhar após a criação de saudação terá êxito, em seguida, Olá máquina virtual será não ser criada novamente quando o fluxo de trabalho de saudação é retomado.

saudação de exemplo a seguir copia o local da rede tooa vários arquivos e define um ponto de verificação após cada arquivo.  Se o local de rede Olá for perdido, o fluxo de trabalho de saudação termina em erro.  Quando ele for iniciado novamente, ele será retomado no hello último ponto de verificação que significa que somente os arquivos de saudação que já foram copiados são ignorados.

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

Como as credenciais de nome de usuário não são mantidas após chamar hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) atividade ou após o último ponto de verificação de saudação, você precisa tooset Olá credenciais toonull e, em seguida, recuperá-los novamente do armazenamento de ativos de saudação após  **Fluxo de trabalho Suspender** ou ponto de verificação é chamado.  Caso contrário, você pode receber Olá a seguinte mensagem de erro: *não é possível continuar o fluxo de trabalho hello, ou porque os dados de persistência podem não ser completamente salvos ou salva dados de persistência estão corrompidos. Você deve reiniciar o fluxo de trabalho de saudação.*

Olá mesmo código a seguir demonstra como toohandle isso em seus runbooks do fluxo de trabalho do PowerShell.

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


Isso não é necessário se você estiver autenticando usando uma conta Executar como configurada com uma entidade de serviço.  

Para obter mais informações sobre pontos de verificação, consulte [tooa de pontos de verificação de adição de fluxo de trabalho de Script](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
