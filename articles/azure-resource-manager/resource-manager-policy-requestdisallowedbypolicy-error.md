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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="4bf37-103">Erro RequestDisallowedByPolicy com a política de recurso do Azure</span><span class="sxs-lookup"><span data-stu-id="4bf37-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="4bf37-104">Este artigo descreve a causa de saudação do erro de RequestDisallowedByPolicy Olá, ele também fornece solução para esse erro.</span><span class="sxs-lookup"><span data-stu-id="4bf37-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="4bf37-105">Sintoma</span><span class="sxs-lookup"><span data-stu-id="4bf37-105">Symptom</span></span>

<span data-ttu-id="4bf37-106">Quando você tenta toodo uma ação durante a implantação, você poderá receber um **RequestDisallowedByPolicy** erro que impede Olá ação ser executada.</span><span class="sxs-lookup"><span data-stu-id="4bf37-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="4bf37-107">a seguir Olá é um exemplo de erro de saudação:</span><span class="sxs-lookup"><span data-stu-id="4bf37-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="4bf37-108">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="4bf37-108">Troubleshooting</span></span>

<span data-ttu-id="4bf37-109">tooretrieve detalhes sobre a política de saudação que bloqueou a sua implantação, use Olá seguindo um dos métodos de saudação:</span><span class="sxs-lookup"><span data-stu-id="4bf37-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="4bf37-110">Método 1</span><span class="sxs-lookup"><span data-stu-id="4bf37-110">Method 1</span></span>

<span data-ttu-id="4bf37-111">No PowerShell, fornecem esse identificador de política como Olá **Id** detalhes do parâmetro tooretrieve sobre a política de saudação que bloqueou a sua implantação.</span><span class="sxs-lookup"><span data-stu-id="4bf37-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="4bf37-112">Método 2</span><span class="sxs-lookup"><span data-stu-id="4bf37-112">Method 2</span></span> 

<span data-ttu-id="4bf37-113">No 2.0 do CLI do Azure, forneça o nome de saudação da definição de política de saudação:</span><span class="sxs-lookup"><span data-stu-id="4bf37-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="4bf37-114">Solução</span><span class="sxs-lookup"><span data-stu-id="4bf37-114">Solution</span></span>

<span data-ttu-id="4bf37-115">Para segurança ou conformidade, seu departamento de TI pode impor uma política de recurso que proíbe a criação de Endereços IP públicos, Grupos de Segurança de Rede, Rotas Definidas pelo Usuário ou tabelas de rotas.</span><span class="sxs-lookup"><span data-stu-id="4bf37-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="4bf37-116">Exemplo hello Olá de mensagem de erro que é descrita na seção "Sintomas" de saudação, política de saudação é denominada **regionPolicyDefinition**, mas ele pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="4bf37-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="4bf37-117">tooresolve esse problema, trabalhar com suas políticas de recursos de TI departamento tooreview hello e determinar como Olá tooperform solicitada ação em conformidade com as políticas.</span><span class="sxs-lookup"><span data-stu-id="4bf37-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="4bf37-118">Para obter mais informações, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bf37-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="4bf37-119">Visão geral da política de recurso</span><span class="sxs-lookup"><span data-stu-id="4bf37-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="4bf37-120">Erros comuns de implantação – RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="4bf37-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


