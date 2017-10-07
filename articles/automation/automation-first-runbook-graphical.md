---
title: "runbook de gráfico primeiro aaaMy na automação do Azure | Microsoft Docs"
description: "Tutorial que orienta você na criação de hello, testes e publicação de um runbook gráfico simple."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, modelo de runbook, automação de runbook, runbook do azure"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>O meu primeiro runbook gráfico

> [!div class="op_single_selector"]
> * [Gráfico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Fluxo de Trabalho do PowerShell](automation-first-runbook-textual.md)
> 
> 

Este tutorial orienta você na criação de saudação de um [runbook gráfico](automation-runbook-types.md#graphical-runbooks) na automação do Azure.  Vamos começar com um runbook simple que testa e publica enquanto explicamos como tootrack Olá status do trabalho de runbook hello.  Em seguida, podemos modificar Olá runbook tooactually gerenciar recursos do Azure, nesse caso, iniciando uma máquina virtual do Azure.  Em seguida, podemos concluir o tutorial de saudação fazendo runbook hello mais robusta, adicionando parâmetros de runbook e links condicionais.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisará Olá a seguir.

* Assinatura do Azure.  Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).
* [Conta de automação do Azure](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.  Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.
* Uma máquina virtual do Azure.  Vamos parar e iniciar esse computador, portanto ele não deve ser de produção.

## <a name="step-1---create-runbook"></a>Etapa 1: criar o runbook
Vamos começar criando um runbook simples que gera o texto de saudação *Hello World*.

1. No portal do Azure de Olá, abra sua conta de automação.  
   página de conta de automação Olá fornece uma exibição rápida dos recursos de saudação nesta conta.  Você já deve ter alguns ativos.  A maioria delas são módulos de saudação que são incluídos automaticamente em uma nova conta de automação.  Você também deve ter o ativo de credencial de saudação que é mencionado na Olá [pré-requisitos](#prerequisites).
2. Clique em Olá **Runbooks** bloco tooopen Olá lista de runbooks.<br> ![Controle de runbooks](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. Criar um novo runbook clicando no hello **adicionar um runbook** botão e, em seguida, **criar um novo runbook**.
4. Nomeie Olá runbook Olá *MyFirstRunbook gráfica*.
5. Nesse caso, vamos toocreate um [runbook gráfico](automation-graphical-authoring-intro.md) escolha **gráfico** para **tipo de Runbook**.<br> ![Novo runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. Clique em **criar** toocreate Olá runbook e editor gráfico Olá aberto.

## <a name="step-2---add-activities-toohello-runbook"></a>Etapa 2: adicionar atividades toohello runbook
saudação de controle de biblioteca no lado esquerdo de saudação do editor de saudação permite tooselect atividades tooadd tooyour runbook.  Vamos tooadd um **Write-Output** cmdlet toooutput texto de saudação runbook.

1. Na Olá controle de biblioteca, clique na caixa de texto de pesquisa hello e digite **Write-Output**.  resultados da pesquisa Olá serão exibidos abaixo. <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. Role para baixo toohello inferior da lista de saudação.  É possível que o botão direito do mouse **Write-Output** e selecione **adicionar toocanvas** ou clique Olá reticências próximo toohello cmdlet e, em seguida, selecione **adicionar toocanvas**.
3. Clique em Olá **Write-Output** atividade na tela hello.  Isso abre a folha de controle de configuração hello, que permite que você tooconfigure atividade de saudação.
4. Olá **rótulo** padrões toohello nome do cmdlet hello, mas é possível alterar toosomething mais amigável. Alterá-la muito*toooutput gravar Hello World*.
5. Clique em **parâmetros** tooprovide valores para parâmetros do cmdlet hello.  
   Alguns cmdlets têm vários conjuntos de parâmetros, e você precisa tooselect que é um toouse. Nesse caso, **Write-Output** tem apenas um conjunto de parâmetros, portanto, você não precisa tooselect um. <br> ![Propriedades de Write-Output](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. Selecione Olá **InputObject** parâmetro.  Isso é o parâmetro hello onde podemos especificar o fluxo de saída do hello texto toosend toohello.
7. Em Olá **fonte de dados** lista suspensa, selecione **PowerShell expressão**.  Olá **fonte de dados** suspensa fornece fontes diferentes que você use toopopulate um valor de parâmetro.  
   Você pode usar a saída dessas fontes como outra atividade, um ativo de Automação ou uma expressão do PowerShell.  Nesse caso, queremos apenas texto de saudação toooutput *Hello World*. Podemos usar uma expressão do PowerShell e especificar uma cadeia de caracteres.
8. Em Olá **expressão** , digite *"Hello World"* e, em seguida, clique em **Okey** tela de toohello tooreturn duas vezes.<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. Salvar o runbook Olá clicando **salvar**.<br> ![Salvar runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>Etapa 3 - teste Olá runbook
Antes de publicamos Olá runbook toomake-lo disponível em produção, queremos tootest-toomake-se de que ele funcione corretamente.  Quando você testa um runbook, executa sua versão de **Rascunho** e vê sua saída interativamente.

1. Clique em **painel teste** tooopen folha de teste de saudação.<br> ![Painel de teste](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. Clique em **iniciar** toostart teste de saudação.  Isso deve ser a opção de Olá só está habilitada.
3. Um [trabalho de runbook](automation-runbook-execution.md) é criado e seu status exibidos no painel de saudação.  
   status do trabalho Olá começa como *na fila* indicando que ele está aguardando um trabalho de runbook no hello toobecome de nuvem disponível.  Ele move muito*iniciando* quando um trabalhador declarações trabalho Olá e, em seguida, *executando* quando Olá runbook realmente começa a ser executado.  
4. Quando o trabalho de runbook Olá for concluído, a saída é exibida. Em nosso caso, deveremos ver *Olá mundo*.<br> ![Olá mundo](media/automation-first-runbook-graphical/runbook-test-results.png)
5. Feche a tela do hello teste folha tooreturn toohello.

## <a name="step-4---publish-and-start-hello-runbook"></a>Etapa 4: publicar e iniciar o runbook Olá
Olá runbook que criamos ainda está em modo de rascunho. Precisamos toopublish antes de fazermos em produção.  Quando você publicar um runbook, você substituir a versão publicada existente de saudação com versão de rascunho de saudação.  Em nosso caso, não temos uma versão publicada ainda porque que acabamos de criar o runbook hello.

1. Clique em **publicar** toopublish Olá runbook e, em seguida, **Sim** quando solicitado.<br> ![Publicar](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. Se você rolar tooview esquerdo Olá runbook no hello **Runbooks** folha, ele mostra um **Status criação** de **publicado**.
3. Folha de saudação do rolagem toohello back tooview direita para **MyFirstRunbook**.  
   Olá opções na parte superior da saudação nos permitem toostart Olá runbook, agendá-la toostart em algum momento futuro de saudação ou criar um [webhook](automation-webhooks.md) para que ele possa ser iniciado por meio de uma chamada HTTP.
4. Queremos apenas toostart Olá runbook clique em **iniciar** e **Sim** quando solicitado.<br> ![Iniciar runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. Uma folha de trabalho é aberta para o trabalho de runbook Olá que criamos.  É possível fechar esta folha, mas nesse caso é deixá-lo aberto para que possamos ver o progresso do trabalho hello.
6. status do trabalho Olá é mostrada na **resumo do trabalho** e correspondências Olá status que vimos Quando testamos Olá runbook.<br> ![Resumo do trabalho](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. Uma vez Olá runbook status mostra *concluído*, clique em **saída**. Olá **saída** folha é aberta e podemos ver nossa *Hello World* no painel de saudação.<br> ![Resumo do trabalho](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. Folha de saída de hello fechar.
9. Clique em **todos os Logs** tooopen folha de fluxos Olá para o trabalho de runbook hello.  Veremos apenas *Hello World* na saída de hello fluxo, mas isso pode mostrar outros fluxos de um trabalho de runbook, como detalhado e de erro se o runbook Olá grava toothem.<br> ![Resumo do trabalho](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. Feche a folha de todos os Logs de saudação e folha do hello trabalho folha tooreturn toohello MyFirstRunbook.
11. Clique em **trabalhos** tooopen folha de trabalhos Olá para este runbook.  Lista todos os trabalhos de saudação criados por este runbook. Um trabalho listado como somente executamos trabalho Olá uma vez só deverá ser exibida.<br> ![Trabalhos](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. Você pode clicar neste trabalho tooopen Olá mesmo painel de trabalho que são exibidos quando é iniciado Olá runbook.  Isso permite que você toogo Voltar no tempo e exibir detalhes de saudação de qualquer trabalho que foi criado para um determinado runbook.

## <a name="step-5---create-variable-assets"></a>Etapa 5: criar ativos de variável
Testamos e publicamos nosso runbook, mas até o momento ele não faz nada útil. Queremos toohave-gerenciar recursos do Azure.  Antes de configuramos Olá runbook tooauthenticate, podemos criar uma ID de assinatura de saudação toohold variável e referenciá-lo depois que configuramos hello atividade tooauthenticate na etapa 6 abaixo.  Incluindo um contexto de assinatura toohello Referência permite tooeasily trabalho entre várias assinaturas.  Antes de continuar, copie sua ID de assinatura da saudação opção assinaturas desativar o painel de navegação de saudação.  

1. Na folha de contas de automação de saudação, clique em Olá **ativos** lado a lado e hello **ativos** folha é aberta.
2. Na folha de ativos de saudação, clique em Olá **variáveis** lado a lado.
3. Na folha de variáveis de saudação, clique em **adicionar uma variável**.<br>![Variável de Automação](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. Olá nova variável folha, no hello **nome** , digite **AzureSubscriptionId** e em Olá **valor** caixa Insira sua ID de assinatura.  Manter *cadeia de caracteres* para Olá **tipo** e o valor padrão Olá **criptografia**.  
5. Clique em **criar** toocreate variável de saudação.  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>Etapa 6: adicionar autenticação toomanage recursos do Azure
Agora que temos uma variável toohold ID da assinatura, podemos configurar nosso tooauthenticate runbook com hello executar como credenciais que são chamados tooin Olá [pré-requisitos](#prerequisites).  Podemos fazer isso com a adição de conexão de executar como do Azure do hello **ativos** e **AzureRMAccount adicionar** cmdlet toohello tela.  

1. Editor gráfico de saudação aberta clicando **editar** na folha de MyFirstRunbook hello.<br> ![Editar runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. Não precisamos Olá **gravar Hello World toooutput** , então clique duas vezes e selecione **excluir**.
3. No hello controle de biblioteca, expanda **conexões** e adicione **AzureRunAsConnection** toohello tela selecionando **adicionar toocanvas**.
4. Na tela hello, selecione **AzureRunAsConnection** e no painel de controle de configuração hello, digite **obter executar como Conexão** em Olá **rótulo** caixa de texto.  Isso é conexão Olá
5. No controle da biblioteca de Olá, digite **AzureRmAccount adicionar** na caixa de texto de pesquisa de saudação.
6. Adicionar **AzureRmAccount adicionar** toohello tela.<br> ![AzureRMAccount adicionar](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. Passe o mouse sobre **obter executar como Conexão** até que um círculo é exibida na parte inferior da saudação de forma hello. Clique Olá círculo e arraste a seta de saudação muito**AzureRmAccount adicionar**.  seta de saudação que você criou é um *link*.  Olá runbook inicia com **obter executar como Conexão** e, em seguida, execute **AzureRmAccount adicionar**.<br> ![Criar link entre as atividades](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Na tela hello, selecione **adicionar AzureRmAccount** e na configuração de saudação tipo de painel de controle **Login tooAzure** em Olá **rótulo** caixa de texto.
9. Clique em **parâmetros** e folha de configuração de parâmetro de atividade de saudação é exibida.
10. **Adicionar AzureRmAccount** tem vários conjuntos de parâmetros, portanto, precisamos tooselect um antes que possamos fornecer os valores de parâmetro.  Clique em **parâmetro definido** e, em seguida, selecione Olá **ServicePrincipalCertificatewithSubscriptionId** conjunto de parâmetros.
11. Depois de selecionar o conjunto de parâmetros Olá, parâmetros Olá são exibidos na folha de configuração de parâmetro de atividade de saudação.  Clique em **APPLICATIONID**.<br> ![Adicionar parâmetros da conta do Azure RM](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. Na folha de valor de parâmetro hello, selecione **saída de atividade** para Olá **fonte de dados** e selecione **obter executar como Conexão** na lista hello, Olá **campo caminho** caixa de texto tipo **ApplicationId**e, em seguida, clique em **Okey**.  Podemos estiver especificando um nome Olá da propriedade Olá para o caminho de campo Olá porque a atividade de hello gera um objeto com várias propriedades.
13. Clique em **CERTIFICATETHUMBPRINT**e na folha do valor do parâmetro hello, selecione **saída de atividade** para Olá **fonte de dados**.  Selecione **obter executar como Conexão** na lista hello, Olá **caminho de campo** caixa de texto tipo **CertificateThumbprint**e, em seguida, clique em **Okey**.
14. Clique em **SERVICEPRINCIPAL**e na folha do valor do parâmetro hello, selecione **ConstantValue** para Olá **fonte de dados**, clique em opção Olá **True**e, em seguida, clique em **Okey**.
15. Clique em **TENANTID**e na folha do valor do parâmetro hello, selecione **saída de atividade** para Olá **fonte de dados**.  Selecione **obter executar como Conexão** na lista hello, Olá **caminho de campo** caixa de texto tipo **TenantId**e, em seguida, clique em **Okey** duas vezes.  
16. No controle da biblioteca de Olá, digite **AzureRmContext conjunto** na caixa de texto de pesquisa de saudação.
17. Adicionar **AzureRmContext conjunto** toohello tela.
18. Na tela hello, selecione **conjunto AzureRmContext** e na configuração de saudação tipo de painel de controle **especificar Id da assinatura** em Olá **rótulo** caixa de texto.
19. Clique em **parâmetros** e folha de configuração de parâmetro de atividade de saudação é exibida.
20. **Conjunto AzureRmContext** tem vários conjuntos de parâmetros, portanto, precisamos tooselect um antes que possamos fornecer os valores de parâmetro.  Clique em **parâmetro definido** e, em seguida, selecione Olá **SubscriptionId** conjunto de parâmetros.  
21. Depois de selecionar o conjunto de parâmetros Olá, parâmetros Olá são exibidos na folha de configuração de parâmetro de atividade de saudação.  Clique em **SubscriptionID**
22. Na folha de valor de parâmetro hello, selecione **ativo variável** para Olá **fonte de dados** e selecione **AzureSubscriptionId** de saudação lista e clique **Okey**  duas vezes.   
23. Passe o mouse sobre **tooAzure Login** até que um círculo é exibida na parte inferior da saudação de forma hello. Clique Olá círculo e arraste a seta de saudação muito**especificar Id da assinatura**.

O runbook deve parecer com hello neste momento a seguir: <br>![Configuração da autenticação do runbook](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>Etapa 7: Adicionar atividade toostart uma máquina virtual
Aqui, adicionamos uma **AzureRmVM início** atividade toostart uma máquina virtual.  Você pode escolher qualquer máquina virtual na sua assinatura do Azure e para, agora você codifique nome para o cmdlet de saudação.

1. No controle da biblioteca de Olá, digite **AzureRm início** na caixa de texto de pesquisa de saudação.
2. Adicionar **início AzureRmVM** toohello tela e, em seguida, clique e arraste-o sob **especificar Id da assinatura**.
3. Passe o mouse sobre **especificar Id da assinatura** até que um círculo é exibida na parte inferior da saudação de forma hello.  Clique Olá círculo e arraste a seta de saudação muito**AzureRmVM início**.
4. Selecione **Start-AzureRmVM**.  Clique em **parâmetros** e **parâmetro definido** tooview Olá define para **AzureRmVM início**.  Selecione Olá **ResourceGroupNameParameterSetName** conjunto de parâmetros. Observe que há pontos de exclamação ao lado de **ResourceGroupName** e **Name**.  Isso indica que são os parâmetros obrigatórios.  Observe também que ambos esperam valores da cadeia de caracteres.
5. Selecione **Name**.  Selecione **PowerShell expressão** para Olá **fonte de dados** e digite o nome de saudação da máquina virtual de saudação colocada entre aspas duplas que vamos começar com este runbook.  Clique em **OK**.<br>![Valor do Parâmetro Name do Start-AzureRmVM](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. Selecione **ResourceGroupName**. Use **PowerShell expressão** para Olá **fonte de dados** e digite o nome de saudação do grupo de recursos de saudação colocado entre aspas duplas.  Clique em **OK**.<br> ![Parâmetros do Start-AzureRmVM](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. Clique em Painel de teste para que podemos testar Olá runbook.
8. Clique em **iniciar** toostart teste de saudação.  Quando for concluída, verifique que a máquina virtual Olá foi iniciada.

O runbook deve parecer com hello neste momento a seguir: <br>![Configuração da autenticação do runbook](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>Etapa 8 - adicionar parâmetros de entrada adicionais toohello runbook
Nosso runbook inicia máquina virtual de saudação no grupo de recursos de saudação que são especificados no hello **AzureRmVM início** cmdlet.  Nosso runbook pode ser mais útil se seria possível especificar ambos quando Olá runbook for iniciado.  Estamos agora adicionar parâmetros de entrada toohello runbook tooprovide essa funcionalidade.

1. Editor gráfico de saudação aberta clicando **editar** em Olá **MyFirstRunbook** painel.
2. Clique em **de entrada e saída** e **Adicionar entrada** painel de parâmetro de entrada do Runbook Olá tooopen.<br> ![Entrada e Saída de runbook](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. Especifique *VMName* para Olá **nome**.  Manter *cadeia de caracteres* para Olá **tipo**, mas alterar **obrigatório** muito*Sim*.  Clique em **OK**.
4. Criar um parâmetro de entrada segundo obrigatório chamado *ResourceGroupName* e, em seguida, clique em **Okey** tooclose Olá **de entrada e saída** painel.<br> ![Parâmetros de Entrada de Runbook](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. Selecione Olá **início AzureRmVM** atividade e clique **parâmetros**.
6. Saudação de alteração **fonte de dados** para **nome** muito**Runbook entrada** e, em seguida, selecione **VMName**.<br>
7. Saudação de alteração **fonte de dados** para **ResourceGroupName** muito**Runbook entrada** e, em seguida, selecione **ResourceGroupName**.<br> ![Parâmetros de Start-AzureVM](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. Salvar o runbook hello e abrir o painel de teste de saudação.  Observe que agora você pode fornecer valores para Olá duas variáveis de entrada que você pode usar em teste hello.
9. Painel de teste Olá fechar.
10. Clique em **publicar** toopublish Olá nova versão de runbook hello.
11. Pare a máquina de virtual Olá iniciado na etapa anterior hello.
12. Clique em **iniciar** toostart Olá runbook.  Tipo de saudação **VMName** e **ResourceGroupName** para a máquina virtual de saudação que vai toostart.<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Quando Olá runbook for concluída, verifique que a máquina virtual Olá foi iniciada.

## <a name="step-9---create-a-conditional-link"></a>Etapa 9: criar um link condicional
Estamos agora modificar Olá runbook para que ele tenta toostart Olá virtual machine somente se não ainda tiver iniciado.  Faça isso adicionando um **AzureRmVM Get** cmdlet toohello runbook que obtém o status de nível de instância Olá da máquina virtual de saudação. Em seguida, adicionar um módulo de código de fluxo de trabalho do PowerShell chamado **obter Status** com um trecho de código do PowerShell de código toodetermine se o estado da máquina virtual hello está em execução ou parado.  Um link condicional de saudação **obter Status** módulo é executado somente **AzureRmVM início** se o estado de execução atual Olá for interrompido.  Por fim, podemos saída tooinform uma mensagem que você se Olá VM foi iniciado com êxito ou não usando Olá cmdlet PowerShell Write-Output.

1. Abra **MyFirstRunbook** no editor gráfico hello.
2. Remover o link de saudação entre **especificar Id da assinatura** e **início AzureRmVM** clicando nele e, em seguida, pressionando Olá *excluir* chave.
3. No controle da biblioteca de Olá, digite **Get-AzureRm** na caixa de texto de pesquisa de saudação.
4. Adicionar **Get-AzureRmVM** toohello tela.
5. Selecione **Get-AzureRmVM** e **parâmetro definido** tooview Olá define para **Get-AzureRmVM**.  Selecione Olá **GetVirtualMachineInResourceGroupNameParamSet** conjunto de parâmetros.  Observe que há pontos de exclamação ao lado de **ResourceGroupName** e **Name**.  Isso indica que são os parâmetros obrigatórios.  Observe também que ambos esperam valores da cadeia de caracteres.
6. Em **Fonte de dados** para **Name**, selecione **Entrada do runbook** e, em seguida, selecione **VMName**.  Clique em **OK**.
7. Em **Fonte de dados** para **ResourceGroupName**, selecione **Entrada do runbook** e, em seguida, selecione **ResourceGroupName**.  Clique em **OK**.
8. Em **Fonte de dados** para **Status**, selecione **Valor constante** e, em seguida, clique em **True**.  Clique em **OK**.  
9. Criar um link de **especificar Id da assinatura** muito**Get-AzureRmVM**.
10. No controle de saudação de biblioteca, expanda **controle de Runbook** e adicione **código** toohello tela.  
11. Criar um link de **Get-AzureRmVM** muito**código**.  
12. Clique em **código** e no painel de configuração do hello, altere o rótulo muito**obter Status**.
13. Selecione **código** parâmetro e hello **Editor de códigos** folha é exibida.  
14. No editor de código hello, cole Olá trecho de código a seguir:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. Criar um link de **obter Status** muito**AzureRmVM início**.<br> ![Runbook com Módulo de Código](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. Selecione o link hello e no painel de configuração hello, altere **aplicar a condição de** muito**Sim**.   Link da anotação Olá ativa tooa tracejado linha indicando que Olá destino atividade é executada somente se a condição de saudação resolve tootrue.  
17. Para Olá **expressão da condição**, tipo *$ActivityOutput ['obter Status'] - eq "Stopped"*.  **Iniciar AzureRmVM** agora só é executada se a máquina virtual de saudação é interrompida.
18. No hello controle de biblioteca, expanda **Cmdlets** e **Utility**.
19. Adicionar **Write-Output** toohello tela duas vezes.<br> ![Runbook com Write-Output](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Em Olá primeiro **Write-Output** de controle, clique em **parâmetros** e alterar Olá **rótulo** valor muito*notificar VM iniciado*.
21. Para **InputObject**, alterar **fonte de dados** muito**PowerShell expressão** e digite Olá expressão *"$VMName iniciado com êxito."* .
22. Em Olá segundo **Write-Output** de controle, clique em **parâmetros** e alterar Olá **rótulo** valor muito*notificar a VM Iniciar falha*
23. Para **InputObject**, alterar **fonte de dados** muito**PowerShell expressão** e digite Olá expressão *"$VMName não foi possível iniciar".* .
24. Criar um link de **início AzureRmVM** muito**notificar VM iniciado** e **notificar a VM Iniciar falha**.
25. Selecione o link de saudação muito**notificar VM iniciado** e alterar **aplicar a condição de** muito**True**.
26. Para Olá **expressão da condição**, tipo *$ActivityOutput ['Início-AzureRmVM']. IsSuccessStatusCode - eq $true*.  Esta saída de gravação controlar agora só é executada se a máquina virtual de saudação foi iniciada com êxito.
27. Selecione o link de saudação muito**notificar a VM Iniciar falha** e alterar **aplicar a condição de** muito**True**.
28. Para Olá **expressão da condição**, tipo *$ActivityOutput ['Início-AzureRmVM']. IsSuccessStatusCode - ne $true*.  Esta saída de gravação controlar agora só é executado se a máquina virtual de saudação não foi iniciada com êxito.
29. Salvar o runbook hello e abrir o painel de teste de saudação.
30. Iniciar runbook Olá com máquina virtual de saudação interrompida e ele deve ser iniciado.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre a criação de gráficos, consulte [criação gráfica na automação do Azure](automation-graphical-authoring-intro.md)
* tooget iniciado com runbooks do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [meu primeiro runbook de fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)

