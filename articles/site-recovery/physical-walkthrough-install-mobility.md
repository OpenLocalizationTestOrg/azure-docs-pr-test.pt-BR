---
title: "Olá aaaInstall serviço de mobilidade de replicação do servidor físico tooAzure | Microsoft Docs"
description: "Este artigo descreve como tooinstall Olá agente de serviço de mobilidade em servidores físicos replicando tooAzure com o serviço do Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a>Etapa 9: Instale o serviço de mobilidade Olá


Este artigo descreve como tooinstall o componente de serviço Olá mobilidade durante a replicação local tooAzure de servidores físicos do Windows/Linux, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.

Olá serviço de mobilidade captura gravações de dados em um computador e as encaminha toohello servidor de processo. Ele deve ser instalado em cada servidor que você deseja tooreplicate tooAzure.

Você pode instalar o serviço de mobilidade Olá manualmente ou recuperação de Site usando uma instalação por push de saudação processar servidor quando a replicação é habilitada, ou usando uma ferramenta como o System Center Configuration Manager. Se você usar a instalação por push, o serviço de saudação está instalado no servidor de saudação quando você habilitar a replicação.

Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalar manualmente

1. Verificar Olá [pré-requisitos](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) para instalação manual.
2. Execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) para instalação manual usando o portal de saudação.
3. Se você preferir tooinstall da linha de comando hello, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Instalar saudação do servidor de processo

Olá toopush instalação do serviço de mobilidade saudação do servidor de processo quando você habilitar a replicação para uma máquina, é necessário uma conta que pode ser usada por máquina de saudação tooaccess do servidor de processo hello. Olá conta só é usada para a instalação por push hello.

1. Se você não tiver criado uma conta, faça isso usando estas diretrizes:

    - Você pode usar uma conta local ou de domínio
    - Para Windows, se você não estiver usando uma conta de domínio, você precisa toodisable controle de acesso de usuário remoto na máquina local hello. toodo, Olá registrar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar entrada DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.
    - Entrada de registro tooadd Olá para Windows de uma CLI, digite:

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - Para o Linux, a conta de Olá deve ser raiz no servidor do hello origem Linux.

2. Em seguida, execute [estas instruções](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) se desejar que o serviço de mobilidade Olá toopush em VMs que executam o Windows ou Linux.

## <a name="other-installation-methods"></a>Outros métodos de instalação

- [Saiba mais sobre](site-recovery-install-mobility-service-using-sccm.md) instalando serviço de mobilidade hello usando o Configuration Manager
- [Saiba mais sobre](site-recovery-automate-mobility-service-install.md) como instalar com o DSC de Automação do Azure.


## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 10: habilitar a replicação](physical-walkthrough-enable-replication.md)
