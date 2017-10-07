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
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Exibições nas soluções de gerenciamento do OMS (Operations Management Suite) (Preview)
> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.    
>
>

[Soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions.md) geralmente inclui uma ou mais exibições toovisualize de dados.  Este artigo descreve como tooexport uma exibição criada pelo Olá [View Designer](../log-analytics/log-analytics-view-designer.md) e incluí-lo em uma solução de gerenciamento.  

> [!NOTE]
> Olá exemplos neste artigo usam parâmetros e variáveis que são ambos soluções toomanagement necessárias ou comuns e descritos na [criando soluções de gerenciamento no OMS Operations Management Suite ()](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você já está familiarizado com como muito[criar uma solução de gerenciamento](operations-management-suite-solutions-creating.md) e estrutura de saudação de um arquivo de solução.

## <a name="overview"></a>Visão geral
tooinclude uma exibição em uma solução de gerenciamento, você cria um **recurso** na Olá [arquivo de solução](operations-management-suite-solutions-creating.md).  Olá JSON que descreve a configuração detalhada do modo de exibição da saudação é normalmente é complexo embora e não é algo que o autor de uma solução típica seria capaz de toocreate manualmente.  Olá, método mais comum é modo de exibição de saudação do toocreate usando Olá [View Designer](../log-analytics/log-analytics-view-designer.md), exportá-lo e, em seguida, adicionar sua solução de toohello configuração detalhada.

etapas básicas de saudação tooadd uma solução de tooa de exibição são da seguinte maneira.  Cada etapa é descrita mais detalhadamente nas seções de saudação abaixo.

1. Olá exibição tooa arquivo de exportação.
2. Crie recursos de exibição Olá Olá solução.
3. Adicione detalhes da exibição de saudação.

## <a name="export-hello-view-tooa-file"></a>Olá exibição tooa arquivo de exportação
Siga as instruções de saudação em [Designer de exibição de análise de Log](../log-analytics/log-analytics-view-designer.md) tooexport um arquivo de tooa de exibição.  Olá arquivo exportado será ser em formato JSON com hello mesmo [elementos como arquivo de solução Olá](operations-management-suite-solutions-solution-file.md).  

Olá **recursos** elemento do arquivo de exibição Olá terá um recurso com um tipo de **Microsoft.OperationalInsights/workspaces** representa Olá espaço de trabalho do OMS.  Este elemento tem um subelemento com um tipo de **exibições** que representa o modo de exibição de saudação e contém sua configuração detalhada.  Você copiará detalhes Olá desse elemento e, em seguida, copie-o em sua solução.

## <a name="create-hello-view-resource-in-hello-solution"></a>Criar recursos de exibição Olá Olá solução
Adicionar Olá toohello de recursos do modo de exibição a seguir **recursos** elemento do arquivo de solução.  Ele usa as variáveis descritas abaixo, que você também deverá adicionar.  Observe que Olá **painel** e **OverviewTile** propriedades são espaços reservados que serão substituídas com propriedades correspondentes de saudação do arquivo de modo de exibição exportado hello.

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

Adicione Olá elemento de variáveis toohello variáveis saudação do arquivo da solução a seguir e substitua Olá valores toothose para sua solução.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Observe que você poderá copiar recursos de toda a exibição de saudação do arquivo exportado do modo de exibição, mas você precisaria Olá toomake as seguintes alterações para que ele toowork em sua solução.  

* Olá **tipo** para exibição Olá recurso precisa toobe alterado de **exibições** muito**Microsoft.OperationalInsights/workspaces**.
* Olá **nome** propriedade para o recurso de exibição Olá precisa de nome de espaço de trabalho do toobe alterado tooinclude hello.
* dependência de saudação no espaço de trabalho de saudação precisa toobe removido desde o recurso de espaço de trabalho Olá não está definido na solução de saudação.
* **DisplayName** propriedade necessidades toobe adicionado toohello exibição.  Olá **Id**, **nome**, e **DisplayName** devem ser compatíveis.
* Nomes de parâmetro devem ser alterados Olá toomatch necessário conjunto de parâmetros.
* Variáveis devem ser definidas na solução hello e usadas nas propriedades de saudação apropriado.

## <a name="add-hello-view-details"></a>Adicionar detalhes da exibição Olá
recurso de exibição Olá Olá exportado Exibir arquivo contém dois elementos em Olá **propriedades** elemento chamado **painel** e **OverviewTile** que contêm Olá configuração detalhada do modo de exibição de saudação.  Copie esses dois elementos e seu conteúdo Olá **propriedades** elemento de recurso de exibição de saudação em seu arquivo de solução.

## <a name="example"></a>Exemplo
Por exemplo, Olá exemplo a seguir mostra um arquivo de solução simples com um modo de exibição.  Reticências (...) são mostradas para Olá **painel** e **OverviewTile** conteúdo por motivos de espaço.

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




## <a name="next-steps"></a>Próximas etapas
* Conheça os detalhes completos de criação das [soluções de gerenciamento](operations-management-suite-solutions-creating.md).
* Incluir os [runbooks de automação na solução de gerenciamento](operations-management-suite-solutions-resources-automation.md).
