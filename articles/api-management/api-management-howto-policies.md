---
title: "Políticas no Gerenciamento de API do Azure | Microsoft Docs"
description: "Aprenda a criar, editar e configurar políticas de Gerenciamento de API."
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
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="d6ace-103">Políticas do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="d6ace-103">Policies in Azure API Management</span></span>
<span data-ttu-id="d6ace-104">No Gerenciamento de API do Azure, as políticas são uma poderosa funcionalidade do sistema que permite ao editor alterar o comportamento da API por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="d6ace-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="d6ace-105">As políticas são um conjunto de instruções executadas em sequência, no momento da solicitação ou da resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="d6ace-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="d6ace-106">Instruções populares incluem a conversão do formato de XML para JSON e limite de taxa de chamada para restringir a quantidade de chamadas recebidas de um desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="d6ace-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="d6ace-107">Muitas políticas estão disponíveis pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="d6ace-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="d6ace-108">Consulte a [Referência de Política][Policy Reference] para ver uma lista completa das instruções de política e suas configurações.</span><span class="sxs-lookup"><span data-stu-id="d6ace-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="d6ace-109">As políticas são aplicadas dentro do gateway que fica entre o consumidor da API e a API gerenciada.</span><span class="sxs-lookup"><span data-stu-id="d6ace-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="d6ace-110">O gateway recebe todas as solicitações e normalmente as encaminha inalteradas à API subjacente.</span><span class="sxs-lookup"><span data-stu-id="d6ace-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="d6ace-111">No entanto, uma política também pode aplicar mudanças à solicitação de entrada e à resposta de saída.</span><span class="sxs-lookup"><span data-stu-id="d6ace-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="d6ace-112">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de Gerenciamento de API, a menos que a política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="d6ace-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="d6ace-113">Algumas políticas como [Controlar fluxo][Control flow] e [Definir variável][Set variable] baseiam-se em expressões de políticas.</span><span class="sxs-lookup"><span data-stu-id="d6ace-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="d6ace-114">Para obter mais informações, confira [Políticas avançadas][Advanced policies] e [Expressões de política][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="d6ace-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="d6ace-115"><a name="scopes"> </a>Como configurar políticas</span><span class="sxs-lookup"><span data-stu-id="d6ace-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="d6ace-116">As políticas podem ser configuradas globalmente ou no escopo de um [Produto][Product], [API][API] ou [Operação][Operation].</span><span class="sxs-lookup"><span data-stu-id="d6ace-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="d6ace-117">Para configurar uma política, navegue até o Editor de políticas no Portal do Editor.</span><span class="sxs-lookup"><span data-stu-id="d6ace-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Menu de políticas][policies-menu]

<span data-ttu-id="d6ace-119">O editor de políticas consiste em três seções principais: o escopo de política (superior), definição de política, em que as políticas são editadas (à esquerda) e a lista de instruções (à direita):</span><span class="sxs-lookup"><span data-stu-id="d6ace-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Editor de políticas][policies-editor]

<span data-ttu-id="d6ace-121">Para começar a configurar uma política, você precisa antes selecionar o escopo ao qual ela deverá se aplicar.</span><span class="sxs-lookup"><span data-stu-id="d6ace-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="d6ace-122">Na captura de tela abaixo, foi selecionado o produto **Inicial**.</span><span class="sxs-lookup"><span data-stu-id="d6ace-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="d6ace-123">Observe que o símbolo de quadrado ao lado do nome da política indica que ela já está aplicada a este nível.</span><span class="sxs-lookup"><span data-stu-id="d6ace-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Escopo][policies-scope]

<span data-ttu-id="d6ace-125">Uma vez que a política já foi aplicada, a configuração é mostrada na exibição de definição.</span><span class="sxs-lookup"><span data-stu-id="d6ace-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configurar][policies-configure]

<span data-ttu-id="d6ace-127">Primeiro, a política é exibida em formato somente leitura.</span><span class="sxs-lookup"><span data-stu-id="d6ace-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="d6ace-128">Para editar a definição, clique na ação **Configurar Política** .</span><span class="sxs-lookup"><span data-stu-id="d6ace-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Editar][policies-edit]

<span data-ttu-id="d6ace-130">A definição da política é um documento XML simples que descreve uma sequência de instruções de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="d6ace-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="d6ace-131">O XML pode ser editado diretamente na janela de definição.</span><span class="sxs-lookup"><span data-stu-id="d6ace-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="d6ace-132">Uma lista de instruções é fornecida à direita e as declarações aplicáveis ao escopo atual ficam habilitadas e destacadas, conforme demonstrado pela instrução **Limit Call Rate** (Taxa limite de chamadas) na captura de tela acima.</span><span class="sxs-lookup"><span data-stu-id="d6ace-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="d6ace-133">Clicar em uma instrução habilitada adicionará o XML adequado ao local onde estiver o cursor na exibição de definição.</span><span class="sxs-lookup"><span data-stu-id="d6ace-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6ace-134">Se a política que deseja adicionar não estiver habilitada, verifique se você está no escopo correto para essa política.</span><span class="sxs-lookup"><span data-stu-id="d6ace-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="d6ace-135">Cada declaração de política é projetada para uso em determinados escopos e seções de política.</span><span class="sxs-lookup"><span data-stu-id="d6ace-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="d6ace-136">Para examinar as seções da política e os escopos de uma política, verifique a seção **Uso** dessa política na [Referência à política][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="d6ace-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="d6ace-137">Uma lista completa de instruções de políticas e suas configurações está disponível na [Referência de política][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="d6ace-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="d6ace-138">Por exemplo, para adicionar uma nova instrução para restringir as solicitações de entrada a endereços IP especificados, posicione o cursor dentro do conteúdo do elemento XML `inbound` e clique na instrução **Restringir IPs de chamada** .</span><span class="sxs-lookup"><span data-stu-id="d6ace-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Políticas de restrição][policies-restrict]

