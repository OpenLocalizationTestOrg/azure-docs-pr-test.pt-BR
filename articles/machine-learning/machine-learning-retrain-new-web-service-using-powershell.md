---
title: "Treinar novamente um novo serviço Web do Azure Machine Learning com o PowerShell | Microsoft Docs"
description: "Saiba como readaptar um modelo de forma programática e atualizar o serviço Web para usar o modelo treinado recentemente no Machine Learning do Azure usando os cmdlets do PowerShell de Gerenciamento do Machine Learning."
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
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="2f2de-103">Readaptar um novo serviço Web baseado no Resource Manager usando os cmdlets do PowerShell de Gerenciamento do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2f2de-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="2f2de-104">Quando você readapta um novo serviço Web, também atualiza a definição do serviço Web de previsão para fazer referenciar ao novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="2f2de-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="2f2de-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f2de-105">Prerequisites</span></span>
<span data-ttu-id="2f2de-106">Você deve ter configurado um teste de treinamento e um experimento de previsão, como mostrado em [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="2f2de-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2f2de-107">O experimento de previsão deve ser implantado como um serviço Web do Machine Learning do Azure Resource Manager (novo).</span><span class="sxs-lookup"><span data-stu-id="2f2de-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="2f2de-108">Para implantar um novo serviço Web, você precisa ter permissões suficientes na assinatura na qual o serviço Web está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="2f2de-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="2f2de-109">Para saber mais, confira [Gerenciar um serviço Web usando o portal de Serviços Web do Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="2f2de-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="2f2de-110">Para obter mais informações sobre como implantar os serviços Web, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2f2de-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="2f2de-111">Esse processo exige que você tenha instalado os Cmdlets do Machine Learning do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f2de-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="2f2de-112">Para obter informações sobre como instalar os cmdlets do Machine Learning, consulte a referência [Cmdlets do Machine Learning do Azure](https://msdn.microsoft.com/library/azure/mt767952.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="2f2de-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="2f2de-113">Copiar as informações a seguir da saída da readaptação:</span><span class="sxs-lookup"><span data-stu-id="2f2de-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="2f2de-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="2f2de-114">BaseLocation</span></span>
* <span data-ttu-id="2f2de-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="2f2de-115">RelativeLocation</span></span>

<span data-ttu-id="2f2de-116">As etapas são:</span><span class="sxs-lookup"><span data-stu-id="2f2de-116">The steps you take are:</span></span>

1. <span data-ttu-id="2f2de-117">Entre sua conta do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f2de-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="2f2de-118">Obter a definição do serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-118">Get the web service definition</span></span>
3. <span data-ttu-id="2f2de-119">Exportar a Definição do Serviço Web como JSON</span><span class="sxs-lookup"><span data-stu-id="2f2de-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="2f2de-120">Atualize a referência para o blob ilearner no JSON.</span><span class="sxs-lookup"><span data-stu-id="2f2de-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="2f2de-121">Importar o JSON para uma Definição do Serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="2f2de-122">Atualizar o serviço Web com a nova Definição do Serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="2f2de-123">Entrar em sua conta do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f2de-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="2f2de-124">Primeiro, você deve entrar em sua conta do Azure no ambiente do PowerShell usando o cmdlet [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2f2de-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="2f2de-125">Obter a definição do serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-125">Get the Web Service Definition</span></span>
<span data-ttu-id="2f2de-126">Em seguida, obtenha o Serviço Web chamando o cmdlet [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2f2de-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="2f2de-127">A definição do serviço Web é uma representação interna do modelo treinado do serviço Web e não pode ser modificada diretamente.</span><span class="sxs-lookup"><span data-stu-id="2f2de-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="2f2de-128">Verifique se você está recuperando a definição do serviço Web para seu experimento de previsão, e não seu teste de treinamento.</span><span class="sxs-lookup"><span data-stu-id="2f2de-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="2f2de-129">Para determinar o nome do grupo de recursos de um serviço Web existente, execute o cmdlet Get-AzureRmMlWebService sem parâmetros para exibir os serviços Web em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2f2de-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="2f2de-130">Localize o serviço Web e examine sua ID de serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="2f2de-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="2f2de-131">O nome do grupo de recursos é o quarto elemento na ID, logo após o elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="2f2de-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="2f2de-132">No exemplo a seguir, o nome do grupo de recursos é Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="2f2de-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="2f2de-133">Como alternativa, para determinar o nome do grupo de recursos de um serviço Web existente, faça logon no portal de serviços Web do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2f2de-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="2f2de-134">Selecione o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2f2de-134">Select the web service.</span></span> <span data-ttu-id="2f2de-135">O nome do grupo de recursos é o quinto elemento da URL do serviço Web, logo após o elemento *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="2f2de-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="2f2de-136">No exemplo a seguir, o nome do grupo de recursos é Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="2f2de-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="2f2de-137">Exportar a Definição do Serviço Web como JSON</span><span class="sxs-lookup"><span data-stu-id="2f2de-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="2f2de-138">Para modificar a definição para o modelo treinado usar o Modelo Treinado recentemente, primeiro você deve usar o cmdlet [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) para exportá-lo para um arquivo no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2f2de-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="2f2de-139">Atualize a referência para o blob ilearner no JSON.</span><span class="sxs-lookup"><span data-stu-id="2f2de-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="2f2de-140">Nos ativos, localize o [modelo treinado] e atualize o valor *uri* no nó *locationInfo* com o URI do blob ilearner.</span><span class="sxs-lookup"><span data-stu-id="2f2de-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="2f2de-141">O URI é gerado combinando *BaseLocation* e *RelativeLocation* na saída da chamada de readaptação BES.</span><span class="sxs-lookup"><span data-stu-id="2f2de-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="2f2de-142">Isso atualiza o caminho para referenciar o novo modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="2f2de-142">This updates the path to reference the new trained model.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="2f2de-143">Importar o JSON para uma Definição do Serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="2f2de-144">É necessário usar o cmdlet [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) para converter o arquivo JSON modificado novamente para uma Definição do Serviço Web que você pode usar para atualizá-lo.</span><span class="sxs-lookup"><span data-stu-id="2f2de-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="2f2de-145">Atualizar o serviço Web com a nova Definição do Serviço Web</span><span class="sxs-lookup"><span data-stu-id="2f2de-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="2f2de-146">Finalmente, use o cmdlet [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) para atualizar a Definição do Serviço Web.</span><span class="sxs-lookup"><span data-stu-id="2f2de-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="2f2de-147">Resumo</span><span class="sxs-lookup"><span data-stu-id="2f2de-147">Summary</span></span>
<span data-ttu-id="2f2de-148">Usando os cmdlets de gerenciamento do PowerShell de Machine Learning, você pode atualizar o modelo treinado de um Serviço Web de previsão habilitando cenários, como:</span><span class="sxs-lookup"><span data-stu-id="2f2de-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="2f2de-149">Readaptação de modelo periódico com novos dados.</span><span class="sxs-lookup"><span data-stu-id="2f2de-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="2f2de-150">A distribuição de um modelo para os clientes com o objetivo de permitir que eles recuperem o modelo usando seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="2f2de-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

