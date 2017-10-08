---
title: fontes de dados de tooannotate aaaHow | Microsoft Docs
description: "Realce como tooarticle como tooannotate ativos de dados no catálogo de dados do Azure, incluindo nomes amigáveis, marcas, descrições e especialistas."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Como tooannotate fontes de dados
## <a name="introduction"></a>Introdução
**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa. Em outras palavras, o catálogo de dados está ajudando as pessoas a descobrir, entender e usar fontes de dados e ajudar as organizações tooget mais valor de seus dados existentes. Quando uma fonte de dados é registrada no catálogo de dados, seus metadados são copiados e indexados pelo serviço de saudação, mas o texto de saudação não termina existe. Catálogo de dados permite que os usuários tooprovide seus próprios metadados de saudação descritivo metadados – como marcas e descrições – toosupplement extraídos da fonte de dados de saudação e mais pessoas toomore compreensível da fonte de dados de saudação do toomake.

## <a name="annotation-and-crowdsourcing"></a>Anotação e crowdsourcing
Todo mundo tem uma opinião. E isso é bom.
O Catálogo de Dados reconhece que diferentes usuários têm diferentes perspectivas em fontes de dados empresariais e cada uma dessas perspectivas pode ser valiosa. Considere Olá cenário a seguir:

* administrador do sistema Olá sabe o contrato de nível de serviço Olá para Olá servidores ou serviços essa fonte de dados de saudação do host.
* administrador de banco de dados de saudação sabe backup Olá agendar para cada banco de dados, e Olá janelas de processamento de ETL permitidos.
* proprietário do sistema Olá sabe processo Olá usuários toorequest acesso toohello fonte de dados.
* administrador de dados Olá sabe como ativos de saudação e atributos na fonte de dados Olá mapeiam toohello modelo de dados de empresa.
* Analista de saudação sabe como dados de saudação são usados no contexto de Olá Olá dos processos de negócios que oferece suporte a ele.

Cada um desses perspectivas é valiosa e catálogo de dados usa um toometadata abordagem crowdsourcing que permite que cada um toobe capturada e usada tooprovide uma visão completa de fontes de dados registrados. Usando o portal do catálogo de dados de hello, cada usuário pode adicionar e editar suas próprias anotações, enquanto estiver sendo tooview capaz de anotações fornecidas por outros usuários.

## <a name="different-types-of-annotations"></a>Diferentes tipos de anotações
Oferece suporte de catálogo de dados Olá seguintes tipos de anotações:

| Anotação | Observações |
| --- | --- |
| Nome amigável |Nomes amigáveis podem ser fornecidos no nível de ativos de dados hello, ativos de dados toomake hello mais facilmente entendido. Nomes amigáveis são mais úteis quando o nome do objeto subjacente Olá é toousers criptografadas, abreviado ou caso contrário, não é significativa. |
| Descrição |As descrições podem ser fornecidas no atributo e o ativo de dados de saudação / níveis de coluna. As descrições são anotações de texto curto de forma livre que descrevem a perspectiva do usuário Olá no ativo de dados hello ou seu uso. |
| Marcas (marcas de usuário) |Marcas podem ser fornecidas no atributo e ativos de dados Olá / níveis de coluna. Marcas de usuário são rótulos definidos pelo usuário que podem ser usado toocategorize ativos de dados ou atributos. |
| Marcas (marcas de glossário) |Marcas podem ser fornecidas no atributo e ativos de dados Olá / níveis de coluna. Marcas de glossário são termos do glossário definidas centralmente que podem ser usado toocategorize ativos de dados ou atributos usando uma taxonomia comum de negócios. Para obter mais informações, consulte [como tooset backup Olá Glossário de negócios para marcação controlado](data-catalog-how-to-business-glossary.md) |
| Especialistas |Os especialistas podem ser fornecidos no nível da saudação dados ativos. Os especialistas identificam usuários ou grupos com perspectivas especialistas em dados hello e podem servir como pontos de contato para usuários que descobrir Olá registrado fontes de dados e tem dúvidas que não foram respondidas por anotações existentes hello. |
| Solicitar acesso |Informações de acesso de solicitação podem ser fornecidas no nível da saudação dados ativos. Essas informações são para os usuários que descobrir uma fonte de dados que eles ainda não têm permissões tooaccess. Os usuários podem inserir o endereço de email de saudação do hello usuário ou grupo que concede acesso, Olá URL do processo Olá, ferramenta que os usuários o acesso necessário toogain ou pode inserir o próprio processo de saudação como texto. |
| Documentação |Documentação pode ser fornecida no nível da saudação dados ativos. A documentação de ativos é informação em rich text que pode incluir links e imagens e fornecer todas as informações que não são transmitidas por meio de marcações e descrições. |

## <a name="annotating-multiple-assets"></a>Anotando vários ativos
Ao selecionar vários ativos de dados no portal do catálogo de dados hello, os usuários podem anotar todos os ativos selecionados em uma única operação. Anotações aplicará ativos tooall selecionado, tornando fácil tooselect e fornecer uma descrição consistente e conjuntos de marcas e especialistas para ativos de dados relacionados.

> [!NOTE]
> As marcas e os especialistas também podem ser fornecidos quando registrar ativos de dados usando dados de catálogo de dados de saudação ferramenta de registro de origem.
>
>

Ao selecionar várias tabelas e exibições, somente colunas todas selecionadas ativos têm em comum de dados será exibido no portal do catálogo de dados de saudação. Isso permite que as marcas de tooprovide de usuários e descrições de todas as colunas com o mesmo nome de saudação para todos os ativos selecionados.

## <a name="annotations-and-discovery"></a>Anotações e descoberta
Assim como Olá extraídos da fonte de dados Olá durante o registro de metadados é adicionado toohello índice de pesquisa de catálogo de dados, metadados fornecidos pelo usuário também é indexado. Isso significa que não apenas fazem anotações facilitam para os dados usuários toounderstand Olá que eles descobrir, anotações facilitam para os usuários toodiscover Olá anotado dados ativos ao pesquisar usando termos Olá que fazem sentido toothem.

## <a name="summary"></a>Resumo
Registrar uma fonte de dados com o catálogo de dados torna dados detectáveis copiando metadados estruturais e descritivo da fonte de dados Olá para Olá serviço de catálogo. Quando uma fonte de dados tiver sido registrada, os usuários podem fornecer anotações toomake mais fácil toodiscover e entender de dentro do portal de catálogo de dados hello.

## <a name="see-also"></a>Consulte também
* [Introdução ao Data Catalog do Azure](data-catalog-get-started.md) tutorial para obter detalhes passo a passo sobre como tooannotate fontes de dados.
