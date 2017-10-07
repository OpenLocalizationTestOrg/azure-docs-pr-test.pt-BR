---
title: "aaaChoose uma SKU ou camada de preços para pesquisa do Azure | Microsoft Docs"
description: "A Pesquisa do Azure pode ser provisionada nestes SKUs: Gratuito, Básico e Standard, sendo que o Standard está disponível em várias configurações de recursos e níveis de capacidade."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Escolher um tipo de preço ou SKU para a Pesquisa do Azure
No Azure Search, um [serviço é provisionado](search-create-service-portal.md) em um tipo de preço específico ou SKU. As opções incluem: **Gratuito**, **Básico** ou **Standard**, sendo que **Standard** está disponível em várias configurações e capacidades.

finalidade de saudação deste artigo é toohelp escolha uma camada. Se a capacidade da camada acontece toobe muito baixo, será necessário tooprovision um novo serviço de camada superior hello e, em seguida, recarregue seus índices. Não há nenhuma atualização in-loco do mesmo serviço de um tooanother SKU de saudação.

> [!NOTE]
> Depois que você escolher uma camada e [provisionar um serviço de pesquisa](search-create-service-portal.md), você pode aumentar a réplica e contagens de partição no serviço de saudação. Para obter orientação, veja [Dimensionar os níveis de recursos para cargas de trabalho de consulta e indexação](search-capacity-planning.md).
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Como tooapproach um preço camada decisão
Na pesquisa do Azure, camada Olá determina a capacidade, a disponibilidade do recurso não. Em geral, os recursos estão disponíveis em todas as camadas, incluindo recursos de versão prévia. Olá uma exceção é não há suporte para indexadores em HD S3.

> [!TIP]
> Recomendamos que você sempre forneça um serviço **Gratuito** (um por assinatura, sem prazo de expiração) a fim de tê-lo prontamente disponível para projetos leves. Saudação de uso **livre** de serviço para teste e avaliação; criar um segundo serviço faturável em Olá **básica** ou **padrão** camada para maiores cargas de trabalho de teste ou produção.
>
>

Capacidade e custos da execução de serviço Olá vá lado a lado. Informações neste artigo podem ajudá-lo a decidir qual SKU fornece equilíbrio correto de hello, mas para qualquer dele toobe útil, é necessário pelo menos aproximadas estimativas na seguinte hello:

* Número e tamanho dos índices planejar toocreate
* Número e tamanho dos tooupload de documentos
* Alguma ideia de volume de consulta, em termos de QPS (consultas por segundo)

Número e tamanho são importantes porque os limites máximos são alcançados por meio de um limite rígido na contagem de saudação de índices ou documentos em um serviço ou recursos (armazenamento ou réplicas) usada pelo serviço de saudação. Olá limite real para o serviço é aquele que é usado primeiro: recursos ou objetos.

Estimativas em mãos, Olá etapas a seguir deve simplificar o processo de saudação:

* **Etapa 1** examine Olá SKU descrições abaixo toolearn sobre as opções disponíveis.
* **Etapa 2** perguntas Olá abaixo tooarrive em uma decisão preliminar.
* **Etapa 3** Finalizar sua decisão revisando os limites físicos de armazenamento e preços.

## <a name="sku-descriptions"></a>Descrições do SKU
Olá, a tabela a seguir fornece descrições de cada camada.

