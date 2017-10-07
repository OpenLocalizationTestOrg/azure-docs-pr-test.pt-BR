---
title: "fontes de dados de toodiscover aaaHow no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo realça como toodiscover ativos de dados registrados no catálogo de dados do Azure, incluindo pesquisando e filtrando e usar Olá ocorrências destacar recursos do portal do catálogo de dados do Azure hello."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Como fontes de dados de toodiscover no catálogo de dados do Azure
## <a name="introduction"></a>Introdução
O Catálogo de Dados do Azure é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e descoberta para fontes de dados da empresa. Em outras palavras, o Catálogo de Dados ajuda as pessoas a descobrir, entender e usar fontes de dados, além de ajudar as organizações a obterem mais valor dos seus dados existentes. Depois que uma fonte de dados for registrada com o catálogo de dados, seus metadados é indexado por serviço hello, para que você pode pesquisar facilmente dados de saudação toodiscover que é necessário.

## <a name="searching-and-filtering"></a>Pesquisando e filtrando
A descoberta no Catálogo de Dados usa dois mecanismos principais: pesquisa e filtragem.

A pesquisa é projetado toobe intuitiva e eficiente. Por padrão, os termos de pesquisa são comparados com qualquer propriedade no catálogo hello, incluindo anotações fornecido pelo usuário.

A filtragem é projetada toocomplement pesquisa. Você pode selecionar características específicas, como especialistas, tipo de fonte de dados, tipo de objeto e marcas. Você pode exibir somente ativos de dados correspondente e restringir a pesquisa resultados toomatching ativos.

Usando uma combinação de pesquisa e filtragem, você pode navegar rapidamente as fontes de dados de saudação que foram registradas com fontes de dados do catálogo de dados toodiscover Olá que é necessário.

## <a name="search-syntax"></a>Sintaxe de pesquisa
Embora a pesquisa de texto livre saudação padrão é simples e intuitiva, você também pode usar a sintaxe de pesquisa do catálogo de dados para maior controle sobre os resultados da pesquisa hello. Dados catálogo pesquisa oferece suporte a saudação técnicas a seguir:

| Técnica | Uso | Exemplo |
| --- | --- | --- |
| Pesquisa básica |Pesquisa básica que usa um ou mais termos de pesquisa. Os resultados são qualquer recurso que corresponde a nenhuma propriedade com um ou mais termos Olá especificados. |`sales data` |
| Escopo de propriedade |Retorno apenas fontes de dados onde o termo de pesquisa de saudação é correspondido com hello especificado de propriedade. |`name:finance` |
| Operadores boolianos |Ampliar ou restringir uma pesquisa usando operações boolianas. |`finance NOT corporate` |
| Agrupamento com parênteses |Use parênteses toogroup partes de saudação consulta tooachieve isolamento lógico, especialmente em conjunto com operadores boolianos. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Operadores de comparação |Use comparações que não sejam de igualdade para propriedades que tenham tipos de dados numéricos e de data. |`modifiedTime > "11/05/2014"` |

Para obter mais informações sobre a pesquisa de catálogo de dados, consulte Olá [Data Catalog do Azure](https://msdn.microsoft.com/library/azure/mt267594.aspx) artigo.

## <a name="hit-highlighting"></a>Realce de ocorrência
Quando você exibir os resultados da pesquisa, qualquer exibido propriedades que correspondem a saudação especificada termos de pesquisa (como o nome do ativo de dados hello, descrição e marcas) são realçado toomake-tooidentify mais fácil por que um ativo de dados foi retornado por uma pesquisa determinada.

> [!NOTE]
> tooturn desativar acerto de realce, use Olá **realçar** alternar no portal do catálogo de dados de saudação.
>
>

Ao exibir os resultados da pesquisa, talvez não seja sempre óbvio o motivo pelo qual um ativo de dados é incluído, mesmo com o destaque de ocorrências habilitado. Como todas as propriedades são pesquisadas por padrão, um ativo de dados pode ser retornado devido a uma correspondência em uma propriedade no nível de coluna. E porque vários usuários podem anotar os ativos de dados registrado com suas próprias marcas e descrições, nem todos os metadados podem ser exibidos na lista de saudação dos resultados da pesquisa.

Exibição de bloco padrão hello, cada lado a lado exibida nos resultados da pesquisa de saudação inclui um **exibição termo de pesquisa corresponder** ícone, para que você pode exibir rapidamente o número de saudação de correspondências e seu local e toojump toothem se você quiser.

 ![O realce de ocorrências e correspondências da pesquisa no portal do catálogo de dados do Azure Olá](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Resumo
Como registrar uma fonte de dados com o catálogo de dados cópias estruturais e descritivas toohello serviço de catálogo da fonte de metadados dos dados hello, hello fonte de dados se torna mais fácil toodiscover e entender. Após ter registrado uma fonte de dados, você pode descobri-lo usando a filtragem e pesquisa a partir do portal do catálogo de dados de saudação.

## <a name="next-steps"></a>Próximas etapas
* Para obter detalhes passo a passo sobre como toodiscover fontes de dados, consulte [Introdução ao Data Catalog do Azure](data-catalog-get-started.md).
