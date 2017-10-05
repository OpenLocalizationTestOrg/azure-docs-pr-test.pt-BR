---
title: "Como usar as propriedades nas políticas de Gerenciamento de API do Azure"
description: "Saiba como usar as propriedades nas políticas de Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="15fdb-103">Como usar as propriedades nas políticas de Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="15fdb-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="15fdb-104">As políticas de Gerenciamento de API representam um recurso poderoso do sistema e permitem ao editor alterar o comportamento da API por meio de configuração.</span><span class="sxs-lookup"><span data-stu-id="15fdb-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="15fdb-105">As políticas são um conjunto de instruções executadas em sequência, na solicitação ou na resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="15fdb-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="15fdb-106">É possível construir declarações de política usando valores de texto literais, expressões de política e propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="15fdb-107">Cada instância de serviço do Gerenciamento de API tem uma coleção de propriedades de pares de chave/valor que são globais à instância do serviço.</span><span class="sxs-lookup"><span data-stu-id="15fdb-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="15fdb-108">Essas propriedades podem ser usadas para gerenciar valores de cadeia de caracteres constantes em todas as configurações e as políticas de API.</span><span class="sxs-lookup"><span data-stu-id="15fdb-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="15fdb-109">Cada propriedade tem os atributos a seguir.</span><span class="sxs-lookup"><span data-stu-id="15fdb-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="15fdb-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="15fdb-110">Attribute</span></span> | <span data-ttu-id="15fdb-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="15fdb-111">Type</span></span> | <span data-ttu-id="15fdb-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="15fdb-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="15fdb-113">Name</span><span class="sxs-lookup"><span data-stu-id="15fdb-113">Name</span></span> |<span data-ttu-id="15fdb-114">string</span><span class="sxs-lookup"><span data-stu-id="15fdb-114">string</span></span> |<span data-ttu-id="15fdb-115">O nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="15fdb-115">The name of the property.</span></span> <span data-ttu-id="15fdb-116">Ele pode conter apenas letras, dígitos, ponto, traço e caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="15fdb-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="15fdb-117">Valor</span><span class="sxs-lookup"><span data-stu-id="15fdb-117">Value</span></span> |<span data-ttu-id="15fdb-118">string</span><span class="sxs-lookup"><span data-stu-id="15fdb-118">string</span></span> |<span data-ttu-id="15fdb-119">O valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="15fdb-119">The value of the property.</span></span> <span data-ttu-id="15fdb-120">Ele não pode ficar vazio ou conter apenas espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="15fdb-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="15fdb-121">Segredo</span><span class="sxs-lookup"><span data-stu-id="15fdb-121">Secret</span></span> |<span data-ttu-id="15fdb-122">Booliano</span><span class="sxs-lookup"><span data-stu-id="15fdb-122">boolean</span></span> |<span data-ttu-id="15fdb-123">Determina se o valor é um segredo e se deve ser criptografado ou não.</span><span class="sxs-lookup"><span data-stu-id="15fdb-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="15fdb-124">Marcas</span><span class="sxs-lookup"><span data-stu-id="15fdb-124">Tags</span></span> |<span data-ttu-id="15fdb-125">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="15fdb-125">array of string</span></span> |<span data-ttu-id="15fdb-126">Marcas opcionais que, quando fornecidas, podem ser usadas para filtrar a lista de propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="15fdb-127">As propriedades são configuradas no portal do editor na guia **Propriedades** .</span><span class="sxs-lookup"><span data-stu-id="15fdb-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="15fdb-128">No exemplo a seguir, três propriedades são configuradas.</span><span class="sxs-lookup"><span data-stu-id="15fdb-128">In the following example, three properties are configured.</span></span>

![Propriedades][api-management-properties]

