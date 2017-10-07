---
title: "aaaOverview de cofres de serviços de recuperação | Microsoft Docs"
description: "Uma visão geral e a comparação entre os cofres de Serviços de Recuperação e os cofres de Backup do Azure."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Visão geral dos cofres dos Serviços de Recuperação

Este artigo descreve os recursos de saudação de um cofre de serviços de recuperação. Um cofre de Serviços de Recuperação é uma entidade de armazenamento no Azure que hospeda dados. dados de saudação normalmente são cópias de dados ou informações de configuração para máquinas virtuais (VMs), as cargas de trabalho, servidores ou estações de trabalho. Um cofre de serviços de recuperação é a versão do Gerenciador de recursos de saudação de um cofre de Backup. A Microsoft incentiva a cofres de serviços de recuperação de toouse e tooconvert cofres de serviços tooRecovery os cofres de Backup.

## <a name="what-is-a-recovery-services-vault"></a>O que é um cofre dos Serviços de Recuperação?

Um cofre de serviços de recuperação é que uma entidade de armazenamento online no Azure usada toohold dados como cópias de backup, os pontos de recuperação e as políticas de backup. Você pode usar os dados de backup de toohold de cofres de serviços de recuperação para vários serviços do Azure como VMs de IaaS (Linux ou Windows) e bancos de dados do SQL Azure. Os cofres de Serviços de Recuperação dão suporte a System Center DPM, Windows Server, Servidor de Backup do Azure e outros. Os cofres de serviços de recuperação tornam fácil tooorganize os dados de backup, minimizando a sobrecarga de gerenciamento.

Em uma assinatura do Azure, você pode criar quantos cofres dos Serviços de Recuperação desejar.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Comparação de cofres de Serviços de Recuperação e cofres de Backup

Cofres de serviços de recuperação baseados no modelo do Azure Resource Manager Olá do Azure, enquanto os cofres de Backup baseados no modelo de Gerenciador de serviço do Azure Olá. Quando você atualiza um cofre de serviços de recuperação de tooa de Cofre de Backup, os dados de backup Olá permanecem intactos durante e após o processo de atualização de saudação. Cofres de Serviços de Recuperação fornecem recursos não disponíveis a cofres de Backup, como:

- **Dados de backup seguro de toohelp recursos avançados**: serviços de recuperação com os cofres, Backup do Azure fornece segurança backups na nuvem tooprotect recursos. Esses recursos de segurança asseguram que você possa proteger seus backups e recuperar com segurança dados de backups em nuvem, mesmo que os servidores de produção e de backup sejam comprometidos. [Saiba mais](backup-azure-security-feature.md)

- **Monitoramento central para seu ambiente de TI híbrida**: com os cofres de Serviços de Recuperação, você pode monitorar não apenas suas [VMs da IaaS do Azure](backup-azure-manage-vms.md), como também seus [ativos locais](backup-azure-manage-windows-server.md#manage-backup-items) de um portal central. [Saiba mais](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **RBAC (Controle de Acesso Baseado em Função)**: o RBAC oferece controle de gerenciamento de acesso detalhado no Azure. [O Azure fornece várias funções internas](../active-directory/role-based-access-built-in-roles.md), e o Backup do Azure tem três [pontos de recuperação funções internas toomanage](backup-rbac-rs-vault.md). Os cofres de serviços de recuperação são compatíveis com RBAC, que restringe o backup e restaurar o acesso toohello definido pelo conjunto de funções de usuário. [Saiba mais](backup-rbac-rs-vault.md)

- **Proteger todas as configurações de Máquinas Virtuais do Azure**: cofres de Serviços de Recuperação protegem VMs com base no Resource Manager, incluindo Premium Disks, Managed Disks e VMs Criptografadas. Atualizando um tooa de Cofre de Backup dos serviços de recuperação cofre dá a você Olá oportunidade tooupgrade seu tooResource de VMs com base no Service Manager VMs baseadas no Gerenciador. Durante a atualização do cofre hello, você pode manter seus pontos de recuperação VM com base no Service Manager e configurar a proteção de saudação atualizado VMs (Gerenciador de recursos habilitado). [Saiba mais](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Restauração instantânea para VMs de IaaS**: cofres usando serviços de recuperação, você pode restaurar arquivos e pastas a partir de uma VM IaaS sem restaurar Olá toda a VM, que permite que os tempos de restauração mais rápidos. Restauração instantânea para VMs da IaaS está disponível para VMs Linux e Windows. [Saiba mais](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Gerenciar os cofres de serviços de recuperação no portal de saudação
Criação e gerenciamento de serviços de recuperação cofres em Olá portal do Azure é fácil porque Olá serviço de Backup é integrado a folha de configurações do Azure hello. Essa integração significa que você pode criar ou gerenciar um cofre de serviços de recuperação *no contexto de saudação do serviço de destino Olá*. Por exemplo, pontos de recuperação de saudação do tooview para uma VM, selecione-o e clique em **Backup** na folha de configurações de saudação. Olá informações de backup específico toothat VM é exibido. Em Olá seguinte exemplo, **ContosoVM** é Olá nome da máquina virtual de saudação. **ContosoVM demovault** é nome de saudação do hello Cofre de serviços de recuperação. Nome de Olá tooremember do Cofre de serviços de recuperação de saudação que armazena os pontos de recuperação Olá não é necessário, você pode acessar essas informações da máquina virtual de saudação.  

![O cofre de Serviços de Recuperação detalha a VM](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Se vários servidores protegidos usando Olá Cofre de serviços de recuperação do mesmo, talvez seja mais lógica toolook no cofre de serviços de recuperação de saudação. Você pode procurar todos os cofres de serviços de recuperação na assinatura hello e escolha uma opção na lista de saudação.

Olá seções a seguir contêm links tooarticles que explicam como toouse serviços de recuperação de um cofre em cada tipo de atividade.

### <a name="back-up-data"></a>Fazer backup de dados
- [Fazer backup de uma VM do Azure](backup-azure-vms-first-look-arm.md)
- [Fazer backup do Windows Server ou da estação de trabalho do Windows](backup-try-azure-backup-in-10-mins.md)
- [Fazer backup de tooAzure de cargas de trabalho do DPM](backup-azure-dpm-introduction.md)
- [Preparar tooback cargas de trabalho usando o servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Gerenciar pontos de recuperação
- [Gerenciar backups da VM do Azure](backup-azure-manage-vms.md)
- [Gerenciando arquivos e pastas](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Restaurar dados do cofre Olá
- [Recuperar arquivos individuais de uma VM do Azure](backup-azure-restore-files-from-vm.md)
- [Restaurar uma VM do Azure](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Cofre Olá segura
- [Protegendo dados de backup de nuvem em cofres dos Serviços de Recuperação](backup-azure-security-feature.md)



## <a name="next-steps"></a>Próximas etapas
Use Olá artigo para a seguir:</br>
[Fazer backup de uma VM IaaS](backup-azure-arm-vms-prepare.md)</br>
[Fazer backup de um Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)</br>
[Fazer backup de um Windows Server](backup-configure-vault.md)
