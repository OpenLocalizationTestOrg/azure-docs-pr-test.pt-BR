---
title: "Definir a ordem de implantação dos recursos do Azure | Microsoft Docs"
description: "Descreve como definir um recurso como dependente de outro recurso durante a implantação para garantir que os recursos sejam implantados na ordem correta."
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
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="036b5-103">Definir a ordem de implantação dos recursos em modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="036b5-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="036b5-104">Para um determinado recurso, pode ser necessário que existam outros recursos antes que o recurso em questão seja implantado.</span><span class="sxs-lookup"><span data-stu-id="036b5-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="036b5-105">Por exemplo, um SQL Server deve existir antes que você tente implantar um Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="036b5-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="036b5-106">Você define essa relação marcando um recurso como dependente do outro.</span><span class="sxs-lookup"><span data-stu-id="036b5-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="036b5-107">Defina uma dependência com o elemento **dependsOn** ou usando a função **reference**.</span><span class="sxs-lookup"><span data-stu-id="036b5-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="036b5-108">O Gerenciador de Recursos avalia as dependências entre os recursos e os implanta na ordem de dependência.</span><span class="sxs-lookup"><span data-stu-id="036b5-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="036b5-109">Quando os recursos não dependem uns dos outros, o Gerenciador de Recursos os implanta paralelamente.</span><span class="sxs-lookup"><span data-stu-id="036b5-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="036b5-110">Você só precisa definir as dependências para recursos que são implantados no mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="036b5-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="036b5-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="036b5-111">dependsOn</span></span>
<span data-ttu-id="036b5-112">No seu modelo, o elemento dependsOn permite definir um recurso como um dependente em um ou mais recursos.</span><span class="sxs-lookup"><span data-stu-id="036b5-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="036b5-113">Seu valor pode ser uma lista de nomes de recurso separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="036b5-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="036b5-114">O exemplo a seguir mostra um conjunto de escala de máquina virtual que depende de um balanceador de carga, de uma rede virtual e de um loop que cria várias contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="036b5-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="036b5-115">Esses outros recursos não são mostrados no exemplo a seguir, mas precisariam existir em outro lugar no modelo.</span><span class="sxs-lookup"><span data-stu-id="036b5-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

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

