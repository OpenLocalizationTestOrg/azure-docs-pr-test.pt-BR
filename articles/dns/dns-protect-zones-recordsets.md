---
title: aaaProtecting zonas DNS e registros | Microsoft Docs
description: Como o registro e zonas DNS tooprotect define no DNS do Microsoft Azure.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="e582d-103">Como tooprotect DNS zonas e os registros</span><span class="sxs-lookup"><span data-stu-id="e582d-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="e582d-104">Registros e zonas DNS são recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="e582d-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="e582d-105">Excluir uma zona DNS ou até mesmo um único registro DNS pode resultar em uma interrupção total do serviço.</span><span class="sxs-lookup"><span data-stu-id="e582d-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="e582d-106">Portanto, é importante que registros e zonas DNS críticos sejam protegidos contra alterações acidentais ou não autorizadas.</span><span class="sxs-lookup"><span data-stu-id="e582d-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="e582d-107">Este artigo explica como DNS do Azure permite que você tooprotect suas zonas DNS e registros de acordo com essas alterações.</span><span class="sxs-lookup"><span data-stu-id="e582d-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="e582d-108">Podemos aplicar dois recursos de segurança avançados fornecidos pelo Azure Resource Manager: [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) e [bloqueios de recurso](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="e582d-109">Controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="e582d-109">Role-based access control</span></span>

