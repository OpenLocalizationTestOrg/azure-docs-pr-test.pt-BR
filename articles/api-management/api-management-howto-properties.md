---
title: "Propriedades de toouse aaaHow nas políticas de gerenciamento de API do Azure"
description: "Saiba como propriedades toouse nas políticas de gerenciamento de API do Azure."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="79909-103">Como propriedades toouse nas políticas de gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="79909-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="79909-104">Políticas de gerenciamento de API são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="79909-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="79909-105">As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="79909-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="79909-106">É possível construir declarações de política usando valores de texto literais, expressões de política e propriedades.</span><span class="sxs-lookup"><span data-stu-id="79909-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="79909-107">Cada instância de serviço de gerenciamento de API tem uma coleção de propriedades de pares chave/valor que são globais toohello instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="79909-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="79909-108">Essas propriedades podem ser valores de cadeia de caracteres constante toomanage usado em todas as políticas e configurações de API.</span><span class="sxs-lookup"><span data-stu-id="79909-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="79909-109">Cada propriedade tem Olá atributos a seguir.</span><span class="sxs-lookup"><span data-stu-id="79909-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="79909-110">Atributo</span><span class="sxs-lookup"><span data-stu-id="79909-110">Attribute</span></span> | <span data-ttu-id="79909-111">Tipo</span><span class="sxs-lookup"><span data-stu-id="79909-111">Type</span></span> | <span data-ttu-id="79909-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="79909-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79909-113">Name</span><span class="sxs-lookup"><span data-stu-id="79909-113">Name</span></span> |<span data-ttu-id="79909-114">string</span><span class="sxs-lookup"><span data-stu-id="79909-114">string</span></span> |<span data-ttu-id="79909-115">nome de saudação da propriedade de saudação.</span><span class="sxs-lookup"><span data-stu-id="79909-115">hello name of hello property.</span></span> <span data-ttu-id="79909-116">Ele pode conter apenas letras, dígitos, ponto, traço e caracteres de sublinhado.</span><span class="sxs-lookup"><span data-stu-id="79909-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="79909-117">Valor</span><span class="sxs-lookup"><span data-stu-id="79909-117">Value</span></span> |<span data-ttu-id="79909-118">string</span><span class="sxs-lookup"><span data-stu-id="79909-118">string</span></span> |<span data-ttu-id="79909-119">valor de saudação da propriedade de saudação.</span><span class="sxs-lookup"><span data-stu-id="79909-119">hello value of hello property.</span></span> <span data-ttu-id="79909-120">Ele não pode ficar vazio ou conter apenas espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="79909-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="79909-121">Segredo</span><span class="sxs-lookup"><span data-stu-id="79909-121">Secret</span></span> |<span data-ttu-id="79909-122">Booliano</span><span class="sxs-lookup"><span data-stu-id="79909-122">boolean</span></span> |<span data-ttu-id="79909-123">Determina se o valor de saudação é um segredo e deve ser criptografado ou não.</span><span class="sxs-lookup"><span data-stu-id="79909-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="79909-124">Marcas</span><span class="sxs-lookup"><span data-stu-id="79909-124">Tags</span></span> |<span data-ttu-id="79909-125">matriz de cadeias de caracteres</span><span class="sxs-lookup"><span data-stu-id="79909-125">array of string</span></span> |<span data-ttu-id="79909-126">Opcional marcas que, quando fornecido pode ser usado toofilter Olá propriedade lista.</span><span class="sxs-lookup"><span data-stu-id="79909-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="79909-127">Propriedades são configuradas no portal do publicador de saudação em Olá **propriedades** guia. Saudação de exemplo a seguir, três propriedades são configuradas.</span><span class="sxs-lookup"><span data-stu-id="79909-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Propriedades][api-management-properties]

