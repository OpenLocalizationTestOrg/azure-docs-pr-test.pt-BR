---
title: "Criar e publicar um aplicativo gerenciado do catálogo de serviços do Azure | Microsoft Docs"
description: "Mostra como criar um aplicativo gerenciado do Azure destinado aos membros de sua organização."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="c65be-103">Publicar um aplicativo gerenciado para consumo interno</span><span class="sxs-lookup"><span data-stu-id="c65be-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="c65be-104">Crie e publique [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização.</span><span class="sxs-lookup"><span data-stu-id="c65be-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="c65be-105">Por exemplo, um departamento de TI pode publicar aplicativos gerenciados que garantem a conformidade com os padrões organizacionais.</span><span class="sxs-lookup"><span data-stu-id="c65be-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="c65be-106">Esses aplicativos gerenciados estão disponíveis por meio do catálogo de serviços, não pelo Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c65be-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="c65be-107">Para publicar um aplicativo gerenciado do catálogo de serviços, você deve:</span><span class="sxs-lookup"><span data-stu-id="c65be-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="c65be-108">Criar um pacote .zip que contém os três arquivos de modelo necessários.</span><span class="sxs-lookup"><span data-stu-id="c65be-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="c65be-109">Decidir qual usuário, grupo ou aplicativo precisa de acesso ao grupo de recursos na assinatura do usuário.</span><span class="sxs-lookup"><span data-stu-id="c65be-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="c65be-110">Criar a definição de aplicativo gerenciado que aponta para o pacote .zip e solicita o acesso à identidade.</span><span class="sxs-lookup"><span data-stu-id="c65be-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="c65be-111">Criar um pacote de aplicativos gerenciados</span><span class="sxs-lookup"><span data-stu-id="c65be-111">Create a managed application package</span></span>

<span data-ttu-id="c65be-112">A primeira etapa é criar os três arquivos de modelo necessários.</span><span class="sxs-lookup"><span data-stu-id="c65be-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="c65be-113">Empacote todos os três arquivos em um arquivo .zip e carregue-o em um local acessível, como uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c65be-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="c65be-114">Passe um link para esse arquivo .zip ao criar a definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="c65be-115">**applianceMainTemplate.json**: esse arquivo define os recursos do Azure que são provisionados como parte do aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="c65be-116">O modelo não é diferente de um modelo normal do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c65be-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="c65be-117">Por exemplo, para criar uma conta de armazenamento por meio de um aplicativo gerenciado, o applianceMainTemplate.json contém:</span><span class="sxs-lookup"><span data-stu-id="c65be-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="c65be-118">**mainTemplate.json**: os usuários implantam esse modelo ao criar o aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="c65be-119">Ele define o recurso de aplicativo gerenciado, que é um tipo de recurso Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="c65be-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="c65be-120">Esse arquivo contém todos os parâmetros necessários para os recursos em applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="c65be-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="c65be-121">Defina duas propriedades importantes nesse modelo.</span><span class="sxs-lookup"><span data-stu-id="c65be-121">You set two important properties in this template.</span></span> <span data-ttu-id="c65be-122">Primeiro, a propriedade **applianceDefinitionId** é a ID de definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="c65be-123">A definição é criada mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="c65be-123">You create the definition later in this topic.</span></span> <span data-ttu-id="c65be-124">Ao definir esse valor, você deve decidir qual assinatura e grupo de recursos serão usados para armazenar as definições de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="c65be-125">Além disso, você deve escolher um nome para a definição.</span><span class="sxs-lookup"><span data-stu-id="c65be-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="c65be-126">A ID está no formato:</span><span class="sxs-lookup"><span data-stu-id="c65be-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="c65be-127">Em segundo lugar, a propriedade **managedResourceGroupId** é a ID do grupo de recursos no qual os recursos do Azure são criados.</span><span class="sxs-lookup"><span data-stu-id="c65be-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="c65be-128">Atribua um valor a esse nome de grupo de recursos ou permita que o usuário forneça um nome.</span><span class="sxs-lookup"><span data-stu-id="c65be-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="c65be-129">O formato da ID é:</span><span class="sxs-lookup"><span data-stu-id="c65be-129">The format of the ID is:</span></span>

  <span data-ttu-id="c65be-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="c65be-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="c65be-131">O exemplo a seguir mostra um arquivo mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="c65be-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="c65be-132">Ele especifica um grupo de recursos para os recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="c65be-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="c65be-133">A ID de definição está definida para usar uma definição chamada **storageApp** em um grupo de recursos chamado **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="c65be-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="c65be-134">Você pode alterar esses valores para usar nomes diferentes.</span><span class="sxs-lookup"><span data-stu-id="c65be-134">You can change these values to use different names.</span></span> <span data-ttu-id="c65be-135">Forneça sua própria ID de assinatura na ID de definição.</span><span class="sxs-lookup"><span data-stu-id="c65be-135">Provide your own subscription ID in the definition ID.</span></span>

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

