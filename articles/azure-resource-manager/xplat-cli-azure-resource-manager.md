---
title: Gerenciar recursos com a CLI do Azure | Microsoft Docs
description: Use a Interface de linha de comando (CLI) do Azure para gerenciar recursos e grupos do Azure
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="2baa2-103">Use a CLI do Azure para gerenciar recursos e grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2baa2-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2baa2-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2baa2-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="2baa2-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2baa2-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="2baa2-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2baa2-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="2baa2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="2baa2-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="2baa2-108">A Interface de linha de comando do Azure (CLI do Azure) é uma das várias ferramentas que você pode usar para implantar e gerenciar recursos com o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2baa2-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="2baa2-109">Este artigo apresenta as maneiras comuns de gerenciar os recursos e os grupos de recursos do Azure usando a CLI do Azure no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2baa2-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="2baa2-110">Para saber mais sobre como usar a CLI para implantar recursos, confira [Implantar recursos com modelos do Resource Manager e a CLI do Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="2baa2-111">Para saber mais sobre o os recursos e o Resource Manager do Azure, visite a [Visão Geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2baa2-112">Para gerenciar os recursos do Azure com a CLI do Azure, você precisa [instalar a CLI](../cli-install-nodejs.md) do Azure, e [fazer logon no Azure](../xplat-cli-connect.md) usando o comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="2baa2-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="2baa2-113">Verifique se a CLI está no modo Resource Manager (execute `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="2baa2-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="2baa2-114">Se você tiver feito isso, você está pronto para continuar.</span><span class="sxs-lookup"><span data-stu-id="2baa2-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="2baa2-115">Obtenha os grupos de recursos e os recursos</span><span class="sxs-lookup"><span data-stu-id="2baa2-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="2baa2-116">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="2baa2-116">Resource groups</span></span>
<span data-ttu-id="2baa2-117">Para obter uma lista de todos os grupos de recursos em sua assinatura e suas localizações, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="2baa2-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="2baa2-118">Recursos</span><span class="sxs-lookup"><span data-stu-id="2baa2-118">Resources</span></span>
 <span data-ttu-id="2baa2-119">Para listar todos os recursos em um grupo, como um de nome *testRG*, por exemplo, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2baa2-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="2baa2-120">Para exibir um recurso individual dentro do grupo, como uma VM denominada *MyUbuntuVM*, use um comando semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="2baa2-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="2baa2-121">Observe o parâmetro **Microsoft.Compute/virtualMachines**.</span><span class="sxs-lookup"><span data-stu-id="2baa2-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="2baa2-122">Esse parâmetro indica o tipo do recurso sobre o qual você está solicitando informações.</span><span class="sxs-lookup"><span data-stu-id="2baa2-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="2baa2-123">Ao usar os comandos **azure resource** que não sejam o comando **list**, você deve especificar a versão da API do recurso com o parâmetro **-o**.</span><span class="sxs-lookup"><span data-stu-id="2baa2-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="2baa2-124">Se você não tiver certeza sobre a versão da API a ser usada, consulte o arquivo de modelo e localize o campo apiVersion do recurso.</span><span class="sxs-lookup"><span data-stu-id="2baa2-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="2baa2-125">Para obter mais informações sobre as versões da API no Resource Manager, consulte [Provedores de recursos e tipos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="2baa2-126">Ao exibir detalhes em um recurso, costuma ser útil usar o parâmetro `--json`.</span><span class="sxs-lookup"><span data-stu-id="2baa2-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="2baa2-127">Esse parâmetro torna a saída mais legível já que alguns valores são estruturas aninhadas ou coleções.</span><span class="sxs-lookup"><span data-stu-id="2baa2-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="2baa2-128">O exemplo a seguir demonstra o retorno dos resultados do comando **show** como um documento JSON.</span><span class="sxs-lookup"><span data-stu-id="2baa2-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="2baa2-129">Caso deseje, salve os dados JSON no arquivo usando o caractere &gt; para direcionar a saída para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="2baa2-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="2baa2-130">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2baa2-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="2baa2-131">Marcas</span><span class="sxs-lookup"><span data-stu-id="2baa2-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="2baa2-132">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="2baa2-132">Manage resources</span></span>
<span data-ttu-id="2baa2-133">Para adicionar um recurso como uma conta de armazenamento a um grupo de recursos, execute um comando semelhante a:</span><span class="sxs-lookup"><span data-stu-id="2baa2-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="2baa2-134">Além de especificar a versão da API do recurso com o parâmetro **-o**, use o parâmetro **-p** para passar uma cadeia de caracteres formatada em JSON com quaisquer propriedades necessárias ou adicionais.</span><span class="sxs-lookup"><span data-stu-id="2baa2-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="2baa2-135">Para excluir um recurso existente, como um recurso de máquina virtual, use um comando como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2baa2-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="2baa2-136">Para mover os recursos existentes para outro grupo de recursos ou assinatura, use o comando **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="2baa2-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="2baa2-137">O exemplo a seguir mostra como mover um Cache Redis para um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2baa2-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="2baa2-138">No parâmetro **-i** , forneça uma lista separada por vírgulas de ids do recurso a serem movidas.</span><span class="sxs-lookup"><span data-stu-id="2baa2-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="2baa2-139">Controlar acesso a recursos</span><span class="sxs-lookup"><span data-stu-id="2baa2-139">Control access to resources</span></span>
<span data-ttu-id="2baa2-140">Você pode usar a CLI do Azure para criar e gerenciar políticas para controlar o acesso aos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2baa2-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="2baa2-141">Para obter informações sobre definições de política e atribuição de políticas para recursos, confira [Usar a política para gerenciar recursos e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="2baa2-142">Por exemplo, defina a seguinte política para negar todas as solicitações onde o local não é Oeste dos EUA ou Centro-Norte dos EUA e salvar para o arquivo de definição de política policy.json:</span><span class="sxs-lookup"><span data-stu-id="2baa2-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="2baa2-143">Em seguida, execute o comando **policy definition create**:</span><span class="sxs-lookup"><span data-stu-id="2baa2-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="2baa2-144">Esse comando exibe uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="2baa2-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="2baa2-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="2baa2-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="2baa2-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="2baa2-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="2baa2-147">Para atribuir uma política no escopo desejado, use a **PolicyDefinitionId** retornada pelo comando anterior.</span><span class="sxs-lookup"><span data-stu-id="2baa2-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="2baa2-148">No exemplo a seguir, este escopo é a assinatura, mas você pode definir o escopo para recursos individuais ou grupos de recursos:</span><span class="sxs-lookup"><span data-stu-id="2baa2-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="2baa2-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="2baa2-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="2baa2-150">Você pode obter, alterar ou remover definições de política usando os comandos **policy definition show**, **policy definition set**, e **policy definition delete**.</span><span class="sxs-lookup"><span data-stu-id="2baa2-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="2baa2-151">De modo semelhante você pode obter, alterar ou remover atribuições de política usando os comandos **policy assignment show**, **policy assignment set** e **policy assignment delete**.</span><span class="sxs-lookup"><span data-stu-id="2baa2-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="2baa2-152">Exportar um grupo de recursos como um modelo</span><span class="sxs-lookup"><span data-stu-id="2baa2-152">Export a resource group as a template</span></span>
<span data-ttu-id="2baa2-153">Para um grupo de recursos existente, você pode exibir o modelo Resource Manager do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2baa2-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="2baa2-154">A exportação do modelo oferece dois benefícios:</span><span class="sxs-lookup"><span data-stu-id="2baa2-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="2baa2-155">Você pode automatizar com facilidade as implantações futuras da solução, pois toda a infraestrutura está definida no modelo.</span><span class="sxs-lookup"><span data-stu-id="2baa2-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="2baa2-156">Você pode familiarizar-se com a sintaxe do modelo analisando o JSON que representa sua solução.</span><span class="sxs-lookup"><span data-stu-id="2baa2-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="2baa2-157">Usando a CLI do Azure, você pode exportar um modelo que representa o estado atual do seu grupo de recursos ou baixar o modelo que foi usado para uma determinada implantação.</span><span class="sxs-lookup"><span data-stu-id="2baa2-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="2baa2-158">**Exportar o modelo para um grupo de recursos** - Isso será útil quando você tiver feito alterações em um grupo de recursos e precisar recuperar a representação JSON de seu estado atual.</span><span class="sxs-lookup"><span data-stu-id="2baa2-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="2baa2-159">No entanto, o modelo gerado contém apenas uma quantidade mínima de parâmetros e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="2baa2-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="2baa2-160">A maioria dos valores no modelo é embutida em código.</span><span class="sxs-lookup"><span data-stu-id="2baa2-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="2baa2-161">Antes de implantar o modelo gerado, convém converter mais valores em parâmetros, para que você possa personalizar a implantação para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="2baa2-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="2baa2-162">Para exportar o modelo de um grupo de recursos para um diretório local, execute o comando `azure group export` como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="2baa2-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="2baa2-163">(Substitua seu ambiente do sistema operacional por um diretório local apropriado).</span><span class="sxs-lookup"><span data-stu-id="2baa2-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="2baa2-164">**Baixar o modelo de uma determinada implantação** – Isso será útil quando você precisar exibir o modelo real que foi usado para implantar os recursos.</span><span class="sxs-lookup"><span data-stu-id="2baa2-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="2baa2-165">O modelo inclui todos os parâmetros e variáveis definidos para a implantação original.</span><span class="sxs-lookup"><span data-stu-id="2baa2-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="2baa2-166">No entanto, se alguém em sua organização tiver feito alterações ao grupo de recursos que estejam fora da definição no modelo, esse modelo não representa o estado atual do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2baa2-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="2baa2-167">Para baixar o modelo usado de uma implantação específica para um diretório local, execute o comando `azure group deployment template download`.</span><span class="sxs-lookup"><span data-stu-id="2baa2-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="2baa2-168">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2baa2-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="2baa2-169">A exportação do modelo está na visualização e nem todos os tipos de recursos oferecem suporte atualmente para a exportação de um modelo.</span><span class="sxs-lookup"><span data-stu-id="2baa2-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="2baa2-170">Ao tentar exportar um modelo, talvez você veja um erro afirmando que alguns recursos não foram exportados.</span><span class="sxs-lookup"><span data-stu-id="2baa2-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="2baa2-171">Se for necessário, defina manualmente esses recursos em seu modelo depois de baixá-lo.</span><span class="sxs-lookup"><span data-stu-id="2baa2-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2baa2-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2baa2-172">Next steps</span></span>
* <span data-ttu-id="2baa2-173">Para obter detalhes de operações de implantação e solucionar erros de implantação com a CLI do Azure, confira [View deployment operations](resource-manager-deployment-operations.md) (Exibir operações de implantação).</span><span class="sxs-lookup"><span data-stu-id="2baa2-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="2baa2-174">Se você quiser usar a CLI para configurar um aplicativo ou script para acessar recursos, confira [Usar a CLI do Azure para criar uma entidade de serviço a fim de acessar recursos](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="2baa2-175">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2baa2-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

