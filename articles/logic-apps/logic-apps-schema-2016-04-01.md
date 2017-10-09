---
title: "aaaSchema atualizações 1 2016 junho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar definições de JSON para Aplicativos Lógicos do Azure com a versão de esquema 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Atualizações de esquema para Aplicativos Lógicos do Azure - 1º de junho de 2016

Esse novo esquema e a API de versão para os aplicativos lógicos do Azure inclui aprimoramentos importantes que tornam os aplicativos lógicos mais toouse mais fácil e confiável:

* [Escopos](#scopes) permitem agrupar ou aninhar ações como uma coleção de ações.
* [Condições e loops](#conditions-loops) agora são ações de primeira classe.
* Ordenação mais precisa para executar ações com hello `runAfter` propriedade, substituindo`dependsOn`

tooupgrade seus aplicativos de lógica de Olá 1 de agosto de 2015 preview esquema toohello esquema de 1º de junho de 2016, [Confira a seção Atualizar Olá](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Escopos

Esse esquema inclui escopos, que permitem agrupar ações ou aninhar ações umas dentro das outras. Por exemplo, uma condição pode conter outra condição. Saiba mais sobre a [sintaxe de escopo](../logic-apps/logic-apps-loops-and-scopes.md) ou examine este exemplo básico de escopo:

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a>Alterações de condições e loops

Em versões de esquema anteriores, condições e loops eram parâmetros associados a uma única ação. Esse esquema remove essa limitação; portanto, condições e loops agora aparecem como tipos de ação. Saiba mais sobre [loops e escopos](../logic-apps/logic-apps-loops-and-scopes.md) ou examine este exemplo básico de uma ação de condição:

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a>Propriedade 'runAfter'

Olá `runAfter` propriedade substitui `dependsOn`, fornecendo mais precisão quando você especifica a ordem Olá executar ações com base no status de saudação das ações anteriores.

Olá `dependsOn` propriedade era sinônimo de "ação Olá foi executado e foi bem-sucedida", não importa quantas vezes desejar tooexecute uma ação com base em se a ação anterior Olá teve êxito, falha ou ignoradas. Olá `runAfter` propriedade proporciona essa flexibilidade como um objeto que especifica todos os Olá nomes de ação após o qual hello objeto é executado. Essa propriedade também define uma matriz de status aceitável como disparadores. Por exemplo, se você quisesse toorun depois de passo A passo é bem-sucedida e também depois B êxito ou falha, você construir isso `runAfter` propriedade:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Atualizar o esquema

Atualizando toohello novo esquema tem apenas algumas etapas. Olá processo de atualização inclui a execução de script de atualização hello, salvar como um novo aplicativo de lógica e, se desejar, possivelmente substitui o aplicativo lógico anterior de saudação.

1. No portal do Azure de Olá, abra o aplicativo de lógica.

2. Vá muito**visão geral**. Na barra de ferramentas do hello lógica aplicativo, escolha **atualizar esquema**.
   
    ![Escolher o Esquema de Atualização][1]
   
    Olá definição atualizada for retornada, que você pode copiar e colar em uma definição de recurso, se necessário. 
    No entanto, podemos **altamente recomendável** você escolher **Salvar como** toomake-se de que todas as referências de conexão são válidas em Olá atualizado o aplicativo lógico.

3. Na barra de ferramentas de atualização de folha hello, escolha **Salvar como**.

4. Insira o nome de lógica de saudação e status. toodeploy seu aplicativo atualizado lógica, escolha **criar**.

5. Confirme se o aplicativo lógico atualizado funciona conforme o esperado.
   
   > [!NOTE]
   > Se você estiver usando um gatilho manual ou de solicitação, URL de retorno de chamada hello alterações em seu novo aplicativo de lógica. Teste Olá nova URL toomake se Olá-ponta a experiência funciona. URLs do toopreserve anterior, você pode clonar sobre a lógica do aplicativo existente.

6. *Opcional* toooverwrite seu aplicativo lógico anterior com a nova versão de esquema hello, na barra de ferramentas hello, escolha **Clone**, Avançar muito**atualizar esquema**. Essa etapa é necessária somente se você quiser tookeep Olá mesmo recurso ID ou a solicitação de URL do gatilho de seu aplicativo lógico.

### <a name="upgrade-tool-notes"></a>Observações sobre a ferramenta de atualização

#### <a name="mapping-conditions"></a>Condições de mapeamento

Na definição de saudação atualizada, ferramenta de saudação se esforça em Agrupar ações de ramificação true e false como um escopo. Especificamente, Olá designer padrão de `@equals(actions('a').status, 'Skipped')` devem aparecer como um `else` ação. No entanto, se a ferramenta Olá detectar padrões irreconhecíveis, ferramenta Olá pode criar condições separadas para true hello e a ramificação falsa hello. É possível remapear ações após a atualização, se necessário.

#### <a name="foreach-loop-with-condition"></a>loop 'foreach' com condição

No novo esquema de saudação, você pode usar o padrão de Olá Olá filtro ação tooreplicate de um `foreach` loop com uma condição por item, mas essa alteração automaticamente deve acontecer quando você atualiza. condição de saudação torna-se uma ação de filtro antes de loop de foreach Olá para retornar apenas uma matriz de itens que correspondem à condição de saudação e essa matriz é passada para a ação de foreach hello. Para obter um exemplo, confira [Loops e escopos](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Marcações de recursos

Depois de atualizar, marcas de recurso são removidas, portanto você deverá redefini-los para fluxo de trabalho Olá atualizado.

## <a name="other-changes"></a>Outras alterações

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Renomear o gatilho 'manual' too'request' gatilho

Olá `manual` tipo de disparador foi preterido e renomeado muito`request` com tipo `http`. Essa alteração cria mais consistência para o tipo de saudação do padrão que Olá gatilho é toobuild usado.

### <a name="new-filter-action"></a>Nova ação 'filter'

toofilter uma matriz grande conjunto de itens, Olá novo menor tooa `filter` tipo aceita uma matriz e uma condição, avalia a condição Olá para cada item e retorna uma matriz com itens que atendem a condição de saudação.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restrições às ações 'foreach' e 'until'

Olá `foreach` e `until` loop são restritos tooa única ação.

### <a name="new-trackedproperties-for-actions"></a>Novo 'trackedProperties' para ações

Ações agora podem ter uma propriedade adicional chamada `trackedProperties`, que é irmão toohello `runAfter` e `type` propriedades. Esse objeto especifica certas entradas de ação ou saídas que você deseja tooinclude na telemetria de diagnóstico do Azure hello, emitida como parte de um fluxo de trabalho. Por exemplo:

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a>Próximas etapas
* [Criar definições de fluxo de trabalho para aplicativos lógicos](../logic-apps/logic-apps-author-definitions.md)
* [Criar modelos de implantação para aplicativos lógicos](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
