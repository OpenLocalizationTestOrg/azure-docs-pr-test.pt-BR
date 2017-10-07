---
title: "aaaDeploy um aplicativo web que é vinculado repositório do GitHub tooa | Microsoft Docs"
description: "Use um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo web que contém um projeto de um repositório do GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Implantar um repositório GitHub do web app vinculado tooa
Neste tópico, você aprenderá como toocreate um modelo do Gerenciador de recursos do Azure que implanta um aplicativo web que é vinculado tooa projeto em um repositório do GitHub. Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para o modelo do hello completa, consulte [modelo vinculado de aplicativo da Web de tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>O que você implantará
Com esse modelo, você implantará um aplicativo web que contém o código de saudação de um projeto no GitHub.

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Olá URL para o repositório do GitHub que contém a saudação toodeploy de projeto. Este parâmetro contém um valor padrão, mas esse valor é somente pretendido tooshow você como tooprovide Olá URL para o repositório. Você pode usar esse valor quando o teste Olá modelo, mas você desejará tooprovide Olá URL seu próprio repositório ao trabalhar com o modelo de saudação.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>branch
ramificação de saudação do hello repositório toouse ao implantar o aplicativo hello. é o valor padrão de saudação mestre, mas você pode fornecer o nome de saudação do qualquer branch no repositório de saudação que você deseja toodeploy.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Recursos toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Aplicativo Web
Cria um aplicativo web de saudação que é vinculado toohello projeto no GitHub. 

Especifique nome de saudação do Olá web aplicativo por meio de saudação **siteName** parâmetro e o local de saudação do aplicativo web de saudação por meio de saudação **siteLocation** parâmetro. Em Olá **dependsOn** elemento, o modelo de saudação define Olá web aplicativo como dependente de serviço Olá plano de hospedagem. Porque ele é dependente de saudação plano de hospedagem, Olá web app não é criado até concluir a saudação plano de hospedagem está sendo criado. Olá **dependsOn** elemento é apenas uma ordem de implantação toospecify usado. Se você não marcar Olá web aplicativo como dependente de plano de hospedagem hello, o Azure Resource Manager tentará toocreate ambos os recursos no hello mesmo tempo e você poderá receber um erro se Olá web app for criado antes de saudação plano de hospedagem.

Olá web aplicativo também tem um recurso filho que é definido em **recursos** seção abaixo. Este recurso filho define o controle de origem para projeto Olá implantado com o aplicativo web de saudação. Neste modelo, o controle de origem de saudação será vinculado tooa determinado repositório do GitHub. repositório do GitHub Olá é definido com o código de saudação **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** pode embutir Olá URL do repositório quando desejar toocreate um modelo que implanta repetidamente um único projeto, exigindo o número mínimo de saudação de parâmetros.
Em vez de embutir em código Olá URL do repositório, você pode adicionar um parâmetro de URL do repositório hello e use esse valor para Olá **RepoUrl** propriedade.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>CLI do Azure

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>CLI do Azure 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Para obter conteúdo do arquivo JSON de parâmetros hello, consulte [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

