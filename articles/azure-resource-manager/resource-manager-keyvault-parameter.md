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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="e9f81-103">Use o valor de parâmetro secure toopass Cofre de chaves durante a implantação</span><span class="sxs-lookup"><span data-stu-id="e9f81-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="e9f81-104">Quando você precisar toopass um valor seguro (como uma senha) como um parâmetro durante a implantação, você pode recuperar o valor de saudação de um [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9f81-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="e9f81-105">Recuperar o valor de saudação referenciando o Cofre de chaves de saudação e segredo no seu arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e9f81-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="e9f81-106">valor de saudação nunca é exposta pois referência apenas a sua ID de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e9f81-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="e9f81-107">Você não precisa toomanually Inserir valor Olá para segredo Olá cada vez que você implanta recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9f81-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="e9f81-108">Cofre de chaves Olá pode existir em uma assinatura diferente que o grupo de recursos de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="e9f81-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="e9f81-109">Ao referenciar o Cofre de chaves hello, você incluir Olá ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="e9f81-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="e9f81-110">Ao criar o Cofre de chaves hello, defina Olá *enabledForTemplateDeployment* propriedade muito*true*.</span><span class="sxs-lookup"><span data-stu-id="e9f81-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="e9f81-111">Definindo tootrue esse valor, é possível permitir acesso de modelos do Gerenciador de recursos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="e9f81-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="e9f81-112">Implantar um cofre da chave e segredo</span><span class="sxs-lookup"><span data-stu-id="e9f81-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="e9f81-113">toocreate um cofre de chaves e o segredo, use a CLI do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9f81-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="e9f81-114">Observe que esse Cofre de chaves hello está habilitado para implantação de modelo.</span><span class="sxs-lookup"><span data-stu-id="e9f81-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="e9f81-115">Para a CLI do Azure, use:</span><span class="sxs-lookup"><span data-stu-id="e9f81-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="e9f81-116">Para o PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="e9f81-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="e9f81-117">Habilitar o segredo de toohello de acesso</span><span class="sxs-lookup"><span data-stu-id="e9f81-117">Enable access toohello secret</span></span>

<span data-ttu-id="e9f81-118">Se você estiver usando um cofre de chaves novo ou existente, certifique-se de usuário Olá implantar modelo Olá pode acessar o segredo Olá.</span><span class="sxs-lookup"><span data-stu-id="e9f81-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="e9f81-119">usuário Olá Implantando um modelo que faz referência a um segredo deve ter Olá `Microsoft.KeyVault/vaults/deploy/action` permissão para o Cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="e9f81-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="e9f81-120">Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) e [Colaborador](../active-directory/role-based-access-built-in-roles.md#contributor) ambas as funções concedem esse acesso.</span><span class="sxs-lookup"><span data-stu-id="e9f81-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="e9f81-121">Você também pode criar um [função personalizada](../active-directory/role-based-access-control-custom-roles.md) que concede essa permissão e adicione a função de toothat usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e9f81-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="e9f81-122">Para obter informações sobre como adicionar uma função de usuário tooa, consulte [atribuir um usuário tooadministrator funções no Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e9f81-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="e9f81-123">Fazer referência a um segredo com ID estática</span><span class="sxs-lookup"><span data-stu-id="e9f81-123">Reference a secret with static ID</span></span>

<span data-ttu-id="e9f81-124">modelo de saudação que recebe um segredo do Cofre de chaves é como qualquer outro modelo.</span><span class="sxs-lookup"><span data-stu-id="e9f81-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="e9f81-125">Isso ocorre porque **você referenciar o cofre da chave no arquivo de parâmetro hello, não o modelo Olá Olá.**</span><span class="sxs-lookup"><span data-stu-id="e9f81-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="e9f81-126">Por exemplo, a saudação modelo a seguir implanta um banco de dados SQL que inclui uma senha de administrador.</span><span class="sxs-lookup"><span data-stu-id="e9f81-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="e9f81-127">o parâmetro de senha Olá é definido tooa cadeia de caracteres segura.</span><span class="sxs-lookup"><span data-stu-id="e9f81-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="e9f81-128">Mas, Olá não especificar onde vem esse valor.</span><span class="sxs-lookup"><span data-stu-id="e9f81-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="e9f81-129">Agora, crie um arquivo de parâmetro hello precede o modelo.</span><span class="sxs-lookup"><span data-stu-id="e9f81-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="e9f81-130">No arquivo de parâmetro hello, especifique um parâmetro que corresponda Olá nome do parâmetro hello no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9f81-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="e9f81-131">Valor de parâmetro hello, referência Olá segredo do Cofre de chave hello.</span><span class="sxs-lookup"><span data-stu-id="e9f81-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="e9f81-132">Você pode referenciar segredo Olá passando o identificador de recurso de saudação do Cofre de chaves de saudação e o nome de saudação do segredo hello.</span><span class="sxs-lookup"><span data-stu-id="e9f81-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="e9f81-133">Em Olá exemplo a seguir, segredo do Cofre de chaves Olá já deve existir e você fornecer um valor estático para sua ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9f81-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="e9f81-134">Fazer referência a um segredo com ID dinâmica</span><span class="sxs-lookup"><span data-stu-id="e9f81-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="e9f81-135">seção anterior Olá mostrou como toopass uma ID de recurso estático para a chave de saudação cofre segredo.</span><span class="sxs-lookup"><span data-stu-id="e9f81-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="e9f81-136">No entanto, em alguns cenários, é necessário tooreference um segredo do Cofre de chaves que varia com base na implantação atual hello.</span><span class="sxs-lookup"><span data-stu-id="e9f81-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="e9f81-137">Nesse caso, você não pode codificar Olá ID de recurso no arquivo de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9f81-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="e9f81-138">Infelizmente, você não é possível gerar dinamicamente Olá ID de recurso no arquivo de parâmetros de saudação porque expressões de modelo não são permitidas no arquivo de parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9f81-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="e9f81-139">toodynamically gerar ID de recurso de saudação de um segredo do Cofre de chaves, você deve mover o recurso de saudação que precisa segredo Olá em um modelo aninhado.</span><span class="sxs-lookup"><span data-stu-id="e9f81-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="e9f81-140">No modelo mestre, você pode adicionar modelo aninhado hello e passa um parâmetro que contém a ID de recurso Olá gerado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e9f81-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e9f81-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9f81-141">Next steps</span></span>
* <span data-ttu-id="e9f81-142">Para obter informações gerais sobre cofres de chaves, veja [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e9f81-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="e9f81-143">Para obter exemplos completos de referência de segredos de chave, veja [Exemplos do cofre da chave](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="e9f81-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

