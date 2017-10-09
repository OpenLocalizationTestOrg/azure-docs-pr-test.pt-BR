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
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="89726-104">Entender os erros de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="89726-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="89726-105">Este tópico descreve os erros de implantação e como você pode descobrir mais informações sobre um erro.</span><span class="sxs-lookup"><span data-stu-id="89726-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="89726-106">Para erros de implantação toocommon resoluções, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="89726-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="89726-107">Dois tipos de erros</span><span class="sxs-lookup"><span data-stu-id="89726-107">Two types of errors</span></span>
<span data-ttu-id="89726-108">Há dois tipos de erros que você pode receber:</span><span class="sxs-lookup"><span data-stu-id="89726-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="89726-109">erros de validação</span><span class="sxs-lookup"><span data-stu-id="89726-109">validation errors</span></span>
* <span data-ttu-id="89726-110">erros de implantação</span><span class="sxs-lookup"><span data-stu-id="89726-110">deployment errors</span></span>

<span data-ttu-id="89726-111">Olá a imagem a seguir mostra o log de atividades de saudação para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="89726-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="89726-112">Ela representa duas implantações.</span><span class="sxs-lookup"><span data-stu-id="89726-112">It represents two deployments.</span></span> <span data-ttu-id="89726-113">Em uma implantação, de falha de validação no modelo de saudação (**validar**) e não prosseguir.</span><span class="sxs-lookup"><span data-stu-id="89726-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="89726-114">Em Olá outra implantação, modelo Olá passou na validação, mas falha ao criar recursos de saudação (**implantações gravar**).</span><span class="sxs-lookup"><span data-stu-id="89726-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![mostrar código de erro](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="89726-116">Erros de validação ocorrem em cenários que podem ser determinados antes da implantação.</span><span class="sxs-lookup"><span data-stu-id="89726-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="89726-117">Eles incluem erros de sintaxe em seu modelo, ou tentar recursos toodeploy que excedem suas cotas de assinatura.</span><span class="sxs-lookup"><span data-stu-id="89726-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="89726-118">Erros de implantação são provenientes de condições que ocorrem durante o processo de implantação hello.</span><span class="sxs-lookup"><span data-stu-id="89726-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="89726-119">Eles incluem tentar tooaccess um recurso que está sendo implantado em paralelo.</span><span class="sxs-lookup"><span data-stu-id="89726-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="89726-120">Ambos os tipos de retorno de erros que você use a implantação de saudação tootroubleshoot um código de erro.</span><span class="sxs-lookup"><span data-stu-id="89726-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="89726-121">Os dois tipos de erros aparecem no hello [log de atividades](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="89726-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="89726-122">No entanto, erros de validação não aparecem no seu histórico de implantação porque a implantação de saudação nunca foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="89726-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="89726-123">Determinar o código de erro</span><span class="sxs-lookup"><span data-stu-id="89726-123">Determine error code</span></span>

<span data-ttu-id="89726-124">Você pode aprender sobre um erro ao examinar a mensagem de saudação do erro e o código de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="89726-125">Olá [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md) artigo lista resoluções por código de erro.</span><span class="sxs-lookup"><span data-stu-id="89726-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="89726-126">Este tópico mostra como toouse Olá código de erro de saudação toodiscover portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89726-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="89726-127">Erros de validação</span><span class="sxs-lookup"><span data-stu-id="89726-127">Validation errors</span></span>

<span data-ttu-id="89726-128">Durante a implantação por meio do portal hello, você verá um erro de validação depois de enviar seus valores.</span><span class="sxs-lookup"><span data-stu-id="89726-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![mostrar erro de validação no portal](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="89726-130">Selecione a mensagem de saudação para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="89726-130">Select hello message for more details.</span></span> <span data-ttu-id="89726-131">Olá a imagem a seguir, verá um **InvalidTemplateDeployment** erro e uma mensagem que indica uma diretiva de implantação está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="89726-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![mostrar detalhes da validação](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="89726-133">Erros de implantação</span><span class="sxs-lookup"><span data-stu-id="89726-133">Deployment errors</span></span>

<span data-ttu-id="89726-134">Quando a operação Olá aprovado na validação, mas falha durante a implantação, você verá o erro de saudação em notificações de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="89726-135">Selecione Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="89726-135">Select hello notification.</span></span>

![erro de notificação](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="89726-137">Você ver mais detalhes sobre a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-137">You see more details about hello deployment.</span></span> <span data-ttu-id="89726-138">Selecione Olá opção toofind obter mais informações sobre o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-138">Select hello option toofind more information about hello error.</span></span>

![falha na implantação](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="89726-140">Você ver códigos de erros e de mensagens de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-140">You see hello error message and error codes.</span></span> <span data-ttu-id="89726-141">Observe que há dois códigos de erro.</span><span class="sxs-lookup"><span data-stu-id="89726-141">Notice there are two error codes.</span></span> <span data-ttu-id="89726-142">Olá primeiro código de erro (**DeploymentFailed**) é um erro geral que não fornece Olá detalhes que você precisa de erro de saudação toosolve.</span><span class="sxs-lookup"><span data-stu-id="89726-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="89726-143">Olá segundo código de erro (**StorageAccountNotFound**) fornece detalhes de saudação é necessário.</span><span class="sxs-lookup"><span data-stu-id="89726-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![detalhes do erro](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="89726-145">Habilitar o log de depuração</span><span class="sxs-lookup"><span data-stu-id="89726-145">Enable debug logging</span></span>
<span data-ttu-id="89726-146">Às vezes você precisa obter mais informações sobre Olá toodiscover de solicitação e resposta que deu errado.</span><span class="sxs-lookup"><span data-stu-id="89726-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="89726-147">Usando o PowerShell ou a CLI do Azure, você pode solicitar que informações adicionais sejam registradas durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="89726-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="89726-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89726-148">PowerShell</span></span>

   <span data-ttu-id="89726-149">No PowerShell, defina Olá **DeploymentDebugLogLevel** parâmetro tooAll, ResponseContent ou RequestContent.</span><span class="sxs-lookup"><span data-stu-id="89726-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="89726-150">Examine o conteúdo da solicitação Olá com hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="89726-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="89726-151">Ou então, Olá conteúdo da resposta:</span><span class="sxs-lookup"><span data-stu-id="89726-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="89726-152">Essas informações podem ajudá-lo a determinar se um valor no modelo hello está sendo definido incorretamente.</span><span class="sxs-lookup"><span data-stu-id="89726-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="89726-153">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="89726-153">Azure CLI</span></span>

   <span data-ttu-id="89726-154">Examine as operações de implantação Olá com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="89726-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="89726-155">Modelo aninhado</span><span class="sxs-lookup"><span data-stu-id="89726-155">Nested template</span></span>

   <span data-ttu-id="89726-156">toolog as informações de depuração para um modelo aninhado, use Olá **debugSetting** elemento.</span><span class="sxs-lookup"><span data-stu-id="89726-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="89726-157">Criar um modelo de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="89726-157">Create a troubleshooting template</span></span>
<span data-ttu-id="89726-158">Em alguns casos, Olá tootroubleshoot de maneira mais fácil o modelo for tootest partes dele.</span><span class="sxs-lookup"><span data-stu-id="89726-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="89726-159">Você pode criar um modelo simplificado que permite que você toofocus parte Olá achar que está causando o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="89726-160">Por exemplo, suponha que você esteja recebendo um erro ao fazer referência a um recurso.</span><span class="sxs-lookup"><span data-stu-id="89726-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="89726-161">Em vez de lidar com um modelo inteiro, crie um modelo que retorna a parte de saudação que possam estar causando o problema.</span><span class="sxs-lookup"><span data-stu-id="89726-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="89726-162">Ele pode ajudar a determinar se você está transmitindo parâmetros à direita do hello, usando funções de modelo corretamente, e Obtendo recurso Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="89726-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="89726-163">Ou, suponha que você está encontrando erros de implantação que você acredita que estão relacionados a tooincorrectly definir dependências.</span><span class="sxs-lookup"><span data-stu-id="89726-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="89726-164">Teste seu modelo dividindo-o em modelos simplificados.</span><span class="sxs-lookup"><span data-stu-id="89726-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="89726-165">Primeiro, crie um modelo que implanta um único recurso (como um SQL Server).</span><span class="sxs-lookup"><span data-stu-id="89726-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="89726-166">Quando você tiver certeza de que esse recurso foi definido corretamente, adicione um recurso depende dele (como um Banco de Dados SQL).</span><span class="sxs-lookup"><span data-stu-id="89726-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="89726-167">Quando esses dois recursos estiverem definidos corretamente, adicione outros recursos dependentes (como políticas de auditoria).</span><span class="sxs-lookup"><span data-stu-id="89726-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="89726-168">Entre cada implantação de teste, exclua Olá grupo toomake-se de que você teste adequadamente Olá dependências de recursos.</span><span class="sxs-lookup"><span data-stu-id="89726-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="89726-169">Verificar a sequência de implantação</span><span class="sxs-lookup"><span data-stu-id="89726-169">Check deployment sequence</span></span>

<span data-ttu-id="89726-170">Muitos erros de implantação ocorrem quando os recursos são implantados em uma sequência inesperada.</span><span class="sxs-lookup"><span data-stu-id="89726-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="89726-171">Esses erros surgem quando as dependências não são definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="89726-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="89726-172">Quando você não tem uma dependência necessária, um recurso tenta toouse que um valor para outro recurso, mas outros Olá ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="89726-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="89726-173">Você obterá um erro informando que um recurso não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="89726-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="89726-174">Você pode encontrar esse tipo de erro intermitentemente porque o tempo de implantação de saudação para cada recurso pode variar.</span><span class="sxs-lookup"><span data-stu-id="89726-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="89726-175">Por exemplo, sua primeira toodeploy de tentativa de seus recursos é bem-sucedido porque um recurso necessário aleatoriamente concluída no tempo.</span><span class="sxs-lookup"><span data-stu-id="89726-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="89726-176">No entanto, a segunda tentativa falha porque Olá necessários recursos não foram concluída no tempo.</span><span class="sxs-lookup"><span data-stu-id="89726-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="89726-177">Porém, você deseja tooavoid dependências de configuração que não são necessários.</span><span class="sxs-lookup"><span data-stu-id="89726-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="89726-178">Quando você tiver o desnecessárias dependências, você prolongar a duração de saudação da implantação hello, impedindo que os recursos que não são dependentes entre si do que está sendo implantado em paralelo.</span><span class="sxs-lookup"><span data-stu-id="89726-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="89726-179">Além disso, você pode criar uma dependência circular que bloqueiam a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="89726-180">Olá [referência](resource-group-template-functions-resource.md#reference) função cria uma dependência implícita em recurso Olá referenciada, quando esse recurso é implantado em Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="89726-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="89726-181">Portanto, você pode ter mais dependências de dependências de saudação especificadas no hello **dependsOn** propriedade.</span><span class="sxs-lookup"><span data-stu-id="89726-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="89726-182">Olá [resourceId](resource-group-template-functions-resource.md#resourceid) função não cria uma dependência implícita ou validar que o recurso de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="89726-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="89726-183">Quando você encontrar problemas de dependência, você precisa toogain percepção ordem Olá de implantação de recursos.</span><span class="sxs-lookup"><span data-stu-id="89726-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="89726-184">ordem de saudação tooview de operações de implantação:</span><span class="sxs-lookup"><span data-stu-id="89726-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="89726-185">Selecione Olá histórico de implantação para seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="89726-185">Select hello deployment history for your resource group.</span></span>

   ![selecionar o histórico de implantação](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="89726-187">Selecione uma implantação do histórico de saudação e selecione **eventos**.</span><span class="sxs-lookup"><span data-stu-id="89726-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![selecionar os eventos de implantação](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="89726-189">Examine a sequência de saudação de eventos para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="89726-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="89726-190">Status de toohello atenção de cada operação de pagamento.</span><span class="sxs-lookup"><span data-stu-id="89726-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="89726-191">Por exemplo, hello imagem a seguir mostra três contas de armazenamento que são implantados em paralelo.</span><span class="sxs-lookup"><span data-stu-id="89726-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="89726-192">Observe que Olá três contas de armazenamento são iniciados em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="89726-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![implantação paralela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="89726-194">imagem seguinte Olá mostra três contas de armazenamento que não são implantadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="89726-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="89726-195">a segunda conta de armazenamento Olá depende da primeira conta de armazenamento Olá e conta de armazenamento terceira Olá depende da segunda conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="89726-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="89726-196">Portanto, a primeira conta de armazenamento Olá é iniciada, aceita e concluída antes de saudação é iniciada.</span><span class="sxs-lookup"><span data-stu-id="89726-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![implantação sequencial](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="89726-198">Mesmo para cenários mais complexos, você pode usar Olá toodiscover de técnica mesmo quando a implantação é iniciada e concluída para cada recurso.</span><span class="sxs-lookup"><span data-stu-id="89726-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="89726-199">Examine a sua toosee de eventos de implantação se a sequência de saudação é diferente do esperado.</span><span class="sxs-lookup"><span data-stu-id="89726-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="89726-200">Nesse caso, reavalie dependências Olá para este recurso.</span><span class="sxs-lookup"><span data-stu-id="89726-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="89726-201">O Resource Manager identifica dependências circulares durante a validação do modelo.</span><span class="sxs-lookup"><span data-stu-id="89726-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="89726-202">Ele retorna uma mensagem de erro afirmando especificamente uma dependência circular existe.</span><span class="sxs-lookup"><span data-stu-id="89726-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="89726-203">toosolve uma dependência circular:</span><span class="sxs-lookup"><span data-stu-id="89726-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="89726-204">No modelo, localize o recurso de saudação identificado na dependência circular hello.</span><span class="sxs-lookup"><span data-stu-id="89726-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="89726-205">Para esse recurso, examinar Olá **dependsOn** propriedade e quaisquer usos das Olá **referência** função toosee quais recursos ele depende.</span><span class="sxs-lookup"><span data-stu-id="89726-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="89726-206">Examine essas toosee recursos quais recursos eles dependem.</span><span class="sxs-lookup"><span data-stu-id="89726-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="89726-207">Execute dependências Olá até você notar um recurso que depende do recurso de saudação original.</span><span class="sxs-lookup"><span data-stu-id="89726-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="89726-208">Para obter recursos Olá envolvidos na dependência circular Olá, examine cuidadosamente todas as funções hello **dependsOn** propriedade tooidentify todas as dependências que não são necessários.</span><span class="sxs-lookup"><span data-stu-id="89726-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="89726-209">Remova essas dependências.</span><span class="sxs-lookup"><span data-stu-id="89726-209">Remove those dependencies.</span></span> <span data-ttu-id="89726-210">Se você não tiver certeza de que uma dependência é necessária, tente removê-lo.</span><span class="sxs-lookup"><span data-stu-id="89726-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="89726-211">Reimplante o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-211">Redeploy hello template.</span></span>

<span data-ttu-id="89726-212">Removendo valores do hello **dependsOn** propriedade pode causar erros quando você implanta o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="89726-213">Se você encontrar um erro, adicione dependência Olá no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="89726-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="89726-214">Se essa abordagem não resolver a dependência circular hello, considere mover a parte de sua lógica de implantação para recursos filho (como extensões ou definições de configuração).</span><span class="sxs-lookup"><span data-stu-id="89726-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="89726-215">Configure os toodeploy de recursos filho após recursos de saudação envolvidos na dependência circular hello.</span><span class="sxs-lookup"><span data-stu-id="89726-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="89726-216">Por exemplo, suponha que você está implantando duas máquinas virtuais, mas você deve definir propriedades em cada um deles que se referem a outros toohello.</span><span class="sxs-lookup"><span data-stu-id="89726-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="89726-217">Você pode implantá-los em Olá ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="89726-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="89726-218">vm1</span><span class="sxs-lookup"><span data-stu-id="89726-218">vm1</span></span>
2. <span data-ttu-id="89726-219">vm2</span><span class="sxs-lookup"><span data-stu-id="89726-219">vm2</span></span>
3. <span data-ttu-id="89726-220">Extensão na vm1 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="89726-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="89726-221">extensão de saudação define valores na vm1 obtém da vm2.</span><span class="sxs-lookup"><span data-stu-id="89726-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="89726-222">Extensão da vm2 depende vm1 e vm2.</span><span class="sxs-lookup"><span data-stu-id="89726-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="89726-223">extensão de saudação define valores vm2 obtém da vm1.</span><span class="sxs-lookup"><span data-stu-id="89726-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="89726-224">Olá a mesma abordagem funciona para aplicativos de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89726-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="89726-225">Considere a possibilidade de mover os valores de configuração em um recurso filho do recurso de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="89726-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="89726-226">Você pode implantar dois aplicativos da web em Olá ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="89726-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="89726-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="89726-227">webapp1</span></span>
2. <span data-ttu-id="89726-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="89726-228">webapp2</span></span>
3. <span data-ttu-id="89726-229">a configuração para webapp1 depende de webapp1 e webapp2.</span><span class="sxs-lookup"><span data-stu-id="89726-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="89726-230">Ele contém configurações do aplicativo com os valores do webapp2.</span><span class="sxs-lookup"><span data-stu-id="89726-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="89726-231">a configuração para webapp2 depende de webapp1 e webapp2.</span><span class="sxs-lookup"><span data-stu-id="89726-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="89726-232">Ele contém configurações do aplicativo com os valores do webapp1.</span><span class="sxs-lookup"><span data-stu-id="89726-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="89726-233">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89726-233">Next steps</span></span>
* <span data-ttu-id="89726-234">Para erros de implantação toocommon resoluções, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="89726-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="89726-235">toolearn sobre a auditoria de ações, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="89726-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="89726-236">toolearn sobre erros de saudação toodetermine ações durante a implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="89726-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
