---
title: aaaAutomate Insights do aplicativo do Azure com o PowerShell | Microsoft Docs
description: Automatize criando testes de disponibilidade, alerta e recursos no PowerShell usando um modelo do Azure Resource Manager.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a>Criar recursos do Application Insights usando o PowerShell
Este artigo mostra como tooautomate Olá criação e atualização de [Application Insights](app-insights-overview.md) recursos automaticamente, usando o gerenciamento de recursos do Azure. Por exemplo, você pode fazer isso como parte de um processo de compilação. Juntamente com recursos básicos de Application Insights hello, você pode criar [testes da web de disponibilidade](app-insights-monitor-web-app-availability.md), configure [alertas](app-insights-alerts.md), defina hello [preços esquema](app-insights-pricing.md)e criar outro do Azure recursos.

Olá chave toocreating esses recursos são os modelos de JSON para [do Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). Em resumo, o procedimento de saudação é: baixar Olá JSON definições de recursos existentes; parametrizar certos valores como nomes; e execute o modelo hello sempre que quiser toocreate um novo recurso. Você pode empacotar vários recursos juntos, toocreate-los em um excelente – por exemplo, um monitor de aplicativo com testes de disponibilidade, alertas e armazenamento para a exportação contínua. Há alguns toosome sutilezas de parametrizações hello, que vamos explicar aqui.

## <a name="one-time-setup"></a>Configuração única
Se você nunca usou o PowerShell com sua assinatura do Azure:

Instale o módulo de Powershell do Azure de saudação na máquina Olá onde deseja toorun Olá scripts:

1. Instale o [Microsoft Web Platform Installer (v5 ou superior)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Use-tooinstall Microsoft Azure Powershell.

## <a name="create-an-azure-resource-manager-template"></a>Criar um modelo do Azure Resource Manager
Criar um novo arquivo .json - vamos chamá-lo de `template1.json` neste exemplo. Copie este conteúdo nele:

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a>Criar recursos do Application Insights
1. No PowerShell, entrar tooAzure:
   
    `Login-AzureRmAccount`
2. Execute um comando como este:
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`é o grupo de saudação onde você deseja toocreate Olá novos recursos.
   * `-TemplateFile`deve ocorrer antes de parâmetros personalizados hello.
   * `-appName`nome de saudação do hello toocreate de recursos.

Você pode adicionar outros parâmetros - você encontrará suas descrições na seção de parâmetros de saudação do modelo de saudação.

## <a name="tooget-hello-instrumentation-key"></a>chave de instrumentação Olá tooget
Depois de criar um recurso de aplicativo, você desejará chave de instrumentação hello: 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Definir plano de preço Olá

Você pode definir Olá [plano de preço](app-insights-pricing.md).

toocreate um recurso de aplicativo com o plano de preço do Enterprise hello, usando o modelo de saudação acima:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|plan|
|---|---|
|1|Básica|
|2|Enterprise|

* Se você quiser apenas o plano de preço básico toouse saudação padrão, você pode omitir o recurso de CurrentBillingFeatures de saudação do modelo de saudação.
* Se você quiser plano de preço Olá toochange depois Olá componente recurso foi criado, você pode usar um modelo que omite o recurso de "microsoft.insights/components" hello. Além disso, omita Olá `dependsOn` nó da saudação recursos de cobrança. 

tooverify Olá plano de preço atualizado, examine a folha de hello "Recursos + preços" no navegador de saudação. **Atualizar exibição de navegador Olá** toomake se você ver o estado mais recente hello.



## <a name="add-a-metric-alert"></a>Adicionar um alerta de Métrica

tooset se um alerta de métrica no hello mesmo tempo como o recurso de aplicativo, código de mesclagem como isso no arquivo de modelo de saudação:

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

Quando você chama o modelo Olá, opcionalmente, você pode adicionar esse parâmetro:

    `-responseTime 2`

É claro que você pode parametrizar outros campos. 

toofind nomes de tipo hello e detalhes de configuração de regras de alerta, criar uma regra manualmente e, em seguida, inspecionar na [do Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Adicionar um teste de disponibilidade

Este exemplo é para um teste de ping (tootest uma única página).  

**Há duas partes** em um teste de disponibilidade: teste Olá em si e o alerta Olá notifica sobre falhas.

Saudação de código a seguir no arquivo de modelo de saudação que cria o aplicativo hello de mesclagem.

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

códigos de saudação toodiscover para outros locais de teste ou criação de saudação tooautomate de testes da web mais complexos, crie um exemplo manualmente e parametrizar, em seguida, o código de saudação do [do Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Adicionar mais recursos

criação de saudação tooautomate de qualquer outro recurso de qualquer tipo, criar um exemplo manualmente e, em seguida, copie e parametrizar seu código de [do Azure Resource Manager](https://resources.azure.com/). 

1. Abra o [Gerenciador de Recursos do Azure](https://resources.azure.com/). Navegar pela `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour recursos de aplicativo. 
   
    ![Navegação no Gerenciador de recursos do Azure](./media/app-insights-powershell/01.png)
   
    *Componentes* é Olá recursos básicos do Application Insights para a exibição de aplicativos. Há recursos separados para Olá associados a regras de alerta e testes da web de disponibilidade.
2. Saudação de cópia JSON de componente de saudação no local apropriado do hello em `template1.json`.
3. Exclua essas propriedades:
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Abrir seções de webtests e alertrules hello e copie Olá JSON para itens individuais no modelo. (Não copiar de saudação webtests ou alertrules nós: vá para itens de saudação sob eles.)
   
    Cada teste da web tem uma regra de alerta associada, para que você tenha toocopy deles.
   
    Você também pode incluir alertas sobre métricas. [Nomes de métrica](app-insights-powershell-alerts.md#metric-names).
5. Insira esta linha em cada recurso:
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Parâmetros de modelo Olá
Agora você tem nomes específicos de saudação de tooreplace com parâmetros. muito[parametrizar um modelo](../azure-resource-manager/resource-group-authoring-templates.md), você escrever expressões que usam um [conjunto de funções auxiliares](../azure-resource-manager/resource-group-template-functions.md). 

Você não pode parametrizar apenas uma parte de uma cadeia de caracteres, use `concat()` toobuild cadeias de caracteres.

Aqui estão exemplos de substituições hello, você desejará toomake. Há várias ocorrências de cada substituição. Talvez seja necessário outras em seu modelo. Esses exemplos usam parâmetros hello e variáveis definidas na parte superior de saudação do modelo de saudação.

| find | substitua por |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"` (minúscula) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Exclua Guid e ID. |

### <a name="set-dependencies-between-hello-resources"></a>Definir dependências entre os recursos de saudação
Azure deve configurar os recursos de saudação em ordem estrita. toomake-se que a instalação seja concluído antes de saudação começa em seguida, adicionar linhas de dependência:

* Em disponibilidade Olá teste recursos:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* No recurso de alerta de saudação para um teste de disponibilidade:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Próximas etapas
Outros artigos sobre automação:

* [Criar um recurso do Application Insights](app-insights-powershell-script-create-resource.md) -método rápido sem usar um modelo.
* [Configurar alertas](app-insights-powershell-alerts.md)
* [Criar testes na Web](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Enviar informações de tooApplication de diagnóstico do Azure](app-insights-powershell-azure-diagnostics.md)
* [Implantar tooAzure do GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Criar anotações de versão](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

