---
title: "os cofres de Backup do Azure aaaManage e servidores do Azure usando o modelo de implantação clássico Olá | Microsoft Docs"
description: Use este tutorial toolearn como toomanage Backup do Azure cofres e servidores.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Gerenciar servidores usando o modelo de implantação clássico hello e cofres de Backup do Azure
> [!div class="op_single_selector"]
> * [Gerenciador de Recursos](backup-azure-manage-windows-server.md)
> * [Clássico](backup-azure-manage-windows-server-classic.md)
>
>

Neste artigo, você encontrará uma visão geral de tarefas de gerenciamento de backup de Olá disponíveis por meio de saudação portal clássico do Azure e o agente de Backup do Microsoft Azure hello.

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
>- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

## <a name="management-portal-tasks"></a>Tarefas do portal de gerenciamento
1. Entrar toohello [Portal de gerenciamento](https://manage.windowsazure.com).
2. Clique em **dos serviços de recuperação**, clique em nome de saudação da página de início rápido do Cofre de backup tooview hello.

    ![Serviços de Recuperação](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Selecionando opções de saudação na parte superior de saudação da página de início rápido do hello, você pode ver tarefas de gerenciamento disponíveis hello.

![Gerenciar guias](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Painel
Selecione **painel** toosee visão geral de uso de saudação para o servidor de saudação. Olá **visão geral de uso** inclui:

* número de saudação de servidores Windows registrados toocloud
* número de saudação de máquinas virtuais do Azure protegidas na nuvem
* armazenamento total de saudação consumido no Azure
* status de saudação de trabalhos recentes

Na parte inferior de saudação do hello painel, você pode executar Olá tarefas a seguir:

* **Gerenciar certificado** - se um certificado foi usado tooregister Olá servidor, use este certificado de saudação tooupdate. Se estiver usando as credenciais do cofre, não use **Gerenciar certificados**.
* **Excluir** -Cofre de backup atual de saudação exclusões. Se já não estiver sendo usado um cofre de backup, você pode excluir toofree o espaço de armazenamento. **Excluir** só estará habilitada após a exclusão de todos os servidores registrados do cofre hello.

![Tarefas do painel Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Itens registrados
Selecione **itens registrados** nomes de saudação do tooview de servidores de saudação que são registrados toothis cofre.

![Itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Olá **tipo** filtrar padrões tooAzure Máquina Virtual. nomes de Olá tooview de servidores Olá cofre toothis registrado, selecione **do Windows server** de saudação menu suspenso.

Aqui você pode executar Olá tarefas a seguir:

* **Permitir novo registro** - quando essa opção é selecionada para um servidor que você pode usar Olá **Assistente de registro** em Olá Microsoft Azure Backup agent tooregister Olá servidor local com o Cofre de backup Olá uma segunda vez . Talvez seja necessário toore registro devido a erro tooan no certificado de saudação ou se um servidor tiver toobe recriado.
* **Excluir** -exclui um servidor do Cofre de backup hello. Todos os dados de saudação armazenado associados ao servidor de saudação são excluídos imediatamente.

    ![Tarefas de itens registrados](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Itens protegidos
Selecione **itens protegidos** tooview itens de saudação que foi feitos um backup de servidores de saudação.

![Itens protegidos](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Configurar
De saudação **configurar** guia, você pode selecionar a opção de redundância de armazenamento apropriado hello. Olá melhor tempo tooselect Olá redundância opção de armazenamento é logo após a criação de um cofre e antes de todas as máquinas tooit registrado.

> [!WARNING]
> Depois que um item tiver sido registrado toohello cofre, opção de redundância de armazenamento hello está bloqueada e não pode ser modificada.
>
>

![Configurar](./media/backup-azure-manage-windows-server-classic/configure.png)

Confira este artigo para saber mais sobre a [redundância de armazenamento](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Tarefas do agente de Backup do Microsoft Azure
### <a name="console"></a>Console
Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).

![Agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

De saudação **ações** disponíveis em Olá direita do console do agente de backup Olá executar Olá tarefas de gerenciamento a seguir:

* Registrar Servidor
* Agendar backup
* Fazer backup agora
* Alterar propriedades

![Ações do console do agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> muito**recuperar dados**, consulte [restaurar arquivos tooa Windows server ou o computador de cliente do Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Modificar um backup existente
1. No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. Em Olá **Assistente de agendamento de Backup** deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.

    ![Modificar um backup agendado](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Se você quiser tooadd ou alterar itens na Olá **selecionar itens tooBackup** tela clique **adicionar itens**.

    Você também pode definir **configurações de exclusão** desta página no Assistente de saudação. Se você quiser tooexclude arquivos ou tipos de arquivo de leitura procedimento Olá para adicionar [configurações de exclusão](#exclusion-settings).
4. Selecione arquivos hello e pastas que deseja tooback backup e clique **Okey**.

    ![Adicionar Itens](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Especifique a saudação **agendamento de backup** e clique em **próximo**.

    Você pode agendar backups diários (no máximo três vezes por dia) ou backups semanais.

    ![Especificar o agendamento do Backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Especificar o agendamento de backup Olá é explicado em detalhes nesta [artigo](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Selecione Olá **política de retenção** para cópia de backup hello e clique em **próximo**.

    ![Selecionar a política de retenção](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Em Olá **confirmação** tela hello Revise as informações e clique em **concluir**.
8. Depois que a conclusão do Assistente de saudação criando Olá **agendamento de backup**, clique em **fechar**.

    Depois de modificar a proteção, você pode confirmar que os backups provocarem corretamente pelo vai toohello **trabalhos** guia e confirmando que as alterações sejam refletidas no hello trabalhos de backup.

### <a name="enable-network-throttling"></a>Habilitar a limitação de rede
Agente de Backup do Azure Olá fornece uma guia de limitação que permite que você toocontrol como largura de banda de rede é usada durante a transferência de dados. Este controle pode ser útil se você precisar tooback os dados durante o horário de trabalho, mas não quiser Olá toointerfere de processo de backup com outro tráfego de internet. Transferência de limitação de dados aplica tooback backup e atividades de restauração.  

tooenable limitação:

1. Em Olá **agente de Backup**, clique em **alterar propriedades**.
2. Selecione Olá **habilitar limitação para operações de backup do uso de largura de banda de internet** caixa de seleção.

    ![Limitação de rede](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Depois que você habilitou a limitação, especificar Olá permitido largura de banda para transferir dados de backup durante **horas de trabalho** e **horas não úteis**.

    os valores de largura de banda Olá começam em 512 quilobytes por segundo (Kbps) e podem subir too1023 megabytes por segundo (Mbps). Você também pode designar início hello e Concluir para **horas de trabalho**, e quais dias da semana Olá são considerados trabalho dias. tempo de saudação fora Olá designado de horas de trabalho é considerado toobe horas de folga.
4. Clique em **OK**.

## <a name="exclusion-settings"></a>Configurações de Exclusão
1. Olá abrir **Microsoft Azure Backup agent** (você pode encontrar pesquisando seu computador para *Backup do Microsoft Azure*).

    ![Abrir agente de backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. No agente de Backup do Microsoft Azure Olá clique **agendamento de Backup**.

    ![Agendar um Backup do Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. No Assistente de agendamento de Backup de saudação deixe Olá **fazer alterações toobackup itens ou horários** opção está selecionada e clique em **próximo**.

    ![Modificar um agendamento](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Clique em **Configurações de Exclusões**.

    ![Selecione os itens tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Clique em **Adicionar Exclusão**.

    ![Adicionar exclusões](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Selecione Olá e, em seguida, clique em **Okey**.

    ![Selecionar um local para exclusão](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Adicionar extensão de arquivo hello em Olá **tipo de arquivo** campo.

    ![Excluir por tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Adição de uma extensão .mp3

    ![Exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd outra extensão, clique em **Adicionar exclusão** e insira outra extensão de tipo de arquivo (Adicionar uma extensão. JPEG).

    ![Outro exemplo de tipo de arquivo](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Quando você tiver adicionado todas as extensões de saudação, clique em **Okey**.
9. Continuar por Olá Assistente de agendamento de Backup clicando em **próximo** até Olá **página de confirmação**, em seguida, clique em **concluir**.

    ![Confirmação de exclusão](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Próximas etapas
* [Restaurar o Windows Server ou o Windows Client do Azure](backup-azure-restore-windows-server.md)
* toolearn mais sobre o Backup do Azure, consulte [visão geral do Backup do Azure](backup-introduction-to-azure-backup.md)
* Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
