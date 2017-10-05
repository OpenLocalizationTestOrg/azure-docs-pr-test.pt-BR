---
title: Implantar recursos com a CLI do Azure e o modelo | Microsoft Docs
description: "Use o Azure Resource Manager e a CLI do Azure para implantar recursos no Azure. Os recursos são definidos em um modelo do Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="7b86f-104">Implantar recursos com modelos do Resource Manager e a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7b86f-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="7b86f-105">Este tópico explica como usar a CLI 2.0 do Azure com modelos do Resource Manager para implantar seus recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="7b86f-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="7b86f-106">Caso não esteja familiarizado com os conceitos de implantação e gerenciamento das suas soluções Azure, confira [Visão geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="7b86f-107">O modelo do Resource Manager que você implanta pode ser um arquivo local do seu computador ou um arquivo externo que está localizado em um repositório como o GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b86f-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="7b86f-108">O modelo que você implanta neste artigo está disponível na seção [Modelo de exemplo](#sample-template) ou como um [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7b86f-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="7b86f-109">Se você não tiver a CLI do Azure instalado, você pode usar o [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="7b86f-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="7b86f-110">Implantar o modelo local</span><span class="sxs-lookup"><span data-stu-id="7b86f-110">Deploy local template</span></span>

<span data-ttu-id="7b86f-111">Ao implantar recursos no Azure, você:</span><span class="sxs-lookup"><span data-stu-id="7b86f-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="7b86f-112">Fazer logon na sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="7b86f-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="7b86f-113">Crie um grupo de recursos que atue como o contêiner para os recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="7b86f-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="7b86f-114">O nome do grupo de recursos pode incluir somente caracteres alfanuméricos, pontos, sublinhados, hifens e parênteses.</span><span class="sxs-lookup"><span data-stu-id="7b86f-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="7b86f-115">Pode ter até 90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="7b86f-115">It can be up to 90 characters.</span></span> <span data-ttu-id="7b86f-116">Não pode terminar com um ponto.</span><span class="sxs-lookup"><span data-stu-id="7b86f-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="7b86f-117">Implanta no grupo de recursos o modelo que define os recursos a serem criados</span><span class="sxs-lookup"><span data-stu-id="7b86f-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="7b86f-118">Um modelo pode incluir parâmetros que permitem personalizar a implantação.</span><span class="sxs-lookup"><span data-stu-id="7b86f-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="7b86f-119">Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="7b86f-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="7b86f-120">O modelo de exemplo define um parâmetro para o SKU da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7b86f-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="7b86f-121">O exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:</span><span class="sxs-lookup"><span data-stu-id="7b86f-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="7b86f-122">A implantação pode levar alguns minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="7b86f-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="7b86f-123">Quando ela for concluída, você verá uma mensagem que inclui o resultado:</span><span class="sxs-lookup"><span data-stu-id="7b86f-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="7b86f-124">Implantar modelo externo</span><span class="sxs-lookup"><span data-stu-id="7b86f-124">Deploy external template</span></span>

<span data-ttu-id="7b86f-125">Em vez de armazenar modelos do Resource Manager no computador local, talvez você prefira armazená-los em um local externo.</span><span class="sxs-lookup"><span data-stu-id="7b86f-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="7b86f-126">É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub).</span><span class="sxs-lookup"><span data-stu-id="7b86f-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="7b86f-127">Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.</span><span class="sxs-lookup"><span data-stu-id="7b86f-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="7b86f-128">Para implantar um modelo externo, use o parâmetro **template-uri**.</span><span class="sxs-lookup"><span data-stu-id="7b86f-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="7b86f-129">Use o URI do exemplo para implantar o modelo de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="7b86f-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="7b86f-130">O exemplo anterior requer um URI acessível publicamente para o modelo, que funciona na maioria dos cenários, pois o modelo não deve incluir dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="7b86f-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="7b86f-131">Se você precisar especificar dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro.</span><span class="sxs-lookup"><span data-stu-id="7b86f-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="7b86f-132">No entanto, se não quiser que o modelo seja acessível publicamente, você pode protegê-lo armazenando-o em um contêiner de armazenamento privado.</span><span class="sxs-lookup"><span data-stu-id="7b86f-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="7b86f-133">Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="7b86f-134">Implantar o modelo do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7b86f-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="7b86f-135">Você pode usar o [Cloud Shell](../cloud-shell/overview.md) para executar os comandos da CLI do Azure a fim de implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="7b86f-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="7b86f-136">No entanto, você deve carregar o modelo primeiro para o compartilhamento de arquivos do seu Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="7b86f-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="7b86f-137">Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="7b86f-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="7b86f-138">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b86f-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="7b86f-139">Selecione o grupo de recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="7b86f-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="7b86f-140">O nome padrão é `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="7b86f-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Escolha o grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="7b86f-142">Selecione a conta de armazenamento do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="7b86f-142">Select the storage account for your Cloud Shell.</span></span>

   ![Escolher conta de armazenamento](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="7b86f-144">Selecionar **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="7b86f-144">Select **Files**.</span></span>

   ![Selecionar arquivos](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="7b86f-146">Selecione o compartilhamento de arquivos para o Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="7b86f-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="7b86f-147">O nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="7b86f-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selecionar compartilhamento de arquivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="7b86f-149">Selecione **Adicionar diretório**.</span><span class="sxs-lookup"><span data-stu-id="7b86f-149">Select **Add directory**.</span></span>

   ![Adicionar diretório](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="7b86f-151">Dê a ele o nome de **modelos**e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b86f-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nomear diretório](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="7b86f-153">Selecione o novo diretório.</span><span class="sxs-lookup"><span data-stu-id="7b86f-153">Select your new directory.</span></span>

   ![Selecionar diretório](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="7b86f-155">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="7b86f-155">Select **Upload**.</span></span>

   ![Selecionar Carregar](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="7b86f-157">Localizar e carregar o modelo.</span><span class="sxs-lookup"><span data-stu-id="7b86f-157">Find and upload your template.</span></span>

   ![Carregar arquivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="7b86f-159">Abra o prompt.</span><span class="sxs-lookup"><span data-stu-id="7b86f-159">Open the prompt.</span></span>

   ![Abrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="7b86f-161">Digite os seguintes comandos no Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="7b86f-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="7b86f-162">Arquivos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="7b86f-162">Parameter files</span></span>

<span data-ttu-id="7b86f-163">Em vez de passar parâmetros como valores embutidos no script, talvez seja mais fácil usar um arquivo JSON que contenha os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7b86f-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="7b86f-164">O arquivo de parâmetro deve estar no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="7b86f-164">The parameter file must be in the following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="7b86f-165">Observe que a seção de parâmetros inclui um nome de parâmetro que corresponde ao parâmetro definido no seu modelo (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="7b86f-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="7b86f-166">O arquivo de parâmetros contém um valor para o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7b86f-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="7b86f-167">Esse valor é passado automaticamente ao modelo durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="7b86f-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="7b86f-168">Você pode criar vários arquivos de parâmetros para diferentes cenários de implantação e, em seguida, passar o arquivo de parâmetros apropriado.</span><span class="sxs-lookup"><span data-stu-id="7b86f-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="7b86f-169">Copie o exemplo anterior e salve-o como um arquivo chamado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="7b86f-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="7b86f-170">Para passar um arquivo de parâmetros local, use `@` para especificar um arquivo local chamado storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="7b86f-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="7b86f-171">Testar uma implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="7b86f-171">Test a template deployment</span></span>

<span data-ttu-id="7b86f-172">Para testar os valores de parâmetro e o modelo sem realmente implantar os recursos, use [az group deployment validate](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="7b86f-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="7b86f-173">Se nenhum erro for detectado, o comando retornará informações sobre a implantação de teste.</span><span class="sxs-lookup"><span data-stu-id="7b86f-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="7b86f-174">Especificamente, observe que o valor de **erro** é null.</span><span class="sxs-lookup"><span data-stu-id="7b86f-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="7b86f-175">Se um erro for detectado, o comando retornará uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="7b86f-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="7b86f-176">Por exemplo, tentar passar um valor incorreto para o SKU da conta de armazenamento, retornará o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="7b86f-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="7b86f-177">Se o modelo tiver um erro de sintaxe, o comando retornará um erro indicando que não foi possível analisar o modelo.</span><span class="sxs-lookup"><span data-stu-id="7b86f-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="7b86f-178">A mensagem indica o número da linha e a posição do erro de análise.</span><span class="sxs-lookup"><span data-stu-id="7b86f-178">The message indicates the line number and position of the parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="7b86f-179">Para usar o modo completo, use o parâmetro `mode`:</span><span class="sxs-lookup"><span data-stu-id="7b86f-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="7b86f-180">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="7b86f-180">Sample template</span></span>

<span data-ttu-id="7b86f-181">O modelo a seguir é usado para os exemplos deste tópico.</span><span class="sxs-lookup"><span data-stu-id="7b86f-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="7b86f-182">Copie-o e salve-o como um arquivo chamado storage.json.</span><span class="sxs-lookup"><span data-stu-id="7b86f-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="7b86f-183">Para entender como criar esse modelo, confira [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="7b86f-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b86f-184">Next steps</span></span>
* <span data-ttu-id="7b86f-185">Os exemplos deste artigo implantam recursos em um grupo de recursos na sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="7b86f-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="7b86f-186">Para usar outra assinatura, confira [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli) (Gerenciar várias assinaturas do Azure).</span><span class="sxs-lookup"><span data-stu-id="7b86f-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="7b86f-187">Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="7b86f-188">Para entender como definir parâmetros em seu modelo, confira [Noções básicas de estrutura e sintaxe dos modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7b86f-189">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="7b86f-190">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="7b86f-191">Para obter orientação sobre como as empresas podem usar o Resource Manager para gerenciar assinaturas de forma eficaz, consulte [Azure enterprise scaffold – controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7b86f-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
