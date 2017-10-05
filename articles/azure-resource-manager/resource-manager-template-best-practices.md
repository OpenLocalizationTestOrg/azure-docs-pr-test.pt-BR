---
title: "Práticas recomendadas para criação de modelos do Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="d8276-103">Práticas recomendadas para criação de modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8276-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="d8276-104">Estas diretrizes podem ajudar a criar modelos do Azure Resource Manager que sejam confiáveis e fáceis de usar.</span><span class="sxs-lookup"><span data-stu-id="d8276-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="d8276-105">As diretrizes são apenas sugestões.</span><span class="sxs-lookup"><span data-stu-id="d8276-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="d8276-106">Elas não são requisitos, exceto onde apontadas.</span><span class="sxs-lookup"><span data-stu-id="d8276-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="d8276-107">Seu cenário pode exigir uma variação de uma das abordagens ou dos exemplos que se seguem.</span><span class="sxs-lookup"><span data-stu-id="d8276-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="d8276-108">Nomes de recurso</span><span class="sxs-lookup"><span data-stu-id="d8276-108">Resource names</span></span>
<span data-ttu-id="d8276-109">Normalmente, você trabalha com três tipos de nome de recurso no Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="d8276-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="d8276-110">Os nomes de recurso devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d8276-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="d8276-111">Nomes de recurso que não precisam ser exclusivos, mas você opta por fornecer um nome que possa ajudar a identificar um recurso com base no contexto.</span><span class="sxs-lookup"><span data-stu-id="d8276-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="d8276-112">Nomes de recursos que podem ser genéricos.</span><span class="sxs-lookup"><span data-stu-id="d8276-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="d8276-113">Para obter informações sobre restrições de nome de recurso, confira [Recursos recomendados de convenções de nomenclatura do Azure](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="d8276-114">Nomes de recurso exclusivos</span><span class="sxs-lookup"><span data-stu-id="d8276-114">Unique resource names</span></span>
<span data-ttu-id="d8276-115">Você deve fornecer um nome de recurso exclusivo para qualquer tipo de recurso que tenha um ponto de extremidade de acesso de dados.</span><span class="sxs-lookup"><span data-stu-id="d8276-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="d8276-116">Entre os tipos comuns de recurso que exigem um nome exclusivo estão:</span><span class="sxs-lookup"><span data-stu-id="d8276-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="d8276-117">Armazenamento do Azure<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d8276-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="d8276-118">Recurso de Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="d8276-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d8276-119">SQL Server</span></span>
* <span data-ttu-id="d8276-120">Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-120">Azure Key Vault</span></span>
* <span data-ttu-id="d8276-121">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-121">Azure Redis Cache</span></span>
* <span data-ttu-id="d8276-122">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-122">Azure Batch</span></span>
* <span data-ttu-id="d8276-123">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="d8276-124">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-124">Azure Search</span></span>
* <span data-ttu-id="d8276-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8276-125">Azure HDInsight</span></span>

