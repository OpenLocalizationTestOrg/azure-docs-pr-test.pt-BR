---
title: "servidores aaaRemove e desabilite a proteção | Microsoft Docs"
description: "Este artigo descreve como os servidores de toounregister de uma recuperação de Site cofre e toodisable proteção para máquinas virtuais e servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="7db61-103">Remover os servidores e desabilitar a proteção</span><span class="sxs-lookup"><span data-stu-id="7db61-103">Remove servers and disable protection</span></span>

<span data-ttu-id="7db61-104">Olá serviço Azure Site Recovery contribui com a estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour.</span><span class="sxs-lookup"><span data-stu-id="7db61-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="7db61-105">serviço de saudação coordena a replicação, failover e recuperação de máquinas virtuais e servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="7db61-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="7db61-106">Computadores podem ser replicado tooAzure ou tooa local secundário data center.</span><span class="sxs-lookup"><span data-stu-id="7db61-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="7db61-107">Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7db61-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="7db61-108">Este artigo descreve como toounregister servidores de serviços de recuperação de um cofre no portal do Azure de saudação e como toodisable proteção para máquinas protegidos pela recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7db61-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="7db61-109">Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7db61-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="7db61-110">Cancelar o registro de um servidor de configuração conectado</span><span class="sxs-lookup"><span data-stu-id="7db61-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="7db61-111">Se você replicar máquinas virtuais do VMware ou tooAzure de servidores físicos do Windows/Linux, você pode cancelar o registro de um servidor conectado de configuração de um cofre da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7db61-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="7db61-112">Desabilite o proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="7db61-112">Disable machine protection.</span></span> <span data-ttu-id="7db61-113">Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="7db61-114">Desassocie todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="7db61-114">Disassociate any policies.</span></span> <span data-ttu-id="7db61-115">Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **políticas de replicação**, clique duas vezes em Olá diretiva associada.</span><span class="sxs-lookup"><span data-stu-id="7db61-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="7db61-116">Servidor de configuração com o botão direito hello > **desassociar**.</span><span class="sxs-lookup"><span data-stu-id="7db61-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="7db61-117">Remova qualquer outro processo local ou servidores de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="7db61-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="7db61-118">Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de saudação com o botão direito > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="7db61-119">Exclua o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="7db61-120">Desinstalar manualmente o serviço de mobilidade Olá em execução no servidor de destino mestre da saudação (Isso será um separado ou servidor ou em execução no servidor de configuração de saudação).</span><span class="sxs-lookup"><span data-stu-id="7db61-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="7db61-121">Desinstale quaisquer servidores de processo adicionais.</span><span class="sxs-lookup"><span data-stu-id="7db61-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="7db61-122">Desinstale o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="7db61-123">No servidor de configuração de hello, desinstale a instância de saudação do MySQL que foi instalada pela recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7db61-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="7db61-124">No registro de saudação saudação do servidor de configuração excluir chave Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="7db61-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="7db61-125">Cancelar o registro de um servidor de configuração não conectado</span><span class="sxs-lookup"><span data-stu-id="7db61-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="7db61-126">Se você replicar máquinas virtuais do VMware ou tooAzure de servidores físicos do Windows/Linux, você pode cancelar o registro de um servidor de configuração desconectado de um cofre da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7db61-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="7db61-127">Desabilite o proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="7db61-127">Disable machine protection.</span></span> <span data-ttu-id="7db61-128">Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="7db61-129">Selecione **parar de gerenciar a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="7db61-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="7db61-130">Remova qualquer outro processo local ou servidores de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="7db61-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="7db61-131">Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de saudação com o botão direito > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="7db61-132">Exclua o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="7db61-133">Desinstalar manualmente o serviço de mobilidade Olá em execução no servidor de destino mestre da saudação (Isso será um separado ou servidor ou em execução no servidor de configuração de saudação).</span><span class="sxs-lookup"><span data-stu-id="7db61-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="7db61-134">Desinstale quaisquer servidores de processo adicionais.</span><span class="sxs-lookup"><span data-stu-id="7db61-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="7db61-135">Desinstale o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="7db61-136">No servidor de configuração de hello, desinstale a instância de saudação do MySQL que foi instalada pela recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="7db61-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="7db61-137">No registro de saudação saudação do servidor de configuração excluir chave Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="7db61-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="7db61-138">Cancelar o registro de um servidor VMM conectado</span><span class="sxs-lookup"><span data-stu-id="7db61-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="7db61-139">Como melhor prática, recomendamos que você cancelar o registro do servidor do VMM hello quando tooAzure tenha se conectado.</span><span class="sxs-lookup"><span data-stu-id="7db61-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="7db61-140">Isso garante que as configurações nos servidores do VMM hello (e em outros servidores do VMM com nuvens emparelhados) sejam limpos corretamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="7db61-141">Remova um servidor desconectado somente se houver um problema de conectividade permanente.</span><span class="sxs-lookup"><span data-stu-id="7db61-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="7db61-142">Se o servidor do VMM Olá não está conectado, será necessário toomanually executar tooclean um script configurações.</span><span class="sxs-lookup"><span data-stu-id="7db61-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="7db61-143">Pare a replicação de máquinas virtuais em nuvens em Olá servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="7db61-144">Exclua qualquer mapeamento de rede usado pelo nuvens no hello servidor VMM que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="7db61-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="7db61-145">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento de rede**, clique o mapeamento de rede hello >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="7db61-146">Desassocie políticas de replicação de nuvens em Olá servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="7db61-147">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="7db61-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="7db61-148">Clique com botão direito nuvem hello > **desassociar**.</span><span class="sxs-lookup"><span data-stu-id="7db61-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="7db61-149">Exclua o servidor do VMM hello ou nó ativo do VMM.</span><span class="sxs-lookup"><span data-stu-id="7db61-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="7db61-150">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **servidores do VMM**, servidor de saudação atalho >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="7db61-151">Desinstale Olá provedor manualmente no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="7db61-152">Se você tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="7db61-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="7db61-153">Se você estiver replicando tooAzure, remova manualmente o agente de serviços de recuperação do Microsoft hello de hosts do Hyper-V nas nuvens Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="7db61-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="7db61-154">Cancelar o registro de um servidor VMM desconectado</span><span class="sxs-lookup"><span data-stu-id="7db61-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="7db61-155">Pare a replicação de máquinas virtuais em nuvens em Olá servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="7db61-156">Exclua qualquer mapeamento de rede usado pelo nuvens no servidor do VMM Olá que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="7db61-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="7db61-157">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento de rede**, clique o mapeamento de rede hello >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="7db61-158">Observe a ID de saudação do servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="7db61-159">Desassocie políticas de replicação de nuvens em Olá servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="7db61-160">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="7db61-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="7db61-161">Clique com botão direito nuvem hello > **desassociar**.</span><span class="sxs-lookup"><span data-stu-id="7db61-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="7db61-162">Exclua o servidor do VMM hello ou nó ativo.</span><span class="sxs-lookup"><span data-stu-id="7db61-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="7db61-163">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **servidores do VMM**, servidor de saudação atalho >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="7db61-164">Baixe e execute Olá [script de limpeza](http://aka.ms/asr-cleanup-script-vmm) no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="7db61-165">Abra o PowerShell com hello **executar como administrador** opção política de execução toochange Olá para o escopo do saudação padrão (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="7db61-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="7db61-166">No script hello, especifique a ID de saudação do hello servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="7db61-167">script Hello remove o registro e informações do servidor de saudação de emparelhamento de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7db61-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="7db61-168">Execute o script de limpeza de saudação em outros servidores VMM que contêm as nuvens que são combinadas com nuvens de saudação servidor VMM que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="7db61-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="7db61-169">Execute o script de limpeza de saudação em qualquer outros passivo VMM nós de cluster com hello que provedor instalado.</span><span class="sxs-lookup"><span data-stu-id="7db61-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="7db61-170">Desinstale Olá provedor manualmente no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="7db61-171">Se você tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="7db61-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="7db61-172">Se você replicar tooAzure, você pode remover agente de serviços de recuperação do Microsoft hello de hosts do Hyper-V em nuvens Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="7db61-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="7db61-173">Cancelar o registro de um host Hyper-V em um site do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7db61-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="7db61-174">Os hosts Hyper-V que não são gerenciados pelo VMM são reunidos em um site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7db61-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="7db61-175">Remova um host de um site do Hyper-V da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7db61-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="7db61-176">Desabilite a replicação para máquinas virtuais do Hyper-V localizado no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="7db61-177">Desassocie políticas para o site do Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="7db61-178">Em **infra-estrutura de recuperação de Site** > **para Sites do Hyper-V** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="7db61-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="7db61-179">Site de saudação do botão direito do mouse > **desassociar**.</span><span class="sxs-lookup"><span data-stu-id="7db61-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="7db61-180">Exclua os hosts Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="7db61-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="7db61-181">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **Hosts Hyper-V**, servidor de saudação atalho >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="7db61-182">Exclua site Olá Hyper-V depois que todos os hosts foram removidos dele.</span><span class="sxs-lookup"><span data-stu-id="7db61-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="7db61-183">Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **Sites Hyper-V**, site de saudação do botão direito do mouse >  **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="7db61-184">Execute Olá script a seguir em cada host Hyper-V que foram removidos.</span><span class="sxs-lookup"><span data-stu-id="7db61-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="7db61-185">Olá script limpa as configurações no servidor de saudação e cancela o registro do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="7db61-186">Desabilitar a proteção de uma VM do VMware ou servidor físico</span><span class="sxs-lookup"><span data-stu-id="7db61-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="7db61-187">Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="7db61-188">Em **Remover Máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="7db61-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="7db61-189">**Desabilite a proteção de máquina da saudação (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="7db61-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="7db61-190">Use este toostop opção replicando máquina hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="7db61-191">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="7db61-192">Você só verá essa opção em Olá circunstâncias a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db61-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="7db61-193">**Tamanho do volume VM Olá**— quando você redimensiona uma saudação do volume virtual máquina entra em um estado crítico.</span><span class="sxs-lookup"><span data-stu-id="7db61-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="7db61-194">Selecione essa proteção de toodisables opção enquanto retém os pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="7db61-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="7db61-195">Ao habilitar a proteção da máquina Olá novamente, dados de Olá para o volume de saudação redimensionada serão transferido tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7db61-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="7db61-196">**Executar um failover recentemente**— depois de executar um failover tootest seu ambiente, selecione esse toostart opção protegendo máquinas locais novamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="7db61-197">Ele desabilita a cada máquina virtual e, em seguida, você precisa tooenable proteção para-los novamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="7db61-198">Desabilitar máquina Olá com essa configuração não afeta Olá máquina de virtual de réplica no Azure.</span><span class="sxs-lookup"><span data-stu-id="7db61-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="7db61-199">Não desinstale o serviço de mobilidade de saudação da máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="7db61-200">**Parar de gerenciar a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="7db61-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="7db61-201">Se você selecionar essa opção, Olá máquina só será removida do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="7db61-202">As configurações de proteção de locais para a máquina de saudação não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="7db61-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="7db61-203">configurações de tooremove máquina hello e tooremove máquina Olá Olá assinatura do Azure, você precisar de configurações de saudação tooclean Desinstalando o serviço de mobilidade hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="7db61-204">Desabilitar a proteção de uma VM Hyper-V em uma nuvem do VMM</span><span class="sxs-lookup"><span data-stu-id="7db61-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="7db61-205">Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="7db61-206">Em **Remover Máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="7db61-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="7db61-207">**Desabilite a proteção de máquina da saudação (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="7db61-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="7db61-208">Use este toostop opção replicando máquina hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="7db61-209">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="7db61-210">**Parar de gerenciar a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="7db61-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="7db61-211">Se você selecionar essa opção, Olá máquina só será removida do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="7db61-212">As configurações de proteção de locais para a máquina de saudação não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="7db61-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="7db61-213">configurações de tooremove máquina hello e tooremove máquina Olá Olá assinatura do Azure, você precisar tooclean Olá configurações backup manualmente, usando instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="7db61-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="7db61-214">Observe que se você selecionar a máquina de virtual toodelete hello e seus discos rígidos, eles serão removidos do local de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="7db61-215">Limpar as configurações de proteção - local do replication tooa secundário do VMM</span><span class="sxs-lookup"><span data-stu-id="7db61-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="7db61-216">Se você selecionou **parar de gerenciar a máquina Olá** e você replicando tooa site secundário, execute este script no tooclean do servidor primário Olá configurações Olá da máquina virtual primária de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="7db61-217">No console do VMM Olá clique console do hello PowerShell botão tooopen Olá PowerShell do VMM.</span><span class="sxs-lookup"><span data-stu-id="7db61-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="7db61-218">Substitua SQLVM1 com o nome da saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7db61-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="7db61-219">No servidor VMM secundário Olá execute tooclean este script configurações Olá da máquina virtual secundária de saudação:</span><span class="sxs-lookup"><span data-stu-id="7db61-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="7db61-220">No servidor VMM secundário hello, atualize máquinas virtuais de saudação no servidor de host do Hyper-V Olá, portanto hello VM secundário obtém detectado novamente no console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="7db61-221">Olá acima etapas limpar as configurações de replicação Olá no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="7db61-222">Se você quiser toostop replicação da máquina virtual de hello, executar Olá seguir script AH Olá VMs primárias e secundárias.</span><span class="sxs-lookup"><span data-stu-id="7db61-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="7db61-223">Substitua SQLVM1 com o nome da saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7db61-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="7db61-224">Limpar as configurações de proteção - tooAzure de replicação</span><span class="sxs-lookup"><span data-stu-id="7db61-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="7db61-225">Se você selecionou **parar de gerenciar a máquina Olá** e replicar tooAzure, execute este script no servidor do VMM de origem de hello, usando o PowerShell do console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="7db61-226">Olá acima etapas limpar as configurações de replicação de saudação no servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="7db61-227">replicação toostop para a máquina virtual de saudação em execução no servidor de host do Hyper-V hello, execute este script.</span><span class="sxs-lookup"><span data-stu-id="7db61-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="7db61-228">Substitua SQLVM1 pelo nome de saudação da sua máquina virtual e host01.contoso.com com o nome de saudação do servidor de host do Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="7db61-229">Desabilitar a proteção de uma VM do Hyper-V em um site do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="7db61-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="7db61-230">Use este procedimento se você estiver replicando tooAzure de VMs Hyper-V sem um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="7db61-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="7db61-231">Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7db61-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="7db61-232">Em **remover máquina**, você pode selecionar Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="7db61-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="7db61-233">**Desabilite a proteção de máquina da saudação (recomendada)**.</span><span class="sxs-lookup"><span data-stu-id="7db61-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="7db61-234">Use este toostop opção replicando máquina hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="7db61-235">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7db61-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="7db61-236">**Parar de gerenciar a máquina Olá**.</span><span class="sxs-lookup"><span data-stu-id="7db61-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="7db61-237">Se você selecionar essa opção Olá máquina só será removida do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="7db61-238">As configurações de proteção de locais para a máquina de saudação não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="7db61-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="7db61-239">configurações de tooremove na máquina hello e tooremove Olá virtual machine de saudação assinatura do Azure, você precisar tooclean Olá configurações backup manualmente.</span><span class="sxs-lookup"><span data-stu-id="7db61-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="7db61-240">Se você selecionar a máquina de virtual toodelete hello e seus discos rígidos, eles serão removidos do local de destino hello.</span><span class="sxs-lookup"><span data-stu-id="7db61-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="7db61-241">Se você selecionou **parar de gerenciar a máquina Olá**, executar esse script no servidor de host do Hyper-V de origem hello, tooremove replicação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="7db61-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="7db61-242">Substitua SQLVM1 com o nome da saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7db61-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
