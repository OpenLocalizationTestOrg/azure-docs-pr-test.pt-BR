---
title: "aaaSecure acessar os aplicativos lógicos tooAzure | Microsoft Docs"
description: "Adicione a segurança para proteger o acesso tootriggers, entradas e saídas, parâmetros de ação e serviços usados com fluxos de trabalho em aplicativos do Azure lógica."
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
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="fefff-103">Proteger o acesso a aplicativos de lógica de tooyour</span><span class="sxs-lookup"><span data-stu-id="fefff-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="fefff-104">Há muitos toohelp disponíveis ferramentas proteger seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="fefff-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="fefff-105">Protegendo o acesso tootrigger um lógica de aplicativo (gatilho de solicitação de HTTP)</span><span class="sxs-lookup"><span data-stu-id="fefff-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="fefff-106">Segurança de acesso toomanage, editar ou ler uma lógica de aplicativo</span><span class="sxs-lookup"><span data-stu-id="fefff-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="fefff-107">Protegendo o acesso toocontents de entradas e saídas para uma execução</span><span class="sxs-lookup"><span data-stu-id="fefff-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="fefff-108">Proteger parâmetros ou entradas em ações em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="fefff-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="fefff-109">Protegendo o acesso tooservices que recebe solicitações de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="fefff-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="fefff-110">Acesso seguro tootrigger</span><span class="sxs-lookup"><span data-stu-id="fefff-110">Secure access tootrigger</span></span>

<span data-ttu-id="fefff-111">Quando você trabalha com um aplicativo de lógica que é acionado em uma solicitação HTTP ([solicitação](../connectors/connectors-native-reqres.md) ou [Webhook](../connectors/connectors-native-webhook.md)), você pode restringir o acesso para que somente clientes autorizados podem acionar Olá lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fefff-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="fefff-112">Todas as solicitações para um aplicativo lógico são criptografadas e protegidas por SSL.</span><span class="sxs-lookup"><span data-stu-id="fefff-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="fefff-113">Assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="fefff-113">Shared Access Signature</span></span>

