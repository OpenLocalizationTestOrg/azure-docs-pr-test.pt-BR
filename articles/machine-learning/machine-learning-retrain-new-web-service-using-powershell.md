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
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="2c2ed-103">Treinar novamente um serviço web do novo Gerenciador de recursos com base usando cmdlets do PowerShell de gerenciamento de aprendizado de máquina Olá</span><span class="sxs-lookup"><span data-stu-id="2c2ed-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="2c2ed-104">Quando você treinar novamente um novo serviço da web, atualiza Olá web de previsão serviço definição tooreference Olá novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="2c2ed-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c2ed-105">Prerequisites</span></span>
<span data-ttu-id="2c2ed-106">Você deve ter configurado um teste de treinamento e um experimento de previsão, como mostrado em [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ed-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2c2ed-107">experiência de previsão Olá deve ser implantada como uma serviço web de aprendizado de máquina do Azure Resource Manager (novo) com base.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="2c2ed-108">toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="2c2ed-109">Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ed-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="2c2ed-110">Para obter mais informações sobre como implantar os serviços Web, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ed-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="2c2ed-111">Esse processo exige que você tenha instalado Olá Cmdlets de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="2c2ed-112">Para obter informações sobre como instalar os cmdlets de aprendizado de máquina Olá, consulte Olá [Cmdlets de aprendizado de máquina do Azure](https://msdn.microsoft.com/library/azure/mt767952.aspx) referência no MSDN.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="2c2ed-113">Olá copiado informações a seguir da saudação treinamento saída:</span><span class="sxs-lookup"><span data-stu-id="2c2ed-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="2c2ed-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="2c2ed-114">BaseLocation</span></span>
* <span data-ttu-id="2c2ed-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="2c2ed-115">RelativeLocation</span></span>

<span data-ttu-id="2c2ed-116">etapas de saudação executadas são:</span><span class="sxs-lookup"><span data-stu-id="2c2ed-116">hello steps you take are:</span></span>

1. <span data-ttu-id="2c2ed-117">Entrar tooyour conta do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="2c2ed-118">Obter definição de serviço web Olá</span><span class="sxs-lookup"><span data-stu-id="2c2ed-118">Get hello web service definition</span></span>
3. <span data-ttu-id="2c2ed-119">Saudação de exportação de definição de serviço Web como JSON</span><span class="sxs-lookup"><span data-stu-id="2c2ed-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="2c2ed-120">Atualização Olá toohello ilearner blob de referência no hello JSON.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="2c2ed-121">Importar Olá JSON em uma definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2c2ed-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="2c2ed-122">Olá web serviço de atualização com a nova definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2c2ed-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="2c2ed-123">Entrar tooyour conta de Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2c2ed-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="2c2ed-124">Você deve primeiro entrar no tooyour conta do Azure a partir de ambiente do PowerShell hello usando Olá [AzureRmAccount adicionar](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="2c2ed-125">Obter Olá definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2c2ed-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="2c2ed-126">Em seguida, obtenha Olá serviço Web por chamada hello [AzureRmMlWebService Get](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="2c2ed-127">Olá definição de serviço Web é uma representação interna do modelo treinado de saudação do serviço web de saudação e não pode ser modificado diretamente.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="2c2ed-128">Certifique-se de que você está recuperando Olá definição de serviço Web para sua experiência de previsão e não sua experiência de treinamento.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="2c2ed-129">nome do grupo toodetermine Olá recursos de um serviço da web existente, execute o cmdlet de Get-AzureRmMlWebService de saudação sem serviços parâmetros toodisplay Olá web em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="2c2ed-130">Localize o serviço web de saudação e, em seguida, examine a sua ID de serviço da web.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="2c2ed-131">nome de Olá Olá do grupo de recursos é quarto elemento Olá Olá ID, logo após Olá *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="2c2ed-132">Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="2c2ed-133">Como alternativa, toodetermine Olá recurso nome de grupo de um serviço da web existente, o log no portal de serviços Web de aprendizado de máquina do Microsoft Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="2c2ed-134">Selecione Olá web service.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-134">Select hello web service.</span></span> <span data-ttu-id="2c2ed-135">nome do grupo de recursos de saudação é elemento quinto Olá Olá URL do serviço da web de hello, logo após Olá *resourceGroups* elemento.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="2c2ed-136">Olá exemplo a seguir, nome do grupo de recursos de saudação é SouthCentralUS-MachineLearning-padrão.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="2c2ed-137">Saudação de exportação de definição de serviço Web como JSON</span><span class="sxs-lookup"><span data-stu-id="2c2ed-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="2c2ed-138">toomodify Olá definição toohello treinado modelo toouse recentemente Olá treinado, primeiro você deve usar Olá [AzureRmMlWebService de exportação](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport-tooa arquivo no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="2c2ed-139">Atualização Olá toohello ilearner blob de referência no hello JSON.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="2c2ed-140">Em ativos hello, localize Olá [treinado], atualização Olá *uri* valor Olá *locationInfo* nó com hello URI do blob de ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="2c2ed-141">Olá URI é gerado pela combinação Olá *BaseLocation* e hello *RelativeLocation* da saída de saudação de saudação chamada novos treinamentos BES.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="2c2ed-142">Isso atualiza Olá caminho tooreference Olá novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="2c2ed-143">Importar Olá JSON em uma definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2c2ed-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="2c2ed-144">Você deve usar o hello [AzureRmMlWebService importação](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert Olá modificado arquivo JSON de volta para uma definição de serviço Web que você pode usar o hello tooupdate definição de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="2c2ed-145">Olá web serviço de atualização com a nova definição de serviço Web</span><span class="sxs-lookup"><span data-stu-id="2c2ed-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="2c2ed-146">Por fim, você use [AzureRmMlWebService atualização](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate Olá definição de serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="2c2ed-147">Resumo</span><span class="sxs-lookup"><span data-stu-id="2c2ed-147">Summary</span></span>
<span data-ttu-id="2c2ed-148">Usando os cmdlets de gerenciamento do PowerShell de aprendizado de máquina hello, você pode atualizar treinado Olá de um serviço Web previsão habilitar cenários, como:</span><span class="sxs-lookup"><span data-stu-id="2c2ed-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="2c2ed-149">Readaptação de modelo periódico com novos dados.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="2c2ed-150">Distribuição de um modelo toocustomers com objetivo de saudação de permitir que eles treinar novamente o modelo de saudação usando seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="2c2ed-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

