---
title: "aaaPrepare máquinas tooset a recuperação de desastres entre regiões do Azure após a migração tooAzure usando o Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooprepare máquinas tooset a recuperação de desastres entre regiões do Azure após a migração tooAzure usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Replicar máquinas virtuais do Azure tooanother região após a migração tooAzure usando o Azure Site Recovery

>[!NOTE]
> A replicação do Azure Site Recovery para as máquinas virtuais (VMs) do Azure está atualmente na versão prévia.

## <a name="overview"></a>Visão geral

Este artigo ajuda você a preparar as máquinas virtuais do Azure para a replicação entre duas regiões do Azure depois de migrar as máquinas de um tooAzure do ambiente local por meio do Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Recuperação de desastre e conformidade
Atualmente, mais empresas estão mudando tooAzure suas cargas de trabalho. Com empresas de mover a produção de missão crítica no local tooAzure de cargas de trabalho, configuração de recuperação de desastres para essas cargas de trabalho é obrigatória para conformidade e toosafeguard contra as interrupções em uma região do Azure.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Etapas para preparar máquinas migradas para replicação
tooprepare máquinas para configurar a replicação tooanother região do Azure:

1. Migração completa.
2. Instale Olá agente do Azure, se necessário.
3. Remova o serviço de mobilidade hello.  
4. Reinicie Olá VM.

Essas etapas são descritas mais detalhadamente nas seções a seguir de saudação.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Etapa 1: Migrar cargas de trabalho em execução em VMs Hyper-V, VMs VMware e servidores físicos toorun em VMs do Azure

tooset até a replicação e migrar seu local Hyper-V, VMware e cargas de trabalho físicas tooAzure, Olá etapas a seguir no hello [migrar do Azure máquinas virtuais entre regiões do Azure com o Azure Site Recovery](site-recovery-migrate-to-azure.md) artigo. 

Após a migração, você não precise toocommit ou excluir um failover. Em vez disso, selecione Olá **concluir a migração** opção para cada máquina que você deseja toomigrate:
1. Em **itens replicados**, clique com botão direito Olá VM e clique em **concluir a migração**. Clique em **Okey** toocomplete etapa de saudação. Você pode acompanhar o progresso nas propriedades VM Olá ao monitorar o trabalho de migração completa Olá no **trabalhos de recuperação de Site**.
2. Olá **concluir a migração** ação conclui o processo de migração hello, remove a replicação para máquina hello e interrompe a cobrança de recuperação de Site para a máquina de saudação.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Etapa 2: Instale o agente de VM do Azure Olá na máquina virtual de saudação
Hello Azure [agente de VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) deve ser instalado na máquina virtual de saudação para Olá recuperação de Site extensão toowork e toohelp protegem a saudação VM.

>[!IMPORTANT]
>Começando com a versão 9.7.0.0, em máquinas virtuais do Windows, instalador do serviço de mobilidade Olá também instala hello mais recente do Azure VM agent disponíveis. Na migração, máquina virtual de saudação atende aos pré-requisitos para usar qualquer extensão VM, incluindo a extensão de recuperação de Site Olá a instalação do agente. Hello Azure VM agent necessidades toobe manualmente instalado somente se Olá serviço de mobilidade instalado Olá migrados máquina é versão 9,6 ou anterior.

Olá tabela a seguir fornece informações adicionais sobre como instalar o agente de VM hello e validar que ele foi instalado:

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalando o agente de VM Olá |Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisa de instalação de saudação do toocomplete de privilégios de administrador. |Instalar hello mais recente [agente Linux](../virtual-machines/linux/agent-user-guide.md). Você precisa de instalação de saudação do toocomplete de privilégios de administrador. É recomendável instalar o agente de saudação do seu repositório de distribuição. Estamos *não é recomendável* instalando Olá agente de VM do Linux diretamente do GitHub.  |
| Validar a instalação do agente VM Olá |1. Procure pasta C:\WindowsAzure\Packages toohello Olá VM do Azure. Você deve ver arquivos de WaAppAgent.exe hello. <br>2. Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** Olá na guia **versão do produto** campo deve ser 2.6.1198.718 ou superior. |N/D |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Etapa 3: Remover Olá serviço de mobilidade de saudação de máquina virtual migrada

Se você migrou suas máquinas do VMware no local ou servidores físicos no Windows/Linux, você precisa de toomanually remoção/desinstalação Olá mobilidade serviço da máquina virtual migrada de Olá.

>[!IMPORTANT]
>Essa etapa não é necessária para tooAzure migrado de VMs Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Desinstalar o serviço de mobilidade de saudação em uma VM do Windows Server
Use um dos Olá serviço de mobilidade métodos toouninstall Olá a seguir em um computador Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Desinstalar usando Olá da interface do usuário do Windows
1. No painel de controle do hello, selecione **programas**.
2. Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.

##### <a name="uninstall-at-a-command-prompt"></a>Desinstalar em um prompt de comando
1. Abra uma janela de Prompt de comando como administrador.
2. serviço de mobilidade em Olá toouninstall, execute o hello comando a seguir:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Desinstalar o serviço de mobilidade Olá em um computador Linux
1. No servidor Linux, entre como um usuário **raiz**.
2. Em um terminal vá muito/usuário/local/ASR.
3. serviço de mobilidade em Olá toouninstall, execute o hello comando a seguir:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Etapa 4: Reiniciar Olá VM

Depois de desinstalar o serviço de mobilidade hello, reinicialização Olá VM antes de você configurar replicação tooanother região do Azure.


## <a name="next-steps"></a>Próximas etapas
- Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).
- Saiba mais sobre as [Diretrizes de rede para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).
