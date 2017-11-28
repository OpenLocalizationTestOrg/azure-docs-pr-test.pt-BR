---
title: "aaaCreate e publicar um aplicativo gerenciado do catálogo de serviço do Azure | Microsoft Docs"
description: "Mostra como toocreate do Azure gerenciados aplicativo destina-se a membros de sua organização."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="3e1f3-103">Publicar um aplicativo gerenciado para consumo interno</span><span class="sxs-lookup"><span data-stu-id="3e1f3-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="3e1f3-104">Crie e publique [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="3e1f3-105">Por exemplo, um departamento de TI pode publicar aplicativos gerenciados que garantem a conformidade com os padrões organizacionais.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="3e1f3-106">Esses aplicativos gerenciados estão disponíveis por meio do catálogo de serviços hello, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="3e1f3-107">toopublish um aplicativo gerenciado para o catálogo de serviços hello, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="3e1f3-108">Crie um pacote. zip que contém três arquivos de modelo hello.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="3e1f3-109">Decida qual usuário, grupo ou aplicativo precisa acessar toohello o grupo de recursos na assinatura saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="3e1f3-110">Crie definição de aplicativo hello gerenciado que pontos de pacote do toohello. zip e solicitações de acesso para a identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="3e1f3-111">Criar um pacote de aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="3e1f3-111">Create a managed application package</span></span>

