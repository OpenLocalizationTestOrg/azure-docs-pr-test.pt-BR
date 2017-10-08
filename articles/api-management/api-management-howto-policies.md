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
# <a name="policies-in-azure-api-management"></a>Políticas do Gerenciamento de API do Azure
No gerenciamento de API do Azure, as políticas são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração. As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API. As instruções populares incluem conversão de formato de XML tooJSON e limitando toorestrict Olá quantidade de chamadas de entrada de um desenvolvedor de taxa de chamada. Muitas outras políticas estão disponíveis sem a necessidade de saudação.

Consulte Olá [referência de política] [ Policy Reference] para obter uma lista completa de declarações de política e suas configurações.

As políticas são aplicadas dentro de gateway Olá que fica entre consumidores de API hello e API Olá gerenciado. Olá gateway recebe todas as solicitações e geralmente encaminha inalteradas toohello subjacente API. No entanto uma política pode ser aplicada a solicitação de entrada alterações tooboth hello e resposta de saída.

Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário. Algumas políticas, como Olá [fluxo de controle] [ Control flow] e [Set variable] [ Set variable] políticas se baseiam em expressões de política. Para obter mais informações, confira [Políticas avançadas][Advanced policies] e [Expressões de política][Policy expressions].

## <a name="scopes"></a>Como tooconfigure políticas
Políticas podem ser configuradas globalmente ou no escopo de saudação de um [produto][Product], [API] [ API] ou [operação] [Operation]. tooconfigure uma política, navegue toohello editor de políticas no portal do publicador hello.

![Menu de políticas][policies-menu]

editor de políticas de saudação consiste em três seções principais: Olá política (superior), Olá política definição de escopo em que as diretivas são editadas (esquerdo) e listam de instruções de saudação (à direita):

![Editor de políticas][policies-editor]

toobegin configurar uma política, que você deve primeiro selecionar escopo Olá no qual Olá política deve ser aplicada. Na captura de tela abaixo Olá Olá **Starter** produto é selecionado. Observe que Olá símbolo quadrado próximo toohello política nome indica que uma política já foi aplicada nesse nível.

![Escopo][policies-scope]

Como uma política já tiver sido aplicada, configuração de saudação é mostrada na exibição de definição de saudação.

![Configurar][policies-configure]

política de saudação é exibida somente leitura no primeiro. Na ordem tooedit definição Olá clique Olá **configurar política** ação.

![Editar][policies-edit]

definição de política de saudação é um documento XML simples que descreve uma sequência de instruções de entrada e saídas. Olá XML pode ser editado diretamente na janela de definição de saudação. Uma lista de instruções é fornecida toohello à direita e o escopo atual do instruções toohello aplicável estão habilitados e realçados; como demonstrado pelo Olá **limite de taxa de chamada** instrução na captura de tela de saudação acima.

Clicar em uma instrução habilitada adicionará Olá XML apropriado no local de saudação do cursor Olá no modo de exibição de definição de saudação. 

> [!NOTE]
> Se a política de saudação que você deseja tooadd não estiver habilitada, certifique-se de que você está no escopo correto de saudação dessa política. Cada declaração de política é projetada para uso em determinados escopos e seções de política. seções de política tooreview hello e escopos de uma política, verifique Olá **uso** seção dessa política no hello [referência de política][Policy Reference].
> 
> 

Uma lista completa das declarações de política e suas configurações estão disponíveis em Olá [referência de política][Policy Reference].

Por exemplo, tooadd um novo toorestrict de instrução entrada solicita toospecified endereços IP, colocar o cursor Olá apenas dentro do conteúdo de saudação do hello `inbound` Olá de elemento e clique em XML **restringir IPs de chamador** instrução.

![Políticas de restrição][policies-restrict]

Isso adicionará uma toohello de trecho de código XML `inbound` elemento que fornece orientação sobre como tooconfigure Olá instrução.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit as solicitações de entrada e aceitar somente aqueles de um endereço IP de 1.2.3.4 modificar Olá XML da seguinte maneira:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Salvar][policies-save]

Ao concluir configuração instruções Olá para política de saudação, clique em **salvar** e alterações de saudação serão propagadas toohello gateway de gerenciamento de API imediatamente.

## <a name="sections"> </a>Compreendendo configuração de políticas
Uma política é uma série de instruções que são executadas para uma solicitação e uma resposta. configuração de saudação é dividida adequadamente `inbound`, `backend`, `outbound`, e `on-error` seções, conforme mostrado na seguinte configuração de saudação.

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

Se houver um erro durante o processamento de saudação de uma solicitação, quaisquer etapas restantes no hello `inbound`, `backend`, ou `outbound` seções são ignoradas e a execução vai toohello instruções Olá `on-error` seção. Colocando em declarações de política em Olá `on-error` seção você pode examinar o erro hello usando Olá `context.LastError` propriedade inspecionar e personalizar resposta de erro hello usando Olá `set-body` política e configurar o que acontece se ocorrer um erro. Há etapas internas e erros que podem ocorrer durante o processamento de saudação de declarações de política de códigos de erro. Para obter mais informações, consulte [Tratamento de erros em políticas de gerenciamento de API](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Como as políticas podem ser especificadas em diferentes níveis (global, produto, api e operação) configuração Olá fornece uma maneira para você ordem de saudação toospecify no qual instruções de definição de política Olá executado com a política do aspecto toohello pai. 

Escopos de política são avaliados na ordem de saudação.

1. Escopo global
2. Escopo do produto
3. Escopo de API
4. Escopo de operação

Olá instruções dentro deles são avaliadas de acordo com o posicionamento de toohello de saudação `base` elemento, se ele estiver presente. Política global tem nenhuma política pai e usando Olá `<base>` elemento em que ele não tem nenhum efeito.

Por exemplo, se você tiver uma política no nível global hello e uma política configurada para uma API, em seguida, sempre que essa API em particular é usado ambas as políticas serão ser aplicadas. Gerenciamento de API permite determinística ordenação de instruções de política combinados por meio do elemento base hello. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Na definição de política exemplo hello acima, Olá `cross-domain` instrução será executado antes de todas as políticas mais alto que por sua vez, ser seguido por Olá `find-and-replace` política. 

políticas de saudação toosee no escopo de saudação atual no editor de diretiva de saudação, clique **recalcular a política efetiva para o escopo selecionado**.

## <a name="next-steps"></a>Próximas etapas
Confira o vídeo a seguir sobre expressões de política.

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
