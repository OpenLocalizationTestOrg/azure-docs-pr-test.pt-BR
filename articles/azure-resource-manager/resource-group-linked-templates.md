---
title: "Vincular modelos para implantação do Azure | Microsoft Docs"
description: "Descreve como usar modelos vinculados em um modelo do Gerenciador de Recursos do Azure para criar uma solução de modelo modular. Mostra como passar valores de parâmetros, especificar um arquivo de parâmetro e URLs criadas dinamicamente."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="adeb3-104">Usando modelos vinculados ao implantar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="adeb3-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="adeb3-105">Em um modelo do Azure Resource Manager, você pode vincular a outro modelo, o que permite decompor sua implantação em um conjunto de modelos orientados para fins específicos.</span><span class="sxs-lookup"><span data-stu-id="adeb3-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="adeb3-106">Assim como com a decomposição de um aplicativo em várias classes de código, a decomposição oferece benefícios em termos de teste, reutilização e legibilidade.</span><span class="sxs-lookup"><span data-stu-id="adeb3-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="adeb3-107">Você pode passar parâmetros de um modelo principal a um modelo vinculado e esses parâmetros podem corresponder diretamente aos parâmetros ou variáveis expostos pelo modelo de chamada.</span><span class="sxs-lookup"><span data-stu-id="adeb3-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="adeb3-108">O modelo vinculado também pode passar uma variável de saída de volta para o modelo de origem, permitindo uma troca de dados bidirecional entre os modelos.</span><span class="sxs-lookup"><span data-stu-id="adeb3-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="adeb3-109">Vinculando a um modelo</span><span class="sxs-lookup"><span data-stu-id="adeb3-109">Linking to a template</span></span>
<span data-ttu-id="adeb3-110">Para criar um vínculo entre dois modelos, adicione um recurso de implantação no modelo principal que aponta para o modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="adeb3-111">Defina a propriedade **templateLink** como o URI do modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="adeb3-112">Você pode fornecer valores de parâmetro para o modelo vinculado diretamente em seu modelo ou em um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="adeb3-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="adeb3-113">O exemplo a seguir usa a propriedade **parameters** para especificar um valor de parâmetro diretamente.</span><span class="sxs-lookup"><span data-stu-id="adeb3-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="adeb3-114">Assim como outros tipos de recurso, você pode definir dependências entre o modelo vinculado e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="adeb3-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="adeb3-115">Portanto, quando outros recursos exigirem um valor de saída do modelo vinculado, você poderá ter certeza de que o modelo vinculado foi implantado antes deles.</span><span class="sxs-lookup"><span data-stu-id="adeb3-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="adeb3-116">Ou, quando o modelo vinculado depender de outros recursos, você poderá verificar se outros recursos foram implantados antes do modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="adeb3-117">Você pode recuperar um valor de um modelo vinculado com a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="adeb3-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="adeb3-118">O serviço do Resource Manager deve ser capaz de acessar o modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="adeb3-119">Você não pode especificar um arquivo local ou um arquivo que esteja disponível apenas em sua rede local para o modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="adeb3-120">Você só pode fornecer um valor de URI que inclua **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="adeb3-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="adeb3-121">Uma opção é colocar o modelo vinculado em uma conta de armazenamento e usar o URI do item, conforme mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="adeb3-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="adeb3-122">Embora o modelo vinculado precise estar disponível externamente, ele não precisa estar disponível para o público.</span><span class="sxs-lookup"><span data-stu-id="adeb3-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="adeb3-123">Você pode adicionar o modelo a uma conta de armazenamento privada que pode ser acessada somente pelo proprietário da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="adeb3-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="adeb3-124">Em seguida, você cria um token SAS (assinatura de acesso compartilhado) para permitir o acesso durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="adeb3-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="adeb3-125">Você pode adicionar esse token SAS ao URI para o modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="adeb3-126">Para ver as etapas para configurar um modelo em uma conta de armazenamento e gerar um token SAS, consulte [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md) ou [Implantar recursos com modelos do Resource Manager e a CLI do Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="adeb3-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="adeb3-127">O exemplo a seguir mostra um modelo pai vinculado a outro modelo.</span><span class="sxs-lookup"><span data-stu-id="adeb3-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="adeb3-128">O modelo vinculado é acessado com um token SAS que é transmitido como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="adeb3-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="adeb3-129">Embora o token seja transmitido como uma cadeia de caracteres segura, o URI do modelo vinculado, incluindo o token SAS, é registrado nas operações de implantação.</span><span class="sxs-lookup"><span data-stu-id="adeb3-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="adeb3-130">Para limitar a exposição, defina uma expiração para o token.</span><span class="sxs-lookup"><span data-stu-id="adeb3-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="adeb3-131">O Resource Manager trata cada modelo vinculado como uma implantação separada.</span><span class="sxs-lookup"><span data-stu-id="adeb3-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="adeb3-132">No histórico de implantações do grupo de recursos, você verá implantações separadas para o modelo pai e os modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="adeb3-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![histórico de implantações](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="adeb3-134">Vinculando a um arquivo de parâmetro</span><span class="sxs-lookup"><span data-stu-id="adeb3-134">Linking to a parameter file</span></span>
<span data-ttu-id="adeb3-135">O exemplo a seguir usa a propriedade **parametersLink** para vincular a um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="adeb3-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="adeb3-136">O valor do URI para o arquivo de parâmetro vinculado não pode ser um arquivo local e deve incluir **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="adeb3-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="adeb3-137">O arquivo de parâmetro também pode ter o acesso limitado por meio de um token SAS.</span><span class="sxs-lookup"><span data-stu-id="adeb3-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="adeb3-138">Usando variáveis para vincular modelos</span><span class="sxs-lookup"><span data-stu-id="adeb3-138">Using variables to link templates</span></span>
<span data-ttu-id="adeb3-139">Os exemplos anteriores mostraram valores codificados de URL para os vínculos de modelo.</span><span class="sxs-lookup"><span data-stu-id="adeb3-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="adeb3-140">Essa abordagem pode funcionar para um modelo simples, mas não funciona bem quando ao trabalhar com um grande conjunto de modelos modulares.</span><span class="sxs-lookup"><span data-stu-id="adeb3-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="adeb3-141">Em vez disso, você pode criar uma variável estática que armazena uma URL de base para o modelo principal e, em seguida, criar dinamicamente URLs para os modelos vinculados dessa URL de base.</span><span class="sxs-lookup"><span data-stu-id="adeb3-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="adeb3-142">A vantagem dessa abordagem é mover ou bifurcar o modelo, pois você precisa alterar a variável estática no modelo principal.</span><span class="sxs-lookup"><span data-stu-id="adeb3-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="adeb3-143">O modelo principal passa os URIs corretos em todo o modelo decomposto.</span><span class="sxs-lookup"><span data-stu-id="adeb3-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="adeb3-144">O exemplo a seguir mostra como usar uma URL base para criar duas URLs para modelos vinculados (**sharedTemplateUrl** e **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="adeb3-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="adeb3-145">Você também pode usar [deployment()](resource-group-template-functions-deployment.md#deployment) para obter a URL base para o modelo atual e usá-lo para obter a URL para outros modelos no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="adeb3-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="adeb3-146">Essa abordagem será útil se o local do modelo é alterado (talvez devido a controle de versão) ou para evitar embutir URLs no arquivo de modelo.</span><span class="sxs-lookup"><span data-stu-id="adeb3-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="adeb3-147">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="adeb3-147">Complete example</span></span>
<span data-ttu-id="adeb3-148">Os exemplos de modelos a seguir mostram uma disposição simplificada de modelos vinculados para ilustrar vários conceitos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="adeb3-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="adeb3-149">Ela pressupõe que os modelos tenham sido adicionados ao mesmo contêiner em uma conta de armazenamento com acesso público desativado.</span><span class="sxs-lookup"><span data-stu-id="adeb3-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="adeb3-150">O modelo vinculado transmite um valor de volta para o modelo principal na seção **outputs** .</span><span class="sxs-lookup"><span data-stu-id="adeb3-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="adeb3-151">O arquivo **parent.json** consiste em:</span><span class="sxs-lookup"><span data-stu-id="adeb3-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="adeb3-152">O arquivo **helloworld.json** consiste em:</span><span class="sxs-lookup"><span data-stu-id="adeb3-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="adeb3-153">No PowerShell, você obtém um token para o contêiner e implanta os modelos com:</span><span class="sxs-lookup"><span data-stu-id="adeb3-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="adeb3-154">Na CLI do Azure 2.0, você obtém um token para o contêiner e implanta os modelos com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="adeb3-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="adeb3-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adeb3-155">Next steps</span></span>
* <span data-ttu-id="adeb3-156">Para saber mais sobre como definir a ordem de implantação para seus recursos, confira [Definição de dependências nos modelos do Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="adeb3-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="adeb3-157">Para saber como definir um recurso, mas criando várias instâncias dele, confira [Criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="adeb3-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

