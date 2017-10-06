---
title: "servidores e cofres de serviços aaaManage recuperação do Azure | Microsoft Docs"
description: "Use este tutorial toolearn como os serviços de recuperação do Azure toomanage cofres e servidores."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Monitore e gerencie os cofres dos serviços de recuperação do Azure e os servidores para os computadores que usam o Windows
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](backup-azure-manage-windows-server.md)
> * [Clássico](backup-azure-manage-windows-server-classic.md)
>
>

Neste artigo você encontrará uma visão geral da saudação monitor e gerenciamento de tarefas de backup disponíveis por meio de saudação agente de Backup do Microsoft Azure hello e portal do Azure. Este artigo pressupõe que você já tem uma assinatura do Azure e já criou pelo menos um cofre dos Serviços de Recuperação.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Abrir um cofre dos Serviços de Recuperação

painel do Cofre de serviços de recuperação de saudação mostra detalhes de saudação ou atributos de um cofre de serviços de recuperação.

1. Entrar toohello [Portal do Azure](https://portal.azure.com/) usando sua assinatura do Azure.
2. No menu de Hub hello, clique em **mais serviços**.

    ![Abrir a lista de cofres dos Serviços de Recuperação, etapa 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Você deseja tooopen um cofre de serviços de recuperação. Na caixa de diálogo hello, comece a digitar **dos serviços de recuperação**. Como começar a digitar, lista Olá filtra com base em sua entrada. Clique em **os cofres de serviços de recuperação** cofres de lista de saudação toodisplay dos serviços de recuperação em sua assinatura.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    saudação de lista de cofres de serviços de recuperação é aberta.

    ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. Na lista de saudação de cofres, selecione o nome de saudação do hello Cofre de serviços de recuperação você deseja tooopen. Abre a folha de painel de Cofre de serviços de recuperação Hello.

    ![painel do cofre dos serviços de recuperação](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Agora que você abriu o Cofre de serviços de recuperação hello, tente qualquer uma das tarefas de monitoramento ou gerenciamento de saudação.

## <a name="monitor-backup-jobs-and-alerts"></a>Monitorar trabalhos e alertas de backup

Monitorar trabalhos e alertas de saudação dos serviços de recuperação cofre dashboard, onde você pode ver:

* Detalhes dos alertas de backup
* Arquivos e pastas, bem como máquinas virtuais do Azure protegidas na nuvem Olá
* Armazenamento total consumido no Azure
* Status do trabalho de backup

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Informações de saudação em cada um desses blocos abre Olá folha associado onde você gerencia as tarefas relacionadas.

Da parte superior de saudação do hello painel:

* As configurações fornecem acesso às tarefas de backup disponíveis.
* Cofre de backup - backup novos arquivos e pastas (ou máquinas virtuais do Azure) dos serviços de recuperação de toohello de Ajuda.
* Excluir - se uma recuperação o Cofre de serviços não está sendo usado, você poderá excluí-la toofree o espaço de armazenamento. Delete só estará habilitada após a exclusão de todos os servidores protegidos do cofre hello.

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Alertas de backups usando o agente de backup do Azure:
| Nível de alerta | Alertas enviados |
| --- | --- |
| Crítico |Falha de backup, falha na recuperação |
| Aviso |Backup foi concluído com avisos (quando menos de 100 arquivos sem backup devido a problemas de toocorruption e mais de um milhão de arquivos é feito com êxito) |
| Informativo |Nenhum |

## <a name="manage-backup-alerts"></a>Gerenciar alertas de Backup
Clique em Olá **alertas de Backup** bloco tooopen Olá **alertas de Backup** folha e gerenciar alertas.

![Alertas de Backup](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

Alertas de Backup Olá bloco mostra Olá número de:

* alertas críticos não resolvidos nas últimas 24 horas
* alertas de aviso não resolvidos nas últimas 24 horas

Clicando em cada um desses links leva toohello **alertas de Backup** folha com uma exibição filtrada desses alertas (crítico ou de aviso).

Na folha de alertas de Backup hello, você:

* Escolha Olá informações apropriadas tooinclude com seus alertas.

    ![Escolher colunas](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Filtra os alertas quanto à gravidade, status e horários de início/término.

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Configura as notificações quanto à gravidade, frequência e destinatários, bem como ativa ou desativa os alertas.

    ![Filtrar alertas](./media/backup-azure-manage-windows-server/configure-notifications.png)

Se **por alerta** é selecionado como Olá **notificar** frequência nenhum agrupamento ou redução nos emails ocorre. Cada alerta resulta em uma notificação. Essa é a configuração de padrão de saudação e email de resolução Olá também é enviada imediatamente.

Se **Digest por hora** é selecionado como Olá **notificar** frequência um email é enviado toohello usuário informando que há não resolvido novos alertas gerados no hello última hora. Um email de resolução é enviado no final de saudação de hora hello.

Alertas podem ser enviados para Olá níveis de severidade a seguir:

* Crítico
* Aviso
* informações

Desativar alerta Olá Olá **desativar** botão na folha de detalhes do trabalho de saudação. Quando você clica em desativar, pode fornecer observações de resolução.

Escolher colunas Olá deseja tooappear como parte do alerta Olá Olá **escolher colunas** botão.

> [!NOTE]
> De saudação **configurações** folha, gerenciar alertas de backup selecionando **monitoramento e relatórios > alertas e eventos > alertas de Backup** e, em seguida, clicando em **filtro** ou  **Configurar notificações**.
>
>

## <a name="manage-backup-items"></a>Gerenciar itens de Backup
Gerenciar backups locais agora está disponível no portal de gerenciamento de saudação. Na seção de Backup de saudação do painel hello, Olá **itens de Backup** bloco mostra o número de saudação de itens de backup protegidos toohello cofre.

Clique em **pastas de arquivos** em Olá Backup itens lado a lado.

![Bloco Itens de backup](./media/backup-azure-manage-windows-server/backup-items-tile.png)

Itens de Backup Olá folha abre com hello filtrar conjunto tooFile-pasta onde você pode ver cada backup específico item listado.

![Itens de Backup](./media/backup-azure-manage-windows-server/backup-item-list.png)

Se você selecionar um item de backup específico na lista de hello, você verá detalhes essenciais de Olá para aquele item.

> [!NOTE]
> De saudação **configurações** folha, gerenciar arquivos e pastas selecionando **itens protegidos > itens de Backup** e, em seguida, selecionando **pastas de arquivos** de saudação menu suspenso.
>
>

![Itens de backup das configurações](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Gerenciar trabalhos de Backup
Trabalhos de backup para local (quando o servidor de local de saudação do backup de tooAzure) e backups do Azure são visíveis no painel de saudação.

Olá seção de Backup Olá painel, bloco de trabalho de Backup Olá mostra número saudação de trabalhos:

* em andamento
* Falha no hello últimas 24 horas.

toomanage os trabalhos de backup, clique em Olá **trabalhos de Backup** lado a lado, que abre a folha de trabalhos de Backup de saudação.

![Itens de backup das configurações](./media/backup-azure-manage-windows-server/backup-jobs.png)

Modificar Olá informações disponíveis na folha de trabalhos de Backup Olá com hello **escolher colunas** botão na parte superior de saudação da página de saudação.

Saudação de uso **filtro** tooselect botão entre arquivos e pastas e backup de máquina virtual do Azure.

Se você não vir os arquivos e pastas, clique em **filtro** botão na parte superior de saudação da página hello e selecione **arquivos e pastas** no menu de tipo de Item de saudação.

> [!NOTE]
> De saudação **configurações** folha, gerenciar trabalhos de backup selecionando **monitoramento e relatórios > trabalhos > trabalhos de Backup** e, em seguida, selecionando **pastas de arquivos** de descarte de saudação menu.
>
>

## <a name="monitor-backup-usage"></a>Monitorar o uso do Backup
Olá seção de Backup Olá painel, bloco de uso do Backup de saudação mostra armazenamento Olá consumido no Azure. O uso do armazenamento é fornecido para:

* Uso de armazenamento LRS de nuvem associado Olá cofre
* A utilização de armazenamento GRS associada Olá cofre em nuvem

## <a name="manage-your-production-servers"></a>Gerenciar seus servidores de produção
clique de seus servidores de produção, toomanage **configurações**.

Em Gerenciar, clique em **Infraestrutura do Backup > Servidores de Produção**.

listas de folha de servidores de produção de Hello de todos os servidores de produção disponíveis. Clique em um servidor em detalhes do servidor de saudação lista tooopen hello.

![Itens protegidos](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Agente de Backup do Azure Olá aberto
Olá abrir **Microsoft Azure Backup agent** (seja pesquisando seu computador para *Backup do Microsoft Azure*).

![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

De saudação **ações** disponíveis em Olá direita do console do agente de backup Olá executar Olá tarefas de gerenciamento a seguir:

* Registrar Servidor
* Agendar backup
* Fazer backup agora
* Alterar propriedades

![Ações do console do agente de Backup do Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> muito**recuperar dados**, consulte [restaurar arquivos tooa Windows server ou o computador de cliente do Windows](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Modificar agendamento de backup Olá
1. No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. Em Olá **Assistente de agendamento de Backup** deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Se você quiser tooadd ou alterar itens na Olá **selecionar itens tooBackup** tela clique **adicionar itens**.

    Você também pode definir **configurações de exclusão** desta página no Assistente de saudação. Se você quiser tooexclude arquivos ou tipos de arquivo de leitura procedimento Olá para adicionar [configurações de exclusão](#manage-exclusion-settings).
4. Selecione arquivos hello e pastas que deseja tooback backup e clique **Okey**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Especifique a saudação **agendamento de backup** e clique em **próximo**.

    Você pode agendar backups diários (no máximo três vezes por dia) ou backups semanais.

    ![Itens para o backup do Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Especificar o agendamento de backup Olá é explicado em detalhes nesta [artigo](backup-azure-backup-cloud-as-tape.md).
   >

6. Selecione Olá **política de retenção** para cópia de backup hello e clique em **próximo**.

    ![Itens para o backup do Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Em Olá **confirmação** tela hello Revise as informações e clique em **concluir**.
8. Depois que a conclusão do Assistente de saudação criando Olá **agendamento de backup**, clique em **fechar**.

    Depois de modificar a proteção, você pode confirmar que os backups provocarem corretamente pelo vai toohello **trabalhos** guia e confirmando que as alterações sejam refletidas no hello trabalhos de backup.

## <a name="enable-network-throttling"></a>Habilitar a limitação de rede

Agente de Backup do Azure Olá fornece uma guia de limitação que permite que você toocontrol como largura de banda de rede é usada durante a transferência de dados. Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de internet. Transferência de limitação de dados aplica tooback backup e atividades de restauração.  

tooenable limitação:

1. Em Olá **agente de Backup**, clique em **alterar propriedades**.
2. Em hello * * limitação guia, selecione **habilitar limitação para operações de backup do uso de largura de banda de internet**.

    ![Limitação de rede](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Depois que você habilitou a limitação, especificar Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.

    os valores de largura de banda Olá começam em 512 quilobytes por segundo (Kbps) e podem subir too1023 megabytes por segundo (Mbps). Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são considerados trabalho dias. tempo de saudação fora Olá designado de horas de trabalho é considerado toobe horas de folga.
3. Clique em **OK**.

## <a name="manage-exclusion-settings"></a>Gerenciar configurações de exclusão
1. Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. No Assistente de agendamento de Backup de saudação deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Clique em **Configurações de Exclusões**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Clique em **Adicionar Exclusão**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Selecione Olá e, em seguida, clique em **Okey**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Adicionar extensão de arquivo hello em Olá **tipo de arquivo** campo.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Adição de uma extensão .mp3

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd outra extensão, clique em **Adicionar exclusão** e insira outra extensão de tipo de arquivo (Adicionar uma extensão. JPEG).

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Quando você tiver adicionado todas as extensões de saudação, clique em **Okey**.
9. Continuar por Olá Assistente de agendamento de Backup clicando em **próximo** até Olá **página de confirmação**, em seguida, clique em **concluir**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Perguntas frequentes
**1º TRIMESTRE. status do trabalho de backup Olá mostra como concluída no hello agente de backup do Azure, porque não ele sejam refletido imediatamente no portal?**

R1. Há é em atraso máximo de 15 minutos entre o status do trabalho de backup Olá refletido no hello agente de backup do Azure e Olá portal do Azure.

**Q.2 quando um trabalho de backup falhar, quanto tempo leva tooraise um alerta?**

A. 2 um alerta é gerado dentro de 20 minutos de saudação falha de backup do Azure.

**P3. Há um caso em que um email não será enviado se as notificações forem configuradas?**

R3. Abaixo estão casos hello quando Olá notificação não será enviada em ruído de alerta tooreduce Olá ordem:

* Se as notificações são configuradas por hora e um alerta é gerado e resolvido na hora de saudação
* o Trabalho será cancelado.
* O segundo trabalho de backup falhou porque o trabalho de backup original estava em andamento.

## <a name="troubleshooting-monitoring-issues"></a>Solucionando problemas de monitoramento
**Problema:** trabalhos de e/ou alertas do agente de Backup do Azure Olá não aparecem no portal de saudação.

**Etapas de solução de problemas:** Olá processo, ```OBRecoveryServicesManagementAgent```, envia Olá toohello dados alerta e trabalho de serviço de Backup do Azure. Ocasionalmente, esse processo pode ficar travado ou ser interrompido.

1. processo de saudação tooverify não está em execução, abra **Gerenciador de tarefas** e verifique se hello ```OBRecoveryServicesManagementAgent``` processo está sendo executado.
2. Supondo que o processo de saudação não está em execução, abra **painel de controle** e navegue Olá lista de serviços. Inicie ou reinicie o **agente de gerenciamento dos Serviços de Recuperação do Microsoft Azure**.

    Para obter mais informações, procure logs de saudação em:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Por exemplo:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Próximas etapas
* [Restaurar o Windows Server ou o Windows Client do Azure](backup-azure-restore-windows-server.md)
* toolearn mais sobre o Backup do Azure, consulte [visão geral do Backup do Azure](backup-introduction-to-azure-backup.md)
* Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
