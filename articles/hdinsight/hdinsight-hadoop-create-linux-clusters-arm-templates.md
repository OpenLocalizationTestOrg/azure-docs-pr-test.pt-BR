---
title: "Criar clusters Hadoop usando modelos – Azure HDInsight | Microsoft Docs"
description: Aprenda a criar clusters para o HDInsight usando modelos do Resource Manager
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/06/2017
ms.author: jgao
ms.openlocfilehash: 38a60a64c8b2207a4795a63cfeb3527dedc8aa91
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Criar clusters Hadoop no HDInsight usando modelos do Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Neste artigo, você aprenderá várias maneiras de criar clusters do Azure HDInsight usando modelos do Azure Resource Manager. Para saber mais, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md). Para aprender sobre outros recursos e outras ferramentas de criação de cluster, clique no seletor de guia na parte superior dessa página ou consulte [Métodos de criação de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Para seguir as instruções neste artigo, você precisará de:

* Uma [assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell e/ou CLI do Azure.

### <a name="resource-manager-templates"></a>Modelos do Gerenciador de Recursos
Um modelo do Resource Manager torna mais fácil criar os seguintes recursos para o seu aplicativo em uma única operação coordenada:
* Clusters HDInsight e seus recursos dependentes (tais como a conta de armazenamento padrão)
* Outros recursos (tais como o Banco de Dados SQL do Azure para usar o Apache Sqoop)

No modelo, você deve definir os recursos que são necessários para o aplicativo. Você também pode especificar parâmetros de implantação para inserir valores para ambientes diferentes. O modelo consiste em JSON e expressões que você pode usar para criar valores para sua implantação.

É possível encontrar amostras de modelo do HDInsight em [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Use o [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) de plataforma cruzada com a [extensão do Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um editor de texto para salvar o modelo em um arquivo da estação de trabalho. 

Para obter mais informações sobre modelos do Resource Manager, consulte os seguintes artigos:

* [Criar modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Implantar um aplicativo com o modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Gerar modelos

O Resource Manager permite que você exporte um modelo do Resource Manager dos recursos existentes em sua assinatura usando diferentes ferramentas. Você pode usar esse modelo gerado para saber mais sobre a sintaxe do modelo ou automatizar a reimplantação de sua solução, conforme o necessário.

- Portal do Azure: consulte [Exportar um modelo do Azure Resource Manager dos recursos existentes](../azure-resource-manager/resource-manager-export-template.md).
- Azure PowerShell: consulte [Exportar modelos do Azure Resource Manager com o PowerShell](../azure-resource-manager/resource-manager-export-template-powershell.md).
- CLI do Azure: consulte [Exportar modelos do Azure Resource Manager com a CLI do Azure](../azure-resource-manager/resource-manager-export-template-cli.md).


## <a name="deploy-using-the-portal"></a>Implantar usando o portal

Você pode implantar um modelo do Resource Manager usando o portal do Azure. Para obter mais informações, consulte [Implantar recursos de modelo personalizado](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template).

## <a name="deploy-using-powershell"></a>Implantar usando o PowerShell

Você pode implantar um modelo do Resource Manager usando o Azure PowerShell. Para obter mais informações, consulte [Implantar recursos com modelos do Resource Manager e do Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md) e [implantar modelo do Resource Manager privado com o token SAS e o Azure PowerShell](../azure-resource-manager/resource-manager-powershell-sas-token.md).

## <a name="deploy-using-cli"></a>Implantar usando a CLI

Você pode implantar um modelo do Resource Manager usando a CLI do Azure. Para obter mais informações, consulte [Implantar recursos com modelos do Resource Manager e da CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e [implantar modelo do Resource Manager privado com o token SAS e a CLI do Azure](../azure-resource-manager/resource-manager-cli-sas-token.md).

## <a name="deploy-using-the-rest-api"></a>Implantar usando a API REST
Você pode implantar um modelo do Resource Manager usando a API REST. Para obter mais informações, consulte [Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Implantação com o Visual Studio
 Use o Visual Studio para criar um projeto do grupo de recursos e implantá-lo ao Azure por meio da interface do usuário. Selecione o tipo de recursos a serem incluídos em seu projeto. Esses recursos são adicionados automaticamente ao modelo do Resource Manager. O projeto também fornece um script do PowerShell para implantar o modelo.

Para obter uma introdução ao uso do Visual Studio com grupos de recursos, veja [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu várias maneiras de criar um cluster HDInsight. Para saber mais, consulte os seguintes artigos:

* Para mais modelos relacionados ao HDInsight, consulte [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).
* Para obter um exemplo de como implantar recursos por meio da biblioteca de cliente do .NET, veja [Implantar recursos usando bibliotecas do .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Para obter um exemplo detalhado de implantação de um aplicativo, confira [Provisionar e implantar microsserviços de forma previsível no Azure](../app-service/app-service-deploy-complex-application-predictably.md).
* Para obter orientação sobre como implantar a solução em ambientes diferentes, confira [Ambientes de desenvolvimento e de teste no Microsoft Azure](../solution-dev-test-environments.md).
* Para saber mais sobre as seções do modelo do Azure Resource Manager, veja [Criando modelos](../azure-resource-manager/resource-group-authoring-templates.md).
* Para obter uma lista das funções que podem ser usadas em um modelo do Azure Resource Manager, veja [Funções do modelo](../azure-resource-manager/resource-group-template-functions.md).