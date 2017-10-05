---
title: Protegendo Registros e Zonas DNS | Microsoft Docs
description: Como proteger conjuntos de registros e zonas DNS no DNS do Microsoft Azure.
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
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="d5748-103">Proteger registros e zonas DNS</span><span class="sxs-lookup"><span data-stu-id="d5748-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="d5748-104">Registros e zonas DNS são recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="d5748-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="d5748-105">Excluir uma zona DNS ou até mesmo um único registro DNS pode resultar em uma interrupção total do serviço.</span><span class="sxs-lookup"><span data-stu-id="d5748-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="d5748-106">Portanto, é importante que registros e zonas DNS críticos sejam protegidos contra alterações acidentais ou não autorizadas.</span><span class="sxs-lookup"><span data-stu-id="d5748-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="d5748-107">Este artigo explica como o DNS do Azure permite que você proteja seus registros e zonas DNS contra essas alterações.</span><span class="sxs-lookup"><span data-stu-id="d5748-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="d5748-108">Podemos aplicar dois recursos de segurança avançados fornecidos pelo Azure Resource Manager: [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) e [bloqueios de recurso](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="d5748-109">Controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="d5748-109">Role-based access control</span></span>

<span data-ttu-id="d5748-110">O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o usuários, grupos e recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5748-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="d5748-111">Usando o RBAC, você pode conceder exatamente a quantidade de acesso que os usuários precisam para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d5748-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="d5748-112">Para obter mais informações sobre como o RBAC ajuda você a gerenciar o acesso, veja [O que é Controle de Acesso Baseado em Função](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="d5748-113">A função 'Colaborador de zona DNS'</span><span class="sxs-lookup"><span data-stu-id="d5748-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="d5748-114">A função 'Colaborador de zona DNS' é uma função interna fornecida pelo Azure para gerenciamento de recursos DNS.</span><span class="sxs-lookup"><span data-stu-id="d5748-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="d5748-115">Atribuir permissões de Colaborador de Zona DNS a um usuário ou grupo permite que esse grupo gerencie recursos DNS, mas não os recursos de qualquer outro tipo.</span><span class="sxs-lookup"><span data-stu-id="d5748-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="d5748-116">Por exemplo, suponha que o grupo de recursos 'myzones' contém cinco zonas para a Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="d5748-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="d5748-117">Conceder permissões de 'Colaborador de Zona DNS' para esse grupo de recursos ao administrador de DNS habilita o controle total sobre essas zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="d5748-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="d5748-118">Isso também evita que permissões desnecessárias sejam concedidas, por exemplo, o administrador de DNS não pode criar ou parar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d5748-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="d5748-119">A maneira mais simples de atribuir permissões de RBAC é [por meio do Portal do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="d5748-120">Abra a folha de 'Controle de acesso (IAM)' para o grupo de recursos, em seguida, clique em 'Adicionar', selecione a função 'Colaborador de zona DNS' e selecione os usuários ou grupos aos quais é necessário conceder permissões.</span><span class="sxs-lookup"><span data-stu-id="d5748-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC de nível do grupo de recursos por meio do Portal do Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="d5748-122">As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="d5748-123">O comando equivalente também está [disponível por meio da CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="d5748-124">RBAC de nível de zona</span><span class="sxs-lookup"><span data-stu-id="d5748-124">Zone level RBAC</span></span>

<span data-ttu-id="d5748-125">É possível aplicar regras de RBAC do Azure a uma assinatura, grupo de recursos ou a um recurso individual.</span><span class="sxs-lookup"><span data-stu-id="d5748-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="d5748-126">No caso do DNS do Azure, esse recurso pode ser uma zona DNS individual ou até mesmo um conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="d5748-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="d5748-127">Por exemplo, suponha que o grupo de recursos 'myzones' contém a zona 'contoso.com' e uma subzona 'customers.contoso.com' na qual os registros CNAME são criados para cada conta de cliente.</span><span class="sxs-lookup"><span data-stu-id="d5748-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="d5748-128">A conta usada para gerenciar esses registros CNAME deve ter permissões para criar registros somente na zona 'customers.contoso.com', ele não deve ter acesso às outras zonas.</span><span class="sxs-lookup"><span data-stu-id="d5748-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="d5748-129">É possível conceder permissões de nível da zona RBAC por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5748-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="d5748-130">Abra a folha de 'Controle de acesso (IAM)' para a zona, em seguida, clique em 'Adicionar', selecione a função 'Colaborador de zona DNS' e selecione os usuários ou grupos aos quais é necessário conceder permissões.</span><span class="sxs-lookup"><span data-stu-id="d5748-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![RBAC de nível da Zona DNS por meio do Portal do Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="d5748-132">As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="d5748-133">O comando equivalente também está [disponível por meio da CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="d5748-134">RBAC de nível do conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="d5748-134">Record set level RBAC</span></span>

<span data-ttu-id="d5748-135">Podemos ir uma etapa adiante.</span><span class="sxs-lookup"><span data-stu-id="d5748-135">We can go one step further.</span></span> <span data-ttu-id="d5748-136">Considere o administrador do email para a Contoso Corporation, que precisa acessar os registros MX e TXT no ápice da zona 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="d5748-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="d5748-137">Ela não precisa ter acesso a nenhum outro registro MX, TXT nem de nenhum outro tipo.</span><span class="sxs-lookup"><span data-stu-id="d5748-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="d5748-138">O DNS do Azure permite que você atribua permissões no nível do conjunto de registros, exatamente aos registros aos quais o administrador de email precisa ter acesso.</span><span class="sxs-lookup"><span data-stu-id="d5748-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="d5748-139">O administrador de email recebe exatamente o controle de que precisa e não pode fazer nenhuma outra alteração.</span><span class="sxs-lookup"><span data-stu-id="d5748-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="d5748-140">Permissões de RBAC de nível do conjunto de registros podem ser configuradas por meio do Portal do Azure, usando o botão 'Usuários' na folha do conjunto de registros:</span><span class="sxs-lookup"><span data-stu-id="d5748-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![RBAC de nível do conjunto de registros por meio do Portal do Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="d5748-142">As permissões RBAC de nível do conjunto de registros também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="d5748-143">O comando equivalente também está [disponível por meio da CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="d5748-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="d5748-144">Funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="d5748-144">Custom roles</span></span>

<span data-ttu-id="d5748-145">A função interna 'Colaborador de Zona DNS' habilita o controle total sobre um recurso DNS.</span><span class="sxs-lookup"><span data-stu-id="d5748-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="d5748-146">Também é possível criar suas próprias funções de cliente do Azure, para fornecer um controle ainda mais refinado.</span><span class="sxs-lookup"><span data-stu-id="d5748-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="d5748-147">Considere novamente o exemplo em que um registro CNAME na zona 'customers.contoso.com' é criado para cada conta de cliente da Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="d5748-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="d5748-148">A conta usada para gerenciar esses CNAMEs deve ter permissão para gerenciar apenas registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="d5748-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="d5748-149">Ela não pode, portanto, modificar os registros de outros tipos (como alterar os registros MX) nem executar operações em nível de zona, como a exclusão de zona.</span><span class="sxs-lookup"><span data-stu-id="d5748-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="d5748-150">O exemplo a seguir mostra uma definição de função personalizada para gerenciar apenas registros CNAME:</span><span class="sxs-lookup"><span data-stu-id="d5748-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="d5748-151">A propriedade Actions define as seguintes permissões específicas do DNS:</span><span class="sxs-lookup"><span data-stu-id="d5748-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="d5748-152">`Microsoft.Network/dnsZones/CNAME/*` concede controle total sobre os registros CNAME</span><span class="sxs-lookup"><span data-stu-id="d5748-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="d5748-153">`Microsoft.Network/dnsZones/read` concede permissão para ler as zonas DNS, mas não para modificá-las, permitindo que você veja a zona na qual o CNAME está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="d5748-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="d5748-154">As Actions restantes são copiadas da [função interna de Colaborador de Zona DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="d5748-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="d5748-155">Usando uma função RBAC personalizada para evitar a exclusão de conjuntos de registros permitindo simultaneamente que eles sejam atualizados não é um controle efetivo.</span><span class="sxs-lookup"><span data-stu-id="d5748-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="d5748-156">Isso impede que os conjuntos de registro sejam excluídos, mas não impede que sejam modificados.</span><span class="sxs-lookup"><span data-stu-id="d5748-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="d5748-157">As modificações permitidas incluem adicionar e remover registros do conjunto de registros, incluindo a remoção de todos os registros para deixar um conjunto de registros 'vazio'.</span><span class="sxs-lookup"><span data-stu-id="d5748-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="d5748-158">Do ponto de vista de resolução de DNS, isso tem o mesmo efeito de excluir o registro.</span><span class="sxs-lookup"><span data-stu-id="d5748-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="d5748-159">Definições de função personalizadas não podem ser definidas por meio do Portal do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="d5748-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="d5748-160">Uma função personalizada com base nessa definição de função pode ser criada usando o Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d5748-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="d5748-161">Ela também pode ser criada por meio da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="d5748-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="d5748-162">A função pode então ser atribuída da mesma forma que as funções internas, conforme descrito anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d5748-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="d5748-163">Para obter mais informações sobre como criar, gerenciar e atribuir funções personalizadas, veja [Funções personalizadas no RBAC do Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="d5748-164">Bloqueios de recurso</span><span class="sxs-lookup"><span data-stu-id="d5748-164">Resource locks</span></span>

<span data-ttu-id="d5748-165">Além do RBAC, Azure Resource Manager dá suporte a outro tipo de controle de segurança, que é a capacidade de 'bloquear' recursos.</span><span class="sxs-lookup"><span data-stu-id="d5748-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="d5748-166">Onde as regras RBAC permitem controlar as ações de usuários e grupos específicos, bloqueios de recurso são aplicados ao recurso e entram em vigor para todos os usuários e funções.</span><span class="sxs-lookup"><span data-stu-id="d5748-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="d5748-167">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="d5748-168">Há dois tipos de bloqueio de recurso: **DoNotDelete** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="d5748-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="d5748-169">Eles podem ser aplicados a uma zona DNS ou a um conjunto de registros individual.</span><span class="sxs-lookup"><span data-stu-id="d5748-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="d5748-170">As seções a seguir descrevem vários cenários comuns e como dar suporte a eles usando bloqueios de recurso.</span><span class="sxs-lookup"><span data-stu-id="d5748-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="d5748-171">Proteção contra todas as alterações</span><span class="sxs-lookup"><span data-stu-id="d5748-171">Protecting against all changes</span></span>

<span data-ttu-id="d5748-172">Para impedir que quaisquer alterações sejam feitas, aplique um bloqueio ReadOnly à zona.</span><span class="sxs-lookup"><span data-stu-id="d5748-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="d5748-173">Isso impede que novos conjuntos de registros sejam criados e que os existentes sejam modificados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="d5748-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="d5748-174">Bloqueios de recurso em nível de zona podem ser criados via Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5748-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="d5748-175">Na folha da zona DNS, clique em 'Bloqueios' e, em seguida, em 'Adicionar':</span><span class="sxs-lookup"><span data-stu-id="d5748-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bloqueios de recurso em nível de zona via Portal do Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="d5748-177">Bloqueios de recurso em nível de zona podem ser criados via Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d5748-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="d5748-178">Não há suporte para configurar os bloqueios de recurso do Azure por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5748-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="d5748-179">Protegendo registros individuais</span><span class="sxs-lookup"><span data-stu-id="d5748-179">Protecting individual records</span></span>

<span data-ttu-id="d5748-180">Para impedir que um conjunto de registros DNS existente sofra modificações, aplique um bloqueio ReadOnly ao conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="d5748-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="d5748-181">Aplicar um bloqueio DoNotDelete a um conjunto de registros não é um controle efetivo.</span><span class="sxs-lookup"><span data-stu-id="d5748-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="d5748-182">Ele impede que os conjuntos de registro sejam excluídos, mas não impede que sejam modificados.</span><span class="sxs-lookup"><span data-stu-id="d5748-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="d5748-183">As modificações permitidas incluem adicionar e remover registros do conjunto de registros, incluindo a remoção de todos os registros para deixar um conjunto de registros 'vazio'.</span><span class="sxs-lookup"><span data-stu-id="d5748-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="d5748-184">Do ponto de vista de resolução de DNS, isso tem o mesmo efeito de excluir o registro.</span><span class="sxs-lookup"><span data-stu-id="d5748-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="d5748-185">Atualmente, os bloqueios de recurso em nível de conjunto de registros só podem ser configurados pelo uso do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5748-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="d5748-186">Eles não têm suporte no Portal do Azure nem na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5748-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="d5748-187">Proteção contra a exclusão de zona</span><span class="sxs-lookup"><span data-stu-id="d5748-187">Protecting against zone deletion</span></span>

<span data-ttu-id="d5748-188">Quando uma zona é excluída no DNS do Azure, todos os conjuntos de registros na zona também são excluídos.</span><span class="sxs-lookup"><span data-stu-id="d5748-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="d5748-189">Essa operação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="d5748-189">This operation cannot be undone.</span></span>  <span data-ttu-id="d5748-190">A exclusão acidental de uma zona crítica tem o potencial para ter um impacto significativo nos negócios.</span><span class="sxs-lookup"><span data-stu-id="d5748-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="d5748-191">Portanto, é muito importante proteger-se contra a exclusão acidental de zona.</span><span class="sxs-lookup"><span data-stu-id="d5748-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="d5748-192">Aplicar um bloqueio DoNotDelete a uma zona impede que a zona seja excluída.</span><span class="sxs-lookup"><span data-stu-id="d5748-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="d5748-193">No entanto, como os bloqueios são herdados pelos recursos filho, ele também impede que eventuais conjuntos de registros na zona sejam excluídos, o que pode ser indesejável.</span><span class="sxs-lookup"><span data-stu-id="d5748-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="d5748-194">Além disso, conforme descrito na observação acima, ele é também ineficaz, pois registros ainda podem ser removidos dos conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="d5748-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="d5748-195">Como alternativa, considere aplicar um bloqueio DoNotDelete em um conjunto de registros na zona, como o conjunto de registros SOA.</span><span class="sxs-lookup"><span data-stu-id="d5748-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="d5748-196">Uma vez que a zona não pode ser excluída sem excluir também os conjuntos de registros, isso protege contra a exclusão de zona embora ainda permita que conjuntos de registros dentro da zona sejam modificados livremente.</span><span class="sxs-lookup"><span data-stu-id="d5748-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="d5748-197">Se ocorrer uma tentativa de excluir a zona, o Azure Resource Manager detectará isso e também excluirá o conjunto de registros SOA, além de bloquear a chamada devido ao estado bloqueado do SOA.</span><span class="sxs-lookup"><span data-stu-id="d5748-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="d5748-198">Nenhum conjunto de registros é excluído.</span><span class="sxs-lookup"><span data-stu-id="d5748-198">No record sets are deleted.</span></span>

<span data-ttu-id="d5748-199">O comando do PowerShell a seguir cria um bloqueio DoNotDelete para o registro SOA da zona fornecida:</span><span class="sxs-lookup"><span data-stu-id="d5748-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="d5748-200">Outra maneira de evitar a exclusão acidental de zonas é usando uma função personalizada para garantir que o operador e as contas de serviço usados para gerenciar as zonas não tenham permissões de exclusão.</span><span class="sxs-lookup"><span data-stu-id="d5748-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="d5748-201">Quando você precisa excluir uma zona, pode impor uma exclusão em duas etapas, primeiro concedendo permissões de exclusão de zonas (no escopo de zona, para evitar excluir a zona errada) e depois para excluir a zona.</span><span class="sxs-lookup"><span data-stu-id="d5748-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="d5748-202">Essa segunda abordagem tem a vantagem de funcionar para todas as zonas acessadas por essas contas, sem ter que se lembrar de criar bloqueios.</span><span class="sxs-lookup"><span data-stu-id="d5748-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="d5748-203">Ela tem a desvantagem de que todas as contas com permissões de exclusão de zonas, como o proprietário da assinatura, ainda podem excluir acidentalmente uma zona crítica.</span><span class="sxs-lookup"><span data-stu-id="d5748-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="d5748-204">É possível usar as duas abordagens - bloqueios de recursos e funções personalizadas - ao mesmo tempo, como abordagem de defesa detalhada para a proteção de zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="d5748-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5748-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5748-205">Next steps</span></span>

* <span data-ttu-id="d5748-206">Para obter mais informações sobre como trabalhar com o RBAC, veja [Introdução ao gerenciamento de acesso no Portal do Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="d5748-207">Para obter mais informações sobre trabalho com bloqueios de recurso, confira [Bloquear recursos com o Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d5748-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

