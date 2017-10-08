---
title: "práticas recomendadas de aaaBest para criar modelos do Gerenciador de recursos | Microsoft Docs"
description: Diretrizes para simplificar seus modelos do Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="7baa2-103">Práticas recomendadas para criação de modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7baa2-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="7baa2-104">Essas diretrizes podem ajudar você a criar modelos do Azure Resource Manager toouse fácil e confiável.</span><span class="sxs-lookup"><span data-stu-id="7baa2-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="7baa2-105">diretrizes de saudação são apenas sugestões.</span><span class="sxs-lookup"><span data-stu-id="7baa2-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="7baa2-106">Elas não são requisitos, exceto onde apontadas.</span><span class="sxs-lookup"><span data-stu-id="7baa2-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="7baa2-107">O cenário pode exigir uma variação de uma saudação abordagens ou exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7baa2-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="7baa2-108">Nomes de recurso</span><span class="sxs-lookup"><span data-stu-id="7baa2-108">Resource names</span></span>
<span data-ttu-id="7baa2-109">Normalmente, você trabalha com três tipos de nome de recurso no Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="7baa2-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="7baa2-110">Os nomes de recurso devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="7baa2-111">Nomes de recursos que não são necessárias toobe exclusivo, mas escolha tooprovide um nome que pode ajudá-lo a identificar um recurso com base no contexto.</span><span class="sxs-lookup"><span data-stu-id="7baa2-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="7baa2-112">Nomes de recursos que podem ser genéricos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="7baa2-113">Para obter informações sobre restrições de nome de recurso, confira [Recursos recomendados de convenções de nomenclatura do Azure](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="7baa2-114">Nomes de recurso exclusivos</span><span class="sxs-lookup"><span data-stu-id="7baa2-114">Unique resource names</span></span>
<span data-ttu-id="7baa2-115">Você deve fornecer um nome de recurso exclusivo para qualquer tipo de recurso que tenha um ponto de extremidade de acesso de dados.</span><span class="sxs-lookup"><span data-stu-id="7baa2-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="7baa2-116">Entre os tipos comuns de recurso que exigem um nome exclusivo estão:</span><span class="sxs-lookup"><span data-stu-id="7baa2-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="7baa2-117">Armazenamento do Azure<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7baa2-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="7baa2-118">Recurso de Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="7baa2-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7baa2-119">SQL Server</span></span>
* <span data-ttu-id="7baa2-120">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-120">Azure Key Vault</span></span>
* <span data-ttu-id="7baa2-121">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-121">Azure Redis Cache</span></span>
* <span data-ttu-id="7baa2-122">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-122">Azure Batch</span></span>
* <span data-ttu-id="7baa2-123">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="7baa2-124">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-124">Azure Search</span></span>
* <span data-ttu-id="7baa2-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7baa2-125">Azure HDInsight</span></span>

<span data-ttu-id="7baa2-126"><sup>1</sup> Os nomes de conta de armazenamento devem estar em letras minúsculas, ter até 24 caracteres e não incluir hifens.</span><span class="sxs-lookup"><span data-stu-id="7baa2-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="7baa2-127">Se você fornecer um parâmetro de nome de um recurso, você deve fornecer um nome exclusivo quando você implanta o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="7baa2-128">Opcionalmente, você pode criar uma variável que usa Olá [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate um nome de função.</span><span class="sxs-lookup"><span data-stu-id="7baa2-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="7baa2-129">Você também pode ser desejável tooadd um prefixo ou sufixo toohello **uniqueString** resultados.</span><span class="sxs-lookup"><span data-stu-id="7baa2-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="7baa2-130">Modificando nome exclusivo de saudação pode ajudá-lo mais facilmente identificar o tipo de recurso de saudação do nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="7baa2-131">Por exemplo, você pode gerar um nome exclusivo para uma conta de armazenamento usando Olá variável a seguir:</span><span class="sxs-lookup"><span data-stu-id="7baa2-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="7baa2-132">Nomes de recurso para identificação</span><span class="sxs-lookup"><span data-stu-id="7baa2-132">Resource names for identification</span></span>
<span data-ttu-id="7baa2-133">Alguns tipos de recursos que talvez você queira tooname, mas seus nomes não tem toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="7baa2-134">Para esses tipos de recurso, você pode fornecer um nome que identifica o contexto do recurso hello e o tipo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="7baa2-135">Forneça um nome descritivo que ajudará você a identificar o recurso de saudação em uma lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="7baa2-136">Se você precisar toouse um nome de recurso diferente para diferentes implantações, você pode usar um parâmetro para o nome da saudação:</span><span class="sxs-lookup"><span data-stu-id="7baa2-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="7baa2-137">Se você não precisar toopass em um nome durante a implantação, você pode usar uma variável:</span><span class="sxs-lookup"><span data-stu-id="7baa2-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="7baa2-138">Também é possível usar um valor embutido em código:</span><span class="sxs-lookup"><span data-stu-id="7baa2-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="7baa2-139">Nomes de recurso genéricos</span><span class="sxs-lookup"><span data-stu-id="7baa2-139">Generic resource names</span></span>
<span data-ttu-id="7baa2-140">Tipos de recursos que você acessa principalmente por meio de um recurso diferente, você pode usar um nome genérico que é embutido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="7baa2-141">Por exemplo, você pode definir um nome genérico padrão para regras de firewall em um servidor SQL:</span><span class="sxs-lookup"><span data-stu-id="7baa2-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="7baa2-142">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7baa2-142">Parameters</span></span>
<span data-ttu-id="7baa2-143">Olá informações a seguir podem ser útil ao trabalhar com parâmetros:</span><span class="sxs-lookup"><span data-stu-id="7baa2-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="7baa2-144">Minimize o uso de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7baa2-144">Minimize your use of parameters.</span></span> <span data-ttu-id="7baa2-145">Sempre que possível, use uma variável ou um valor literal.</span><span class="sxs-lookup"><span data-stu-id="7baa2-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="7baa2-146">Use parâmetros somente para estes cenários:</span><span class="sxs-lookup"><span data-stu-id="7baa2-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="7baa2-147">Configurações que você deseja toouse variações de acordo com tooenvironment (SKU, tamanho, capacidade).</span><span class="sxs-lookup"><span data-stu-id="7baa2-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="7baa2-148">Nomes de recurso que você deseja toospecify para facilitar sua identificação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="7baa2-149">Valores que você utiliza com frequência toocomplete outras tarefas (como um nome de usuário de administrador).</span><span class="sxs-lookup"><span data-stu-id="7baa2-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="7baa2-150">Segredos (como senhas).</span><span class="sxs-lookup"><span data-stu-id="7baa2-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="7baa2-151">número de saudação ou matriz de valores toouse quando você criar várias instâncias de um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="7baa2-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="7baa2-152">Use minúsculas concatenadas para nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7baa2-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="7baa2-153">Forneça uma descrição de cada parâmetro na Olá metadados:</span><span class="sxs-lookup"><span data-stu-id="7baa2-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="7baa2-154">Defina valores padrão para parâmetros (exceto senhas e chaves SSH):</span><span class="sxs-lookup"><span data-stu-id="7baa2-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="7baa2-155">Use **SecureString** para todos os segredos e senhas:</span><span class="sxs-lookup"><span data-stu-id="7baa2-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="7baa2-156">Sempre que possível, não use um local de toospecify do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7baa2-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="7baa2-157">Em vez disso, use Olá **local** propriedade saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="7baa2-158">Usando Olá **resourceGroup () .location** expressão de todos os seus recursos, os recursos no modelo de saudação são implantados em Olá mesmo local que o grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="7baa2-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="7baa2-159">Se um tipo de recurso é suportado em apenas um número limitado de locais, você poderá toospecify um local válido diretamente no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="7baa2-160">Se você deve usar um **local** parâmetro, compartilhar esse valor de parâmetro tanto quanto possível com recursos que são provavelmente toobe em Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="7baa2-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="7baa2-161">Isso minimiza o número de saudação de vezes que os usuários são solicitados tooprovide informações de localização.</span><span class="sxs-lookup"><span data-stu-id="7baa2-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="7baa2-162">Evite usar um parâmetro ou variável para a versão da API Olá para um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="7baa2-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="7baa2-163">Os valores e propriedades do recurso podem variar de acordo com o número de versão.</span><span class="sxs-lookup"><span data-stu-id="7baa2-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="7baa2-164">IntelliSense em um editor de código não é possível determinar o esquema correto hello quando a versão da API Olá é definida tooa parâmetro ou variável.</span><span class="sxs-lookup"><span data-stu-id="7baa2-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="7baa2-165">Em vez disso, codificar Olá versão de API no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="7baa2-166">variáveis</span><span class="sxs-lookup"><span data-stu-id="7baa2-166">Variables</span></span>
<span data-ttu-id="7baa2-167">Olá informações a seguir podem ser útil ao trabalhar com variáveis:</span><span class="sxs-lookup"><span data-stu-id="7baa2-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="7baa2-168">Use variáveis para valores que você precisa toouse mais de uma vez em um modelo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="7baa2-169">Se um valor é usado apenas uma vez, um valor embutido faz seu tooread mais fácil de modelo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="7baa2-170">Você não pode usar o hello [referência](resource-group-template-functions-resource.md#reference) função hello **variáveis** seção Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="7baa2-171">Olá **referência** função deriva seu valor de estado de tempo de execução do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="7baa2-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="7baa2-172">No entanto, variáveis são resolvidas durante a saudação inicial de análise do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="7baa2-173">Construir valores que precisam de saudação **referência** função diretamente no hello **recursos** ou **gera** seção Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="7baa2-174">Inclua variáveis em nomes de recurso que devem ser exclusivos, conforme descrito em [Nomes de recurso](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="7baa2-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="7baa2-175">Você pode agrupar variáveis em objetos complexos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-175">You can group variables into complex objects.</span></span> <span data-ttu-id="7baa2-176">Saudação de uso **variable.subentry** tooreference um valor de um objeto complexo de formato.</span><span class="sxs-lookup"><span data-stu-id="7baa2-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="7baa2-177">O agrupamento de variáveis pode ajudar a rastrear variáveis relacionadas.</span><span class="sxs-lookup"><span data-stu-id="7baa2-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="7baa2-178">Isso também melhora a legibilidade do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-178">It also improves readability of hello template.</span></span> <span data-ttu-id="7baa2-179">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="7baa2-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7baa2-180">Um objeto complexo não pode conter uma expressão que faça referência a um valor de um objeto complexo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="7baa2-181">Defina uma variável separada para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="7baa2-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="7baa2-182">Para obter exemplos avançados de como usar objetos complexos como variáveis, confira [Compartilhar estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="7baa2-183">Recursos</span><span class="sxs-lookup"><span data-stu-id="7baa2-183">Resources</span></span>
<span data-ttu-id="7baa2-184">Olá informações a seguir podem ser útil ao trabalhar com recursos:</span><span class="sxs-lookup"><span data-stu-id="7baa2-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="7baa2-185">toohelp outros colaboradores entender a finalidade de saudação do recurso de saudação, especifique **comentários** para cada recurso no modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="7baa2-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="7baa2-186">Você pode usar marcas tooadd metadados tooresources.</span><span class="sxs-lookup"><span data-stu-id="7baa2-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="7baa2-187">Use metadados tooadd informações sobre os recursos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="7baa2-188">Por exemplo, você pode adicionar detalhes de cobrança toorecord metadados para um recurso.</span><span class="sxs-lookup"><span data-stu-id="7baa2-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="7baa2-189">Para obter mais informações, consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="7baa2-190">Se você usar um *ponto de extremidade público* no modelo (como um Blob do Azure storage ponto de extremidade público), *faça não embutir* Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="7baa2-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="7baa2-191">Saudação de uso **referência** função toodynamically recuperar Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="7baa2-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="7baa2-192">Você pode usar ambientes com namespace pública essa abordagem toodeploy Olá modelo toodifferent sem alterar manualmente o ponto de extremidade Olá no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="7baa2-193">Definir Olá API versão toohello mesma versão que você está usando para a conta de armazenamento Olá no modelo:</span><span class="sxs-lookup"><span data-stu-id="7baa2-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="7baa2-194">Se conta de armazenamento Olá for implantada em Olá mesmo modelo que você está criando, você não precisa namespace do provedor Olá toospecify ao fazer referência a recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="7baa2-195">Esta é a sintaxe de saudação simplificada:</span><span class="sxs-lookup"><span data-stu-id="7baa2-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="7baa2-196">Se você tiver outros valores em seu modelo que são configurado toouse um espaço para nome público, alterar esses valores tooreflect Olá mesmo **referência** função.</span><span class="sxs-lookup"><span data-stu-id="7baa2-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="7baa2-197">Por exemplo, você pode definir Olá **storageUri** propriedade do perfil de diagnóstico de máquina virtual hello:</span><span class="sxs-lookup"><span data-stu-id="7baa2-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="7baa2-198">Você também pode fazer referência a uma conta de armazenamento existente que esteja em um grupo de recursos diferente:</span><span class="sxs-lookup"><span data-stu-id="7baa2-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="7baa2-199">Atribua pública tooa de endereços IP máquina virtual somente quando um aplicativo exija isso.</span><span class="sxs-lookup"><span data-stu-id="7baa2-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="7baa2-200">tooconnect tooa máquina virtual (VM) para a depuração, ou para fins administrativos, ou gerenciamento usar regras de NAT de entrada, um gateway de rede virtual ou um jumpbox.</span><span class="sxs-lookup"><span data-stu-id="7baa2-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="7baa2-201">Para obter mais informações sobre como se conectar a máquinas de toovirtual, consulte:</span><span class="sxs-lookup"><span data-stu-id="7baa2-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="7baa2-202">Executar VMs para uma arquitetura de N camadas no Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="7baa2-203">Configurar acesso WinRM para VMs no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7baa2-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="7baa2-204">Permitir o acesso externo tooyour VM usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="7baa2-205">Permitir o acesso externo tooyour VM usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7baa2-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="7baa2-206">Permitir o acesso externo tooyour VM do Linux usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7baa2-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="7baa2-207">Olá **domainNameLabel** propriedade para endereços IP públicos deve ser exclusiva.</span><span class="sxs-lookup"><span data-stu-id="7baa2-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="7baa2-208">Olá **domainNameLabel** valor deve ter entre 3 e 63 caracteres e seguem as regras de saudação especificadas por essa expressão regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="7baa2-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="7baa2-209">Porque Olá **uniqueString** função gera uma cadeia de caracteres que é 13 caracteres hello **dnsPrefixString** parâmetro é limitado too50 caracteres:</span><span class="sxs-lookup"><span data-stu-id="7baa2-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="7baa2-210">Quando você adiciona uma extensão de script personalizado tooa senha, use Olá **commandToExecute** propriedade Olá **protectedSettings** propriedade:</span><span class="sxs-lookup"><span data-stu-id="7baa2-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="7baa2-211">tooensure os segredos são criptografados quando eles são passados como parâmetros tooVMs e extensões, use Olá **protectedSettings** propriedade das extensões de saudação relevantes.</span><span class="sxs-lookup"><span data-stu-id="7baa2-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="7baa2-212">outputs</span><span class="sxs-lookup"><span data-stu-id="7baa2-212">Outputs</span></span>
<span data-ttu-id="7baa2-213">Se você usar um modelo toocreate os endereços IP públicos, inclua um **gera** seção que retorna detalhes do endereço IP de saudação e nome de domínio totalmente qualificado da saudação (FQDN).</span><span class="sxs-lookup"><span data-stu-id="7baa2-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="7baa2-214">Você pode usar a saída valores tooeasily recuperar detalhes sobre os FQDNs e endereços IP públicos após a implantação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="7baa2-215">Ao fazer referência a recursos hello, use a versão de hello API que você usou toocreate-lo:</span><span class="sxs-lookup"><span data-stu-id="7baa2-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="7baa2-216">Modelo único vs. modelos aninhados</span><span class="sxs-lookup"><span data-stu-id="7baa2-216">Single template vs. nested templates</span></span>
<span data-ttu-id="7baa2-217">toodeploy sua solução, você pode usar um único modelo ou um modelo principal com vários modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7baa2-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="7baa2-218">Os modelos aninhados são comuns em cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="7baa2-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="7baa2-219">Usando um oferece modelo aninhado você Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="7baa2-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="7baa2-220">Você pode dividir uma solução em componentes direcionados.</span><span class="sxs-lookup"><span data-stu-id="7baa2-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="7baa2-221">Você pode reutilizar modelos aninhados com diferentes modelos principais.</span><span class="sxs-lookup"><span data-stu-id="7baa2-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="7baa2-222">Se você escolher modelos toouse aninhado, Olá diretrizes a seguir pode ajudá-lo a padronizar o design do modelo.</span><span class="sxs-lookup"><span data-stu-id="7baa2-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="7baa2-223">Essas diretrizes se baseiam nos [padrões de design para modelos do Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="7baa2-224">Recomendamos um design que tem Olá modelos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7baa2-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="7baa2-225">**Modelo principal** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7baa2-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="7baa2-226">Uso de parâmetros de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="7baa2-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="7baa2-227">**Modelo de recursos compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-227">**Shared resources template**.</span></span> <span data-ttu-id="7baa2-228">Use toodeploy os recursos que usam todos os outros recursos compartilhados (por exemplo, virtual de rede e disponibilidade conjuntos).</span><span class="sxs-lookup"><span data-stu-id="7baa2-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="7baa2-229">Saudação de uso **dependsOn** tooensure de expressão que esse modelo é implantado antes de outros modelos.</span><span class="sxs-lookup"><span data-stu-id="7baa2-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="7baa2-230">**Modelo de recursos opcionais**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-230">**Optional resources template**.</span></span> <span data-ttu-id="7baa2-231">Use tooconditionally implantar recursos com base em um parâmetro (por exemplo, um jumpbox).</span><span class="sxs-lookup"><span data-stu-id="7baa2-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="7baa2-232">**Modelo de recursos de membro**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-232">**Member resources template**.</span></span> <span data-ttu-id="7baa2-233">Cada tipo de instância dentro de uma camada de aplicativo tem sua própria configuração.</span><span class="sxs-lookup"><span data-stu-id="7baa2-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="7baa2-234">Dentro de uma camada, você pode definir tipos diferentes de instância.</span><span class="sxs-lookup"><span data-stu-id="7baa2-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="7baa2-235">(Por exemplo, Olá instância primeiro cria um cluster, e instâncias adicionais são adicionadas cluster existente toohello.) Cada tipo de instância tem seu próprio modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="7baa2-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-236">**Scripts**.</span></span> <span data-ttu-id="7baa2-237">Scripts amplamente reutilizáveis são aplicáveis a cada tipo de instância (por exemplo, inicializar e formatar discos adicionais).</span><span class="sxs-lookup"><span data-stu-id="7baa2-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="7baa2-238">Os scripts personalizados que você cria para uma finalidade específica de personalização forem diferentes, com base no tipo de instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Modelo aninhado](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="7baa2-240">Para saber mais, confira [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="7baa2-241">Vincular condicionalmente toonested modelos</span><span class="sxs-lookup"><span data-stu-id="7baa2-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="7baa2-242">Você pode usar modelos de toonested de parâmetro tooconditionally link.</span><span class="sxs-lookup"><span data-stu-id="7baa2-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="7baa2-243">parâmetro Hello se torna parte da saudação URI para o modelo de saudação:</span><span class="sxs-lookup"><span data-stu-id="7baa2-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="7baa2-244">Formato de modelo</span><span class="sxs-lookup"><span data-stu-id="7baa2-244">Template format</span></span>
<span data-ttu-id="7baa2-245">É uma boa prática toopass seu modelo por meio de um validador JSON.</span><span class="sxs-lookup"><span data-stu-id="7baa2-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="7baa2-246">Um validador pode ajudar a remover vírgulas, parênteses e colchetes irrelevantes que podem gerar um erro durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="7baa2-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="7baa2-247">Experimente o [JSONLint](http://jsonlint.com/) ou um pacote linter para seu ambiente de edição favorito (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="7baa2-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="7baa2-248">Também é uma boa ideia tooformat o JSON para melhor legibilidade.</span><span class="sxs-lookup"><span data-stu-id="7baa2-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="7baa2-249">Você pode usar um pacote de formatador JSON para seu editor local.</span><span class="sxs-lookup"><span data-stu-id="7baa2-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="7baa2-250">No Visual Studio, o documento de saudação tooformat, pressione **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="7baa2-251">No Visual Studio Code, pressione **Alt + Shift + F**.</span><span class="sxs-lookup"><span data-stu-id="7baa2-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="7baa2-252">Se seu editor de local não Formatar documento hello, você pode usar um [formatador online](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="7baa2-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7baa2-253">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7baa2-253">Next steps</span></span>
* <span data-ttu-id="7baa2-254">Para obter diretrizes sobre a arquitetura de sua solução para máquinas virtuais, confira [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Executar uma VM Windows no Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Executar uma VM Linux no Azure).</span><span class="sxs-lookup"><span data-stu-id="7baa2-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="7baa2-255">Para obter orientação sobre como configurar uma conta de armazenamento, confira [Lista de verificação de desempenho e escalabilidade do armazenamento do Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="7baa2-256">toolearn sobre como uma empresa pode usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold Azure enterprise: controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7baa2-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