<span data-ttu-id="d6ace-140">Isto adicionará um trecho XML ao elemento `inbound` que fornecerá diretrizes de como configurar a instrução.</span><span class="sxs-lookup"><span data-stu-id="d6ace-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="d6ace-141">Para limitar as solicitações de entrada e aceitar somente as provenientes de um endereço IP 1.2.3.4, modifique o XML da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d6ace-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salvar][policies-save]

<span data-ttu-id="d6ace-143">Quando concluir a configuração das instruções da política, clique em **Salvar** para que as alterações sejam propagadas para o gateway de Gerenciamento de API imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d6ace-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="d6ace-144"><a name="sections"> </a>Compreendendo configuração de políticas</span><span class="sxs-lookup"><span data-stu-id="d6ace-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="d6ace-145">Uma política é uma série de instruções que são executadas para uma solicitação e uma resposta.</span><span class="sxs-lookup"><span data-stu-id="d6ace-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="d6ace-146">A configuração é dividida adequadamente entre as seções `inbound`, `backend`, `outbound` e `on-error`, conforme demonstrado na configuração seguinte.</span><span class="sxs-lookup"><span data-stu-id="d6ace-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="d6ace-147">Se houver um erro durante o processamento de uma solicitação, quaisquer etapas restantes nas seções `inbound`, `backend` ou `outbound` serão ignoradas e a execução saltará para as instruções na seção `on-error`.</span><span class="sxs-lookup"><span data-stu-id="d6ace-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="d6ace-148">Ao colocar instruções de políticas na seção `on-error`, você pode revisar o erro usando a propriedade `context.LastError`, inspecionar e personalizar a resposta de erro usando a política `set-body` e configurar o que acontece se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="d6ace-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="d6ace-149">Há códigos de erro para obter as etapas internas e erros que podem ocorrer durante o processamento de instruções de política.</span><span class="sxs-lookup"><span data-stu-id="d6ace-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="d6ace-150">Para obter mais informações, consulte [Tratamento de erros em políticas de gerenciamento de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6ace-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="d6ace-151">Uma vez que as políticas podem ser especificadas em diferentes níveis (global, de produto, API e operação), a configuração oferece uma forma de especifica a ordem na qual as instruções dessa definição são executadas com relação à política pai.</span><span class="sxs-lookup"><span data-stu-id="d6ace-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="d6ace-152">Os escopos de política são avaliados na ordem a seguir.</span><span class="sxs-lookup"><span data-stu-id="d6ace-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="d6ace-153">Escopo global</span><span class="sxs-lookup"><span data-stu-id="d6ace-153">Global scope</span></span>
2. <span data-ttu-id="d6ace-154">Escopo do produto</span><span class="sxs-lookup"><span data-stu-id="d6ace-154">Product scope</span></span>
3. <span data-ttu-id="d6ace-155">Escopo de API</span><span class="sxs-lookup"><span data-stu-id="d6ace-155">API scope</span></span>
4. <span data-ttu-id="d6ace-156">Escopo de operação</span><span class="sxs-lookup"><span data-stu-id="d6ace-156">Operation scope</span></span>

<span data-ttu-id="d6ace-157">As declarações dentro deles são avaliadas de acordo com o posicionamento do elemento `base` , se ele estiver presente.</span><span class="sxs-lookup"><span data-stu-id="d6ace-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="d6ace-158">Uma política global não tem nenhuma política pai e usar o elemento `<base>` nela não terá nenhum efeito.</span><span class="sxs-lookup"><span data-stu-id="d6ace-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="d6ace-159">Por exemplo, se você tiver uma política a nível global e uma política configurada para uma API, então, sempre que essa API em particular for usado, ambas as políticas serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="d6ace-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="d6ace-160">O Gerenciamento de API permite uma ordenação determinista de instruções de política combinadas por meio do elemento base.</span><span class="sxs-lookup"><span data-stu-id="d6ace-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="d6ace-161">No exemplo de definição de política acima, a instrução `cross-domain` seria executada antes de quaisquer políticas maiores que, por sua vez, seriam seguidas da política `find-and-replace`.</span><span class="sxs-lookup"><span data-stu-id="d6ace-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="d6ace-162">Para ver as políticas no escopo atual no editor de política, clique em **Recalcular a política efetiva para o escopo selecionado**.</span><span class="sxs-lookup"><span data-stu-id="d6ace-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6ace-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6ace-163">Next steps</span></span>
<span data-ttu-id="d6ace-164">Confira o vídeo a seguir sobre expressões de política.</span><span class="sxs-lookup"><span data-stu-id="d6ace-164">Check out following video on policy expressions.</span></span>

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
