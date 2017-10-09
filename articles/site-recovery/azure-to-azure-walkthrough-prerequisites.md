---
title: "aaaBefore você iniciar a replicação de máquinas virtuais do Azure tooanother região | Microsoft Docs"
description: "Resume as etapas de saudação precisar tootake antes de replicar máquinas virtuais do Azure entre regiões do Azure, usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Etapa 2: antes de iniciar

Depois que você tiver examinado Olá [arquitetura](azure-to-azure-walkthrough-architecture.md) para replicar máquinas virtuais (VMs) do Azure entre regiões do Azure com [do Azure Site Recovery](site-recovery-overview.md), pré-requisitos de tooverify neste artigo. 

- Quando você terminar de artigo hello, você deve ter uma clara compreensão sobre o que é necessário a implantação de saudação toomake trabalhar e concluiu as etapas de pré-requisito hello.
- Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> Atualmente, a replicação de VM do Azure está em versão prévia.



## <a name="support-recommendations"></a>Recomendações de suporte

Tabela de saudação de revisão abaixo.

**Componente** | **Requisito**
--- | ---
**Cofre dos Serviços de Recuperação** | É recomendável que você crie um cofre de serviços de recuperação no destino Olá região do Azure que você deseja toouse para recuperação de desastres. Por exemplo, se você quiser tooreplicate fonte VMs no Leste dos EUA tooCentral dos EUA, crie cofre Olá no centro dos EUA.
**Assinatura do Azure** | Sua assinatura do Azure deve ser habilitado toocreate VMs, no local de destino Olá que você deseja toouse como a região de recuperação de desastres hello. Contate o suporte tooenable Olá cota necessária.
**Capacidade da região de destino** | Destino Olá região do Azure, Olá assinatura deve ter capacidade suficiente para VMs, contas de armazenamento e componentes de rede.
**Armazenamento** | Saudação de uso [diretrizes de armazenamento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para sua fonte de VMs do Azure, tooavoid problemas de desempenho.<br/><br/> Contas de armazenamento devem estar no hello mesma região Olá cofre.<br/><br/> Você não pode replicar contas toopremium no centro e Sul da Índia.<br/><br/> Se você implantar a replicação com as configurações padrão de saudação, recuperação de Site cria contas de armazenamento Olá necessárias com base na configuração de fonte de saudação. Se você personalizar as configurações, siga Olá [alvos de escalabilidade para discos de VM](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Rede** | É necessário ter conectividade de saída de tooallow de VMs do Azure, para intervalos específicos de URLs/IP.<br/><br/> Contas de rede devem estar no hello mesma região Olá cofre. 
**VM do Azure** | Verifique se que todos os certificados raiz da mais recentes Olá estão em Olá VM do Windows/Linux do Azure. Se não estiver, não será capaz de tooregister Olá VM na recuperação de Site, devido a restrições de segurança.
**Conta de usuário do Azure** | Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma máquina virtual do Azure.

Obter uma lista completa dos requisitos de suporte em Olá [matriz de suporte](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Definir permissões na conta de saudação

1. Leia sobre Olá [permissões](site-recovery-role-based-linked-access-control.md) é necessário para replicação.
2. Siga estas [instruções](../active-directory/role-based-access-control-configure.md#add-access) tooadd permissões.


## <a name="verify-target-resources"></a>Verifique os recursos de destino

1. Ativar sua assinatura do Azure tooallow toocreate VMs em Olá destino região que você deseja toouse para recuperação de desastres que você deseja toouse como a região de recuperação de desastres hello. Contate o suporte tooenable Olá cota necessária.
2. Verifique se que sua assinatura tem suficiente tooenable recursos VMs com tamanhos que corresponde a sua fonte de VMs. Por padrão, quando configurar a replicação, recuperação de Site escolhe Olá mesmo tamanho para Olá VM de destino ou Olá tamanho possível mais próximo. Saiba mais sobre a [solução de problemas](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) de recursos de destino.

## <a name="verify-azure-vm-certificates"></a>Verifique os certificados de VM do Azure

1. Verifique se todos os certificados raiz mais recentes de saudação estão presentes no Windows hello ou VMs do Linux que você deseja tooreplicate. Se os certificados raiz mais recentes de saudação não estiverem presentes, Olá VM não pode ser registrado tooSite recuperação devido a restrições de toosecurity.
2. Para VMs do Windows hello a seguir:

    - Instale todas as atualizações do Windows mais recentes Olá em Olá VM para que todos os certificados de raiz confiável do hello estiverem na máquina de saudação.
    - Em um ambiente desconectado, siga saudação padrão Windows Update processo/certificado processo de atualização em sua organização, certificados de raiz tooget hello mais recentes e CRL atualizada, em VMs de saudação.
3. Para VMs do Linux, siga orientação Olá fornecida pelo seu Linux distribuidor tooget hello mais recentes certificados raiz confiáveis e hello mais recente lista de certificados revogados no hello VM. Saiba mais sobre a [solução de problemas](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) para problemas de raiz confiável.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 3: planejar a rede](azure-to-azure-walkthrough-network.md) tooset a conectividade de saída.
