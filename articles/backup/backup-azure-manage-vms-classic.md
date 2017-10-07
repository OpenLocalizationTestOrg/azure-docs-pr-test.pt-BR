---
title: "monitor e aaaManage backups de máquina virtual do Azure | Microsoft Docs"
description: "Saiba como monitor virtual do Azure e toomanage máquina backups"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Gerenciar trabalhos de Backup do Azure comuns e os alertas de disparador no portal clássico Olá
> [!div class="op_single_selector"]
> * [Gerenciar backups da VM do Azure](backup-azure-manage-vms.md)
> * [Gerenciar backups de VMs clássicas](backup-azure-manage-vms-classic.md)
>
>

Este artigo fornece informações sobre tarefas comuns de gerenciamento e monitoramento para máquinas virtuais do modelo Clássico protegidas no Azure.  

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Consulte [preparar seu tooback ambiente backup de máquinas virtuais do Azure](backup-azure-vms-prepare.md) para obter detalhes sobre como trabalhar com implantação clássico VMs de modelo.
>
> [!IMPORTANT]
>A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
>
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.

## <a name="manage-protected-virtual-machines"></a>Gerenciar máquinas virtuais protegidas
toomanage máquinas virtuais protegidas:

1. tooview e gerenciar as configurações de backup para uma máquina virtual, clique em Olá **itens protegidos** guia.
2. Clique no nome de saudação de uma saudação do item protegido toosee **detalhes de Backup** guia, que mostra informações sobre o último backup de saudação.

    ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview e gerenciar configurações de política de backup para uma máquina virtual, clique em Olá **políticas** guia.

    ![Política de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Olá **políticas de Backup** guia mostra Olá política existente. Você pode modificar conforme necessário. Se você precisar de uma nova política de toocreate clique **criar** em Olá **políticas** página. Observe que se você quiser tooremove uma política de ele não deve ter todas as máquinas virtuais associadas a ele.

    ![Política de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. Você pode obter mais informações sobre ações ou status para uma máquina virtual em Olá **trabalhos** página. Clique em um trabalho em Olá lista tooget mais detalhes, ou filtre os trabalhos para uma máquina virtual específica.

    ![Trabalhos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Backup sob demanda de uma máquina virtual
Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção. Se o backup de saudação inicial está pendente para a máquina virtual de hello, backup sob demanda criará uma cópia completa da máquina virtual de saudação no cofre de backup do Azure. Se o primeiro backup for concluído, será backup sob demanda somente alterações de envio do backup anterior de backup tooAzure cofre ou seja, ele é sempre incremental.

> [!NOTE]
> Período de retenção de um backup sob demanda é definir o valor de tooretention especificado para retenção diária na política de backup correspondente toohello VM.  
>
>

backup tootake uma demanda de uma máquina virtual:

1. Navegue toohello **itens protegidos** página e selecione **Máquina Virtual do Azure** como **tipo** (se ainda não estiver selecionado) e clique em **selecione**botão.

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. Selecionar máquina virtual de saudação na qual você deseja tootake uma demanda backup e clique em **Backup agora** botão final Olá Olá página.

    ![Fazer backup agora](./media/backup-azure-manage-vms/backup-now.png)

    Isso criará um trabalho de backup na máquina virtual de saudação selecionada. Período de retenção de ponto de recuperação criado por esse trabalho será o mesmo que a especificada na política de saudação associada à máquina virtual de saudação.

    ![Criando um trabalho de backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > política de saudação tooview associada a uma máquina virtual, detalhada para baixo em máquina virtual no hello **itens protegidos** guia de política de toobackup vá e página.
   >
   >
3. Quando o trabalho de saudação é criado, você pode clicar em **Exibir trabalho** botão torrada Olá barra toosee trabalho correspondente do hello na página de trabalhos de saudação.

    ![Trabalho de backup criado](./media/backup-azure-manage-vms/created-job.png)
4. Após a conclusão bem-sucedida do trabalho hello, um ponto de recuperação será criado que você pode usar toorestore Olá VM. Isso também será incrementado valor de coluna de ponto de recuperação Olá por 1 na **itens protegidos** página.

## <a name="stop-protecting-virtual-machines"></a>Interromper a proteção de máquinas virtuais
Você pode escolher toostop futuros backups saudação de uma máquina virtual com hello as opções a seguir:

* Reter dados de backup associados à máquina virtual no cofre de Backup do Azure
* Excluir dados de backup associados à máquina virtual

Se você tiver selecionado dados de backup tooretain associados à máquina virtual, você pode usar a máquina virtual do hello dados de backup toorestore Olá. Para obter detalhes de preço dessas máquinas virtuais, clique [aqui](https://azure.microsoft.com/pricing/details/backup/).

proteção de tooStop para uma máquina virtual:

1. Navegue muito**itens protegidos** página e selecione **máquina virtual do Azure** como tipo de filtro da saudação (se ainda não estiver selecionado) e clique em **selecione** botão.

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. Selecione a máquina virtual de saudação e clique em **parar proteção** final Olá Olá página.

    ![Parar a proteção](./media/backup-azure-manage-vms/stop-protection.png)
3. Por padrão, Backup do Azure não excluir os dados de backup Olá associados à máquina virtual de saudação.

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Se você quiser toodelete dados de backup, marque a caixa de seleção de saudação.

    ![Caixa de seleção](./media/backup-azure-manage-vms/checkbox.png)

    Selecione um motivo para interromper o backup de saudação. Enquanto isso é opcional, fornecer um motivo ajuda toowork de Backup do Azure nos comentários de saudação e priorizar os cenários de cliente Olá.
4. Clique em **enviar** saudação do botão toosubmit **interromper a proteção** trabalho. Clique em **Exibir trabalho** toosee Olá trabalho Olá correspondente em **trabalhos** página.

    ![Parar a proteção](./media/backup-azure-manage-vms/stop-protect-success.png)

    Se você não selecionou **excluir os dados de backup associados** opção durante **parar proteção** proteção Assistente e, em seguida, após a conclusão do trabalho, status muda muito**proteção interrompida**. dados de saudação permanecem com o Azure Backup até que sejam excluídas explicitamente. Você sempre pode excluir dados saudação, selecionando a máquina virtual de saudação no hello **itens protegidos** página e clicando em **excluir**.

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Se você tiver selecionado Olá **excluir os dados de backup associados** opção, hello máquina virtual não fará parte dos Olá **itens protegidos** página.

## <a name="re-protect-virtual-machine"></a>Proteger novamente a Máquina virtual
Se você não selecionou Olá **excluir dados de backup associados** opção **parar proteção**, proteger máquina virtual de saudação novamente seguindo Olá etapas semelhantes toobacking backup registrado virtual máquinas. Depois de protegido, esta máquina virtual terá proteção do backup de dados retidos toostop anterior e pontos de recuperação criado após protege novamente.

Depois de proteger novamente, o status de proteção da máquina de virtual Olá será alterado muito**protegidos** se houver pontos de recuperação anterior muito**parar proteção**.

  ![Máquina virtual protegida novamente](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Ao proteger novamente a máquina virtual de hello, você pode escolher uma regra diferente que a política de saudação com a qual a máquina virtual foi inicialmente protegida.
>
>

## <a name="unregister-virtual-machines"></a>Cancelar o registro das máquinas virtuais
Se você desejar tooremove Olá máquina de virtual do Cofre de backup hello:

1. Clique em Olá **UNREGISTER** botão final Olá Olá página.

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/unregister-button.png)

    Uma notificação do sistema será exibido na parte inferior da saudação da tela hello solicitando a confirmação. Clique em **Sim** toocontinue.

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Excluir dados de backup
Você pode excluir os dados de backup Olá associados a uma máquina virtual, ou:

* Durante a interrupção do trabalho da proteção
* Após uma interrupção no trabalho de proteção ser concluída em uma máquina virtual

toodelete dados de backup em uma máquina virtual, que está na saudação *proteção interrompida* estado após a conclusão bem-sucedida de um **parar Backup** trabalho:

1. Navegue toohello **itens protegidos** página e selecione **Máquina Virtual do Azure** como *tipo* e clique em Olá **selecione** botão.

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. Selecione a máquina virtual de saudação. máquina virtual de saudação estará em **proteção interrompida** estado.

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Clique em Olá **excluir** botão final Olá Olá página.

    ![Excluir backup](./media/backup-azure-manage-vms/delete-backup.png)
4. Em Olá **excluir dados de backup** assistente, selecione um motivo para a exclusão de dados de backup (recomendados) e clique em **enviar**.

    ![Excluir dados de backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Isso criará um trabalho toodelete backup de dados de máquina virtual selecionada. Clique em **Exibir trabalho** toosee o trabalho correspondente na página trabalhos.

    ![Exclusão de dados bem-sucedida](./media/backup-azure-manage-vms/delete-data-success.png)

    Após a conclusão do trabalho hello, Olá entrada de máquina virtual de toohello correspondente será removida do **itens protegidos** página.

## <a name="dashboard"></a>Painel
Em Olá **painel** página você pode examinar informações sobre máquinas virtuais do Azure, armazenamento e trabalhos associados a eles no hello últimas 24 horas. Você pode exibir o status de backup e quaisquer erros de backup associados.

![Painel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Os valores no painel de saudação são atualizados uma vez a cada 24 horas.
>
>

## <a name="auditing-operations"></a>Operações de auditoria
O backup do Azure fornece análise de hello "logs de operação" das operações de backup disparados por cliente Olá tornando fácil toosee exatamente quais operações de gerenciamento foram realizadas no cofre de backup hello. Logs de operações habilitar post-mortem grande e suporte para operações de backup de saudação de auditoria.

Olá operações a seguir é registrada nos logs de operação:

* Registrar
* Cancelar o registro 
* Configurar a proteção
* Backup (tanto as agendadas quanto as sob demanda por meio do BackupNow)
* Restaurar
* Parar a proteção
* Excluir dados de backup
* Adicionar política
* Excluir política
* Atualizar política
* Cancelar trabalho

Cofre de backup correspondente tooa logs da operação de tooview:

1. Navegue muito**serviços de gerenciamento de** no portal do Azure e, em seguida, clique em Olá **Logs de operação** guia.

    ![Logs de operação](./media/backup-azure-manage-vms/ops-logs.png)
2. Em filtros de saudação, selecione **Backup** como *tipo* e especifique o nome do Cofre de backup Olá na *nome do serviço* e clique em **enviar**.

    ![Filtro de logs de operação](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Nos logs de operações de saudação, selecione qualquer operação e clique em **detalhes** toosee detalhes de operação tooan correspondente.

    ![Detalhes de busca de logs de operação](./media/backup-azure-manage-vms/ops-logs-details.png)

    Olá **Assistente detalhes** contém informações sobre a operação Olá disparada, o Id de recurso em que essa operação é disparada e hora de início da operação de saudação do trabalho.

    ![Detalhes da Operação](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Notificações de alerta
Você pode obter notificações de alerta personalizadas para trabalhos de saudação no portal. Isso é possível ao definir regras de alerta do PowerShell baseadas em eventos de logs operacionais. É recomendável usar o *PowerShell versão 1.3.0 ou superior*.

toodefine tooalert uma notificação personalizada para falhas de backup, um comando de exemplo será semelhante:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: você pode obter isso no pop-up Logs de Operações, conforme descrito na seção acima. ResourceUri na janela pop-up de detalhes de uma operação é Olá ResourceId toobe fornecido para este cmdlet.

**OperationName**: esse será o formato de saudação "Microsoft.Backup/backupvault/<EventName>" onde EventName um de registrar, cancelar registro, ConfigureProtection, Backup, restauração, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**Status**: os valores com suporte são Started, Succeeded e Failed.

**ResourceGroup**: grupo de recursos do recurso de saudação no qual a operação é disparada. Você pode obter isso do valor ResourceId. Valor entre campos */resourceGroups/* e */providers/* em ResourceId valor é o valor de saudação para o grupo de recursos.

**Nome**: nome da regra de alerta de saudação.

**CustomEmail**: especificar Olá email personalizado endereço toowhich deseja toosend notificação de alerta

**SendToServiceOwners**: essa opção envia os administradores tooall de notificação de alerta e os coadministradores de assinatura de saudação. Pode ser usado no cmdlet **New-AzureRmAlertRuleEmail**

### <a name="limitations-on-alerts"></a>Limitações sobre alertas
Alertas baseados em eventos estão sujeito toohello seguintes limitações:

1. Os alertas são disparados em todas as máquinas virtuais no cofre de backup hello. Você não é possível personalizá-lo tooget alertas para um conjunto específico de máquinas virtuais em um cofre de backup.
2. Esse recurso está em Preview. [Saiba mais](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Você receberá alertas de “alerts-noreply@mail.windowsazure.com”. Atualmente você não pode modificar o remetente do email hello.

## <a name="next-steps"></a>Próximas etapas
* [Restaurar máquinas virtuais do Azure](backup-azure-restore-vms.md)
