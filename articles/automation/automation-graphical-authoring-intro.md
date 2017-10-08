---
title: "aaaGraphical criação na automação do Azure | Microsoft Docs"
description: "Criação gráfica permite que você toocreate runbooks de automação do Azure sem trabalhar com o código. Este artigo fornece uma introdução de criação de toographical e todos os detalhes de saudação necessária toostart criando um runbook gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Criação gráfica na Automação do Azure
## <a name="introduction"></a>Introdução
Criação gráfica permite toocreate runbooks de automação do Azure sem as complexidades de saudação do código subjacente saudação do Windows PowerShell ou fluxo de trabalho do PowerShell. Adicionar atividades toohello tela de uma biblioteca de cmdlets e runbooks, conectá-los e configurar tooform um fluxo de trabalho.  Se você já trabalhou com o System Center Orchestrator ou Service Management Automation (SMA), isso deve ser tooyou familiar.   

Este artigo fornece uma introdução toographical conceitos de criação e hello que necessário tooget iniciado na criação de um runbook gráfico.

## <a name="graphical-runbooks"></a>Runbooks gráficos
Todos os runbooks na Automação do Azure são Fluxos de Trabalho do Windows PowerShell.  Gráfico e fluxo de trabalho do PowerShell gráfica runbooks gerar código do PowerShell que é executado por funcionários de automação hello, mas não é capaz de tooview-la ou modificá-la diretamente.  Um runbook gráfico pode ser convertido tooa fluxo de trabalho do PowerShell gráfica runbook e vice-versa, mas eles não podem ser runbook textual tooa convertido. Um runbook textual existente não pode ser importado para o editor gráfico hello.  

## <a name="overview-of-graphical-editor"></a>Visão geral do editor gráfico
Você pode abrir o editor gráfico Olá no portal do Azure de saudação criando ou editando um runbook gráfico.

