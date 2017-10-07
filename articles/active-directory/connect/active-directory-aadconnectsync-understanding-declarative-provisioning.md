---
title: "Azure AD Connect: Noções básicas sobre provisionamento declarativo | Microsoft Docs"
description: "Explica Olá declarativa configuração modelo de provisionamento no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Sincronização do Azure AD Connect: noções básicas sobre expressões de provisionamento declarativo
Este tópico explica o modelo de configuração de saudação no Azure AD Connect. modelo de saudação é chamado de provisionamento declarativo e permite que você toomake uma alteração de configuração com facilidade. Muitos itens descritos neste tópico são avançados e não são necessários para a maioria dos cenários do cliente.

## <a name="overview"></a>Visão geral
Provisionamento declarativo é proveniente um diretório de origem conectado de objetos de processamento e determina como os atributos e objeto Olá devem ser transformados de um origem tooa destino. Um objeto é processado em um pipeline de sincronização e pipeline de saudação é hello mesmo para regras de entrada e saídas. Uma regra de entrada é de um metaverso de toohello de espaço do conector e é uma regra de saída do espaço do conector Olá metaverso tooa.

![Pipeline de sincronização](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

pipeline de saudação tem vários módulos diferentes. Cada um é responsável por um conceito na sincronização de objeto.

![Pipeline de sincronização](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Fonte, o objeto de origem Olá
* [Escopo](#scope)localiza todas as regras de sincronização que estão no escopo
* [Ingressar](#join)determina a relação entre o metaverso e o espaço do conector
* [Transformar](#transform)calcula como os atributos devem ser transformados e fluir
* [Precedência](#precedence)resolve conflitos de contribuições de atributo
* Destino, o objeto de destino Olá

## <a name="scope"></a>Escopo
módulo de escopo de saudação está avaliando um objeto e determina as regras de saudação que estejam no escopo e devem ser incluídas no processamento de saudação. Dependendo de valores de atributos de saudação no objeto hello, regras de sincronização diferentes são toobe avaliada no escopo. Por exemplo, um usuário desabilitado sem uma caixa de correio do Exchange tem regras diferentes das de um usuário habilitado com uma caixa de correio.  
![Escopo](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

Olá escopo é definido como grupos e cláusulas. cláusulas Olá estão dentro de um grupo. Um E lógico é usado entre todas as cláusulas em um grupo. Por exemplo, (department =TI E country = Dinamarca). Um OU lógico é usado entre grupos.

![Escopo](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
escopo de saudação nesta imagem deve ser lidos como (departamento = IT e país = Dinamarca) ou (país = Suécia). Se o grupo 1 ou 2 for avaliado tootrue, regra hello está no escopo.

módulo de escopo Olá dá suporte a saudação operações a seguir.

| Operação | Descrição |
| --- | --- |
| EQUAL, NOTEQUAL |Uma comparação de cadeia de caracteres que é avaliada se valor for igual toohello no atributo hello. Para atributos com valores múltiplos, confira ISIN e ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Uma comparação de cadeia de caracteres que é avaliada se o valor é menor que do valor de saudação no atributo de saudação. |
| CONTAINS, NOTCONTAINS |Uma comparação de cadeia de caracteres que é avaliada se o valor pode ser encontrado em algum lugar dentro do valor no atributo hello. |
| STARTSWITH, NOTSTARTSWITH |Uma comparação de cadeia de caracteres que é avaliada se o valor está no início de saudação do valor de saudação no atributo de saudação. |
| ENDSWITH, NOTENDSWITH |Uma comparação de cadeia de caracteres que é avaliada se o valor está no final de saudação do valor de saudação no atributo hello. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Uma comparação de cadeia de caracteres que é avaliada se o valor for maior do valor de saudação no atributo de saudação. |
| ISNULL, ISNOTNULL |Avalia se o atributo hello está ausente do objeto de saudação. Se o atributo de saudação não está presente e, portanto, null, regra hello está no escopo. |
| ISIN, ISNOTIN |Avalia se o valor de saudação estiver presente no atributo Olá definido. Esta operação é Olá múltiplos igual e NOTEQUAL. atributo Olá deve toobe um atributo com vários valores e se o valor de saudação pode ser encontrado em qualquer um dos valores de atributo Olá, regra de saudação é no escopo. |
| ISBITSET, ISNOTBITSET |Avalia se um bit específico está definido. Por exemplo, pode ser usado tooevaluate bits Olá em userAccountControl toosee se um usuário está habilitado ou desabilitado. |
| ISMEMBEROF, ISNOTMEMBEROF |valor de saudação deve conter um grupo de tooa DN no espaço do conector hello. Se o objeto de saudação for um membro do grupo de saudação especificado, a regra hello está no escopo. |

## <a name="join"></a>Ingressar
módulo de junção Olá no pipeline de sincronização de saudação é responsável para localizar a relação Olá entre Olá na fonte de saudação um objeto e no destino hello. Em uma regra de entrada, essa relação seria um objeto em um espaço do conector localizar um objeto de relação tooan no metaverso hello.  
![Junção entre cs e mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
meta de saudação é toosee se houver um objeto no metaverso hello, criado por outro conector, ele deve ser associado. Por exemplo, em um recurso de conta de usuário de saudação floresta da floresta de conta Olá deve ser Unido com usuário Olá da floresta de recursos de saudação.

Junções são usadas principalmente em regras de entrada toojoin toohello do conjunto de objetos do espaço conector mesmo objeto do metaverso.

Olá junções são definidas como um ou mais grupos. Dentro de um grupo, há cláusulas. Um E lógico é usado entre todas as cláusulas em um grupo. Um OU lógico é usado entre grupos. Olá grupos são processados na ordem de toobottom superior. Quando um grupo encontrou uma correspondência exata com um objeto no destino hello, nenhuma outra regra de associação é avaliada. Se zero ou mais de um objeto for localizado, o processamento continuará toohello próximo grupo de regras. Por esse motivo, regras de saudação devem ser criadas na ordem de saudação do mais explícito primeiro e mais difusa final hello.  
![Definição de junção](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
Olá junções nesta imagem são processadas de toobottom superior. Pipeline de sincronização Olá primeiro vê se houver uma correspondência no employeeID. Caso contrário, a regra segundo Olá vê se nome da conta Olá pode ser usado toojoin Olá objetos juntos. Se isso não for uma correspondência ou, terceira e última regra Olá é uma correspondência difusa mais usando o nome de saudação do usuário.

Se todas as regras de junção tenham sido avaliadas e não há uma correspondência, Olá **tipo de Link** em Olá **descrição** página é usada. Se essa opção for definida muito**provisionar**, será criado um novo objeto de destino de saudação.  
![Provisionar ou ingressar](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Um objeto deve ter apenas uma única regra de sincronização com as regras de associação em escopo. Se houver várias regras de sincronização em que a associação esteja definida, ocorrerá um erro. Precedência não é usada tooresolve conflitos de associação. Um objeto deve ter uma regra de associação no escopo de atributos tooflow com hello mesma direção de entrada/saída. Se você precisar tooflow atributos toohello de entrada e saída mesmo objeto, você deve ter uma entrada e uma regra de sincronização de saída com a junção.

Associação de saída tem um comportamento especial quando ele tenta tooprovision um espaço do conector do objeto tooa destino. atributo Olá DN é usado toofirst tente uma junção inversa. Se já houver um objeto no espaço do conector de destino Olá com hello mesmo DN, Olá objetos associados.

módulo de junção Olá é avaliado apenas depois que quando uma nova regra de sincronização estiver no escopo. Quando ingressou em um objeto, ele não está saindo mesmo se os critérios de união Olá não for atendida. Se você quiser toodisjoin um objeto, regra de sincronização de saudação que ingressaram objetos Olá deve ir fora do escopo.

### <a name="metaverse-delete"></a>Exclusão de metaverso
Um objeto do metaverso permanece, contanto que haja uma regra de sincronização no escopo com **tipo de Link** definido muito**provisionar** ou **StickyJoin**. Um StickyJoin é usado quando um conector não é permitido tooprovision um novo objeto do metaverso toohello, mas quando ele foi adicionado, ele deve ser excluído na fonte de saudação antes de objeto do metaverso Olá é excluído.

Quando um objeto do metaverso é excluído, todos os objetos associados a uma regra de sincronização de saída marcada para **provisionar** são marcados para uma exclusão.

## <a name="transformations"></a>Transformações
transformações de saudação são toodefine usado como atributos devem fluir de saudação origem toohello destino. Olá fluxos podem ter um dos seguintes Olá **fluxo tipos**: direto, constante ou expressão. Um fluxo direto; flui um valor de atributo como está, sem transformações adicionais. Saudação de define um valor constante de valor especificado. Uma expressão usa Olá declarativa provisionamento expressão idioma tooexpress como transformação Olá deve ser. Olá detalhes para linguagem de expressão Olá pode ser encontrada no hello [Noções básicas sobre a linguagem de expressão de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) tópico.

![Provisionar ou ingressar](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Olá **aplicar uma vez** caixa de seleção define esse Olá atributo deve ser definido somente quando o objeto de saudação é criado inicialmente. Por exemplo, essa configuração pode ser usado tooset uma senha inicial para um novo objeto de usuário.

### <a name="merging-attribute-values"></a>Mesclando valores de atributo
Fluxos de atributo Olá há toodetermine uma configuração se múltiplos atributos devem ser mesclados em vários conectores diferentes. valor padrão de saudação é **atualização**, que indica essa regra de sincronização Olá com precedência mais alta deve vencer.

![Tipos de mesclagem](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Também há **Merge** e **MergeCaseInsensitive**. Essas opções permitem toomerge valores de origens diferentes. Por exemplo, ele pode ser o atributo de membro ou proxyAddresses de saudação de toomerge usado de várias florestas diferentes. Quando você usar essa opção, todos sincronizados regras no escopo para um objeto deve usar Olá mesmo tipo de mesclagem. Não é possível definir **Update** de um conector e **Merge** de outro. Se tentar, você receberá um erro.

Olá diferença entre **mesclar** e **MergeCaseInsensitive** é como tooprocess duplicar valores de atributo. mecanismo de sincronização de saudação verifica se os valores duplicados não são inseridos no atributo de destino de saudação. Com **MergeCaseInsensitive**, duplicar valores com apenas uma diferença no caso de não serão toobe presente. Por exemplo, você não verá ambos "SMTP:bob@contoso.com"e"smtp:bob@contoso.com" no atributo de destino de saudação. **Mesclar** é apenas observando valores exatos hello e vários valores em que há apenas uma diferença em maiusculas podem estar presentes.

Olá opção **substituir** é Olá igual **atualização**, mas ele não é usado.

### <a name="control-hello-attribute-flow-process"></a>Processo de fluxo de atributo de saudação do controle
Quando várias regras de sincronização de entrada serão configurado toocontribute toohello mesmo atributo de metaverso, precedência é vencedor de saudação toodetermine usado. regra de sincronização de saudação com precedência mais alta (valor numérico menor) será o valor de saudação toocontribute. Olá que mesmo acontece para regras de saída. regra de sincronização de saudação com precedência mais alta vence e contribuir valor de saudação toohello diretório conectado.

Em alguns casos, em vez de contribuir com um valor, regra de sincronização Olá deve determinar o comportamento do outras regras. Há alguns literais especiais usados para esse caso.

Para regras de sincronização de entrada, Olá literal **nulo** pode ser usado tooindicate fluxo Olá não tem toocontribute nenhum valor. Outra regra com menor precedência pode contribuir com um valor. Se nenhuma regra tiver contribuído com um valor, o atributo de metaverso Olá é removido. Para uma regra de saída, se **nulo** é o valor final Olá depois do processamento de todas as regras de sincronização, valor Olá será removido no diretório conectado Olá.

Olá literal **AuthoritativeNull** é muito semelhante**nulo** , mas com diferença de saudação que não há regras de precedência inferiores podem contribuir com um valor.

Um fluxo de atributos também pode usar **IgnoreThisFlow**. É semelhante tooNULL no sentido de saudação que indica que não há nada toocontribute. diferença de saudação é que ele não remove um valor já existente no destino hello. É como o fluxo de atributos Olá nunca tiver sido existe.

Aqui está um exemplo:

Em *Out tooAD - híbrida do Exchange do usuário* Olá fluxo a seguir pode ser encontrado:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Essa expressão deve ser lido como: se a caixa de correio de usuário hello está localizada no AD do Azure, em seguida, fluir o atributo de saudação do AD do Azure tooAD. Se não, não fluem nada back tooActive Directory. Nesse caso, ele seria manter valor existente Olá no AD.

### <a name="importedvalue"></a>ImportedValue
função Hello ImportedValue é diferente de todas as outras funções, como o nome do atributo Olá deve ser colocado entre aspas em vez de colchetes:  
`ImportedValue("proxyAddresses")`.

Normalmente durante a sincronização de um atributo usa valor esperado de hello, mesmo se não tiver sido exportado ainda ou um erro foi recebido durante a exportação ("topo da torre hello"). Uma sincronização de entrada presumirá que um atributo que ainda não atingiu um diretório conectado finalmente o atingirá. Em alguns casos, é importante tooonly sincronizar um valor que foi confirmado pelo diretório conectado de saudação ("holograma e torre de importação de delta").

Um exemplo dessa função pode ser encontrado na Olá out-of-box regra de sincronização *no AD – usuário Common do Exchange*. No Exchange híbrido, valor Olá adicionado pelo Exchange online só deverá ser sincronizado quando ele foi confirmado que o valor de saudação foi exportado com êxito:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Precedência
Quando várias regras de sincronização toocontribute Olá mesmo destino de toohello de valor de atributo, o valor de precedência de saudação é vencedor de saudação toodetermine usado. regra de saudação com precedência mais alta, o menor valor numérico, será toocontribute atributo de saudação em um conflito.

![Tipos de mesclagem](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Essa classificação pode ser usado toodefine mais preciso fluxos para um pequeno subconjunto de objetos de atributos. Por exemplo, a saudação fora-de--regras automáticas Certifique-se de que atributos de uma conta habilitada (**Useraccountenabled**) têm precedência de outras contas.

A precedência pode ser definida entre Conectores. Que permite que os conectores com valores de toocontribute melhor dados primeiro.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Olá de vários objetos do mesmo espaço do conector
Se você tiver vários objetos em Olá conector mesmo espaço toohello ingressado no metaverso do mesmo objeto, precedência deve ser ajustada. Se vários objetos estejam no escopo do hello mesma regra de sincronização, o mecanismo de sincronização Olá não é capaz de toodetermine precedência. Ele é ambíguo qual objeto de origem deve contribuir Olá valor toohello metaverso. Essa configuração será relatada como ambígua, mesmo se tem de atributos Olá na fonte Olá Olá mesmo valor.  
![Vários objetos ingressados toohello mesmo objeto mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

Para este cenário, você precisa toochange escopo Olá regras de sincronização Olá para que objetos de fonte de saudação tem regras de sincronização diferentes no escopo. Que permite que você toodefine precedência de diferentes.  
![Vários objetos ingressados toohello mesmo objeto mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre a linguagem de expressão Olá em [Noções básicas sobre expressões de provisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Veja declarativa como o provisionamento é usada fora da caixa na [Compreendendo a configuração padrão da saudação](active-directory-aadconnectsync-understanding-default-configuration.md).
* Veja como toomake um práticos alterados usando provisionamento declarativo em [como toomake toohello uma alteração de configuração padrão](active-directory-aadconnectsync-change-the-configuration.md).
* Continuar tooread como usuários e contatos funcionam juntos no [Noções básicas sobre usuários e contatos](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

**Tópicos de referência**

* [Azure AD Connect Sync: referência de funções](active-directory-aadconnectsync-functions-reference.md)
