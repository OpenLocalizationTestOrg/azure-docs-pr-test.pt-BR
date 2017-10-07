---
title: "políticas de laboratório aaaGrant usuário permissões toospecific | Microsoft Docs"
description: "Saiba como toogrant permissões toospecific laboratório as políticas de usuário no DevTest Labs com base nas necessidades de cada usuário"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Conceder permissões de usuário toospecific políticas de laboratório
## <a name="overview"></a>Visão geral
Este artigo ilustra como toouse política do PowerShell toogrant usuários permissões tooa laboratório específico. Dessa forma, as permissões podem ser aplicadas com base nas necessidades de cada usuário. Por exemplo, convém toogrant um configurações de política específica de usuário Olá capacidade toochange Olá VM, mas não Olá custo políticas.

## <a name="policies-as-resources"></a>Políticas como recursos
Conforme discutido em Olá [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md) artigo, RBAC permite o gerenciamento de acesso refinado de recursos do Azure. Usando o RBAC, você pode separar as tarefas dentro de sua equipe de DevOps e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos.

Em DevTest Labs, uma política é um tipo de recurso que permite que a ação de RBAC Olá **Microsoft.DevTestLab/labs/policySets/policies/**. Cada política de laboratório é um recurso no tipo de recurso de política de saudação e pode ser atribuída como uma função RBAC tooan escopo.

Por exemplo, em ordem toogrant usuários leitura/gravação permissão toohello **permitidos tamanhos de VM** política, você deve criar uma função personalizada que funciona com hello **Microsoft.DevTestLab/labs/policySets/policies/** * a ação e, em seguida, atribuir Olá usuários apropriados toothis função personalizada no escopo de saudação do **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn mais informações sobre funções personalizadas em RBAC, consulte Olá [funções personalizadas de controle de acesso](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Criar uma função personalizada do laboratório usando o PowerShell
Em tooget ordem iniciado, você precisará Olá tooread artigo que explica a seguir como tooinstall e configurar os cmdlets do PowerShell do Azure Olá: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Depois que você configurou Olá cmdlets do PowerShell do Azure, você pode executar Olá tarefas a seguir:

* Lista todas as operações/ações Olá para um provedor de recursos
* Listar ações em uma função específica:
* Criar uma função personalizada

saudação de script do PowerShell a seguir mostra exemplos de como tooperform essas tarefas:

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Atribuir permissões tooa usuário para uma política específica usando funções personalizadas
Depois que você tiver definido suas funções personalizadas, você pode atribuí-los toousers. Em ordem tooassign um usuário de tooa de função personalizada, você deve primeiro obter Olá **ObjectId** representar esse usuário. toodo que use Olá **AzureRmADUser Get** cmdlet.

Em Olá exemplo a seguir, Olá **ObjectId** de saudação *SomeUser* usuário é 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Depois que você tiver Olá **ObjectId** para usuário hello e um nome de função personalizada, você pode atribuir usuário função toohello com hello **AzureRmRoleAssignment novo** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

No exemplo anterior de saudação, Olá **AllowedVmSizesInLab** política é usada. Você pode usar qualquer um dos Olá políticas a seguir:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Próximas etapas
Uma vez você concedeu políticas de laboratório de toospecific de permissões de usuário, aqui estão alguns próxima tooconsider de etapas:

* [Laboratório de tooa acesso seguro](devtest-lab-add-devtest-user.md).
* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md).
* [Criar um modelo de laboratório](devtest-lab-create-template.md).
* [Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).
* [Adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md).

