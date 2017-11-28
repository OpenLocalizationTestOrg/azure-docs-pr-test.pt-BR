---
title: recurso de filho aaaDefine no modelo do Azure | Microsoft Docs
description: "Mostra como tooset Olá tipo de recurso e o nome de recurso filho em um modelo do Gerenciador de recursos do Azure"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="96bee-103">Definir o nome e o tipo do recurso filho no modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="96bee-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="96bee-104">Ao criar um modelo, você normalmente precisa tooinclude um recurso filho que é o recurso pai de tooa relacionados.</span><span class="sxs-lookup"><span data-stu-id="96bee-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="96bee-105">Por exemplo, o modelo pode incluir um banco de dados e um servidor SQL.</span><span class="sxs-lookup"><span data-stu-id="96bee-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="96bee-106">Olá SQL server é o recurso pai de Olá, e banco de dados de saudação recurso filho de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="96bee-107">formato de Olá Olá filho do tipo de recurso é:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="96bee-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="96bee-108">formato de saudação do nome de recurso Olá filho é:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="96bee-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="96bee-109">No entanto, você especificar o tipo hello e o nome de um modelo diferente com base em se ele está aninhado no recurso pai de hello, ou por conta própria no nível superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="96bee-110">Este tópico mostra como toohandle ambas as abordagens.</span><span class="sxs-lookup"><span data-stu-id="96bee-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="96bee-111">Ao construir um recurso de tooa referência totalmente qualificada, Olá ordem toocombine segmentos de tipo hello e nome não é simplesmente uma concatenação de saudação dois.</span><span class="sxs-lookup"><span data-stu-id="96bee-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="96bee-112">Em vez disso, após a saudação namespace, use uma sequência de *nome do tipo* pares de menos específico toomost específico:</span><span class="sxs-lookup"><span data-stu-id="96bee-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="96bee-113">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="96bee-113">For example:</span></span>

<span data-ttu-id="96bee-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`está correto, `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` não está correto</span><span class="sxs-lookup"><span data-stu-id="96bee-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="96bee-115">Recurso filho aninhado</span><span class="sxs-lookup"><span data-stu-id="96bee-115">Nested child resource</span></span>
<span data-ttu-id="96bee-116">toodefine de maneira mais fácil de saudação um recurso filho é toonest-lo no recurso pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="96bee-117">Olá, exemplo a seguir mostra um banco de dados SQL aninhado em um SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96bee-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="96bee-118">Para o recurso de filho hello, tipo de saudação está definido muito`databases` , mas seu tipo de recurso completo é `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="96bee-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="96bee-119">Você não fornecer `Microsoft.Sql/servers/` porque é considerado Olá pai do tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="96bee-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="96bee-120">nome do recurso filho Hello está definido muito`exampledatabase` mas nome completo Olá inclui o nome do pai hello.</span><span class="sxs-lookup"><span data-stu-id="96bee-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="96bee-121">Você não fornecer `exampleserver` porque supõe-se do recurso pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="96bee-122">Recurso filho de nível superior</span><span class="sxs-lookup"><span data-stu-id="96bee-122">Top-level child resource</span></span>
<span data-ttu-id="96bee-123">Você pode definir o recurso de filho Olá no nível superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="96bee-124">Você pode usar essa abordagem se o recurso pai de saudação não é implantado em Olá mesmo modelo, ou se deseja toouse `copy` toocreate vários recursos filho.</span><span class="sxs-lookup"><span data-stu-id="96bee-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="96bee-125">Com essa abordagem, forneça o tipo de recurso completo de saudação e incluem o nome do recurso pai Olá no nome de recurso Olá filho.</span><span class="sxs-lookup"><span data-stu-id="96bee-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="96bee-126">banco de dados de Olá é um servidor de toohello de recursos filho, embora elas são definidas em Olá mesmo nível no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bee-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96bee-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96bee-127">Next steps</span></span>
* <span data-ttu-id="96bee-128">Para obter recomendações sobre como toocreate modelos, consulte [práticas recomendadas para a criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="96bee-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="96bee-129">Para obter um exemplo de como criar vários recursos filho, consulte [Implantar várias instâncias de recursos nos modelos do Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="96bee-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
