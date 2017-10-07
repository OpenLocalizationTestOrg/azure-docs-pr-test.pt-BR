---
title: "aaaRetrain um serviço web de aprendizado de máquina do Azure nova com o PowerShell | Microsoft Docs"
description: "Saiba como tooprogrammatically treinar novamente um modelo e uma atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure usando cmdlets do PowerShell de gerenciamento de aprendizado de máquina hello."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Treinar novamente um serviço web do novo Gerenciador de recursos com base usando cmdlets do PowerShell de gerenciamento de aprendizado de máquina Olá
Quando você treinar novamente um novo serviço da web, atualiza Olá web de previsão serviço definição tooreference Olá novo modelo treinado.  

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter configurado um teste de treinamento e um experimento de previsão, como mostrado em [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> experiência de previsão Olá deve ser implantada como uma serviço web de aprendizado de máquina do Azure Resource Manager (novo) com base. toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

Para obter mais informações sobre como implantar os serviços Web, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Esse processo exige que você tenha instalado Olá Cmdlets de aprendizado de máquina do Azure. Para obter informações sobre como instalar os cmdlets de aprendizado de máquina Olá, consulte Olá [Cmdlets de aprendizado de máquina do Azure](https://msdn.microsoft.com/library/azure/mt767952.aspx) referência no MSDN.

Olá copiado informações a seguir da saudação treinamento saída:

* BaseLocation
* RelativeLocation

etapas de saudação executadas são:

1. Entrar tooyour conta do Azure Resource Manager.
2. Obter definição de serviço web Olá
3. Saudação de exportação de definição de serviço Web como JSON
4. Atualização Olá toohello ilearner blob de referência no hello JSON.
5. Importar Olá JSON em uma definição de serviço Web
6. Olá web serviço de atualização com a nova definição de serviço Web

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Entrar tooyour conta de Gerenciador de recursos do Azure
Você deve primeiro entrar no tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition"></a>Obter Olá definição de serviço Web
Em seguida, obtenha Olá serviço Web por chamada hello [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Olá definição de serviço Web é uma representação interna do modelo treinado de saudação do serviço web de saudação e não pode ser modificado diretamente. Certifique-se de que você está recuperando Olá definição de serviço Web para sua experiência de previsão e não sua experiência de treinamento.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

nome do grupo toodetermine Olá recursos de um serviço da web existente, execute o cmdlet de Get-AzureRmMlWebService de saudação sem serviços parâmetros toodisplay Olá web em sua assinatura. Localize o serviço web de saudação e, em seguida, examine a sua ID de serviço da web. nome de Olá Olá do grupo de recursos é quarto elemento Olá Olá ID, logo após Olá *resourceGroups* elemento. Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Como alternativa, toodetermine Olá recurso nome de grupo de um serviço da web existente, o log no portal de serviços Web de aprendizado de máquina do Microsoft Azure toohello. Selecione Olá web service. nome do grupo de recursos de saudação é elemento quinto Olá Olá URL do serviço da web de hello, logo após Olá *resourceGroups* elemento. Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Saudação de exportação de definição de serviço Web como JSON
toomodify Olá definição toohello treinado modelo toouse recentemente Olá treinado, primeiro você deve usar Olá [AzureRmMlWebService de exportação](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport-tooa arquivo no formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Atualização Olá toohello ilearner blob de referência no hello JSON.
Em ativos hello, localize Olá [treinado], atualização Olá *uri* valor Olá *locationInfo* nó com hello URI do blob de ilearner hello. Olá URI é gerado pela combinação Olá *BaseLocation* e hello *RelativeLocation* da saída de saudação de saudação chamada novos treinamentos BES. Isso atualiza Olá caminho tooreference Olá novo modelo treinado.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>Importar Olá JSON em uma definição de serviço Web
Você deve usar o hello [AzureRmMlWebService importação](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Olá modificado arquivo JSON de volta para uma definição de serviço Web que você pode usar o hello tooupdate definição de serviço Web.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Olá web serviço de atualização com a nova definição de serviço Web
Por fim, você use [AzureRmMlWebService atualização](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Olá definição de serviço Web.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Resumo
Usando os cmdlets de gerenciamento do PowerShell de aprendizado de máquina hello, você pode atualizar treinado Olá de um serviço Web previsão habilitar cenários, como:

* Readaptação de modelo periódico com novos dados.
* Distribuição de um modelo toocustomers com objetivo de saudação de permitir que eles treinar novamente o modelo de saudação usando seus próprios dados.

