---
title: "ordem de implantação de aaaSet para recursos do Azure | Microsoft Docs"
description: "Descreve como um recurso tooset como depende de outro recurso durante tooensure os recursos de implantação são implantados na ordem correta hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="e5fbf-103">Defina a ordem de saudação para implantar recursos em modelos do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e5fbf-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="e5fbf-104">Para um determinado recurso, pode haver outros recursos que devem existir antes da implantação de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="e5fbf-105">Por exemplo, um SQL server deve existir antes de tentar toodeploy um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="e5fbf-106">Definir esta relação marcando um recurso como dependente Olá outro recurso.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="e5fbf-107">Definir uma dependência com hello **dependsOn** elemento, ou usando Olá **referência** função.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="e5fbf-108">Gerenciador de recursos avalia Olá dependências entre os recursos e implanta-os em sua ordem dependente.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="e5fbf-109">Quando os recursos não dependem uns dos outros, o Gerenciador de Recursos os implanta paralelamente.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="e5fbf-110">Você só precisa de toodefine dependências de recursos que são implantados em Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="e5fbf-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="e5fbf-111">dependsOn</span></span>
<span data-ttu-id="e5fbf-112">Dentro de seu modelo, Olá dependsOn elemento permite que você toodefine um recurso como um dependente em um ou mais recursos.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="e5fbf-113">Seu valor pode ser uma lista de nomes de recurso separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="e5fbf-114">Olá, exemplo a seguir mostra um conjunto de escala de máquina virtual depende de um balanceador de carga de rede virtual e um loop que cria várias contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="e5fbf-115">Esses outros recursos não são mostrados no exemplo a seguir de saudação, mas precisam tooexist em outro lugar no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="e5fbf-116">No hello anterior de exemplo, uma dependência está incluída nos recursos de saudação que são criados por meio de um loop de cópia chamado **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="e5fbf-117">Por exemplo, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="e5fbf-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="e5fbf-118">Ao definir dependências, você pode incluir Olá recurso provedor namespace e o recurso tipo tooavoid ambiguidade.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="e5fbf-119">Por exemplo, tooclarify de formato de um balanceador de carga e rede virtual que pode ter Olá que mesmos nomes, como outros recursos, use Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5fbf-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="e5fbf-120">Embora você possa estar toouse decidido dependsOn toomap relações entre os recursos, é importante toounderstand por que você está fazendo.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="e5fbf-121">Por exemplo, toodocument como os recursos são interconectados, dependsOn não é abordagem certa hello.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="e5fbf-122">Não é possível consultar os recursos que foram definidos no elemento de dependsOn Olá após a implantação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="e5fbf-123">Ao usar o dependsOn, você potencialmente afeta o tempo de implantação, pois o Resource Manager não implanta paralelamente dois recursos que têm uma dependência.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="e5fbf-124">toodocument relações entre os recursos, em vez disso, use [vinculação de recursos](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="e5fbf-125">Recursos filho</span><span class="sxs-lookup"><span data-stu-id="e5fbf-125">Child resources</span></span>
<span data-ttu-id="e5fbf-126">propriedade de recursos Olá permite recursos filho toospecify que sejam toohello relacionados do recurso que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="e5fbf-127">Os recursos filho só podem ser definidos em cinco níveis de profundidade.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="e5fbf-128">É importante toonote uma dependência implícita não é criada entre um recurso filho e o recurso pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="e5fbf-129">Se precisar hello filho recurso toobe implantado após o recurso pai de hello, deve declarar explicitamente essa dependência com a propriedade de dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="e5fbf-130">Cada recurso pai aceita somente determinados tipos de recurso como recursos filho.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="e5fbf-131">Olá aceita tipos de recurso são especificados em Olá [esquema de modelo](https://github.com/Azure/azure-resource-manager-schemas) do recurso pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="e5fbf-132">nome de saudação filho do tipo de recurso inclui o nome de saudação do tipo de recurso pai hello, como **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** são ambos os recursos filho de saudação  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="e5fbf-133">saudação de exemplo a seguir mostra um SQL server e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="e5fbf-134">Observe que uma dependência explícita é definida entre o banco de dados do hello SQL e SQL server, mesmo que o banco de dados de saudação é um filho do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="e5fbf-135">Função reference</span><span class="sxs-lookup"><span data-stu-id="e5fbf-135">reference function</span></span>
<span data-ttu-id="e5fbf-136">Olá [fazem referência a função](resource-group-template-functions-resource.md#reference) permite que uma expressão tooderive seu valor de outros pares de nome e valor JSON ou recursos de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="e5fbf-137">Expressões de referência declaram de maneira implícita que um recurso depende de outro.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="e5fbf-138">formato de saudação geral é:</span><span class="sxs-lookup"><span data-stu-id="e5fbf-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="e5fbf-139">Em Olá exemplo a seguir, um ponto de extremidade CDN depende explicitamente Olá perfil CDN e implicitamente depende de um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="e5fbf-140">Você pode usar este elemento ou Olá dependsOn elemento toospecify as dependências, mas você não precisa toouse ambos para Olá mesmo recurso dependente.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="e5fbf-141">Sempre que possível, use um tooavoid referência implícita adicionando uma dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="e5fbf-142">mais, consulte toolearn [fazem referência a função](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="e5fbf-143">Recomendações para a configuração de dependências</span><span class="sxs-lookup"><span data-stu-id="e5fbf-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="e5fbf-144">Ao decidir qual tooset dependências, use Olá diretrizes a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5fbf-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="e5fbf-145">Defina o mínimo de dependências possível.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="e5fbf-146">Defina um recurso filho como dependente do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="e5fbf-147">Saudação de uso **referência** tooset dependências de implícita entre os recursos que precisam de tooshare uma propriedade de função.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="e5fbf-148">Não adicione uma dependência explícita (**dependsOn**) quando você já definiu uma dependência implícita.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="e5fbf-149">Essa abordagem reduz o risco de saudação de ter dependências desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="e5fbf-150">Defina uma dependência quando um recurso não pode ser **criado** sem funcionalidades de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="e5fbf-151">Não defina uma dependência se recursos Olá interagem somente após a implantação.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="e5fbf-152">Coloque as dependências em cascata sem defini-las explicitamente.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="e5fbf-153">Por exemplo, sua máquina virtual depende de uma interface de rede virtual e interface de rede virtual Olá depende de uma rede virtual e endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="e5fbf-154">Portanto, máquina virtual de saudação é implantados depois que todos os três recursos, mas não defina explicitamente Olá VM como dependentes em todos os três recursos.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="e5fbf-155">Essa abordagem esclarece a ordem de dependência hello e torna mais fácil do modelo de saudação toochange mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="e5fbf-156">Se um valor pode ser determinado antes da implantação, tente implantar recursos de saudação sem uma dependência.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="e5fbf-157">Por exemplo, se um valor de configuração precisa de nome de saudação de outro recurso, talvez não seja necessário uma dependência.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="e5fbf-158">Este guia não funciona sempre porque alguns recursos Verifique a existência de saudação do hello outro recurso.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="e5fbf-159">Se você receber um erro, adicione uma dependência.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="e5fbf-160">O Resource Manager identifica dependências circulares durante a validação do modelo.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="e5fbf-161">Se você receber um erro indicando que existe uma dependência circular, avalie sua toosee de modelo se qualquer dependência não é necessários e pode ser removida.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="e5fbf-162">Se remover dependências não funcionar, você pode evitar dependências circulares ao mover algumas operações de implantação em recursos filho que são implantados após recursos Olá com dependência circular hello.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="e5fbf-163">Por exemplo, suponha que você está implantando duas máquinas virtuais, mas você deve definir propriedades em cada um deles que se referem a outros toohello.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="e5fbf-164">Você pode implantá-los em Olá ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5fbf-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="e5fbf-165">vm1</span><span class="sxs-lookup"><span data-stu-id="e5fbf-165">vm1</span></span>
2. <span data-ttu-id="e5fbf-166">vm2</span><span class="sxs-lookup"><span data-stu-id="e5fbf-166">vm2</span></span>
3. <span data-ttu-id="e5fbf-167">Extensão na vm1 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="e5fbf-168">extensão de saudação define valores na vm1 obtém da vm2.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="e5fbf-169">Extensão da vm2 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="e5fbf-170">extensão de saudação define valores vm2 obtém da vm1.</span><span class="sxs-lookup"><span data-stu-id="e5fbf-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="e5fbf-171">Para obter informações sobre como avaliar uma ordem de implantação hello e resolver erros de dependência, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fbf-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5fbf-172">Next steps</span></span>
* <span data-ttu-id="e5fbf-173">toolearn sobre dependências de solução de problemas durante a implantação, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e5fbf-174">toolearn sobre como criar modelos do Azure Resource Manager, consulte [criar modelos](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="e5fbf-175">Para obter uma lista das funções disponíveis do hello em um modelo, consulte [funções de modelo](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="e5fbf-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

