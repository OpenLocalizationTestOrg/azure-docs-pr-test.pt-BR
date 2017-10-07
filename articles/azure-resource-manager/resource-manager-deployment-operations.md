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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Exibir operações de implantação com o Azure Resource Manager


Você pode exibir as operações de saudação para uma implantação por meio do portal do Azure de saudação. Você pode ser mais interessado em ver operações hello quando você recebeu um erro durante a implantação para que este artigo enfoca exibindo operações que falharam. portal de saudação fornece uma interface que permite que você tooeasily erros de saudação de localizar e determinar possíveis correções.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portal
operações de implantação toosee hello, Olá use as etapas a seguir:

1. Olá para grupo de recursos envolvido na implantação hello, observe o status de saudação da última implantação de saudação. Você pode selecionar esse status tooget obter mais detalhes.
   
    ![status da implantação](./media/resource-manager-deployment-operations/deployment-status.png)
2. Consulte o histórico recente de implantação hello. Selecione a implantação de saudação que falhou.
   
    ![status da implantação](./media/resource-manager-deployment-operations/select-deployment.png)
3. Selecione Olá link toosee uma descrição do motivo Olá Falha na implantação. Imagem Olá abaixo, o registro DNS de saudação não é exclusivo.  
   
    ![exibir implantação com falha](./media/resource-manager-deployment-operations/view-error.png)
   
    Essa mensagem de erro deve ser suficiente para que você toobegin de solução de problemas. No entanto, se você precisar obter mais detalhes sobre quais tarefas foram concluídas, você pode exibir operações Olá conforme Olá etapas a seguir.
4. Você pode exibir todas as operações de implantação de saudação em Olá **implantação** folha. Selecione qualquer operação toosee obter mais detalhes.
   
    ![exibir operações](./media/resource-manager-deployment-operations/view-operations.png)
   
    Nesse caso, você ver a conta de armazenamento hello, a rede virtual e o conjunto de disponibilidade foram criados com êxito. Falha do endereço IP público de saudação e outros recursos não foram tentados.
5. Você pode exibir eventos para implantação de saudação selecionando **eventos**.
   
    ![exibir eventos](./media/resource-manager-deployment-operations/view-events.png)
6. Você vê todos os eventos de saudação para implantação de saudação e selecione qualquer um para obter mais detalhes. Observe muito Olá IDs de correlação. Esse valor pode ser útil ao trabalhar com o suporte técnico tootroubleshoot uma implantação.
   
    ![consultar eventos](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget Olá status geral de uma implantação, use Olá **AzureRmResourceGroupDeployment Get** comando. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Ou, você pode filtrar os resultados de saudação para somente as implantações com falha.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Cada implantação inclui várias operações. Cada operação representa uma etapa no processo de implantação de saudação. toodiscover o que deu errado com uma implantação, é geralmente necessário toosee detalhes sobre operações de implantação de saudação. Você pode ver o status de saudação de operações de saudação com **Get-AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Que retorna várias operações com cada um em Olá formato a seguir:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget mais detalhes sobre operações com falha, recuperar propriedades de saudação para operações com **falha** estado.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Que retorna que todos os Olá operações com falha com cada uma em Olá formato a seguir:

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

    Observe Olá serviceRequestId e trackingId Olá para operação de saudação. Olá serviceRequestId pode ser útil ao trabalhar com o suporte técnico tootroubleshoot uma implantação. Você usará trackingId Olá Olá próxima etapa toofocus em uma operação específica.
4. tooget a mensagem de status de saudação de uma determinada operação com falha, use Olá comando a seguir:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Que retorna:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Cada operação de implantação no Azure inclui conteúdo da solicitação e resposta. conteúdo da solicitação Olá é o que você enviou tooAzure durante a implantação (por exemplo, criar uma VM, disco do sistema operacional e outros recursos). conteúdo de resposta de saudação é o Azure enviadas da sua solicitação de implantação. Durante a implantação, você pode usar **DeploymentDebugLogLevel** toospecify de parâmetro que Olá a solicitação de e/ou resposta são mantidas no log de saudação. 

  Obter informações de log Olá e salvá-lo localmente usando Olá comandos do PowerShell a seguir:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>CLI do Azure

1. Obter Olá status geral de uma implantação com hello **Mostrar de implantação de grupo do azure** comando.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Um dos valores retornada de saudação é hello **correlationId**. Esse valor é usado tootrack relacionados a eventos e pode ser útil quando trabalhar com suporte técnico tootroubleshoot uma implantação.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. operações de saudação toosee para uma implantação, use:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Obter informações sobre uma implantação com hello [obter informações sobre uma implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operação.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Em resposta hello, observe em particular Olá **provisioningState**, **correlationId**, e **erro** elementos. Olá **correlationId** usado tootrack relacionados a eventos e pode ser útil quando trabalhar com suporte técnico tootroubleshoot uma implantação.

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

2. Obter informações sobre operações de implantação com hello [liste todas as operações de implantação de modelo](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operação. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    resposta de saudação inclui informações de solicitação de e/ou resposta com base no que você especificou no hello **debugSetting** propriedade durante a implantação.

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


## <a name="next-steps"></a>Próximas etapas
* Para obter ajuda na resolução de erros de implantação específico, consulte [resolver erros comuns ao implantar recursos tooAzure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sobre como usar a atividade de saudação logs toomonitor outros tipos de ações, consulte [toomanage Azure dos logs de atividades de exibição recursos](resource-group-audit.md).
* toovalidate sua implantação antes de executá-lo, consulte [implantar um grupo de recursos com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

