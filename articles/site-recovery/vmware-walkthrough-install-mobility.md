---
title: "Olá aaaInstall serviço de mobilidade de replicação do VMware tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente de serviço de mobilidade para VMware tooAzure replicação com o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>Etapa 10: Instalar o serviço de mobilidade Olá


Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais VMware, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Olá serviço de mobilidade captura gravações de dados em um computador e as encaminha toohello servidor de processo. Ele deve ser instalado em cada computador que você deseja tooreplicate tooAzure.

Você pode instalar o manual de serviço de mobilidade hello, usando uma instalação por push do servidor de processo de recuperação de Site hello quando a replicação é habilitada, ou usar uma ferramenta do System Center Configuration Manager. Se você usar a instalação por push, o serviço de saudação está instalado na VM de saudação quando a replicação está habilitada.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalar manualmente

1. Verificar Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.
2. Execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para instalação manual usando o portal de saudação.
3. Se você preferir tooinstall da linha de comando hello, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Instalar saudação do servidor de processo

Se você quiser toopush instalação de serviço de mobilidade Olá saudação do servidor de processo quando você habilita a replicação para uma máquina virtual, você precisa de uma conta que pode ser usada por tooaccess do servidor de processo Olá Olá VM. Olá conta só é usada para a instalação por push hello.

1. Você deve ter [criado uma conta](vmware-walkthrough-prepare-vmware.md) que pode ser usado para a instalação por push. Você especificar conta Olá que desejar toouse quando você definir configurações de origem durante a implantação da recuperação de Site.
2. Em seguida, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar que o serviço de mobilidade Olá toopush em VMs que executam o Windows ou Linux.

## <a name="other-methods"></a>Outros métodos

Saiba mais sobre [instalando usando o Gerenciador de configuração de serviço de mobilidade Olá](site-recovery-install-mobility-service-using-sccm.md), ou usando [DSC de automação do Azure](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 11: habilitar a replicação](vmware-walkthrough-enable-replication.md)
