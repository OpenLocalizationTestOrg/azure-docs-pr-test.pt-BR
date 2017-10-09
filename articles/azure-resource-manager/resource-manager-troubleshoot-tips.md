---
title: "erros de implantação do Azure aaaUnderstand | Microsoft Docs"
description: "Descreve como toolearn sobre erros de implantação do Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erro de implantação, implantação do azure, implantar tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Entender os erros de implantação do Azure
Este tópico descreve os erros de implantação e como você pode descobrir mais informações sobre um erro. Para erros de implantação toocommon resoluções, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Dois tipos de erros
Há dois tipos de erros que você pode receber:

* erros de validação
* erros de implantação

Olá a imagem a seguir mostra o log de atividades de saudação para uma assinatura. Ela representa duas implantações. Em uma implantação, de falha de validação no modelo de saudação (**validar**) e não prosseguir. Em Olá outra implantação, modelo Olá passou na validação, mas falha ao criar recursos de saudação (**implantações gravar**). 

![mostrar código de erro](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Erros de validação ocorrem em cenários que podem ser determinados antes da implantação. Eles incluem erros de sintaxe em seu modelo, ou tentar recursos toodeploy que excedem suas cotas de assinatura. Erros de implantação são provenientes de condições que ocorrem durante o processo de implantação hello. Eles incluem tentar tooaccess um recurso que está sendo implantado em paralelo.

Ambos os tipos de retorno de erros que você use a implantação de saudação tootroubleshoot um código de erro. Os dois tipos de erros aparecem no hello [log de atividades](resource-group-audit.md). No entanto, erros de validação não aparecem no seu histórico de implantação porque a implantação de saudação nunca foi iniciada.

## <a name="determine-error-code"></a>Determinar o código de erro

Você pode aprender sobre um erro ao examinar a mensagem de saudação do erro e o código de erro de saudação. Olá [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md) artigo lista resoluções por código de erro. Este tópico mostra como toouse Olá código de erro de saudação toodiscover portal do Azure.

### <a name="validation-errors"></a>Erros de validação

Durante a implantação por meio do portal hello, você verá um erro de validação depois de enviar seus valores.

![mostrar erro de validação no portal](./media/resource-manager-troubleshoot-tips/validation-error.png)

Selecione a mensagem de saudação para obter mais detalhes. Olá a imagem a seguir, verá um **InvalidTemplateDeployment** erro e uma mensagem que indica uma diretiva de implantação está bloqueado.

![mostrar detalhes da validação](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Erros de implantação

Quando a operação Olá aprovado na validação, mas falha durante a implantação, você verá o erro de saudação em notificações de saudação. Selecione Olá notificação.

![erro de notificação](./media/resource-manager-troubleshoot-tips/notification.png)

Você ver mais detalhes sobre a implantação de saudação. Selecione Olá opção toofind obter mais informações sobre o erro de saudação.

![falha na implantação](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Você ver códigos de erros e de mensagens de erro de saudação. Observe que há dois códigos de erro. Olá primeiro código de erro (**DeploymentFailed**) é um erro geral que não fornece Olá detalhes que você precisa de erro de saudação toosolve. Olá segundo código de erro (**StorageAccountNotFound**) fornece detalhes de saudação é necessário. 

![detalhes do erro](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Habilitar o log de depuração
Às vezes você precisa obter mais informações sobre Olá toodiscover de solicitação e resposta que deu errado. Usando o PowerShell ou a CLI do Azure, você pode solicitar que informações adicionais sejam registradas durante a implantação.

- PowerShell

   No PowerShell, defina Olá **DeploymentDebugLogLevel** parâmetro tooAll, ResponseContent ou RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Examine o conteúdo da solicitação Olá com hello cmdlet a seguir:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   Ou então, Olá conteúdo da resposta:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Essas informações podem ajudá-lo a determinar se um valor no modelo hello está sendo definido incorretamente.

- CLI do Azure

   Examine as operações de implantação Olá com hello comando a seguir:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Modelo aninhado

   toolog as informações de depuração para um modelo aninhado, use Olá **debugSetting** elemento.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Criar um modelo de solução de problemas
Em alguns casos, Olá tootroubleshoot de maneira mais fácil o modelo for tootest partes dele. Você pode criar um modelo simplificado que permite que você toofocus parte Olá achar que está causando o erro de saudação. Por exemplo, suponha que você esteja recebendo um erro ao fazer referência a um recurso. Em vez de lidar com um modelo inteiro, crie um modelo que retorna a parte de saudação que possam estar causando o problema. Ele pode ajudar a determinar se você está transmitindo parâmetros à direita do hello, usando funções de modelo corretamente, e Obtendo recurso Olá esperado.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

Ou, suponha que você está encontrando erros de implantação que você acredita que estão relacionados a tooincorrectly definir dependências. Teste seu modelo dividindo-o em modelos simplificados. Primeiro, crie um modelo que implanta um único recurso (como um SQL Server). Quando você tiver certeza de que esse recurso foi definido corretamente, adicione um recurso depende dele (como um Banco de Dados SQL). Quando esses dois recursos estiverem definidos corretamente, adicione outros recursos dependentes (como políticas de auditoria). Entre cada implantação de teste, exclua Olá grupo toomake-se de que você teste adequadamente Olá dependências de recursos. 

## <a name="check-deployment-sequence"></a>Verificar a sequência de implantação

Muitos erros de implantação ocorrem quando os recursos são implantados em uma sequência inesperada. Esses erros surgem quando as dependências não são definidas corretamente. Quando você não tem uma dependência necessária, um recurso tenta toouse que um valor para outro recurso, mas outros Olá ainda não existe. Você obterá um erro informando que um recurso não foi encontrado. Você pode encontrar esse tipo de erro intermitentemente porque o tempo de implantação de saudação para cada recurso pode variar. Por exemplo, sua primeira toodeploy de tentativa de seus recursos é bem-sucedido porque um recurso necessário aleatoriamente concluída no tempo. No entanto, a segunda tentativa falha porque Olá necessários recursos não foram concluída no tempo. 

Porém, você deseja tooavoid dependências de configuração que não são necessários. Quando você tiver o desnecessárias dependências, você prolongar a duração de saudação da implantação hello, impedindo que os recursos que não são dependentes entre si do que está sendo implantado em paralelo. Além disso, você pode criar uma dependência circular que bloqueiam a implantação de saudação. Olá [referência](resource-group-template-functions-resource.md#reference) função cria uma dependência implícita em recurso Olá referenciada, quando esse recurso é implantado em Olá mesmo modelo. Portanto, você pode ter mais dependências de dependências de saudação especificadas no hello **dependsOn** propriedade. Olá [resourceId](resource-group-template-functions-resource.md#resourceid) função não cria uma dependência implícita ou validar que o recurso de saudação existe.

Quando você encontrar problemas de dependência, você precisa toogain percepção ordem Olá de implantação de recursos. ordem de saudação tooview de operações de implantação:

1. Selecione Olá histórico de implantação para seu grupo de recursos.

   ![selecionar o histórico de implantação](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Selecione uma implantação do histórico de saudação e selecione **eventos**.

   ![selecionar os eventos de implantação](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Examine a sequência de saudação de eventos para cada recurso. Status de toohello atenção de cada operação de pagamento. Por exemplo, hello imagem a seguir mostra três contas de armazenamento que são implantados em paralelo. Observe que Olá três contas de armazenamento são iniciados em Olá simultaneamente.

   ![implantação paralela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   imagem seguinte Olá mostra três contas de armazenamento que não são implantadas em paralelo. a segunda conta de armazenamento Olá depende da primeira conta de armazenamento Olá e conta de armazenamento terceira Olá depende da segunda conta de armazenamento Olá. Portanto, a primeira conta de armazenamento Olá é iniciada, aceita e concluída antes de saudação é iniciada.

   ![implantação sequencial](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Mesmo para cenários mais complexos, você pode usar Olá toodiscover de técnica mesmo quando a implantação é iniciada e concluída para cada recurso. Examine a sua toosee de eventos de implantação se a sequência de saudação é diferente do esperado. Nesse caso, reavalie dependências Olá para este recurso.

O Resource Manager identifica dependências circulares durante a validação do modelo. Ele retorna uma mensagem de erro afirmando especificamente uma dependência circular existe. toosolve uma dependência circular:

1. No modelo, localize o recurso de saudação identificado na dependência circular hello. 
2. Para esse recurso, examinar Olá **dependsOn** propriedade e quaisquer usos das Olá **referência** função toosee quais recursos ele depende. 
3. Examine essas toosee recursos quais recursos eles dependem. Execute dependências Olá até você notar um recurso que depende do recurso de saudação original.
5. Para obter recursos Olá envolvidos na dependência circular Olá, examine cuidadosamente todas as funções hello **dependsOn** propriedade tooidentify todas as dependências que não são necessários. Remova essas dependências. Se você não tiver certeza de que uma dependência é necessária, tente removê-lo. 
6. Reimplante o modelo de saudação.

Removendo valores do hello **dependsOn** propriedade pode causar erros quando você implanta o modelo de saudação. Se você encontrar um erro, adicione dependência Olá no modelo de saudação. 

Se essa abordagem não resolver a dependência circular hello, considere mover a parte de sua lógica de implantação para recursos filho (como extensões ou definições de configuração). Configure os toodeploy de recursos filho após recursos de saudação envolvidos na dependência circular hello. Por exemplo, suponha que você está implantando duas máquinas virtuais, mas você deve definir propriedades em cada um deles que se referem a outros toohello. Você pode implantá-los em Olá ordem a seguir:

1. vm1
2. vm2
3. Extensão na vm1 depende vm1 e vm2. extensão de saudação define valores na vm1 obtém da vm2.
4. Extensão da vm2 depende vm1 e vm2. extensão de saudação define valores vm2 obtém da vm1.

Olá a mesma abordagem funciona para aplicativos de serviço de aplicativo. Considere a possibilidade de mover os valores de configuração em um recurso filho do recurso de aplicativo hello. Você pode implantar dois aplicativos da web em Olá ordem a seguir:

1. webapp1
2. webapp2
3. a configuração para webapp1 depende de webapp1 e webapp2. Ele contém configurações do aplicativo com os valores do webapp2.
4. a configuração para webapp2 depende de webapp1 e webapp2. Ele contém configurações do aplicativo com os valores do webapp1.


## <a name="next-steps"></a>Próximas etapas
* Para erros de implantação toocommon resoluções, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sobre a auditoria de ações, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).
* toolearn sobre erros de saudação toodetermine ações durante a implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
