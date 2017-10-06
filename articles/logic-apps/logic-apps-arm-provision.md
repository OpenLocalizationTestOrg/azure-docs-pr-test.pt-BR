---
title: "aaaCreate um aplicativo lógico usando um modelo no Azure | Microsoft Docs"
description: "Use um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo lógico para definir fluxos de trabalho."
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
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="1e8f8-103">Crie um Aplicativo Lógico usando um modelo</span><span class="sxs-lookup"><span data-stu-id="1e8f8-103">Create a Logic App using a template</span></span>
<span data-ttu-id="1e8f8-104">Modelos fornecem uma maneira rápida toouse conectores diferentes dentro de um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="1e8f8-105">Aplicativos lógicos inclui modelos do Gerenciador de recursos do Azure para toocreate um aplicativo de lógica que pode ser usado toodefine fluxos de trabalho comerciais.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="1e8f8-106">Você pode definir quais recursos são implantados e como toodefine parâmetros quando você implanta o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="1e8f8-107">Você pode usar este modelo para seus próprios cenários de negócios ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="1e8f8-108">Para obter mais detalhes sobre propriedades do aplicativo hello lógica, consulte [lógica de API de gerenciamento de fluxo de trabalho de aplicativo](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e8f8-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="1e8f8-109">Para obter exemplos de definição de saudação em si, consulte [definições de aplicativo de lógica de autor](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="1e8f8-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="1e8f8-110">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1e8f8-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="1e8f8-111">Para o modelo do hello completa, consulte [modelo de aplicativo lógico](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="1e8f8-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="1e8f8-112">O que você implanta</span><span class="sxs-lookup"><span data-stu-id="1e8f8-112">What you deploy</span></span>
<span data-ttu-id="1e8f8-113">Neste modelo, você implanta um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="1e8f8-114">implantação de saudação toorun automaticamente, selecione Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e8f8-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="1e8f8-115">[![Implantar tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1e8f8-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="1e8f8-116">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1e8f8-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="1e8f8-117">testUri</span><span class="sxs-lookup"><span data-stu-id="1e8f8-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="1e8f8-118">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="1e8f8-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="1e8f8-119">Aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="1e8f8-119">Logic app</span></span>
<span data-ttu-id="1e8f8-120">Cria um aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-120">Creates hello logic app.</span></span>

<span data-ttu-id="1e8f8-121">modelos de saudação usa um valor de parâmetro para o nome do aplicativo hello lógica.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="1e8f8-122">Ele define o local de saudação do hello lógica aplicativo toohello mesmo local que o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="1e8f8-123">Esta definição específica é executado uma vez por hora e pings Olá local especificado em Olá **testUri** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1e8f8-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

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


## <a name="commands-toorun-deployment"></a><span data-ttu-id="1e8f8-124">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="1e8f8-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="1e8f8-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e8f8-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="1e8f8-126">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1e8f8-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



