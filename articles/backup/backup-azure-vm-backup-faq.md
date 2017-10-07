---
title: Perguntas frequentes sobre o Backup de VM do aaaAzure | Microsoft Docs
description: "Respostas a perguntas toocommon sobre: como funciona backup da VM do Azure, limitações e o que acontece quando toopolicy alterações ocorrem"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "backup de vm do Azure, política de backup e restauração de vm do Azure"
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Perguntas sobre Olá serviço VM do Azure Backup
Este artigo possui respostas toocommon perguntas toohelp componentes de Backup de VM do Azure Olá você compreender rapidamente. Em algumas das respostas hello, há artigos de toohello links com informações abrangentes. Você também pode postar perguntas sobre Olá serviço Backup do Azure no hello [Fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Configurar o backup
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Os cofres de Serviços de Recuperação dão suporte a VMs clássicas ou VMs com base no Gerenciador de Recursos? <br/>
Os cofres dos Serviços de Recuperação dão suporte a ambos os modelos.  Você pode fazer backup de uma VM clássica (criada no portal clássico do hello) ou um tooa do Gerenciador de recursos de VM (criado no portal do Azure de saudação) Cofre de serviços de recuperação.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Quais configurações não têm suporte pelo backup de VM do Azure?
Acesse os [Sistemas operacionais com suporte](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) e [Limitações de backup de VM](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Por que não consigo ver minha VM no assistente de backup de configuração?
No Assistente de backup de configuração, o Backup do Azure lista apenas as VMs que são:
* Ainda não estiver protegido - você pode verificar o status de backup de saudação de uma VM indo tooVM folha e verificando o status de Backup no Menu de configurações da folha de saudação. Saiba mais sobre como muito[verificar o status do backup de uma VM](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Pertence toosame região como VM

## <a name="backup"></a>Backup
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>O trabalho de backup sob demanda seguirá o mesmo agendamento de retenção que os backups agendados?
Não. Período de retenção de saudação toospecify são necessários para um trabalho de backup sob demanda. Por padrão, ele será retido por 30 dias quando disparado do portal. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Eu recentemente habilitei a Criptografia de Disco do Azure em algumas VMs. Meus backups continuará toowork?
Você precisa de permissões de toogive para tooaccess de serviço de Backup do Azure Key Vault. Você pode fornecer essas permissões no PowerShell usando as etapas mencionadas na seção *Habilitar Backup* da documentação do [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Eu migrados discos de discos de toomanaged uma VM. Meus backups continuará toowork?
Sim, os backups funcionam perfeitamente e não há necessidade toore-configurar o backup. 

## <a name="restore"></a>Restaurar
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Como decidir entre a restauração de discos em comparação com a restauração completa da VM?
Pense na restauração completa da VM do Azure como uma maneira de opção de criação rápida para a VM restaurada. Restaure a VM opção irá alterar nomes de saudação de discos, contêineres usado pela interface de rede, endereços IP públicos, discos nomes de exclusividade de recursos obtendo criados como parte da criação de VM. Ele também não adicionará Olá VM tooavailability conjunto. 

Use os discos de restauração para:
* Personalizar Olá VM que é criado a partir do ponto na configuração de tempo como alterar o tamanho de saudação da configuração de backup
* Adicionar configurações que não estão presentes no momento de saudação do backup 
* Convenção de nomenclatura de saudação do controle para recursos obtendo criados
* Adicionar conjunto de tooavailability VM
* Você tem configurações que podem ser alcançadas usando apenas a definição do PowerShell/um modelo declarativo

## <a name="manage-vm-backups"></a>Gerenciar backups de VM
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>O que acontece quando altero uma política de backup nas VMs?
Quando uma nova política é aplicada em VMs, agenda e retenção de nova política de saudação serão seguidos. Se a retenção estendida, pontos de recuperação existentes serão marcados tookeep-los de acordo com a nova política. Se retenção é reduzida, eles são marcados para remoção no próximo trabalho de limpeza hello e serão excluídos. 