| Camada | Principais cenários |
| --- | --- |
| **Gratuito** |Um serviço compartilhado, sem custo adicional, usado para avaliação, investigação ou cargas de trabalho pequenas. Porque ele é compartilhado com outros assinantes, taxa de transferência de consulta e indexação varia de acordo com quem mais usando o serviço de saudação. Capacidade pequena (50 MB ou três índices com até 10 mil documentos cada). |
| **Básico** |Cargas de trabalho de produção pequenas em hardware dedicado. Altamente disponível. A capacidade é too3 réplicas e a 1 partição (2 GB). |
| **S1** |Standard 1 oferece suporte a combinações flexíveis de partições (12) e réplicas (12), usadas para as cargas de trabalho de produção média no hardware dedicado. Você pode alocar partições e réplicas em combinações com suporte de um número máximo de 36 unidades de pesquisa faturáveis. Nesse nível, as partições têm 25 GB cada e a taxa de QPS é aproximadamente 15 consultas por segundo. |
| **S2** |2 padrão executa maiores cargas de trabalho de produção usando unidades de pesquisa Olá 36 mesmo S1 mas com réplicas e partições de tamanhos maior. Nesse nível, as partições têm 100 GB e a taxa de QPS é cerca de 60 consultas por segundo. |
| **S3** |3 padrão executa proporcionalmente maiores cargas de trabalho de produção em sistemas de alta capacidade, em configurações de backup too12 partições ou 12 réplicas em 36 unidades de pesquisa. Nesse nível, as partições têm 200 GB e a taxa de QPS é maior que 60 consultas por segundo. |
| **S3 HD** |A Alta Densidade Standard 3 destina-se a um grande número de índices menores. Você pode ter até too3 partições, 200 GB. QPS de mais de 60 consultas por segundo. |

> [!NOTE]
> Limites máximos de partição e de réplica são cobrados como unidades de pesquisa (unidade 36 máximo por serviço), que impõe um limite efetivo menor que o máximo de saudação implica inicialmente. Por exemplo, no máximo toouse Olá 12 réplicas, você pode ter no máximo 3 partições (3 * 12 = 36 unidades). Da mesma forma, partições de máximo de toouse, reduzir too3 de réplicas. Confira [Dimensionar os níveis de recursos para cargas de trabalho de consulta e indexação na Pesquisa do Azure](search-capacity-planning.md) para obter um gráfico de combinações permitidas.
>
>

## <a name="review-limits-per-tier"></a>Revisar os limites por tipo
Olá, gráfico a seguir é um subconjunto dos limites de saudação do [limites de serviço na pesquisa do Azure](search-limits-quotas-capacity.md). Ela lista Olá de fatores provavelmente tooimpact uma decisão de SKU. Você pode consultar o gráfico toothis ao revisar as perguntas de saudação abaixo.

| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrato de nível de serviço (SLA) |Não <sup>1</sup> |Sim |Sim |Sim |Sim |Sim |
| Limites de índice |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Limites do documento |10.000 no total |1 milhão por serviço |15 milhões por partição |60 milhões por partição |120 milhões por partição |1 milhões por índice |
| Máximo de partições |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Tamanho da partição |Total de 50 MB |2 GB por serviço |25 GB por partição |100 GB por partição (o máximo de tooa de 1,2 TB por serviço) |200 GB por partição (o máximo de tooa de 2,4 TB por serviço) |200 GB (o máximo de tooa de 600 GB por serviço) |
| Máximo de réplicas |N/D |3 |12 |12 |12 |12 |
| Consultas por segundo |N/D |~3 por réplica |~15 por réplica |~60 por réplica |>60 por réplica |>60 por réplica |

<sup>1</sup> Os recursos de camada gratuita e de versão prévia não vêm com SLAs (contratos de nível de serviço). Para todas as camadas faturáveis, os SLAs entram em vigor quando você provisiona redundância suficiente para o serviço. Duas ou mais réplicas são necessárias para o SLA de consulta (leitura). Três ou mais réplicas são necessárias para consulta e indexação do SLA (leitura-gravação). número de saudação de partições não é uma consideração de SLA. 

<sup>2</sup> S3 e S3 HD contam com infraestrutura de alta capacidade idênticas, mas cada um deles atinge seu limite máximo de maneiras diferentes. O S3 tem como alvo um número menor de índices muito grandes. Como tal, seu limite máximo está vinculado a recursos (2,4 TB para cada serviço). O S3 HD destina-se um grande número de índices muito pequenos. Em 1.000 índices, S3 HD atinja os limites na forma de saudação de restrições de índice. Se você for um cliente de HD S3 que precise de mais de 1.000 índices, contate o Microsoft Support para obter informações sobre como tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Eliminar SKUs que não atendam aos requisitos
Olá perguntas a seguir pode ajudá-lo a chegar a decisão correta de SKU Olá para sua carga de trabalho.

