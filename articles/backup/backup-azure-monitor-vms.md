---
title: "backups de máquina de virtual implantada para o Gerenciador de recursos de aaaMonitor | Microsoft Docs"
description: "Monitorar eventos e alertas a partir dos backups da máquina virtual implantados pelo Resource Manager. Envie um email com base em alertas."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Monitorar alertas para os backups das máquinas virtuais do Azure
Alertas são respostas do serviço de saudação que um limite de evento foi atingido ou ultrapassado. Saber quando problemas de início podem ser crítico tookeeping custos de negócios para baixo. Alertas normalmente não ocorrem em um agendamento e, portanto, é útil tooknow assim que possível após a ocorrem de alertas. Por exemplo, quando um trabalho de backup ou restauração falhar, um alerta ocorre dentro de cinco minutos de falha de saudação. No painel do cofre hello, Olá bloco alertas de Backup exibe os eventos de nível de aviso e crítico. Em configurações de alertas de Backup hello, você pode exibir todos os eventos. Mas o que fazer se um alerta ocorrer quando você estiver trabalhando em um problema separado? Se você não souber ao alerta Olá acontece, pode ser uma inconveniência secundária ou ele pode comprometer os dados. Quando isso ocorre, toomake se Olá correto as pessoas estejam cientes de um alerta - configure Olá serviço toosend notificações de alerta por email. Para obter detalhes sobre como configurar as notificações por email, confira [Configurar notificações](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Como localizar informações sobre alertas Olá?
tooview informações sobre o evento de saudação que gerou um alerta, você deve abrir a folha de alertas de Backup Olá. Há dois folha de alertas de Backup maneiras tooopen Olá: Olá bloco alertas de Backup no painel do Cofre de saudação tanto a partir da folha de alertas e eventos de saudação do.

bloco de folha de alertas de Backup Olá tooopen de alertas de Backup:

* Em Olá **alertas de Backup** bloco no painel do cofre hello, clique em **crítico** ou **aviso** tooview Olá eventos operacionais para o nível de gravidade.

    ![Bloco Alertas de Backup](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

folha de alertas de Backup tooopen Olá da folha de alertas e eventos hello:

1. No painel do cofre hello, clique em **todas as configurações**. ![Botão Todas as Configurações](./media/backup-azure-monitor-vms/all-settings-button.png)
2. Em Olá **configurações** folha, clique em **alertas e eventos**. ![Botão Alertas e Eventos](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. Em Olá **alertas e eventos** folha, clique em **alertas de Backup**. ![Botão Alertas de Backup](./media/backup-azure-monitor-vms/backup-alerts.png)

    Olá **alertas de Backup** folha é aberto e exibe Olá alertas filtradas.

    ![Bloco Alertas de Backup](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview obter informações detalhadas sobre um determinado alerta, na lista de saudação de eventos, clique em tooopen alerta Olá seu **detalhes** folha.

    ![Detalhe do Evento](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    atributos de saudação toocustomize exibidos na lista de hello, consulte [exibir atributos adicionais do evento](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Configurar notificações
 Você pode configurar notificações por email de toosend de serviço do Olá para alertas de saudação que ocorreram Olá última hora, ou quando ocorrem determinados tipos de eventos.

tooset as notificações de email para alertas

1. Olá alertas de Backup, clique em menu **configurar notificações**

    ![Menu Alertas de Backup](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    Abre a folha do Hello configurar notificações.

    ![Folha Configurar notificações](./media/backup-azure-monitor-vms/configure-notifications.png)
2. Na folha de notificações de configurar hello, notificações de Email, clique em **em**.

    Olá destinatários e caixas de diálogo de severidade têm uma estrela toothem próximo porque essa informação é necessária. Forneça pelo menos um endereço de email e selecione pelo menos uma Gravidade.
3. Em Olá **destinatários (Email)** caixa de diálogo, endereços de email do tipo Olá para quem recebe notificações de saudação. Use o formato de saudação: username@domainname.com. Separe os vários endereços de email com um ponto e vírgula (;).
4. Em Olá **notificar** área, escolha **por alerta** toosend notificação quando hello especificado ocorrer alerta, ou **Digest por hora** toosend um resumo de saudação última hora.
5. Em Olá **severidade** caixa de diálogo, escolha um ou mais níveis que você deseja tootrigger notificação por email.
6. Clique em **Salvar**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Quais tipos de alertas estão disponíveis para o backup da VM IaaS do Azure?
   | Nível de alerta | Alertas enviados |
   | --- | --- |
   | Crítico |Falha de backup, falha na recuperação |
   | Aviso |Nenhum |
   | Informativo |Nenhum |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Há situações em que o email não será enviado mesmo se as notificações estiverem configuradas?
Há situações em que um alerta não é enviado, mesmo que as notificações de saudação foi configuradas corretamente. Olá notificações por email de situações seguintes não são enviadas tooavoid ruído de alerta:

* Se as notificações são configurada tooHourly Digest e um alerta é gerado e resolvido na hora de saudação.
* Olá trabalho será cancelado.
* Um trabalho de backup é disparado e falha e outro trabalho de backup está em andamento.
* Inicia um trabalho de backup agendado para uma VM do Gerenciador de recursos habilitado, mas Olá VM não existe mais.

## <a name="customize-your-view-of-events"></a>Personalizar a exibição de eventos
Olá **logs de auditoria** configuração vem com um conjunto predefinido de filtros e colunas mostrando as informações de evento operacional. Você pode personalizar o modo de exibição de saudação para que quando Olá **eventos** folha for aberta, ela mostra Olá informações que você deseja.

1. Em Olá [painel Cofre](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), procurar tooand clique **os Logs de auditoria** tooopen Olá **eventos** folha.

    ![Logs de Auditoria](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Olá **eventos** folha abre toohello eventos operacionais filtrados para o cofre atual hello.

    ![Filtro de Logs da Auditoria](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    folha de saudação mostra Olá lista dos crítico, erro, aviso e informativos eventos que ocorreram Olá semana passada. Olá, período de tempo é um valor padrão definido em Olá **filtro**. Olá **eventos** folha também mostra um gráfico de barras de controle quando Olá eventos ocorridos. Se você não quiser o gráfico de barras toosee hello, em Olá **eventos** menu, clique em **ocultar gráfico** tootoggle fora do gráfico de saudação. exibição padrão de saudação de eventos mostra informações de operação, nível, Status, recursos e tempo. Para obter informações sobre expor atributos adicionais do evento, consulte a seção de saudação [expandir as informações de evento](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Para obter informações adicionais sobre um evento operacional, no hello **operação** coluna, clique em um evento operacional tooopen sua folha. folha de saudação contém informações detalhadas sobre eventos de saudação. Eventos são agrupados por sua ID de correlação e uma lista de eventos de saudação que ocorreram no período de tempo de saudação.

    ![Detalhes da Operação](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview obter informações detalhadas sobre um evento específico, na lista de saudação de eventos, clique em Olá evento tooopen seu **detalhes** folha.

    ![Detalhe do Evento](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    informações de nível de evento Olá são tão detalhadas como Olá obtém informações. Se você preferir ver essa quantidade informações sobre cada evento e gostaria de tooadd isso muito detalhe toohello **eventos** folha, consulte a seção Olá [expandir as informações de evento](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Personalizar o filtro de evento Olá
Saudação de uso **filtro** tooadjust ou escolha as informações de saudação que aparece em uma folha específica. informações do evento Olá toofilter:

1. Em Olá [painel Cofre](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), procurar tooand clique **os Logs de auditoria** tooopen Olá **eventos** folha.

    ![Logs de Auditoria](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Olá **eventos** folha abre toohello eventos operacionais filtrados para o cofre atual hello.

    ![Filtro de Logs da Auditoria](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. Em Olá **eventos** menu, clique em **filtro** tooopen folha.

    ![abrir folha do filtro](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. Em Olá **filtro** folha, ajustar Olá **nível**, **período**, e **chamador** filtros. Olá outros filtros não estão disponíveis depois que foram definidas as informações atuais tooprovide Olá para o Cofre de serviços de recuperação de saudação.

    ![Detalhes da consulta dos Logs de Auditoria](./media/backup-azure-monitor-vms/filter-blade.png)

    Você pode especificar Olá **nível** do evento: crítico, erro, aviso ou informativo. Você pode escolher qualquer combinação de Níveis de evento, mas deve ter, pelo menos, um Nível selecionado. Alterne Olá nível ativado ou desativado. Olá **período** filtro permite que você toospecify Olá período de tempo para capturar eventos. Se você usar um intervalo de tempo personalizado, pode definir Olá início e término.
4. Quando estiver pronto tooquery Olá operations logs usando o filtro, clique em **atualização**. os resultados de saudação exibem no hello **eventos** folha.

    ![Detalhes da Operação](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Exibir atributos adicionais do evento
Usando Olá **colunas** botão, você pode habilitar tooappear de atributos de evento adicionais na lista Olá Olá **eventos** folha. a lista de eventos padrão Olá exibe informações de operação, nível, Status, recursos e tempo. atributos adicionais de tooenable:

1. Em Olá **eventos** folha, clique em **colunas**.

    ![Abrir Colunas](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Olá **escolher colunas** folha é aberta.

    ![Folha Colunas](./media/backup-azure-monitor-vms/columns-blade.png)
2. Olá tooselect atributo, clique em caixa de seleção de saudação. caixa de seleção de atributo Olá ativa e desativa.
3. Clique em **redefinir** tooreset lista de saudação de atributos no hello **eventos** folha. Depois de adicionar ou remover atributos da lista hello, use **redefinir** tooview Olá nova lista de atributos de evento.
4. Clique em **atualização** tooupdate dados de saudação em atributos de evento hello. Olá, a tabela a seguir fornece informações sobre cada atributo.

| Nome da coluna | Descrição |
| --- | --- |
| Operação |nome de saudação da operação de saudação |
| Nível |Olá nível da operação hello, os valores podem ser: informativo, aviso, erro ou crítico |
| Status |Estado descritivo da operação de saudação |
| Recurso |URL que identifica o recurso de saudação. também conhecido como o ID de recurso Olá |
| Hora |Tempo, medido a partir do hello hora atual, em que ocorreu o evento Olá |
| Chamador |Quem ou o que chamado ou acionou o evento Olá; pode ser sistema hello, ou um usuário |
| Timestamp |tempo de saudação quando o evento Olá foi disparado |
| Grupo de recursos |grupo de recursos associado Olá |
| Tipo de recurso |tipo de recurso interno de saudação usado pelo Gerenciador de recursos |
| ID da assinatura |Olá associado à ID de assinatura |
| Categoria |Categoria de evento de saudação |
| ID de Correlação |ID comum para eventos relacionados |

## <a name="use-powershell-toocustomize-alerts"></a>Use o PowerShell toocustomize alertas
Você pode obter notificações de alerta personalizadas para trabalhos de saudação no portal de saudação. tooget esses trabalhos, definir regras em Olá operacional registra eventos de alerta com base em PowerShell. Use o *PowerShell versão 1.3.0 ou posterior*.

toodefine tooalert uma notificação personalizada para falhas de backup, use um comando como Olá script a seguir:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : você pode obter ResourceId da saudação logs de auditoria. Olá ResourceId é uma URL fornecida na coluna de recurso Olá Olá logs de operação.

**OperationName** : OperationName está no formato de hello "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" onde *EventName* pode ser:<br/>

* Registrar <br/>
* Cancelar o registro  <br/>
* Configurar Proteção  <br/>
* Backup  <br/>
* Restaurar  <br/>
* Parar Proteção  <br/>
* Excluir Dados de Backup  <br/>
* Criar Política de Proteção  <br/>
* Excluir Política de Proteção  <br/>
* Atualizar Política de Proteção  <br/>

**Status** : os valores com suporte são Iniciado, Êxito ou Falha.

**ResourceGroup** : isso é hello grupo de recursos toowhich Olá recurso pertence. Você pode adicionar Olá logs de toohello gerado de coluna de grupo de recursos. Grupo de recursos é um dos tipos disponíveis de saudação de informações de eventos.

**Nome** : nome da regra de alerta de saudação.

**CustomEmail** : especificar toowhich de endereço de email personalizado Olá deseja toosend uma notificação de alerta

**SendToServiceOwners** : essa opção envia os administradores tooall de notificações de alerta e os coadministradores de assinatura de saudação. Pode ser usado no cmdlet **New-AzureRmAlertRuleEmail**

### <a name="limitations-on-alerts"></a>Limitações sobre alertas
Alertas baseados em eventos são toohello assunto seguintes limitações:

1. Os alertas são disparados em todas as máquinas virtuais Olá que Cofre de serviços de recuperação. Você não pode personalizar o alerta de saudação para um subconjunto de máquinas virtuais em um cofre de serviços de recuperação.
2. Esse recurso está em Preview. [Saiba mais](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Os alertas são enviados de “alerts-noreply@mail.windowsazure.com”. Atualmente você não pode modificar o remetente do email hello.

## <a name="next-steps"></a>Próximas etapas
Logs de eventos habilitar post-mortem grande e suporte para operações de backup de saudação de auditoria. Olá operações a seguir é registrado:

* Registrar
* Cancelar o registro 
* Configurar a proteção
* Backup (backup agendado ou sob demanda)
* Restaurar 
* Parar a proteção
* Excluir dados de backup
* Adicionar política
* Excluir política
* Atualizar política
* Cancelar trabalho

Para obter uma explicação amplo de eventos, as operações e os logs de auditoria em Olá serviços do Azure, consulte o artigo de hello, [exibir eventos e logs de auditoria](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Para obter informações sobre como recriar uma máquina virtual a partir de um ponto de recuperação, verifique [Restaurar VMs do Azure](backup-azure-restore-vms.md). Se você precisar obter informações sobre como proteger suas máquinas virtuais, consulte [primeiro olhar: fazer backup de máquinas virtuais tooa Cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md). Saiba mais sobre tarefas de gerenciamento de saudação para backups VM no artigo hello, [backups de máquina virtual do Azure gerenciar](backup-azure-manage-vms.md).
