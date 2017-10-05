---
title: "Acesso just in time à máquina virtual na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento orienta você sobre como o acesso just in time à VM, na Central de Segurança do Azure, ajuda você a controlar o acesso às suas máquinas virtuais do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="6d3e6-103">Gerenciar o acesso à máquina virtual usando o just in time</span><span class="sxs-lookup"><span data-stu-id="6d3e6-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="6d3e6-104">O acesso just in time à VM (máquina virtual) pode ser usado para bloquear o tráfego de entrada às suas VMs do Azure, reduzindo a exposição aos ataques, fornecendo acesso fácil para conectar às VMs quando necessário.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="6d3e6-105">O recurso just in time está em versão prévia e está disponível na camada Standard da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="6d3e6-106">Confira os [Preços](security-center-pricing.md) para saber mais sobre os tipos de preço da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="6d3e6-107">Cenário de ataque</span><span class="sxs-lookup"><span data-stu-id="6d3e6-107">Attack scenario</span></span>

<span data-ttu-id="6d3e6-108">Ataques de força bruta geralmente se destinam às portas de gerenciamento como um meio para obter acesso a uma VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="6d3e6-109">Se for bem-sucedido, um invasor poderá assumir o controle sobre a VM e estabelecer uma base em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="6d3e6-110">Uma maneira de reduzir a exposição a um ataque de força bruta é limitar a quantidade de tempo que uma porta fica aberta.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="6d3e6-111">As portas de gerenciamento não precisam ficar abertas o tempo todo.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="6d3e6-112">Elas só precisam ser abertas enquanto você estiver conectado à VM, por exemplo, para realizar tarefas de manutenção ou gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="6d3e6-113">Quando o just in time está habilitado, a Central de Segurança usa regras de [NSG](../virtual-network/virtual-networks-nsg.md) (Grupo de Segurança de Rede), que restringem o acesso às portas de gerenciamento para que elas não se tornem alvo de invasores.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Cenário just in time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="6d3e6-115">Como funciona o acesso just in time?</span><span class="sxs-lookup"><span data-stu-id="6d3e6-115">How does just in time access work?</span></span>

<span data-ttu-id="6d3e6-116">Quando o just in time está habilitado, a Central de Segurança bloqueia o tráfego de entrada às suas VMs do Azure, criando uma regra de NSG.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="6d3e6-117">Você seleciona as portas na VM para as quais o tráfego de entrada será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="6d3e6-118">Essas portas são controladas pela solução just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="6d3e6-119">Quando um usuário solicita acesso a uma VM, a Central de Segurança verifica se o usuário tem permissões de [RBAC (Controle de acesso baseado em função)](../active-directory/role-based-access-control-configure.md) que fornecem acesso de gravação ao recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="6d3e6-120">Se o usuário tem permissões de gravação, a solicitação é aprovada e a Central de Segurança configura automaticamente os NSGs (Grupos de Segurança de Rede) para permitir o tráfego de entrada às portas de gerenciamento pelo período de tempo que você especificou.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="6d3e6-121">Depois que o tempo expirar, a Central de Segurança restaura os NSGs aos seus estados anteriores.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="6d3e6-122">O acesso just in time à VM da Central de Segurança atualmente dá suporte somente a VMs implantadas por meio do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="6d3e6-123">Para saber mais sobre os modelos de implantação clássica e do Resource Manager, consulte [Azure Resource Manager vs implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d3e6-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="6d3e6-124">Usando o acesso just in time</span><span class="sxs-lookup"><span data-stu-id="6d3e6-124">Using just in time access</span></span>

<span data-ttu-id="6d3e6-125">O bloco **Acesso à VM just in time** na folha **Central de Segurança** mostra o número de VMs configuradas para o acesso just in time e o número de solicitações de acesso aprovadas na última semana.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="6d3e6-126">Selecione o bloco **Acesso à VM just in time** e a folha **Acesso à VM just in time** é aberta.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Bloco acesso à VM just in time][2]

