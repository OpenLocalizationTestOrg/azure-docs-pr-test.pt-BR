---
title: "aaaMy primeiro PowerShell runbook na automação do Azure | Microsoft Docs"
description: "Tutorial que orienta você na criação de hello, testes e publicação de um runbook simple do PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "azure powershell, tutorial de script do powershell, automação do powershell"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Meu primeiro runbook do PowerShell

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial orienta você na criação de saudação de um [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) na automação do Azure. Vamos começar com um runbook simple que podemos testar e publicar enquanto explicamos como tootrack Olá status do trabalho de runbook hello. Em seguida, podemos modificar Olá runbook tooactually gerenciar recursos do Azure, nesse caso, iniciando uma máquina virtual do Azure. Por fim, fazemos Olá runbook mais robusta, adicionando parâmetros de runbook.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá a seguir:

* Assinatura do Azure. Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).
* [Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.  Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.
* Uma máquina virtual do Azure. Paramos e iniciamos o computador, portanto, ele não deve ser uma VM de produção.

## <a name="step-1---create-new-runbook"></a>Etapa 1: criar o novo runbook
Vamos começar criando um runbook simples que gera o texto de saudação *Hello World*.

1. No portal do Azure de Olá, abra sua conta de automação.  
   página de conta de automação Olá fornece uma exibição rápida dos recursos de saudação nesta conta. Você já deve ter alguns ativos. A maioria delas são módulos de saudação que são incluídos automaticamente em uma nova conta de automação. Você também deve ter o ativo de credencial de saudação que é mencionado na Olá [pré-requisitos](#prerequisites).
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Criar um novo runbook clicando Olá **adicionar um runbook** botão e, em seguida, **criar um novo runbook**.
4. Nomeie Olá runbook Olá *MyFirstRunbook PowerShell*.
5. Nesse caso, vamos toocreate um [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) escolha **Powershell** para **tipo de Runbook**.<br><br> ![Runbook Type](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Clique em **criar** toocreate Olá runbook e editor textual Olá aberto.

## <a name="step-2---add-code-toohello-runbook"></a>Etapa 2: adicionar código toohello runbook
Você pode o código de tipo diretamente no runbook hello, ou você pode selecionar cmdlets, runbooks e ativos de saudação controle da biblioteca e eles adicionou toohello runbook com os parâmetros relacionados. Para este passo a passo, digite diretamente no runbook hello.

1. Nosso runbook está vazio no momento. Digite *Write-Output "Olá mundo."*.<br><br> ![Olá mundo](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Salvar o runbook Olá clicando **salvar**.<br><br> ![Botão Salvar](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Etapa 3 - teste Olá runbook
Antes de publicamos Olá runbook toomake-lo disponível em produção, queremos tootest-toomake-se de que ele funcione corretamente. Quando você testa um runbook, executa sua versão de **Rascunho** e vê sua saída interativamente.

1. Clique em **painel teste** tooopen painel de teste de saudação.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Clique em **iniciar** toostart teste de saudação. Isso deve ser a opção de Olá só está habilitada.
3. Um [trabalho de runbook](automation-runbook-execution.md) é criado e seu status é exibido.  
   status do trabalho Olá começa como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toocome de nuvem disponível. Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.  
4. Quando o trabalho de runbook Olá for concluído, a saída é exibida. Em nosso caso, deveremos ver *Olá mundo*.<br><br> ![Saída do painel de teste](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Feche a tela de toohello Olá teste painel tooreturn.

## <a name="step-4---publish-and-start-hello-runbook"></a>Etapa 4: publicar e iniciar o runbook Olá
Olá runbook que criamos ainda está em modo de rascunho. Precisamos toopublish antes de fazermos em produção.  Quando você publicar um runbook, você substituir a versão publicada existente de saudação com versão de rascunho de saudação.  Em nosso caso, não temos uma versão publicada ainda porque que acabamos de criar o runbook hello.

1. Clique em **publicar** toopublish Olá runbook e, em seguida, **Sim** quando solicitado.<br><br> ![Botão Publicar](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Se você rolar tooview esquerdo Olá runbook no hello **Runbooks** painel agora, ele mostrará um **Status criação** de **publicado**.
3. Rolagem toohello back tooview direita Olá painel **MyFirstRunbook PowerShell**.  
   Hello opções na parte superior da saudação nos permitem toostart Olá runbook, exibir hello runbook, agendá-la toostart em algum momento futuro de saudação ou criar um [webhook](automation-webhooks.md) para que ele possa ser iniciado por meio de uma chamada HTTP.
4. Podemos ser toostart Olá runbook, clique em **iniciar** e, em seguida, clique em **Okey** quando abre a folha de iniciar Runbook hello.<br><br> ![Botão Iniciar](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Um painel de trabalho é aberto para o trabalho de runbook Olá que criamos. É possível fechar esse painel, mas nesse caso é deixá-lo aberto para que possamos ver o progresso do trabalho hello.
6. status do trabalho Olá é mostrada na **resumo do trabalho** e correspondências Olá status que vimos Quando testamos Olá runbook.<br><br> ![Resumo do trabalho](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Uma vez Olá runbook status mostra *concluído*, clique em **saída**. Painel de saída de saudação é aberto e podemos ver nossa *Hello World*.<br><br> ![Saída do trabalho](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Painel de saída Olá fechar.
9. Clique em **todos os Logs** tooopen Olá fluxos painel trabalho de runbook hello. Veremos apenas *Hello World* na saída de hello fluxo, mas isso pode mostrar outros fluxos de um trabalho de runbook, como detalhado e de erro se o runbook Olá grava toothem.<br><br> ![Todos os Logs](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Feche o painel de fluxos de saudação e Olá trabalho tooreturn toohello MyFirstRunbook PowerShell um painel.
11. Clique em **trabalhos** tooopen painel de trabalhos Olá para este runbook. Lista todos os trabalhos de saudação criados por este runbook. Um trabalho listado como somente executamos trabalho Olá uma vez só deverá ser exibida.<br><br> ![Lista de trabalhos](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. Você pode clicar neste trabalho tooopen Olá mesmo painel de trabalho que são exibidos quando é iniciado Olá runbook. Isso permite que você toogo Voltar no tempo e exibir detalhes de saudação de qualquer trabalho que foi criado para um determinado runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Etapa 5: adicionar autenticação toomanage recursos do Azure
Testamos e publicamos nosso runbook, mas até o momento ele não faz nada útil. Queremos toohave-gerenciar recursos do Azure. Ele não será capaz de toodo, embora a menos que temos-autenticar usando credenciais Olá chamado hello tooin [pré-requisitos](#prerequisites). Podemos fazer isso com hello **AzureRmAccount adicionar** cmdlet.

1. Editor de textual Olá aberta clicando **editar** no painel de saudação MyFirstRunbook PowerShell.<br><br> ![Editar runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Não é necessário Olá **Write-Output** mais de linha, portanto vá em frente e excluí-lo.
3. Digite ou copie e cole Olá código que manipula a autenticação de saudação à sua conta de automação executar como a seguir:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Clique em **painel teste** para que podemos testar Olá runbook.
5. Clique em **iniciar** toostart teste de saudação. Quando for concluída, você deve receber toohello semelhante de saída a seguir, exibindo informações básicas de sua conta. Isso confirma que Olá credencial é válida.<br><br> ![Autenticar](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Etapa 6: adicionar código toostart uma máquina virtual
Agora que nossa runbook está se autenticando tooour assinatura do Azure, podemos gerenciar recursos. Vamos adicionar um comando toostart uma máquina virtual. Você pode escolher qualquer máquina virtual na sua assinatura do Azure e agora vamos codificar esse nome no runbook hello.

1. Depois de *adicionar AzureRmAccount*, tipo *AzureRmVM Start-nome 'VMName' - ResourceGroupName 'NameofResourceGroup'* fornecendo o nome de saudação e nome do grupo de recursos do hello toostart de máquina virtual.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Salvar o runbook hello e, em seguida, clique em **painel teste** para que podemos testar.
3. Clique em **iniciar** toostart teste de saudação. Quando for concluída, verifique que a máquina virtual Olá foi iniciada.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Etapa 7: adicionar um runbook de toohello do parâmetro de entrada
Nosso runbook inicia Olá virtual da máquina que possamos codificado no runbook hello, mas pode ser mais útil se especificamos máquina virtual de saudação quando Olá runbook for iniciado. Vamos agora adicionar parâmetros de entrada toohello runbook tooprovide essa funcionalidade.

1. Adicionar parâmetros para *VMName* e *ResourceGroupName* toohello runbook e usar essas variáveis com hello **AzureRmVM início** cmdlet como no exemplo hello abaixo.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Salvar o runbook hello e abrir o painel de teste de saudação. Agora fornecem valores para Olá duas variáveis de entrada que são usadas no teste de saudação.
3. Painel de teste Olá fechar.
4. Clique em **publicar** toopublish Olá nova versão de runbook hello.
5. Pare a máquina de virtual Olá iniciado na etapa anterior hello.
6. Clique em **iniciar** toostart Olá runbook. Tipo de saudação **VMName** e **ResourceGroupName** para a máquina virtual de saudação que vai toostart.<br><br> ![Passar parâmetro](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Quando Olá runbook for concluída, verifique que a máquina virtual Olá foi iniciada.

## <a name="differences-from-powershell-workflow"></a>Diferenças do fluxo de trabalho do PowerShell
Runbooks do PowerShell têm Olá mesmo ciclo de vida, recursos e gerenciamento como runbooks de fluxo de trabalho do PowerShell, mas há algumas diferenças e limitações:

1. Runbooks do PowerShell execute tooPowerShell rápida em comparação com o fluxo de trabalho runbooks que elas não tenham a etapa de compilação.
2. Runbooks de fluxo de trabalho do PowerShell oferece suporte a pontos de verificação, usando os pontos de verificação, runbooks do fluxo de trabalho do PowerShell pode retomar de qualquer ponto no runbook Olá enquanto runbooks do PowerShell pode retomar somente do início da saudação.
3. Os runbooks do fluxo de trabalho do PowerShell dão suporte à execução em paralelo e serial, enquanto os runbooks do PowerShell só podem executar comandos de forma serial.
4. Em um runbook do fluxo de trabalho do PowerShell, uma atividade, um comando ou um bloco de script pode ter seu próprio espaço de execução, enquanto em um runbook do PowerShell, tudo em um script é executado em um único espaço de execução. Também há algumas [diferenças sintáticas](https://technet.microsoft.com/magazine/dn151046.aspx) entre um runbook nativo do PowerShell e um runbook do Fluxo de Trabalho do PowerShell.

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* tooknow mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)
* Para saber mais sobre o recurso de suporte de script do PowerShell, veja [Native PowerShell script support in Azure Automation (Suporte a scripts nativos do PowerShell na Automação do Azure)](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

