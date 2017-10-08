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
# <a name="publish-a-managed-application-for-internal-consumption"></a>Publicar um aplicativo gerenciado para consumo interno

Crie e publique [aplicativos gerenciados](managed-application-overview.md) do Azure destinados aos membros de sua organização. Por exemplo, um departamento de TI pode publicar aplicativos gerenciados que garantem a conformidade com os padrões organizacionais. Esses aplicativos gerenciados estão disponíveis por meio do catálogo de serviços hello, hello Azure Marketplace.

toopublish um aplicativo gerenciado para o catálogo de serviços hello, faça o seguinte:

* Crie um pacote. zip que contém três arquivos de modelo hello.
* Decida qual usuário, grupo ou aplicativo precisa acessar toohello o grupo de recursos na assinatura saudação do usuário.
* Crie definição de aplicativo hello gerenciado que pontos de pacote do toohello. zip e solicitações de acesso para a identidade de saudação.

## <a name="create-a-managed-application-package"></a>Criar um pacote de aplicativos gerenciados

Olá primeira etapa é arquivos de modelo necessárias três toocreate hello. Todos os três arquivos de pacote em um arquivo. zip e carregá-lo em local acessível tooan, como uma conta de armazenamento. Você passa um arquivo. zip do link toothis quando Olá criando gerenciado a definição do aplicativo.

* **applianceMainTemplate.json**: este arquivo define hello Azure aplicativo os recursos que são provisionados como parte da saudação gerenciados. modelo de saudação não é diferente de um modelo regular do Gerenciador de recursos. Por exemplo, toocreate uma conta de armazenamento por meio de um aplicativo gerenciado, applianceMainTemplate.json contém:

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

* **mainTemplate.json**: os usuários implantar este modelo quando criar hello aplicativo gerenciado. Ele define o recurso de aplicativo hello gerenciado, que é um tipo de recurso Microsoft.Solutions/appliances. Esse arquivo contém todos os parâmetros de saudação que é necessário para recursos de saudação em applianceMainTemplate.json.

  Defina duas propriedades importantes nesse modelo. Primeiro, Olá **applianceDefinitionId** propriedade é ID Olá Olá gerenciado da definição do aplicativo. Você cria a definição de saudação neste tópico. Ao definir esse valor, você deve decidir qual assinatura e toouse do grupo de recursos para armazenar Olá definições de aplicativo gerenciado. E, você deve decidir sobre um nome para a definição de saudação. Olá ID está no formato de saudação:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  Em segundo lugar, Olá **managedResourceGroupId** propriedade é a ID de Olá Olá do grupo de recursos onde hello recursos do Azure são criados. Você pode atribuir um valor para esse nome de grupo de recursos ou permitir que o usuário Olá forneça um nome. formato Olá Olá ID é:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  saudação de exemplo a seguir mostra um arquivo mainTemplate.json. Especifica um grupo de recursos para recursos de saudação implantado. Olá, ID de definição é toouse de conjunto nomeada de uma definição de **storageApp** em um grupo de recursos denominado **managedApplicationGroup**. Você pode alterar esses nomes diferentes de toouse de valores. Fornecer sua própria ID de assinatura na ID de definição de saudação.

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

* **applianceCreateUiDefinition.json**: hello portal do Azure usa esse arquivo toogenerate Olá interface do usuário para os usuários que criam Olá aplicativo gerenciado. Você define como os usuários fornecem a entrada para cada parâmetro. Você pode usar opções como uma lista suspensa, caixa de texto, caixa de senha e outras ferramentas de entrada. toolearn como toocreate um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Olá, exemplo a seguir mostra um arquivo applianceCreateUiDefinition.json que permite que os usuários toospecify Olá armazenamento conta prefixo de nome por meio de uma caixa de texto.

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

