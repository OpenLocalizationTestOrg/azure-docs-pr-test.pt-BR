---
title: aaaPolicies no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como toocreate, editar e configurar políticas de gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="d64ac-103">Políticas do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="d64ac-103">Policies in Azure API Management</span></span>
<span data-ttu-id="d64ac-104">No gerenciamento de API do Azure, as políticas são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="d64ac-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="d64ac-105">As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="d64ac-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="d64ac-106">As instruções populares incluem conversão de formato de XML tooJSON e limitando toorestrict Olá quantidade de chamadas de entrada de um desenvolvedor de taxa de chamada.</span><span class="sxs-lookup"><span data-stu-id="d64ac-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="d64ac-107">Muitas outras políticas estão disponíveis sem a necessidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="d64ac-108">Consulte Olá [referência de política] [ Policy Reference] para obter uma lista completa de declarações de política e suas configurações.</span><span class="sxs-lookup"><span data-stu-id="d64ac-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="d64ac-109">As políticas são aplicadas dentro de gateway Olá que fica entre consumidores de API hello e API Olá gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d64ac-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="d64ac-110">Olá gateway recebe todas as solicitações e geralmente encaminha inalteradas toohello subjacente API.</span><span class="sxs-lookup"><span data-stu-id="d64ac-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="d64ac-111">No entanto uma política pode ser aplicada a solicitação de entrada alterações tooboth hello e resposta de saída.</span><span class="sxs-lookup"><span data-stu-id="d64ac-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="d64ac-112">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="d64ac-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="d64ac-113">Algumas políticas, como Olá [fluxo de controle] [ Control flow] e [Set variable] [ Set variable] políticas se baseiam em expressões de política.</span><span class="sxs-lookup"><span data-stu-id="d64ac-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="d64ac-114">Para obter mais informações, confira [Políticas avançadas][Advanced policies] e [Expressões de política][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="d64ac-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="d64ac-115"><a name="scopes"></a>Como tooconfigure políticas</span><span class="sxs-lookup"><span data-stu-id="d64ac-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="d64ac-116">Políticas podem ser configuradas globalmente ou no escopo de saudação de um [produto][Product], [API] [ API] ou [operação] [Operation].</span><span class="sxs-lookup"><span data-stu-id="d64ac-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="d64ac-117">tooconfigure uma política, navegue toohello editor de políticas no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="d64ac-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Menu de políticas][policies-menu]

<span data-ttu-id="d64ac-119">editor de políticas de saudação consiste em três seções principais: Olá política (superior), Olá política definição de escopo em que as diretivas são editadas (esquerdo) e listam de instruções de saudação (à direita):</span><span class="sxs-lookup"><span data-stu-id="d64ac-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Editor de políticas][policies-editor]

<span data-ttu-id="d64ac-121">toobegin configurar uma política, que você deve primeiro selecionar escopo Olá no qual Olá política deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="d64ac-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="d64ac-122">Na captura de tela abaixo Olá Olá **Starter** produto é selecionado.</span><span class="sxs-lookup"><span data-stu-id="d64ac-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="d64ac-123">Observe que Olá símbolo quadrado próximo toohello política nome indica que uma política já foi aplicada nesse nível.</span><span class="sxs-lookup"><span data-stu-id="d64ac-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Escopo][policies-scope]

<span data-ttu-id="d64ac-125">Como uma política já tiver sido aplicada, configuração de saudação é mostrada na exibição de definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Configurar][policies-configure]

<span data-ttu-id="d64ac-127">política de saudação é exibida somente leitura no primeiro.</span><span class="sxs-lookup"><span data-stu-id="d64ac-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="d64ac-128">Na ordem tooedit definição Olá clique Olá **configurar política** ação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Editar][policies-edit]

