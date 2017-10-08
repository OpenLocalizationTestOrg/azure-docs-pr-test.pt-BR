---
title: "aaaStart/parar máquinas virtuais durante a solução de fora do horário comercial [visualização] | Microsoft Docs"
description: "soluções de gerenciamento de VM Olá inicia e interrompe a máquinas virtuais do Gerenciador de recursos do Azure em um agendamento e monitorar proativamente a partir de análise de Log."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Solução Iniciar/Parar VMs fora do horário comercial [Visualização] na Automação

Hello VMs iniciar/parar durante a solução de fora do horário comercial [visualização] inicia e interrompe as máquinas virtuais do Azure Resource Manager em um agendamento definido pelo usuário e fornece informações sobre o sucesso de saudação de trabalhos de automação de saudação que iniciar e interromper as máquinas virtuais com o OMS Análise de log.  

## <a name="prerequisites"></a>Pré-requisitos

- Olá runbooks trabalhar com um [conta executar como do Azure](automation-offering-get-started.md#authentication-methods).  Olá conta executar como é o método de autenticação de saudação preferido porque ele usa a autenticação de certificado em vez de uma senha que pode expirar ou alterados com frequência.  

- Esta solução só pode gerenciar máquinas virtuais que estão em Olá mesma assinatura onde reside a conta de automação de saudação.  

- Essa solução implantará somente toohello regiões do Azure - Leste dos EUA, Sudeste da Austrália, Sudeste da Ásia e Europa Ocidental a seguir.  Olá runbooks que gerencia o agendamento VM Olá pode direcionar VMs em qualquer região.  

- toosend notificações por email quando Olá iniciar e parar runbooks VM completa, uma assinatura de classe de negócios do Office 365 é necessária.  

## <a name="solution-components"></a>Componentes da solução

Essa solução consiste em Olá recursos que serão importados e adicionaram tooyour conta de automação a seguir.

### <a name="runbooks"></a>Runbooks

Runbook | Descrição|
--------|------------|
CleanSolution-MS-Mgmt-VM | Esse runbook removerá independente de todos os recursos e agendamentos, quando você for toodelete solução de saudação de sua assinatura.|  
SendMailO365-MS-Mgmt | Esse runbook envia um email pelo Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Este runbook é pretendido toostart VMs (ambos clássico e ARM com base em máquinas virtuais) que reside em uma determinada lista de grupos de recursos do Azure.
StopByResourceGroup-MS-Mgmt-VM | Este runbook é pretendido toostop VMs (ambos clássico e ARM com base em máquinas virtuais) que reside em uma determinada lista de grupos de recursos do Azure.|
<br>

### <a name="variables"></a>variáveis

Variável | Descrição|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Especifica se os runbooks StartByResourceGroup-MS-Mgmt-VM e StopByResourceGroup-MS-Mgmt-VM podem enviar notificação por email após a conclusão.  Selecione **True** tooenable e **False** toodisable alertas de email. O valor padrão é **False**.| 
Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Insira a VM nomes toobe excluído da operação de gerenciamento. Separe os nomes usando semi-colon(;) sem espaços. Os valores diferenciam maiúsculas de minúsculas e há suporte para curingas (asterisco).|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que pode ser anexada toohello a partir do corpo de mensagem de email de saudação.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica o nome de saudação do hello conta de automação contém Olá Email runbook.  **Não modifique essa variável.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Especifica o nome de saudação do hello email runbook.  Isso é usado por hello StartByResourceGroup-MS-Mgmt-VM e o email de toosend runbooks StopByResourceGroup-MS-Mgmt-VM.  **Não modifique essa variável.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica o nome de Olá Olá do grupo de recursos que contém a saudação Email runbook.  **Não modifique essa variável.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Especifica o texto de saudação para linha de assunto de saudação de email de saudação.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica a saudação destinatários de email hello.  Digite nomes separados usando ponto e vírgula (;) sem espaços.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Insira a VM nomes toobe excluído da operação de gerenciamento. Separe os nomes usando semi-colon(;) sem espaços. Os valores diferenciam maiúsculas de minúsculas e há suporte para curingas (asterisco).  Valor padrão (com asterisco) incluirá todos os grupos de recursos na assinatura de saudação.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica a assinatura Olá que contém toobe de VMs gerenciada por essa solução.  Isso deve ser Olá a mesma assinatura em que reside o hello conta de automação dessa solução.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Insira a VM nomes toobe excluído da operação de gerenciamento. Separe os nomes usando semi-colon(;) sem espaços. Os valores diferenciam maiúsculas de minúsculas e há suporte para curingas (asterisco).|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que pode ser anexada toohello a partir do corpo de mensagem de email de saudação.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica o nome de saudação do hello conta de automação contém Olá Email runbook.  **Não modifique essa variável.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica o nome de Olá Olá do grupo de recursos que contém a saudação Email runbook.  **Não modifique essa variável.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Especifica o texto de saudação para linha de assunto de saudação de email de saudação.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica a saudação destinatários de email hello.  Digite nomes separados usando ponto e vírgula (;) sem espaços.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Insira a VM nomes toobe excluído da operação de gerenciamento. Separe os nomes usando semi-colon(;) sem espaços. Os valores diferenciam maiúsculas de minúsculas e há suporte para curingas (asterisco).  Valor padrão (com asterisco) incluirá todos os grupos de recursos na assinatura de saudação.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica a assinatura Olá que contém toobe de VMs gerenciada por essa solução.  Isso deve ser Olá a mesma assinatura em que reside o hello conta de automação dessa solução.|  
<br>

### <a name="schedules"></a>Agendas

Agenda | Descrição|
---------|------------|
StartByResourceGroup-agenda-MS-Mgmt | Agenda de runbook StartByResourceGroup, que executa a inicialização de saudação de VMs gerenciadas por essa solução. Quando criado, padrão é tooUTC fuso horário.|
StopByResourceGroup-agenda-MS-Mgmt | Agenda de runbook StopByResourceGroup, que executa o desligamento de saudação de VMs gerenciadas por essa solução. Quando criado, padrão é tooUTC fuso horário.|

### <a name="credentials"></a>Credenciais

Credencial | Descrição|
-----------|------------|
O365Credential | Especifica um email de toosend conta do usuário do Office 365 válido.  Necessário apenas se a variável SendMailO365-IsSendEmail-MS-Mgmt está definido muito**True**.

## <a name="configuration"></a>Configuração

Olá durante o horário de trabalho [visualização] solução tooyour conta de automação a seguir etapas tooadd Olá VMs iniciar/parar de executar e, em seguida, configurar a solução de Olá Olá variáveis toocustomize.

1. Saudação inicial-tela hello portal do Azure, selecione Olá **Marketplace** lado a lado.  Se Olá bloco não está mais tooyour fixados home-tela hello à esquerda no painel de navegação, selecione **novo**.  
2. Na folha do Marketplace hello, digite **iniciar VM** na caixa de pesquisa hello e solução de hello, em seguida, selecione **iniciar/parar VMs fora do horário comercial [visualização]** Olá dos resultados da pesquisa.  
3. Em Olá **iniciar/parar VMs fora do horário comercial [visualização]** folha para Olá selecionado solução, examine as informações de resumo hello e, em seguida, clique em **criar**.  
4. Olá **adicionar solução** lâmina aparece onde você está tooconfigure solicitadas Olá solução antes de importá-lo em sua assinatura de automação.<br><br> ![Folha Adicionar Solução do Gerenciamento de VM](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Em Olá **adicionar solução** folha, selecione **espaço de trabalho** e aqui, você selecionar um espaço de trabalho do OMS é vinculado toohello mesma assinatura do Azure que Olá conta de automação está em ou criar um novo espaço de trabalho do OMS.  Se você não tiver um espaço de trabalho do OMS, você pode selecionar **criar novo espaço de trabalho** e Olá **espaço de trabalho do OMS** folha executar seguinte hello: 
   - Especifique um nome para Olá novo **espaço de trabalho do OMS**.
   - Selecione um **assinatura** toolink tooby selecionando na lista suspensa de saudação se padrão Olá selecionado não é apropriado.
   - Em **Grupo de Recursos**, você pode selecionar um grupo de recursos existente ou criar um novo.  
   - Selecione um **Local**.  No momento Olá únicos locais fornecidos para seleção, são **Sudeste da Austrália**, **Leste dos EUA**, **Sudeste da Ásia**, e **Ocidental**.
   - Selecione um **tipo de preço**.  Olá solução é oferecida em duas camadas: gratuito e OMS paga da camada.  camada gratuita Olá tem um limite na quantidade de saudação dos dados coletados diariamente, período de retenção e minutos de tempo de execução do trabalho de runbook.  Olá OMS paga da camada não tem um limite na quantidade de saudação de dados coletados diariamente.  

        > [!NOTE]
        > Enquanto Olá autônomo paga camada é exibida como uma opção, não é aplicável.  Se você selecioná-la e continuar com a criação de saudação da solução em sua assinatura, ele falhará.  Essa questão será abordada quando a solução for lançada oficialmente.<br>Se você usar essa solução, ela só usará minutos de trabalho de automação e de ingestão de log.  solução de saudação não adicionar ambiente tooyour de nós OMS adicionais.  

6. Depois de fornecer informações de saudação necessárias em Olá **espaço de trabalho do OMS** folha, clique em **criar**.  Enquanto as informações de saudação são verificadas e espaço de trabalho de saudação é criado, você pode acompanhar seu progresso em **notificações** menu hello.  Você será retornado toohello **adicionar solução** folha.  
7. Em Olá **adicionar solução** folha, selecione **conta de automação**.  Se você estiver criando um novo espaço de trabalho do OMS, será necessário tooalso criar uma nova conta de automação que será associada com hello novo espaço de trabalho OMS especificado anteriormente, incluindo sua assinatura do Azure, o grupo de recursos e a região.  Você pode selecionar **criar uma conta de automação** e Olá **conta de automação adicionar** folha, fornecer Olá seguintes: 
  - Em Olá **nome** campo, digite nome Olá Olá conta de automação.

    Todas as outras opções são preenchidas automaticamente com base no espaço de trabalho do OMS Olá selecionado e essas opções não podem ser modificadas.  Uma conta executar como do Azure é o método de autenticação padrão Olá para runbooks Olá incluído nesta solução.  Depois de clicar em **Okey**, opções de configuração de saudação são validadas e Olá conta de automação é criado.  Você pode acompanhar seu progresso em **notificações** menu hello. 

    Caso contrário, você pode selecionar uma conta Executar como de Automação existente.  Observe que a conta Olá selecionada não pode ser vinculado tooanother espaço de trabalho do OMS, caso contrário, uma mensagem será apresentada na Olá folha tooinform você.  Se já estiver vinculado, será necessário tooselect uma conta executar como automação diferente ou crie um novo.<br><br> ![Automação conta já vinculado tooOMS espaço de trabalho](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Por fim no hello **adicionar solução** folha, selecione **configuração** e hello **parâmetros** folha é exibida.  Em Olá **parâmetros** folha, você precisará:  
   - Especifique a saudação **nomes de grupo de recursos de destino**, que é um nome de grupo de recursos que contém toobe de VMs gerenciada por essa solução.  Você pode inserir mais de um nome e separá-los usando ponto-e-vírgula (os valores diferenciam maiúsculas de minúsculas).  Usar um caractere curinga é suportado se você quiser tootarget VMs em todos os grupos de recursos na assinatura de saudação.
   - Selecione um **agenda** que é uma recorrência de data e hora, iniciando e parando Olá da VM no hello grupos de recursos de destino.  Por padrão, agendamento de saudação é fuso horário configurado toohello UTC e selecionar uma região diferente não está disponível.  Se você quiser tooconfigure Olá agenda tooyour fuso horário específico depois de configurar a solução hello, consulte [agenda de inicialização e desligamento Olá modificando](#modifying-the-startup-and-shutdown-schedule) abaixo.    

10. Depois de ter concluído a saudação inicial configurações necessárias para a solução de saudação, selecione **criar**.  Todas as configurações serão validadas e, em seguida, ele tentará toodeploy solução de saudação em sua assinatura.  Esse processo pode levar vários segundos toocomplete e você pode acompanhar seu progresso em **notificações** menu hello. 

## <a name="collection-frequency"></a>Frequência de coleta

Dados de fluxo automação trabalho log e o trabalho é incluídos no repositório do OMS Olá a cada cinco minutos.  

## <a name="using-hello-solution"></a>Usando a solução de saudação

Quando você adiciona a solução de gerenciamento de VM hello, em sua saudação de espaço de trabalho do OMS **StartStopVM exibição** bloco será adicionado tooyour painel do OMS.  Este bloco exibe uma contagem e a representação gráfica dos trabalhos de runbooks Olá para solução de saudação que iniciaram e concluiu com êxito.<br><br> ![Bloco de exibição StartStopVM de Gerenciamento de VM](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Em sua conta de automação, você pode acessar e gerenciar a solução Olá selecionando Olá **soluções** lado a lado e, em seguida, Olá **soluções** folha, selecionando a solução Olá **[Start-Stop-VM Espaço de trabalho]** da lista de saudação.<br><br> ![Lista de soluções de automação](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Selecionar solução Olá exibirá Olá **Start-Stop-VM [espaço de trabalho]** folha de solução, onde você pode analisar detalhes importantes como Olá **StartStopVM** lado a lado, como no espaço de trabalho do OMS, que Exibe uma contagem e a representação gráfica dos trabalhos de runbooks Olá para solução de saudação que iniciaram e foram concluídos com êxito.<br><br> ![Folha Solução VM de Automação](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Aqui você pode também abrir seu espaço de trabalho do OMS e executar a análise dos registros de trabalho hello.  Basta clicar em **todas as configurações**e em Olá **configurações** folha, selecione **início rápido** e, em seguida, em Olá **início rápido** selecione folha  **Portal do OMS**.   Isso abrirá uma nova guia ou sessão do navegador e introduzirá seu espaço de trabalho do OMS associado à sua conta de Automação e assinatura.  


### <a name="configuring-e-mail-notifications"></a>Configurando notificações por email

tooenable as notificações por email quando hello iniciar e parar runbooks VM completa, você precisará Olá toomodify **O365Credential** de credencial e, no mínimo, Olá seguintes variáveis:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

Olá tooconfigure **O365Credential** de credencial, execute Olá etapas a seguir:

1. Na sua conta de automação, clique em **todas as configurações de** na parte superior de saudação da janela de saudação. 
2. Em Olá **configurações** folha na seção Olá **recursos de automação**, selecione **ativos**. 
3. Em Olá **ativos** folha, selecione Olá **credencial** lado a lado e de saudação **credencial** folha, selecione Olá **O365Credential**.  
4. Insira um nome de usuário válido do Office 365 e uma senha e, em seguida, clique em **salvar** toosave suas alterações.  

variáveis de saudação tooconfigure realçados anteriormente, execute Olá etapas a seguir:

1. Na sua conta de automação, clique em **todas as configurações de** na parte superior de saudação da janela de saudação. 
2. Em Olá **configurações** folha na seção Olá **recursos de automação**, selecione **ativos**. 
3. Em Olá **ativos** folha, selecione Olá **variáveis** lado a lado e de saudação **variáveis** folha, selecione variável Olá listado acima e, em seguida, modificar seu valor Olá a seguir Descrição para ele especificado no hello [variável](##variables) seção anterior.  
4. Clique em **salvar** variável de toohello toosave Olá alterações.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Modificar agendamento de inicialização e desligamento Olá

Gerencia agenda de inicialização e desligamento do hello nesta solução segue Olá mesmo etapas, conforme descrito na [agendar um runbook na automação do Azure](automation-schedules.md).  Lembre-se de que você não pode modificar a configuração de agendamento de saudação.  Você precisará toodisable Olá agendamento existente e, em seguida, crie um novo e, em seguida, vincular toohello **StartByResourceGroup-MS-Mgmt-VM** ou **StopByResourceGroup-MS-Mgmt-VM** runbook que você deseja Olá Agende tooapply para.   

## <a name="log-analytics-records"></a>Registros do Log Analytics

Automação cria dois tipos de registros no repositório do OMS hello.

### <a name="job-logs"></a>Logs de trabalho

Propriedade | Descrição|
----------|----------|
Chamador |  Quem iniciou a operação de saudação.  Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados.|
Categoria | Classificação de tipo de saudação de dados.  Para automação, o valor de saudação é JobLogs.|
CorrelationId | GUID que é hello Id de correlação de trabalho de runbook hello.|
JobId | GUID que é hello Id do trabalho de runbook hello.|
operationName | Especifica o tipo de saudação da operação executada no Azure.  Para automação, o valor de saudação será o trabalho.|
resourceId | Especifica o tipo de recurso Olá no Azure.  Para automação, o valor de saudação é conta de automação Olá associada hello.|
ResourceGroup | Especifica o nome do grupo de recursos Olá Olá do trabalho de runbook.|
ResourceProvider | Especifica a saudação do serviço do Azure que fornece recursos de saudação, você pode implantar e gerenciar.  Para automação, o valor de saudação é automação do Azure.|
ResourceType | Especifica o tipo de recurso Olá no Azure.  Para automação, o valor de saudação é conta de automação Olá associada hello.|
resultType | status de Olá Olá do trabalho de runbook.  Os valores possíveis são:<br>- Iniciado<br>- Parado<br>- Suspenso<br>- Com falha<br>- Êxito|
resultDescription | Descreve o estado de resultado do trabalho de runbook hello.  Os valores possíveis são:<br>- O trabalho foi iniciado<br>- O trabalho falhou<br>- Trabalho Concluído|
RunbookName | Especifica o nome de saudação do runbook hello.|
SourceSystem | Especifica o sistema de origem Olá para dados de saudação enviados.  Para automação, o valor de saudação será: OpsManager|
StreamType | Especifica o tipo de saudação do evento. Os valores possíveis são:<br>- Detalhado<br>- Saída<br>- Erro<br>- Aviso|
SubscriptionId | Especifica a ID de assinatura de saudação do trabalho de saudação.
Hora | Data e hora quando o trabalho de runbook Olá executado.|


### <a name="job-streams"></a>Transmissões de trabalho

Propriedade | Descrição|
----------|----------|
Chamador |  Quem iniciou a operação de saudação.  Os valores possíveis são um endereço de email ou o sistema para trabalhos agendados.|
Categoria | Classificação de tipo de saudação de dados.  Para automação, o valor de saudação é JobStreams.|
JobId | GUID que é hello Id do trabalho de runbook hello.|
operationName | Especifica o tipo de saudação da operação executada no Azure.  Para automação, o valor de saudação será o trabalho.|
ResourceGroup | Especifica o nome do grupo de recursos Olá Olá do trabalho de runbook.|
resourceId | Especifica a Id de recurso Olá no Azure.  Para automação, o valor de saudação é conta de automação Olá associada hello.|
ResourceProvider | Especifica a saudação do serviço do Azure que fornece recursos de saudação, você pode implantar e gerenciar.  Para automação, o valor de saudação é automação do Azure.|
ResourceType | Especifica o tipo de recurso Olá no Azure.  Para automação, o valor de saudação é conta de automação Olá associada hello.|
resultType | resultado de Olá Olá do trabalho de runbook no evento Olá Olá foi gerado.  Os valores possíveis são:<br>- InProgress|
resultDescription | Inclui Olá fluxo de saída de runbook hello.|
RunbookName | nome de saudação do runbook hello.|
SourceSystem | Especifica o sistema de origem Olá para dados de saudação enviados.  Para automação, o valor de saudação será OpsManager|
StreamType | tipo de saudação do fluxo de trabalho. Os valores possíveis são:<br>- Andamento<br>- Saída<br>- Aviso<br>- Erro<br>- Depurar<br>- Detalhado|
Hora | Data e hora quando o trabalho de runbook Olá executado.|

Quando você executa qualquer pesquisa de log que retorna registros de categoria de **JobLogs** ou **JobStreams**, você pode selecionar Olá **JobLogs** ou **JobStreams** exibição que exibe um conjunto de quadros de resumo de atualizações de saudação retornadas pela pesquisa de saudação.

## <a name="sample-log-searches"></a>Pesquisas de log de exemplo

Olá tabela a seguir fornece pesquisas de log de exemplo para registros de trabalho coletados por essa solução. 

Consultar | Descrição|
----------|----------|
Localizar trabalhos de runbook StartVM que foram concluídos com êxito | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Localizar trabalhos de runbook StopVM que foram concluídos com êxito | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Mostrar o status do trabalho ao longo do tempo para runbooks StartVM e StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Remover solução Olá

Se você decidir que não mais precisar toouse solução de saudação qualquer adicional, você poderá excluí-la da saudação conta de automação.  Excluir solução Olá removerá apenas runbooks hello, não excluirá agendas hello ou variáveis que foram criadas quando a solução de saudação foi adicionada.  Esses ativos você precisará toodelete manualmente se você não estiver usando-os com outros runbooks.  

toodelete Olá solução, execute Olá etapas a seguir:

1.  Na sua conta de automação, selecione Olá **soluções** lado a lado.  
2.  Em Olá **soluções** folha, solução de saudação selecione **Start-Stop-VM [espaço de trabalho]**.  Em Olá **VMManagementSolution [espaço de trabalho]** folha, do menu do botão Olá **excluir**.<br><br> ![Excluir a Solução de Gerenciamento de VM](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  Em Olá **excluir solução** janela, confirme que você deseja toodelete Olá solução.
4.  Enquanto informações de saudação são verificadas e solução de saudação for excluída, você pode acompanhar seu progresso em **notificações** menu hello.  Você será retornado toohello **VMManagementSolution [espaço de trabalho]** folha depois Olá processo tooremove solução começa.  

espaço de trabalho do OMS e conta de automação de saudação não serão excluídos como parte desse processo.  Se você não quiser que espaço de trabalho do OMS tooretain hello, será necessário toomanually excluí-lo.  Isso pode ser feito também da saudação portal do Azure.   Saudação inicial-tela hello portal do Azure, selecione **análise de Log** e, em seguida, em Olá **análise de Log** folha, espaço de trabalho Olá selecione e clique em **excluir** do menu Olá folha de configurações de espaço de trabalho de saudação.  
      
## <a name="next-steps"></a>Próximas etapas

- toolearn mais sobre como consultas de pesquisa diferentes tooconstruct e examine Olá automação trabalho logs de análise de Log, consulte [pesquisas de Log na análise de Log](../log-analytics/log-analytics-log-searches.md)
- toolearn mais sobre a execução do runbook, como trabalhos de runbook toomonitor e outros detalhes técnicos, consulte [acompanhar um trabalho de runbook](automation-runbook-execution.md)
- toolearn mais sobre análise de logs do OMS e fontes de coleta de dados, consulte [dados de armazenamento do Azure coleta na visão geral da análise de Log](../log-analytics/log-analytics-azure-storage.md)






   

