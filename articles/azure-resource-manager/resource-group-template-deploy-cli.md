---
title: recursos de aaaDeploy com CLI do Azure e o modelo | Microsoft Docs
description: "Use o Gerenciador de recursos do Azure e a CLI do Azure toodeploy um tooAzure de recursos. Olá recursos são definidos em um modelo do Gerenciador de recursos."
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
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="a9710-104">Implantar recursos com modelos do Resource Manager e a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a9710-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="a9710-105">Este tópico explica como toouse 2.0 do CLI do Azure com o Gerenciador de recursos modelos toodeploy tooAzure seus recursos.</span><span class="sxs-lookup"><span data-stu-id="a9710-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="a9710-106">Se você não estiver familiarizado com conceitos de saudação de implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="a9710-107">modelo do Gerenciador de recursos de saudação implantar pode ser um arquivo local no seu computador ou um arquivo externo que está localizado em um repositório como GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9710-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="a9710-108">modelo de saudação implantar neste artigo está disponível no hello [modelo](#sample-template) seção, ou como um [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a9710-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="a9710-109">Se você não tiver a CLI do Azure instalado, você pode usar o hello [nuvem Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="a9710-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="a9710-110">Implantar o modelo local</span><span class="sxs-lookup"><span data-stu-id="a9710-110">Deploy local template</span></span>

<span data-ttu-id="a9710-111">Ao implantar recursos tooAzure, você:</span><span class="sxs-lookup"><span data-stu-id="a9710-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="a9710-112">Faça logon no tooyour conta do Azure</span><span class="sxs-lookup"><span data-stu-id="a9710-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="a9710-113">Crie um grupo de recursos que funciona como contêiner Olá para recursos de saudação implantado.</span><span class="sxs-lookup"><span data-stu-id="a9710-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="a9710-114">nome de Olá saudação do grupo de recursos pode incluir somente caracteres alfanuméricos, períodos, sublinhados, hifens e parênteses.</span><span class="sxs-lookup"><span data-stu-id="a9710-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="a9710-115">Ele pode ser too90 caracteres.</span><span class="sxs-lookup"><span data-stu-id="a9710-115">It can be up too90 characters.</span></span> <span data-ttu-id="a9710-116">Não pode terminar com um ponto.</span><span class="sxs-lookup"><span data-stu-id="a9710-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="a9710-117">Implantar o modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate</span><span class="sxs-lookup"><span data-stu-id="a9710-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="a9710-118">Um modelo pode incluir parâmetros que permitem a implantação de saudação toocustomize.</span><span class="sxs-lookup"><span data-stu-id="a9710-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="a9710-119">Por exemplo, você pode fornecer valores que são personalizados para um determinado ambiente (como desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="a9710-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="a9710-120">modelo de exemplo Hello define um parâmetro para a conta de armazenamento Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="a9710-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="a9710-121">saudação de exemplo a seguir cria um grupo de recursos e implanta um modelo do computador local:</span><span class="sxs-lookup"><span data-stu-id="a9710-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="a9710-122">implantação de saudação pode levar toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a9710-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="a9710-123">Quando terminar, você verá uma mensagem que contém o resultado de saudação:</span><span class="sxs-lookup"><span data-stu-id="a9710-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="a9710-124">Implantar modelo externo</span><span class="sxs-lookup"><span data-stu-id="a9710-124">Deploy external template</span></span>

