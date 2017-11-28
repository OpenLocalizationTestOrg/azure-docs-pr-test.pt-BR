---
title: "aaaViews em soluções de gerenciamento do Operations Management Suite (OMS) | Microsoft Docs"
description: "Soluções de gerenciamento no OMS Operations Management Suite () normalmente incluirá uma ou mais exibições toovisualize de dados.  Este artigo descreve como tooexport uma exibição criada pelo Olá Designer de exibição e incluí-lo em uma solução de gerenciamento. "
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
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="97fc6-104">Exibições nas soluções de gerenciamento do OMS (Operations Management Suite) (Preview)</span><span class="sxs-lookup"><span data-stu-id="97fc6-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="97fc6-105">Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="97fc6-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="97fc6-106">Qualquer esquema descrita abaixo é toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="97fc6-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="97fc6-107">[Soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions.md) geralmente inclui uma ou mais exibições toovisualize de dados.</span><span class="sxs-lookup"><span data-stu-id="97fc6-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="97fc6-108">Este artigo descreve como tooexport uma exibição criada pelo Olá [View Designer](../log-analytics/log-analytics-view-designer.md) e incluí-lo em uma solução de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="97fc6-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="97fc6-109">Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="97fc6-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="97fc6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97fc6-110">Prerequisites</span></span>
<span data-ttu-id="97fc6-111">Este artigo pressupõe que você já está familiarizado com como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e estrutura de saudação de um arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="97fc6-112">Visão geral</span><span class="sxs-lookup"><span data-stu-id="97fc6-112">Overview</span></span>
<span data-ttu-id="97fc6-113">tooinclude uma exibição em uma solução de gerenciamento, você cria um **recurso** na Olá [arquivo de solução](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="97fc6-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="97fc6-114">Olá JSON que descreve a configuração detalhada do modo de exibição da saudação é normalmente é complexo embora e não é algo que o autor de uma solução típica seria capaz de toocreate manualmente.</span><span class="sxs-lookup"><span data-stu-id="97fc6-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="97fc6-115">Olá, método mais comum é modo de exibição de saudação do toocreate usando Olá [View Designer](../log-analytics/log-analytics-view-designer.md), exportá-lo e, em seguida, adicionar sua solução de toohello configuração detalhada.</span><span class="sxs-lookup"><span data-stu-id="97fc6-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="97fc6-116">etapas básicas de saudação tooadd uma solução de tooa de exibição são da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="97fc6-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="97fc6-117">Cada etapa é descrita mais detalhadamente nas seções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="97fc6-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="97fc6-118">Olá exibição tooa arquivo de exportação.</span><span class="sxs-lookup"><span data-stu-id="97fc6-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="97fc6-119">Crie recursos de exibição Olá Olá solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="97fc6-120">Adicione detalhes da exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fc6-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="97fc6-121">Olá exibição tooa arquivo de exportação</span><span class="sxs-lookup"><span data-stu-id="97fc6-121">Export hello view tooa file</span></span>
<span data-ttu-id="97fc6-122">Siga as instruções de saudação em [Designer de exibição de análise de Log](../log-analytics/log-analytics-view-designer.md) tooexport um arquivo de tooa de exibição.</span><span class="sxs-lookup"><span data-stu-id="97fc6-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="97fc6-123">Olá arquivo exportado será ser em formato JSON com hello mesmo [elementos como arquivo de solução Olá](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="97fc6-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="97fc6-124">Olá **recursos** elemento do arquivo de exibição Olá terá um recurso com um tipo de **Microsoft.OperationalInsights/workspaces** representa Olá espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="97fc6-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="97fc6-125">Este elemento tem um subelemento com um tipo de **exibições** que representa o modo de exibição de saudação e contém sua configuração detalhada.</span><span class="sxs-lookup"><span data-stu-id="97fc6-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="97fc6-126">Você copiará detalhes Olá desse elemento e, em seguida, copie-o em sua solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="97fc6-127">Criar recursos de exibição Olá Olá solução</span><span class="sxs-lookup"><span data-stu-id="97fc6-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="97fc6-128">Adicionar Olá toohello de recursos do modo de exibição a seguir **recursos** elemento do arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="97fc6-129">Ele usa as variáveis descritas abaixo, que você também deverá adicionar.</span><span class="sxs-lookup"><span data-stu-id="97fc6-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="97fc6-130">Observe que Olá **painel** e **OverviewTile** propriedades são espaços reservados que serão substituídas com propriedades correspondentes de saudação do arquivo de modo de exibição exportado hello.</span><span class="sxs-lookup"><span data-stu-id="97fc6-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

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

<span data-ttu-id="97fc6-131">Adicione Olá elemento de variáveis toohello variáveis saudação do arquivo da solução a seguir e substitua Olá valores toothose para sua solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="97fc6-132">Observe que você poderá copiar recursos de toda a exibição de saudação do arquivo exportado do modo de exibição, mas você precisaria Olá toomake as seguintes alterações para que ele toowork em sua solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="97fc6-133">Olá **tipo** para exibição Olá recurso precisa toobe alterado de **exibições** muito**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="97fc6-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="97fc6-134">Olá **nome** propriedade para o recurso de exibição Olá precisa de nome de espaço de trabalho do toobe alterado tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="97fc6-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="97fc6-135">dependência de saudação no espaço de trabalho de saudação precisa toobe removido desde o recurso de espaço de trabalho Olá não está definido na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fc6-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="97fc6-136">**DisplayName** propriedade necessidades toobe adicionado toohello exibição.</span><span class="sxs-lookup"><span data-stu-id="97fc6-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="97fc6-137">Olá **Id**, **nome**, e **DisplayName** devem ser compatíveis.</span><span class="sxs-lookup"><span data-stu-id="97fc6-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="97fc6-138">Nomes de parâmetro devem ser alterados Olá toomatch necessário conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="97fc6-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="97fc6-139">Variáveis devem ser definidas na solução hello e usadas nas propriedades de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="97fc6-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="97fc6-140">Adicionar detalhes da exibição Olá</span><span class="sxs-lookup"><span data-stu-id="97fc6-140">Add hello view details</span></span>
<span data-ttu-id="97fc6-141">recurso de exibição Olá Olá exportado Exibir arquivo contém dois elementos em Olá **propriedades** elemento chamado **painel** e **OverviewTile** que contêm Olá configuração detalhada do modo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="97fc6-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="97fc6-142">Copie esses dois elementos e seu conteúdo Olá **propriedades** elemento de recurso de exibição de saudação em seu arquivo de solução.</span><span class="sxs-lookup"><span data-stu-id="97fc6-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="97fc6-143">Exemplo</span><span class="sxs-lookup"><span data-stu-id="97fc6-143">Example</span></span>
<span data-ttu-id="97fc6-144">Por exemplo, Olá exemplo a seguir mostra um arquivo de solução simples com um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="97fc6-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="97fc6-145">Reticências (...) são mostradas para Olá **painel** e **OverviewTile** conteúdo por motivos de espaço.</span><span class="sxs-lookup"><span data-stu-id="97fc6-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="97fc6-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97fc6-146">Next steps</span></span>
* <span data-ttu-id="97fc6-147">Conheça os detalhes completos de criação das [soluções de gerenciamento](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="97fc6-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="97fc6-148">Incluir os [runbooks de automação na solução de gerenciamento](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="97fc6-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