<span data-ttu-id="d8276-126"><sup>1</sup> Os nomes de conta de armazenamento devem estar em letras minúsculas, ter até 24 caracteres e não incluir hifens.</span><span class="sxs-lookup"><span data-stu-id="d8276-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="d8276-127">Se você fornecer um parâmetro para um nome de recurso, será preciso fornecer um nome exclusivo na implantação do recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="d8276-128">Como opção, você pode criar uma variável que use a função [uniqueString()](resource-group-template-functions-string.md#uniquestring) para gerar um nome.</span><span class="sxs-lookup"><span data-stu-id="d8276-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="d8276-129">Também convém adicionar um prefixo ou sufixo ao resultado **uniqueString**.</span><span class="sxs-lookup"><span data-stu-id="d8276-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="d8276-130">Modificar o nome exclusivo pode ajudar você a identificar mais facilmente o tipo de recurso pelo nome.</span><span class="sxs-lookup"><span data-stu-id="d8276-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="d8276-131">Por exemplo, você pode gerar um nome exclusivo para uma conta de armazenamento usando a seguinte variável:</span><span class="sxs-lookup"><span data-stu-id="d8276-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="d8276-132">Nomes de recurso para identificação</span><span class="sxs-lookup"><span data-stu-id="d8276-132">Resource names for identification</span></span>
<span data-ttu-id="d8276-133">Alguns tipos de recurso que talvez você queira nomear não precisam que seus nomes sejam exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d8276-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="d8276-134">Para esses tipos de recurso, você pode fornecer um nome que identifique o contexto do recurso e o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="d8276-135">Forneça um nome descritivo que ajude a identificar o recurso em uma lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8276-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="d8276-136">Se precisar usar um nome de recurso diferente para diferentes implantações, é possível usar um parâmetro para o nome:</span><span class="sxs-lookup"><span data-stu-id="d8276-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="d8276-137">Se não for necessário passar um nome durante a implantação, você poderá usar uma variável:</span><span class="sxs-lookup"><span data-stu-id="d8276-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="d8276-138">Também é possível usar um valor embutido em código:</span><span class="sxs-lookup"><span data-stu-id="d8276-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="d8276-139">Nomes de recurso genéricos</span><span class="sxs-lookup"><span data-stu-id="d8276-139">Generic resource names</span></span>
<span data-ttu-id="d8276-140">Para os tipos de recurso que você mais acessa por meio de um recurso diferente, é possível usar um nome genérico que seja embutido em código no modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="d8276-141">Por exemplo, você pode definir um nome genérico padrão para regras de firewall em um servidor SQL:</span><span class="sxs-lookup"><span data-stu-id="d8276-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="d8276-142">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d8276-142">Parameters</span></span>
<span data-ttu-id="d8276-143">As seguintes informações podem ser úteis quando você trabalha com parâmetros:</span><span class="sxs-lookup"><span data-stu-id="d8276-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="d8276-144">Minimize o uso de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d8276-144">Minimize your use of parameters.</span></span> <span data-ttu-id="d8276-145">Sempre que possível, use uma variável ou um valor literal.</span><span class="sxs-lookup"><span data-stu-id="d8276-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="d8276-146">Use parâmetros somente para estes cenários:</span><span class="sxs-lookup"><span data-stu-id="d8276-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="d8276-147">Configurações em que queira usar variações de acordo com o ambiente (SKU, tamanho e capacidade).</span><span class="sxs-lookup"><span data-stu-id="d8276-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="d8276-148">Nomes de recurso que queira especificar para fácil identificação.</span><span class="sxs-lookup"><span data-stu-id="d8276-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="d8276-149">Valores que usa com frequência para concluir outras tarefas (como um nome de usuário de administrador).</span><span class="sxs-lookup"><span data-stu-id="d8276-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="d8276-150">Segredos (como senhas).</span><span class="sxs-lookup"><span data-stu-id="d8276-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="d8276-151">O número ou a matriz de valores a ser usado durante a criação de várias instâncias de um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="d8276-152">Use minúsculas concatenadas para nomes de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d8276-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="d8276-153">Forneça uma descrição de cada parâmetro nos metadados:</span><span class="sxs-lookup"><span data-stu-id="d8276-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="d8276-154">Defina valores padrão para parâmetros (exceto senhas e chaves SSH):</span><span class="sxs-lookup"><span data-stu-id="d8276-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="d8276-155">Use **SecureString** para todos os segredos e senhas:</span><span class="sxs-lookup"><span data-stu-id="d8276-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="d8276-156">Sempre que possível, não use um parâmetro para especificar o local.</span><span class="sxs-lookup"><span data-stu-id="d8276-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="d8276-157">Em vez disso, use a propriedade **location** do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d8276-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="d8276-158">Ao usar a expressão **resourceGroup().location** para todos os seus recursos, os recursos no modelo são implantados no mesmo local do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="d8276-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
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
   
   <span data-ttu-id="d8276-159">Se um tipo de recurso tiver suporte em apenas um número limitado de locais, talvez seja conveniente especificar um local válido diretamente no modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="d8276-160">Se você precisar usar um parâmetro **location**, compartilhe esse valor de parâmetro o máximo possível com os recursos que provavelmente estarão no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="d8276-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="d8276-161">Isso minimiza o número de vezes que os usuários são solicitados a fornecer informações de local.</span><span class="sxs-lookup"><span data-stu-id="d8276-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="d8276-162">Evite usar um parâmetro ou variável para a versão de API de um tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="d8276-163">Os valores e propriedades do recurso podem variar de acordo com o número de versão.</span><span class="sxs-lookup"><span data-stu-id="d8276-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="d8276-164">O IntelliSense em um editor de código não pode determinar o esquema correto quando a versão da API é definida como um parâmetro ou uma variável.</span><span class="sxs-lookup"><span data-stu-id="d8276-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="d8276-165">Em vez disso, codifique a versão da API no modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="d8276-166">variáveis</span><span class="sxs-lookup"><span data-stu-id="d8276-166">Variables</span></span>