<span data-ttu-id="d64ac-130">definição de política de saudação é um documento XML simples que descreve uma sequência de instruções de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="d64ac-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="d64ac-131">Olá XML pode ser editado diretamente na janela de definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="d64ac-132">Uma lista de instruções é fornecida toohello à direita e o escopo atual do instruções toohello aplicável estão habilitados e realçados; como demonstrado pelo Olá **limite de taxa de chamada** instrução na captura de tela de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="d64ac-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="d64ac-133">Clicar em uma instrução habilitada adicionará Olá XML apropriado no local de saudação do cursor Olá no modo de exibição de definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="d64ac-134">Se a política de saudação que você deseja tooadd não estiver habilitada, certifique-se de que você está no escopo correto de saudação dessa política.</span><span class="sxs-lookup"><span data-stu-id="d64ac-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="d64ac-135">Cada declaração de política é projetada para uso em determinados escopos e seções de política.</span><span class="sxs-lookup"><span data-stu-id="d64ac-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="d64ac-136">seções de política tooreview hello e escopos de uma política, verifique Olá **uso** seção dessa política no hello [referência de política][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="d64ac-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="d64ac-137">Uma lista completa das declarações de política e suas configurações estão disponíveis em Olá [referência de política][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="d64ac-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="d64ac-138">Por exemplo, tooadd um novo toorestrict de instrução entrada solicita toospecified endereços IP, colocar o cursor Olá apenas dentro do conteúdo de saudação do hello `inbound` Olá de elemento e clique em XML **restringir IPs de chamador** instrução.</span><span class="sxs-lookup"><span data-stu-id="d64ac-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Políticas de restrição][policies-restrict]

<span data-ttu-id="d64ac-140">Isso adicionará uma toohello de trecho de código XML `inbound` elemento que fornece orientação sobre como tooconfigure Olá instrução.</span><span class="sxs-lookup"><span data-stu-id="d64ac-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="d64ac-141">toolimit as solicitações de entrada e aceitar somente aqueles de um endereço IP de 1.2.3.4 modificar Olá XML da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d64ac-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salvar][policies-save]

<span data-ttu-id="d64ac-143">Ao concluir configuração instruções Olá para política de saudação, clique em **salvar** e alterações de saudação serão propagadas toohello gateway de gerenciamento de API imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d64ac-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="d64ac-144"><a name="sections"> </a>Compreendendo configuração de políticas</span><span class="sxs-lookup"><span data-stu-id="d64ac-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="d64ac-145">Uma política é uma série de instruções que são executadas para uma solicitação e uma resposta.</span><span class="sxs-lookup"><span data-stu-id="d64ac-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="d64ac-146">configuração de saudação é dividida adequadamente `inbound`, `backend`, `outbound`, e `on-error` seções, conforme mostrado na seguinte configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="d64ac-147">Se houver um erro durante o processamento de saudação de uma solicitação, quaisquer etapas restantes no hello `inbound`, `backend`, ou `outbound` seções são ignoradas e a execução vai toohello instruções Olá `on-error` seção.</span><span class="sxs-lookup"><span data-stu-id="d64ac-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="d64ac-148">Colocando em declarações de política em Olá `on-error` seção você pode examinar o erro hello usando Olá `context.LastError` propriedade inspecionar e personalizar resposta de erro hello usando Olá `set-body` política e configurar o que acontece se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="d64ac-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="d64ac-149">Há etapas internas e erros que podem ocorrer durante o processamento de saudação de declarações de política de códigos de erro.</span><span class="sxs-lookup"><span data-stu-id="d64ac-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="d64ac-150">Para obter mais informações, consulte [Tratamento de erros em políticas de gerenciamento de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="d64ac-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="d64ac-151">Como as políticas podem ser especificadas em diferentes níveis (global, produto, api e operação) configuração Olá fornece uma maneira para você ordem de saudação toospecify no qual instruções de definição de política Olá executado com a política do aspecto toohello pai.</span><span class="sxs-lookup"><span data-stu-id="d64ac-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="d64ac-152">Escopos de política são avaliados na ordem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d64ac-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="d64ac-153">Escopo global</span><span class="sxs-lookup"><span data-stu-id="d64ac-153">Global scope</span></span>
2. <span data-ttu-id="d64ac-154">Escopo do produto</span><span class="sxs-lookup"><span data-stu-id="d64ac-154">Product scope</span></span>
3. <span data-ttu-id="d64ac-155">Escopo de API</span><span class="sxs-lookup"><span data-stu-id="d64ac-155">API scope</span></span>
4. <span data-ttu-id="d64ac-156">Escopo de operação</span><span class="sxs-lookup"><span data-stu-id="d64ac-156">Operation scope</span></span>

<span data-ttu-id="d64ac-157">Olá instruções dentro deles são avaliadas de acordo com o posicionamento de toohello de saudação `base` elemento, se ele estiver presente.</span><span class="sxs-lookup"><span data-stu-id="d64ac-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="d64ac-158">Política global tem nenhuma política pai e usando Olá `<base>` elemento em que ele não tem nenhum efeito.</span><span class="sxs-lookup"><span data-stu-id="d64ac-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="d64ac-159">Por exemplo, se você tiver uma política no nível global hello e uma política configurada para uma API, em seguida, sempre que essa API em particular é usado ambas as políticas serão ser aplicadas.</span><span class="sxs-lookup"><span data-stu-id="d64ac-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="d64ac-160">Gerenciamento de API permite determinística ordenação de instruções de política combinados por meio do elemento base hello.</span><span class="sxs-lookup"><span data-stu-id="d64ac-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="d64ac-161">Na definição de política exemplo hello acima, Olá `cross-domain` instrução será executado antes de todas as políticas mais alto que por sua vez, ser seguido por Olá `find-and-replace` política.</span><span class="sxs-lookup"><span data-stu-id="d64ac-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="d64ac-162">políticas de saudação toosee no escopo de saudação atual no editor de diretiva de saudação, clique **recalcular a política efetiva para o escopo selecionado**.</span><span class="sxs-lookup"><span data-stu-id="d64ac-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d64ac-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d64ac-163">Next steps</span></span>
<span data-ttu-id="d64ac-164">Confira o vídeo a seguir sobre expressões de política.</span><span class="sxs-lookup"><span data-stu-id="d64ac-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
