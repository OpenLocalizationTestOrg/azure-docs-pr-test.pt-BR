---
title: "aaaMy primeiro fluxo de trabalho do PowerShell runbook na automação do Azure | Microsoft Docs"
description: "Tutorial que orienta você na criação de hello, testes e publicação de um runbook de texto simples usando o fluxo de trabalho do PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: fluxo de trabalho do powershell, exemplos de fluxo de trabalho do powershell, fluxo de trabalho powershell
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b5a34d363ef4865878f3f68119833367b5280f83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Meu primeiro runbook de Fluxo de Trabalho do PowerShell

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial orienta você na criação de saudação de um [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) na automação do Azure. Vamos começar com um runbook simple que podemos testar e publicar ao explicar como tootrack Olá status do trabalho de runbook hello. Em seguida, podemos modificar Olá runbook tooactually gerenciar recursos do Azure, nesse caso, iniciando uma máquina virtual do Azure. Por fim, fazemos Olá runbook mais robusta, adicionando parâmetros de runbook.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisará Olá a seguir:

* Assinatura do Azure. Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).
* [Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.  Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.
* Uma máquina virtual do Azure. Paramos e iniciamos o computador, portanto, ele não deve ser uma VM de produção.

## <a name="step-1---create-new-runbook"></a>Etapa 1: criar o novo runbook
Vamos começar criando um runbook simples que gera o texto de saudação *Hello World*.

1. No portal do Azure de Olá, abra sua conta de automação.  
   página de conta de automação Olá fornece uma exibição rápida dos recursos de saudação nesta conta. Você já deve ter alguns ativos. A maioria delas são módulos de saudação que são incluídos automaticamente em uma nova conta de automação. Você também deve ter o ativo de credencial de saudação que é mencionado na Olá [pré-requisitos](#prerequisites).
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.<br><br> ![Controle de runbooks](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Criar um novo runbook clicando no hello **adicionar um runbook** botão e, em seguida, **criar um novo runbook**.
4. Nomeie Olá runbook Olá *MyFirstRunbook fluxo de trabalho*.
5. Nesse caso, vamos toocreate um [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) escolha **fluxo de trabalho do Powershell** para **tipo de Runbook**.<br><br> ![Novo runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Clique em **criar** toocreate Olá runbook e editor textual Olá aberto.

## <a name="step-2---add-code-toohello-runbook"></a>Etapa 2: adicionar código toohello runbook
Você pode o código de tipo diretamente no runbook hello, ou você pode selecionar cmdlets, runbooks e ativos de saudação controle da biblioteca e eles adicionou toohello runbook com os parâmetros relacionados. Para este passo a passo, estamos digitará diretamente no runbook Olá.

1. Nosso runbook está vazia com apenas Olá necessário *fluxo de trabalho* palavra-chave, nome de saudação de nossos runbook e chaves de saudação que serão o fluxo de trabalho inteiro Olá encase.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Digite *Write-Output "Hello World."* entre chaves hello.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Salvar o runbook Olá clicando **salvar**.<br><br> ![Salvar runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-hello-runbook"></a>Etapa 3 - teste Olá runbook
Antes de publicamos Olá runbook toomake-lo disponível em produção, queremos tootest-toomake-se de que ele funcione corretamente. Quando você testa um runbook, executa sua versão de **Rascunho** e vê sua saída interativamente.

1. Clique em **painel teste** tooopen painel de teste de saudação.<br><br> ![Painel de teste](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Clique em **iniciar** toostart teste de saudação. Isso deve ser a opção de Olá só está habilitada.
3. Um [trabalho de runbook](automation-runbook-execution.md) é criado e seu status é exibido.  
   status do trabalho Olá será iniciado como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toocome de nuvem disponível. Em seguida, ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.  
4. Quando o trabalho de runbook Olá for concluído, a saída é exibida. Em nosso caso, deveremos ver *Olá mundo*.<br><br> ![Olá mundo](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Feche a tela de toohello Olá teste painel tooreturn.

## <a name="step-4---publish-and-start-hello-runbook"></a>Etapa 4: publicar e iniciar o runbook Olá
Olá runbook que acabou de criar ainda está em modo de rascunho. Precisamos toopublish antes de fazermos em produção. Quando você publicar um runbook, você substituir a versão publicada existente de saudação com versão de rascunho de saudação. Em nosso caso, não temos uma versão publicada ainda porque que acabamos de criar o runbook hello.

1. Clique em **publicar** toopublish Olá runbook e, em seguida, **Sim** quando solicitado.<br><br> ![Publicar](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Se você rolar tooview esquerdo Olá runbook no hello **Runbooks** painel agora, ele mostrará um **Status criação** de **publicado**.
3. Rolagem toohello back tooview direita Olá painel **MyFirstRunbook fluxo de trabalho**.  
   Olá opções na parte superior da saudação nos permitem toostart Olá runbook, agendá-la toostart em algum momento futuro de saudação ou criar um [webhook](automation-webhooks.md) para que ele possa ser iniciado por meio de uma chamada HTTP.
4. Queremos apenas toostart Olá runbook clique em **iniciar** e **Sim** quando solicitado.<br><br> ![Iniciar runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Um painel de trabalho é aberto para o trabalho de runbook Olá que acabou de criar. É possível fechar esse painel, mas nesse caso é deixá-lo aberto para que possamos ver o progresso do trabalho hello.
6. status do trabalho Olá é mostrada na **resumo do trabalho** e correspondências Olá status que vimos Quando testamos Olá runbook.<br><br> ![Resumo do trabalho](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Uma vez Olá runbook status mostra *concluído*, clique em **saída**. Painel de saída de saudação é aberto e podemos ver nossa *Hello World*.<br><br> ![Resumo do trabalho](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Painel de saída Olá fechar.
9. Clique em **todos os Logs** tooopen Olá fluxos painel trabalho de runbook hello. Veremos apenas *Hello World* na saída de hello fluxo, mas isso pode mostrar outros fluxos de um trabalho de runbook, como detalhado e de erro se o runbook Olá grava toothem.<br><br> ![Resumo do trabalho](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Feche o painel de fluxos de saudação e Olá trabalho tooreturn toohello MyFirstRunbook um painel.
11. Clique em **trabalhos** tooopen painel de trabalhos Olá para este runbook. Lista todos os trabalhos de saudação criados por este runbook. Um trabalho listado como somente executamos trabalho Olá uma vez só deverá ser exibida.<br><br> ![Trabalhos](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. Você pode clicar em Olá de tooopen esse trabalho que mesmo painel de trabalho que são exibidos quando é iniciado Olá runbook. Isso permite que você toogo Voltar no tempo e exibir detalhes de saudação de qualquer trabalho que foi criado para um determinado runbook.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Etapa 5: adicionar autenticação toomanage recursos do Azure
Testamos e publicamos nosso runbook, mas até o momento ele não faz nada útil. Queremos toohave-gerenciar recursos do Azure. Ele não será capaz de toodo, embora a menos que temos-autenticar usando credenciais Olá chamado hello tooin [pré-requisitos](#prerequisites). Podemos fazer isso com hello **AzureRMAccount adicionar** cmdlet.

1. Editor de textual Olá aberta clicando **editar** no painel de saudação MyFirstRunbook fluxo de trabalho.<br><br> ![Editar runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Não é necessário Olá **Write-Output** mais de linha, portanto vá em frente e excluí-lo.
3. Posicione o cursor de saudação em uma linha em branco entre chaves hello.
4. Digite ou copie e cole Olá código que tratará autenticação Olá com sua conta de automação executar como a seguir:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Clique em **painel teste** para que podemos testar Olá runbook.
6. Clique em **iniciar** toostart teste de saudação. Quando for concluída, você deve receber toohello semelhante de saída a seguir, exibindo informações básicas de sua conta. Isso confirma que Olá credencial é válida.<br><br> ![Autenticar](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Etapa 6: adicionar código toostart uma máquina virtual
Agora que nossa runbook está se autenticando tooour assinatura do Azure, podemos gerenciar recursos. Vamos adicionar um comando toostart uma máquina virtual. Você pode escolher qualquer máquina virtual na sua assinatura do Azure e agora será codificar nome no runbook hello.

1. Depois de *adicionar AzureRmAccount*, tipo *AzureRmVM Start-nome 'VMName' - ResourceGroupName 'NameofResourceGroup'* fornecendo o nome de saudação e nome do grupo de recursos do hello toostart de máquina virtual.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Salvar o runbook hello e, em seguida, clique em **painel teste** para que podemos testar.
3. Clique em **iniciar** toostart teste de saudação. Quando for concluída, verifique que a máquina virtual Olá foi iniciada.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Etapa 7: adicionar um runbook de toohello do parâmetro de entrada
Nosso runbook inicia Olá virtual da máquina que possamos codificado no runbook hello, mas pode ser mais útil se seria possível especificar a máquina virtual de saudação quando Olá runbook for iniciado. Vamos agora adicionar parâmetros de entrada toohello runbook tooprovide essa funcionalidade.

1. Adicionar parâmetros para *VMName* e *ResourceGroupName* toohello runbook e usar essas variáveis com hello **AzureRmVM início** cmdlet como no exemplo hello abaixo.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Salvar o runbook hello e abrir o painel de teste de saudação. Observe que agora você pode fornecer valores para Olá duas variáveis de entrada que serão usados no teste de saudação.
3. Painel de teste Olá fechar.
4. Clique em **publicar** toopublish Olá nova versão de runbook hello.
5. Pare a máquina de virtual Olá iniciado na etapa anterior hello.
6. Clique em **iniciar** toostart Olá runbook. Tipo de saudação **VMName** e **ResourceGroupName** para a máquina virtual de saudação que vai toostart.<br><br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Quando Olá runbook for concluída, verifique que a máquina virtual Olá foi iniciada.  

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)
* tooget iniciado com runbooks do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md)
* toolearn mais sobre os tipos de runbook, suas vantagens e limitações, consulte [tipos de runbook de automação do Azure](automation-runbook-types.md)
* Para saber mais sobre o recurso de suporte de script do PowerShell, veja [Native PowerShell script support in Azure Automation (Suporte a scripts nativos do PowerShell na Automação do Azure)](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