Depois que todos os arquivos de saudação necessário estiverem prontos, empacotá-las como um arquivo. zip. Olá três arquivos deverão estar no nível de raiz de saudação do arquivo. zip de saudação. Se você pode colocá-los em uma pasta, você recebe um erro quando criando Olá gerenciado a definição de aplicativo que declara Olá necessários arquivos não estão presentes. Carregar um local acessível de tooan do pacote de saudação de onde eles podem ser consumidos. Olá restante deste artigo presume que o arquivo. zip de saudação existe em um contêiner de blob de armazenamento acessíveis publicamente.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Criar um grupo de usuários ou aplicativo do Azure Active Directory

Olá segunda etapa é tooselect um grupo de usuários ou aplicativos para gerenciamento de recursos de saudação em nome do cliente hello. Este grupo de usuário ou aplicativo tem permissões no hello recurso gerenciado grupo acordo toohello função atribuída. função Hello pode ser qualquer função interna de controle de acesso baseado em função (RBAC) como o proprietário ou colaborador. Você também pode dar a um usuário individual recursos de saudação do toomanage de permissão, mas normalmente você atribuir a esse grupo de usuário permissão tooa. toocreate um novo grupo de usuários do Active Directory, consulte [criar um grupo e adicionar membros no Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

É necessário ID de objeto de saudação do hello toouse de grupo de usuário para gerenciar recursos de saudação. saudação de exemplo a seguir mostra como tooget Olá ID de objeto do nome de exibição do grupo hello:

```azurecli-interactive
az ad group show --group exampleGroupName
```

o comando de exemplo Hello retorna Olá saída a seguir:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

ID do objeto tooretrieve Olá apenas, use:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Obter ID de definição de função hello

Em seguida, você precisa Olá ID de definição da função de saudação função interna RBAC, você deseja toogrant toohello usuário, grupo de usuário ou aplicativo. Normalmente, você usa Olá proprietário ou colaborador ou o leitor de função. saudação de comando a seguir mostra como tooget Olá ID de definição de função para a função de proprietário de saudação:


```azurecli-interactive
az role definition list --name owner
```

Esse comando retorna Olá saída a seguir:

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

É necessário um valor Olá Olá "" da propriedade de nome de saudação anterior exemplo. Recupere apenas essa propriedade com:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Criar definição de aplicativo hello gerenciado

Se você ainda não tiver um grupo de recursos para armazenar a definição de aplicativo gerenciado, crie um agora:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Agora, crie o recurso de definição de aplicativo hello gerenciado.

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

Olá parâmetros usados em Olá anterior exemplo são:

* **grupo de recursos**: nome Olá Olá do grupo de recursos onde Olá gerenciada a definição de aplicativo é criado.
* **nível de bloqueio**: tipo de saudação do bloqueio colocado no grupo de recurso gerenciado Olá. Ela impede que o cliente Olá operações indesejáveis no grupo de recursos. Atualmente, somente leitura é Olá só tem suporte a nível de bloqueio. Quando somente leitura é especificada, cliente Olá somente pode ler recursos de Olá presentes no grupo de recurso gerenciado hello.
* **autorizações**: descreve ID principal hello e ID de definição de função hello toogrant usado permissão toohello recurso gerenciado grupo. Ele é especificado no formato de saudação do `<principalId>:<roleDefinitionId>`. Vários valores também podem ser especificados para essa propriedade. Se houver necessidade de vários valores, deve ser especificados no formulário de saudação `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Vários valores são separados por um espaço.
* **uri do arquivo de pacote**: Olá local do pacote de aplicativo gerenciado Olá que contém os arquivos de modelo de saudação, que podem ser um blob de armazenamento do Azure.

## <a name="next-steps"></a>Próximas etapas

* Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).
* Para obter exemplos de arquivos hello, consulte [gerenciados exemplos de aplicativo](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).
* Para obter informações sobre publicação toohello de aplicativos gerenciados do Azure Marketplace, consulte [Azure gerenciados aplicativos Olá Marketplace](managed-application-author-marketplace.md).
* Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).
* toolearn como toocreate um arquivo de definição de interface do usuário para um aplicativo gerenciado, consulte [Introdução ao CreateUiDefinition](managed-application-createuidefinition-overview.md).
