---
title: "Proteger o acesso aos Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Adicione segurança para proteger o acesso a gatilhos, entradas e saídas, parâmetros de ação e serviços usados com fluxos de trabalho em Aplicativos Lógicos do Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="eae07-103">Proteger o acesso aos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="eae07-103">Secure access to your logic apps</span></span>

<span data-ttu-id="eae07-104">Há muitas ferramentas disponíveis para ajudar a proteger seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="eae07-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="eae07-105">Proteger o acesso para acionar um aplicativo lógico (gatilho de solicitação de HTTP)</span><span class="sxs-lookup"><span data-stu-id="eae07-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="eae07-106">Proteger o acesso para gerenciar, editar ou ler um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="eae07-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="eae07-107">Proteger o acesso ao conteúdo de entradas e saídas para uma execução</span><span class="sxs-lookup"><span data-stu-id="eae07-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="eae07-108">Proteger parâmetros ou entradas em ações em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="eae07-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="eae07-109">Proteger o acesso aos serviços que recebem solicitações de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="eae07-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="eae07-110">Proteger o acesso a gatilhos</span><span class="sxs-lookup"><span data-stu-id="eae07-110">Secure access to trigger</span></span>

<span data-ttu-id="eae07-111">Ao trabalhar com um aplicativo lógico que é acionado em uma solicitação HTTP ([Solicitação](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), você pode restringir o acesso para que somente clientes autorizados possam acionar o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="eae07-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="eae07-112">Todas as solicitações para um aplicativo lógico são criptografadas e protegidas por SSL.</span><span class="sxs-lookup"><span data-stu-id="eae07-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="eae07-113">Assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="eae07-113">Shared Access Signature</span></span>

<span data-ttu-id="eae07-114">Cada ponto de extremidade de solicitação para um aplicativo lógico inclui uma [Assinatura de Acesso Compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS) como parte da URL.</span><span class="sxs-lookup"><span data-stu-id="eae07-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="eae07-115">Cada URL contém um parâmetro de consulta `sp`, `sv`, e `sig`.</span><span class="sxs-lookup"><span data-stu-id="eae07-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="eae07-116">As permissões são especificadas por `sp`e correspondem aos métodos HTTP permitidos, `sv` é a versão usada para gerar e `sig` é usado para autenticar o acesso para disparar.</span><span class="sxs-lookup"><span data-stu-id="eae07-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="eae07-117">A assinatura é gerada usando o algoritmo SHA256 com uma chave secreta em todos os caminhos de URL e propriedades.</span><span class="sxs-lookup"><span data-stu-id="eae07-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="eae07-118">A chave secreta nunca é exposta e publicada e é mantida criptografada e armazenada como parte do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="eae07-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="eae07-119">Seu aplicativo lógico somente autoriza gatilhos que contêm uma assinatura válida criada com a chave secreta.</span><span class="sxs-lookup"><span data-stu-id="eae07-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="eae07-120">Regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="eae07-120">Regenerate access keys</span></span>

<span data-ttu-id="eae07-121">Você pode regenerar uma nova chave segura a qualquer momento por meio da API REST ou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae07-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="eae07-122">Todas as URLs atuais que foram geradas anteriormente usando a chave antiga são invalidadas e têm sua autorização para acionar o aplicativo lógico revogada.</span><span class="sxs-lookup"><span data-stu-id="eae07-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="eae07-123">No portal do Azure, abra o aplicativo lógico que você cuja chave você deseja regenerar</span><span class="sxs-lookup"><span data-stu-id="eae07-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="eae07-124">Clique no item de menu **Chaves de Acesso** em **Configurações**</span><span class="sxs-lookup"><span data-stu-id="eae07-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="eae07-125">Escolha a chave a regenerar e conclua o processo</span><span class="sxs-lookup"><span data-stu-id="eae07-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="eae07-126">As URLs obtidas após a regeneração são assinadas com a nova chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="eae07-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="eae07-127">Criar URLs de retorno de chamada com uma data de expiração</span><span class="sxs-lookup"><span data-stu-id="eae07-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="eae07-128">Se você estiver compartilhando a URL com terceiros, você poderá gerar URLs com chaves específicas e datas de vencimento, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="eae07-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="eae07-129">Você poderá então reverter chaves perfeitamente ou então assegurar que o acesso para acionar um aplicativo fique restrito a um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="eae07-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="eae07-130">Você pode especificar uma data de expiração para uma URL por meio da [API REST dos Aplicativos Lógicos](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="eae07-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="eae07-131">No corpo, inclua a propriedade `NotAfter` como uma cadeia de caracteres de data JSON, que retorna uma URL de retorno de chamada que só é válida até a data e hora `NotAfter`.</span><span class="sxs-lookup"><span data-stu-id="eae07-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="eae07-132">Criar URLs com chave secreta primária ou secundária</span><span class="sxs-lookup"><span data-stu-id="eae07-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="eae07-133">Quando você gera ou lista URLs de retorno de chamada para gatilhos com base em solicitações, você também pode especificar qual chave usar para acessar a URL.</span><span class="sxs-lookup"><span data-stu-id="eae07-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="eae07-134">Você pode gerar uma URL assinada por uma chave específica por meio da [API REST de aplicativos lógicos](https://docs.microsoft.com/rest/api/logic/workflowtriggers) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eae07-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="eae07-135">No corpo, inclua a propriedade `KeyType` como `Primary` ou `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="eae07-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="eae07-136">Isso retorna uma URL assinada pela chave segura especificada.</span><span class="sxs-lookup"><span data-stu-id="eae07-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="eae07-137">Restringir endereços IP de entrada</span><span class="sxs-lookup"><span data-stu-id="eae07-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="eae07-138">Além da Assinatura de Acesso Compartilhado, talvez você queira restringir chamando um aplicativo lógico somente de clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="eae07-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="eae07-139">Por exemplo, se você gerenciar seu ponto de extremidade por meio do Gerenciamento de API do Azure, você pode restringir o aplicativo lógico para só aceitar a solicitação quando a solicitação é proveniente do endereço IP de instância de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="eae07-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="eae07-140">Essa configuração pode ser definida nas configurações de aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="eae07-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="eae07-141">No portal do Azure, abra o aplicativo lógico cuja chave você deseja regenerar</span><span class="sxs-lookup"><span data-stu-id="eae07-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="eae07-142">Clique no item de menu **Configuração de Controle de Acesso** em **Configurações**</span><span class="sxs-lookup"><span data-stu-id="eae07-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="eae07-143">Especifique a lista de intervalos de endereços IP a serem aceitos pelo gatilho</span><span class="sxs-lookup"><span data-stu-id="eae07-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="eae07-144">Um intervalo IP válido assume o formato `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="eae07-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="eae07-145">Se quiser que o aplicativo lógico seja acionado apenas como um aplicativo lógico aninhado, selecione a opção **Somente outros aplicativos lógicos**.</span><span class="sxs-lookup"><span data-stu-id="eae07-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="eae07-146">Essa opção grava uma matriz vazia para o recurso, o que significa que somente chamadas do serviço em si (aplicativos lógicos pai) acionam com êxito.</span><span class="sxs-lookup"><span data-stu-id="eae07-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="eae07-147">Você ainda pode executar um aplicativo lógico com um gatilho de solicitação por meio de `/triggers/{triggerName}/run` da API REST/Gerenciamento, independentemente do IP.</span><span class="sxs-lookup"><span data-stu-id="eae07-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="eae07-148">Esse cenário requer autenticação em relação à API REST do Azure e todos os eventos apareceriam no Log de Auditoria do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae07-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="eae07-149">Defina políticas de controle de acesso de apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="eae07-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="eae07-150">Definir intervalos de IP na definição de recurso</span><span class="sxs-lookup"><span data-stu-id="eae07-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="eae07-151">Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) para automatizar suas implantações, as configurações de intervalo IP podem ser configuradas no modelo de recurso.</span><span class="sxs-lookup"><span data-stu-id="eae07-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="eae07-152">Adicionar Azure Active Directory, OAuth, ou outra proteção</span><span class="sxs-lookup"><span data-stu-id="eae07-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="eae07-153">Para adicionar mais protocolos de autorização sobre um aplicativo lógico, o [Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/) oferece monitoramento avançado, segurança, política e documentação para qualquer ponto de extremidade com a capacidade de expor um aplicativo lógico como uma API.</span><span class="sxs-lookup"><span data-stu-id="eae07-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="eae07-154">O Gerenciamento de API do Azure pode expor um ponto de extremidade público ou privado para o aplicativo lógico, que pode usar o Azure Active Directory, certificado, OAuth ou outros padrões de segurança.</span><span class="sxs-lookup"><span data-stu-id="eae07-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="eae07-155">Quando uma solicitação é recebida, o Gerenciamento de API do Azure encaminha a solicitação para o aplicativo lógico (executando quaisquer transformações necessárias ou restrições em andamento).</span><span class="sxs-lookup"><span data-stu-id="eae07-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="eae07-156">Você pode usar as configurações de intervalo IP de entrada no aplicativo lógico para permitir que somente o aplicativo lógico seja disparado do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="eae07-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="eae07-157">Proteger o acesso para gerenciar ou editar aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="eae07-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="eae07-158">Você pode restringir o acesso a operações de gerenciamento em um aplicativo lógico para que somente usuários ou grupos específicos sejam capazes de realizar operações no recurso.</span><span class="sxs-lookup"><span data-stu-id="eae07-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="eae07-159">Aplicativos lógicos usam o recurso de [RBAC (Controle de Acesso Baseado em Função)](../active-directory/role-based-access-control-configure.md) do Azure e podem ser personalizados com as mesmas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="eae07-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="eae07-160">Há algumas funções internas que você pode aos atribuir membros da sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="eae07-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="eae07-161">**Colaborador do Aplicativo Lógico** - Fornece acesso para exibir, editar e atualizar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="eae07-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="eae07-162">Não pode remover o recurso ou executar operações de administração.</span><span class="sxs-lookup"><span data-stu-id="eae07-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="eae07-163">**Operador de Aplicativo Lógico** - Pode exibir o aplicativo lógico e histórico de execução e habilitar/desabilitar.</span><span class="sxs-lookup"><span data-stu-id="eae07-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="eae07-164">Não é pode editar ou atualizar a definição.</span><span class="sxs-lookup"><span data-stu-id="eae07-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="eae07-165">Você também pode usar o [Bloqueio de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md) para evitar a alteração ou exclusão de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="eae07-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="eae07-166">Essa funcionalidade é importante para evitar que os recursos de produção sejam alterados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="eae07-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="eae07-167">Proteger o acesso ao conteúdo do histórico de execução</span><span class="sxs-lookup"><span data-stu-id="eae07-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="eae07-168">Você pode restringir o acesso ao conteúdo de entradas ou saídas de execuções anteriores para intervalos de endereços IP específicos.</span><span class="sxs-lookup"><span data-stu-id="eae07-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="eae07-169">Todos os dados dentro de uma execução de fluxo de trabalho são criptografados em trânsito e em repouso.</span><span class="sxs-lookup"><span data-stu-id="eae07-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="eae07-170">Quando uma chamada para o histórico de execução é feita, o serviço autentica a solicitação e fornece links para a solicitação e resposta de entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="eae07-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="eae07-171">Esse link pode ser protegido para que somente solicitações para exibir o conteúdo de um intervalo de endereços IP designado retornem o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="eae07-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="eae07-172">Você pode usar essa funcionalidade para controle de acesso adicional.</span><span class="sxs-lookup"><span data-stu-id="eae07-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="eae07-173">Você pode até mesmo especificar um endereço IP como `0.0.0.0` para que ninguém possa acessar entradas/saídas.</span><span class="sxs-lookup"><span data-stu-id="eae07-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="eae07-174">Somente alguém com permissões de administrador poderá remover essa restrição, fornecendo a possibilidade para acesso 'just-in-time' ao conteúdo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="eae07-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="eae07-175">Essa configuração pode ser definida nas configurações de recurso do portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="eae07-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="eae07-176">No portal do Azure, abra o aplicativo lógico cuja chave você deseja regenerar</span><span class="sxs-lookup"><span data-stu-id="eae07-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="eae07-177">Clique no item de menu **Configuração de Controle de Acesso** em **Configurações**</span><span class="sxs-lookup"><span data-stu-id="eae07-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="eae07-178">Especificar a lista de intervalos de endereços IP para acesso ao conteúdo</span><span class="sxs-lookup"><span data-stu-id="eae07-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="eae07-179">Definir intervalos de IP na definição de recurso</span><span class="sxs-lookup"><span data-stu-id="eae07-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="eae07-180">Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) para automatizar suas implantações, as configurações de intervalo IP podem ser configuradas no modelo de recurso.</span><span class="sxs-lookup"><span data-stu-id="eae07-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="eae07-181">Proteger parâmetros e entradas em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="eae07-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="eae07-182">Você pode querer parametrizar alguns aspectos de uma definição de fluxo de trabalho para implantação entre ambientes.</span><span class="sxs-lookup"><span data-stu-id="eae07-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="eae07-183">Além disso, alguns parâmetros podem ser parâmetros seguros que você não deseja que apareçam ao editar um fluxo de trabalho, como uma ID de cliente e o segredo do cliente para a [Autenticação do Azure Active Directory](../connectors/connectors-native-http.md#authentication) de uma ação HTTP.</span><span class="sxs-lookup"><span data-stu-id="eae07-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="eae07-184">Usar parâmetros e proteger parâmetros</span><span class="sxs-lookup"><span data-stu-id="eae07-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="eae07-185">A [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs) fornece uma operação `@parameters()` para acessar o valor de um parâmetro de recurso em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="eae07-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="eae07-186">Além disso, você pode [especificar parâmetros no modelo de implantação do recurso](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="eae07-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="eae07-187">Mas se você especificar o tipo de parâmetro para ser `securestring`, ele não será retornado com o restante da definição de recurso e não poderá ser acessado ao exibir o recurso após a implantação.</span><span class="sxs-lookup"><span data-stu-id="eae07-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="eae07-188">Se o parâmetro for usado nos cabeçalhos ou no corpo de uma solicitação, ele poderá ser visível ao acessar o histórico de execução e a solicitação HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="eae07-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="eae07-189">Certifique-se de definir as políticas de acesso ao conteúdo apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="eae07-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="eae07-190">Cabeçalhos de autorização nunca são visíveis por meio de entradas ou saídas.</span><span class="sxs-lookup"><span data-stu-id="eae07-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="eae07-191">Então, se o segredo estiver sendo usado ali, esse segredo não será recuperável.</span><span class="sxs-lookup"><span data-stu-id="eae07-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="eae07-192">Modelo de implantação de recursos com segredos</span><span class="sxs-lookup"><span data-stu-id="eae07-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="eae07-193">O exemplo a seguir mostra uma implantação que faz referência a um parâmetro seguro de `secret` em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="eae07-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="eae07-194">Em um arquivo de parâmetros separado, você poderia especificar o valor de ambiente para o `secret` ou usar o [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) para recuperar os segredos no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="eae07-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is the request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="eae07-195">Proteger o acesso aos serviços que recebem solicitações de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="eae07-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="eae07-196">Há várias maneiras para ajudar a proteger qualquer ponto de extremidade que o aplicativo lógico precisa acessar.</span><span class="sxs-lookup"><span data-stu-id="eae07-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="eae07-197">Usar a autenticação em solicitações de saída</span><span class="sxs-lookup"><span data-stu-id="eae07-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="eae07-198">Ao trabalhar com uma ação HTTP, HTTP + Swagger (API Open) ou Webhook, você pode adicionar autenticação para a solicitação que está sendo enviada.</span><span class="sxs-lookup"><span data-stu-id="eae07-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="eae07-199">Você pode incluir a autenticação básica, autenticação de certificado ou autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eae07-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="eae07-200">Detalhes sobre como configurar essa autenticação podem ser encontrados [neste artigo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="eae07-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="eae07-201">Restringir o acesso a endereços IP de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="eae07-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="eae07-202">Todas as chamadas de aplicativos lógicos vêm de um conjunto específico de endereços IP por região.</span><span class="sxs-lookup"><span data-stu-id="eae07-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="eae07-203">Você pode adicionar filtragem adicional para aceitar somente solicitações desses endereços IP designados.</span><span class="sxs-lookup"><span data-stu-id="eae07-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="eae07-204">Para obter uma lista desses endereços IP, consulte [limites e configuração do aplicativo lógico](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="eae07-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="eae07-205">Conectividade local</span><span class="sxs-lookup"><span data-stu-id="eae07-205">On-premises connectivity</span></span>

<span data-ttu-id="eae07-206">Aplicativos lógicos fornecem integração com diversos serviços que fornecem comunicação local segura e confiável.</span><span class="sxs-lookup"><span data-stu-id="eae07-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="eae07-207">Gateway de dados local</span><span class="sxs-lookup"><span data-stu-id="eae07-207">On-premises data gateway</span></span>

<span data-ttu-id="eae07-208">Muitos conectores gerenciados de aplicativo lógico fornecem conectividade segura para sistemas locais, incluindo o sistema de arquivos, SQL, SharePoint, DB2 e muito mais.</span><span class="sxs-lookup"><span data-stu-id="eae07-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="eae07-209">O gateway retransmite dados de fontes locais em canais criptografados por meio do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="eae07-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="eae07-210">Todo o tráfego é originado como tráfego de saída seguro do agente de gateway.</span><span class="sxs-lookup"><span data-stu-id="eae07-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="eae07-211">Saiba mais sobre [como o gateway de dados funciona](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="eae07-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="eae07-212">Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="eae07-212">Azure API Management</span></span>

<span data-ttu-id="eae07-213">O [Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/) tem opções de conectividade local incluindo integração VPN e ExpressRoute site a site para proxy seguro e a comunicação com sistemas locais.</span><span class="sxs-lookup"><span data-stu-id="eae07-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="eae07-214">No Designer de Aplicativos Lógicos, você pode selecionar rapidamente uma API exposta do Gerenciamento de API do Azure em um fluxo de trabalho, fornecendo acesso rápido a sistemas locais.</span><span class="sxs-lookup"><span data-stu-id="eae07-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="eae07-215">Conexões híbridas do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="eae07-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="eae07-216">Você pode usar o recurso de conexão híbrida local para a API do Azure e aplicativos da Web para se comunicar no local.</span><span class="sxs-lookup"><span data-stu-id="eae07-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="eae07-217">Detalhes sobre conexões híbridas e como configurá-las podem ser encontrados [neste artigo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eae07-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eae07-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eae07-218">Next steps</span></span>
[<span data-ttu-id="eae07-219">Criar um modelo de implantação</span><span class="sxs-lookup"><span data-stu-id="eae07-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="eae07-220">Manipulação de exceção</span><span class="sxs-lookup"><span data-stu-id="eae07-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="eae07-221">Monitorar seus aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="eae07-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="eae07-222">Diagnosticando falhas e problemas nos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="eae07-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
