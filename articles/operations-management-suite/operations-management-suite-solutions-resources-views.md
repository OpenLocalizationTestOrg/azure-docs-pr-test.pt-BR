---
title: "Exibições nas soluções de gerenciamento do OMS (Operations Management Suite) | Microsoft Docs"
description: "As soluções de gerenciamento no OMS (Operations Management Suite) normalmente incluirão uma ou mais exibições para visualizar os dados.  Este artigo descreve como exportar uma exibição criada pelo Designer de Exibição e incluí-la em uma solução de gerenciamento. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="80d5a-104">Exibições nas soluções de gerenciamento do OMS (Operations Management Suite) (Preview)</span><span class="sxs-lookup"><span data-stu-id="80d5a-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="80d5a-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="80d5a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="80d5a-106">Os esquemas descritos a seguir estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="80d5a-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="80d5a-107">As [soluções de gerenciamento no OMS (Operations Management Suite)](operations-management-suite-solutions.md) normalmente incluirão uma ou mais exibições para visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="80d5a-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="80d5a-108">Este artigo descreve como exportar uma exibição criada pelo [Designer de Exibição](../log-analytics/log-analytics-view-designer.md) e incluí-la em uma solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="80d5a-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="80d5a-109">Os exemplos neste artigo usam parâmetros e variáveis que são necessários ou comuns para as soluções de gerenciamento e estão descritos em [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) (Criando soluções de gerenciamento no OMS (Operations Management Suite))</span><span class="sxs-lookup"><span data-stu-id="80d5a-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="80d5a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80d5a-110">Prerequisites</span></span>
<span data-ttu-id="80d5a-111">Este artigo pressupõe que você já esteja familiarizado com o modo para [criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e com a estrutura de um arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="80d5a-112">Visão geral</span><span class="sxs-lookup"><span data-stu-id="80d5a-112">Overview</span></span>
<span data-ttu-id="80d5a-113">Para incluir uma exibição em uma solução de gerenciamento, crie um **recurso** no [arquivo de solução](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="80d5a-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="80d5a-114">O JSON que descreve a configuração detalhada da exibição geralmente é complexo e não algo que um autor típico de solução seria capaz de criar manualmente.</span><span class="sxs-lookup"><span data-stu-id="80d5a-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="80d5a-115">O método mais comum é criar a exibição usando o [Designer de Exibição](../log-analytics/log-analytics-view-designer.md), exportá-la e, em seguida, adicionar sua configuração detalhada na solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="80d5a-116">As etapas básicas para adicionar uma exibição a uma solução são da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="80d5a-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="80d5a-117">Cada etapa é descrita mais detalhadamente nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="80d5a-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="80d5a-118">Exportar a exibição para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="80d5a-118">Export the view to a file.</span></span>
2. <span data-ttu-id="80d5a-119">Criar o recurso de exibição na solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="80d5a-120">Adicionar os detalhes da exibição.</span><span class="sxs-lookup"><span data-stu-id="80d5a-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="80d5a-121">Exportar a exibição para um arquivo</span><span class="sxs-lookup"><span data-stu-id="80d5a-121">Export the view to a file</span></span>
<span data-ttu-id="80d5a-122">Siga as instruções em [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) (Designer de exibição do Log Analytics) para exportar uma exibição para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="80d5a-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="80d5a-123">O arquivo exportado será no formato JSON com os mesmos [elementos do arquivo de solução](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="80d5a-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="80d5a-124">O elemento **resources** do arquivo de exibição terá um recurso com um tipo de **Microsoft.OperationalInsights/workspaces**, que representa o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="80d5a-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="80d5a-125">Esse elemento terá um subelemento com um tipo de **views**, que representa a exibição e contém a configuração detalhada.</span><span class="sxs-lookup"><span data-stu-id="80d5a-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="80d5a-126">Você copiará os detalhes desse elemento e, em seguida, vai copiá-lo em sua solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="80d5a-127">Criar o recurso de exibição na solução</span><span class="sxs-lookup"><span data-stu-id="80d5a-127">Create the view resource in the solution</span></span>
<span data-ttu-id="80d5a-128">Adicione o seguinte recurso de exibição ao elemento **resources** do seu arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="80d5a-129">Ele usa as variáveis descritas abaixo, que você também deverá adicionar.</span><span class="sxs-lookup"><span data-stu-id="80d5a-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="80d5a-130">Observe que as propriedades **Dashboard** e **OverviewTile** são espaços reservados que serão substituídos pelas propriedades correspondentes do arquivo de exibição exportado.</span><span class="sxs-lookup"><span data-stu-id="80d5a-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="80d5a-131">Adicione as variáveis a seguir ao elemento de variáveis do arquivo de solução e substitua os valores pelos da solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="80d5a-132">Observe que você poderá copiar todo o recurso de exibição do arquivo de exibição exportado, mas precisará fazer as seguintes alterações para que ele funcione em sua solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="80d5a-133">O **type** para o recurso de exibição precisa ser alterado de **views** para **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="80d5a-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="80d5a-134">A propriedade **name** para o recurso de exibição precisa ser alterada para incluir o nome do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="80d5a-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="80d5a-135">A dependência no espaço de trabalho precisa ser removida, uma vez que o recurso workspace não foi definido na solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="80d5a-136">A propriedade **DisplayName** precisa ser adicionada à exibição.</span><span class="sxs-lookup"><span data-stu-id="80d5a-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="80d5a-137">**Id**, **Name** e **DisplayName** devem ser compatíveis.</span><span class="sxs-lookup"><span data-stu-id="80d5a-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="80d5a-138">Os nomes dos parâmetros devem ser alterados para coincidirem com o conjunto de parâmetros exigido.</span><span class="sxs-lookup"><span data-stu-id="80d5a-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="80d5a-139">As variáveis devem ser definidas na solução e usadas nas propriedades adequadas.</span><span class="sxs-lookup"><span data-stu-id="80d5a-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="80d5a-140">Adicionar os detalhes de exibição</span><span class="sxs-lookup"><span data-stu-id="80d5a-140">Add the view details</span></span>
<span data-ttu-id="80d5a-141">O recurso de exibição no arquivo de exibição exportado terá dois elementos no elemento **properties** chamados **Dashboard** e **OverviewTile**, que terão a configuração detalhada da exibição.</span><span class="sxs-lookup"><span data-stu-id="80d5a-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="80d5a-142">Copie esses dois elementos e seus conteúdos no elemento **properties** do recurso de exibição em seu arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="80d5a-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="80d5a-143">Exemplo</span><span class="sxs-lookup"><span data-stu-id="80d5a-143">Example</span></span>
<span data-ttu-id="80d5a-144">Por exemplo, a amostra a seguir apresenta um arquivo de solução simples com uma exibição.</span><span class="sxs-lookup"><span data-stu-id="80d5a-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="80d5a-145">As reticências (...) são mostradas para os conteúdos de **Dashboard** e **OverviewTile** por motivos de espaço.</span><span class="sxs-lookup"><span data-stu-id="80d5a-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="80d5a-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80d5a-146">Next steps</span></span>
* <span data-ttu-id="80d5a-147">Conheça os detalhes completos de criação das [soluções de gerenciamento](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="80d5a-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="80d5a-148">Incluir os [runbooks de automação na solução de gerenciamento](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="80d5a-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
