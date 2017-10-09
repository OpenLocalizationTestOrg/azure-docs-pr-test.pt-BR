---
title: "aaaJust na máquina virtual do tempo de acesso na Central de segurança do Azure | Microsoft Docs"
description: "Este documento orienta como apenas em tempo de acesso da máquina virtual na Ajuda da Central de segurança do Azure você controlar o acesso tooyour Azure máquinas virtuais."
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
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="bf1c0-103">Gerenciar o acesso à máquina virtual usando o just in time</span><span class="sxs-lookup"><span data-stu-id="bf1c0-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="bf1c0-104">Just-in-time VM (máquina virtual) o acesso pode ser usado toolock para baixo tráfego de entrada tooyour VMs do Azure, reduzindo a exposição tooattacks enquanto fornecem acesso fácil tooconnect tooVMs quando necessário.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1c0-105">Olá apenas no recurso de tempo está no modo de visualização e disponível no hello camada padrão da Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="bf1c0-106">Consulte [preços](security-center-pricing.md) camadas de preços do toolearn mais sobre o Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="bf1c0-107">Cenário de ataque</span><span class="sxs-lookup"><span data-stu-id="bf1c0-107">Attack scenario</span></span>

<span data-ttu-id="bf1c0-108">Força bruta ataques geralmente as portas de gerenciamento de destino como um tooa de acesso significa toogain VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="bf1c0-109">Se for bem-sucedido, um invasor pode assumir controle Olá VM e estabelecer destaque em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="bf1c0-110">Ataque de força bruta tooreduce unidirecional exposição tooa é toolimit Olá período de tempo que uma porta está aberta.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="bf1c0-111">As portas de gerenciamento fazer não abrir de toobe necessário em todos os momentos.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="bf1c0-112">Eles só precisarem de toobe aberto enquanto você conectado toohello VM, por exemplo tooperform de são tarefas de manutenção ou gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="bf1c0-113">Quando está habilitada no momento, a Central de segurança usa [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regras (NSG), que restringem o acesso toomanagement portas para que eles não podem ser alvo de invasores.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Cenário just in time][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="bf1c0-115">Como funciona o acesso just in time?</span><span class="sxs-lookup"><span data-stu-id="bf1c0-115">How does just in time access work?</span></span>

<span data-ttu-id="bf1c0-116">Quando está habilitada no momento, a Central de segurança bloqueia o tráfego de entrada tooyour VMs do Azure, criando uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="bf1c0-117">Selecione as portas de saudação em Olá VM toowhich o tráfego de entrada será bloqueado para baixo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="bf1c0-118">Essas portas são controladas por Olá apenas na solução de tempo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="bf1c0-119">Quando um usuário solicita acesso tooa VM, Central de segurança verifica se o usuário Olá tem [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) permissões que fornecem acesso de gravação para Olá recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="bf1c0-120">Se eles têm permissões de gravação, Olá solicitação for aprovada e Central de segurança configura automaticamente os grupos de segurança de rede (NSGs) hello tooallow portas de gerenciamento de toohello de tráfego de entrada quantidade de saudação de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="bf1c0-121">Depois que o tempo de saudação expirou, Central de segurança restaura estados anteriores da saudação NSGs tootheir.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="bf1c0-122">O acesso just in time à VM da Central de Segurança atualmente dá suporte somente a VMs implantadas por meio do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="bf1c0-123">toolearn mais sobre hello clássico e modelos de implantação do Gerenciador de recursos, consulte [do Azure Resource Manager versus implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bf1c0-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="bf1c0-124">Usando o acesso just in time</span><span class="sxs-lookup"><span data-stu-id="bf1c0-124">Using just in time access</span></span>

<span data-ttu-id="bf1c0-125">Olá **apenas no acesso de tempo de VM** bloco Olá **Central de segurança** folha mostra o número de saudação de máquinas virtuais configuradas para apenas no tempo acesso e Olá o número de solicitações de acesso aprovado feitas no hello última semana.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="bf1c0-126">Selecione Olá **apenas no acesso de tempo de VM** lado a lado e hello **apenas no acesso de tempo de VM** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Bloco acesso à VM just in time][2]

<span data-ttu-id="bf1c0-128">Olá **apenas no acesso de tempo de VM** folha fornece informações sobre o estado de saudação das suas máquinas virtuais:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="bf1c0-129">**Configurado** -VMs que foram toosupport configurado apenas no acesso de tempo de VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="bf1c0-130">dados Olá apresentados para Olá na semana passada e incluem para cada número de saudação do VM de solicitações aprovadas, a data do último acesso e a hora e do último usuário.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="bf1c0-131">**Recomendada** – VMs que podem dar suporte ao acesso à VM just in time, mas não foram configurados para isso.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="bf1c0-132">É recomendável que você habilite o controle de acesso à VM just in time para essas VMs.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="bf1c0-133">Consulte [Habilitar acesso à VM just in time](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="bf1c0-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="bf1c0-134">**Nenhuma recomendação** -razões que podem causar uma VM não toobe recomendado são:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="bf1c0-135">Ausente NSG - Olá apenas no tempo solução requer um toobe NSG em vigor.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="bf1c0-136">VM Clássica – o acesso à VM just in time da Central de Segurança atualmente dá suporte apenas às VMs implantadas por meio do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="bf1c0-137">Uma implantação clássica não é suportada pelo Olá apenas na solução de tempo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="bf1c0-138">Outros - uma VM é nesta categoria se Olá no momento a solução está desativada na política de segurança de saudação da assinatura de saudação ou grupo de recursos hello, ou que hello VM está faltando um IP público e não tiver um NSG em vigor.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="bf1c0-139">Configurando uma política de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="bf1c0-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="bf1c0-140">Olá tooselect VMs que você deseja tooenable:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="bf1c0-141">Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **recomendado** guia.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Habilitar o acesso just in time][3]

2. <span data-ttu-id="bf1c0-143">Em **VMs**, selecione Olá VMs que você deseja tooenable.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="bf1c0-144">Isso coloca uma tooa de marca de seleção próxima VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="bf1c0-145">Selecione **Habilitar JIT nas VMs**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="bf1c0-146">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="bf1c0-147">Portas padrão</span><span class="sxs-lookup"><span data-stu-id="bf1c0-147">Default ports</span></span>

<span data-ttu-id="bf1c0-148">Você pode ver as portas padrão Olá Central de segurança recomenda habilitar no momento.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="bf1c0-149">Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **recomendado** guia.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Exibir portas padrão][6]