* <span data-ttu-id="c65be-136">**applianceCreateUiDefinition.json**: o portal do Azure usa esse arquivo para gerar a interface do usuário para os usuários que criam o aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="c65be-137">Você define como os usuários fornecem a entrada para cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c65be-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="c65be-138">Você pode usar opções como uma lista suspensa, caixa de texto, caixa de senha e outras ferramentas de entrada.</span><span class="sxs-lookup"><span data-stu-id="c65be-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="c65be-139">Para saber como criar um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="c65be-140">O exemplo a seguir mostra um arquivo applianceCreateUiDefinition.json que permite aos usuários especificar o prefixo de nome da conta de armazenamento por meio de uma caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c65be-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
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

<span data-ttu-id="c65be-141">Depois que todos os arquivos necessários estiverem prontos, empacote-os como um arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="c65be-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="c65be-142">Os três arquivos devem estar no nível raiz do arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="c65be-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="c65be-143">Se você colocá-los em uma pasta, receberá um erro ao criar a definição de aplicativo gerenciado que indica que os arquivos necessários não estão presentes.</span><span class="sxs-lookup"><span data-stu-id="c65be-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="c65be-144">Carregue o pacote em um local acessível no qual ele pode ser consumido.</span><span class="sxs-lookup"><span data-stu-id="c65be-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="c65be-145">O restante deste artigo pressupõe que o arquivo .zip exista em um contêiner de blobs de armazenamento publicamente acessível.</span><span class="sxs-lookup"><span data-stu-id="c65be-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="c65be-146">Criar um grupo de usuários ou aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c65be-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="c65be-147">A segunda etapa é selecionar um grupo de usuários ou um aplicativo para gerenciar os recursos em nome do cliente.</span><span class="sxs-lookup"><span data-stu-id="c65be-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="c65be-148">Esse grupo de usuários ou aplicativo tem permissões no grupo de recursos gerenciados de acordo com a função atribuída.</span><span class="sxs-lookup"><span data-stu-id="c65be-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="c65be-149">A função pode ser qualquer função interna de RBAC (Controle de acesso baseado em função) como Proprietário ou Colaborador.</span><span class="sxs-lookup"><span data-stu-id="c65be-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="c65be-150">Também é possível conceder a um usuário individual permissões para gerenciar os recursos, mas, normalmente, você atribui essa permissão a um grupo de usuários.</span><span class="sxs-lookup"><span data-stu-id="c65be-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="c65be-151">Para criar um novo grupo de usuários do Active Directory, consulte [Criar um grupo e adicionar membros no Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="c65be-152">É necessário usar a ID de objeto do grupo de usuários para gerenciar os recursos.</span><span class="sxs-lookup"><span data-stu-id="c65be-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="c65be-153">O seguinte exemplo mostra como obter a ID de objeto do nome de exibição do grupo:</span><span class="sxs-lookup"><span data-stu-id="c65be-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="c65be-154">O comando de exemplo retorna a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="c65be-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="c65be-155">Para recuperar apenas a ID de objeto, use:</span><span class="sxs-lookup"><span data-stu-id="c65be-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="c65be-156">Obter a ID de definição da função</span><span class="sxs-lookup"><span data-stu-id="c65be-156">Get the role definition ID</span></span>