<span data-ttu-id="3e1f3-112">Olá primeira etapa é arquivos de modelo necessárias três toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="3e1f3-113">Todos os três arquivos de pacote em um arquivo. zip e carregá-lo em local acessível tooan, como uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="3e1f3-114">Você passa um arquivo. zip do link toothis quando Olá criando gerenciado a definição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="3e1f3-115">**applianceMainTemplate.json**: este arquivo define hello Azure aplicativo os recursos que são provisionados como parte da saudação gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="3e1f3-116">modelo de saudação não é diferente de um modelo regular do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="3e1f3-117">Por exemplo, toocreate uma conta de armazenamento por meio de um aplicativo gerenciado, applianceMainTemplate.json contém:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="3e1f3-118">**mainTemplate.json**: os usuários implantar este modelo quando criar hello aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="3e1f3-119">Ele define o recurso de aplicativo hello gerenciado, que é um tipo de recurso Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="3e1f3-120">Esse arquivo contém todos os parâmetros de saudação que é necessário para recursos de saudação em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="3e1f3-121">Defina duas propriedades importantes nesse modelo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-121">You set two important properties in this template.</span></span> <span data-ttu-id="3e1f3-122">Primeiro, Olá **applianceDefinitionId** propriedade é ID Olá Olá gerenciado da definição do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="3e1f3-123">Você cria a definição de saudação neste tópico.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="3e1f3-124">Ao definir esse valor, você deve decidir qual assinatura e toouse do grupo de recursos para armazenar Olá definições de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="3e1f3-125">E, você deve decidir sobre um nome para a definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="3e1f3-126">Olá ID está no formato de saudação:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="3e1f3-127">Em segundo lugar, Olá **managedResourceGroupId** propriedade é a ID de Olá Olá do grupo de recursos onde hello recursos do Azure são criados.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="3e1f3-128">Você pode atribuir um valor para esse nome de grupo de recursos ou permitir que o usuário Olá forneça um nome.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="3e1f3-129">formato Olá Olá ID é:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="3e1f3-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="3e1f3-131">saudação de exemplo a seguir mostra um arquivo mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="3e1f3-132">Especifica um grupo de recursos para recursos de saudação implantado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="3e1f3-133">Olá, ID de definição é toouse de conjunto nomeada de uma definição de **storageApp** em um grupo de recursos denominado **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="3e1f3-134">Você pode alterar esses nomes diferentes de toouse de valores.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-134">You can change these values toouse different names.</span></span> <span data-ttu-id="3e1f3-135">Fornecer sua própria ID de assinatura na ID de definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-135">Provide your own subscription ID in hello definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="3e1f3-136">**applianceCreateUiDefinition.json**: hello portal do Azure usa esse arquivo toogenerate Olá interface do usuário para os usuários que criam Olá aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="3e1f3-137">Você define como os usuários fornecem a entrada para cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="3e1f3-138">Você pode usar opções como uma lista suspensa, caixa de texto, caixa de senha e outras ferramentas de entrada.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="3e1f3-139">toolearn como toocreate um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="3e1f3-140">Olá, exemplo a seguir mostra um arquivo applianceCreateUiDefinition.json que permite que os usuários toospecify Olá armazenamento conta prefixo de nome por meio de uma caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="3e1f3-141">Depois que todos os arquivos de saudação necessário estiverem prontos, empacotá-las como um arquivo. zip.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="3e1f3-142">Olá três arquivos deverão estar no nível de raiz de saudação do arquivo. zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="3e1f3-143">Se você pode colocá-los em uma pasta, você recebe um erro quando criando Olá gerenciado a definição de aplicativo que declara Olá necessários arquivos não estão presentes.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="3e1f3-144">Carregar um local acessível de tooan do pacote de saudação de onde eles podem ser consumidos.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="3e1f3-145">Olá restante deste artigo presume que o arquivo. zip de saudação existe em um contêiner de blob de armazenamento acessíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="3e1f3-146">Criar um grupo de usuários ou aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e1f3-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="3e1f3-147">Olá segunda etapa é tooselect um grupo de usuários ou aplicativos para gerenciamento de recursos de saudação em nome do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="3e1f3-148">Este grupo de usuário ou aplicativo tem permissões no hello recurso gerenciado grupo acordo toohello função atribuída.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="3e1f3-149">função Hello pode ser qualquer função interna de controle de acesso baseado em função (RBAC) como o proprietário ou colaborador.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="3e1f3-150">Você também pode dar a um usuário individual recursos de saudação do toomanage de permissão, mas normalmente você atribuir a esse grupo de usuário permissão tooa.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="3e1f3-151">toocreate um novo grupo de usuários do Active Directory, consulte [criar um grupo e adicionar membros no Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="3e1f3-152">É necessário ID de objeto de saudação do hello toouse de grupo de usuário para gerenciar recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="3e1f3-153">saudação de exemplo a seguir mostra como tooget Olá ID de objeto do nome de exibição do grupo hello:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="3e1f3-154">o comando de exemplo Hello retorna Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="3e1f3-155">ID do objeto tooretrieve Olá apenas, use:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="3e1f3-156">Obter ID de definição de função hello</span><span class="sxs-lookup"><span data-stu-id="3e1f3-156">Get hello role definition ID</span></span>

<span data-ttu-id="3e1f3-157">Em seguida, você precisa Olá ID de definição da função de saudação função interna RBAC, você deseja toogrant toohello usuário, grupo de usuário ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="3e1f3-158">Normalmente, você usa Olá proprietário ou colaborador ou o leitor de função.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="3e1f3-159">saudação de comando a seguir mostra como tooget Olá ID de definição de função para a função de proprietário de saudação:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="3e1f3-160">Esse comando retorna Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="3e1f3-161">É necessário um valor Olá Olá "" da propriedade de nome de saudação anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="3e1f3-162">Recupere apenas essa propriedade com:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="3e1f3-163">Criar definição de aplicativo hello gerenciado</span><span class="sxs-lookup"><span data-stu-id="3e1f3-163">Create hello managed application definition</span></span>

<span data-ttu-id="3e1f3-164">Se você ainda não tiver um grupo de recursos para armazenar a definição de aplicativo gerenciado, crie um agora:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="3e1f3-165">Agora, crie o recurso de definição de aplicativo hello gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-165">Now, create hello managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="3e1f3-166">Olá parâmetros usados em Olá anterior exemplo são:</span><span class="sxs-lookup"><span data-stu-id="3e1f3-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="3e1f3-167">**grupo de recursos**: nome Olá Olá do grupo de recursos onde Olá gerenciada a definição de aplicativo é criado.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="3e1f3-168">**nível de bloqueio**: tipo de saudação do bloqueio colocado no grupo de recurso gerenciado Olá.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="3e1f3-169">Ela impede que o cliente Olá operações indesejáveis no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="3e1f3-170">Atualmente, somente leitura é Olá só tem suporte a nível de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="3e1f3-171">Quando somente leitura é especificada, cliente Olá somente pode ler recursos de Olá presentes no grupo de recurso gerenciado hello.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="3e1f3-172">**autorizações**: descreve ID principal hello e ID de definição de função hello toogrant usado permissão toohello recurso gerenciado grupo.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="3e1f3-173">Ele é especificado no formato de saudação do `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="3e1f3-174">Vários valores também podem ser especificados para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="3e1f3-175">Se houver necessidade de vários valores, deve ser especificados no formulário de saudação `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="3e1f3-176">Vários valores são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="3e1f3-177">**uri do arquivo de pacote**: Olá local do pacote de aplicativo gerenciado Olá que contém os arquivos de modelo de saudação, que podem ser um blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1f3-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e1f3-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e1f3-178">Next steps</span></span>

* <span data-ttu-id="3e1f3-179">Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3e1f3-180">Para obter exemplos de arquivos hello, consulte [gerenciados exemplos de aplicativo](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="3e1f3-181">Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="3e1f3-182">Para obter informações sobre publicação toohello de aplicativos gerenciados do Azure Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="3e1f3-183">Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="3e1f3-184">toolearn como toocreate um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e1f3-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
