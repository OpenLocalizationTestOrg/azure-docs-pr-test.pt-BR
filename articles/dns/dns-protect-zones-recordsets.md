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
# <a name="how-tooprotect-dns-zones-and-records"></a>Como tooprotect DNS zonas e os registros

Registros e zonas DNS são recursos críticos. Excluir uma zona DNS ou até mesmo um único registro DNS pode resultar em uma interrupção total do serviço.  Portanto, é importante que registros e zonas DNS críticos sejam protegidos contra alterações acidentais ou não autorizadas.

Este artigo explica como DNS do Azure permite que você tooprotect suas zonas DNS e registros de acordo com essas alterações.  Podemos aplicar dois recursos de segurança avançados fornecidos pelo Azure Resource Manager: [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) e [bloqueios de recurso](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Controle de acesso baseado em função

O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o usuários, grupos e recursos do Azure. Usando o RBAC, você pode conceder com precisão a quantidade Olá de acesso que os usuários precisam tooperform seus trabalhos. Para obter mais informações sobre como o RBAC ajuda você a gerenciar o acesso, veja [O que é Controle de Acesso Baseado em Função](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>função de 'Colaborador de zona DNS' Hello

função de 'Colaborador de zona DNS' Hello é uma função interna fornecida pelo Azure para gerenciamento de recursos DNS.  Atribuindo grupo ou usuário de tooa de permissões de Colaborador de zona do DNS permite que os recursos do grupo toomanage DNS, mas não os recursos de qualquer outro tipo.

Por exemplo, suponha que grupo de recursos de saudação 'myzones' contém cinco zonas para Contoso Corporation. Concessão Olá DNS administrador 'Colaborador de zona DNS' permissões toothat grupo de recursos, permite controle total sobre as zonas DNS. Ele também evita conceder permissões desnecessárias, administrador do DNS por exemplo hello não é possível criar ou parar máquinas virtuais.

permissões de RBAC de tooassign de maneira mais simples de saudação é [por meio do portal do Azure de saudação](../active-directory/role-based-access-control-configure.md).  Abra a folha de saudação 'controle de acesso (IAM)' para o grupo de recursos Olá, e em seguida, clique em 'Adicionar' e selecione função de 'Colaborador de zona DNS' hello e usuários Selecione Olá necessário ou toogrant permissões.

![Nível de grupo de recursos RBAC via Olá portal do Azure](./media/dns-protect-zones-recordsets/rbac1.png)

As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>RBAC de nível de zona

Regras RBAC do Azure podem ser aplicadas tooa assinatura, um recurso de chamadas individual tooan ou de grupo de recursos. No caso de saudação do DNS do Azure, esse recurso pode ser uma zona DNS individual, ou até mesmo um conjunto de registros individual.

Por exemplo, suponha que o grupo de recursos de saudação 'myzones' contém Olá zona 'contoso.com' e uma subzona 'customers.contoso.com' no qual os registros CNAME são criados para cada conta de cliente.  Olá conta usada toomanage esses registros CNAME devem ser atribuídos permissões toocreate registros Olá 'customers.contoso.com' zona apenas, ele não deve ter acesso toohello outras regiões.

Podem ser concedidas permissões em nível de zona RBAC via Olá portal do Azure.  Abrir Olá 'Controle de acesso (IAM)' folha para a zona Olá, em seguida, clique em 'Adicionar' e selecione função de 'Colaborador de zona DNS' hello e usuários Selecione Olá necessário ou toogrant permissões.

![RBAC nível de zona do DNS por meio de saudação portal do Azure](./media/dns-protect-zones-recordsets/rbac2.png)

As permissões também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>RBAC de nível do conjunto de registros

Podemos ir uma etapa adiante. Considere Olá administrador do sistema para a Contoso Corporation, que precisa de acesso toohello MX e registros TXT no ápice da saudação da zona de 'contoso.com' hello.  Ela não precisa acessar tooany outros registros MX ou TXT ou tooany registros de qualquer outro tipo.  DNS do Azure permite a você permissões tooassign Olá conjunto de registros de nível, tooprecisely Olá registros que Olá administrador de mail precisa acessar.  Olá administrador de mail é concedido controle Olá ela precisa e é toomake não é possível que outras alterações.

Permissões RBAC no nível do conjunto de registros podem ser configuradas via Olá portal do Azure, usando o botão de saudação 'usuários' na folha de conjunto de registros de saudação:

![Nível de RBAC por meio do portal do Azure de saudação do conjunto de registros](./media/dns-protect-zones-recordsets/rbac3.png)

As permissões RBAC de nível do conjunto de registros também podem ser [concedidas usando o Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

comando equivalente Olá também é [disponíveis por meio de saudação CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Funções personalizadas

função interna de 'Colaborador de zona DNS' Hello permite controle total sobre um recurso DNS. Ele também é possível toobuild seu próprio cliente Azure funções, tooprovide mesmo refinado controle.

Considere novamente o exemplo hello em que um registro CNAME na zona Olá 'customers.contoso.com' é criado para cada conta de cliente da Contoso Corporation.  Olá conta usada toomanage esses CNAMEs devem ser concedidas permissão toomanage CNAME somente registros.  É, em seguida, não é possível toomodify registros de outros tipos (como alterar os registros MX) ou executar operações de nível de zona, como a exclusão de zona.

saudação de exemplo a seguir mostra uma definição de função personalizada para gerenciar apenas os registros CNAME:

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

Olá propriedade ações define Olá permissões específicas do DNS a seguir:

* `Microsoft.Network/dnsZones/CNAME/*` concede controle total sobre os registros CNAME
* `Microsoft.Network/dnsZones/read`concede as zonas DNS de tooread de permissão, mas não toomodify-los, permitindo que você toosee Olá zona no qual Olá CNAME está sendo criada.

Olá ações restantes são copiadas do hello [função de Colaborador de zona DNS interna](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Usar um tooprevent personalizada de função RBAC excluir registro define enquanto ainda permite que eles toobe atualizada não é um controle eficiente. Isso impede que os conjuntos de registro sejam excluídos, mas não impede que sejam modificados.  Modificações permitidas incluem a adição e remoção de registros do conjunto de registros de hello, incluindo a remoção de todos os registros tooleave um conjunto de registros 'empty'. Isso tem Olá mesmo efeito de exclusão de registro Olá definido de um ponto de vista de resolução DNS.

Definições de função personalizada não podem ser definidas no momento por meio de saudação portal do Azure. Uma função personalizada com base nessa definição de função pode ser criada usando o Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Ele também pode ser criado por meio de saudação CLI do Azure:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello função pode ser atribuída em Olá mesma forma como as funções internas, como descrito anteriormente neste artigo.

Para obter mais informações sobre como toocreate, gerenciar e atribuir funções personalizadas, consulte [funções personalizadas no Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Bloqueios de recurso

Em adição tooRBAC, Gerenciador de recursos do Azure oferece suporte a outro tipo de controle de segurança, ou seja, too'lock de capacidade de saudação ' recursos. Onde as regras RBAC permitirem toocontrol ações de saudação de usuários e grupos específicos, bloqueios de recursos são aplicados toohello recursos e entrarão em vigor em todos os usuários e funções. Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).

Há dois tipos de bloqueio de recurso: **DoNotDelete** e **ReadOnly**. Elas podem ser aplicadas tooa zona DNS ou tooan conjunto de registros individuais.  Olá, seções a seguir descrevem vários cenários comuns e como toosupport-los usando bloqueios de recursos.

### <a name="protecting-against-all-changes"></a>Proteção contra todas as alterações

tooprevent as alterações que estão sendo feitas, aplicar uma zona de toohello de bloqueio de somente leitura.  Isso impede que novos conjuntos de registros sejam criados e que os existentes sejam modificados ou excluídos.

Bloqueios de recursos de nível de zona podem ser criados por meio de saudação portal do Azure.  Na folha de zona do DNS hello, clique em 'Bloqueios', em seguida, 'Add':

![Bloqueios de recursos de nível de zona via Olá portal do Azure](./media/dns-protect-zones-recordsets/locks1.png)

Bloqueios de recurso em nível de zona podem ser criados via Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Não é suportada atualmente ao configurar os bloqueios de recursos do Azure por meio de saudação CLI do Azure.

### <a name="protecting-individual-records"></a>Protegendo registros individuais

tooprevent um registro DNS existente definida contra a modificação, se aplicam a um conjunto de registros do toohello de bloqueio de somente leitura.

> [!NOTE]
> Aplicar um tooa de bloqueio DoNotDelete conjunto de registros não é um controle eficiente. Isso impede que o registro Olá definir sejam excluídas, mas ele não impede que ele está sendo modificado.  Modificações permitidas incluem a adição e remoção de registros do conjunto de registros de hello, incluindo a remoção de todos os registros tooleave um conjunto de registros 'empty'. Isso tem Olá mesmo efeito de exclusão de registro Olá definido de um ponto de vista de resolução DNS.

Atualmente, os bloqueios de recurso em nível de conjunto de registros só podem ser configurados pelo uso do Azure PowerShell.  Eles não têm suporte no portal do Azure de saudação ou CLI do Azure.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Proteção contra a exclusão de zona

Quando uma zona é excluída no DNS do Azure, todos os conjuntos de registros na zona Olá também são excluídos.  Essa operação não pode ser desfeita.  A exclusão acidental de uma zona crítica tem toohave potencial Olá um impacto significativo nos negócios.  Portanto, é muito importante tooprotect contra a exclusão acidental de zona.

Aplicar uma zona de tooa DoNotDelete bloqueio impede a zona Olá sejam excluídas.  No entanto, desde que os bloqueios são herdados pelos recursos filho, ele também evita qualquer conjuntos de registros na zona de saudação sejam excluídas, que pode ser indesejável.  Além disso, conforme descrito na nota da saudação acima, também é ineficiente desde registros ainda podem ser removidos de conjuntos de registros existentes hello.

Como alternativa, considere a aplicação de um registro de tooa DoNotDelete bloqueio definido na zona hello, como o conjunto de registros de SOA hello.  Desde que a zona de saudação não pode ser excluída sem também excluir conjuntos de registros Olá, isso protege contra a exclusão de zona, enquanto ainda permite que os conjuntos de registros dentro de saudação zona toobe modificadas livremente. Se uma tentativa for feita toodelete zona de hello, Azure Resource Manager detecta isso também deve excluir conjunto de registros de SOA hello e blocos Olá chamada porque Olá SOA está bloqueado.  Nenhum conjunto de registros é excluído.

saudação de comando do PowerShell a seguir cria um bloqueio de DoNotDelete no registro SOA de saudação do hello dada zona:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Permissões de exclusão de outra forma, a exclusão acidental de zona tooprevent está usando um operador de saudação tooensure função personalizada e o serviço contas usadas toomanage suas zonas não têm de zona. Quando você precisar toodelete uma zona, você pode impor uma exclusão de duas etapas, primeiro conceder permissões de exclusão de zona (no escopo de zona de hello, tooprevent Excluir zona errado Olá) e a segunda zona de saudação toodelete.

Essa segunda abordagem tem a vantagem de saudação que funciona para todas as zonas acessadas por essas contas, sem a necessidade tooremember toocreate todos os bloqueios. Ele tem a desvantagem de saudação que todas as contas com permissões de exclusão de zona, como o proprietário da assinatura hello, ainda acidentalmente podem excluir uma zona crítica.

É possível toouse - bloqueios de recursos e funções personalizadas - ambas as abordagens em Olá a mesma hora, como uma abordagem de defesa em profundidade tooDNS zona a proteção.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre como trabalhar com RBAC, consulte [Introdução ao gerenciamento de acesso no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).
* Para obter mais informações sobre trabalho com bloqueios de recurso, confira [Bloquear recursos com o Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

