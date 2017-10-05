---
title: Criar o primeiro modelo do Azure Resource Manager | Microsoft Docs
description: "Um guia passo a passo para criar seu primeiro modelo do Azure Resource Manager. Ele mostra como usar a referência de modelo para uma conta de armazenamento para criar o modelo."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="68600-104">Criar e implantar seu primeiro modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="68600-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="68600-105">Este tópico explica as etapas de criação de seu primeiro modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68600-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="68600-106">Os modelos do Resource Manager são arquivos JSON que definem os recursos necessários para implantar sua solução.</span><span class="sxs-lookup"><span data-stu-id="68600-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="68600-107">Para entender os conceitos associados à implantação e ao gerenciamento de soluções do Azure, consulte [Visão geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68600-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="68600-108">Se você já tiver recursos e quiser obter um modelo para esses recursos, consulte [Exportar um modelo do Azure Resource Manager de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="68600-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="68600-109">Para criar e revisar os modelos, você precisa de um editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="68600-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="68600-110">[Visual Studio Code](https://code.visualstudio.com/) é um editor de código entre plataformas aberto e leve.</span><span class="sxs-lookup"><span data-stu-id="68600-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="68600-111">Recomendamos usar o Visual Studio Code para criar modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68600-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="68600-112">Este tópico pressupõe que você esteja usando o VS Code; no entanto, se você tiver outro editor de JSON (como o Visual Studio), use-o.</span><span class="sxs-lookup"><span data-stu-id="68600-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68600-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68600-113">Prerequisites</span></span>

* <span data-ttu-id="68600-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="68600-114">Visual Studio Code.</span></span> <span data-ttu-id="68600-115">Se for necessário, instale-o pelo site [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="68600-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="68600-116">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="68600-116">An Azure subscription.</span></span> <span data-ttu-id="68600-117">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="68600-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="68600-118">Criar modelo</span><span class="sxs-lookup"><span data-stu-id="68600-118">Create template</span></span>

<span data-ttu-id="68600-119">Vamos começar com um modelo simples que implanta uma conta de armazenamento na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="68600-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="68600-120">Selecione **Arquivo** > **Novo Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="68600-120">Select **File** > **New File**.</span></span> 

   ![Novo arquivo](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="68600-122">Copie e cole a seguinte sintaxe JSON em seu arquivo:</span><span class="sxs-lookup"><span data-stu-id="68600-122">Copy and paste the following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="68600-123">Os nomes de conta de armazenamento têm várias restrições que os tornam difíceis de definir.</span><span class="sxs-lookup"><span data-stu-id="68600-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="68600-124">O nome deve ter entre três e 24 caracteres de comprimento e usar somente números e letras minúsculas, além de ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="68600-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="68600-125">O modelo anterior usa a função [uniqueString](resource-group-template-functions-string.md#uniquestring) para gerar um valor de hash.</span><span class="sxs-lookup"><span data-stu-id="68600-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="68600-126">Para dar mais significado a esse valor de hash, ele adiciona o prefixo *storage*.</span><span class="sxs-lookup"><span data-stu-id="68600-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="68600-127">Salve esse arquivo como **azuredeploy.json** em uma pasta local.</span><span class="sxs-lookup"><span data-stu-id="68600-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Salvar modelo](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="68600-129">Implantar modelo</span><span class="sxs-lookup"><span data-stu-id="68600-129">Deploy template</span></span>

<span data-ttu-id="68600-130">Você está pronto para implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="68600-130">You are ready to deploy this template.</span></span> <span data-ttu-id="68600-131">Use o PowerShell ou a CLI do Azure para criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="68600-132">Em seguida, implante uma conta de armazenamento para esse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="68600-133">No caso do PowerShell, use os seguintes comandos na pasta que contém o modelo:</span><span class="sxs-lookup"><span data-stu-id="68600-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="68600-134">No caso de uma instalação local da CLI do Azure, use os seguintes comandos na pasta que contém o modelo:</span><span class="sxs-lookup"><span data-stu-id="68600-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="68600-135">Quando a implantação é concluída, sua conta de armazenamento passa a existir no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="68600-136">Implantar o modelo do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="68600-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="68600-137">Você pode usar o [Cloud Shell](../cloud-shell/overview.md) para executar os comandos da CLI do Azure a fim de implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="68600-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="68600-138">No entanto, você deve carregar o modelo primeiro para o compartilhamento de arquivos do seu Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="68600-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="68600-139">Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="68600-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="68600-140">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68600-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="68600-141">Selecione o grupo de recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="68600-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="68600-142">O nome padrão é `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="68600-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Escolha o grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="68600-144">Selecione a conta de armazenamento do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="68600-144">Select the storage account for your Cloud Shell.</span></span>

   ![Escolher conta de armazenamento](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="68600-146">Selecionar **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="68600-146">Select **Files**.</span></span>

   ![Selecionar arquivos](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="68600-148">Selecione o compartilhamento de arquivos para o Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="68600-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="68600-149">O nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="68600-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selecionar compartilhamento de arquivos](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="68600-151">Selecione **Adicionar diretório**.</span><span class="sxs-lookup"><span data-stu-id="68600-151">Select **Add directory**.</span></span>

   ![Adicionar diretório](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="68600-153">Dê a ele o nome de **modelos**e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="68600-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nomear diretório](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="68600-155">Selecione o novo diretório.</span><span class="sxs-lookup"><span data-stu-id="68600-155">Select your new directory.</span></span>

   ![Selecionar diretório](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="68600-157">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="68600-157">Select **Upload**.</span></span>

   ![Selecionar Carregar](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="68600-159">Localizar e carregar o modelo.</span><span class="sxs-lookup"><span data-stu-id="68600-159">Find and upload your template.</span></span>

   ![Carregar arquivo](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="68600-161">Abra o prompt.</span><span class="sxs-lookup"><span data-stu-id="68600-161">Open the prompt.</span></span>

   ![Abrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="68600-163">Digite os seguintes comandos no Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="68600-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="68600-164">Quando a implantação é concluída, sua conta de armazenamento passa a existir no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="68600-165">Personalizar o modelo</span><span class="sxs-lookup"><span data-stu-id="68600-165">Customize the template</span></span>

<span data-ttu-id="68600-166">O modelo funciona bem, mas não é flexível.</span><span class="sxs-lookup"><span data-stu-id="68600-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="68600-167">Ele sempre implanta um armazenamento com redundância local no Centro-Sul dos EUA.</span><span class="sxs-lookup"><span data-stu-id="68600-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="68600-168">O nome é sempre *armazenamento*, seguido de um valor de hash.</span><span class="sxs-lookup"><span data-stu-id="68600-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="68600-169">Para habilitar o uso do modelo em cenários diferentes, adicione parâmetros a ele.</span><span class="sxs-lookup"><span data-stu-id="68600-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="68600-170">O exemplo a seguir mostra a seção de parâmetros com dois parâmetros.</span><span class="sxs-lookup"><span data-stu-id="68600-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="68600-171">O primeiro parâmetro, `storageSKU`, permite que você especifique o tipo de redundância.</span><span class="sxs-lookup"><span data-stu-id="68600-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="68600-172">Ele restringe os valores que você pode transmitir a valores que são válidos para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="68600-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="68600-173">Ela também especifica um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="68600-173">It also specifies a default value.</span></span> <span data-ttu-id="68600-174">O segundo parâmetro, `storageNamePrefix`, está definido para permitir um máximo de 11 caracteres.</span><span class="sxs-lookup"><span data-stu-id="68600-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="68600-175">Ele especifica um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="68600-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="68600-176">Na seção de variáveis, adicione uma variável chamada `storageName`.</span><span class="sxs-lookup"><span data-stu-id="68600-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="68600-177">Ela combina o valor de prefixo dos parâmetros e um valor de hash a partir da função [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="68600-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="68600-178">Ela usa a função [toLower](resource-group-template-functions-string.md#tolower) para converter todos os caracteres em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="68600-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="68600-179">Para usar esses novos valores na sua conta de armazenamento, altere a definição do recurso:</span><span class="sxs-lookup"><span data-stu-id="68600-179">To use these new values for your storage account, change the resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="68600-180">Observe que o nome da conta de armazenamento agora está definido como a variável que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="68600-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="68600-181">O nome da SKU é definido como o valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="68600-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="68600-182">O local é definido como o mesmo do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="68600-183">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="68600-183">Save your file.</span></span> 

<span data-ttu-id="68600-184">Depois de concluir as etapas neste artigo, o modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="68600-184">After completing the steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="68600-185">Reimplantar o modelo</span><span class="sxs-lookup"><span data-stu-id="68600-185">Redeploy template</span></span>

<span data-ttu-id="68600-186">Reimplante o modelo com valores diferentes.</span><span class="sxs-lookup"><span data-stu-id="68600-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="68600-187">Para o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="68600-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="68600-188">Para a CLI do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="68600-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="68600-189">Para o Cloud Shell, carregue o modelo alterado no compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="68600-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="68600-190">Substitua o arquivo existente.</span><span class="sxs-lookup"><span data-stu-id="68600-190">Overwrite the existing file.</span></span> <span data-ttu-id="68600-191">Em seguida, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="68600-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="68600-192">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="68600-192">Clean up resources</span></span>

<span data-ttu-id="68600-193">Quando não forem mais necessários, limpe os recursos implantados excluindo o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68600-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="68600-194">Para o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="68600-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="68600-195">Para a CLI do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="68600-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="68600-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68600-196">Next steps</span></span>
* <span data-ttu-id="68600-197">Para saber mais sobre a estrutura de um modelo, confira [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="68600-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="68600-198">Para saber mais sobre as propriedades de uma conta de armazenamento, confira [Referência do modelo de contas de armazenamento](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="68600-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="68600-199">Para exibir modelos completos para muitos tipos diferentes de soluções, consulte os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="68600-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
