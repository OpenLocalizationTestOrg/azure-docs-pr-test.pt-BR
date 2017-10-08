---
title: "aaaUnderstand criação de definição de interface do usuário para aplicativos gerenciados do Azure | Microsoft Docs"
description: "Descreve como toocreate definições de interface do usuário para aplicativos gerenciados do Azure"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="dc2a8-103">Introdução a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="dc2a8-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="dc2a8-104">Este documento apresenta os conceitos básicos de saudação de um CreateUiDefinition, que é usado pela interface de usuário de Olá Olá toogenerate portal do Azure para criar um aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="dc2a8-105">Um CreateUiDefinition sempre contém três propriedades:</span><span class="sxs-lookup"><span data-stu-id="dc2a8-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="dc2a8-106">handler</span><span class="sxs-lookup"><span data-stu-id="dc2a8-106">handler</span></span>
* <span data-ttu-id="dc2a8-107">version</span><span class="sxs-lookup"><span data-stu-id="dc2a8-107">version</span></span>
* <span data-ttu-id="dc2a8-108">parâmetros</span><span class="sxs-lookup"><span data-stu-id="dc2a8-108">parameters</span></span>

<span data-ttu-id="dc2a8-109">Para aplicativos gerenciados, o manipulador deve sempre ser `Microsoft.Compute.MultiVm`, e a versão mais recente com suporte de saudação é `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="dc2a8-110">esquema de saudação da propriedade de parâmetros de saudação depende da combinação de saudação do manipulador de saudação especificado e a versão.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="dc2a8-111">Para aplicativos gerenciados, propriedades de saudação com suporte são `basics`, `steps`, e `outputs`.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="dc2a8-112">Propriedades de Noções básicas e etapas Hello contêm Olá _elementos_ - como caixas de texto e listas suspensas - toobe exibido no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="dc2a8-113">Olá saídas propriedade é toomap usados valores de saída Olá Olá elementos especificados toohello parâmetros de modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="dc2a8-114">A inclusão de `$schema` é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="dc2a8-115">Se especificado, Olá valor `version` deve coincidir com a versão Olá Olá `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="dc2a8-116">Noções básicas</span><span class="sxs-lookup"><span data-stu-id="dc2a8-116">Basics</span></span>
<span data-ttu-id="dc2a8-117">etapa de Noções básicas de saudação sempre é Olá primeira etapa do Assistente de saudação gerado quando a saudação portal do Azure analisa um CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="dc2a8-118">Além de elementos de saudação toodisplaying especificado no `basics`, portal Olá injeta elementos para assinatura de saudação toochoose usuários, o grupo de recursos e o local para a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="dc2a8-119">Em geral, os elementos de consulta para parâmetros de toda a implantação, como nome de saudação de credenciais de um cluster ou o administrador, devem ficar nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="dc2a8-120">Se o comportamento de um elemento depende da assinatura do usuário hello, grupo de recursos ou local, esse elemento não pode ser usado em Noções básicas.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="dc2a8-121">Por exemplo, **Microsoft.Compute.SizeSelector** depende assinatura e localização toodetermine Olá lista do usuário Olá de tamanhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="dc2a8-122">Portanto, **Microsoft.Compute.SizeSelector** só pode ser usado em steps.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="dc2a8-123">Em geral, apenas elementos no hello **Microsoft.Common** namespace pode ser usado em Noções básicas.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="dc2a8-124">Embora alguns elementos de outros namespaces (como **Microsoft.Compute.Credentials**) que não dependem do contexto do usuário hello, ainda são permitidos.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="dc2a8-125">Etapas</span><span class="sxs-lookup"><span data-stu-id="dc2a8-125">Steps</span></span>
<span data-ttu-id="dc2a8-126">propriedade de etapas de saudação pode conter zero ou mais toodisplay de etapas adicionais após Noções básicas, cada qual contendo um ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="dc2a8-127">Considere adicionar etapas por função ou camada do aplicativo hello está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="dc2a8-128">Por exemplo, adicione uma etapa para entradas de nós mestres Olá e um para nós de trabalho Olá em um cluster.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="dc2a8-129">outputs</span><span class="sxs-lookup"><span data-stu-id="dc2a8-129">Outputs</span></span>
<span data-ttu-id="dc2a8-130">Olá, portal do Azure usa Olá `outputs` toomap elementos da propriedade de `basics` e `steps` toohello parâmetros de modelo de implantação do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="dc2a8-131">chaves deste dicionário Olá são nomes de Olá Olá dos parâmetros de modelo e valores de saudação são propriedades dos objetos de saída Olá dos elementos de saudação referenciado.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="dc2a8-132">Funções</span><span class="sxs-lookup"><span data-stu-id="dc2a8-132">Functions</span></span>
<span data-ttu-id="dc2a8-133">Semelhante muito[funções de modelo](resource-group-template-functions.md) no Azure Resource Manager (tanto na sintaxe e funcionalidade), CreateUiDefinition fornece funções para trabalhar com elementos entradas e saídas, bem como recursos como condicionais.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc2a8-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc2a8-134">Next steps</span></span>
<span data-ttu-id="dc2a8-135">O próprio CreateUiDefinition tem um esquema simples.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="dc2a8-136">profundidade de saudação real é proveniente de todos os elementos de saudação com suporte e funções, quais Olá documentos a seguir descrevem detalhadamente esplêndida:</span><span class="sxs-lookup"><span data-stu-id="dc2a8-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="dc2a8-137">Elementos</span><span class="sxs-lookup"><span data-stu-id="dc2a8-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="dc2a8-138">Funções</span><span class="sxs-lookup"><span data-stu-id="dc2a8-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="dc2a8-139">Um esquema JSON atual para CreateUiDefinition está disponível aqui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="dc2a8-140">Em versões posteriores estarão disponíveis em Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="dc2a8-141">Substituir saudação `0.1.2-preview` parte da URL hello e hello `version` valor com o identificador de versão Olá você pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="dc2a8-142">identificadores de versão Olá atualmente com suporte são `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="dc2a8-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
