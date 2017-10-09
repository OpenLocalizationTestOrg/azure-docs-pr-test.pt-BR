---
title: "Serviços Web do Azure Machine Learning: implantação e consumo | Microsoft Docs"
description: "Recursos para implantar e consumir serviços Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Serviços Web do Azure Machine Learning: implantação e consumo
Você pode usar modelos e fluxos de trabalho de aprendizado de máquina toodeploy aprendizado de máquina do Azure como serviços da web. Esses serviços da web, em seguida, podem ser usado toocall Olá aprendizado de máquina modelos de aplicativos em previsões de toodo de Internet Olá em tempo real ou em modo de lote. Porque Olá web serviços RESTful, você pode chamá-los de várias linguagens de programação e plataformas, como o .NET e Java e de aplicativos, como o Excel.

seções a seguir Olá fornecem links toowalkthroughs, código e documentação toohelp começar.

## <a name="deploy-a-web-service"></a>Implantar um serviço Web
### <a name="with-azure-machine-learning-studio"></a>Com o Azure Machine Learning Studio
Estúdio de aprendizado de máquina e o portal de serviços Web de aprendizado de máquina do Microsoft Azure Olá ajudarão-lo a implantar e gerenciar um serviço web sem escrever código.

Olá, links a seguir fornecem informações gerais sobre como toodeploy um novo serviço web:

* Para obter uma visão geral sobre como toodeploy um novo serviço da web com base no Gerenciador de recursos do Azure, consulte [implantar um novo serviço da web](machine-learning-webservice-deploy-a-web-service.md).
* Para obter instruções sobre como toodeploy um serviço web, consulte [implantar um serviço web de aprendizado de máquina do Azure](machine-learning-publish-a-machine-learning-web-service.md).
* Para obter uma explicação completa sobre como toocreate e implantar um serviço web, consulte [passo a passo etapa 1: criar um espaço de trabalho do aprendizado de máquina](machine-learning-walkthrough-1-create-ml-workspace.md).
* Para obter exemplos específicos que implantam um serviço Web, consulte:

  * [Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md)
  * [Como toodeploy um web serviço toomultiple regiões](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Com as APIs do provedor de recursos dos serviços Web (APIs do Azure Resource Manager)
provedor de recursos de aprendizado de máquina do Azure Olá para serviços da web permite que a implantação e gerenciamento de serviços da web usando chamadas da API REST. Para obter mais detalhes, veja a referência [Serviço Web do Machine Learning (REST)](/rest/api/machinelearning/index).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Com os cmdlets do PowerShell
O provedor de recursos do Azure Machine Learning para serviços Web permite a implantação e o gerenciamento dos serviços Web usando cmdlets do PowerShell.

toouse Olá cmdlets, você deve primeiro entrar tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Se você estiver familiarizado com como toocall PowerShell os comandos que se baseiam no Gerenciador de recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport testar sua previsão, use [esse código de exemplo](https://github.com/ritwik20/AzureML-WebServices). Depois de criar o arquivo de .exe de saudação do código hello, você pode digitar:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Executar o aplicativo hello cria um modelo JSON de serviço da web. toouse Olá modelo toodeploy um serviço web, você deve adicionar Olá informações a seguir:

* Nome e chave da conta de armazenamento

    Você pode obter Olá nome de conta de armazenamento e chave de qualquer Olá [portal do Azure](https://portal.azure.com/) ou hello [portal clássico do Azure](http://manage.windowsazure.com/).
* ID do plano de compromisso

    Você pode obter o ID do plano de saudação do hello [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal entrar e clicando em um nome de plano.

Adicioná-los toohello modelo JSON como filhos do hello *propriedades* nó na saudação de mesmo nível como Olá *MachineLearningWorkspace* nó.

Aqui está um exemplo:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Consulte Olá artigos a seguir e exemplo de código para obter detalhes adicionais:

* 
            [cmdlets do Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) no MSDN
* [Passo a passo](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) de exemplo no GitHub

## <a name="consume-hello-web-services"></a>Consumir serviços web de saudação
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>De saudação serviços da Web de aprendizado do Azure máquina UI (teste)
Você pode testar o serviço web do portal de serviços de Web de aprendizado de máquina do Azure hello. Isso inclui o serviço de solicitação-resposta hello (RR) de teste e interfaces de serviço de execução de lote (BES).

* [Implantar um novo serviço Web](machine-learning-webservice-deploy-a-web-service.md)
* 
            [Implantar um serviço Web de Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Etapa 5 do passo a passo: Implantar o serviço de web de aprendizado de máquina do Azure Olá](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>No Excel
Você pode baixar um modelo do Excel que consome Olá web serviço:

* [Consumindo um Serviço Web do Azure Machine Learning por meio do Excel](machine-learning-consuming-from-excel.md)
* [Suplemento do Excel para Serviços Web do Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Em um cliente baseado em REST
Os Serviços Web do Azure Machine Learning são APIs RESTful. Você pode usar essas APIs de várias plataformas, como .NET, Python, R, Java, Olá etc. **consumir** página para seu serviço da web em Olá [portal de serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net) tem exemplo código que pode ajudá-lo a começar. Para obter mais informações, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).
