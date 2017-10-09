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
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a><span data-ttu-id="0f917-103">Replicar máquinas virtuais do Azure tooanother região após a migração tooAzure usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0f917-103">Replicate Azure VMs tooanother region after migration tooAzure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="0f917-104">A replicação do Azure Site Recovery para as máquinas virtuais (VMs) do Azure está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="0f917-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="0f917-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0f917-105">Overview</span></span>

<span data-ttu-id="0f917-106">Este artigo ajuda você a preparar as máquinas virtuais do Azure para a replicação entre duas regiões do Azure depois de migrar as máquinas de um tooAzure do ambiente local por meio do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0f917-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment tooAzure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="0f917-107">Recuperação de desastre e conformidade</span><span class="sxs-lookup"><span data-stu-id="0f917-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="0f917-108">Atualmente, mais empresas estão mudando tooAzure suas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0f917-108">Today, more and more enterprises are moving their workloads tooAzure.</span></span> <span data-ttu-id="0f917-109">Com empresas de mover a produção de missão crítica no local tooAzure de cargas de trabalho, configuração de recuperação de desastres para essas cargas de trabalho é obrigatória para conformidade e toosafeguard contra as interrupções em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f917-109">With enterprises moving mission-critical on-premises production workloads tooAzure, setting up disaster recovery for these workloads is mandatory for compliance and toosafeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="0f917-110">Etapas para preparar máquinas migradas para replicação</span><span class="sxs-lookup"><span data-stu-id="0f917-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="0f917-111">tooprepare máquinas para configurar a replicação tooanother região do Azure:</span><span class="sxs-lookup"><span data-stu-id="0f917-111">tooprepare migrated machines for setting up replication tooanother Azure region:</span></span>

1. <span data-ttu-id="0f917-112">Migração completa.</span><span class="sxs-lookup"><span data-stu-id="0f917-112">Complete migration.</span></span>
2. <span data-ttu-id="0f917-113">Instale Olá agente do Azure, se necessário.</span><span class="sxs-lookup"><span data-stu-id="0f917-113">Install hello Azure agent if needed.</span></span>
3. <span data-ttu-id="0f917-114">Remova o serviço de mobilidade hello.</span><span class="sxs-lookup"><span data-stu-id="0f917-114">Remove hello Mobility service.</span></span>  
4. <span data-ttu-id="0f917-115">Reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0f917-115">Restart hello VM.</span></span>

<span data-ttu-id="0f917-116">Essas etapas são descritas mais detalhadamente nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f917-116">These steps are described in more detail in hello following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a><span data-ttu-id="0f917-117">Etapa 1: Migrar cargas de trabalho em execução em VMs Hyper-V, VMs VMware e servidores físicos toorun em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="0f917-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers toorun on Azure VMs</span></span>

