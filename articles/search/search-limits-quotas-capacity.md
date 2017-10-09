---
title: limites de aaaService na pesquisa do Azure | Microsoft Docs
description: "Limites do serviço usados para o planejamento de capacidade e limites máximos de solicitações e respostas para o Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Limites de serviço na Pesquisa do Azure
Os limites máximos de armazenamento, cargas de trabalho, quantidades de índices, documentos e outros objetos dependem do tipo de preço ao qual o [Azure Search é provisionado](search-create-service-portal.md), que pode ser **Gratuito**, **Básico** ou **Standard**.

* **Gratuito** é um serviço compartilhado multilocatário fornecido com sua assinatura do Azure. É uma opção de não--custo adicional para assinantes existentes que permite que você tooexperiment com o serviço de saudação antes de se inscrever para recursos dedicados.
* **Básico** fornece recursos de computação dedicados para cargas de trabalho de produção em uma escala menor.
* **Standard** é executado em computadores dedicados, com mais capacidade de armazenamento e processamento em cada nível. Standard vem em quatro níveis: S1, S2, S3 e S3 Alta Densidade (S3 HD).

> [!NOTE]
> Um serviço é provisionado em uma camada específica. Se você precisar toojump camadas tooget mais capacidade, você deve fornecer um novo serviço (não há nenhuma atualização in-loco). Para obter mais informações, confira [Escolher uma camada ou SKU](search-sku-tier.md). toolearn mais sobre o ajuste de capacidade em um serviço já tiver provisionado, consulte [níveis de recursos para cargas de trabalho de indexação e consulta de escala](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Por limites de assinatura
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Por limites do serviço
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Por limites de índice
Há uma correspondência entre os limites em índices e aqueles em indexadores. Dado um limite de 200 índices, o limite máximo de indexadores do hello também é 200 para Olá mesmo serviço.

| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Índice: campos máximos por índice |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Índice: máximo de perfis de pontuação por índice |100 |100 |100 |100 |100 |100 |
| Índice: funções máximas por perfil |8 |8 |8 |8 |8 |8 |
| Indexadores: carga de indexação máxima por invocação |10.000 documentos |Limitado apenas pelo máximo de documentos |Limitado apenas pelo máximo de documentos |Limitado apenas pelo máximo de documentos |Limitado apenas pelo máximo de documentos |N/D <sup>2</sup> |
| Indexadores: tempo de execução máximo | 1 a 3 minutos <sup>3</sup> |24 horas |24 horas |24 horas |24 horas |N/D <sup>2</sup> |
| Indexador de blob: tamanho máximo do blob, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indexador de blob: número máximo de caracteres de conteúdo extraído de um blob |32.000 |64.000 |4 milhões |4 milhões |4 milhões |N/D <sup>2</sup> |

<sup>1</sup> camada básica é Olá somente SKU com um limite inferior de 100 campos por índice.

<sup>2</sup> O S3 HD atualmente não dá suporte a indexadores. Contate o suporte do Azure se você tiver uma necessidade urgente para essa funcionalidade.

<sup>3</sup> indexador tempo máximo de execução para a camada gratuita Olá é 3 minutos para fontes de blob e 1 minuto para todas as outras fontes de dados.

## <a name="document-size-limits"></a>Limites de tamanho do documento
| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Tamanho do documento individual por API do Índice |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

Refere-se a tamanho do documento máximo toohello ao chamar uma API de índice. Tamanho do documento é realmente um limite de tamanho de saudação do hello corpo de solicitação de API de índice. Desde que você pode passar um lote de vários documentos toohello API de índice ao mesmo tempo, limite de tamanho de saudação realmente depende de quantos documentos são em lote hello. Para um lote com um único documento, o tamanho de documento máximo de saudação é 16 MB de JSON.

tookeep tamanho do documento, lembre-se de dados não podem ser consultados tooexclude da solicitação de saudação. Imagens e outros dados binários não são diretamente passível de consulta e não devem ser armazenados no índice de saudação. dados não podem ser consultados toointegrate resultados da pesquisa, defina um campo não pesquisável que armazena um recurso de toohello de referência de URL.

## <a name="workload-limits-queries-per-second"></a>Limites de carga de trabalho (consultas por segundo)
| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N/D  |~3 por réplica |~15 por réplica |~60 por réplica |>60 por réplica |>60 por réplica |

Consultas por segundo (QPS) é uma aproximação com base na heurística, usando os valores de tooderive estimado de cargas de trabalho cliente simulada e reais. Taxa de transferência QPS exata varia dependendo de sua natureza hello e dados de consulta de saudação.

Embora estimativas aproximadas são fornecidas acima, uma taxa real é difícil toodetermine, especialmente em Olá que livre compartilhado serviço em que a taxa de transferência é baseada em largura de banda disponível e da competição por recursos do sistema. Na camada gratuita do hello, recursos de computação e armazenamento são compartilhados por vários assinantes, portanto QPS para sua solução sempre irá variar dependendo de quantas outras cargas de trabalho são executados em Olá simultaneamente.

No nível padrão de saudação, você pode estimar QPS mais perto porque você tem controle sobre mais dos parâmetros de saudação. Consulte a seção de práticas recomendada Olá em [gerenciar a sua solução de pesquisa](search-manage.md) para obter orientação sobre como toocalculate QPS para suas cargas de trabalho.

## <a name="api-request-limits"></a>Limites de Solicitação da API
* Máximo de 16 MB por solicitação <sup>1</sup>
* Comprimento máximo da URL de 8 KB
* Máximo de 1000 documentos por lote de carregamentos, mesclagens ou exclusões de índice
* Máximo de 32 campos na cláusula $orderby
* O tamanho máximo do termo de pesquisa é de 32.766 bytes (32 KB menos 2 bytes) de texto codificado em UTF-8

<sup>1</sup> na pesquisa do Azure, o corpo da saudação de uma solicitação é assunto tooan limite de 16 MB, que impõe um limite prático em conteúdos de saudação de campos individuais ou coleções que não são restritas contrário limites teórico (consulte [com suporte tipos de dados](https://msdn.microsoft.com/library/azure/dn798938.aspx) para obter mais informações sobre a composição de campo e restrições).

## <a name="api-response-limits"></a>Limites de resposta da API
* Máximo de 1000 documentos retornados por página de resultados da pesquisa
* Máximo de 100 sugestões retornadas por solicitação de Sugerir API

## <a name="api-key-limits"></a>Limites de chave de API
As chaves de API são usadas para autenticação de serviço. Há dois tipos. Chaves de administração são especificadas no cabeçalho de solicitação de saudação e conceder serviço toohello de acesso de leitura / gravação completa. As chaves de consulta são somente leitura, especificado na URL hello e normalmente distribuídos tooclient aplicativos.

* Máximo de duas chaves de administração por serviço
* Máximo de 50 chaves de consulta por serviço