<span data-ttu-id="6d3e6-128">A folha **Acesso à VM just in time** fornece informações sobre o estado das suas VMs:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="6d3e6-129">**Configurada** – VMs que foram configuradas para dar suporte ao acesso à VM just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="6d3e6-130">Os dados apresentados são da última semana e incluem, para cada VM, o número de solicitações aprovadas, a data e a hora do último acesso e o último usuário.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="6d3e6-131">**Recomendada** – VMs que podem dar suporte ao acesso à VM just in time, mas não foram configurados para isso.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="6d3e6-132">É recomendável que você habilite o controle de acesso à VM just in time para essas VMs.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="6d3e6-133">Consulte [Habilitar acesso à VM just in time](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="6d3e6-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="6d3e6-134">**Nenhuma recomendação** – as razões que podem fazer com que uma VM não seja recomendada são:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="6d3e6-135">NSG ausente – a solução just in time exige que um NSG esteja em vigor.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="6d3e6-136">VM Clássica – o acesso à VM just in time da Central de Segurança atualmente dá suporte apenas às VMs implantadas por meio do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="6d3e6-137">Não há suporte para uma implantação clássica na solução just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="6d3e6-138">Outros – uma VM estará nessa categoria se a solução just in time estiver desativada na política de segurança da assinatura ou do grupo de recursos ou se estiver faltando um IP público da VM e ela não tiver um NSG em vigor.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="6d3e6-139">Configurando uma política de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="6d3e6-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="6d3e6-140">Para selecionar as VMs que você deseja habilitar:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="6d3e6-141">Na folha **Acesso à VM just in time**, selecione a guia **Recomendada**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Habilitar o acesso just in time][3]

2. <span data-ttu-id="6d3e6-143">Em **VMs**, selecione as VMs que você deseja habilitar.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="6d3e6-144">Isso coloca uma marca de seleção ao lado de uma VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="6d3e6-145">Selecione **Habilitar JIT nas VMs**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="6d3e6-146">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="6d3e6-147">Portas padrão</span><span class="sxs-lookup"><span data-stu-id="6d3e6-147">Default ports</span></span>

<span data-ttu-id="6d3e6-148">Você pode ver as portas padrão nas quais a Central de Segurança recomenda habilitar o just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="6d3e6-149">Na folha **Acesso à VM just in time**, selecione a guia **Recomendada**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Exibir portas padrão][6]

2. <span data-ttu-id="6d3e6-151">Em **VMs**, selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="6d3e6-152">Isso coloca uma marca de seleção ao lado da VM e abre a folha **Configuração de acesso à VM JIT**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="6d3e6-153">Esta folha exibe as portas padrão.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="6d3e6-154">Adicionar portas</span><span class="sxs-lookup"><span data-stu-id="6d3e6-154">Add ports</span></span>

<span data-ttu-id="6d3e6-155">Na folha **Configuração de acesso à VM JIT**, você também pode adicionar e configurar uma nova porta na qual deseja habilitar a solução just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="6d3e6-156">Na folha **Configuração de acesso à VM JIT**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="6d3e6-157">Isso abre a folha **Adicionar configuração de porta**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-157">This opens the **Add port configuration** blade.</span></span>

  ![Configuração de portas][7]

2. <span data-ttu-id="6d3e6-159">Na folha **Adicionar configuração de porta**, você identifica a porta, o tipo de protocolo, os IPs de origem com permissão e o tempo máximo de solicitação.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="6d3e6-160">Os IPs de origem permitidos são os intervalos de IP que têm permissão para obter acesso após uma solicitação aprovada.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="6d3e6-161">Tempo máximo de solicitação é a janela de tempo máxima que uma porta específica pode ser aberta.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="6d3e6-162">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="6d3e6-163">Solicitando acesso a uma VM</span><span class="sxs-lookup"><span data-stu-id="6d3e6-163">Requesting access to a VM</span></span>

<span data-ttu-id="6d3e6-164">Para solicitar acesso a uma VM:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-164">To request access to a VM:</span></span>

1. <span data-ttu-id="6d3e6-165">Na folha **Acesso à VM just in time**, selecione a guia **Configurada**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="6d3e6-166">Em **VMs**, selecione as VMs que você deseja habilitar o acesso.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="6d3e6-167">Isso coloca uma marca de seleção ao lado de uma VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="6d3e6-168">Selecione **Solicitar acesso**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-168">Select **Request access**.</span></span> <span data-ttu-id="6d3e6-169">Isso abre a folha **Solicitar acesso**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-169">This opens the **Request access** blade.</span></span>

  ![Solicitar acesso a uma VM][4]

4. <span data-ttu-id="6d3e6-171">Na folha **Solicitar acesso**, você configura, para cada VM, as portas a serem abertas juntamente com o IP de origem para o qual a porta está aberta e a janela de tempo para a qual a porta está aberta.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="6d3e6-172">Você pode solicitar acesso somente para as portas que estão configuradas na política just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="6d3e6-173">Cada porta tem um tempo máximo permitido derivado da política just in time.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="6d3e6-174">Selecione **Abrir portas**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="6d3e6-175">Edição de uma política de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="6d3e6-175">Editing a just in time access policy</span></span>

