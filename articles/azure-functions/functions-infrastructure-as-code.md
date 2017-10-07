---
title: "implantação de recursos de aaaAutomate para um aplicativo de função em funções do Azure | Microsoft Docs"
description: "Saiba como toobuild um modelo do Gerenciador de recursos do Azure que implanta o aplicativo de função."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, arquitetura sem servidores, infraestrutura como código, azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Automatizar a implantação de recursos para seu aplicativo de funções do Azure Functions

Você pode usar um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo de função. Este artigo descreve recursos Olá necessárias e os parâmetros para fazer isso. Talvez seja necessário obter recursos adicionais toodeploy, dependendo da saudação [gatilhos e associações](functions-triggers-bindings.md) em seu aplicativo de função.

Para saber mais sobre a criação de modelos, consulte [Criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Para modelos de exemplo, consulte:
- [Aplicativo de funções no Plano de Consumo]
- [Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]

## <a name="required-resources"></a>Recursos necessários

Um aplicativo de funções requer estes recursos:

* Uma conta de [Armazenamento do Azure](../storage/index.md)
* Um plano de hospedagem (Plano de Consumo ou Plano do Serviço de Aplicativo)
* Um aplicativo de funções 

### <a name="storage-account"></a>Conta de armazenamento

Uma conta de armazenamento do Azure é necessária para um aplicativo de funções. Você precisa de uma conta de finalidade geral que dá suporte a blobs, tabelas, consultas e arquivos. Para saber mais, confira [Requisitos da conta de armazenamento do Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Além disso, Olá propriedades `AzureWebJobsStorage` e `AzureWebJobsDashboard` devem ser especificados como configurações de aplicativo na configuração do site hello. tempo de execução de funções do Azure Olá usa Olá `AzureWebJobsStorage` toocreate as filas internas de cadeia de caracteres de conexão. Olá a cadeia de caracteres de conexão `AzureWebJobsDashboard` é usado toolog tooAzure tabela armazenamento e energia hello **Monitor** no portal de saudação.

Essas propriedades são especificadas em Olá `appSettings` coleção em Olá `siteConfig` objeto:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Plano de hospedagem

definição de saudação do plano de hospedagem de saudação varia, dependendo se você usar um plano de serviço de aplicativo ou de consumo. Consulte [implantar um aplicativo de função no plano de consumo Olá](#consumption) e [implantar um aplicativo de função em Olá plano de serviço de aplicativo](#app-service-plan).

### <a name="function-app"></a>Aplicativo de funções

recurso de aplicativo de função Hello é definido usando um recurso do tipo **Microsoft.Web/Site** e tipo **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Implantar um aplicativo de função no plano de consumo Olá

Você pode executar um aplicativo de função em dois modos diferentes: Olá plano de consumo e hello plano de serviço de aplicativo. plano de consumo Olá aloca automaticamente a capacidade de computação quando seu código está em execução, pode ser dimensionado como carga de toohandle necessário e expande para baixo quando o código não está em execução. Portanto, você não tem toopay para máquinas virtuais ociosas, e você não tem capacidade tooreserve com antecedência. toolearn mais sobre hospedagem planos, consulte [planos de serviço de aplicativo e o consumo de funções do Azure](functions-scale.md).

Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano de Consumo].

### <a name="create-a-consumption-plan"></a>Criar um Plano de Consumo

Um Plano de Consumo é um tipo especial de recurso "serverfarm". Especificá-lo usando Olá `Dynamic` valor Olá `computeMode` e `sku` propriedades:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Criar um aplicativo de funções

Além disso, um plano de consumo requer duas configurações adicionais na configuração do site Olá: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`. Essas propriedades configuram Olá armazenamento conta e o caminho onde o código do aplicativo de função hello e configuração são armazenados.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Implantar um aplicativo de função em Olá plano de serviço de aplicativo

Em Olá plano de serviço de aplicativo, seu aplicativo de função é executado em máquinas virtuais dedicadas em aplicativos de tooweb Basic, Standard e Premium SKUs, semelhantes. Para obter detalhes sobre como funciona a saudação plano de serviço de aplicativo, consulte Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano do Serviço de Aplicativo do Azure].

### <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Criar um aplicativo de funções 

Depois de selecionar uma opção de dimensionamento, crie um aplicativo de funções. Olá aplicativo é o contêiner de saudação que contém todas as suas funções.

Um aplicativo de funções tem muitos recursos filho que podem ser usados na sua implantação, incluindo configurações do aplicativo e opções de controle do código-fonte. Você também pode escolher Olá tooremove **sourcecontrols** recurso filho e use outra [opção de implantação](functions-continuous-deployment.md) em vez disso.

> [!IMPORTANT]
> toosuccessfully implantar seu aplicativo usando o Gerenciador de recursos do Azure, é importante toounderstand como os recursos são implantados no Azure. Em Olá exemplo a seguir, as configurações de nível superior são aplicadas usando **siteConfig**. É importante tooset essas configurações em um alto nível, porque eles transmitem o mecanismo de tempo de execução e a implantação de funções de toohello do informações. Informações de nível superior é necessário antes do filho Olá **sourcecontrols/web** recursos é aplicado. Embora seja possível tooconfigure essas configurações no hello nível filho **config/appSettings** recursos, em alguns casos, seu aplicativo de função deve ser implantado *antes de* **config/appSettings**  é aplicado. Por exemplo, quando você está usado funções com [aplicativos lógicos](../logic-apps/index.md), as funções são uma dependência de outro recurso.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Este modelo usa Olá [projeto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valor de configurações de aplicativo, que define o diretório base hello, na qual Olá mecanismo de implantação de funções (Kudu) procura código implantável. Em nosso repositório, nosso funções estão em uma subpasta da saudação **src** pasta. Portanto, em Olá anterior de exemplo, definimos o valor de configurações de aplicativo hello muito`src`. Se as funções estão na raiz de saudação do repositório, ou se não estiver implantando do controle de origem, você pode remover esse valor de configurações do aplicativo.

## <a name="deploy-your-template"></a>Implantar o modelo

Você pode usar qualquer Olá toodeploy maneiras a seguir o modelo:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [API REST](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>TooAzure botão implantar

Substituir ```<url-encoded-path-to-azuredeploy-json>``` com um [codificados de URL](https://www.bing.com/search?q=url+encode) versão do caminho bruto de saudação do seu `azuredeploy.json` arquivo no GitHub.

Este é um exemplo que usa markdown:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Este é um exemplo que usa HTML:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como toodevelop e configure funções do Azure.

* [Referência do desenvolvedor do Azure Functions](functions-reference.md)
* [Como tooconfigure Azure funciona configurações do aplicativo](functions-how-to-use-azure-function-app-settings.md)
* [Como criar a sua primeira função do Azure](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicativo de funções no Plano de Consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