2. <span data-ttu-id="bf1c0-151">Em **VMs**, selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="bf1c0-152">Isso coloca uma saudação do marca de seleção próxima toohello VM e abre **configuração de acesso de JIT VM** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="bf1c0-153">Esta folha exibe as portas padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="bf1c0-154">Adicionar portas</span><span class="sxs-lookup"><span data-stu-id="bf1c0-154">Add ports</span></span>

<span data-ttu-id="bf1c0-155">De saudação **configuração de acesso de JIT VM** folha, você pode também adicionar e configurar uma nova porta na qual você deseja tooenable Olá apenas na solução de tempo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="bf1c0-156">Em Olá **configuração de acesso de JIT VM** folha, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="bf1c0-157">Isso abre o hello **Adicionar configuração de porta** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-157">This opens hello **Add port configuration** blade.</span></span>

  ![Configuração de portas][7]

2. <span data-ttu-id="bf1c0-159">Em **Adicionar configuração de porta** folha, identificar porta hello, tipo de protocolo, tempo de solicitação de IPs de origem e o máximo permitida.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="bf1c0-160">Permitido IPs de origem são Olá IP intervalos tooget permitido acesso após uma solicitação aprovado.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="bf1c0-161">Tempo máximo de solicitação é a janela de tempo máximo de saudação que uma porta específica pode ser aberta.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="bf1c0-162">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="bf1c0-163">Solicitando acesso tooa VM</span><span class="sxs-lookup"><span data-stu-id="bf1c0-163">Requesting access tooa VM</span></span>

<span data-ttu-id="bf1c0-164">acesso de toorequest tooa VM:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="bf1c0-165">Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **configurado** guia.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="bf1c0-166">Em **VMs**, selecione Olá VMs que você deseja acesso tooenable.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="bf1c0-167">Isso coloca uma tooa de marca de seleção próxima VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="bf1c0-168">Selecione **Solicitar acesso**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-168">Select **Request access**.</span></span> <span data-ttu-id="bf1c0-169">Isso abre o hello **solicitar acesso** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-169">This opens hello **Request access** blade.</span></span>

  ![Solicitar acesso tooa VM][4]

4. <span data-ttu-id="bf1c0-171">Em Olá **solicitar acesso** folha, que você configurar para cada tooopen de portas VM Olá junto com o IP de origem de Olá Olá porta está aberta tooand janela de tempo de saudação para o qual Olá porta está aberta.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="bf1c0-172">Você pode solicitar portas de toohello apenas de acesso que são configuradas no hello apenas na diretiva de tempo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="bf1c0-173">Cada porta tem um tempo máximo permitido derivado Olá apenas na diretiva de tempo.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="bf1c0-174">Selecione **Abrir portas**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="bf1c0-175">Edição de uma política de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="bf1c0-175">Editing a just in time access policy</span></span>

