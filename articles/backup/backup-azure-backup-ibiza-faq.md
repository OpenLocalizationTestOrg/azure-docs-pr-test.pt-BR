---
title: "perguntas Frequentes de Cofre de serviços aaaRecovery | Microsoft Docs"
description: "Esta versão do hello perguntas frequentes sobre dá suporte à versão de visualização pública de saudação do hello serviço Backup do Azure. Toofrequently respostas perguntas frequentes sobre o agente de backup hello, backup e retenção, recuperação, segurança e outras perguntas comuns sobre Olá solução de Backup do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "solução de backup; serviço de backup"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Cofre dos Serviços de Recuperação - Perguntas Frequentes
Este artigo fornece um cofre de serviços de informações específicas de tooRecovery e ela complementa a saudação [perguntas frequentes sobre o Backup do Azure](backup-azure-backup-faq.md). Olá perguntas frequentes sobre o Backup do Azure fornece um conjunto completo de saudação de perguntas e respostas sobre Olá serviço Backup do Azure.  

Você pode fazer perguntas sobre Backup do Azure no hello Disqus seção neste artigo ou um artigo relacionado. Você também pode postar perguntas sobre Olá serviço Backup do Azure no hello [Fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Os cofres dos Serviços de Recuperação se baseiam no Resource Manager. Os cofres de Backup (modo clássico) ainda têm suporte? <br/>
Sim, os cofres de Backup ainda têm suporte. Criar os cofres de Backup no hello [portal clássico](https://manage.windowsazure.com). Criar cofres dos serviços de recuperação no hello [portal do Azure](https://portal.azure.com). No entanto é altamente recomendável você toocreate recuperação Cofre de serviços como todas as melhorias futuras estarão disponível apenas no cofre de serviços de recuperação.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Posso migrar um cofre de serviços de recuperação de tooa de Cofre de Backup? <br/>
Infelizmente não, neste momento você não pode migrar conteúdo de saudação de um tooa de Cofre de Backup que Cofre de serviços de recuperação. Estamos trabalhando na adição dessa funcionalidade, mas ela não está disponível como parte da Visualização Pública.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Os cofres de Serviços de Recuperação dão suporte a VMs clássicas ou VMs com base no Gerenciador de Recursos? <br/>
Os cofres dos Serviços de Recuperação dão suporte a ambos os modelos.  Você pode fazer backup de uma VM criada no portal de clássico hello (que são máquinas virtuais de modo clássico) ou uma máquina virtual criada no hello portal do Azure (que o Gerenciador de recursos com base em) dos serviços de recuperação de tooa cofre.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Fiz backup de minhas VMs clássicas no cofre de backup. Agora quero toomigrate minhas máquinas virtuais de modo do Gerenciador de tooResource de modo clássico.  Como fazer backup delas no cofre dos serviços de recuperação?
Backups de VMs clássicos no cofre de backup não migram automaticamente o Cofre de serviços toorecovery quando você migra Olá VMs clássico tooResource modo do Gerenciador. Siga estas etapas para a migração de backups de VMs:

1. No cofre de backup, vá muito**itens protegidos** guia e selecione Olá VM. Clique em [Interromper a Proteção](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Excluir dados de backup associados***desmarcada**.
2. Em Olá [portal do Azure](https://portal.azure.com), vá toohello **extensões** menu para Olá VM e desinstalar Olá **VMSnapshot/VMSnapshotLinux** extensão.
3. Migre máquina virtual de saudação do modo do Gerenciador de tooResource de modo clássico. Certifique-se de armazenamento e rede correspondente toovirtual máquina também são migradas tooResource Manager modo.
4. Criar um cofre de serviços de recuperação e configurar backup em Olá migrados máquina virtual usando **Backup** ação na parte superior do painel do cofre. Saiba mais sobre como muito[permitir backup no cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md)
