---
title: "aaaHow tooUse controle de acesso baseado em função no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como toouse Olá funções internas e criar funções personalizadas no gerenciamento de API do Azure"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Como tooUse baseada em função de controle de acesso no gerenciamento de API do Azure
Gerenciamento de API do Azure depende de gerenciamento de acesso refinado tooenable o Access RBAC (controle) para serviços de gerenciamento de API e entidades (por exemplo, APIs, as políticas). Este artigo fornece uma visão geral das funções internas e personalizadas de saudação no gerenciamento de API. Se você quiser obter mais detalhes sobre o gerenciamento de acesso no hello portal do Azure, consulte [Introdução ao gerenciamento de acesso no hello portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Funções internas
Gerenciamento de API no momento fornece 3 funções internas e adicionará 2 mais funções hello futuro próximo. Essas funções podem ser atribuídas em escopos diferentes, incluindo assinatura, grupo de recursos e instância individual do Gerenciamento de API. Por exemplo, se função de "Leitor de serviço de gerenciamento de API do Azure" hello é atribuída tooan usuário no nível do grupo de recursos de saudação, em seguida, hello usuário terão instâncias de API de gerenciamento do acesso de leitura tooall dentro do grupo de recursos de saudação. 

Olá tabela a seguir fornece descrições breves de saudação funções internas. Você pode atribuir essas funções usando Olá Portal do Azure ou outras ferramentas, incluindo o Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), o Azure [interface de linha de comando](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), e [API REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Para obter detalhes sobre como as funções internas de tooassign, consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Função          | Acesso de leitura<sup>[1]</sup> | Acesso de gravação<sup>[2]</sup> | Criação, exclusão, dimensionamento do serviço, configuração de VPN e domínio personalizado | Acesso toolegacy Publsiher Portal | Descrição
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Colaborador do serviço de Gerenciamento de API do Azure | ✓ | ✓  | ✓  | ✓ | Superusuário. Tem completo CRUD acessar serviços de gerenciamento de tooAPI e entidades (por exemplo, APIs, as políticas). Tem acesso toohello publicador herdados portal. |
| Leitor do serviço de Gerenciamento de API do Azure | ✓  | | || Tem entidades e os serviços de gerenciamento de tooAPI acesso somente leitura. |
| Operador do serviço de Gerenciamento de API do Azure | ✓ | | ✓ | | Pode gerenciar os serviços de Gerenciamento de API, mas não as entidades.|
| Editor do serviço de Gerenciamento de API do Azure<sup>*</sup> | ✓ | ✓ | |  | Pode gerenciar as entidades de Gerenciamento de API, mas não os serviços.|
| Gerenciador de conteúdo do Gerenciamento de API do Azure<sup>*</sup> | ✓ | | | ✓ | Pode gerenciar o portal do desenvolvedor. Acesso somente leitura tooservices e entidades.|

<sup>[1] serviços de gerenciamento do acesso de leitura tooAPI e entidades (por exemplo, APIs, as políticas)</sup>

<sup>Serviços de gerenciamento do [2], acesso de gravação tooAPI e entidades, exceto opeartions seguintes: 1) instância criação, exclusão e dimensionamento de configuração de nome de domínio do VPN 2) configuração 3) personalizado</sup>

<sup>\*função de Editor de serviço de saudação estarão disponível depois que migramos todos admin da interface do usuário da saudação existente publicador portal toohello portal do Azure. Olá função Gerenciador de conteúdo estará disponível após o portal do publicador Olá, é refatorado tooonly conter portal do desenvolvedor funcionalidades relacionadas toomanaging hello.</sup>  


## <a name="custom-roles"></a>Funções personalizadas
Se nenhuma das funções internas Olá atender às suas necessidades específicas, funções personalizadas podem ser criadas tooprovide mais granular gerenciamento para entidades de gerenciamento de API de acesso. Por exemplo, você pode criar uma função personalizada que tem acesso somente leitura tooan serviço de gerenciamento de API, mas só tem acesso de gravação tooone específico API. mais detalhes sobre funções personalizadas, consulte o toolearn [funções personalizadas no Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Quando você cria uma função personalizada, é mais fácil toostart com uma das funções internas de saudação. Editar saudação atributos tooadd ações hello, NotActions ou AssignableScopes, salvar as alterações de saudação como uma nova função. Olá exemplo a seguir começa com a função de "serviço de gerenciamento do Azure API Reader" hello e cria uma função personalizada chamada "Editor de API de calculadora". função personalizada Olá pode ser atribuída somente tooa que API específica, portanto, só será tem acesso toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Assista a uma visão geral em vídeo

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre o Controle de Acesso baseado em função no Azure
  * [Introdução ao gerenciamento de acesso no hello portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Funções personalizadas no Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
