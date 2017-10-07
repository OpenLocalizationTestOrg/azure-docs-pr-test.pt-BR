---
title: aaaCreate primeiro o modelo do Gerenciador de recursos do Azure | Microsoft Docs
description: "Um guia passo a passo toocreating seu primeiro modelo do Gerenciador de recursos do Azure. Ele mostra como toouse Olá referência de modelo para um modelo de saudação de toocreate de conta de armazenamento."
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
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="c6c2d-104">Criar e implantar seu primeiro modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6c2d-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="c6c2d-105">Este tópico o guiará durante as etapas de saudação de criar seu primeiro modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="c6c2d-106">Modelos do Gerenciador de recursos são arquivos JSON que definem recursos Olá precisar toodeploy para sua solução.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="c6c2d-107">conceitos de saudação do toounderstand associados ao implantar e gerenciar suas soluções do Azure, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="c6c2d-108">Se você tiver os recursos existentes e deseja tooget um modelo para esses recursos, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="c6c2d-109">modelos de toocreate e revisar, é necessário um editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="c6c2d-110">[Visual Studio Code](https://code.visualstudio.com/) é um editor de código entre plataformas aberto e leve.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="c6c2d-111">Recomendamos usar o Visual Studio Code para criar modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="c6c2d-112">Este tópico pressupõe que você esteja usando o VS Code; no entanto, se você tiver outro editor de JSON (como o Visual Studio), use-o.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6c2d-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6c2d-113">Prerequisites</span></span>

* <span data-ttu-id="c6c2d-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-114">Visual Studio Code.</span></span> <span data-ttu-id="c6c2d-115">Se for necessário, instale-o pelo site [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="c6c2d-116">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-116">An Azure subscription.</span></span> <span data-ttu-id="c6c2d-117">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="c6c2d-118">Criar modelo</span><span class="sxs-lookup"><span data-stu-id="c6c2d-118">Create template</span></span>

<span data-ttu-id="c6c2d-119">Vamos começar com um modelo simple que implanta uma tooyour assinatura da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="c6c2d-120">Selecione **Arquivo** > **Novo Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-120">Select **File** > **New File**.</span></span> 

   ![Novo arquivo](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="c6c2d-122">Copie e cole Olá sintaxe JSON a seguir no arquivo:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="c6c2d-123">Nomes de conta de armazenamento tem várias restrições que os tornam difícil tooset.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="c6c2d-124">Olá nome deve ter entre 3 e 24 caracteres de comprimento, use apenas números e letras minúsculas e ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="c6c2d-125">o modelo anterior Hello usa Olá [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate um valor de hash de função.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="c6c2d-126">toogive esse hash valor mais ou seja, ele adiciona o prefixo Olá *armazenamento*.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="c6c2d-127">Salve esse arquivo como **azuredeploy.json** tooa pasta de local.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Salvar modelo](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="c6c2d-129">Implantar modelo</span><span class="sxs-lookup"><span data-stu-id="c6c2d-129">Deploy template</span></span>

<span data-ttu-id="c6c2d-130">Você está pronto toodeploy este modelo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="c6c2d-131">Use o PowerShell ou CLI do Azure toocreate um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="c6c2d-132">Em seguida, você pode implantar um grupo de recursos de toothat de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="c6c2d-133">Para o PowerShell, use Olá comandos a seguir da pasta Olá contendo Olá modelo:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="c6c2d-134">Para uma instalação local da CLI do Azure, use Olá comandos a seguir da pasta Olá contendo Olá modelo:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="c6c2d-135">Quando termina de implantação, sua conta de armazenamento existe no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="c6c2d-136">Implantar o modelo do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="c6c2d-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="c6c2d-137">Você pode usar [nuvem Shell](../cloud-shell/overview.md) comandos toorun Olá CLI do Azure para implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="c6c2d-138">No entanto, você deve carregar o modelo pela primeira vez no compartilhamento de arquivo hello para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="c6c2d-139">Se você ainda não usou o Cloud Shell, confira [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md) para saber mais sobre como configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="c6c2d-140">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="c6c2d-141">Selecione o grupo de recursos do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="c6c2d-142">Olá nome padrão é `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Escolha o grupo de recursos](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="c6c2d-144">Selecione a conta de armazenamento de saudação para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Escolher conta de armazenamento](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="c6c2d-146">Selecionar **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-146">Select **Files**.</span></span>

   ![Selecionar arquivos](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="c6c2d-148">Selecione o compartilhamento de arquivo de saudação para o Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="c6c2d-149">Olá nome padrão é `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selecionar compartilhamento de arquivos](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="c6c2d-151">Selecione **Adicionar diretório**.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-151">Select **Add directory**.</span></span>

   ![Adicionar diretório](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="c6c2d-153">Dê a ele o nome de **modelos**e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nomear diretório](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="c6c2d-155">Selecione o novo diretório.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-155">Select your new directory.</span></span>

   ![Selecionar diretório](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="c6c2d-157">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-157">Select **Upload**.</span></span>

   ![Selecionar Carregar](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="c6c2d-159">Localizar e carregar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-159">Find and upload your template.</span></span>

   ![Carregar arquivo](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="c6c2d-161">Prompt Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-161">Open hello prompt.</span></span>

   ![Abrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="c6c2d-163">Digite hello comandos Olá Shell de nuvem a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="c6c2d-164">Quando termina de implantação, sua conta de armazenamento existe no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="c6c2d-165">Personalizar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="c6c2d-165">Customize hello template</span></span>

<span data-ttu-id="c6c2d-166">modelo de saudação funciona bem, mas não é flexível.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="c6c2d-167">Ele sempre implanta tooSouth um armazenamento redundante localmente centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="c6c2d-168">nome da saudação é sempre *armazenamento* seguido de um valor de hash.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="c6c2d-169">tooenable usando o modelo de saudação para diferentes cenários, adicionar parâmetros toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="c6c2d-170">Olá exemplo a seguir mostra a saudação parâmetros seção com dois parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="c6c2d-171">Olá primeiro parâmetro `storageSKU` permite que você toospecify o tipo de saudação de redundância.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="c6c2d-172">Ele limita os valores hello que você pode passar de toovalues são válidos para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="c6c2d-173">Ela também especifica um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-173">It also specifies a default value.</span></span> <span data-ttu-id="c6c2d-174">Olá segundo parâmetro `storageNamePrefix` é conjunto tooallow um máximo de 11 caracteres.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="c6c2d-175">Ele especifica um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-175">It specifies a default value.</span></span>

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
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="c6c2d-176">Na seção de variáveis hello, adicione uma variável chamada `storageName`.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="c6c2d-177">Ele combina o valor de prefixo de saudação de parâmetros de saudação e um valor de hash da saudação [uniqueString](resource-group-template-functions-string.md#uniquestring) função.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="c6c2d-178">Ele usa Olá [toLower](resource-group-template-functions-string.md#tolower) função tooconvert toolowercase de todos os caracteres.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="c6c2d-179">toouse esses novos valores para a conta de armazenamento, altere a definição de recurso de saudação:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="c6c2d-180">Observe que Olá nome da conta de armazenamento Olá agora está definido para a variável toohello que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="c6c2d-181">nome da SKU Olá estiver definido como toohello valor do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="c6c2d-182">Olá local é definido Olá mesmo local que o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="c6c2d-183">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-183">Save your file.</span></span> 

<span data-ttu-id="c6c2d-184">Depois de concluir as etapas de saudação neste artigo, seu modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-184">After completing hello steps in this article, your template now looks like:</span></span>

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
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="c6c2d-185">Reimplantar o modelo</span><span class="sxs-lookup"><span data-stu-id="c6c2d-185">Redeploy template</span></span>

<span data-ttu-id="c6c2d-186">Reimplante o modelo de saudação com valores diferentes.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="c6c2d-187">Para o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="c6c2d-188">Para a CLI do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="c6c2d-189">Para Olá Shell de nuvem, carregue o compartilhamento de arquivo do modelo alterado toohello.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="c6c2d-190">Substitua arquivo existente hello.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-190">Overwrite hello existing file.</span></span> <span data-ttu-id="c6c2d-191">Em seguida, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="c6c2d-192">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="c6c2d-192">Clean up resources</span></span>

<span data-ttu-id="c6c2d-193">Quando não é mais necessário, limpe os recursos de saudação implantado excluindo grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6c2d-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="c6c2d-194">Para o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="c6c2d-195">Para a CLI do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="c6c2d-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="c6c2d-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6c2d-196">Next steps</span></span>
* <span data-ttu-id="c6c2d-197">toolearn mais sobre a estrutura de saudação de um modelo, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c6c2d-198">toolearn sobre propriedades de saudação para uma conta de armazenamento, consulte [referência de modelo de contas de armazenamento](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="c6c2d-199">modelos de tooview completa para muitos tipos diferentes de soluções, consulte Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="c6c2d-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