<span data-ttu-id="c65be-157">Em seguida, é necessário o ID de definição de função da função RBAC interna para conceder acesso ao usuário, grupo de usuários ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c65be-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="c65be-158">Normalmente, você usa a função Proprietário, Colaborador ou Leitor.</span><span class="sxs-lookup"><span data-stu-id="c65be-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="c65be-159">O comando a seguir mostra como obter a ID de definição de função para a função Proprietário:</span><span class="sxs-lookup"><span data-stu-id="c65be-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="c65be-160">O comando retorna a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="c65be-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
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

<span data-ttu-id="c65be-161">Você precisa do valor da propriedade "name" do exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="c65be-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="c65be-162">Recupere apenas essa propriedade com:</span><span class="sxs-lookup"><span data-stu-id="c65be-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="c65be-163">Criar a definição de aplicativo gerenciado</span><span class="sxs-lookup"><span data-stu-id="c65be-163">Create the managed application definition</span></span>

<span data-ttu-id="c65be-164">Se você ainda não tiver um grupo de recursos para armazenar a definição de aplicativo gerenciado, crie um agora:</span><span class="sxs-lookup"><span data-stu-id="c65be-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="c65be-165">Agora, crie o recurso de definição de aplicativo gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-165">Now, create the managed application definition resource.</span></span>

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

<span data-ttu-id="c65be-166">Os parâmetros usados no exemplo anterior são:</span><span class="sxs-lookup"><span data-stu-id="c65be-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="c65be-167">**resource-group**: o nome do grupo de recursos no qual a definição de aplicativo gerenciado é criada.</span><span class="sxs-lookup"><span data-stu-id="c65be-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="c65be-168">**lock-level**: o tipo de bloqueio colocado no grupo de recursos gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="c65be-169">Ela impede que o cliente execute operações indesejáveis no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c65be-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="c65be-170">Atualmente, ReadOnly é o único nível de bloqueio com suporte.</span><span class="sxs-lookup"><span data-stu-id="c65be-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="c65be-171">Quando ReadOnly é especificado, o cliente pode ler somente os recursos presentes no grupo de recursos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c65be-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="c65be-172">**authorizations**: descreve a ID da entidade e a ID de definição de função que são usadas para conceder permissão ao grupo de recursos gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c65be-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="c65be-173">Ele é especificado no formato `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="c65be-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="c65be-174">Vários valores também podem ser especificados para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="c65be-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="c65be-175">Se houver a necessidade de vários valores, eles deverão ser especificados no formulário `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="c65be-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="c65be-176">Vários valores são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="c65be-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="c65be-177">**package-file-uri**: o local do pacote de aplicativos gerenciados que contém os arquivos de modelo, que podem ser um Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="c65be-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c65be-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c65be-178">Next steps</span></span>

* <span data-ttu-id="c65be-179">Para obter uma introdução aos aplicativos gerenciados, consulte [Visão geral de aplicativos gerenciados](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c65be-180">Para obter exemplos dos arquivos, consulte [Exemplos de aplicativo gerenciado](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="c65be-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="c65be-181">Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="c65be-182">Para obter informações sobre como publicar aplicativos gerenciados para o Azure Marketplace, consulte [Aplicativos gerenciados do Azure no Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="c65be-183">Para obter informações sobre como consumir um aplicativo gerenciado do Marketplace, consulte [Consumir aplicativos gerenciados pelo Azure no Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="c65be-184">Para saber como criar um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c65be-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
