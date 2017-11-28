---
title: "Preparar computadores para configurar a recuperação de desastre entre regiões do Azure após a migração para o Azure usando o Site Recovery | Microsoft Docs"
description: "Este artigo descreve como preparar computadores para configurar a recuperação de desastre entre regiões do Azure após a migração para o Azure usando o Azure Site Recovery."
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
ms.openlocfilehash: 2aee0fb8d1ba1ff1584bee91b4d1cc34b654d97f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-to-another-region-after-migration-to-azure-by-using-azure-site-recovery"></a><span data-ttu-id="d7e42-103">Replicar VMs do Azure para outra região após a migração para o Azure usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d7e42-103">Replicate Azure VMs to another region after migration to Azure by using Azure Site Recovery</span></span>

>[!NOTE]
> <span data-ttu-id="d7e42-104">A replicação do Azure Site Recovery para as máquinas virtuais (VMs) do Azure está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="d7e42-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

## <a name="overview"></a><span data-ttu-id="d7e42-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d7e42-105">Overview</span></span>

<span data-ttu-id="d7e42-106">Este artigo ajuda você a preparar as máquinas virtuais do Azure para a replicação entre duas regiões do Azure depois que essas máquinas foram migradas de um ambiente local para o Azure usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d7e42-106">This article helps you prepare Azure virtual machines for replication between two Azure regions after these machines have been migrated from an on-premises environment to Azure by using Azure Site Recovery.</span></span>

## <a name="disaster-recovery-and-compliance"></a><span data-ttu-id="d7e42-107">Recuperação de desastre e conformidade</span><span class="sxs-lookup"><span data-stu-id="d7e42-107">Disaster recovery and compliance</span></span>
<span data-ttu-id="d7e42-108">Atualmente, mais empresas estão adotando as cargas de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-108">Today, more and more enterprises are moving their workloads to Azure.</span></span> <span data-ttu-id="d7e42-109">Com as empresas movendo as cargas de trabalho de produção locais e essenciais do Azure, configurar a recuperação de desastre para essas cargas de trabalho é obrigatório para a conformidade e segurança contra as interrupções em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-109">With enterprises moving mission-critical on-premises production workloads to Azure, setting up disaster recovery for these workloads is mandatory for compliance and to safeguard against any disruptions in an Azure region.</span></span>

## <a name="steps-for-preparing-migrated-machines-for-replication"></a><span data-ttu-id="d7e42-110">Etapas para preparar máquinas migradas para replicação</span><span class="sxs-lookup"><span data-stu-id="d7e42-110">Steps for preparing migrated machines for replication</span></span>
<span data-ttu-id="d7e42-111">Para preparar máquinas migradas para configurar a replicação para outra região do Azure:</span><span class="sxs-lookup"><span data-stu-id="d7e42-111">To prepare migrated machines for setting up replication to another Azure region:</span></span>

1. <span data-ttu-id="d7e42-112">Migração completa.</span><span class="sxs-lookup"><span data-stu-id="d7e42-112">Complete migration.</span></span>
2. <span data-ttu-id="d7e42-113">Instale o agente do Azure, se necessário.</span><span class="sxs-lookup"><span data-stu-id="d7e42-113">Install the Azure agent if needed.</span></span>
3. <span data-ttu-id="d7e42-114">Remova o Serviço de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="d7e42-114">Remove the Mobility service.</span></span>  
4. <span data-ttu-id="d7e42-115">Reinicie a VM.</span><span class="sxs-lookup"><span data-stu-id="d7e42-115">Restart the VM.</span></span>

<span data-ttu-id="d7e42-116">Essas etapas estão descritas com mais detalhes nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="d7e42-116">These steps are described in more detail in the following sections.</span></span>

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-to-run-on-azure-vms"></a><span data-ttu-id="d7e42-117">Etapa 1: migre cargas de trabalho em execução em VMs do Hyper-V locais, VMs VMware e servidores físicos para execução em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="d7e42-117">Step 1: Migrate workloads running on Hyper-V VMs, VMware VMs, and physical servers to run on Azure VMs</span></span>