<span data-ttu-id="e582d-110">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o usuários, grupos e recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="e582d-111">Usando o RBAC, você pode conceder com precisão a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="e582d-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="e582d-112">Para obter mais informações sobre como o RBAC ajuda você a gerenciar o acesso, veja [O que é Controle de Acesso Baseado em Função](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="e582d-113">função de 'Colaborador de zona DNS' Hello</span><span class="sxs-lookup"><span data-stu-id="e582d-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="e582d-114">função de 'Colaborador de zona DNS' Hello é uma função interna fornecida pelo Azure para gerenciamento de recursos DNS.</span><span class="sxs-lookup"><span data-stu-id="e582d-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="e582d-115">Atribuindo grupo ou usuário de tooa de permissões de Colaborador de zona do DNS permite que os recursos do grupo toomanage DNS, mas não os recursos de qualquer outro tipo.</span><span class="sxs-lookup"><span data-stu-id="e582d-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="e582d-116">Por exemplo, suponha que grupo de recursos de saudação 'myzones' contém cinco zonas para Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="e582d-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="e582d-117">Concessão Olá DNS administrador 'Colaborador de zona DNS' permissões toothat grupo de recursos, permite controle total sobre as zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="e582d-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="e582d-118">Ele também evita conceder permissões desnecessárias, administrador do DNS por exemplo hello não é possível criar ou parar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e582d-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="e582d-119">permissões de RBAC de tooassign de maneira mais simples de saudação é [por meio do portal do Azure de saudação](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="e582d-120">Abra a folha de saudação 'controle de acesso (IAM)' para o grupo de recursos Olá, e em seguida, clique em 'Adicionar' e selecione função de 'Colaborador de zona DNS' hello e usuários Selecione Olá necessário ou toogrant permissões.</span><span class="sxs-lookup"><span data-stu-id="e582d-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Nível de grupo de recursos RBAC via Olá portal do Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="e582d-122">As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="e582d-123">comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="e582d-124">RBAC de nível de zona</span><span class="sxs-lookup"><span data-stu-id="e582d-124">Zone level RBAC</span></span>

<span data-ttu-id="e582d-125">Regras RBAC do Azure podem ser aplicadas tooa assinatura, um recurso de chamadas individual tooan ou de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e582d-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="e582d-126">No caso de saudação do DNS do Azure, esse recurso pode ser uma zona DNS individual, ou até mesmo um conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="e582d-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="e582d-127">Por exemplo, suponha que o grupo de recursos de saudação 'myzones' contém Olá zona 'contoso.com' e uma subzona 'customers.contoso.com' no qual os registros CNAME são criados para cada conta de cliente.</span><span class="sxs-lookup"><span data-stu-id="e582d-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="e582d-128">Olá conta usada toomanage esses registros CNAME devem ser atribuídos permissões toocreate registros Olá 'customers.contoso.com' zona apenas, ele não deve ter acesso toohello outras regiões.</span><span class="sxs-lookup"><span data-stu-id="e582d-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="e582d-129">Podem ser concedidas permissões em nível de zona RBAC via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="e582d-130">Abrir Olá 'Controle de acesso (IAM)' folha para a zona Olá, em seguida, clique em 'Adicionar' e selecione função de 'Colaborador de zona DNS' hello e usuários Selecione Olá necessário ou toogrant permissões.</span><span class="sxs-lookup"><span data-stu-id="e582d-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![RBAC nível de zona do DNS por meio de saudação portal do Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="e582d-132">As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="e582d-133">comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="e582d-134">RBAC de nível do conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="e582d-134">Record set level RBAC</span></span>

<span data-ttu-id="e582d-135">Podemos ir uma etapa adiante.</span><span class="sxs-lookup"><span data-stu-id="e582d-135">We can go one step further.</span></span> <span data-ttu-id="e582d-136">Considere Olá administrador do sistema para a Contoso Corporation, que precisa de acesso toohello MX e registros TXT no ápice da saudação da zona de 'contoso.com' hello.</span><span class="sxs-lookup"><span data-stu-id="e582d-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="e582d-137">Ela não precisa acessar tooany outros registros MX ou TXT ou tooany registros de qualquer outro tipo.</span><span class="sxs-lookup"><span data-stu-id="e582d-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="e582d-138">DNS do Azure permite a você permissões tooassign Olá conjunto de registros de nível, tooprecisely Olá registros que Olá administrador de mail precisa acessar.</span><span class="sxs-lookup"><span data-stu-id="e582d-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="e582d-139">Olá administrador de mail é concedido controle Olá ela precisa e é toomake não é possível que outras alterações.</span><span class="sxs-lookup"><span data-stu-id="e582d-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="e582d-140">Permissões RBAC no nível do conjunto de registros podem ser configuradas via Olá portal do Azure, usando o botão de saudação 'usuários' na folha de conjunto de registros de saudação:</span><span class="sxs-lookup"><span data-stu-id="e582d-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Nível de RBAC por meio do portal do Azure de saudação do conjunto de registros](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="e582d-142">As permissões RBAC de nível do conjunto de registros também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="e582d-143">comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="e582d-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="e582d-144">Funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="e582d-144">Custom roles</span></span>

<span data-ttu-id="e582d-145">função interna de 'Colaborador de zona DNS' Hello permite controle total sobre um recurso DNS.</span><span class="sxs-lookup"><span data-stu-id="e582d-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="e582d-146">Ele também é possível toobuild seu próprio cliente Azure funções, tooprovide mesmo refinado controle.</span><span class="sxs-lookup"><span data-stu-id="e582d-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="e582d-147">Considere novamente o exemplo hello em que um registro CNAME na zona Olá 'customers.contoso.com' é criado para cada conta de cliente da Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="e582d-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="e582d-148">Olá conta usada toomanage esses CNAMEs devem ser concedidas permissão toomanage CNAME somente registros.</span><span class="sxs-lookup"><span data-stu-id="e582d-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="e582d-149">É, em seguida, não é possível toomodify registros de outros tipos (como alterar os registros MX) ou executar operações de nível de zona, como a exclusão de zona.</span><span class="sxs-lookup"><span data-stu-id="e582d-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="e582d-150">saudação de exemplo a seguir mostra uma definição de função personalizada para gerenciar apenas os registros CNAME:</span><span class="sxs-lookup"><span data-stu-id="e582d-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="e582d-151">Olá propriedade ações define Olá permissões específicas do DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="e582d-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="e582d-152">`Microsoft.Network/dnsZones/CNAME/*` concede controle total sobre os registros CNAME</span><span class="sxs-lookup"><span data-stu-id="e582d-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="e582d-153">`Microsoft.Network/dnsZones/read`concede as zonas DNS de tooread de permissão, mas não toomodify-los, permitindo que você toosee Olá zona no qual Olá CNAME está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="e582d-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="e582d-154">Olá ações restantes são copiadas do hello [função de Colaborador de zona DNS interna](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="e582d-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="e582d-155">Usar um tooprevent personalizada de função RBAC excluir registro define enquanto ainda permite que eles toobe atualizada não é um controle eficiente.</span><span class="sxs-lookup"><span data-stu-id="e582d-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="e582d-156">Isso impede que os conjuntos de registro sejam excluídos, mas não impede que sejam modificados.</span><span class="sxs-lookup"><span data-stu-id="e582d-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="e582d-157">Modificações permitidas incluem a adição e remoção de registros do conjunto de registros de hello, incluindo a remoção de todos os registros tooleave um conjunto de registros 'empty'.</span><span class="sxs-lookup"><span data-stu-id="e582d-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="e582d-158">Isso tem Olá mesmo efeito de exclusão de registro Olá definido de um ponto de vista de resolução DNS.</span><span class="sxs-lookup"><span data-stu-id="e582d-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="e582d-159">Definições de função personalizada não podem ser definidas no momento por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="e582d-160">Uma função personalizada com base nessa definição de função pode ser criada usando o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e582d-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="e582d-161">Ele também pode ser criado por meio de saudação CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="e582d-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="e582d-162">Hello função pode ser atribuída em Olá mesma forma como as funções internas, como descrito anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e582d-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="e582d-163">Para obter mais informações sobre como toocreate, gerenciar e atribuir funções personalizadas, consulte [funções personalizadas no Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="e582d-164">Bloqueios de recurso</span><span class="sxs-lookup"><span data-stu-id="e582d-164">Resource locks</span></span>

<span data-ttu-id="e582d-165">Em adição tooRBAC, Gerenciador de recursos do Azure oferece suporte a outro tipo de controle de segurança, ou seja, too'lock de capacidade de saudação ' recursos.</span><span class="sxs-lookup"><span data-stu-id="e582d-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="e582d-166">Onde as regras RBAC permitirem toocontrol ações de saudação de usuários e grupos específicos, bloqueios de recursos são aplicados toohello recursos e entrarão em vigor em todos os usuários e funções.</span><span class="sxs-lookup"><span data-stu-id="e582d-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="e582d-167">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="e582d-168">Há dois tipos de bloqueio de recurso: **DoNotDelete** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="e582d-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="e582d-169">Elas podem ser aplicadas tooa zona DNS ou tooan conjunto de registros individuais.</span><span class="sxs-lookup"><span data-stu-id="e582d-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="e582d-170">Olá, seções a seguir descrevem vários cenários comuns e como toosupport-los usando bloqueios de recursos.</span><span class="sxs-lookup"><span data-stu-id="e582d-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="e582d-171">Proteção contra todas as alterações</span><span class="sxs-lookup"><span data-stu-id="e582d-171">Protecting against all changes</span></span>

<span data-ttu-id="e582d-172">tooprevent as alterações que estão sendo feitas, aplicar uma zona de toohello de bloqueio de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e582d-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="e582d-173">Isso impede que novos conjuntos de registros sejam criados e que os existentes sejam modificados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="e582d-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="e582d-174">Bloqueios de recursos de nível de zona podem ser criados por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="e582d-175">Na folha de zona do DNS hello, clique em 'Bloqueios', em seguida, 'Add':</span><span class="sxs-lookup"><span data-stu-id="e582d-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bloqueios de recursos de nível de zona via Olá portal do Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="e582d-177">Bloqueios de recurso em nível de zona podem ser criados via Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e582d-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="e582d-178">Não é suportada atualmente ao configurar os bloqueios de recursos do Azure por meio de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="e582d-179">Protegendo registros individuais</span><span class="sxs-lookup"><span data-stu-id="e582d-179">Protecting individual records</span></span>

<span data-ttu-id="e582d-180">tooprevent um registro DNS existente definida contra a modificação, se aplicam a um conjunto de registros do toohello de bloqueio de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e582d-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="e582d-181">Aplicar um tooa de bloqueio DoNotDelete conjunto de registros não é um controle eficiente.</span><span class="sxs-lookup"><span data-stu-id="e582d-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="e582d-182">Isso impede que o registro Olá definir sejam excluídas, mas ele não impede que ele está sendo modificado.</span><span class="sxs-lookup"><span data-stu-id="e582d-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="e582d-183">Modificações permitidas incluem a adição e remoção de registros do conjunto de registros de hello, incluindo a remoção de todos os registros tooleave um conjunto de registros 'empty'.</span><span class="sxs-lookup"><span data-stu-id="e582d-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="e582d-184">Isso tem Olá mesmo efeito de exclusão de registro Olá definido de um ponto de vista de resolução DNS.</span><span class="sxs-lookup"><span data-stu-id="e582d-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="e582d-185">Atualmente, os bloqueios de recurso em nível de conjunto de registros só podem ser configurados pelo uso do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e582d-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="e582d-186">Eles não têm suporte no portal do Azure de saudação ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e582d-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="e582d-187">Proteção contra a exclusão de zona</span><span class="sxs-lookup"><span data-stu-id="e582d-187">Protecting against zone deletion</span></span>

<span data-ttu-id="e582d-188">Quando uma zona é excluída no DNS do Azure, todos os conjuntos de registros na zona Olá também são excluídos.</span><span class="sxs-lookup"><span data-stu-id="e582d-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="e582d-189">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="e582d-189">This operation cannot be undone.</span></span>  <span data-ttu-id="e582d-190">A exclusão acidental de uma zona crítica tem toohave potencial Olá um impacto significativo nos negócios.</span><span class="sxs-lookup"><span data-stu-id="e582d-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="e582d-191">Portanto, é muito importante tooprotect contra a exclusão acidental de zona.</span><span class="sxs-lookup"><span data-stu-id="e582d-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="e582d-192">Aplicar uma zona de tooa DoNotDelete bloqueio impede a zona Olá sejam excluídas.</span><span class="sxs-lookup"><span data-stu-id="e582d-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="e582d-193">No entanto, desde que os bloqueios são herdados pelos recursos filho, ele também evita qualquer conjuntos de registros na zona de saudação sejam excluídas, que pode ser indesejável.</span><span class="sxs-lookup"><span data-stu-id="e582d-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="e582d-194">Além disso, conforme descrito na nota da saudação acima, também é ineficiente desde registros ainda podem ser removidos de conjuntos de registros existentes hello.</span><span class="sxs-lookup"><span data-stu-id="e582d-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="e582d-195">Como alternativa, considere a aplicação de um registro de tooa DoNotDelete bloqueio definido na zona hello, como o conjunto de registros de SOA hello.</span><span class="sxs-lookup"><span data-stu-id="e582d-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="e582d-196">Desde que a zona de saudação não pode ser excluída sem também excluir conjuntos de registros Olá, isso protege contra a exclusão de zona, enquanto ainda permite que os conjuntos de registros dentro de saudação zona toobe modificadas livremente.</span><span class="sxs-lookup"><span data-stu-id="e582d-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="e582d-197">Se uma tentativa for feita toodelete zona de hello, Azure Resource Manager detecta isso também deve excluir conjunto de registros de SOA hello e blocos Olá chamada porque Olá SOA está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="e582d-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="e582d-198">Nenhum conjunto de registros é excluído.</span><span class="sxs-lookup"><span data-stu-id="e582d-198">No record sets are deleted.</span></span>

<span data-ttu-id="e582d-199">saudação de comando do PowerShell a seguir cria um bloqueio de DoNotDelete no registro SOA de saudação do hello dada zona:</span><span class="sxs-lookup"><span data-stu-id="e582d-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="e582d-200">Permissões de exclusão de outra forma, a exclusão acidental de zona tooprevent está usando um operador de saudação tooensure função personalizada e o serviço contas usadas toomanage suas zonas não têm de zona.</span><span class="sxs-lookup"><span data-stu-id="e582d-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="e582d-201">Quando você precisar toodelete uma zona, você pode impor uma exclusão de duas etapas, primeiro conceder permissões de exclusão de zona (no escopo de zona de hello, tooprevent Excluir zona errado Olá) e a segunda zona de saudação toodelete.</span><span class="sxs-lookup"><span data-stu-id="e582d-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="e582d-202">Essa segunda abordagem tem a vantagem de saudação que funciona para todas as zonas acessadas por essas contas, sem a necessidade tooremember toocreate todos os bloqueios.</span><span class="sxs-lookup"><span data-stu-id="e582d-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="e582d-203">Ele tem a desvantagem de saudação que todas as contas com permissões de exclusão de zona, como o proprietário da assinatura hello, ainda acidentalmente podem excluir uma zona crítica.</span><span class="sxs-lookup"><span data-stu-id="e582d-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="e582d-204">É possível toouse - bloqueios de recursos e funções personalizadas - ambas as abordagens em Olá a mesma hora, como uma abordagem de defesa em profundidade tooDNS zona a proteção.</span><span class="sxs-lookup"><span data-stu-id="e582d-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e582d-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e582d-205">Next steps</span></span>

* <span data-ttu-id="e582d-206">Para obter mais informações sobre como trabalhar com RBAC, consulte [Introdução ao gerenciamento de acesso no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="e582d-207">Para obter mais informações sobre trabalho com bloqueios de recurso, confira [Bloquear recursos com o Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e582d-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