<span data-ttu-id="0f917-118">tooset até a replicação e migrar seu local Hyper-V, VMware e cargas de trabalho físicas tooAzure, Olá etapas a seguir no hello [migrar do Azure máquinas virtuais entre regiões do Azure com o Azure Site Recovery](site-recovery-migrate-to-azure.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0f917-118">tooset up replication and migrate your on-premises Hyper-V, VMware, and physical workloads tooAzure, follow hello steps in hello [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="0f917-119">Após a migração, você não precise toocommit ou excluir um failover.</span><span class="sxs-lookup"><span data-stu-id="0f917-119">After migration, you don't need toocommit or delete a failover.</span></span> <span data-ttu-id="0f917-120">Em vez disso, selecione Olá **concluir a migração** opção para cada máquina que você deseja toomigrate:</span><span class="sxs-lookup"><span data-stu-id="0f917-120">Instead, select hello **Complete Migration** option for each machine you want toomigrate:</span></span>
1. <span data-ttu-id="0f917-121">Em **itens replicados**, clique com botão direito Olá VM e clique em **concluir a migração**.</span><span class="sxs-lookup"><span data-stu-id="0f917-121">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="0f917-122">Clique em **Okey** toocomplete etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f917-122">Click **OK** toocomplete hello step.</span></span> <span data-ttu-id="0f917-123">Você pode acompanhar o progresso nas propriedades VM Olá ao monitorar o trabalho de migração completa Olá no **trabalhos de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="0f917-123">You can track progress in hello VM properties by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="0f917-124">Olá **concluir a migração** ação conclui o processo de migração hello, remove a replicação para máquina hello e interrompe a cobrança de recuperação de Site para a máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f917-124">hello **Complete Migration** action completes hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="0f917-126">Etapa 2: Instale o agente de VM do Azure Olá na máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="0f917-126">Step 2: Install hello Azure VM agent on hello virtual machine</span></span>
<span data-ttu-id="0f917-127">Hello Azure [agente de VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) deve ser instalado na máquina virtual de saudação para Olá recuperação de Site extensão toowork e toohelp protegem a saudação VM.</span><span class="sxs-lookup"><span data-stu-id="0f917-127">hello Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on hello virtual machine for hello Site Recovery extension toowork and toohelp protect hello VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0f917-128">Começando com a versão 9.7.0.0, em máquinas virtuais do Windows, instalador do serviço de mobilidade Olá também instala hello mais recente do Azure VM agent disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0f917-128">Beginning with version 9.7.0.0, on Windows virtual machines, hello Mobility service installer also installs hello latest available Azure VM agent.</span></span> <span data-ttu-id="0f917-129">Na migração, máquina virtual de saudação atende aos pré-requisitos para usar qualquer extensão VM, incluindo a extensão de recuperação de Site Olá a instalação do agente.</span><span class="sxs-lookup"><span data-stu-id="0f917-129">On migration, hello virtual machine meets the agent installation prerequisite for using any VM extension, including hello Site Recovery extension.</span></span> <span data-ttu-id="0f917-130">Hello Azure VM agent necessidades toobe manualmente instalado somente se Olá serviço de mobilidade instalado Olá migrados máquina é versão 9,6 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="0f917-130">hello Azure VM agent needs toobe manually installed only if hello Mobility service installed on hello migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="0f917-131">Olá tabela a seguir fornece informações adicionais sobre como instalar o agente de VM hello e validar que ele foi instalado:</span><span class="sxs-lookup"><span data-stu-id="0f917-131">hello following table provides additional information about installing hello VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="0f917-132">**Operação**</span><span class="sxs-lookup"><span data-stu-id="0f917-132">**Operation**</span></span> | <span data-ttu-id="0f917-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="0f917-133">**Windows**</span></span> | <span data-ttu-id="0f917-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="0f917-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f917-135">Instalando o agente de VM Olá</span><span class="sxs-lookup"><span data-stu-id="0f917-135">Installing hello VM agent</span></span> |<span data-ttu-id="0f917-136">Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0f917-136">Download and install hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="0f917-137">Você precisa de instalação de saudação do toocomplete de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0f917-137">You need administrator privileges toocomplete hello installation.</span></span> |<span data-ttu-id="0f917-138">Instalar hello mais recente [agente Linux](../virtual-machines/linux/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0f917-138">Install hello latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="0f917-139">Você precisa de instalação de saudação do toocomplete de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0f917-139">You need administrator privileges toocomplete hello installation.</span></span> <span data-ttu-id="0f917-140">É recomendável instalar o agente de saudação do seu repositório de distribuição.</span><span class="sxs-lookup"><span data-stu-id="0f917-140">We recommend installing hello agent from your distribution repository.</span></span> <span data-ttu-id="0f917-141">Estamos *não é recomendável* instalando Olá agente de VM do Linux diretamente do GitHub.</span><span class="sxs-lookup"><span data-stu-id="0f917-141">We *do not recommend* installing hello Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="0f917-142">Validar a instalação do agente VM Olá</span><span class="sxs-lookup"><span data-stu-id="0f917-142">Validating hello VM agent installation</span></span> |<span data-ttu-id="0f917-143">1. Procure pasta C:\WindowsAzure\Packages toohello Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f917-143">1. Browse toohello C:\WindowsAzure\Packages folder in hello Azure VM.</span></span> <span data-ttu-id="0f917-144">Você deve ver arquivos de WaAppAgent.exe hello.</span><span class="sxs-lookup"><span data-stu-id="0f917-144">You should see hello WaAppAgent.exe file.</span></span> <br><span data-ttu-id="0f917-145">2. Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** Olá na guia **versão do produto** campo deve ser 2.6.1198.718 ou superior.</span><span class="sxs-lookup"><span data-stu-id="0f917-145">2. Right-click hello file, go too**Properties**, and then select hello **Details** tab. hello **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="0f917-146">N/D</span><span class="sxs-lookup"><span data-stu-id="0f917-146">N/A</span></span> |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a><span data-ttu-id="0f917-147">Etapa 3: Remover Olá serviço de mobilidade de saudação de máquina virtual migrada</span><span class="sxs-lookup"><span data-stu-id="0f917-147">Step 3: Remove hello Mobility service from hello migrated virtual machine</span></span>

<span data-ttu-id="0f917-148">Se você migrou suas máquinas do VMware no local ou servidores físicos no Windows/Linux, você precisa de toomanually remoção/desinstalação Olá mobilidade serviço da máquina virtual migrada de Olá.</span><span class="sxs-lookup"><span data-stu-id="0f917-148">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need toomanually remove/uninstall hello Mobility service from hello migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0f917-149">Essa etapa não é necessária para tooAzure migrado de VMs Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0f917-149">This step is not required for Hyper-V VMs migrated tooAzure.</span></span>

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="0f917-150">Desinstalar o serviço de mobilidade de saudação em uma VM do Windows Server</span><span class="sxs-lookup"><span data-stu-id="0f917-150">Uninstall hello Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="0f917-151">Use um dos Olá serviço de mobilidade métodos toouninstall Olá a seguir em um computador Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0f917-151">Use one of hello following methods toouninstall hello Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-hello-windows-ui"></a><span data-ttu-id="0f917-152">Desinstalar usando Olá da interface do usuário do Windows</span><span class="sxs-lookup"><span data-stu-id="0f917-152">Uninstall by using hello Windows UI</span></span>
1. <span data-ttu-id="0f917-153">No painel de controle do hello, selecione **programas**.</span><span class="sxs-lookup"><span data-stu-id="0f917-153">In hello Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="0f917-154">Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="0f917-154">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="0f917-155">Desinstalar em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="0f917-155">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="0f917-156">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="0f917-156">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="0f917-157">serviço de mobilidade em Olá toouninstall, execute o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f917-157">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a><span data-ttu-id="0f917-158">Desinstalar o serviço de mobilidade Olá em um computador Linux</span><span class="sxs-lookup"><span data-stu-id="0f917-158">Uninstall hello Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="0f917-159">No servidor Linux, entre como um usuário **raiz**.</span><span class="sxs-lookup"><span data-stu-id="0f917-159">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="0f917-160">Em um terminal vá muito/usuário/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="0f917-160">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="0f917-161">serviço de mobilidade em Olá toouninstall, execute o hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0f917-161">toouninstall hello Mobility service, run hello following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a><span data-ttu-id="0f917-162">Etapa 4: Reiniciar Olá VM</span><span class="sxs-lookup"><span data-stu-id="0f917-162">Step 4: Restart hello VM</span></span>

<span data-ttu-id="0f917-163">Depois de desinstalar o serviço de mobilidade hello, reinicialização Olá VM antes de você configurar replicação tooanother região do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f917-163">After you uninstall hello Mobility service, restart hello VM before you set up replication tooanother Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0f917-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f917-164">Next steps</span></span>
- <span data-ttu-id="0f917-165">Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0f917-165">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="0f917-166">Saiba mais sobre as [Diretrizes de rede para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="0f917-166">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
