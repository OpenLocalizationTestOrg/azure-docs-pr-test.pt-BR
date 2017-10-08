---
title: segredo do cofre aaaKey com o modelo do Gerenciador de recursos | Microsoft Docs
description: "Mostra como toopass um segredo de uma chave de cofre como um parâmetro durante a implantação."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Use o valor de parâmetro secure toopass Cofre de chaves durante a implantação

Quando você precisar toopass um valor seguro (como uma senha) como um parâmetro durante a implantação, você pode recuperar o valor de saudação de um [Azure Key Vault](../key-vault/key-vault-whatis.md). Recuperar o valor de saudação referenciando o Cofre de chaves de saudação e segredo no seu arquivo de parâmetro. valor de saudação nunca é exposta pois referência apenas a sua ID de Cofre de chaves. Você não precisa toomanually Inserir valor Olá para segredo Olá cada vez que você implanta recursos de saudação. Cofre de chaves Olá pode existir em uma assinatura diferente que o grupo de recursos de saudação que você está implantando. Ao referenciar o Cofre de chaves hello, você incluir Olá ID da assinatura.

Ao criar o Cofre de chaves hello, defina Olá *enabledForTemplateDeployment* propriedade muito*true*. Definindo tootrue esse valor, é possível permitir acesso de modelos do Gerenciador de recursos durante a implantação.  

## <a name="deploy-a-key-vault-and-secret"></a>Implantar um cofre da chave e segredo

toocreate um cofre de chaves e o segredo, use a CLI do Azure ou o PowerShell. Observe que esse Cofre de chaves hello está habilitado para implantação de modelo. 

Para a CLI do Azure, use:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Para o PowerShell, use:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Habilitar o segredo de toohello de acesso

Se você estiver usando um cofre de chaves novo ou existente, certifique-se de usuário Olá implantar modelo Olá pode acessar o segredo Olá. usuário Olá Implantando um modelo que faz referência a um segredo deve ter Olá `Microsoft.KeyVault/vaults/deploy/action` permissão para o Cofre de chaves hello. Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) e [Colaborador](../active-directory/role-based-access-built-in-roles.md#contributor) ambas as funções concedem esse acesso. Você também pode criar um [função personalizada](../active-directory/role-based-access-control-custom-roles.md) que concede essa permissão e adicione a função de toothat usuário hello. Para obter informações sobre como adicionar uma função de usuário tooa, consulte [atribuir um usuário tooadministrator funções no Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Fazer referência a um segredo com ID estática

modelo de saudação que recebe um segredo do Cofre de chaves é como qualquer outro modelo. Isso ocorre porque **você referenciar o cofre da chave no arquivo de parâmetro hello, não o modelo Olá Olá.** Por exemplo, a saudação modelo a seguir implanta um banco de dados SQL que inclui uma senha de administrador. o parâmetro de senha Olá é definido tooa cadeia de caracteres segura. Mas, Olá não especificar onde vem esse valor.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Agora, crie um arquivo de parâmetro hello precede o modelo. No arquivo de parâmetro hello, especifique um parâmetro que corresponda Olá nome do parâmetro hello no modelo de saudação. Valor de parâmetro hello, referência Olá segredo do Cofre de chave hello. Você pode referenciar segredo Olá passando o identificador de recurso de saudação do Cofre de chaves de saudação e o nome de saudação do segredo hello. Em Olá exemplo a seguir, segredo do Cofre de chaves Olá já deve existir e você fornecer um valor estático para sua ID de recurso.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Fazer referência a um segredo com ID dinâmica

seção anterior Olá mostrou como toopass uma ID de recurso estático para a chave de saudação cofre segredo. No entanto, em alguns cenários, é necessário tooreference um segredo do Cofre de chaves que varia com base na implantação atual hello. Nesse caso, você não pode codificar Olá ID de recurso no arquivo de parâmetros de saudação. Infelizmente, você não é possível gerar dinamicamente Olá ID de recurso no arquivo de parâmetros de saudação porque expressões de modelo não são permitidas no arquivo de parâmetros de saudação.

toodynamically gerar ID de recurso de saudação de um segredo do Cofre de chaves, você deve mover o recurso de saudação que precisa segredo Olá em um modelo aninhado. No modelo mestre, você pode adicionar modelo aninhado hello e passa um parâmetro que contém a ID de recurso Olá gerado dinamicamente.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter informações gerais sobre cofres de chaves, veja [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md).
* Para obter exemplos completos de referência de segredos de chave, veja [Exemplos do cofre da chave](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