<span data-ttu-id="fefff-114">Cada ponto de extremidade de solicitação para um aplicativo de lógica inclui um [assinatura de acesso compartilhado (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) como parte da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="fefff-115">Cada URL contém um parâmetro de consulta `sp`, `sv`, e `sig`.</span><span class="sxs-lookup"><span data-stu-id="fefff-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="fefff-116">As permissões são especificadas por `sp`, e correspondem tooHTTP métodos permitidos, `sv` é Olá versão usada toogenerate, e `sig` é usado tooauthenticate tootrigger de acesso.</span><span class="sxs-lookup"><span data-stu-id="fefff-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="fefff-117">assinatura de saudação é gerada usando o algoritmo de saudação SHA256 com uma chave de segredo em todos os caminhos de URL hello e propriedades.</span><span class="sxs-lookup"><span data-stu-id="fefff-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="fefff-118">chave secreta Olá nunca é exposta e publicado e são mantidos criptografados e armazenados como parte do aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="fefff-119">Seu aplicativo lógico somente autorizará gatilhos que contém uma assinatura válida criada com a chave secreta hello.</span><span class="sxs-lookup"><span data-stu-id="fefff-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="fefff-120">Regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="fefff-120">Regenerate access keys</span></span>

<span data-ttu-id="fefff-121">Você pode regenerar uma nova chave segura na qualquer momento por meio do portal Olá de API REST ou o Azure.</span><span class="sxs-lookup"><span data-stu-id="fefff-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="fefff-122">Todas as URLs atuais que foram geradas anteriormente usando a chave antiga Olá são toofire invalidada e não autorizados Olá lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fefff-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="fefff-123">No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooregenerate uma chave</span><span class="sxs-lookup"><span data-stu-id="fefff-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="fefff-124">Clique em Olá **chaves de acesso** item de menu no **configurações**</span><span class="sxs-lookup"><span data-stu-id="fefff-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="fefff-125">Escolha tooregenerate chave hello e processo Olá concluída</span><span class="sxs-lookup"><span data-stu-id="fefff-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="fefff-126">Recuperar após a regeneração de URLs são assinados com a nova chave de acesso hello.</span><span class="sxs-lookup"><span data-stu-id="fefff-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="fefff-127">Criar URLs de retorno de chamada com uma data de expiração</span><span class="sxs-lookup"><span data-stu-id="fefff-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="fefff-128">Se você estiver compartilhando Olá URL com terceiros, você pode gerar URLs com chaves específicas e datas de expiração conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="fefff-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="fefff-129">Você pode facilmente reverter chaves de, ou garantir acesso toofire um aplicativo é restrito tooa determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="fefff-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="fefff-130">Você pode especificar uma data de validade para uma URL por meio de saudação [lógica aplicativos REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="fefff-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="fefff-131">No corpo do hello, incluir a propriedade de saudação `NotAfter` como uma cadeia de caracteres JSON data, que retorna uma URL de retorno de chamada que só é válida até Olá `NotAfter` data e hora.</span><span class="sxs-lookup"><span data-stu-id="fefff-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="fefff-132">Criar URLs com chave secreta primária ou secundária</span><span class="sxs-lookup"><span data-stu-id="fefff-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="fefff-133">Quando você gera ou lista de URLs de retorno de chamada para baseado em solicitação gatilhos, você também pode especificar qual URL de saudação toosign toouse chave.</span><span class="sxs-lookup"><span data-stu-id="fefff-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="fefff-134">Você pode gerar uma URL assinada por uma chave específica por meio de saudação [lógica aplicativos REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="fefff-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="fefff-135">No corpo do hello, incluir a propriedade de saudação `KeyType` como `Primary` ou `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="fefff-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="fefff-136">Isso retorna uma URL assinada pela chave segura de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="fefff-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="fefff-137">Restringir endereços IP de entrada</span><span class="sxs-lookup"><span data-stu-id="fefff-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="fefff-138">Além disso toohello assinatura de acesso compartilhado, talvez você queira toorestrict chamar um aplicativo lógico somente de clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="fefff-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="fefff-139">Por exemplo, se você gerenciar seu ponto de extremidade por meio do gerenciamento de API do Azure, você pode restringir lógica Olá aplicativo tooonly aceitar solicitação de hello quando a solicitação hello proveniente Olá endereço IP de instância de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fefff-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="fefff-140">Essa configuração pode ser configurada nas configurações de aplicativo hello lógica:</span><span class="sxs-lookup"><span data-stu-id="fefff-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="fefff-141">No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooadd as restrições de endereço IP</span><span class="sxs-lookup"><span data-stu-id="fefff-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="fefff-142">Clique em Olá **configuração de controle de acesso** item de menu no **configurações**</span><span class="sxs-lookup"><span data-stu-id="fefff-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="fefff-143">Especificar lista de saudação do toobe de intervalos de endereço IP aceito pelo gatilho Olá</span><span class="sxs-lookup"><span data-stu-id="fefff-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="fefff-144">Um intervalo IP válido assume o formato de saudação `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="fefff-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="fefff-145">Se você desejar Olá lógica aplicativo tooonly incêndio como um aplicativo lógica aninhada, selecione Olá **somente outros aplicativos lógicos** opção.</span><span class="sxs-lookup"><span data-stu-id="fefff-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="fefff-146">Esta opção grava um recurso de toohello matriz em branco, que significa que somente chamadas de saudação próprio serviço incêndio (pai lógica aplicativos) com êxito.</span><span class="sxs-lookup"><span data-stu-id="fefff-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="fefff-147">Você ainda pode executar um aplicativo de lógica com um gatilho de solicitação por meio da API REST de saudação / gerenciamento `/triggers/{triggerName}/run` independentemente de IP.</span><span class="sxs-lookup"><span data-stu-id="fefff-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="fefff-148">Esse cenário requer autenticação em relação a saudação API REST do Azure, e todos os eventos apareceria em Olá Log de auditoria do Azure.</span><span class="sxs-lookup"><span data-stu-id="fefff-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="fefff-149">Defina políticas de controle de acesso de apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="fefff-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="fefff-150">Definir intervalos de IP na definição de recurso Olá</span><span class="sxs-lookup"><span data-stu-id="fefff-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="fefff-151">Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) tooautomate suas implantações, as configurações de intervalo IP hello podem ser configuradas no modelo de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="fefff-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="fefff-152">Adicionar Azure Active Directory, OAuth, ou outra proteção</span><span class="sxs-lookup"><span data-stu-id="fefff-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="fefff-153">tooadd autorização mais protocolos na parte superior de um aplicativo lógico, [gerenciamento do Azure API](https://azure.microsoft.com/services/api-management/) oferece avançados de monitoramento, segurança, política e documentação para qualquer ponto de extremidade com hello recurso tooexpose um aplicativo lógico como uma API.</span><span class="sxs-lookup"><span data-stu-id="fefff-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="fefff-154">Gerenciamento de API do Azure podem expor um ponto de extremidade público ou privado para o aplicativo lógico hello, o que poderia usar o Active Directory do Azure, certificado, OAuth ou outros padrões de segurança.</span><span class="sxs-lookup"><span data-stu-id="fefff-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="fefff-155">Quando uma solicitação é recebida, o gerenciamento de API do Azure encaminha aplicativo hello solicitação toohello lógico (executando qualquer transformações necessárias ou restrições em andamento).</span><span class="sxs-lookup"><span data-stu-id="fefff-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="fefff-156">Você pode usar o intervalo IP entrado Olá Olá lógica aplicativo tooonly configurações permitem que Olá lógica aplicativo toobe disparado do gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fefff-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="fefff-157">Proteger o acesso toomanage ou editar os aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="fefff-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="fefff-158">Você pode restringir o acesso toomanagement operações em um aplicativo lógico para que somente usuários específicos ou grupos sejam tooperform capaz de operações no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="fefff-159">Aplicativos lógicos usam hello Azure [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) de recursos e pode ser personalizada com hello mesmas ferramentas.</span><span class="sxs-lookup"><span data-stu-id="fefff-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="fefff-160">Há algumas funções internas que você pode atribuir os membros de sua assinatura tooas também:</span><span class="sxs-lookup"><span data-stu-id="fefff-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="fefff-161">**Lógica aplicativo Colaborador** -fornece acesso tooview, editar e atualizar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="fefff-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="fefff-162">Não é possível remover o recurso de saudação ou executar operações de administração.</span><span class="sxs-lookup"><span data-stu-id="fefff-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="fefff-163">**Operador de aplicativo de lógica** - pode exibir o aplicativo de lógica de saudação e histórico de execução e habilitar/desabilitar.</span><span class="sxs-lookup"><span data-stu-id="fefff-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="fefff-164">Não é possível editar ou atualizar definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="fefff-165">Você também pode usar [bloqueio de recurso do Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent alterar ou excluir aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="fefff-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="fefff-166">Esse recurso é tooprevent valiosos recursos de produção de alterações ou exclusões.</span><span class="sxs-lookup"><span data-stu-id="fefff-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="fefff-167">Acesso seguro toocontents de saudação histórico de execução</span><span class="sxs-lookup"><span data-stu-id="fefff-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="fefff-168">Você pode restringir o acesso toocontents de entradas ou saídas em intervalos de endereço IP do anteriores é executado toospecific.</span><span class="sxs-lookup"><span data-stu-id="fefff-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="fefff-169">Todos os dados dentro de uma execução de fluxo de trabalho são criptografados em trânsito e em repouso.</span><span class="sxs-lookup"><span data-stu-id="fefff-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="fefff-170">Quando um histórico de toorun chamada é feito, o serviço de saudação autentica a solicitação hello e fornece links toohello solicitação e saídas e entradas de resposta.</span><span class="sxs-lookup"><span data-stu-id="fefff-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="fefff-171">Esse link pode ser protegidas solicitações de forma que só tooview conteúdo de um intervalo de endereço IP designado retornar o conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="fefff-172">Você pode usar essa funcionalidade para controle de acesso adicional.</span><span class="sxs-lookup"><span data-stu-id="fefff-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="fefff-173">Você pode até mesmo especificar um endereço IP como `0.0.0.0` para que ninguém possa acessar entradas/saídas.</span><span class="sxs-lookup"><span data-stu-id="fefff-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="fefff-174">Somente uma pessoa com permissões de administrador pode remover essa restrição, fornecendo a possibilidade de saudação para conteúdo de tooworkflow de acesso 'just-in-time'.</span><span class="sxs-lookup"><span data-stu-id="fefff-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="fefff-175">Essa configuração pode ser definida nas configurações de recurso de saudação de saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="fefff-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="fefff-176">No portal do Azure de Olá, abra o aplicativo de lógica de Olá deseja tooadd as restrições de endereço IP</span><span class="sxs-lookup"><span data-stu-id="fefff-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="fefff-177">Clique em Olá **configuração de controle de acesso** item de menu no **configurações**</span><span class="sxs-lookup"><span data-stu-id="fefff-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="fefff-178">Especificar Olá lista de intervalos de endereços IP para acesso toocontent</span><span class="sxs-lookup"><span data-stu-id="fefff-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="fefff-179">Definir intervalos de IP na definição de recurso Olá</span><span class="sxs-lookup"><span data-stu-id="fefff-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="fefff-180">Se você estiver usando um [modelo de implantação](logic-apps-create-deploy-template.md) tooautomate suas implantações, as configurações de intervalo IP hello podem ser configuradas no modelo de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="fefff-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="fefff-181">Proteger parâmetros e entradas em um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="fefff-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="fefff-182">Talvez você queira tooparameterize alguns aspectos de uma definição de fluxo de trabalho para implantação em ambientes.</span><span class="sxs-lookup"><span data-stu-id="fefff-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="fefff-183">Além disso, alguns parâmetros podem estar seguros parâmetros que você não quiser tooappear ao editar um fluxo de trabalho, como uma ID de cliente e o segredo do cliente para [autenticação do Active Directory do Azure](../connectors/connectors-native-http.md#authentication) de uma ação HTTP.</span><span class="sxs-lookup"><span data-stu-id="fefff-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="fefff-184">Usar parâmetros e proteger parâmetros</span><span class="sxs-lookup"><span data-stu-id="fefff-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="fefff-185">tooaccess Olá valor de um parâmetro de recurso em tempo de execução, hello [linguagem de definição de fluxo de trabalho](http://aka.ms/logicappsdocs) fornece um `@parameters()` operação.</span><span class="sxs-lookup"><span data-stu-id="fefff-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="fefff-186">Além disso, você pode [especificar parâmetros em um modelo de implantação de recursos de saudação](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="fefff-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="fefff-187">Porém, se você especificar o tipo de parâmetro hello como `securestring`, parâmetro hello não será retornado com rest Olá Olá da definição do recurso e não poderão ser acessado exibindo recursos Olá após a implantação.</span><span class="sxs-lookup"><span data-stu-id="fefff-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="fefff-188">Se o parâmetro é usado em cabeçalhos de saudação ou corpo de uma solicitação, o parâmetro hello pode estar visível acessando o histórico de saudação executar e solicitações HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="fefff-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="fefff-189">Verifique se tooset suas políticas de acesso ao conteúdo adequadamente.</span><span class="sxs-lookup"><span data-stu-id="fefff-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="fefff-190">Cabeçalhos de autorização nunca são visíveis por meio de entradas ou saídas.</span><span class="sxs-lookup"><span data-stu-id="fefff-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="fefff-191">Se segredo hello está sendo usado há, segredo Olá não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="fefff-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="fefff-192">Modelo de implantação de recursos com segredos</span><span class="sxs-lookup"><span data-stu-id="fefff-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="fefff-193">Olá, exemplo a seguir mostra uma implantação que faz referência a um parâmetro seguro de `secret` em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="fefff-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="fefff-194">Em um arquivo de parâmetros separados, você pode especificar o valor de ambiente Olá para Olá `secret`, ou use [Azure o Gerenciador de recursos KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve segredos na hora da implantação.</span><span class="sxs-lookup"><span data-stu-id="fefff-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

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
                "body": "This is hello request"
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

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="fefff-195">Proteger o acesso tooservices solicitações de recebimento de um fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="fefff-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="fefff-196">Há muitos toohelp de maneiras segura de que qualquer aplicativo de lógica de saudação do ponto de extremidade precisa tooaccess.</span><span class="sxs-lookup"><span data-stu-id="fefff-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="fefff-197">Usar a autenticação em solicitações de saída</span><span class="sxs-lookup"><span data-stu-id="fefff-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="fefff-198">Ao trabalhar com um HTTP, HTTP + Swagger (API Open) ou ação de Webhook, você pode adicionar autenticação toohello solicitação.</span><span class="sxs-lookup"><span data-stu-id="fefff-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="fefff-199">Você pode incluir a autenticação básica, autenticação de certificado ou autenticação do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fefff-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="fefff-200">Obter detalhes sobre como tooconfigure essa autenticação pode ser encontrada [neste artigo](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="fefff-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="fefff-201">Restringir o acesso toologic aplicativo endereços</span><span class="sxs-lookup"><span data-stu-id="fefff-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="fefff-202">Todas as chamadas de aplicativos lógicos vêm de um conjunto específico de endereços IP por região.</span><span class="sxs-lookup"><span data-stu-id="fefff-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="fefff-203">Você pode adicionar filtragem adicional tooonly aceitar as solicitações dos endereços IP de designado.</span><span class="sxs-lookup"><span data-stu-id="fefff-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="fefff-204">Para obter uma lista desses endereços IP, consulte [limites e configuração do aplicativo lógico](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="fefff-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="fefff-205">Conectividade local</span><span class="sxs-lookup"><span data-stu-id="fefff-205">On-premises connectivity</span></span>

<span data-ttu-id="fefff-206">Aplicativos lógicos fornecem integração com vários tooprovide serviços segura e confiável de comunicação no local.</span><span class="sxs-lookup"><span data-stu-id="fefff-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="fefff-207">Gateway de dados local</span><span class="sxs-lookup"><span data-stu-id="fefff-207">On-premises data gateway</span></span>

<span data-ttu-id="fefff-208">Muitos conectores gerenciados para os aplicativos lógicos fornecem conectividade segura entre sistemas de tooon locais, incluindo o sistema de arquivos, SQL, SharePoint, DB2 e muito mais.</span><span class="sxs-lookup"><span data-stu-id="fefff-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="fefff-209">gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="fefff-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="fefff-210">Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fefff-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="fefff-211">Saiba mais sobre [como funciona o gateway de dados Olá](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="fefff-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="fefff-212">Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="fefff-212">Azure API Management</span></span>

<span data-ttu-id="fefff-213">[Gerenciamento de API do Azure](https://azure.microsoft.com/services/api-management/) tem opções de conectividade local, incluindo a integração de rota expressa e VPN site a site para sistemas de tooon locais de proxy e comunicação seguras.</span><span class="sxs-lookup"><span data-stu-id="fefff-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="fefff-214">Olá lógica de aplicativo Designer, você pode selecionar uma API exposta do gerenciamento de API do Azure dentro de um fluxo de trabalho, fornecendo acesso rápido a sistemas locais tooon rapidamente.</span><span class="sxs-lookup"><span data-stu-id="fefff-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="fefff-215">Conexões híbridas do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="fefff-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="fefff-216">Você pode usar o recurso de conexão de híbrido do hello local para a API do Azure e Web apps toocommunicate local.</span><span class="sxs-lookup"><span data-stu-id="fefff-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="fefff-217">Obter detalhes sobre conexões híbridas e como pode ser encontrado tooconfigure [neste artigo](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fefff-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fefff-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fefff-218">Next steps</span></span>
[<span data-ttu-id="fefff-219">Criar um modelo de implantação</span><span class="sxs-lookup"><span data-stu-id="fefff-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="fefff-220">Manipulação de exceção</span><span class="sxs-lookup"><span data-stu-id="fefff-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="fefff-221">Monitorar seus aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="fefff-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="fefff-222">Diagnosticando falhas e problemas nos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="fefff-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