<span data-ttu-id="15fdb-130">Os valores de propriedade podem conter cadeias de caracteres literais e [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="15fdb-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="15fdb-131">A tabela a seguir mostra as propriedades dos três exemplos anteriores e seus atributos.</span><span class="sxs-lookup"><span data-stu-id="15fdb-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="15fdb-132">O valor de `ExpressionProperty` é uma expressão de política que retorna uma cadeia de caracteres com a data e a hora atuais.</span><span class="sxs-lookup"><span data-stu-id="15fdb-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="15fdb-133">A propriedade `ContosoHeaderValue` é marcada como um segredo e, portanto, seu valor não é exibido.</span><span class="sxs-lookup"><span data-stu-id="15fdb-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="15fdb-134">Name</span><span class="sxs-lookup"><span data-stu-id="15fdb-134">Name</span></span> | <span data-ttu-id="15fdb-135">Valor</span><span class="sxs-lookup"><span data-stu-id="15fdb-135">Value</span></span> | <span data-ttu-id="15fdb-136">Segredo</span><span class="sxs-lookup"><span data-stu-id="15fdb-136">Secret</span></span> | <span data-ttu-id="15fdb-137">Marcas</span><span class="sxs-lookup"><span data-stu-id="15fdb-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="15fdb-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="15fdb-138">ContosoHeader</span></span> |<span data-ttu-id="15fdb-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="15fdb-139">TrackingId</span></span> |<span data-ttu-id="15fdb-140">Falso</span><span class="sxs-lookup"><span data-stu-id="15fdb-140">False</span></span> |<span data-ttu-id="15fdb-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="15fdb-141">Contoso</span></span> |
| <span data-ttu-id="15fdb-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="15fdb-142">ContosoHeaderValue</span></span> |<span data-ttu-id="15fdb-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="15fdb-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="15fdb-144">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="15fdb-144">True</span></span> |<span data-ttu-id="15fdb-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="15fdb-145">Contoso</span></span> |
| <span data-ttu-id="15fdb-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="15fdb-146">ExpressionProperty</span></span> |<span data-ttu-id="15fdb-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="15fdb-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="15fdb-148">Falso</span><span class="sxs-lookup"><span data-stu-id="15fdb-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="15fdb-149">Para usar uma propriedade</span><span class="sxs-lookup"><span data-stu-id="15fdb-149">To use a property</span></span>
<span data-ttu-id="15fdb-150">Para usar uma propriedade em uma política, coloque o nome da propriedade entre dois pares de chaves, como em `{{ContosoHeader}}`, de acordo com o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="15fdb-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="15fdb-151">Neste exemplo, `ContosoHeader` é usado como o nome de um cabeçalho em uma política `set-header` e `ContosoHeaderValue` é usado como o valor desse cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="15fdb-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="15fdb-152">Quando essa política é avaliada durante uma solicitação ou uma resposta para o gateway de Gerenciamento de API, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` são substituídos pelos valores de suas respectivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="15fdb-153">As propriedades podem ser usadas como valores de atributo ou de elemento, como mostra o exemplo anterior, mas também podem ser inseridas ou combinadas com parte de uma expressão de texto literal, como mostra o exemplo a seguir: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="15fdb-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="15fdb-154">As propriedades também podem conter expressões de política.</span><span class="sxs-lookup"><span data-stu-id="15fdb-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="15fdb-155">No exemplo a seguir, o `ExpressionProperty` é usado.</span><span class="sxs-lookup"><span data-stu-id="15fdb-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="15fdb-156">Quando essa política é avaliada, `{{ExpressionProperty}}` é substituído por seu valor: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="15fdb-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="15fdb-157">Como o valor é uma expressão de política, a expressão é avaliada e a política prossegue com a execução.</span><span class="sxs-lookup"><span data-stu-id="15fdb-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="15fdb-158">Você pode testar isso no portal do desenvolvedor chamando uma operação que tenha uma política com propriedades no escopo.</span><span class="sxs-lookup"><span data-stu-id="15fdb-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="15fdb-159">No exemplo a seguir, uma operação é chamada com os dois exemplos de políticas `set-header` anteriores com propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="15fdb-160">Observe que a resposta contém dois cabeçalhos personalizados configurados usando políticas com propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Portal do desenvolvedor][api-management-send-results]

<span data-ttu-id="15fdb-162">Se você analisar o [rastreamento do Inspetor de API](api-management-howto-api-inspector.md) de uma chamada que inclui os dois exemplos de política anteriores com propriedades, será possível ver as duas políticas `set-header` com os valores de propriedade inseridos, bem como a avaliação da expressão de política para a propriedade que continha a expressão de política.</span><span class="sxs-lookup"><span data-stu-id="15fdb-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Rastreamento do Inspetor de API][api-management-api-inspector-trace]

<span data-ttu-id="15fdb-164">Observe que, embora os valores de propriedade possam conter expressões de política, os valores de propriedade não podem conter outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="15fdb-165">Se um texto contendo uma referência de propriedade for usado para um valor de propriedade, por exemplo, `Property value text {{MyProperty}}`, essa referência de propriedade não será substituída e será incluída como parte do valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="15fdb-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="15fdb-166">Para criar uma propriedade</span><span class="sxs-lookup"><span data-stu-id="15fdb-166">To create a property</span></span>
<span data-ttu-id="15fdb-167">Para criar uma propriedade, clique em **Adicionar propriedade** na guia **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="15fdb-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Adicionar propriedade][api-management-properties-add-property-menu]

<span data-ttu-id="15fdb-169">**Nome** e **Valor** são valores obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="15fdb-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="15fdb-170">Se o valor dessa propriedade for um segredo, marque a caixa de seleção **Isto é um segredo** .</span><span class="sxs-lookup"><span data-stu-id="15fdb-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="15fdb-171">Insira uma ou mais marcas opcionais para ajudar a organizar suas propriedades e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="15fdb-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Adicionar propriedade][api-management-properties-add-property]

<span data-ttu-id="15fdb-173">Quando uma nova propriedade for salva, a caixa de texto **Propriedade de pesquisa** será preenchida com o nome da nova propriedade e a nova propriedade será exibida.</span><span class="sxs-lookup"><span data-stu-id="15fdb-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="15fdb-174">Para exibir todas as propriedades, desmarque a caixa de texto **Propriedade de pesquisa** e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="15fdb-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Propriedades][api-management-properties-property-saved]

<span data-ttu-id="15fdb-176">Para saber mais sobre como criar uma propriedade usando a API REST, confira [Criar uma propriedade usando a API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="15fdb-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="15fdb-177">Para editar uma propriedade</span><span class="sxs-lookup"><span data-stu-id="15fdb-177">To edit a property</span></span>
<span data-ttu-id="15fdb-178">Para editar uma propriedade, clique em **Editar** ao lado da propriedade que você quer editar.</span><span class="sxs-lookup"><span data-stu-id="15fdb-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Editar propriedade][api-management-properties-edit]

<span data-ttu-id="15fdb-180">Faça as alterações desejadas e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="15fdb-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="15fdb-181">Se você alterar o nome da propriedade, todas as políticas que fizerem referência a essa propriedade serão automaticamente atualizadas para usar o novo nome.</span><span class="sxs-lookup"><span data-stu-id="15fdb-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Editar propriedade][api-management-properties-edit-property]

<span data-ttu-id="15fdb-183">Para saber mais sobre como editar uma propriedade usando a API REST, confira [Editar uma propriedade usando a API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="15fdb-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="15fdb-184">Para excluir uma propriedade</span><span class="sxs-lookup"><span data-stu-id="15fdb-184">To delete a property</span></span>
<span data-ttu-id="15fdb-185">Para excluir uma propriedade, clique em **Excluir** ao lado da propriedade que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="15fdb-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Excluir propriedade][api-management-properties-delete]

<span data-ttu-id="15fdb-187">Clique em **Sim, excluir** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="15fdb-187">Click **Yes, delete it** to confirm.</span></span>

![Confirmar exclusão][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="15fdb-189">Se a propriedade for consultada por quaisquer políticas, não será possível excluí-la até que você remova a propriedade de todas as políticas que a utilizam.</span><span class="sxs-lookup"><span data-stu-id="15fdb-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="15fdb-190">Para saber mais sobre como excluir uma propriedade usando a API REST, confira [Excluir uma propriedade usando a API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="15fdb-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="15fdb-191">Para pesquisar e filtrar propriedades</span><span class="sxs-lookup"><span data-stu-id="15fdb-191">To search and filter properties</span></span>
<span data-ttu-id="15fdb-192">A guia **Propriedades** inclui recursos de pesquisa e filtragem para ajudar você a gerenciar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="15fdb-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="15fdb-193">Para filtrar a lista de propriedades pelo nome da propriedade, insira um termo de pesquisa na caixa de texto **Propriedade de pesquisa** .</span><span class="sxs-lookup"><span data-stu-id="15fdb-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="15fdb-194">Para exibir todas as propriedades, desmarque a caixa de texto **Propriedade de pesquisa** e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="15fdb-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Pesquisar][api-management-properties-search]

<span data-ttu-id="15fdb-196">Para filtrar a lista de propriedades por valores de marca, insira uma ou mais marcas na caixa de texto **Filtrar por marcas** .</span><span class="sxs-lookup"><span data-stu-id="15fdb-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="15fdb-197">Para exibir todas as propriedades, desmarque a caixa de texto **Filtrar por marcas** e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="15fdb-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtro][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="15fdb-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15fdb-199">Next steps</span></span>
* <span data-ttu-id="15fdb-200">Saiba mais sobre como trabalhar com políticas</span><span class="sxs-lookup"><span data-stu-id="15fdb-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="15fdb-201">Políticas no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="15fdb-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="15fdb-202">Referência de política</span><span class="sxs-lookup"><span data-stu-id="15fdb-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="15fdb-203">Expressões de política</span><span class="sxs-lookup"><span data-stu-id="15fdb-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="15fdb-204">Assista a uma visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="15fdb-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

