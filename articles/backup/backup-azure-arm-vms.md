---
title: "aaaBack backup de máquinas virtuais do Azure | Microsoft Docs"
description: "Descobrir, registrar e fazer backup de Cofre de serviços de recuperação de tooa de máquinas virtuais do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup de máquinas virtuais; fazer backup de máquina virtual, backup e recuperação de desastres; backup de vm arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Fazer backup de máquinas virtuais do Azure cofre dos serviços de recuperação de tooa
> [!div class="op_single_selector"]
> * [Fazer backup de Cofre de serviços de tooRecovery de VMs](backup-azure-arm-vms.md)
> * [Fazer backup de máquinas virtuais tooBackup cofre](backup-azure-vms.md)
>
>

Este artigo fornece detalhes sobre como tooback backup de máquinas virtuais do Azure (Gerenciador de recursos implantados e implantado clássico) tooa serviços de recuperação do cofre. A maioria do trabalho hello para fazer backup de máquinas virtuais é preparação hello. Antes de fazer backup ou proteger uma máquina virtual, você deve concluir Olá [pré-requisitos](backup-azure-arm-vms-prepare.md) tooprepare seu ambiente para proteger suas VMs. Depois de concluir os pré-requisitos de saudação, você pode iniciar instantâneos de tootake Olá operação de backup da VM.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Para obter mais informações, consulte os artigos de saudação em [Planejando sua infra-estrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Disparo do trabalho de backup Olá
política de backup Olá associada Olá que Cofre de serviços de recuperação define a frequência e quando a operação de backup Olá é executado. Por padrão, o primeiro backup agendado de saudação é backup inicial hello. Até que ocorra o backup inicial hello, Olá Status do último Backup em Olá **trabalhos de Backup** folha mostra como **aviso (backup inicial pendente)**.

![Backup pendente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A menos que o backup inicial está vencido toobegin em breve, é recomendável que você execute **backup agora**. Olá procedimento a seguir inicia no painel do Cofre de saudação. Esse procedimento serve para executar o trabalho de backup inicial Olá depois de concluir todos os pré-requisitos. Se o trabalho de backup inicial Olá já foi executado, esse procedimento não está disponível. Olá, política de backup associada determina próximo trabalho de backup hello.  

toorun saudação inicial trabalho de backup:

1. No painel do cofre hello, clique em número de saudação em **itens de Backup**, ou clique em Olá **itens de Backup** lado a lado. <br/>
  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Olá **itens de Backup** folha é aberta.

  ![Fazer backup de itens](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Em Olá **itens de Backup** folha, item Olá select.

  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Olá **itens de Backup** lista é aberta. <br/>

  ![Trabalho de backup iniciado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Em Olá **itens de Backup** lista, clique nas reticências de saudação **...**  tooopen menu de contexto de saudação.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu.png)

  menu de contexto de saudação aparece.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. No menu de contexto de saudação, clique em **Backup agora**.

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  Fazer Backup agora folha Olá é aberto.

  ![mostra o Backup agora folha Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Olá Backup agora folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.

  ![conjunto Olá último dia Olá Backup agora o ponto de recuperação será mantido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notificações de implantação informar o trabalho de backup Olá foi disparado, e que você pode monitorar o progresso de saudação do trabalho de saudação na página de trabalhos de Backup hello. Dependendo do tamanho de saudação da VM, criar backup de saudação inicial pode demorar um pouco.

6. status de saudação tooview ou rastrear do backup inicial hello, no painel do cofre hello, em Olá **trabalhos de Backup** bloco clique **em andamento**.

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Abre a folha de trabalhos de Backup de saudação.

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Em Olá **trabalhos de Backup** folha, você pode ver o status de saudação de todos os trabalhos. Verifique se o trabalho de backup Olá para sua VM ainda está em andamento ou se ele tiver sido concluída. Quando um trabalho de backup for concluído, o status de saudação é *concluído*.

  > [!NOTE]
  > Como parte da operação de backup hello, Olá serviço Backup do Azure emite uma extensão de backup de toohello do comando em cada tooflush VM todas as gravações e tirar um instantâneo consistente.
  >
  >

## <a name="troubleshooting-errors"></a>Solucionar erros
Se você tiver problemas durante a cópia sua máquina virtual, consulte Olá [artigo de solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.

## <a name="next-steps"></a>Próximas etapas
Agora que você protegeu sua VM, consulte Olá toolearn artigos sobre tarefas de gerenciamento de VM, a seguir e como toorestore VMs.

* [Gerenciar e monitorar suas máquinas virtuais](backup-azure-manage-vms.md)
* [Restaurar máquinas virtuais](backup-azure-arm-restore-vms.md)
