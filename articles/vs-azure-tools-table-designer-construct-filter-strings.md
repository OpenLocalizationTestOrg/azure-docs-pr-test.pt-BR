---
title: "aaaConstructing cadeias de caracteres de filtro para o designer de tabela Olá | Microsoft Docs"
description: "Construindo cadeias de caracteres de filtro para o designer de tabela Olá"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Construindo cadeias de caracteres de filtro para Olá Designer de tabela
## <a name="overview"></a>Visão geral
Olá de toofilter dados em uma tabela do Azure que é exibido no Visual Studio **Designer de tabela**, construir uma cadeia de caracteres de filtro e insira-o no campo de filtro de saudação. sintaxe de cadeia de caracteres de filtro de saudação é definido por Olá WCF Data Services e é semelhante tooa cláusula SQL WHERE, mas é enviada toohello serviço tabela por meio de uma solicitação HTTP. Olá **Designer de tabela** identificadores Olá codificação adequada para você, caso toofilter em um valor de propriedade desejada, você só precisa inserir Olá nome de propriedade, o operador de comparação, valor de critérios, e, opcionalmente, o operador booleano no hello filtrar campo. Opção de consulta Olá $filter tooinclude não é necessário como você faria se foram construindo uma tabela de saudação do URL tooquery via Olá [referência de API de REST de serviços de armazenamento](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Olá WCF Data Services se baseiam no hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Para obter detalhes sobre a opção de consulta do sistema de filtro de saudação (**$filter**), consulte Olá [especificação de convenções de URI do OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Operadores de comparação
Olá seguintes operadores lógicos têm suporte para todos os tipos de propriedade:

| Operador lógico | Descrição | Cadeia de caracteres de filtro de exemplo |
| --- | --- | --- |
| eq |Igual a |City eq 'Redmond' |
| gt |Maior que |Preço gt 20 |
| ge |Maior que ou igual muito|Preço ge 10 |
| lt |Menor que |Preço lt 20 |
| le |Menor ou igual a |Preço le 100 |
| ne |Diferente de |City ne 'London' |
| e |e |Preço le 200 e Preço gt 3,5 |
| ou o |ou o |Preço le 3,5 ou Preço gt 200 |
| não |não |não isAvailable |

Ao construir uma cadeia de caracteres de filtro, hello regras a seguir são importantes:

* Use operadores lógicos de saudação toocompare um valor da propriedade tooa. Observe que não é possível toocompare um valor dinâmico tooa da propriedade; um lado da expressão Olá deve ser uma constante.
* Todas as partes da cadeia de caracteres de filtro Olá diferenciam maiusculas de minúsculas.
* valor constante Olá deve ser de saudação mesmo tipo que propriedade Olá para que os resultados Olá filtro tooreturn válidos. Para obter mais informações sobre os tipos de propriedade com suporte, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filtrando nas propriedades de cadeia de caracteres
Quando você filtrar em Propriedades de cadeia de caracteres, coloque constante de cadeia de caracteres de saudação entre aspas.

Olá filtros de exemplo a seguir no hello **PartitionKey** e **RowKey** propriedades; adicional não-chave propriedades também podem ser adicionadas toohello cadeia de caracteres de filtro:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Você pode colocar cada expressão de filtro entre parênteses, embora não seja necessário:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Observe que Olá serviço tabela não oferece suporte a consultas com caractere curinga, e eles não têm suporte no Designer de tabela de saudação ou. No entanto, você pode executar usando operadores de comparação no prefixo desejado Olá de correspondência de prefixo. Olá, exemplo a seguir retorna entidades com um sobrenome propriedade que começa com a letra de saudação 'A':

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filtrando em propriedades numéricas
toofilter em um inteiro ou um número de ponto flutuante, especifique o número de saudação sem aspas.

Este exemplo retorna todas as entidades com uma propriedade Idade cujo valor é maior que 30:

    Age gt 30

Este exemplo retorna todas as entidades com uma propriedade AmountDue cujo valor é menor que ou igual a too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filtrando em Propriedades Boolianas
toofilter em um valor booliano, especifique **true** ou **false** sem aspas.

Olá exemplo a seguir retorna todas as entidades onde Olá IsActive propriedade foi definido muito**true**:

    IsActive eq true

Você também pode escrever esta expressão de filtro sem um operador lógico hello. Em Olá exemplo a seguir, Olá serviço tabela também retornará todas as entidades onde IsActive é **true**:

    IsActive

tooreturn todas as entidades, onde é false, você pode usar o IsActive Olá não operador:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filtrando em Propriedades DateTime
toofilter em um valor DateTime, especifique Olá **datetime** palavra-chave, seguido pela constante de data/hora de saudação entre aspas. constante de data/hora Olá deve estar no formato UTC combinado, conforme descrito em [formatação de valores de propriedade DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).

saudação de exemplo a seguir retorna entidades em que a propriedade de CustomerSince Olá tooJuly igual a 10, 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