<span data-ttu-id="6d3e6-176">Você pode alterar a política just in time existente de uma VM adicionando e configurando uma nova porta a ser aberta para essa VM ou alterando qualquer outro parâmetro relacionado a uma porta já protegida.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="6d3e6-177">Para editar a política just in time existente de uma VM, usa-se a guia **Configurada**:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="6d3e6-178">Em **VMs**, selecione uma VM para a qual adicionar uma porta, clicando nos três pontos dentro da linha dessa VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="6d3e6-179">Isso abre um menu.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-179">This opens a menu.</span></span>
2. <span data-ttu-id="6d3e6-180">Selecione **Editar** no menu.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="6d3e6-181">Isso abre a folha **Configuração de acesso à VM JIT**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![Editar política][8]

3. <span data-ttu-id="6d3e6-183">Na folha **Configuração de acesso à VM JIT**, você pode editar as configurações existentes de uma porta já protegida clicando em sua porta ou você pode selecionar **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="6d3e6-184">Isso abre a folha **Adicionar configuração de porta**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-184">This opens the **Add port configuration** blade.</span></span>

  ![Adicionar uma porta][7]

4. <span data-ttu-id="6d3e6-186">Na folha **Adicionar configuração de porta**, identifique a porta, o tipo de protocolo, os IPs de origem com permissão e o tempo máximo de solicitação.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="6d3e6-187">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-187">Select **OK**.</span></span>
6. <span data-ttu-id="6d3e6-188">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="6d3e6-189">Auditoria em atividades de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="6d3e6-189">Auditing just in time access activity</span></span>

<span data-ttu-id="6d3e6-190">Você pode obter informações sobre as atividades de VM usando a pesquisa de logs.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="6d3e6-191">Para exibir os logs:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-191">To view logs:</span></span>

1. <span data-ttu-id="6d3e6-192">Na folha **Acesso à VM just in time**, selecione a guia **Configurada**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="6d3e6-193">Em **VMs**, selecione uma VM para exibir as respectivas informações, clicando nos três pontos dentro da linha dessa VM.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="6d3e6-194">Isso abre um menu.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-194">This opens a menu.</span></span>
3. <span data-ttu-id="6d3e6-195">Selecione **Log de atividades** no menu.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="6d3e6-196">Isso abre a folha **Log de atividades**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-196">This opens the **Activity log** blade.</span></span>

![Selecionar o log de atividades][9]

<span data-ttu-id="6d3e6-198">A folha **Log de atividades** fornece uma exibição filtrada das operações anteriores dessa VM junto com a hora, a data e a assinatura.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Exibir log de atividades][5]

<span data-ttu-id="6d3e6-200">Você pode baixar as informações de log selecionando **Clique aqui para baixar todos os itens como CSV**.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="6d3e6-201">Modifique os filtros e selecione **Aplicar** para criar uma pesquisa e um log.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="6d3e6-202">Usando o acesso à VM just in time por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d3e6-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="6d3e6-203">Para usar a solução just in time por meio do PowerShell, verifique se você tem a versão [mais recente](/powershell/azure/install-azurerm-ps) do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="6d3e6-204">Depois disso, você precisa instalar a Central de Segurança do Azure [mais recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) da galeria do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="6d3e6-205">Configurando uma política just in time para uma VM</span><span class="sxs-lookup"><span data-stu-id="6d3e6-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="6d3e6-206">Para configurar uma política just in time em uma VM específica, você precisa executar este comando em sua sessão do PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="6d3e6-207">Siga a documentação do cmdlet para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="6d3e6-208">Solicitando acesso a uma VM</span><span class="sxs-lookup"><span data-stu-id="6d3e6-208">Requesting access to a VM</span></span>

<span data-ttu-id="6d3e6-209">Para acessar uma VM específica que esteja protegida com a solução just in time, você precisa executar este comando em sua sessão do PowerShell: Invoke-ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="6d3e6-210">Siga a documentação do cmdlet para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d3e6-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d3e6-211">Next steps</span></span>
<span data-ttu-id="6d3e6-212">Nesse artigo você aprendeu como o acesso just in time à VM na Central de Segurança ajuda você a controlar o acesso às suas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="6d3e6-213">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d3e6-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="6d3e6-214">[Configurando políticas de segurança](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="6d3e6-215">[Gerenciar recomendações de segurança](security-center-recommendations.md) – saiba como as recomendações ajudam a proteger seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="6d3e6-216">[Monitoramento da integridade da segurança](security-center-monitoring.md) – saiba como monitorar a integridade dos seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="6d3e6-217">[Gerenciar e responder aos alertas de segurança](security-center-managing-and-responding-alerts.md) – aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="6d3e6-218">[Monitorar as soluções de parceiros](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="6d3e6-219">[Perguntas frequentes da Central de Segurança](security-center-faq.md) - encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="6d3e6-220">[Blog de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d3e6-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
