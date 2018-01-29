---
title: "Serviços Web do Azure Machine Learning: implantação e consumo | Microsoft Docs"
description: "Recursos para implantar e consumir serviços Web."
services: machine-learning
documentationcenter: 
author: garyericson
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
ms.openlocfilehash: b0afbd54ddad4cc4be2b35c85d81abe90c717692
ms.sourcegitcommit: 42ee5ea09d9684ed7a71e7974ceb141d525361c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/09/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Serviços Web do Azure Machine Learning: implantação e consumo
Você pode usar o Azure Machine Learning para implantar fluxos de trabalho e modelos de aprendizado de máquina como serviços Web. Esses serviços Web podem ser usados para chamar os modelos de aprendizado de máquina de aplicativos pela Internet para fazer previsões em tempo real ou no modo de lote. Como os serviços Web são RESTful, você pode chamá-los por meio de várias linguagens de programação e plataformas, como .NET e Java, e de aplicativos, como o Excel.

As próximas seções fornecem links para passo a passos, código e documentação para ajudá-lo a se familiarizar.

## <a name="deploy-a-web-service"></a>Implantar um serviço Web

### <a name="with-azure-machine-learning-studio"></a>Com o Azure Machine Learning Studio
O Machine Learning Studio e o portal dos Serviços Web do Microsoft Azure Machine Learning ajudam a implantar e gerenciar um serviço Web sem a necessidade de escrever código.

Os seguintes links fornecem informações gerais sobre como implantar um novo serviço Web:

* Para obter uma visão geral de como implantar um novo serviço Web baseado no Azure Resource Manager, consulte [Implantar um novo serviço Web](publish-a-machine-learning-web-service.md).
* Para ver um passo a passo de como implantar um serviço Web, consulte [Implantar um serviço Web do Azure Machine Learning](publish-a-machine-learning-web-service.md).
* Para obter um passo a passo completo de como criar e implantar um serviço Web, consulte [Etapa 1 do passo a passo: Criar um espaço de trabalho do Machine Learning](walkthrough-1-create-ml-workspace.md).
* Para obter exemplos específicos que implantam um serviço Web, consulte:

  * [Etapa 5 do passo-a-passo: Implantar o serviço Web de Azure Machine Learning](walkthrough-5-publish-web-service.md)
  * [Como implantar um serviço Web em várias regiões](how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Com as APIs do provedor de recursos dos serviços Web (APIs do Azure Resource Manager)
O provedor de recursos do Azure Machine Learning para serviços Web permite a implantação e o gerenciamento dos serviços Web usando chamadas à API REST. Para obter mais detalhes, veja a referência [Serviço Web do Machine Learning (REST)](/rest/api/machinelearning/index).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Com os cmdlets do PowerShell
O provedor de recursos do Azure Machine Learning para serviços Web permite a implantação e o gerenciamento dos serviços Web usando cmdlets do PowerShell.

Para usar os cmdlets, primeiro você deve entrar em sua conta do Azure no ambiente do PowerShell usando o cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) . Se não souber como chamar comandos do PowerShell baseados no Resource Manager, consulte [Usando o Azure PowerShell com o Azure Resource Manager](../../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

Para exportar seu experimento preditivo, use este [código de exemplo](https://github.com/ritwik20/AzureML-WebServices). Depois de criar o arquivo .exe com base no código, você pode digitar:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Executar o aplicativo cria um modelo JSON do serviço Web. Para usar o modelo para implantar um serviço Web, você deve adicionar as seguintes informações:

* Nome e chave da conta de armazenamento

    É possível obter o nome e a chave da conta de armazenamento no [portal do Azure](https://portal.azure.com/).
* ID do plano de compromisso

    Você pode obter a ID do plano no portal [Serviços Web do Azure Machine Learning](https://services.azureml.net) fazendo logon e clicando no nome de um plano.

Adicione-a ao modelo JSON como filho do nó *Properties* no mesmo nível do nó *MachineLearningWorkspace*.

Aqui está um exemplo:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Consulte os seguintes artigos e o código de exemplo para obter mais detalhes:

* [cmdlets do Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) no MSDN
* [Passo a passo](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) de exemplo no GitHub

## <a name="consume-the-web-services"></a>Consumir os serviços Web
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a>Na interface do usuário dos Serviços Web do Azure Machine Learning (Teste)
Você pode testar o serviço Web no portal dos Serviços Web do Azure Machine Learning. Isso inclui o teste das interfaces do RRS (serviço de Solicitação-Resposta) e do BES (serviço de Execução em Lotes).

* [Implantar um novo serviço Web](publish-a-machine-learning-web-service.md)
* [Implantar um serviço Web de Azure Machine Learning](publish-a-machine-learning-web-service.md)
* [Etapa 5 do passo-a-passo: Implantar o serviço Web de Azure Machine Learning](walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>No Excel
Você pode baixar um modelo do Excel que consome o serviço Web:

* [Consumindo um Serviço Web do Azure Machine Learning por meio do Excel](consuming-from-excel.md)
* [Suplemento do Excel para Serviços Web do Azure Machine Learning](excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Em um cliente baseado em REST
Os Serviços Web do Azure Machine Learning são APIs RESTful. Você pode consumir essas APIs em várias plataformas, como .NET, Python, R, Java, etc. A página **Consumo** do serviço Web no [portal dos Serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net) traz um código de exemplo que pode ajudá-lo a se familiarizar. Para saber mais, veja [Como consumir um serviço Web do Azure Machine Learning](consume-web-services.md).