<span data-ttu-id="d7e42-118">Para configurar a replicação e migrar suas cargas de trabalho do Hyper-V, VMware e físicas locais para o Azure, siga as etapas no artigo [Migrar máquinas virtuais IaaS do Azure entre regiões do Azure com o Azure Site Recovery](site-recovery-migrate-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d7e42-118">To set up replication and migrate your on-premises Hyper-V, VMware, and physical workloads to Azure, follow the steps in the [Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery](site-recovery-migrate-to-azure.md) article.</span></span> 

<span data-ttu-id="d7e42-119">Depois da migração, você não precisa confirmar excluir um failover.</span><span class="sxs-lookup"><span data-stu-id="d7e42-119">After migration, you don't need to commit or delete a failover.</span></span> <span data-ttu-id="d7e42-120">Em vez disso, você seleciona a opção **Migração Completa** para cada computador que deseja migrar:</span><span class="sxs-lookup"><span data-stu-id="d7e42-120">Instead, select the **Complete Migration** option for each machine you want to migrate:</span></span>
1. <span data-ttu-id="d7e42-121">Em **Itens Replicados**, clique com botão direito na VM e clique em **Concluir a Migração**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-121">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="d7e42-122">Clique em **OK** para concluir a etapa.</span><span class="sxs-lookup"><span data-stu-id="d7e42-122">Click **OK** to complete the step.</span></span> <span data-ttu-id="d7e42-123">Você pode acompanhar o progresso nas propriedades da VM, monitorando o trabalho de Migração Completa em **trabalhos do Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-123">You can track progress in the VM properties by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
2. <span data-ttu-id="d7e42-124">A ação **Concluir Migração** conclui o processo de migração, remove a replicação da máquina e interrompe a cobrança do Site Recovery para o computador.</span><span class="sxs-lookup"><span data-stu-id="d7e42-124">The **Complete Migration** action completes the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-the-azure-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="d7e42-126">Etapa 2: instale o agente da VM do Azure na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d7e42-126">Step 2: Install the Azure VM agent on the virtual machine</span></span>
<span data-ttu-id="d7e42-127">O [agente da VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) do Azure deve ser instalado na máquina virtual para a extensão do Site Recovery para trabalhar e ajudar a proteger a VM.</span><span class="sxs-lookup"><span data-stu-id="d7e42-127">The Azure [VM agent](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) must be installed on the virtual machine for the Site Recovery extension to work and to help protect the VM.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d7e42-128">A partir da versão 9.7.0.0, em máquinas virtuais do Windows, o instalador do Serviço de mobilidade também instala o último agente da VM do Azure disponível.</span><span class="sxs-lookup"><span data-stu-id="d7e42-128">Beginning with version 9.7.0.0, on Windows virtual machines, the Mobility service installer also installs the latest available Azure VM agent.</span></span> <span data-ttu-id="d7e42-129">Sobre a migração, a máquina virtual atende aos pré-requisitos de instalação do agente para usar qualquer extensão da VM, incluindo a extensão do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d7e42-129">On migration, the virtual machine meets the agent installation prerequisite for using any VM extension, including the Site Recovery extension.</span></span> <span data-ttu-id="d7e42-130">O agente da VM do Azure precisa ser instalado manualmente somente se o Serviço de mobilidade instalado no computador migrado for versão 9.6 ou anterior.</span><span class="sxs-lookup"><span data-stu-id="d7e42-130">The Azure VM agent needs to be manually installed only if the Mobility service installed on the migrated machine is version 9.6 or earlier.</span></span>

<span data-ttu-id="d7e42-131">A tabela a seguir fornece informações adicionais sobre como instalar o agente da VM e validar que ele foi instalado:</span><span class="sxs-lookup"><span data-stu-id="d7e42-131">The following table provides additional information about installing the VM agent and validating that it was installed:</span></span>

| <span data-ttu-id="d7e42-132">**Operação**</span><span class="sxs-lookup"><span data-stu-id="d7e42-132">**Operation**</span></span> | <span data-ttu-id="d7e42-133">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d7e42-133">**Windows**</span></span> | <span data-ttu-id="d7e42-134">**Linux**</span><span class="sxs-lookup"><span data-stu-id="d7e42-134">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d7e42-135">Instalando o agente de VM</span><span class="sxs-lookup"><span data-stu-id="d7e42-135">Installing the VM agent</span></span> |<span data-ttu-id="d7e42-136">Baixe e instale o [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d7e42-136">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="d7e42-137">Você precisa de privilégios de administrador para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="d7e42-137">You need administrator privileges to complete the installation.</span></span> |<span data-ttu-id="d7e42-138">Instale o [agente Linux](../virtual-machines/linux/agent-user-guide.md) mais recente.</span><span class="sxs-lookup"><span data-stu-id="d7e42-138">Install the latest [Linux agent](../virtual-machines/linux/agent-user-guide.md).</span></span> <span data-ttu-id="d7e42-139">Você precisa de privilégios de administrador para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="d7e42-139">You need administrator privileges to complete the installation.</span></span> <span data-ttu-id="d7e42-140">É recomendável instalar o agente do seu repositório de distribuição.</span><span class="sxs-lookup"><span data-stu-id="d7e42-140">We recommend installing the agent from your distribution repository.</span></span> <span data-ttu-id="d7e42-141">*Não é recomendável* instalar o agente de VM Linux diretamente do GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7e42-141">We *do not recommend* installing the Linux VM agent directly from GitHub.</span></span>  |
| <span data-ttu-id="d7e42-142">Validação da instalação do agente de VM</span><span class="sxs-lookup"><span data-stu-id="d7e42-142">Validating the VM agent installation</span></span> |<span data-ttu-id="d7e42-143">1. Navegue até a pasta :\WindowsAzure\Packages na VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-143">1. Browse to the C:\WindowsAzure\Packages folder in the Azure VM.</span></span> <span data-ttu-id="d7e42-144">Você deve ver o arquivo WaAppAgent.exe.</span><span class="sxs-lookup"><span data-stu-id="d7e42-144">You should see the WaAppAgent.exe file.</span></span> <br><span data-ttu-id="d7e42-145">2. Clique com o botão direito do mouse no arquivo, vá para **Propriedades** e selecione a guia **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-145">2. Right-click the file, go to **Properties**, and then select the **Details** tab.</span></span> <span data-ttu-id="d7e42-146">O campo **Versão do Produto** deve ser 2.6.1198.718 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="d7e42-146">The **Product Version** field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="d7e42-147">N/D</span><span class="sxs-lookup"><span data-stu-id="d7e42-147">N/A</span></span> |


### <a name="step-3-remove-the-mobility-service-from-the-migrated-virtual-machine"></a><span data-ttu-id="d7e42-148">Etapa 3: remova o serviço de Mobilidade da máquina virtual migrada</span><span class="sxs-lookup"><span data-stu-id="d7e42-148">Step 3: Remove the Mobility service from the migrated virtual machine</span></span>

<span data-ttu-id="d7e42-149">Se migrou suas máquinas do VMware locais ou servidores físicos no Windows/Linux, você precisa remover/desinstalar manualmente o Serviço de mobilidade da máquina virtual migrada.</span><span class="sxs-lookup"><span data-stu-id="d7e42-149">If you have migrated your on-premises VMware machines or physical servers on Windows/Linux, you need to manually remove/uninstall the Mobility service from the migrated virtual machine.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d7e42-150">Esta etapa não é necessária para VMs do Hyper-V migradas para o Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-150">This step is not required for Hyper-V VMs migrated to Azure.</span></span>

#### <a name="uninstall-the-mobility-service-on-a-windows-server-vm"></a><span data-ttu-id="d7e42-151">Desinstalar o Serviço de mobilidade de uma VM do Windows Server</span><span class="sxs-lookup"><span data-stu-id="d7e42-151">Uninstall the Mobility service on a Windows Server VM</span></span>
<span data-ttu-id="d7e42-152">Use um dos métodos a seguir para desinstalar o Serviço de mobilidade em um computador Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d7e42-152">Use one of the following methods to uninstall the Mobility service on a Windows Server computer.</span></span>

##### <a name="uninstall-by-using-the-windows-ui"></a><span data-ttu-id="d7e42-153">Desinstalar usando a interface do usuário do Windows</span><span class="sxs-lookup"><span data-stu-id="d7e42-153">Uninstall by using the Windows UI</span></span>
1. <span data-ttu-id="d7e42-154">No Painel de Controle, selecione **Programas**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-154">In the Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="d7e42-155">Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

##### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="d7e42-156">Desinstalar em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="d7e42-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="d7e42-157">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="d7e42-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="d7e42-158">Para desinstalar o Serviço de mobilidade, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d7e42-158">To uninstall the Mobility service, run the following command:</span></span>

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-the-mobility-service-on-a-linux-computer"></a><span data-ttu-id="d7e42-159">Desinstalar o Serviço de mobilidade de um computador Linux</span><span class="sxs-lookup"><span data-stu-id="d7e42-159">Uninstall the Mobility service on a Linux computer</span></span>
1. <span data-ttu-id="d7e42-160">No servidor Linux, entre como um usuário **raiz**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="d7e42-161">Em um terminal, acesse /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="d7e42-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="d7e42-162">Para desinstalar o Serviço de mobilidade, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d7e42-162">To uninstall the Mobility service, run the following command:</span></span>

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-the-vm"></a><span data-ttu-id="d7e42-163">Etapa 4: reinicie a VM</span><span class="sxs-lookup"><span data-stu-id="d7e42-163">Step 4: Restart the VM</span></span>

<span data-ttu-id="d7e42-164">Depois de desinstalar o Serviço de mobilidade, reinicie a VM antes de configurar a replicação para outra região do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-164">After you uninstall the Mobility service, restart the VM before you set up replication to another Azure region.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7e42-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7e42-165">Next steps</span></span>
- <span data-ttu-id="d7e42-166">Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d7e42-166">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
- <span data-ttu-id="d7e42-167">Saiba mais sobre as [Diretrizes de rede para replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="d7e42-167">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
