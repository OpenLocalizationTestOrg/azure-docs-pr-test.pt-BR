---
title: "Criar um aplicativo lógico usando um modelo no Azure | Microsoft Docs"
description: "Use um modelo do Azure Resource Manager para implantar um aplicativo lógico para definir fluxos de trabalho."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="e1739-103">Crie um Aplicativo Lógico usando um modelo</span><span class="sxs-lookup"><span data-stu-id="e1739-103">Create a Logic App using a template</span></span>
<span data-ttu-id="e1739-104">Os modelos fornecem uma maneira rápida de usar conectores diferentes dentro de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e1739-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="e1739-105">Os aplicativos lógicos incluem modelos do Azure Resource Manager para criar um aplicativo lógico que pode ser usado para definir fluxos de trabalho comerciais.</span><span class="sxs-lookup"><span data-stu-id="e1739-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="e1739-106">Você pode definir quais recursos são implantados e como definir os parâmetros quando implantar seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e1739-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="e1739-107">Você pode usar esse modelo para seus próprios cenários de negócios ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="e1739-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="e1739-108">Para obter mais detalhes sobre as propriedades do Aplicativo lógico, consulte [API de Gerenciamento de Fluxo de Trabalho de Aplicativo Lógico](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1739-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="e1739-109">Para obter exemplos da definição em si, consulte [Criar definições de Aplicativos Lógicos](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="e1739-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="e1739-110">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1739-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="e1739-111">Para o modelo completo, consulte [Modelo de Aplicativo Lógico](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e1739-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="e1739-112">O que você implanta</span><span class="sxs-lookup"><span data-stu-id="e1739-112">What you deploy</span></span>
<span data-ttu-id="e1739-113">Neste modelo, você implanta um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e1739-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="e1739-114">Para executar a implantação automaticamente, selecione o seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="e1739-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="e1739-115">[![Implantar no Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e1739-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e1739-116">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="e1739-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="e1739-117">testUri</span><span class="sxs-lookup"><span data-stu-id="e1739-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="e1739-118">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="e1739-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="e1739-119">Aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="e1739-119">Logic app</span></span>
<span data-ttu-id="e1739-120">Cria o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e1739-120">Creates the logic app.</span></span>

<span data-ttu-id="e1739-121">Os modelos usam um valor de parâmetro para o nome do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e1739-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="e1739-122">Ele define o local do aplicativo lógico para o mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e1739-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="e1739-123">Essa definição específica é executada uma vez por hora e executa ping do local especificado no parâmetro **testUri** .</span><span class="sxs-lookup"><span data-stu-id="e1739-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-to-run-deployment"></a><span data-ttu-id="e1739-124">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="e1739-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e1739-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1739-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="e1739-126">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e1739-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



