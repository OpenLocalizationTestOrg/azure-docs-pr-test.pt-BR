---
title: "Erro de aaaRequestDisallowedByPolicy com a política de recurso do Azure | Microsoft Docs"
description: "Descreve a causa Olá Olá RequestDisallowedByPolicy erro."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Erro RequestDisallowedByPolicy com a política de recurso do Azure

Este artigo descreve a causa de saudação do erro de RequestDisallowedByPolicy Olá, ele também fornece solução para esse erro.

## <a name="symptom"></a>Sintoma

Quando você tenta toodo uma ação durante a implantação, você poderá receber um **RequestDisallowedByPolicy** erro que impede Olá ação ser executada. a seguir Olá é um exemplo de erro de saudação:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Solucionar problemas

tooretrieve detalhes sobre a política de saudação que bloqueou a sua implantação, use Olá seguindo um dos métodos de saudação:

### <a name="method-1"></a>Método 1

No PowerShell, fornecem esse identificador de política como Olá **Id** detalhes do parâmetro tooretrieve sobre a política de saudação que bloqueou a sua implantação.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Método 2 

No 2.0 do CLI do Azure, forneça o nome de saudação da definição de política de saudação: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Solução

Para segurança ou conformidade, seu departamento de TI pode impor uma política de recurso que proíbe a criação de Endereços IP públicos, Grupos de Segurança de Rede, Rotas Definidas pelo Usuário ou tabelas de rotas. Exemplo hello Olá de mensagem de erro que é descrita na seção "Sintomas" de saudação, política de saudação é denominada **regionPolicyDefinition**, mas ele pode ser diferente.
tooresolve esse problema, trabalhar com suas políticas de recursos de TI departamento tooreview hello e determinar como Olá tooperform solicitada ação em conformidade com as políticas.


Para obter mais informações, consulte Olá artigos a seguir:

- [Visão geral da política de recurso](resource-manager-policy.md)
- [Erros comuns de implantação – RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