<span data-ttu-id="036b5-116">No exemplo anterior, uma dependência foi incluída nos recursos criados por meio de um loop de cópia chamado **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="036b5-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="036b5-117">Por exemplo, consulte [Criar várias instâncias de recursos no Gerenciador de Recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="036b5-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="036b5-118">Ao definir dependências, você pode incluir o namespace do provedor de recurso e o tipo de recurso para evitar ambiguidade.</span><span class="sxs-lookup"><span data-stu-id="036b5-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="036b5-119">Por exemplo, para esclarecer um balanceador de carga e uma rede virtual que possam ter os mesmos nomes que outros recursos, use o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="036b5-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="036b5-120">Embora você talvez queira usar o dependsOn para mapear as relações entre os seus recursos, é importante entender por que você está fazendo isso.</span><span class="sxs-lookup"><span data-stu-id="036b5-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="036b5-121">Por exemplo, para documentar como os recursos são interconectados, o dependsOn não é a abordagem correta.</span><span class="sxs-lookup"><span data-stu-id="036b5-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="036b5-122">Você não pode consultar quais recursos foram definidos no elemento dependsOn após a implantação.</span><span class="sxs-lookup"><span data-stu-id="036b5-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="036b5-123">Ao usar o dependsOn, você potencialmente afeta o tempo de implantação, pois o Resource Manager não implanta paralelamente dois recursos que têm uma dependência.</span><span class="sxs-lookup"><span data-stu-id="036b5-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="036b5-124">Para documentar relações entre recursos, use a [vinculação de recursos](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="036b5-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="036b5-125">Recursos filho</span><span class="sxs-lookup"><span data-stu-id="036b5-125">Child resources</span></span>
<span data-ttu-id="036b5-126">A propriedade resources permite especificar os recursos filho relacionados ao recurso que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="036b5-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="036b5-127">Os recursos filho só podem ser definidos em cinco níveis de profundidade.</span><span class="sxs-lookup"><span data-stu-id="036b5-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="036b5-128">É importante observar que não é criada uma dependência implícita entre um recurso filho e o pai.</span><span class="sxs-lookup"><span data-stu-id="036b5-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="036b5-129">Se precisar que o recurso filho seja implantado após o recurso pai, você deve declarar explicitamente essa dependência com a propriedade dependsOn.</span><span class="sxs-lookup"><span data-stu-id="036b5-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="036b5-130">Cada recurso pai aceita somente determinados tipos de recurso como recursos filho.</span><span class="sxs-lookup"><span data-stu-id="036b5-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="036b5-131">Os tipos de recurso aceitos são especificados no [esquema do modelo](https://github.com/Azure/azure-resource-manager-schemas) do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="036b5-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="036b5-132">O nome do tipo de recurso de filho inclui o nome do tipo de recurso pai, assim como **Microsoft.Web/sites/config** e **Microsoft.Web/sites/extensions** são ambos recursos filho do **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="036b5-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="036b5-133">O exemplo a seguir mostra um SQL Server e um Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="036b5-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="036b5-134">Observe que uma dependência explícita é definida entre o Banco de Dados SQL e o SQL Server, ainda que o banco de dados seja um filho do servidor.</span><span class="sxs-lookup"><span data-stu-id="036b5-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="036b5-135">Função reference</span><span class="sxs-lookup"><span data-stu-id="036b5-135">reference function</span></span>
<span data-ttu-id="036b5-136">A [função de referência](resource-group-template-functions-resource.md#reference) permite que uma expressão derive seu valor de outro nome JSON e de pares de valor ou de recursos de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="036b5-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="036b5-137">Expressões de referência declaram de maneira implícita que um recurso depende de outro.</span><span class="sxs-lookup"><span data-stu-id="036b5-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="036b5-138">O formato geral é:</span><span class="sxs-lookup"><span data-stu-id="036b5-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="036b5-139">No exemplo a seguir, um ponto de extremidade CDN depende explicitamente do perfil CDN e implicitamente de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="036b5-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="036b5-140">Você pode usar esse elemento ou o elemento dependsOn para especificar dependências, mas não é necessário usar ambos para o mesmo recurso dependente.</span><span class="sxs-lookup"><span data-stu-id="036b5-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="036b5-141">Sempre que possível, use uma referência implícita para evitar adicionar uma dependência desnecessária.</span><span class="sxs-lookup"><span data-stu-id="036b5-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="036b5-142">Para saber mais, consulte [Função de referência](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="036b5-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="036b5-143">Recomendações para a configuração de dependências</span><span class="sxs-lookup"><span data-stu-id="036b5-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="036b5-144">Ao decidir quais são as dependências a serem definidas, use as seguintes diretrizes:</span><span class="sxs-lookup"><span data-stu-id="036b5-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="036b5-145">Defina o mínimo de dependências possível.</span><span class="sxs-lookup"><span data-stu-id="036b5-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="036b5-146">Defina um recurso filho como dependente do recurso pai.</span><span class="sxs-lookup"><span data-stu-id="036b5-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="036b5-147">Use a função **reference** para definir as dependências implícitas entre os recursos que precisam compartilhar uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="036b5-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="036b5-148">Não adicione uma dependência explícita (**dependsOn**) quando você já definiu uma dependência implícita.</span><span class="sxs-lookup"><span data-stu-id="036b5-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="036b5-149">Essa abordagem reduz o risco de ter dependências desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="036b5-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="036b5-150">Defina uma dependência quando um recurso não pode ser **criado** sem funcionalidades de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="036b5-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="036b5-151">Não defina uma dependência se os recursos interagem somente após a implantação.</span><span class="sxs-lookup"><span data-stu-id="036b5-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="036b5-152">Coloque as dependências em cascata sem defini-las explicitamente.</span><span class="sxs-lookup"><span data-stu-id="036b5-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="036b5-153">Por exemplo, sua máquina virtual depende de uma interface de rede virtual e a interface de rede virtual depende de uma rede virtual e de endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="036b5-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="036b5-154">Portanto, a máquina virtual é implantada depois de todos os três recursos, mas não está definida explicitamente como dependente de todos os três recursos.</span><span class="sxs-lookup"><span data-stu-id="036b5-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="036b5-155">Essa abordagem esclarece a ordem de dependência e facilita a alteração do modelo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="036b5-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="036b5-156">Se um valor pode ser determinado antes da implantação, tente implantar o recurso sem uma dependência.</span><span class="sxs-lookup"><span data-stu-id="036b5-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="036b5-157">Por exemplo, se um valor de configuração precisa do nome de outro recurso, talvez não seja necessário uma dependência.</span><span class="sxs-lookup"><span data-stu-id="036b5-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="036b5-158">Essa orientação nem sempre funciona porque alguns recursos verificam a existência de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="036b5-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="036b5-159">Se você receber um erro, adicione uma dependência.</span><span class="sxs-lookup"><span data-stu-id="036b5-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="036b5-160">O Resource Manager identifica dependências circulares durante a validação do modelo.</span><span class="sxs-lookup"><span data-stu-id="036b5-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="036b5-161">Se você receber um erro indicando que existe uma dependência circular, avalie o modelo para ver se existem dependências desnecessárias que podem ser removidas.</span><span class="sxs-lookup"><span data-stu-id="036b5-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="036b5-162">Se a remoção de dependências não funcionar, você pode evitar dependências circulares movendo algumas operações de implantação para recursos filhos que são implantados depois dos recursos que possuem a dependência circular.</span><span class="sxs-lookup"><span data-stu-id="036b5-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="036b5-163">Por exemplo, suponha que você estiver implantando duas máquinas virtuais, mas você deve definir propriedades em cada um deles que se referem a outro.</span><span class="sxs-lookup"><span data-stu-id="036b5-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="036b5-164">Você pode implantá-los na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="036b5-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="036b5-165">vm1</span><span class="sxs-lookup"><span data-stu-id="036b5-165">vm1</span></span>
2. <span data-ttu-id="036b5-166">vm2</span><span class="sxs-lookup"><span data-stu-id="036b5-166">vm2</span></span>
3. <span data-ttu-id="036b5-167">Extensão na vm1 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="036b5-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="036b5-168">A extensão define valores na vm1 que ele obtém da vm2.</span><span class="sxs-lookup"><span data-stu-id="036b5-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="036b5-169">Extensão da vm2 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="036b5-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="036b5-170">A extensão define valores de vm2 obtido do vm1.</span><span class="sxs-lookup"><span data-stu-id="036b5-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="036b5-171">Para obter informações sobre como avaliar a ordem de implantação e resolver erros de dependência, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="036b5-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="036b5-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="036b5-172">Next steps</span></span>
* <span data-ttu-id="036b5-173">Para saber mais sobre a solução de problemas de dependência durante a implantação, confira [Solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="036b5-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="036b5-174">Para saber mais sobre a criação de modelos do Gerenciador de Recursos do Azure, consulte [Criando modelos](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="036b5-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="036b5-175">Para obter uma lista das funções disponíveis em um modelo, consulte [Funções de modelo](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="036b5-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