<span data-ttu-id="79909-129">Os valores de propriedade podem conter cadeias de caracteres literais e [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="79909-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="79909-130">Olá tabela a seguir mostra Olá anterior exemplo três propriedades e seus atributos.</span><span class="sxs-lookup"><span data-stu-id="79909-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="79909-131">Olá valor `ExpressionProperty` é uma expressão de diretiva que retorna uma cadeia de caracteres que contém Olá data e hora atuais.</span><span class="sxs-lookup"><span data-stu-id="79909-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="79909-132">Olá propriedade `ContosoHeaderValue` está marcado como um segredo, portanto, seu valor não é exibido.</span><span class="sxs-lookup"><span data-stu-id="79909-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="79909-133">Nome</span><span class="sxs-lookup"><span data-stu-id="79909-133">Name</span></span> | <span data-ttu-id="79909-134">Valor</span><span class="sxs-lookup"><span data-stu-id="79909-134">Value</span></span> | <span data-ttu-id="79909-135">Segredo</span><span class="sxs-lookup"><span data-stu-id="79909-135">Secret</span></span> | <span data-ttu-id="79909-136">Marcas</span><span class="sxs-lookup"><span data-stu-id="79909-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="79909-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="79909-137">ContosoHeader</span></span> |<span data-ttu-id="79909-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="79909-138">TrackingId</span></span> |<span data-ttu-id="79909-139">Falso</span><span class="sxs-lookup"><span data-stu-id="79909-139">False</span></span> |<span data-ttu-id="79909-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="79909-140">Contoso</span></span> |
| <span data-ttu-id="79909-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="79909-141">ContosoHeaderValue</span></span> |<span data-ttu-id="79909-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="79909-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="79909-143">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="79909-143">True</span></span> |<span data-ttu-id="79909-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="79909-144">Contoso</span></span> |
| <span data-ttu-id="79909-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="79909-145">ExpressionProperty</span></span> |<span data-ttu-id="79909-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="79909-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="79909-147">Falso</span><span class="sxs-lookup"><span data-stu-id="79909-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="79909-148">toouse uma propriedade</span><span class="sxs-lookup"><span data-stu-id="79909-148">toouse a property</span></span>
<span data-ttu-id="79909-149">como o nome da propriedade Olá local dentro de um duplo par de chaves toouse uma propriedade em uma política, `{{ContosoHeader}}`, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="79909-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="79909-150">Neste exemplo, `ContosoHeader` é usado como nome de saudação de um cabeçalho em um `set-header` política, e `ContosoHeaderValue` é usado como valor de saudação desse cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="79909-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="79909-151">Quando essa política é avaliada durante uma solicitação ou resposta toohello API gateway de gerenciamento, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` são substituídas por seus valores de propriedade do respectivos.</span><span class="sxs-lookup"><span data-stu-id="79909-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="79909-152">Propriedades podem ser usadas como atributo concluído ou valores de elemento, conforme mostrado no exemplo anterior hello, mas eles também podem ser inseridos ou combinados com parte de uma expressão de texto literal, conforme mostrado no exemplo a seguir de saudação:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="79909-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="79909-153">As propriedades também podem conter expressões de política.</span><span class="sxs-lookup"><span data-stu-id="79909-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="79909-154">Em Olá exemplo a seguir, Olá `ExpressionProperty` é usado.</span><span class="sxs-lookup"><span data-stu-id="79909-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="79909-155">Quando essa política é avaliada, `{{ExpressionProperty}}` é substituído por seu valor: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="79909-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="79909-156">Como valor de saudação é uma expressão de diretiva, Olá expressão é avaliada e política Olá prossegue com a sua execução.</span><span class="sxs-lookup"><span data-stu-id="79909-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="79909-157">Você pode testar isso no portal do desenvolvedor Olá chamando uma operação que tenha uma política com as propriedades no escopo.</span><span class="sxs-lookup"><span data-stu-id="79909-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="79909-158">Em Olá exemplo a seguir, uma operação é chamada no exemplo anterior dois de saudação `set-header` políticas com propriedades.</span><span class="sxs-lookup"><span data-stu-id="79909-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="79909-159">Observe que a resposta de saudação contém dois cabeçalhos personalizados que foram configurados usando políticas com propriedades.</span><span class="sxs-lookup"><span data-stu-id="79909-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Portal do desenvolvedor][api-management-send-results]

<span data-ttu-id="79909-161">Se você observar Olá [rastreamento de API do Inspetor](api-management-howto-api-inspector.md) para uma chamada que inclui Olá duas anterior exemplo políticas com propriedades, você pode ver Olá dois `set-header` políticas com valores de propriedade Olá inseridos, bem como expressão de diretiva Olá avaliação de propriedade Olá que continha a expressão de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="79909-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Rastreamento do Inspetor de API][api-management-api-inspector-trace]

<span data-ttu-id="79909-163">Observe que, embora os valores de propriedade possam conter expressões de política, os valores de propriedade não podem conter outras propriedades.</span><span class="sxs-lookup"><span data-stu-id="79909-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="79909-164">Se o texto que contém uma referência de propriedade é usado para um valor de propriedade, como `Property value text {{MyProperty}}`, que referência da propriedade não será substituída e será incluída como parte do valor da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="79909-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="79909-165">toocreate uma propriedade</span><span class="sxs-lookup"><span data-stu-id="79909-165">toocreate a property</span></span>
<span data-ttu-id="79909-166">toocreate uma propriedade, clique em **adicionar propriedade** em Olá **propriedades** guia.</span><span class="sxs-lookup"><span data-stu-id="79909-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Adicionar propriedade][api-management-properties-add-property-menu]

<span data-ttu-id="79909-168">**Nome** e **Valor** são valores obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="79909-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="79909-169">Se o valor dessa propriedade é um segredo, verifique Olá **é um segredo** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="79909-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="79909-170">Insira um ou mais toohelp de marcas opcionais com organizar suas propriedades e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="79909-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Adicionar propriedade][api-management-properties-add-property]

<span data-ttu-id="79909-172">Quando uma nova propriedade é salvo, Olá **propriedades de pesquisa** caixa de texto é preenchida com o nome hello da nova propriedade de saudação e nova propriedade de saudação é exibida.</span><span class="sxs-lookup"><span data-stu-id="79909-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="79909-173">toodisplay todas as propriedades, desmarque Olá **propriedades de pesquisa** caixa de texto e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="79909-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Propriedades][api-management-properties-property-saved]

<span data-ttu-id="79909-175">Para obter informações sobre a criação de uma propriedade usando Olá API REST, consulte [criar uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="79909-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="79909-176">tooedit uma propriedade</span><span class="sxs-lookup"><span data-stu-id="79909-176">tooedit a property</span></span>
<span data-ttu-id="79909-177">tooedit uma propriedade, clique em **editar** ao lado de saudação tooedit de propriedade.</span><span class="sxs-lookup"><span data-stu-id="79909-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Editar propriedade][api-management-properties-edit]

<span data-ttu-id="79909-179">Faça as alterações desejadas e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="79909-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="79909-180">Se você alterar o nome da propriedade hello, todas as políticas que fazem referência a essa propriedade são novo nome de saudação toouse atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="79909-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Editar propriedade][api-management-properties-edit-property]

<span data-ttu-id="79909-182">Para obter informações sobre como editar uma propriedade usando Olá API REST, consulte [editar uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="79909-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="79909-183">toodelete uma propriedade</span><span class="sxs-lookup"><span data-stu-id="79909-183">toodelete a property</span></span>
<span data-ttu-id="79909-184">toodelete uma propriedade, clique em **excluir** ao lado de saudação toodelete de propriedade.</span><span class="sxs-lookup"><span data-stu-id="79909-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Excluir propriedade][api-management-properties-delete]

<span data-ttu-id="79909-186">Clique em **Sim, excluí-la** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="79909-186">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmar exclusão][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="79909-188">Se a propriedade de saudação é referenciada por nenhuma das políticas, não será possível toosuccessfully excluí-lo até que você remova a propriedade de saudação de todas as políticas que usá-lo.</span><span class="sxs-lookup"><span data-stu-id="79909-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="79909-189">Para obter informações sobre como excluir uma propriedade usando Olá API REST, consulte [excluir uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="79909-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="79909-190">propriedades toosearch e filtro</span><span class="sxs-lookup"><span data-stu-id="79909-190">toosearch and filter properties</span></span>
<span data-ttu-id="79909-191">Olá **propriedades** guia inclui pesquisando e filtrando toohelp recursos gerenciar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="79909-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="79909-192">lista de propriedades de saudação toofilter pelo nome da propriedade, digite um termo de pesquisa no hello **propriedades de pesquisa** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="79909-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="79909-193">toodisplay todas as propriedades, desmarque Olá **propriedades de pesquisa** caixa de texto e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="79909-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Pesquisar][api-management-properties-search]

<span data-ttu-id="79909-195">lista de propriedades de saudação toofilter pelos valores de marca, insira uma ou mais marcas em Olá **filtrar por marcas** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="79909-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="79909-196">toodisplay todas as propriedades, desmarque Olá **filtrar por marcas** caixa de texto e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="79909-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filter][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="79909-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79909-198">Next steps</span></span>
* <span data-ttu-id="79909-199">Saiba mais sobre como trabalhar com políticas</span><span class="sxs-lookup"><span data-stu-id="79909-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="79909-200">Políticas no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="79909-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="79909-201">Referência de política</span><span class="sxs-lookup"><span data-stu-id="79909-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="79909-202">Expressões de política</span><span class="sxs-lookup"><span data-stu-id="79909-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="79909-203">Assista a uma visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="79909-203">Watch a video overview</span></span>
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