1. Você tem requisitos de **SLA (Contrato de Nível de Serviço)** ? Você pode usar qualquer camada faturável (plano Básico em diante), mas você deve configurar seu serviço para redundância. Duas ou mais réplicas são necessárias para o SLA de consulta (leitura). Três ou mais réplicas são necessárias para consulta e indexação do SLA (leitura-gravação). número de saudação de partições não é uma consideração de SLA.
2. **De quantos índices** você precisa? Uma das variáveis de maiores Olá fatorar em uma decisão de SKU é o número de saudação de índices com suporte por cada SKU. Suporte de índice é em muito diferentes níveis de saudação inferior camadas de preços. Os requisitos do número de índices pode ser um determinante principal de uma decisão do SKU.
3. **Quantos documentos** será carregado em cada índice? Olá número e o tamanho dos documentos determinará o tamanho eventual de saudação do índice de saudação. Supondo que você pode estimar Olá projetado tamanho do índice de saudação, você pode comparar esse número com tamanho de partição Olá por SKU, estendido pelo número de saudação de toostore necessário partições um índice desse tamanho.
4. **O que há de carga de consulta esperada Olá**? Após definir os requisitos de armazenamento, considere as cargas de trabalho de consulta. O S2 e os dois SKUs S3 oferecem um rendimento quase equivalente, mas os requisitos de SLA descartarão quaisquer SKUs em fase preview.
5. Se você estiver considerando Olá S2 ou S3 camada, determine se você precisa de [indexadores](search-indexer-overview.md). Indexadores ainda não estão disponíveis para a camada de HD S3 hello. Abordagem alternativa é toouse um modelo de push para atualizações de índice, em que você gravar toopush de código do aplicativo, um índice de tooan do conjunto de dados.

A maioria dos clientes pode regra uma SKU específica ou com base em seu toohello respostas acima perguntas. Se você ainda não tiver certeza qual toogo SKU com, você pode postar perguntas tooMSDN ou StackOverflow fóruns ou entre em contato com o suporte do Azure para obter mais orientações.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>Validação de decisão: Olá SKU oferecem armazenamento suficiente e QPS?
Como última etapa, revisitar Olá [página de preços](https://azure.microsoft.com/pricing/details/search/) e hello [seções por serviço e por índice em limites de serviço](search-limits-quotas-capacity.md) toodouble seleção suas estimativas em limites de assinatura e de serviço.

Se qualquer um dos requisitos de preço ou armazenamento Olá estão fora dos limites, você poderá toorefactor cargas de trabalho de saudação entre vários serviços menores (por exemplo). No nível mais granular, você pode recriar índices toobe menor ou use os filtros toomake consultas mais eficientes.

> [!NOTE]
> Os requisitos de armazenamento podem ser excessivos se os documentos contiverem dados estranhos. O ideal é que os documentos contenham somente metadados ou dados pesquisáveis. Dados binários não pode ser pesquisado e devem ser armazenados separadamente (talvez em um armazenamento de tabela ou blob do Azure) com um campo em Olá índice toohold um URL referência toohello externo de dados. Olá o tamanho máximo de um documento individual é de 16 MB ou menos, se você estiver em massa carregar vários documentos em uma solicitação. Confira [Limites de serviço na Pesquisa do Azure](search-limits-quotas-capacity.md) para saber mais.
>
>

## <a name="next-step"></a>Próxima etapa
Quando você souber qual SKU é hello ajustar à direita, continue com estas etapas:

* [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md)
* [Alterar a alocação de saudação de partições e réplicas tooscale seu serviço](search-capacity-planning.md)
