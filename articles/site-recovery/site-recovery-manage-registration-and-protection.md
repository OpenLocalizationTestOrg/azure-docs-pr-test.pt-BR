---
title: "Remover os servidores e desabilitar a proteção | Microsoft Docs"
description: "Este artigo descreve como cancelar o registro de servidores de um cofre de Recuperação de Site e desabilitar a proteção para máquinas virtuais e servidores físicos."
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
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="9a5f2-103">Remover os servidores e desabilitar a proteção</span><span class="sxs-lookup"><span data-stu-id="9a5f2-103">Remove servers and disable protection</span></span>

<span data-ttu-id="9a5f2-104">O serviço Azure Site Recovery contribui para sua estratégia de BCDR (continuidade de negócios e recuperação de desastre).</span><span class="sxs-lookup"><span data-stu-id="9a5f2-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="9a5f2-105">O serviço orquestra a replicação, o failover e a recuperação de máquinas virtuais e servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="9a5f2-106">As máquinas podem ser replicadas no Azure ou em um datacenter local secundário.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="9a5f2-107">Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9a5f2-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="9a5f2-108">Este artigo descreve como cancelar o registro de servidores de um cofre dos Serviços de Recuperação no Portal do Azure, e como desabilitar a proteção de máquinas protegidas pelo Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="9a5f2-109">Publique eventuais comentários ou perguntas no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9a5f2-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="9a5f2-110">Cancelar o registro de um servidor de configuração conectado</span><span class="sxs-lookup"><span data-stu-id="9a5f2-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="9a5f2-111">Se você replicar VMs VMware ou servidores físicos com Windows/Linux no Azure, será possível cancelar o registro de um servidor de configuração conectado em um cofre da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="9a5f2-112">Desabilite o proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-112">Disable machine protection.</span></span> <span data-ttu-id="9a5f2-113">Em **Itens Protegidos** > **Itens Replicados**, clique com o botão direito na máquina > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="9a5f2-114">Desassocie todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-114">Disassociate any policies.</span></span> <span data-ttu-id="9a5f2-115">Em **Infraestrutura do Site Recovery** > **Para Máquinas Físicas e de VMWare**  > **Políticas de Replicação**, clique duas vezes na política associada.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="9a5f2-116">Clique com botão direito no servidor de configuração > **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="9a5f2-117">Remova qualquer outro processo local ou servidores de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="9a5f2-118">Em **Infraestrutura do Site Recovery** > **Para Máquinas Físicas e de VMWare** > **Servidores de Configuração**, clique com o botão direito no servidor > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="9a5f2-119">Excluir o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="9a5f2-120">Desinstale manualmente o serviço Mobilidade que está em execução no servidor de destino mestre (será um servidor separado ou em execução no servidor de configuração).</span><span class="sxs-lookup"><span data-stu-id="9a5f2-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="9a5f2-121">Desinstale quaisquer servidores de processo adicionais.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="9a5f2-122">Desinstale o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="9a5f2-123">No servidor de configuração, desinstale a instância do MySQL foi instalado pelo Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="9a5f2-124">No registro do servidor de configuração, exclua a chave ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="9a5f2-125">Cancelar o registro de um servidor de configuração não conectado</span><span class="sxs-lookup"><span data-stu-id="9a5f2-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="9a5f2-126">Se você replicar VMs VMware ou servidores físicos com Windows/Linux no Azure, será possível cancelar o registro de um servidor de configuração não conectado em um cofre da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="9a5f2-127">Desabilite o proteção da máquina.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-127">Disable machine protection.</span></span> <span data-ttu-id="9a5f2-128">Em **Itens Protegidos** > **Itens Replicados**, clique com o botão direito na máquina > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="9a5f2-129">Selecione **Interromper o gerenciamento da máquina**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="9a5f2-130">Remova qualquer outro processo local ou servidores de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="9a5f2-131">Em **Infraestrutura do Site Recovery** > **Para Máquinas Físicas e de VMWare** > **Servidores de Configuração**, clique com o botão direito no servidor > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="9a5f2-132">Excluir o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="9a5f2-133">Desinstale manualmente o serviço Mobilidade que está em execução no servidor de destino mestre (será um servidor separado ou em execução no servidor de configuração).</span><span class="sxs-lookup"><span data-stu-id="9a5f2-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="9a5f2-134">Desinstale quaisquer servidores de processo adicionais.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="9a5f2-135">Desinstale o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="9a5f2-136">No servidor de configuração, desinstale a instância do MySQL foi instalado pelo Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="9a5f2-137">No registro do servidor de configuração, exclua a chave ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="9a5f2-138">Cancelar o registro de um servidor VMM conectado</span><span class="sxs-lookup"><span data-stu-id="9a5f2-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="9a5f2-139">Como prática recomendada, recomendamos o cancelamento do registro do servidor VMM quando ele estiver conectado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="9a5f2-140">Isso garante que as configurações nos servidores do VMM (e em outros servidores VMM com nuvens emparelhadas) sejam limpas corretamente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="9a5f2-141">Remova um servidor desconectado somente se houver um problema de conectividade permanente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="9a5f2-142">Se o servidor VMM não estiver conectado, você precisará executar manualmente um script para limpar as configurações.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="9a5f2-143">Pare de replicar VMs em nuvens no servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="9a5f2-144">Exclua qualquer mapeamento de rede usado por nuvens no servidor VMM que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="9a5f2-145">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Mapeamento de Rede**, clique com o botão direito no mapeamento de rede > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="9a5f2-146">Desassocie políticas de replicação de nuvens no servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="9a5f2-147">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** >  **Políticas de Replicação**, clique duas vezes na política associada.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="9a5f2-148">Clique com o botão direito na nuvem > **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="9a5f2-149">Exclua o servidor VMM ou o nó ativo do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="9a5f2-150">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Servidores VMM**, clique com o botão direito do servidor > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="9a5f2-151">Desinstalar manualmente o Provedor no servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="9a5f2-152">Se você tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="9a5f2-153">Se você estiver replicando para o Azure, remova manualmente o agente dos Serviços de Recuperação da Microsoft dos hosts Hyper-V nas nuvens excluídas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="9a5f2-154">Cancelar o registro de um servidor VMM desconectado</span><span class="sxs-lookup"><span data-stu-id="9a5f2-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="9a5f2-155">Pare de replicar VMs em nuvens no servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="9a5f2-156">Exclua qualquer mapeamento de rede usado por nuvens no servidor VMM que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="9a5f2-157">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Mapeamento de Rede**, clique com o botão direito no mapeamento de rede > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="9a5f2-158">Anote a ID do servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="9a5f2-159">Desassocie políticas de replicação de nuvens no servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="9a5f2-160">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** >  **Políticas de Replicação**, clique duas vezes na política associada.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="9a5f2-161">Clique com o botão direito na nuvem > **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="9a5f2-162">Exclua o servidor VMM ou o nó ativo.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="9a5f2-163">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Servidores VMM**, clique com o botão direito do servidor > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="9a5f2-164">Baixe e execute o [script de limpeza](http://aka.ms/asr-cleanup-script-vmm) no servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="9a5f2-165">Abra o PowerShell com a opção **Executar como Administrador** para alterar a política de execução para o escopo padrão (LocalMachine).</span><span class="sxs-lookup"><span data-stu-id="9a5f2-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="9a5f2-166">No script, especifique a ID do servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="9a5f2-167">O script remove o registro e as informações de emparelhamento na nuvem do servidor.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="9a5f2-168">Execute o script de limpeza em outros servidores VMM que contêm nuvens emparelhadas com nuvens no servidor VMM que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="9a5f2-169">Execute o script de limpeza em quaisquer outros nós de cluster passivos do VMM nos quais o Provedor está instalado.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="9a5f2-170">Desinstalar manualmente o Provedor no servidor VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="9a5f2-171">Se você tiver um cluster, remova todos os nós.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="9a5f2-172">Se você estiver replicando no Azure, remova o agente dos Serviços de Recuperação da Microsoft dos hosts Hyper-V nas nuvens excluídas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="9a5f2-173">Cancelar o registro de um host Hyper-V em um site do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="9a5f2-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="9a5f2-174">Os hosts Hyper-V que não são gerenciados pelo VMM são reunidos em um site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="9a5f2-175">Remova um host de um site do Hyper-V da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="9a5f2-176">Desabilite a replicação para VMs do Hyper-V localizadas no host.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="9a5f2-177">Desassocie as políticas para o site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="9a5f2-178">Em **Infraestrutura do Site Recovery** > **Para sites do Hyper-V** >  **Políticas de Replicação**, clique duas vezes na política associada.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="9a5f2-179">Clique com o botão direito no site > **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="9a5f2-180">Exclua os hosts Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="9a5f2-181">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Hosts Hyper-V**, clique com o botão direito do servidor > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="9a5f2-182">Exclua site do Hyper-V depois que todos os hosts tiverem sido removidos dele.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="9a5f2-183">Em **Infraestrutura do Site Recovery** > **Para VMM do System Center** > **Sites do Hyper-V**, clique com o botão direito do site > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="9a5f2-184">Execute o seguinte script em cada host Hyper-V removido.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="9a5f2-185">O script limpa as configurações no servidor e cancela o registro do cofre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
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
                "Stopping the Azure Site Recovery service..."
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

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="9a5f2-186">Desabilitar a proteção de uma VM do VMware ou servidor físico</span><span class="sxs-lookup"><span data-stu-id="9a5f2-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="9a5f2-187">Em **Itens Protegidos** > **Itens Replicados**, clique com o botão direito na máquina > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="9a5f2-188">Em **Remover Máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="9a5f2-189">**Desabilitar proteção da máquina (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="9a5f2-190">Use esta opção para interromper a replicação da máquina.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="9a5f2-191">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="9a5f2-192">Você só verá essa opção nas seguintes circunstâncias:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="9a5f2-193">**Você redimensionou o volume da VM**—Quando você redimensiona um volume, a máquina virtual entra em um estado crítico.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="9a5f2-194">Selecione essa opção para desabilitar a proteção enquanto retém os pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="9a5f2-195">Quando você habilita novamente a proteção para a máquina, os dados do volume redimensionado são transferidos para o Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="9a5f2-196">**Você executou recentemente um failover**—Após a execução de um failover para testar o ambiente, selecione essa opção para voltar a proteger os computadores locais.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="9a5f2-197">Isso desabilita cada máquina virtual e, depois, será necessário reabilitar a proteção para elas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="9a5f2-198">Desabilitar a máquina com essa configuração não afeta a máquina virtual de réplica no Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="9a5f2-199">Não desinstale o serviço de Mobilidade da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="9a5f2-200">**Interrompa o gerenciamento da máquina**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-200">**Stop managing the machine**.</span></span> <span data-ttu-id="9a5f2-201">Se você selecionar essa opção, a máquina será removida somente do cofre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="9a5f2-202">As configurações de proteção local da máquina não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="9a5f2-203">Para remover as configurações na máquina e remover a máquina da assinatura do Azure, será necessário limpar as configurações desinstalando o serviço de Mobilidade.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="9a5f2-204">Desabilitar a proteção de uma VM Hyper-V em uma nuvem do VMM</span><span class="sxs-lookup"><span data-stu-id="9a5f2-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="9a5f2-205">Em **Itens Protegidos** > **Itens Replicados**, clique com o botão direito na máquina > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="9a5f2-206">Em **Remover Máquina**, selecione uma destas opções:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="9a5f2-207">**Desabilitar proteção da máquina (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="9a5f2-208">Use esta opção para interromper a replicação da máquina.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="9a5f2-209">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="9a5f2-210">**Interrompa o gerenciamento da máquina**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-210">**Stop managing the machine**.</span></span> <span data-ttu-id="9a5f2-211">Se você selecionar essa opção, a máquina será removida somente do cofre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="9a5f2-212">As configurações de proteção local da máquina não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="9a5f2-213">Para remover as configurações na máquina e remover a máquina da assinatura do Azure, será necessário limpar as configurações manualmente usando as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="9a5f2-214">Observe que se você optar por excluir a máquina virtual e seus discos rígidos, eles serão removidos do local de destino.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="9a5f2-215">Limpar as configurações de proteção - replicação para um site secundário do VMM</span><span class="sxs-lookup"><span data-stu-id="9a5f2-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="9a5f2-216">Se você selecionou **Parar de gerenciar a máquina** e estiver replicando para um site secundário, execute este script no servidor primário para limpar as configurações para a máquina virtual primária.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="9a5f2-217">No console do VMM, clique no botão do PowerShell para abrir o console do PowerShell do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="9a5f2-218">Substitua SQLVM1 pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="9a5f2-219">No servidor VMM secundário, execute este script para limpar as configurações da máquina virtual secundária:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="9a5f2-220">No servidor do VMM secundário, atualize as máquinas virtuais no servidor do host Hyper-V para que a VM secundária seja novamente detectada no console do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="9a5f2-221">As etapas acima limpam as configurações de replicação no servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="9a5f2-222">Se você quiser interromper a replicação para a máquina virtual, execute o seguinte script nas VMs primárias e secundárias.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="9a5f2-223">Substitua SQLVM1 pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="9a5f2-224">Limpar as configurações de proteção - replicação no Azure</span><span class="sxs-lookup"><span data-stu-id="9a5f2-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="9a5f2-225">Se você selecionou **Parar de gerenciar a máquina** e tiver replicado no Azure, execute este script no servidor VMM de origem, usando o PowerShell no console do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="9a5f2-226">As etapas acima limpam as configurações de replicação no servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="9a5f2-227">Para interromper a replicação para a máquina virtual em execução no servidor do host Hyper-V, execute este script.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="9a5f2-228">Substitua SQLVM1 pelo nome de sua máquina virtual e host01.contoso.com pelo nome do servidor do host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="9a5f2-229">Desabilitar a proteção de uma VM do Hyper-V em um site do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="9a5f2-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="9a5f2-230">Use este procedimento se você estiver replicando VMs do Hyper-V para o Azure sem um servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="9a5f2-231">Em **Itens Protegidos** > **Itens Replicados**, clique com o botão direito na máquina > **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="9a5f2-232">Em **Remover Máquina**, você pode selecionar as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="9a5f2-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="9a5f2-233">**Desabilitar proteção da máquina (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="9a5f2-234">Use esta opção para interromper a replicação da máquina.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="9a5f2-235">As configurações do Site Recovery serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="9a5f2-236">**Interrompa o gerenciamento da máquina**.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-236">**Stop managing the machine**.</span></span> <span data-ttu-id="9a5f2-237">Se você selecionar essa opção, a máquina será removida somente do cofre.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="9a5f2-238">As configurações de proteção local da máquina não serão afetadas.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="9a5f2-239">Para remover as configurações na máquina e remover a máquina virtual da assinatura do Azure, será necessário limpar as configurações manualmente.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="9a5f2-240">Se você optar por excluir a máquina virtual e seus discos rígidos, eles serão removidos do local de destino.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="9a5f2-241">Se você selecionou **Parar o gerenciamento da máquina**, execute este script no servidor do host Hyper-V de origem para remover a replicação para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="9a5f2-242">Substitua SQLVM1 pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9a5f2-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