<span data-ttu-id="a9710-125">Em vez de armazenar modelos do Gerenciador de recursos em seu computador local, você pode preferir toostore-los em um local externo.</span><span class="sxs-lookup"><span data-stu-id="a9710-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="a9710-126">É possível armazenar modelos em um repositório de controle de código-fonte (como o GitHub).</span><span class="sxs-lookup"><span data-stu-id="a9710-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="a9710-127">Ou ainda armazená-los em uma conta de armazenamento do Azure para acesso compartilhado na sua organização.</span><span class="sxs-lookup"><span data-stu-id="a9710-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="a9710-128">toodeploy um modelo externo, use Olá **modelo uri** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a9710-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="a9710-129">Use Olá URI no modelo de exemplo hello exemplo toodeploy saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9710-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="a9710-130">Olá exemplo anterior requer um URI acessível publicamente para modelo de saudação, que funciona na maioria dos cenários, porque o modelo não deve incluir dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="a9710-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="a9710-131">Se você precisar toospecify os dados confidenciais (como uma senha de administrador), passe esse valor como um parâmetro seguro.</span><span class="sxs-lookup"><span data-stu-id="a9710-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="a9710-132">No entanto, se você não quiser que seu modelo toobe publicamente acessível, você pode protegê-los, armazenando-o em um contêiner de armazenamento privado.</span><span class="sxs-lookup"><span data-stu-id="a9710-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="a9710-133">Para obter informações sobre como implantar um modelo que exige um token SAS (assinatura de acesso compartilhado), confira [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="a9710-134">Implantar o modelo do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="a9710-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="a9710-135">Você pode usar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="a9710-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="a9710-136">No entanto, você deve carregar o modelo pela primeira vez no compartilhamento de arquivo hello para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9710-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="a9710-137">Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="a9710-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="a9710-138">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9710-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="a9710-139">Selecione o grupo de recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a9710-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="a9710-140">Olá nome padrão é `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="a9710-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Escolha o grupo de recursos](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="a9710-142">Selecione a conta de armazenamento de saudação para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9710-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Escolher conta de armazenamento](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="a9710-144">Selecionar **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a9710-144">Select **Files**.</span></span>

   ![Selecionar arquivos](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="a9710-146">Selecione o compartilhamento de arquivo de saudação para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9710-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="a9710-147">Olá nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="a9710-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selecionar compartilhamento de arquivos](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="a9710-149">Selecione **Adicionar diretório**.</span><span class="sxs-lookup"><span data-stu-id="a9710-149">Select **Add directory**.</span></span>

   ![Adicionar diretório](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="a9710-151">Dê a ele o nome de **modelos**e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9710-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nomear diretório](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="a9710-153">Selecione o novo diretório.</span><span class="sxs-lookup"><span data-stu-id="a9710-153">Select your new directory.</span></span>

   ![Selecionar diretório](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="a9710-155">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="a9710-155">Select **Upload**.</span></span>

   ![Selecionar Carregar](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="a9710-157">Localizar e carregar o modelo.</span><span class="sxs-lookup"><span data-stu-id="a9710-157">Find and upload your template.</span></span>

   ![Carregar arquivo](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="a9710-159">Prompt Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="a9710-159">Open hello prompt.</span></span>

   ![Abrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="a9710-161">Digite hello comandos Olá Shell de nuvem a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9710-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="a9710-162">Arquivos de parâmetros</span><span class="sxs-lookup"><span data-stu-id="a9710-162">Parameter files</span></span>

<span data-ttu-id="a9710-163">Em vez de passar parâmetros como valores embutido em seu script, talvez seja mais fácil toouse um arquivo JSON que contém os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="a9710-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="a9710-164">arquivo de parâmetro Hello deve ser Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9710-164">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="a9710-165">Observe que a seção de parâmetros de saudação inclui um nome de parâmetro que coincide com o parâmetro hello definido no modelo (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="a9710-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="a9710-166">arquivo de parâmetro Hello contém um valor para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="a9710-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="a9710-167">Esse valor é automaticamente passado toohello modelo durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="a9710-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="a9710-168">Você pode criar vários arquivos de parâmetro para diferentes cenários de implantação e, em seguida, passe no arquivo de parâmetro apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9710-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="a9710-169">Copie Olá anterior de exemplo e salve-o como um arquivo chamado `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="a9710-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="a9710-170">toopass um arquivo de parâmetro de local, use `@` toospecify um arquivo local chamado storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="a9710-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="a9710-171">Testar uma implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="a9710-171">Test a template deployment</span></span>

<span data-ttu-id="a9710-172">tootest seus valores de parâmetro e de modelo sem realmente implantar qualquer recurso, use [implantação de grupo az validar](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="a9710-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="a9710-173">Se nenhum erro for detectado, o comando de Olá retorna informações sobre a implantação de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9710-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="a9710-174">Em particular, observe que Olá **erro** valor é nulo.</span><span class="sxs-lookup"><span data-stu-id="a9710-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="a9710-175">Se um erro for detectado, o comando Olá retorna uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="a9710-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="a9710-176">Por exemplo, a tentativa de toopass um valor incorreto para a conta de armazenamento Olá SKU, retorna Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9710-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="a9710-177">Se seu modelo tem um erro de sintaxe, o comando Olá retorna um erro indicando que ele não foi possível analisar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9710-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="a9710-178">mensagem de saudação indica o número de linha de saudação e a posição do erro de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9710-178">hello message indicates hello line number and position of hello parsing error.</span></span>

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

<span data-ttu-id="a9710-179">toouse completa modo, use Olá `mode` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="a9710-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="a9710-180">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="a9710-180">Sample template</span></span>

<span data-ttu-id="a9710-181">Olá modelo a seguir é usado para obter exemplos de saudação neste tópico.</span><span class="sxs-lookup"><span data-stu-id="a9710-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="a9710-182">Copie-o e salve-o como um arquivo chamado storage.json.</span><span class="sxs-lookup"><span data-stu-id="a9710-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="a9710-183">toounderstand como toocreate esse modelo, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="a9710-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a9710-184">Next steps</span></span>
* <span data-ttu-id="a9710-185">exemplos de saudação neste artigo implantar grupo de recursos de tooa de recursos em sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="a9710-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="a9710-186">toouse uma assinatura diferente, consulte [gerenciar várias assinaturas do Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9710-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="a9710-187">Para um script de exemplo completo que implanta um modelo, veja [Script de implantação do modelo do Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="a9710-188">toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a9710-189">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="a9710-190">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="a9710-191">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a9710-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