<span data-ttu-id="bf1c0-176">Você pode alterar uma VM existente apenas na diretiva de tempo adicionando e configurando um novo tooopen de porta para a VM ou alterando a qualquer outro parâmetro tooan relacionada já protegido porta.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="bf1c0-177">Em ordem tooedit um existente apenas na diretiva de tempo de uma VM, hello **configurado** guia é usada:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="bf1c0-178">Em **VMs**, selecione uma VM tooadd um tooby porta clicando em pontos de saudação três na linha de saudação para a VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="bf1c0-179">Isso abre um menu.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-179">This opens a menu.</span></span>
2. <span data-ttu-id="bf1c0-180">Selecione **editar** no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="bf1c0-181">Isso abre o hello **configuração de acesso de JIT VM** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Editar política][8]

3. <span data-ttu-id="bf1c0-183">Em Olá **configuração de acesso de JIT VM** folha, você pode editar as configurações existentes de uma porta já protegida Olá clicando em sua porta, ou você pode selecionar **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="bf1c0-184">Isso abre o hello **Adicionar configuração de porta** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-184">This opens hello **Add port configuration** blade.</span></span>

  ![Adicionar uma porta][7]

4. <span data-ttu-id="bf1c0-186">Em **Adicionar configuração de porta** folha identificar porta hello, tipo de protocolo, IPs de origem permitido e tempo máximo de solicitações.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="bf1c0-187">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-187">Select **OK**.</span></span>
6. <span data-ttu-id="bf1c0-188">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="bf1c0-189">Auditoria em atividades de acesso just in time</span><span class="sxs-lookup"><span data-stu-id="bf1c0-189">Auditing just in time access activity</span></span>

<span data-ttu-id="bf1c0-190">Você pode obter informações sobre as atividades de VM usando a pesquisa de logs.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="bf1c0-191">logs de tooview:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-191">tooview logs:</span></span>

1. <span data-ttu-id="bf1c0-192">Em Olá **apenas no acesso de tempo de VM** folha, selecione Olá **configurado** guia.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="bf1c0-193">Em **VMs**, selecione um tooview de VM informações sobre clicando em pontos de saudação três na linha de saudação para a VM.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="bf1c0-194">Isso abre um menu.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-194">This opens a menu.</span></span>
3. <span data-ttu-id="bf1c0-195">Selecione **Log de atividades** no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="bf1c0-196">Isso abre o hello **log de atividades** folha.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-196">This opens hello **Activity log** blade.</span></span>

![Selecionar o log de atividades][9]

<span data-ttu-id="bf1c0-198">Olá **log de atividades** folha fornece uma exibição filtrada de operações anteriores para a VM junto com a assinatura, data e hora.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Exibir log de atividades][5]

<span data-ttu-id="bf1c0-200">Você pode baixar informações do log Olá selecionando **clique aqui toodownload todos os itens de saudação como CSV**.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="bf1c0-201">Modificar filtros hello e selecione **aplicar** toocreate uma pesquisa e log.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="bf1c0-202">Usando o acesso à VM just in time por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf1c0-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="bf1c0-203">Na saudação de toouse ordem apenas na solução de tempo por meio do PowerShell, certifique-se de ter Olá [mais recente](/powershell/azure/install-azurerm-ps) versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="bf1c0-204">Depois que você fizer isso, você precisa Olá tooinstall [mais recente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Central de segurança do Azure da Galeria do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="bf1c0-205">Configurando uma política just in time para uma VM</span><span class="sxs-lookup"><span data-stu-id="bf1c0-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="bf1c0-206">tooconfigure apenas na diretiva de tempo em uma VM específica, você precisa de toorun esse comando em sua sessão do PowerShell: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="bf1c0-207">Siga Olá cmdlet documentação toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="bf1c0-208">Solicitando acesso tooa VM</span><span class="sxs-lookup"><span data-stu-id="bf1c0-208">Requesting access tooa VM</span></span>

<span data-ttu-id="bf1c0-209">tooaccess uma VM específica que é protegida com Olá apenas na solução de tempo, você precisa toorun esse comando em sua sessão do PowerShell: ASCJITAccess invocar.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="bf1c0-210">Siga Olá cmdlet documentação toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf1c0-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf1c0-211">Next steps</span></span>
<span data-ttu-id="bf1c0-212">Neste artigo, você aprendeu como apenas em tempo de acesso da máquina virtual na Central de segurança ajuda controlar o acesso tooyour Azure máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="bf1c0-213">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bf1c0-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="bf1c0-214">[Definir políticas de segurança](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="bf1c0-215">[Gerenciar recomendações de segurança](security-center-recommendations.md) – saiba como as recomendações ajudam a proteger seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="bf1c0-216">[Monitoramento de integridade de segurança](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="bf1c0-217">[Gerenciando e responder a alertas toosecurity](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="bf1c0-218">[Monitoramento de soluções de parceiros](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="bf1c0-219">[Perguntas frequentes sobre o Centro de segurança](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="bf1c0-220">[Blog de Segurança do Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1c0-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