<span data-ttu-id="d8276-167">As seguintes informações podem ser úteis quando você trabalha com variáveis:</span><span class="sxs-lookup"><span data-stu-id="d8276-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="d8276-168">Use variáveis para valores que você precisa usar mais de uma vez em um modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="d8276-169">Se um valor for usado apenas uma vez, um valor embutido em código facilita a leitura do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="d8276-170">Não é possível usar a função [reference](resource-group-template-functions-resource.md#reference) na seção de **variables** do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="d8276-171">A função **reference** deriva seu valor do estado de tempo de execução do recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="d8276-172">No entanto, as variáveis são resolvidas durante a análise inicial do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="d8276-173">Construa valores que precisam da função **reference** diretamente na seção **resources** ou **outputs** do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="d8276-174">Inclua variáveis em nomes de recurso que devem ser exclusivos, conforme descrito em [Nomes de recurso](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="d8276-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="d8276-175">Você pode agrupar variáveis em objetos complexos.</span><span class="sxs-lookup"><span data-stu-id="d8276-175">You can group variables into complex objects.</span></span> <span data-ttu-id="d8276-176">Use o formato **variable.subentry** para fazer referência a um valor de um objeto complexo.</span><span class="sxs-lookup"><span data-stu-id="d8276-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="d8276-177">O agrupamento de variáveis pode ajudar a rastrear variáveis relacionadas.</span><span class="sxs-lookup"><span data-stu-id="d8276-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="d8276-178">Ele também melhora a legibilidade do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-178">It also improves readability of the template.</span></span> <span data-ttu-id="d8276-179">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="d8276-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="d8276-180">Um objeto complexo não pode conter uma expressão que faça referência a um valor de um objeto complexo.</span><span class="sxs-lookup"><span data-stu-id="d8276-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="d8276-181">Defina uma variável separada para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="d8276-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="d8276-182">Para obter exemplos avançados de como usar objetos complexos como variáveis, confira [Compartilhar estado nos modelos do Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="d8276-183">Recursos</span><span class="sxs-lookup"><span data-stu-id="d8276-183">Resources</span></span>
<span data-ttu-id="d8276-184">As seguintes informações podem ser úteis quando você trabalha com recursos:</span><span class="sxs-lookup"><span data-stu-id="d8276-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="d8276-185">Para ajudar outros colaboradores a entender a finalidade do recurso, especifique **comentários** para cada recurso no modelo:</span><span class="sxs-lookup"><span data-stu-id="d8276-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="d8276-186">Você pode usar marcação para adicionar metadados aos recursos.</span><span class="sxs-lookup"><span data-stu-id="d8276-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="d8276-187">Use metadados para adicionar informações sobre os recursos.</span><span class="sxs-lookup"><span data-stu-id="d8276-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="d8276-188">Por exemplo, você pode adicionar metadados para registrar detalhes de cobrança para um recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="d8276-189">Para obter mais informações, veja [Usando marcas para organizar os recursos do Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="d8276-190">Se você usar um *ponto de extremidade público* em seu modelo (como um ponto de extremidade público de Armazenamento de Blobs do Azure), o namespace *não deverá ser embutido em código*.</span><span class="sxs-lookup"><span data-stu-id="d8276-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="d8276-191">Use a função **reference** para recuperar dinamicamente o namespace.</span><span class="sxs-lookup"><span data-stu-id="d8276-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="d8276-192">Você pode usar essa abordagem para implantar o modelo em ambientes de namespace públicos diferentes, sem alterar manualmente o ponto de extremidade no modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="d8276-193">Defina a versão da API para a mesma versão que você está usando para a conta de armazenamento em seu modelo:</span><span class="sxs-lookup"><span data-stu-id="d8276-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="d8276-194">Se a conta de armazenamento for implantada no mesmo modelo que você estiver criando, não será preciso especificar o namespace do provedor quando referenciar o recurso.</span><span class="sxs-lookup"><span data-stu-id="d8276-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="d8276-195">Esta é a sintaxe simplificada:</span><span class="sxs-lookup"><span data-stu-id="d8276-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="d8276-196">Se você tiver outros valores no seu modelo que sejam configurados para usar um namespace público, altere esses valores para refletir a mesma função **reference**.</span><span class="sxs-lookup"><span data-stu-id="d8276-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="d8276-197">Por exemplo, a propriedade **storageUri** do perfil de diagnóstico da máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="d8276-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="d8276-198">Você também pode fazer referência a uma conta de armazenamento existente que esteja em um grupo de recursos diferente:</span><span class="sxs-lookup"><span data-stu-id="d8276-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="d8276-199">Atribua endereços IP públicos a uma máquina virtual somente quando um aplicativo exigir.</span><span class="sxs-lookup"><span data-stu-id="d8276-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="d8276-200">Para se conectar a uma VM (máquina virtual) para depuração, ou para fins administrativos ou de gerenciamento, use regras NAT de entrada, um gateway de rede virtual ou um jumpbox.</span><span class="sxs-lookup"><span data-stu-id="d8276-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="d8276-201">Para saber mais sobre como se conectar às máquinas virtuais, confira:</span><span class="sxs-lookup"><span data-stu-id="d8276-201">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="d8276-202">Executar VMs para uma arquitetura de N camadas no Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="d8276-203">Configurar acesso WinRM para VMs no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8276-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="d8276-204">Permitir acesso externo à sua VM usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="d8276-205">Permitir acesso externo à sua VM usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8276-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="d8276-206">Permitir acesso externo à sua VM Linux usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d8276-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="d8276-207">A propriedade **domainNameLabel** para endereços IP públicos deve ser exclusiva.</span><span class="sxs-lookup"><span data-stu-id="d8276-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="d8276-208">O valor de **domainNameLabel** deve ter entre 3 e 63 caracteres e seguir as regras especificadas por essa expressão regular: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="d8276-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="d8276-209">Como a função **uniqueString** gera uma cadeia de caracteres com tamanho de 13 caracteres, o parâmetro **dnsPrefixString** é limitado a 50 caracteres:</span><span class="sxs-lookup"><span data-stu-id="d8276-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="d8276-210">Quando você adiciona uma senha a uma extensão de script personalizada, use a propriedade **commandToExecute** na propriedade **protectedSettings**:</span><span class="sxs-lookup"><span data-stu-id="d8276-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="d8276-211">Para garantir que os segredos sejam criptografados quando passados como parâmetros para VMs e extensões, use a propriedade **protectedSettings** das extensões relevantes.</span><span class="sxs-lookup"><span data-stu-id="d8276-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="d8276-212">outputs</span><span class="sxs-lookup"><span data-stu-id="d8276-212">Outputs</span></span>
<span data-ttu-id="d8276-213">Se você usar um modelo para criar endereços IP públicos, inclua uma seção **outputs** que retorne detalhes do endereço IP e o FQDN (nome de domínio totalmente qualificado).</span><span class="sxs-lookup"><span data-stu-id="d8276-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="d8276-214">É possível usar valores de saída para recuperar facilmente detalhes sobre endereços IP públicos e FQDNs após a implantação.</span><span class="sxs-lookup"><span data-stu-id="d8276-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="d8276-215">Ao fazer referência ao recurso, use a versão da API que foi usada para criá-lo:</span><span class="sxs-lookup"><span data-stu-id="d8276-215">When you reference the resource, use the API version that you used to create it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="d8276-216">Modelo único vs. modelos aninhados</span><span class="sxs-lookup"><span data-stu-id="d8276-216">Single template vs. nested templates</span></span>
<span data-ttu-id="d8276-217">Para implantar sua solução, você pode usar um único modelo, ou um modelo principal com vários modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d8276-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="d8276-218">Os modelos aninhados são comuns em cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="d8276-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="d8276-219">Usar um modelo aninhado proporciona as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="d8276-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="d8276-220">Você pode dividir uma solução em componentes direcionados.</span><span class="sxs-lookup"><span data-stu-id="d8276-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="d8276-221">Você pode reutilizar modelos aninhados com diferentes modelos principais.</span><span class="sxs-lookup"><span data-stu-id="d8276-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="d8276-222">Caso opte por usar modelos aninhados, as diretrizes a seguir podem ajudar a padronizar o design do modelo.</span><span class="sxs-lookup"><span data-stu-id="d8276-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="d8276-223">Essas diretrizes se baseiam nos [padrões de design para modelos do Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="d8276-224">É recomendável um design que tenha os seguintes modelos:</span><span class="sxs-lookup"><span data-stu-id="d8276-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="d8276-225">**Modelo principal** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d8276-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="d8276-226">Use para os parâmetros de entrada.</span><span class="sxs-lookup"><span data-stu-id="d8276-226">Use for the input parameters.</span></span>
* <span data-ttu-id="d8276-227">**Modelo de recursos compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="d8276-227">**Shared resources template**.</span></span> <span data-ttu-id="d8276-228">Use para implantar recursos compartilhados que todos os outros recursos usam (por exemplo, rede virtual e conjuntos de disponibilidade).</span><span class="sxs-lookup"><span data-stu-id="d8276-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="d8276-229">Use a expressão **dependsOn** para garantir que esse modelo seja implantado antes de outros modelos.</span><span class="sxs-lookup"><span data-stu-id="d8276-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="d8276-230">**Modelo de recursos opcionais**.</span><span class="sxs-lookup"><span data-stu-id="d8276-230">**Optional resources template**.</span></span> <span data-ttu-id="d8276-231">Use para implantar condicionalmente recursos baseados em um parâmetro (por exemplo, um jumpbox).</span><span class="sxs-lookup"><span data-stu-id="d8276-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="d8276-232">**Modelo de recursos de membro**.</span><span class="sxs-lookup"><span data-stu-id="d8276-232">**Member resources template**.</span></span> <span data-ttu-id="d8276-233">Cada tipo de instância dentro de uma camada de aplicativo tem sua própria configuração.</span><span class="sxs-lookup"><span data-stu-id="d8276-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="d8276-234">Dentro de uma camada, você pode definir tipos diferentes de instância.</span><span class="sxs-lookup"><span data-stu-id="d8276-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="d8276-235">(Por exemplo, a primeira instância cria um cluster e as instâncias adicionais são incluídas no cluster existente.) Cada tipo de instância tem seu próprio modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="d8276-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="d8276-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="d8276-236">**Scripts**.</span></span> <span data-ttu-id="d8276-237">Scripts amplamente reutilizáveis são aplicáveis a cada tipo de instância (por exemplo, inicializar e formatar discos adicionais).</span><span class="sxs-lookup"><span data-stu-id="d8276-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="d8276-238">Os scripts personalizados que você cria para uma finalidade específica de personalização são diferentes, com base no tipo de instância.</span><span class="sxs-lookup"><span data-stu-id="d8276-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Modelo aninhado](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="d8276-240">Para saber mais, confira [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="d8276-241">Criar link condicional para modelos aninhados</span><span class="sxs-lookup"><span data-stu-id="d8276-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="d8276-242">Você pode usar um parâmetro para criar link condicional para modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d8276-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="d8276-243">O parâmetro torna-se parte do URI do modelo:</span><span class="sxs-lookup"><span data-stu-id="d8276-243">The parameter becomes part of the URI for the template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="d8276-244">Formato de modelo</span><span class="sxs-lookup"><span data-stu-id="d8276-244">Template format</span></span>
<span data-ttu-id="d8276-245">É uma boa prática passar o modelo por meio de um validador JSON.</span><span class="sxs-lookup"><span data-stu-id="d8276-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="d8276-246">Um validador pode ajudar a remover vírgulas, parênteses e colchetes irrelevantes que podem gerar um erro durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="d8276-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="d8276-247">Experimente o [JSONLint](http://jsonlint.com/) ou um pacote linter para seu ambiente de edição favorito (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d8276-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="d8276-248">Também convém formatar o JSON para melhorar a legibilidade.</span><span class="sxs-lookup"><span data-stu-id="d8276-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="d8276-249">Você pode usar um pacote de formatador JSON para seu editor local.</span><span class="sxs-lookup"><span data-stu-id="d8276-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="d8276-250">No Visual Studio, para formatar o documento, pressione **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="d8276-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="d8276-251">No Visual Studio Code, pressione **Alt + Shift + F**.</span><span class="sxs-lookup"><span data-stu-id="d8276-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="d8276-252">Se o seu editor local não formata o documento, use um [formatador online](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="d8276-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8276-253">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8276-253">Next steps</span></span>
* <span data-ttu-id="d8276-254">Para obter diretrizes sobre a arquitetura de sua solução para máquinas virtuais, confira [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Executar uma VM Windows no Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Executar uma VM Linux no Azure).</span><span class="sxs-lookup"><span data-stu-id="d8276-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="d8276-255">Para obter orientação sobre como configurar uma conta de armazenamento, confira [Lista de verificação de desempenho e escalabilidade do armazenamento do Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="d8276-256">Para saber mais sobre como uma empresa pode usar o Resource Manager para gerenciar assinaturas com eficiência, confira [Andaime empresarial do Azure: governança de assinatura prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d8276-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