![Espaço de trabalho gráfico](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Olá seções a seguir descrevem controles Olá no editor gráfico hello.

### <a name="canvas"></a>Tela
Olá tela é onde você projetar seu runbook.  Adicionar atividades em nós Olá Olá biblioteca controle toohello runbook e conecte-se com a lógica de saudação toodefine links de runbook hello.

Você pode usar controles de saudação final Olá Olá tela toozoom e sair.

![Espaço de trabalho gráfico](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Controle de Biblioteca
Olá controle da biblioteca é onde você seleciona [atividades](#activities) tooadd tooyour runbook.  Você adicioná-las toohello tela onde você conectá-los tooother atividades.  Ele inclui quatro seções descritas no Olá a tabela a seguir.

| Seção | Descrição |
|:--- |:--- |
| Cmdlets |Inclui todos os cmdlets de saudação que pode ser usados em seu runbook.  Os cmdlets são organizados por módulo.  Todos os módulos de saudação que você instalou na sua conta de automação estarão disponíveis. |
| Runbooks |Inclui Olá runbooks em sua conta de automação. Esses runbooks podem ser adicionados toohello tela toobe usado como runbooks filho. Somente runbooks Olá mesmo tipo de núcleo Olá runbook que está sendo editado são mostradas; para gráfico runbooks apenas com base em PowerShell runbooks são mostradas, enquanto para fluxo de trabalho do PowerShell gráfica runbooks runbooks somente-fluxo de trabalho-com base em PowerShell são mostrados. |
| Ativos |Inclui Olá [ativos de automação](http://msdn.microsoft.com/library/dn939988.aspx) em sua conta de automação que pode ser usada em seu runbook.  Quando você adiciona um runbook de tooa ativo, ele adicionará uma atividade de fluxo de trabalho que obtém ativo selecionado hello.  No caso de saudação de ativos de variável, você pode selecionar se tooadd tooget uma atividade Olá variável Olá variável ou definido. |
| Controle de Runbook |Inclui as atividades de controle de runbook que podem ser usadas em seu runbook atual. Um *junção* pega várias entradas e aguarda até que todas sejam concluídas antes de fluxo de trabalho Olá continuando. Um *código* atividade é executada uma ou mais linhas de código do PowerShell ou fluxo de trabalho do PowerShell dependendo do tipo de runbook gráfico hello.  Você pode usar essa atividade para código personalizado ou para a funcionalidade que é difícil tooachieve com outras atividades. |

### <a name="configuration-control"></a>Controle de Configuração
Olá, controle de configuração é onde você fornece detalhes para um objeto selecionado na tela hello. Propriedades de saudação disponíveis neste controle dependerá de tipo de saudação do objeto selecionado.  Quando você seleciona uma opção em Olá controle de configuração, ela será aberta folhas adicionais nas informações adicionais de tooprovide de ordem.

### <a name="test-control"></a>Controle de Teste
Olá controle de teste não é exibida quando o editor gráfico Olá é iniciado pela primeira vez. Ele é aberto quando você [testa um runbook gráfico](#graphical-runbook-procedures)interativamente.  

## <a name="graphical-runbook-procedures"></a>Procedimentos de runbook gráfico
### <a name="exporting-and-importing-a-graphical-runbook"></a>Exportar e importar um runbook gráfico
Você só pode exportar Olá a versão publicada de um runbook gráfico.  Se o runbook Olá ainda não foram publicado, Olá **exportação publicada** botão será desabilitado.  Quando você clica em Olá **exportação publicada** botão, runbook hello é computador local tooyour baixado.  nome de saudação do arquivo hello corresponde o nome de saudação do runbook Olá com um *graphrunbook* extensão.

![Exportar publicado](media/automation-graphical-authoring-intro/runbook-export.png)

Você pode importar um arquivo de runbook gráfico ou fluxo de trabalho do PowerShell gráfico selecionando Olá **importar** opção ao adicionar um runbook.   Quando você seleciona Olá tooimport de arquivo, você pode manter Olá mesmo **nome** ou forneça um novo.  Olá campo de tipo de Runbook exibirá o tipo de saudação de runbook após ele avalia arquivo hello selecionado e se você tentar tooselect um tipo diferente que não está correto, que será apresentada uma mensagem de observar, há conflitos em potencial e durante a conversão, pode haver erros de sintaxe.  

![Importar runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Testando um runbook gráfico
Você pode testar a versão de rascunho de saudação de um runbook no portal do Azure de saudação enquanto deixar Olá publicado versão de runbook Olá inalterado, ou você pode testar um novo runbook antes que ele foi publicado. Isso permite que você tooverify que Olá runbook está funcionando corretamente antes de substituir a versão publicada hello. Quando você testar um runbook, Olá runbook de rascunho é executado e as ações que ele realiza são concluídas. Nenhum histórico de trabalho é criado, mas a saída é exibida no painel de saída do teste de saudação. 

Abrir o controle de teste de saudação de um runbook abrindo Olá runbook para editar e clique em Olá **painel teste** botão.

![Botão do painel de teste](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

Olá controle teste solicitará para parâmetros de entrada, e você pode iniciar o runbook Olá clicando em Olá **iniciar** botão.

![Botões de controle de teste](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Publicando um runbook gráfico
Cada runbook na Automação do Azure tem um Rascunho e uma versão Publicada. Somente a versão do hello publicada está disponível toobe executar, e somente a versão de rascunho Olá pode ser editada. versão publicada de saudação é afetado por uma versão de rascunho toohello alterações. Quando versão de rascunho hello está pronto toobe disponível, em seguida, publicá-la que substitui a versão publicada de saudação com versão de rascunho de saudação.

Você pode publicar um runbook gráfico abrindo Olá runbook para edição e, em seguida, clicando em Olá **publicar** botão.

![Botão Publicar](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Quando um runbook ainda não foi publicado, ele tem um status de **Novo**.  Quando é publicado, ele tem um status de **Publicado**.  Se você editar o runbook Olá depois que ele foi publicado e versões de rascunho e publicado Olá forem diferentes, o runbook Olá tem um status de **em edição**.

![Status de runbook](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

Você também tem a versão do hello opção toorevert toohello publicada de um runbook.  Isso descarta as alterações feitas desde o runbook Olá foi publicado pela última vez e substitui a versão de rascunho de saudação do hello runbook com a versão publicada de saudação.

![Reverter toopublished botão](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Atividades
Atividades são os blocos de construção de saudação de um runbook.  Uma atividade pode ser um cmdlet do PowerShell, um runbook filho ou uma atividade de fluxo de trabalho.  Adicionar um runbook de toohello atividade direito clicando em Olá controle da biblioteca e selecionando **adicionar toocanvas**.  Você pode clique e arraste hello atividade tooplace-la em qualquer lugar no hello tela que você deseja.  Hello local da saudação da atividade de saudação na tela hello não afeta a operação Olá de runbook Olá de qualquer forma.  Você pode layout seu runbook no entanto, você achar mais adequado toovisualize sua operação. 

![Adicionar toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Selecione suas propriedades e parâmetros de uma atividade de Olá em Olá tela tooconfigure na folha de configuração de saudação.  Você pode alterar Olá **rótulo** de toosomething de atividade de saudação é tooyou descritivo.  cmdlet original Olá ainda está sendo executado, você está alterando simplesmente seu nome de exibição que será usado no editor gráfico hello.  Olá rótulo deve ser exclusivo dentro de runbook hello. 

### <a name="parameter-sets"></a>Conjuntos de parâmetros
Um conjunto de parâmetros define parâmetros Olá obrigatórios e opcionais que aceitam valores de um cmdlet específico.  Todos os cmdlets têm pelo menos um conjunto de parâmetros, e alguns têm vários.  Se um cmdlet tem vários conjuntos de parâmetros, você deve selecionar qual deles usará para poder configurar os parâmetros.  parâmetros de saudação que você pode configurar dependerá de conjunto de parâmetros de saudação que você escolher.  Você pode alterar o conjunto de parâmetros de saudação usado por uma atividade selecionando **parâmetro definido** e selecionar outro conjunto.  Nesse caso, quaisquer valores de parâmetros que você tiver configurado serão perdidos.

Saudação de exemplo a seguir, Olá Get-AzureRmVM cmdlet tem três conjuntos de parâmetros.  Você não pode configurar valores de parâmetro até que você selecione um dos conjuntos de parâmetros de saudação.  Olá ListVirtualMachineInResourceGroupParamSet conjunto de parâmetros é para retornar todas as máquinas virtuais em um grupo de recursos e tem um único parâmetro opcional.  Olá GetVirtualMachineInResourceGroupParamSet é para especificar a máquina virtual de saudação desejado tooreturn e tem dois obrigatório e um parâmetro opcional.

![Conjunto de Parâmetros](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Valores de parâmetros
Quando você especificar um valor para um parâmetro, você pode selecionar um toodetermine de fonte de dados como valor de saudação será especificado.  fontes de dados de saudação que estão disponíveis para um determinado parâmetro dependerá dos valores válidos para esse parâmetro hello.  Por exemplo, Null não será uma opção disponível para um parâmetro que não permita valores nulos.

| Fonte de dados | Descrição |
|:--- |:--- |
| Valor Constante |Digite um valor para o parâmetro hello.  Isso só está disponível para Olá seguintes tipos de dados: Int32, Int64, String, Boolean, DateTime, comutador. |
| Saída de Atividade |Saída de uma atividade que precede a atividade atual Olá no fluxo de trabalho de saudação.  Todas as atividades válidas serão listadas.  Selecione apenas o hello atividade toouse sua saída para o valor do parâmetro hello.  Se a atividade de hello gera um objeto com várias propriedades, você pode digite Olá nome da propriedade Olá depois de selecionar a atividade de saudação. |
| Entrada do Runbook |Selecione um parâmetro de entrada do runbook como parâmetro de atividade de entrada toohello. |
| Ativo da Variável |Selecione uma Variável de Automação como entrada. |
| Ativo da Credencial |Selecione uma Credencial de Automação como entrada. |
| Ativo do Certificado |Selecione um Certificado de Automação como entrada. |
| Ativo da Conexão |Selecione uma Conexão de Automação como entrada. |
| Expressão do PowerShell |Especifique a [expressão simples do PowerShell](#powershell-expressions).  Olá expressão será avaliada antes hello atividade e hello resultado usado para o valor do parâmetro hello.  Você pode usar a saída de toohello toorefer variáveis de uma atividade ou um parâmetro de entrada do runbook. |
| Não configurado |Limpa qualquer valor que foi configurado anteriormente. |

#### <a name="optional-additional-parameters"></a>Parâmetros adicionais opcionais
Todos os cmdlets terá parâmetros adicionais do hello opção tooprovide.  Estes são os parâmetros comuns do PowerShell ou outros parâmetros personalizados.  Será exibida uma caixa de texto em que você pode fornecer parâmetros usando a sintaxe do PowerShell.  Por exemplo, toouse Olá **detalhado** parâmetro comum, você especificaria **"-Verbose: $True"**.

### <a name="retry-activity"></a>Atividade de repetição
**Comportamento de repetição** permite que um toobe atividade executado várias vezes até que uma determinada condição for atendida, assim como um loop.  Você pode usar esse recurso para atividades que deve ser executado várias vezes, estão sujeitos a erros e pode precisa de mais de uma tentativa para o sucesso ou de teste Olá informações de saída da atividade de saudação de dados válido.    

Quando você habilita a repetição de uma atividade, é possível definir um atraso e uma condição.  atraso de saudação é tempo de saudação (medido em segundos ou minutos) esse runbook Olá aguardará antes de executar atividade Olá novamente.  Se nenhum atraso for especificado, em seguida, hello atividade será executada novamente imediatamente após a sua conclusão. 

![Atraso de repetição de atividade](media/automation-graphical-authoring-intro/retry-delay.png)

condição de repetição de saudação é uma expressão do PowerShell que é avaliada após a execução de cada atividade de saudação do tempo.  Se Olá a expressão é resolvida tooTrue, em seguida, hello atividade é executada novamente.  Se a expressão Olá resolve tooFalse hello atividade não execute novamente e Olá runbook prossegue toohello próxima atividade. 

![Atraso de repetição de atividade](media/automation-graphical-authoring-intro/retry-condition.png)

condição de repetição Olá pode usar uma variável chamada $RetryData que fornece acesso tooinformation sobre tentativas de atividade de saudação.  Essa variável tem propriedades de saudação em Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| NumberOfAttempts |Número de vezes que hello atividade foi executado. |
| Saída |Saída de saudação da última execução da atividade de saudação. |
| TotalDuration |Atingiu o tempo decorrido desde hello atividade foi iniciada Olá a primeira vez. |
| StartedAt |Tempo de atividade de saudação do formato UTC foi iniciado pela primeira vez. |

Veja a seguir exemplos de condições de repetição da atividade.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Depois de configurar uma condição de repetição para uma atividade, atividade de saudação inclui dois tooremind de indicações visuais você.  Um é apresentado na atividade de saudação e Olá outros é quando você examinar configuração Olá da atividade de saudação.

![Indicadores Visuais de Repetição da Atividade](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Controle de Script de Fluxo de Trabalho
Um controle de código é uma atividade especial que aceita o script PowerShell ou o fluxo de trabalho do PowerShell, dependendo do tipo hello de runbook gráfico criado na funcionalidade de tooprovide ordem caso contrário, não estejam disponível.  Ele não pode aceitar parâmetros, mas pode usar variáveis para saída de atividade e parâmetros de entrada de runbook.  Todas as saídas da atividade de saudação é adicionada toohello databus menos que ele tenha nenhum link de saída nesse caso, ele é adicionado toohello saída de runbook hello.

Por exemplo hello código a seguir executa cálculos de data usando uma variável de entrada do runbook chamada $NumberOfDays.  Em seguida, envia uma data e hora calculadas como saída toobe usado por atividades subsequentes no runbook hello.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Links e fluxo de trabalho
Um **link** em um runbook gráfico conecta duas atividades.  Ele será exibido na tela hello como uma seta apontando da atividade de destino do hello origem atividade toohello.  atividades de Olá executadas na direção de saudação de seta Olá com atividade de destino de saudação inicial após a conclusão da atividade de origem hello.  

### <a name="create-a-link"></a>Criar um link
Crie um link entre duas atividades pela atividade de origem Olá selecionando e clicando em círculo de saudação na parte inferior da saudação de forma hello.  Arraste a atividade de destino do hello seta toohello e versão.

![Criar um link](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Selecione Olá link tooconfigure suas propriedades na folha de configuração de saudação.  Isso incluirá o tipo de link de saudação que é descrito em Olá a tabela a seguir.

| Tipo de link | Descrição |
|:--- |:--- |
| Pipeline |atividade de destino Olá é executada uma vez para cada objeto de saída da atividade de origem hello.  atividade de destino Olá não será executado se a atividade de origem Olá resulta em nenhuma saída.  Saída da atividade de origem hello está disponível como um objeto. |
| Sequência |atividade de destino Olá é executado apenas uma vez.  Ele recebe uma matriz de objetos da atividade de origem hello.  Saída da atividade de origem hello está disponível como uma matriz de objetos. |

### <a name="starting-activity"></a>Atividade de início
Um runbook gráfico será iniciado com todas as atividades que não têm um link de entrada.  Isso geralmente será apenas uma atividade que deverá atuar como Olá Iniciar atividade de runbook hello.  Se várias atividades não tiverem um link de entrada, Olá runbook será iniciado por executá-los em paralelo.  Em seguida, ele seguirá Olá links toorun outras atividades cada conclusão.

### <a name="conditions"></a>Condições
Quando você especificar uma condição em um link, atividade de destino Olá é executada somente se a condição de saudação tootrue seja resolvida.  Normalmente, você usará uma variável $ActivityOutput em uma saída de hello tooretrieve condição da atividade de origem hello.  

Para um link de pipeline, você especificar uma condição para um único objeto e condição Olá é avaliada para cada objeto de saída pela atividade de origem hello.  atividade de destino Hello, em seguida, é executada para cada objeto que satisfaça a condição de saudação.  Por exemplo, com uma atividade de origem de Get-AzureRmVm, Olá sintaxe a seguir pode ser usado para um tooretrieve de link de pipeline condicional somente Olá de máquinas virtuais no grupo de recursos chamado *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Para um link de sequência, condição de saudação é avaliada apenas uma vez como uma única matriz é retornada que contém a saída de todos os objetos da atividade de origem hello.  Por isso, um link de sequência não pode ser usado para filtragem como um link de pipeline, mas simplesmente determinará ou não a próxima atividade de saudação é executada. Considere, por exemplo, Olá após o conjunto de atividades em nosso runbook iniciar VM.<br> ![Link Condicional com Sequências](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Há três links de sequência diferente que está verificando valores foram fornecidos parâmetros de entrada de runbook do tootwo que representa o nome da VM e o nome de grupo de recursos no toodetermine ordem que é Olá ação apropriada tootake - iniciar uma única VM, inicie todas as máquinas virtuais em Olá grupo de recurso, ou todas as VMs em uma assinatura.  Link de sequência Olá entre tooAzure conectar e obter única VM, aqui está a lógica da condição hello:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Quando você usa um link condicional, Olá dados disponíveis de atividades de tooother de atividade de origem de saudação na filial serão filtrados pela condição hello.  Se uma atividade for links de toomultiple fonte Olá, em seguida, Olá tooactivities disponíveis em cada ramificação dependerá condição Olá no link Olá toothat ramificação de conexão de dados.

Por exemplo, Olá **AzureRmVm início** atividade no runbook de saudação abaixo inicia todas as máquinas virtuais.  Ela tem dois links condicionais.  link de condicional primeiro Olá usa a expressão de saudação *$ActivityOutput ['Início-AzureRmVM']. IsSuccessStatusCode - eq $true* toofilter se Olá AzureRmVm Iniciar atividade concluída com êxito.  Olá segundo usa a expressão de saudação *$ActivityOutput ['Início-AzureRmVM']. IsSuccessStatusCode - ne $true* toofilter se atividade Olá AzureRmVm início falhou toostart Olá VM.  

![Exemplo de link condicional](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Qualquer atividade que segue o link primeiro hello e usa hello atividade saída de Get-AzureVM só receberá máquinas virtuais Olá foram iniciados em tempo de saudação Get-AzureVM foi executado.  Qualquer atividade que segue o link segundo Olá só receberá Olá Olá VMs que foram interrompidos em tempo de saudação Get-AzureVM foi executado.  Qualquer atividade seguindo o link de terceiro Olá obterá todas as máquinas virtuais, independentemente do estado de execução.

### <a name="junctions"></a>Junções
Uma junção é uma atividade especial que esperará até que todas as ramificações de entrada sejam concluídas.  Isso permite toorun várias atividades em paralelo e garantir que todas sejam concluídas antes de continuar.

Embora uma junção possa ter um número ilimitado de links de entrada, apenas um desses links pode ser um pipeline.  número de saudação de links de sequência de entrada não é restrito.  Poderá ser toocreate junção de saudação com vários links de pipeline de entrada e salvar o runbook hello, mas falhará quando ele é executado.

exemplo Hello abaixo é parte de um runbook que inicia um conjunto de máquinas virtuais, enquanto simultaneamente baixar patches toobe aplicadas toothose máquinas.  Uma junção é usada tooensure que ambos os processos sejam concluídos antes da continuação da saudação runbook.

![Junção](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Ciclos
Um ciclo é quando uma atividade de destino vincula novamente tooits atividade de atividade ou tooanother que eventualmente links faça tooits fonte da fonte.  No momento, os ciclos não são permitidos na criação de gráficos.  Se seu runbook tiver um ciclo, ele será salvo corretamente, mas receberá um erro quando for executado.

![Ciclo](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Compartilhando dados entre atividades
Todos os dados de saída por uma atividade com um link de saída são gravados toohello *databus* Olá runbook.  Qualquer atividade no runbook Olá pode usar dados nos valores de parâmetro hello databus toopopulate ou incluir no código de script.  Uma atividade pode acessar a saída de saudação de qualquer atividade anterior no fluxo de trabalho de saudação.     

Como os dados de saudação são gravados toohello databus dependem Olá tipo de link na atividade de saudação.  Para uma **pipeline**, dados de saudação são a saída como objetos de múltiplos.  Para uma **sequência** vincular, hello saída dos dados é como uma matriz.  Se houver apenas um valor, ele será gerado como uma matriz de elemento único.

Você pode acessar dados em Olá databus usando um destes dois métodos.  Primeiro, está usando um **atividade saída** toopopulate da fonte de dados de um parâmetro de outra atividade.  Se a saída de hello é um objeto, você pode especificar uma única propriedade.

![Saída de Atividade](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

Você também pode recuperar a saída de saudação de uma atividade em um **PowerShell expressão** fonte de dados ou de um **Script de fluxo de trabalho** atividade com uma variável ActivityOutput.  Se a saída de hello é um objeto, você pode especificar uma única propriedade.  Variáveis de ActivityOutput usam Olá sintaxe a seguir.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Pontos de verificação
Você pode definir [pontos de verificação](automation-powershell-workflow.md#checkpoints) em um runbook do Fluxo de Trabalho do PowerShell Gráfico selecionando *Runbook do ponto de verificação* em qualquer atividade.  Isso faz com que um toobe de ponto de verificação definida depois hello atividade é executada.

![Ponto de verificação](media/automation-graphical-authoring-intro/set-checkpoint.png)

Os pontos de verificação são habilitados somente nos runbooks do Fluxo de Trabalho do PowerShell Gráficos; eles não estão disponíveis nos runbooks Gráficos.  Se Olá runbook usa cmdlets do Azure, você deve seguir qualquer atividade de ponto de verificação com uma AzureRMAccount adicionar no caso de Olá runbook está suspenso e reinicia desse ponto de verificação no outro trabalho. 

## <a name="authenticating-tooazure-resources"></a>Recursos de autenticação tooAzure
Requer autenticação tooAzure runbooks na automação do Azure que gerenciar recursos do Azure.  Olá [conta executar como](automation-offering-get-started.md#creating-an-automation-account) (também chamado tooas uma entidade de serviço) é saudação padrão método tooaccess recursos do Gerenciador de recursos do Azure em sua assinatura com runbooks de automação.  Você pode adicionar esse runbook gráfico de tooa funcionalidade adicionando Olá **AzureRunAsConnection** ativo de Conexão, o que está usando Olá PowerShell [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet e [Adicionar AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello tela. Isso é ilustrado no exemplo a seguir de saudação.<br>![Atividades de Autenticação Executar Como](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hello atividade obter executar como Conexão (por exemplo, Get-AutomationConnection), é configurado com uma fonte de dados de valor constante denominada AzureRunAsConnection.<br>![Configuração da Conexão Executar Como](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
próxima atividade de Hello, Add-AzureRmAccount adiciona Olá autenticado a conta executar como para uso no runbook hello.<br>
![Conjunto de parâmetros Add-AzureRmAccount](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Para parâmetros de saudação **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, e **TENANTID** você precisará toospecify Olá nome da propriedade Olá para o caminho de campo Olá porque atividade de Hello gera um objeto com várias propriedades.  Caso contrário, quando você executar o runbook hello, ele falhará tooauthenticate tentativa.  Este é o que você precisa em um mínimo tooauthenticate seu runbook com hello conta executar como.

toomaintain com versões anteriores a compatibilidade para assinantes que tiver criado uma automação de conta usando um [conta de usuário do AD do Azure](automation-create-aduser-account.md) toomanage implantação clássica do Azure ou para recursos do Gerenciador de recursos do Azure, Olá tooauthenticate de método é o cmdlet Add-AzureAccount de saudação com um [ativo de credencial](automation-credentials.md) que representa um usuário do Active Directory com acesso toohello conta do Azure.

Você pode adicionar esse runbook gráfico de tooa funcionalidade adicionando uma tela de toohello do ativo de credencial seguida por uma atividade de Add-AzureAccount.  Adicionar-AzureAccount usa a atividade de credencial de saudação para sua entrada.  Isso é ilustrado no exemplo a seguir de saudação.

![Atividades de autenticação](media/automation-graphical-authoring-intro/authentication-activities.png)

Você tem tooauthenticate no início de saudação do runbook hello e depois de cada ponto de verificação.  Isso significa adicionar uma atividade de adição Add-AzureAccount depois de qualquer atividade Checkpoint-Workflow. Você não precisa de uma credencial de adição Olá a atividade desde que você pode usar o mesmo 

![Saída de Atividade](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Entrada e saída de runbook
### <a name="runbook-input"></a>Entrada do Runbook
Um runbook pode exigir entrada do usuário quando eles são iniciados Olá runbook por meio de saudação portal do Azure ou de outro runbook se Olá atual é usado como um filho.
Por exemplo, se você tiver um runbook que cria uma máquina virtual, talvez seja necessário informações tooprovide como nome de saudação da máquina virtual de saudação e outras propriedades toda vez que iniciar o runbook hello.  

Você aceita a entrada para um runbook definindo um ou mais parâmetros de entrada.  Você pode fornecer valores para esses parâmetros de que cada runbook de saudação do tempo é iniciado.  Quando você inicia um runbook com hello portal do Azure, ele solicitará que você tooprovide valores para Olá de Olá do runbook parâmetros de entrada.

Você pode acessar os parâmetros de entrada para um runbook clicando Olá **de entrada e saída** botão na barra de ferramentas do runbook hello.  

![Entrada e saída de runbook](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Isso abre o hello **de entrada e saída** controle onde você pode editar um parâmetro de entrada existente ou criar um novo clicando em **Adicionar entrada**. 

![Adicionar entrada](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Cada parâmetro de entrada é definido pelas propriedades Olá Olá a tabela a seguir.

| Propriedade | Descrição |
|:--- |:--- |
| Nome |nome exclusivo de saudação do parâmetro hello.  Pode conter apenas caracteres alfanuméricos e não pode conter espaços. |
| Descrição |Uma descrição opcional para o parâmetro de entrada hello. |
| Tipo |Tipo de dados esperado para o valor do parâmetro hello.  Olá portal do Azure fornecem um controle apropriado para o tipo de dados Olá para cada parâmetro quando a solicitação de entrada. |
| Obrigatório |Especifica se deve ser fornecido um valor para o parâmetro hello.  Olá runbook não pode ser iniciado se você não fornecer um valor para cada parâmetro obrigatório que não tem um valor padrão definido. |
| Valor Padrão |Especifica o valor que é usado para o parâmetro hello se não for fornecido.  Pode ser Nulo ou um valor específico. |

### <a name="runbook-output"></a>Saída de runbook
Os dados criados por qualquer atividade que não tem uma conexão de saída serão adicionados toohello [saída do runbook Olá](http://msdn.microsoft.com/library/azure/dn879148.aspx).  saída de Hello é salva com o trabalho de runbook hello e é o runbook pai tooa disponíveis quando Olá runbook é usado como um filho.  

## <a name="powershell-expressions"></a>Expressões do PowerShell
Uma das vantagens de saudação do gráfico de criação oferece uma capacidade de saudação toobuild um runbook com o mínimo de conhecimento do PowerShell.  No momento, você precisa tooknow um pouco de PowerShell para popular certos [valores de parâmetro](#activities) e para configuração [vincular condições](#links-and-workflow).  Esta seção fornece uma rápida introdução tooPowerShell expressões para os usuários que podem não estar familiarizados com ele.  Detalhes completos do PowerShell estão disponíveis em [scripts com o Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>Fonte de dados de expressão do PowerShell
Você pode usar uma expressão do PowerShell como um valor de saudação dados fonte toopopulate de um [parâmetro de atividade](#activities) com resultados de saudação de algum código do PowerShell.  Isso pode ser uma única linha de código que executa uma função simples ou várias linhas que realizam alguma lógica complexa.  Nenhuma saída de um comando que não está atribuído tooa variável é o valor do parâmetro de toohello de saída. 

Por exemplo, Olá comando a seguir geraria Olá data atual. 

    Get-Date

Hello comandos a seguir construir uma cadeia de caracteres de saudação data atual e atribuí-la tooa variável.  conteúdo de saudação da variável de saudação, em seguida, é enviado para saída toohello 

    $string = "hello current date is " + (Get-Date)
    $string

Olá comandos a seguir avaliam Olá data atual e retornam uma cadeia de caracteres que indica se Olá dia atual é um fim de semana ou dia da semana. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Saída de Atividade
saída de hello toouse de uma atividade anterior no runbook hello, usar a variável de saudação $ActivityOutput com hello sintaxe a seguir.

    $ActivityOutput['Activity Label'].PropertyName

Por exemplo, você pode ter uma atividade com uma propriedade que requer um nome de saudação de uma máquina virtual caso em que você pode usar o hello expressão a seguir.

    $ActivityOutput['Get-AzureVm'].Name

Se a propriedade Olá Olá objeto de máquina virtual em vez de apenas uma propriedade, em seguida, é necessário retornaria usando o objeto inteiro Olá Olá sintaxe a seguir.

    $ActivityOutput['Get-AzureVm']

Você também pode usar a saída de saudação de uma atividade em uma expressão mais complexa, como a seguir Olá que concatena o nome da máquina virtual toohello texto.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Condições
Use [operadores de comparação](https://technet.microsoft.com/library/hh847759.aspx) toocompare valores ou determinar se um valor corresponde a um padrão especificado.  Uma comparação retorna um valor de $true ou $false.

Por exemplo, a saudação condição a seguir determina se a máquina virtual de saudação de uma atividade denominada *Get-AzureVM* está *interrompido*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

verificações de condição a seguir de saudação se hello mesma máquina virtual está em um estado diferente de *interrompido*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Você pode unir várias condições usando um [operador lógico](https://technet.microsoft.com/library/hh847789.aspx) como **- e** ou **- ou**.  Por exemplo, Olá condição a seguir verifica se hello mesma máquina virtual no exemplo anterior hello está em um estado de *interrompido* ou *parando*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Tabelas de hash
[Tabelas de hash](http://technet.microsoft.com/library/hh847780.aspx) são pares nome/valor que são úteis para retornar um conjunto de valores.  Propriedades de determinadas atividades podem esperar uma tabela de hash em vez de um valor simples.  Você também poderá ver a tabela de hash chamado tooas um dicionário. 

Você pode criar uma tabela de hash com hello sintaxe a seguir.  Uma tabela de hash pode conter qualquer número de entradas, mas cada um é definido por um nome e valor.

    @{ <name> = <value>; [<name> = <value> ] ...}

Por exemplo, hello expressão a seguir cria um toobe da tabela de hash usado na fonte de dados de saudação para um parâmetro de atividade que espera uma tabela de hash com valores para uma pesquisa na internet.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Olá, exemplo a seguir usa a saída de uma atividade chamada *obter Conexão Twitter* toopopulate uma tabela de hash.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md) 
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooknow mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)
* toounderstand como tooauthenticate usando Olá automação executar como conta, consulte [configurar Azure conta executar como](automation-sec-configure-azure-runas-account.md)

