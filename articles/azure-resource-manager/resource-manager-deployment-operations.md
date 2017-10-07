---
title: "aaaDeployment operações com o Gerenciador de recursos do Azure | Microsoft Docs"
description: "Descreve como operações de implantação do Azure Resource Manager tooview com hello portal, PowerShell, CLI do Azure e API REST."
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
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="436de-103">Exibir operações de implantação com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="436de-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="436de-104">Você pode exibir as operações de saudação para uma implantação por meio do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="436de-105">Você pode ser mais interessado em ver operações hello quando você recebeu um erro durante a implantação para que este artigo enfoca exibindo operações que falharam.</span><span class="sxs-lookup"><span data-stu-id="436de-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="436de-106">portal de saudação fornece uma interface que permite que você tooeasily erros de saudação de localizar e determinar possíveis correções.</span><span class="sxs-lookup"><span data-stu-id="436de-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="436de-107">Portal</span><span class="sxs-lookup"><span data-stu-id="436de-107">Portal</span></span>
<span data-ttu-id="436de-108">operações de implantação toosee hello, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="436de-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="436de-109">Olá para grupo de recursos envolvido na implantação hello, observe o status de saudação da última implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="436de-110">Você pode selecionar esse status tooget obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="436de-110">You can select this status tooget more details.</span></span>
   
    ![status da implantação](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="436de-112">Consulte o histórico recente de implantação hello.</span><span class="sxs-lookup"><span data-stu-id="436de-112">You see hello recent deployment history.</span></span> <span data-ttu-id="436de-113">Selecione a implantação de saudação que falhou.</span><span class="sxs-lookup"><span data-stu-id="436de-113">Select hello deployment that failed.</span></span>
   
    ![status da implantação](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="436de-115">Selecione Olá link toosee uma descrição do motivo Olá Falha na implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="436de-116">Imagem Olá abaixo, o registro DNS de saudação não é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="436de-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![exibir implantação com falha](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="436de-118">Essa mensagem de erro deve ser suficiente para que você toobegin de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="436de-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="436de-119">No entanto, se você precisar obter mais detalhes sobre quais tarefas foram concluídas, você pode exibir operações Olá conforme Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="436de-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="436de-120">Você pode exibir todas as operações de implantação de saudação em Olá **implantação** folha.</span><span class="sxs-lookup"><span data-stu-id="436de-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="436de-121">Selecione qualquer operação toosee obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="436de-121">Select any operation toosee more details.</span></span>
   
    ![exibir operações](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="436de-123">Nesse caso, você ver a conta de armazenamento hello, a rede virtual e o conjunto de disponibilidade foram criados com êxito.</span><span class="sxs-lookup"><span data-stu-id="436de-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="436de-124">Falha do endereço IP público de saudação e outros recursos não foram tentados.</span><span class="sxs-lookup"><span data-stu-id="436de-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="436de-125">Você pode exibir eventos para implantação de saudação selecionando **eventos**.</span><span class="sxs-lookup"><span data-stu-id="436de-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![exibir eventos](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="436de-127">Você vê todos os eventos de saudação para implantação de saudação e selecione qualquer um para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="436de-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="436de-128">Observe muito Olá IDs de correlação.</span><span class="sxs-lookup"><span data-stu-id="436de-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="436de-129">Esse valor pode ser útil ao trabalhar com o suporte técnico tootroubleshoot uma implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="436de-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="436de-131">PowerShell</span></span>
1. <span data-ttu-id="436de-132">tooget Olá status geral de uma implantação, use Olá **AzureRmResourceGroupDeployment Get** comando.</span><span class="sxs-lookup"><span data-stu-id="436de-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="436de-133">Ou, você pode filtrar os resultados de saudação para somente as implantações com falha.</span><span class="sxs-lookup"><span data-stu-id="436de-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="436de-134">Cada implantação inclui várias operações.</span><span class="sxs-lookup"><span data-stu-id="436de-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="436de-135">Cada operação representa uma etapa no processo de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="436de-136">toodiscover o que deu errado com uma implantação, é geralmente necessário toosee detalhes sobre operações de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="436de-137">Você pode ver o status de saudação de operações de saudação com **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="436de-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="436de-138">Que retorna várias operações com cada um em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="436de-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="436de-139">tooget mais detalhes sobre operações com falha, recuperar propriedades de saudação para operações com **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="436de-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="436de-140">Que retorna que todos os Olá operações com falha com cada uma em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="436de-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="436de-141">Observe Olá serviceRequestId e trackingId Olá para operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="436de-142">Olá serviceRequestId pode ser útil ao trabalhar com o suporte técnico tootroubleshoot uma implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="436de-143">Você usará trackingId Olá Olá próxima etapa toofocus em uma operação específica.</span><span class="sxs-lookup"><span data-stu-id="436de-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="436de-144">tooget a mensagem de status de saudação de uma determinada operação com falha, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="436de-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="436de-145">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="436de-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="436de-146">Cada operação de implantação no Azure inclui conteúdo da solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="436de-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="436de-147">conteúdo da solicitação Olá é o que você enviou tooAzure durante a implantação (por exemplo, criar uma VM, disco do sistema operacional e outros recursos).</span><span class="sxs-lookup"><span data-stu-id="436de-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="436de-148">conteúdo de resposta de saudação é o Azure enviadas da sua solicitação de implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="436de-149">Durante a implantação, você pode usar **DeploymentDebugLogLevel** toospecify de parâmetro que Olá a solicitação de e/ou resposta são mantidas no log de saudação.</span><span class="sxs-lookup"><span data-stu-id="436de-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="436de-150">Obter informações de log Olá e salvá-lo localmente usando Olá comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="436de-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="436de-151">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="436de-151">Azure CLI</span></span>

1. <span data-ttu-id="436de-152">Obter Olá status geral de uma implantação com hello **Mostrar de implantação de grupo do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="436de-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="436de-153">Um dos valores retornada de saudação é hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="436de-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="436de-154">Esse valor é usado tootrack relacionados a eventos e pode ser útil quando trabalhar com suporte técnico tootroubleshoot uma implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="436de-155">operações de saudação toosee para uma implantação, use:</span><span class="sxs-lookup"><span data-stu-id="436de-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="436de-156">REST</span><span class="sxs-lookup"><span data-stu-id="436de-156">REST</span></span>

1. <span data-ttu-id="436de-157">Obter informações sobre uma implantação com hello [obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="436de-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="436de-158">Em resposta hello, observe em particular Olá **provisioningState**, **correlationId**, e **erro** elementos.</span><span class="sxs-lookup"><span data-stu-id="436de-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="436de-159">Olá **correlationId** usado tootrack relacionados a eventos e pode ser útil quando trabalhar com suporte técnico tootroubleshoot uma implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="436de-160">Obter informações sobre operações de implantação com hello [liste todas as operações de implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operação.</span><span class="sxs-lookup"><span data-stu-id="436de-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="436de-161">resposta de saudação inclui informações de solicitação de e/ou resposta com base no que você especificou no hello **debugSetting** propriedade durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="436de-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="436de-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="436de-162">Next steps</span></span>
* <span data-ttu-id="436de-163">Para obter ajuda na resolução de erros de implantação específico, consulte [resolver erros comuns ao implantar recursos tooAzure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="436de-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="436de-164">toolearn sobre como usar a atividade de saudação logs toomonitor outros tipos de ações, consulte [toomanage Azure dos logs de atividades de exibição recursos](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="436de-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="436de-165">toovalidate sua implantação antes de executá-lo, consulte [implantar um grupo de recursos com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="436de-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

