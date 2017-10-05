---
title: "Entender como criar definição de interface do usuário para aplicativos gerenciados do Azure | Microsoft Docs"
description: "Descreve como criar definições de interface do usuário para aplicativos gerenciados do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="b7d77-103">Introdução a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="b7d77-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="b7d77-104">Este documento apresenta os conceitos básicos de um CreateUiDefinition, que é usado pelo portal do Azure para gerar a interface do usuário para a criação de um aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="b7d77-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="b7d77-105">Um CreateUiDefinition sempre contém três propriedades:</span><span class="sxs-lookup"><span data-stu-id="b7d77-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="b7d77-106">handler</span><span class="sxs-lookup"><span data-stu-id="b7d77-106">handler</span></span>
* <span data-ttu-id="b7d77-107">version</span><span class="sxs-lookup"><span data-stu-id="b7d77-107">version</span></span>
* <span data-ttu-id="b7d77-108">parameters</span><span class="sxs-lookup"><span data-stu-id="b7d77-108">parameters</span></span>

<span data-ttu-id="b7d77-109">Para aplicativos gerenciados, o manipulador deve sempre ser `Microsoft.Compute.MultiVm`, e a versão mais recente com suporte é `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="b7d77-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="b7d77-110">O esquema da propriedade parameters depende da combinação do manipulador e da versão especificados.</span><span class="sxs-lookup"><span data-stu-id="b7d77-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="b7d77-111">Para aplicativos gerenciados, as propriedades com suporte são `basics`, `steps` e `outputs`.</span><span class="sxs-lookup"><span data-stu-id="b7d77-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="b7d77-112">As propriedades basic e steps contêm os _elementos_, como caixas de texto e listas suspensas, que serão exibidos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d77-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="b7d77-113">A propriedade outputs é usada para mapear os valores de saída de elementos especificados para os parâmetros do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7d77-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="b7d77-114">A inclusão de `$schema` é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="b7d77-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="b7d77-115">Se especificado, o valor de `version` deve corresponder à versão dentro do URI `$schema`.</span><span class="sxs-lookup"><span data-stu-id="b7d77-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="b7d77-116">Noções básicas</span><span class="sxs-lookup"><span data-stu-id="b7d77-116">Basics</span></span>
<span data-ttu-id="b7d77-117">A etapa Noções básicas é sempre a primeira etapa do assistente gerada quando o portal do Azure analisa um CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="b7d77-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="b7d77-118">Além de exibir os elementos especificados em `basics`, o portal injeta elementos para que os usuários escolham a assinatura, o grupo de recursos e o local da implantação.</span><span class="sxs-lookup"><span data-stu-id="b7d77-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="b7d77-119">Em geral, elementos que fazem consulta de parâmetros de toda a implantação, como nome de um cluster ou credenciais de administrador, devem entrar nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="b7d77-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="b7d77-120">Se o comportamento de um elemento depende da assinatura, do grupo de recursos ou do local do usuário, esse elemento não pode ser usado em basics.</span><span class="sxs-lookup"><span data-stu-id="b7d77-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="b7d77-121">Por exemplo, **Microsoft.Compute.SizeSelector** depende da assinatura e do local para determinar a lista de tamanhos disponíveis para o usuário.</span><span class="sxs-lookup"><span data-stu-id="b7d77-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="b7d77-122">Portanto, **Microsoft.Compute.SizeSelector** só pode ser usado em steps.</span><span class="sxs-lookup"><span data-stu-id="b7d77-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="b7d77-123">Geralmente, apenas os elementos no namespace **Microsoft.Common** podem ser usados em basics.</span><span class="sxs-lookup"><span data-stu-id="b7d77-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="b7d77-124">No entanto, alguns elementos de outros namespaces (como **Microsoft.Compute.Credentials**) que não dependem do contexto do usuário ainda são permitidos.</span><span class="sxs-lookup"><span data-stu-id="b7d77-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="b7d77-125">Etapas</span><span class="sxs-lookup"><span data-stu-id="b7d77-125">Steps</span></span>
<span data-ttu-id="b7d77-126">A propriedade steps pode conter uma ou mais etapas adicionais para exibir depois de basics, cada uma contendo um ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="b7d77-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="b7d77-127">Considere adicionar etapas por função ou camada do aplicativo que está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="b7d77-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="b7d77-128">Por exemplo, adicione uma etapa nas entradas para os nós mestres e uma etapa para os nós de trabalho em um cluster.</span><span class="sxs-lookup"><span data-stu-id="b7d77-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="b7d77-129">outputs</span><span class="sxs-lookup"><span data-stu-id="b7d77-129">Outputs</span></span>
<span data-ttu-id="b7d77-130">O portal do Azure usa a propriedade `outputs` para mapear os elementos de `basics` e `steps` para os parâmetros do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7d77-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="b7d77-131">As chaves do dicionário são os nomes dos parâmetros do modelo, e os valores são propriedades dos objetos da saída dos elementos referenciados.</span><span class="sxs-lookup"><span data-stu-id="b7d77-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="b7d77-132">Funções</span><span class="sxs-lookup"><span data-stu-id="b7d77-132">Functions</span></span>
<span data-ttu-id="b7d77-133">Semelhantemente às [funções de modelo](resource-group-template-functions.md) no Azure Resource Manager (tanto em sintaxe quanto em funcionalidade), CreateUiDefinition fornece funções para trabalhar com entradas e saídas dos elementos e recursos como condicionais.</span><span class="sxs-lookup"><span data-stu-id="b7d77-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7d77-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7d77-134">Next steps</span></span>
<span data-ttu-id="b7d77-135">O próprio CreateUiDefinition tem um esquema simples.</span><span class="sxs-lookup"><span data-stu-id="b7d77-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="b7d77-136">A profundidade real vem de todos os elementos e funções com suporte que os documentos abaixo descrevem em muitos detalhes:</span><span class="sxs-lookup"><span data-stu-id="b7d77-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="b7d77-137">Elementos</span><span class="sxs-lookup"><span data-stu-id="b7d77-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="b7d77-138">Funções</span><span class="sxs-lookup"><span data-stu-id="b7d77-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="b7d77-139">Um esquema JSON atual para CreateUiDefinition está disponível aqui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="b7d77-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="b7d77-140">Versões mais recentes serão disponibilizadas no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="b7d77-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="b7d77-141">Substitua a parte `0.1.2-preview` da URL e o valor `version` pelo identificador de versão que você pretende usar.</span><span class="sxs-lookup"><span data-stu-id="b7d77-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="b7d77-142">Os identificadores de versão com suporte atualmente são `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview` e `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="b7d77-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>