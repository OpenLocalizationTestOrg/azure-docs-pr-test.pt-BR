---
title: Definir o recurso filho no modelo do Azure | Microsoft Docs
description: Mostra como definir o tipo de recurso e o nome do recurso filho em um modelo do Azure Resource Manager
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="1f53a-103">Definir o nome e o tipo do recurso filho no modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f53a-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="1f53a-104">Ao criar um modelo, você frequentemente precisa incluir um recurso filho que está relacionado a um recurso pai.</span><span class="sxs-lookup"><span data-stu-id="1f53a-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="1f53a-105">Por exemplo, o modelo pode incluir um banco de dados e um servidor SQL.</span><span class="sxs-lookup"><span data-stu-id="1f53a-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="1f53a-106">O servidor SQL é o recurso pai e o banco de dados é o recurso filho.</span><span class="sxs-lookup"><span data-stu-id="1f53a-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="1f53a-107">O formato do tipo do recurso filho é: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="1f53a-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="1f53a-108">O formato do nome do recurso filho é: `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="1f53a-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="1f53a-109">No entanto, o tipo e o nome são especificados de forma diferente no modelo dependendo de estarem aninhados no recurso pai ou sozinhos no nível superior.</span><span class="sxs-lookup"><span data-stu-id="1f53a-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="1f53a-110">Este tópico mostra como lidar com as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="1f53a-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="1f53a-111">Ao construir uma referência totalmente qualificada para um recurso, a ordem para combinar os segmentos do tipo e nome não é simplesmente uma concatenação dos dois.</span><span class="sxs-lookup"><span data-stu-id="1f53a-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="1f53a-112">Em vez disso, após o namespace, use uma sequência de pares *tipo/nome* do menos específico para o mais específico:</span><span class="sxs-lookup"><span data-stu-id="1f53a-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="1f53a-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1f53a-113">For example:</span></span>

<span data-ttu-id="1f53a-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`está correto, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` não está correto</span><span class="sxs-lookup"><span data-stu-id="1f53a-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="1f53a-115">Recurso filho aninhado</span><span class="sxs-lookup"><span data-stu-id="1f53a-115">Nested child resource</span></span>
<span data-ttu-id="1f53a-116">A maneira mais fácil de definir um recurso filho é aninhando-o dentro do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="1f53a-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="1f53a-117">O exemplo a seguir mostra um Banco de Dados SQL aninhado em um SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1f53a-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="1f53a-118">Para o recurso filho, o tipo é definido como `databases` , mas seu tipo de recurso completo é `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="1f53a-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="1f53a-119">O `Microsoft.Sql/servers/` não é fornecido porque ele é presumido do tipo de recurso pai.</span><span class="sxs-lookup"><span data-stu-id="1f53a-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="1f53a-120">O nome do recurso filho é definido como `exampledatabase` , mas o nome completo inclui o nome do pai.</span><span class="sxs-lookup"><span data-stu-id="1f53a-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="1f53a-121">O `exampleserver` não é fornecido porque ele é presumido do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="1f53a-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="1f53a-122">Recurso filho de nível superior</span><span class="sxs-lookup"><span data-stu-id="1f53a-122">Top-level child resource</span></span>
<span data-ttu-id="1f53a-123">Você pode definir o recurso filho no nível superior.</span><span class="sxs-lookup"><span data-stu-id="1f53a-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="1f53a-124">Você pode usar essa abordagem se o recurso pai não estiver implantado no mesmo modelo ou se quiser usar o `copy` para criar vários recursos filho.</span><span class="sxs-lookup"><span data-stu-id="1f53a-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="1f53a-125">Com essa abordagem, forneça o tipo de recurso completo e inclua o nome do recurso pai no nome do recurso filho.</span><span class="sxs-lookup"><span data-stu-id="1f53a-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="1f53a-126">O banco de dados é um recurso filho para o servidor mesmo que eles estejam definidos no mesmo nível do modelo.</span><span class="sxs-lookup"><span data-stu-id="1f53a-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f53a-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f53a-127">Next steps</span></span>
* <span data-ttu-id="1f53a-128">Para ver recomendações sobre como criar modelos, consulte [Práticas recomendadas para criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="1f53a-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="1f53a-129">Para obter um exemplo de como criar vários recursos filho, consulte [Implantar várias instâncias de recursos nos modelos do Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1f53a-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
