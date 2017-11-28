---
title: "modelos de aaaLink para implantação do Azure | Microsoft Docs"
description: "Descreve como toouse vinculados modelos em um toocreate de modelo do Azure Resource Manager uma solução de modelo modular. Mostra como os valores de parâmetros toopass, especificar um arquivo de parâmetro e criados dinamicamente as URLs."
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="b43e0-104">Usando modelos vinculados ao implantar os recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="b43e0-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="b43e0-105">De dentro de um modelo do Azure Resource Manager, você pode vincular tooanother modelo, que permite que você toodecompose sua implantação em um conjunto de modelos de destino, a finalidade específica.</span><span class="sxs-lookup"><span data-stu-id="b43e0-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="b43e0-106">Assim como com a decomposição de um aplicativo em várias classes de código, a decomposição oferece benefícios em termos de teste, reutilização e legibilidade.</span><span class="sxs-lookup"><span data-stu-id="b43e0-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="b43e0-107">Você pode passar parâmetros de um modelo vinculado do modelo principal tooa e esses parâmetros diretamente podem mapear tooparameters ou variáveis expostos pelo Olá chamando o modelo.</span><span class="sxs-lookup"><span data-stu-id="b43e0-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="b43e0-108">modelo vinculado Olá também pode passar um modelo de origem da variável toohello back saída, habilitando uma troca de dados bidirecional entre os modelos.</span><span class="sxs-lookup"><span data-stu-id="b43e0-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="b43e0-109">Vinculando tooa modelo</span><span class="sxs-lookup"><span data-stu-id="b43e0-109">Linking tooa template</span></span>
<span data-ttu-id="b43e0-110">Você cria um vínculo entre dois modelos com a adição de um recurso de implantação no modelo principal Olá pontos toohello modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="b43e0-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="b43e0-111">Definir Olá **templateLink** toohello propriedade URI de modelo vinculada hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="b43e0-112">Você pode fornecer valores de parâmetro de modelo vinculada Olá diretamente em seu modelo ou em um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b43e0-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="b43e0-113">Olá, exemplo a seguir usa Olá **parâmetros** propriedade toospecify diretamente um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b43e0-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="b43e0-114">Como outros tipos de recurso, você pode definir dependências entre modelo vinculado hello e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="b43e0-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="b43e0-115">Portanto, quando outros recursos requerem um valor de saída de modelo vinculada hello, você pode fazer se o modelo vinculado Olá foi implantado antes delas.</span><span class="sxs-lookup"><span data-stu-id="b43e0-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="b43e0-116">Ou, quando o modelo vinculado Olá depende de outros recursos, você pode verificar se que outros recursos são implantados antes de modelo vinculada hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="b43e0-117">Você pode recuperar um valor de um modelo vinculado com hello sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="b43e0-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="b43e0-118">Olá serviço Gerenciador de recursos deve ser modelo vinculada do tooaccess capaz de saudação.</span><span class="sxs-lookup"><span data-stu-id="b43e0-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="b43e0-119">Você não pode especificar um arquivo local ou um arquivo que está disponível apenas em sua rede local para o modelo vinculado hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="b43e0-120">Você só pode fornecer um valor de URI que inclua **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="b43e0-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="b43e0-121">Uma opção é tooplace seu modelo vinculado em uma conta de armazenamento e use hello URI para esse item, como mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b43e0-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="b43e0-122">Embora o modelo vinculado Olá deve estar disponível externamente, não precisa toobe toohello disponível público.</span><span class="sxs-lookup"><span data-stu-id="b43e0-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="b43e0-123">Você pode adicionar sua conta de armazenamento particular de tooa de modelo que é proprietário da conta de armazenamento tooonly acessível hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="b43e0-124">Em seguida, você deve criar um acesso de tooenable token de assinatura (SAS) de acesso compartilhado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b43e0-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="b43e0-125">Você adiciona esse toohello token SAS URI para o modelo vinculado hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="b43e0-126">Para ver as etapas para configurar um modelo em uma conta de armazenamento e gerar um token SAS, consulte [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md) ou [Implantar recursos com modelos do Resource Manager e a CLI do Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b43e0-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="b43e0-127">saudação de exemplo a seguir mostra um modelo de pai modelo tooanother links.</span><span class="sxs-lookup"><span data-stu-id="b43e0-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="b43e0-128">modelo vinculado Olá é acessado com um token SAS que é passado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b43e0-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="b43e0-129">Mesmo que o token de saudação é passado como uma cadeia de caracteres segura, hello URI do modelo de saudação vinculado, incluindo o token SAS Olá, é registrado em operações de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b43e0-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="b43e0-130">exposição de toolimit, definir uma expiração de token de saudação.</span><span class="sxs-lookup"><span data-stu-id="b43e0-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="b43e0-131">O Resource Manager trata cada modelo vinculado como uma implantação separada.</span><span class="sxs-lookup"><span data-stu-id="b43e0-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="b43e0-132">Histórico de implantação Olá Olá para grupo de recursos, você verá implantações separadas para pai hello e modelos aninhados.</span><span class="sxs-lookup"><span data-stu-id="b43e0-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![histórico de implantações](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="b43e0-134">Arquivo de parâmetro tooa de vinculação</span><span class="sxs-lookup"><span data-stu-id="b43e0-134">Linking tooa parameter file</span></span>
<span data-ttu-id="b43e0-135">Olá próximo exemplo usa Olá **parametersLink** arquivo de parâmetro propriedade toolink tooa.</span><span class="sxs-lookup"><span data-stu-id="b43e0-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="b43e0-136">Olá URI valor Olá parâmetro vinculado arquivo não pode ser um arquivo local e deve incluir **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="b43e0-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="b43e0-137">arquivo de parâmetro Hello também pode ser limitado tooaccess por meio de um token SAS.</span><span class="sxs-lookup"><span data-stu-id="b43e0-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="b43e0-138">Usando variáveis toolink modelos</span><span class="sxs-lookup"><span data-stu-id="b43e0-138">Using variables toolink templates</span></span>
<span data-ttu-id="b43e0-139">exemplos anteriores Olá mostraram valores codificados de URL para links de modelo hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="b43e0-140">Essa abordagem pode funcionar para um modelo simples, mas não funciona bem quando ao trabalhar com um grande conjunto de modelos modulares.</span><span class="sxs-lookup"><span data-stu-id="b43e0-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="b43e0-141">Em vez disso, você pode criar uma variável estática que armazena uma URL base para o modelo principal hello e, em seguida, criar dinamicamente URLs para modelos de saudação vinculado dessa URL base.</span><span class="sxs-lookup"><span data-stu-id="b43e0-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="b43e0-142">benefício de saudação dessa abordagem é, você pode facilmente mover ou bifurcação de modelo de saudação porque você só precisa de variável estática do toochange Olá no modelo principal hello.</span><span class="sxs-lookup"><span data-stu-id="b43e0-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="b43e0-143">modelo principal Olá passa Olá correto de que URIs em toda a saudação decomposto modelo.</span><span class="sxs-lookup"><span data-stu-id="b43e0-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="b43e0-144">Olá exemplo a seguir mostra como toouse uma toocreate URL base duas URLs para vinculam modelos (**sharedTemplateUrl** e **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="b43e0-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="b43e0-145">Você também pode usar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Olá URL base para o modelo atual hello e usar essa URL de saudação do tooget para outros modelos de saudação mesmo local.</span><span class="sxs-lookup"><span data-stu-id="b43e0-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="b43e0-146">Essa abordagem é útil se o local do modelo for alterado (talvez devido tooversioning) ou deseja tooavoid rígido URLs no arquivo de modelo de saudação de codificação.</span><span class="sxs-lookup"><span data-stu-id="b43e0-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="b43e0-147">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="b43e0-147">Complete example</span></span>
<span data-ttu-id="b43e0-148">Olá modelos de exemplo a seguir mostra uma organização simplificada de modelos vinculados tooillustrate vários conceitos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b43e0-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="b43e0-149">Ele pressupõe que foram adicionados modelos Olá toohello mesmo contêiner em uma conta de armazenamento com acesso público desativado.</span><span class="sxs-lookup"><span data-stu-id="b43e0-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="b43e0-150">modelo vinculado Olá passa um modelo principal do valor toohello back Olá **gera** seção.</span><span class="sxs-lookup"><span data-stu-id="b43e0-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="b43e0-151">Olá **parent.json** arquivo consiste em:</span><span class="sxs-lookup"><span data-stu-id="b43e0-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="b43e0-152">Olá **helloworld.json** arquivo consiste em:</span><span class="sxs-lookup"><span data-stu-id="b43e0-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="b43e0-153">No PowerShell, obter um token para o contêiner de saudação e implantar modelos de saudação com:</span><span class="sxs-lookup"><span data-stu-id="b43e0-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="b43e0-154">No 2.0 do CLI do Azure, obter um token para o contêiner de saudação e implantar modelos de saudação com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b43e0-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b43e0-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b43e0-155">Next steps</span></span>
* <span data-ttu-id="b43e0-156">toolearn sobre Olá definindo a ordem de implantação Olá para seus recursos, consulte [definem as dependências em modelos do Gerenciador de recursos do Azure](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="b43e0-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="b43e0-157">toolearn como um recurso de toodefine mas criar muitas instâncias do mesmo, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="b43e0-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

