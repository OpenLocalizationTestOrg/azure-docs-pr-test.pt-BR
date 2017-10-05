---
title: "Operações de implantação com o Azure Resource Manager | Microsoft Docs"
description: "Descreve como exibir as operações de implantação do Azure Resource Manager com o portal, o PowerShell, a CLI do Azure e a API REST."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="43fcc-103">Exibir operações de implantação com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43fcc-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="43fcc-104">Você pode exibir as operações para uma implantação por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43fcc-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="43fcc-105">Você pode estar mais interessado em ver as operações quando recebeu um erro durante a implantação para que este artigo foque em exibir as operações que falharam.</span><span class="sxs-lookup"><span data-stu-id="43fcc-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="43fcc-106">O portal fornece uma interface que permite encontrar facilmente os erros e determinar as possíveis correções.</span><span class="sxs-lookup"><span data-stu-id="43fcc-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="43fcc-107">Portal</span><span class="sxs-lookup"><span data-stu-id="43fcc-107">Portal</span></span>
<span data-ttu-id="43fcc-108">Para ver as operações de implantação, use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="43fcc-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="43fcc-109">Para o grupo de recursos envolvido na implantação, observe o status da última implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="43fcc-110">Selecione esse status para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="43fcc-110">You can select this status to get more details.</span></span>
   
    ![status da implantação](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="43fcc-112">Você vê o histórico recente de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-112">You see the recent deployment history.</span></span> <span data-ttu-id="43fcc-113">Selecione a implantação que falhou.</span><span class="sxs-lookup"><span data-stu-id="43fcc-113">Select the deployment that failed.</span></span>
   
    ![status da implantação](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="43fcc-115">Selecione o link para ver uma descrição do motivo da falha na implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="43fcc-116">Na imagem abaixo, o registro DNS não é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="43fcc-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![exibir implantação com falha](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="43fcc-118">Essa mensagem de erro deve ser suficiente para você começar a solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="43fcc-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="43fcc-119">No entanto, se você precisar de mais detalhes sobre quais tarefas foram concluídas, poderá exibir as operações, como mostrado nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="43fcc-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="43fcc-120">Você pode exibir todas as operações de implantação na folha **Implantação**.</span><span class="sxs-lookup"><span data-stu-id="43fcc-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="43fcc-121">Selecione qualquer operação para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="43fcc-121">Select any operation to see more details.</span></span>
   
    ![exibir operações](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="43fcc-123">Neste caso, verá que a conta de armazenamento, a rede virtual e o conjunto de disponibilidades foram criados com êxito.</span><span class="sxs-lookup"><span data-stu-id="43fcc-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="43fcc-124">O endereço IP público falhou e outros recursos não foram tentados.</span><span class="sxs-lookup"><span data-stu-id="43fcc-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="43fcc-125">Você pode exibir os eventos para a implantação selecionando **Eventos**.</span><span class="sxs-lookup"><span data-stu-id="43fcc-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![exibir eventos](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="43fcc-127">Você vê todos os eventos da implantação e seleciona qualquer um para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="43fcc-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="43fcc-128">Observe também a IDs de correlação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="43fcc-129">Esse valor pode ser útil ao trabalhar com o suporte técnico para solucionar um problema de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="43fcc-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43fcc-131">PowerShell</span></span>
1. <span data-ttu-id="43fcc-132">Para obter o status geral de uma implantação, use e comando **Get-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="43fcc-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="43fcc-133">Ou você pode filtrar os resultados para mostrar somente as implantações que falharam.</span><span class="sxs-lookup"><span data-stu-id="43fcc-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="43fcc-134">Cada implantação inclui várias operações.</span><span class="sxs-lookup"><span data-stu-id="43fcc-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="43fcc-135">Cada operação representa uma etapa no processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="43fcc-136">Para descobrir o que deu errado com uma implantação, geralmente você precisa ver os detalhes sobre as operações de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="43fcc-137">É possível ver o status das operações com **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="43fcc-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="43fcc-138">Que retorna várias operações com cada uma no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="43fcc-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="43fcc-139">Para obter mais detalhes sobre as operações com falha, recupere as propriedades das operações com o estado **Falha** .</span><span class="sxs-lookup"><span data-stu-id="43fcc-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="43fcc-140">Retorna todas as operações com falha com cada uma no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="43fcc-140">Which returns all the failed operations with each one in the following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="43fcc-141">Observe serviceRequestId e trackingId para a operação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="43fcc-142">serviceRequestId pode ser útil ao trabalhar com o suporte técnico para solucionar um problema de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="43fcc-143">Você usará trackingId na próxima etapa para focar em uma determinada operação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="43fcc-144">Para obter a mensagem de status de uma determinada operação com falha, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="43fcc-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="43fcc-145">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="43fcc-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="43fcc-146">Cada operação de implantação no Azure inclui conteúdo da solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="43fcc-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="43fcc-147">O conteúdo da solicitação é aquilo que é enviado para o Azure durante a implantação (por exemplo, criar uma VM, disco do sistema operacional e outros recursos).</span><span class="sxs-lookup"><span data-stu-id="43fcc-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="43fcc-148">O conteúdo da resposta é aquilo que o Azure enviou de volta com base em sua solicitação de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="43fcc-149">Durante a implantação, você pode usar o parâmetro **DeploymentDebugLogLevel** para especificar que a solicitação e/ou resposta seja mantida no log.</span><span class="sxs-lookup"><span data-stu-id="43fcc-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="43fcc-150">Você obtém informações do log e salva-as localmente usando os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="43fcc-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="43fcc-151">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="43fcc-151">Azure CLI</span></span>

1. <span data-ttu-id="43fcc-152">Obtenha o status geral de uma implantação com o comando **azure group deployment show** .</span><span class="sxs-lookup"><span data-stu-id="43fcc-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="43fcc-153">Um dos valores retornados é **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="43fcc-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="43fcc-154">Esse valor é usado para acompanhar eventos relacionados e pode ser útil ao trabalhar com o suporte técnico na solução de um problema de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="43fcc-155">Para ver as operações de uma implantação, use:</span><span class="sxs-lookup"><span data-stu-id="43fcc-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="43fcc-156">REST</span><span class="sxs-lookup"><span data-stu-id="43fcc-156">REST</span></span>

1. <span data-ttu-id="43fcc-157">Obtenha informações sobre uma implantação com a operação [Obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="43fcc-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="43fcc-158">Na resposta, observe em particular os elementos **provisioningState**, **correlationId** e **error**.</span><span class="sxs-lookup"><span data-stu-id="43fcc-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="43fcc-159">**correlationId** é usado para acompanhar eventos relacionados e pode ser útil ao trabalhar com o suporte técnico na solução de um problema de implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="43fcc-160">Obtenha informações sobre operações de implantação com a operação [Listar todas as operações de implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List).</span><span class="sxs-lookup"><span data-stu-id="43fcc-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="43fcc-161">A resposta inclui informações de solicitação e/ou resposta com base no que foi especificado na propriedade **debugSetting** durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="43fcc-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="43fcc-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43fcc-162">Next steps</span></span>
* <span data-ttu-id="43fcc-163">Para obter ajuda com a resolução de erros de implantação específicos, veja [Resolver erros comuns ao implantar recursos no Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="43fcc-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="43fcc-164">Para saber mais sobre como usar os logs de atividades para monitorar outros tipos de ação, confira [View activity logs to manage Azure resources](resource-group-audit.md) (Exibir logs de atividades para gerenciar recursos do Azure).</span><span class="sxs-lookup"><span data-stu-id="43fcc-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="43fcc-165">Para validar sua implantação antes de executá-la, consulte [Implantar um grupo de recursos com um modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="43fcc-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

