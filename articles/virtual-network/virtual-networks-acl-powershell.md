---
title: "listas de controle de acesso do Azure ponto de extremidade de aaaManage | PowerShell | Clássico | Microsoft Docs"
description: Saiba como toomanage ACLs com o PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="723b8-103">Gerenciar listas de controle de acesso do ponto de extremidade usando o PowerShell no modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="723b8-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="723b8-104">Você pode criar e gerenciar a rede controle listas de acesso (ACLs) para pontos de extremidade usando o PowerShell do Azure ou no Portal de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="723b8-105">Neste tópico, você encontrará procedimentos para tarefas comuns de ACL que podem ser concluídas usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="723b8-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="723b8-106">Para obter lista de saudação do Azure PowerShell cmdlets, consulte [Cmdlets de gerenciamento do Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="723b8-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="723b8-107">Para saber mais sobre ACLs, confira [O que é uma lista de controle de acesso (ACL) de rede?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="723b8-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="723b8-108">Se você quiser toomanage suas ACLs usando o Portal de gerenciamento de saudação, consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="723b8-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="723b8-109">Gerenciar ACLs de rede usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="723b8-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="723b8-110">Você pode usar toocreate de cmdlets do PowerShell do Azure, remover e configurar (definir) Network Access Control Lists (ACLs).</span><span class="sxs-lookup"><span data-stu-id="723b8-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="723b8-111">Incluímos alguns exemplos de algumas das maneiras de saudação, que você pode configurar uma ACL usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="723b8-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="723b8-112">tooretrieve uma lista completa de saudação cmdlets do PowerShell ACL, você pode usar qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="723b8-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="723b8-113">Criar uma ACL de rede com regras que permitem o acesso de uma sub-rede remota</span><span class="sxs-lookup"><span data-stu-id="723b8-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="723b8-114">exemplo Hello abaixo ilustra uma maneira toocreate uma nova ACL que contém as regras.</span><span class="sxs-lookup"><span data-stu-id="723b8-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="723b8-115">Essa ACL é então aplicado tooa ponto de extremidade de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="723b8-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="723b8-116">regras de ACL Olá no exemplo hello abaixo permitirá o acesso de uma sub-rede remota.</span><span class="sxs-lookup"><span data-stu-id="723b8-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="723b8-117">toocreate uma nova ACL de rede com as regras de permissão para uma sub-rede remota, abra o Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="723b8-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="723b8-118">Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="723b8-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="723b8-119">Crie novo objeto de ACL de rede hello.</span><span class="sxs-lookup"><span data-stu-id="723b8-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="723b8-120">Defina uma regra que permite o acesso de uma sub-rede remota.</span><span class="sxs-lookup"><span data-stu-id="723b8-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="723b8-121">O exemplo hello abaixo, você define a regra *100* (que tem prioridade sobre a regra 200 e superior) sub-rede remota de saudação tooallow *10.0.0.0/8* acessar o ponto de extremidade de máquina virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="723b8-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="723b8-122">Substitua valores hello com seus próprios requisitos de configuração.</span><span class="sxs-lookup"><span data-stu-id="723b8-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="723b8-123">nome Hello "Configuração da ACL de SharePoint" deve ser substituído pelo nome amigável do hello que você deseja toocall essa regra.</span><span class="sxs-lookup"><span data-stu-id="723b8-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="723b8-124">Para regras adicionais, repita o cmdlet hello, substituindo os valores hello com seus próprios requisitos de configuração.</span><span class="sxs-lookup"><span data-stu-id="723b8-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="723b8-125">Ser-se de que toochange Olá regra número ordem tooreflect Olá ordem na qual você deseja Olá regras toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="723b8-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="723b8-126">número mais baixo de regra Olá tem precedência sobre o número mais alto de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="723b8-127">Em seguida, você pode criar um novo ponto de extremidade (Adicionar) ou definir hello ACL para um ponto de extremidade existente (Set).</span><span class="sxs-lookup"><span data-stu-id="723b8-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="723b8-128">Neste exemplo, vamos adicionar que um novo ponto de extremidade de máquina virtual chamado "web" e atualização Olá máquina virtual ponto de extremidade com hello configurações de ACL.</span><span class="sxs-lookup"><span data-stu-id="723b8-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="723b8-129">Em seguida, combinar Olá cmdlets e execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="723b8-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="723b8-130">Para este exemplo hello cmdlets combinados teria esta aparência:</span><span class="sxs-lookup"><span data-stu-id="723b8-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="723b8-131">Remover uma regra de ACL de rede que permite o acesso de uma sub-rede remota</span><span class="sxs-lookup"><span data-stu-id="723b8-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="723b8-132">exemplo Hello abaixo ilustra uma maneira tooremove uma regra ACL de rede.</span><span class="sxs-lookup"><span data-stu-id="723b8-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="723b8-133">regras de tooremove uma regra de ACL de rede com permissão para uma sub-rede remota, abra um Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="723b8-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="723b8-134">Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="723b8-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="723b8-135">Primeira etapa é o objeto de ACL de rede tooget Olá para o ponto de extremidade de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="723b8-136">Você, em seguida, removerá a regra de ACL de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="723b8-137">Nesse caso, estamos removendo-a através da ID de regra.</span><span class="sxs-lookup"><span data-stu-id="723b8-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="723b8-138">Isso removerá apenas Olá ID da regra 0 da saudação ACL.</span><span class="sxs-lookup"><span data-stu-id="723b8-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="723b8-139">Não remove o objeto de ACL de saudação do ponto de extremidade de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="723b8-140">Em seguida, você deverá aplicar o ponto de extremidade do hello ACL de rede objeto toohello máquina virtual e atualizar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="723b8-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="723b8-141">Remover uma ACL de rede de um ponto de extremidade de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="723b8-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="723b8-142">Em determinados cenários, você pode querer tooremove um objeto de ACL de rede de um ponto de extremidade de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="723b8-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="723b8-143">toodo isso, abra o Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="723b8-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="723b8-144">Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="723b8-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="723b8-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="723b8-145">Next steps</span></span>
[<span data-ttu-id="723b8-146">O que é uma lista de controle de acesso (ACL) de rede?</span><span class="sxs-lookup"><span data-stu-id="723b8-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

