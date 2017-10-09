---
title: aaaCapacity planejamento para pesquisa do Azure | Microsoft Docs
description: "Ajusta os recursos de computador de partição e réplica no Azure Search, onde o preço de cada recurso é definido em unidades de pesquisa faturáveis."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Dimensionar os níveis de recursos para cargas de trabalho de consulta e indexação na Pesquisa do Azure
Depois que você [escolher um tipo de preço](search-sku-tier.md) e [provisionar um serviço de pesquisa](search-create-service-portal.md), Olá próxima etapa é toooptionally aumento Olá número de réplicas ou partições usadas pelo serviço. Cada camada oferece um número fixo de unidades de cobrança. Este artigo explica como tooallocate tooachieve essas unidades uma configuração ideal que equilibra a seus requisitos para execução da consulta, indexação e armazenamento.

Configuração de recurso está disponível quando você configurar um serviço em Olá [camada básica](http://aka.ms/azuresearchbasic) ou uma saudação [camadas padrão](search-limits-quotas-capacity.md). Para os serviços faturáveis nessas camadas, a capacidade é comprada em incrementos de SUs (*unidades de pesquisa*), em que cada partição e réplica conta como uma SU. 

Usar menos SUs resulta em uma lista menor proporcionalmente. A cobrança está em vigor para como Olá serviço está configurado. Se você não temporariamente estiver usando um serviço, a única maneira de saudação tooavoid cobrança é excluindo serviço hello e, em seguida, recriá-la quando precisar dele.

> [!Note]
> Excluir um serviço exclui tudo nele. Há um recurso no Azure Search para fazer backup e restaurar dados de pesquisa persistentes. tooredeploy um índice existente em um novo serviço, você deve executar Olá programa usado toocreate e carregá-lo originalmente. 

## <a name="terminology-partitions-and-replicas"></a>Terminologia: partições e réplicas
Partições e réplicas são recursos principais de saudação que dão suporte a um serviço de pesquisa.

| Recurso | Definição |
|----------|------------|
|*Partições* | Fornecem armazenamento de índice e E/S para operações de leitura/gravação (por exemplo, ao recompilar ou atualizar um índice).|
|*Réplicas* | Instâncias do serviço de pesquisa Olá, usadas principalmente tooload saldo operações de consulta. Cada réplica sempre hospeda uma cópia de um índice. Se você tiver 12 réplicas, você terá 12 cópias de cada índice carregado no serviço de saudação.|

> [!NOTE]
> Não é possível toodirectly manipular ou gerenciar quais índices executado em uma réplica. Uma cópia de cada índice em cada réplica é parte da arquitetura de serviço de saudação.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Como tooallocate partições e réplicas
Na Pesquisa do Azure, um serviço recebe inicialmente um nível mínimo de recursos compostos por uma partição e uma réplica. Para tipos que dão suporte a isso, você poderá ajustar de forma incremental a capacidade de recursos computacionais aumentando as partições, se precisar de mais armazenamento e E/S ou adicionar mais réplicas para volumes maiores de consulta ou melhor desempenho. Um único serviço deve ter toohandle de recursos suficientes, todas as cargas de trabalho (indexação e consultas). Você não pode subdividir cargas de trabalho entre vários serviços.

alocação de Olá tooincrease ou alteração de réplicas e partições, recomendamos usar Olá portal do Azure. portal de saudação impõe limites de combinações permitidas permanecem abaixo de limites máximos:

1. Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione o serviço de pesquisa de saudação.
2. Em **configurações**, abra Olá **escala** folha e use Olá controles deslizantes tooincrease ou diminuir o número de saudação de partições e réplicas.

Se você precisar de uma abordagem de provisionamento baseado em código ou script, Olá [API REST de gerenciamento](https://msdn.microsoft.com/library/azure/dn832687.aspx) é um portal toohello alternativo.

Geralmente, os aplicativos de pesquisa precisam mais réplicas de partições, principalmente quando operações de serviço Olá tendem para cargas de trabalho de consulta. Olá seção em [alta disponibilidade](#HA) explica o motivo.

> [!NOTE]
> Depois que um serviço é fornecido, ele não pode ser atualizado tooa SKU superior. Será necessário toocreate um serviço de pesquisa na nova camada de saudação e recarregue seus índices. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda com o provisionamento do serviço.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Alta disponibilidade
Como é fácil e rápido relativamente tooscale backup, geralmente recomendamos que você iniciar com uma partição e uma ou duas réplicas e expansão vertical como volumes de consulta de compilação. Para muitos serviços em camadas de saudação Basic ou S1, uma partição fornece armazenamento e e/s suficientes (em 15 milhões de documentos por partição).

As cargas de trabalho de consulta são executadas principalmente em réplicas. Se precisar de mais taxa de transferência ou alta disponibilidade, provavelmente, você precisará de mais réplicas.

Recomendações gerais para alta disponibilidade são:

* Duas réplicas para alta disponibilidade de cargas de trabalho somente leitura (consultas)
* Três ou mais réplicas para alta disponibilidade de cargas de trabalho de leitura/gravação (consultas e indexação à medida que documentos individuais são adicionados, atualizados ou excluídos)

Os SLAs (contratos de nível de serviço) do Azure Search são direcionados a operações de consulta e a atualizações de índice formadas pela adição, atualização ou exclusão de documentos.

### <a name="index-availability-during-a-rebuild"></a>Disponibilidade de índice durante uma recompilação

Alta disponibilidade para a pesquisa do Azure se refere a atualizações de índice e tooqueries que não envolvem a recriação de um índice. Se você excluir um campo, alterar um tipo de dados ou renomear um campo, você precisará de índice de saudação toorebuild. índice de saudação toorebuild, você deve excluir Olá de índice, recrie o índice de saudação e recarregar dados hello.

> [!NOTE]
> Você pode adicionar o novo índice de pesquisa do Azure tooan campos sem recriar o índice de saudação. valor de saudação do novo campo de saudação será null para todos os documentos já existentes nesse índice hello.

disponibilidade de índice toomaintain durante uma reconstrução, você deve ter uma cópia do índice de saudação com um nome diferente em Olá mesmo serviço ou uma cópia da saudação de índice com o mesmo nome em um serviço diferente e, em seguida, fornecer lógica de redirecionamento ou failover no seu código de saudação.

## <a name="disaster-recovery"></a>Recuperação de desastre
Atualmente, não há mecanismo integrado para recuperação de desastres. Adicionando partições ou réplicas seria a estratégia errado Olá para atender a objetivos de recuperação de desastres. abordagem mais comum de saudação é tooadd redundância no nível de serviço hello, configurando um segundo serviço de pesquisa em outra região. Assim como a disponibilidade durante uma recriação de índice, redirecionamento de saudação ou lógica de failover deve vir do seu código.

## <a name="increase-query-performance-with-replicas"></a>Aumentar o desempenho de consulta com réplicas
A latência da consulta é um indicador da necessidade de réplicas adicionais. Geralmente, uma primeira etapa para melhorar o desempenho de consulta é tooadd mais deste recurso. Como adicionar réplicas, cópias adicionais do índice de saudação sejam colocadas online toosupport maiores cargas de trabalho de consulta e solicitações de saudação do saldo tooload pela Olá várias réplicas.

Não é possível fornecer estimativas de disco rígidas em consultas por segundo (QPS): consulta desempenho depende da complexidade de saudação da saudação de consulta e cargas de trabalho concorrentes. Em média, uma réplica em SKUs Básico ou S1 pode atender cerca de 15 QPS, mas a taxa de transferência será um maior ou menor dependendo da complexidade da consulta (consultas facetadas são mais complexas) e da latência de rede. Além disso, é importante toorecognize que embora adicionar réplicas irá adicionar definitivamente o dimensionamento e desempenho, Olá resultado não é estritamente linear: adicionar três réplicas não garante a taxa de transferência triplique.

toolearn sobre QPS, incluindo métodos para calcular QPS para cargas de trabalho, consulte [gerenciar o serviço de pesquisa](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Aumentar o desempenho de indexação com partições
Aplicativos de pesquisa que exigem atualização de dados quase em tempo real precisarão proporcionalmente de mais partições de réplicas. A adição de partições distribui as operações de leitura/gravação em uma quantidade maior de recursos de computação. Também oferece mais espaço em disco para armazenar documentos e índices adicionais.

Índices maiores têm mais tooquery. Assim, você poderá perceber que cada aumento incremental em partições requer um aumento proporcional, mas menor, em réplicas. complexidade de saudação de suas consultas e o volume de consulta serão fatorados em como rapidamente a execução da consulta é devolvida.

## <a name="basic-tier-partition-and-replica-combinations"></a>Camada Básica: combinações de partição e réplica
Um serviço básico pode ter exatamente uma partição e até toothree réplicas, para um limite máximo de três SUs. recursos apenas ajustável Olá é réplicas. É necessário um mínimo de duas réplicas para alta disponibilidade em consultas.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Tipos Standard: combinações de partição e réplica
Esta tabela mostra Olá SUs necessário toosupport combinações de réplicas e partições, limite de 36 SU toohello assunto, para todas as camadas padrão.

|   | **1 partição** | **2 partições** | **3 partições** | **4 partições** | **6 partições** | **12 partições** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 réplica** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 réplicas** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **3 réplicas** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 réplicas** |4 SU |8 SU |12 SU |16 SU |24 SU |N/D |
| **5 réplicas** |5 SU |10 SU |15 SU |20 SU |30 SU |N/D |
| **6 réplicas** |6 SU |12 SU |18 SU |24 SU |36 SU |N/D |
| **12 réplicas** |12 SU |24 SU |36 SU |N/D |N/D |N/D |

SUs, preço e capacidade são explicadas em detalhes em Olá site do Azure. Para obter mais informações, consulte [Detalhes de Preço](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> número de saudação de partições e réplicas uniformemente divide em 12 (especificamente, 1, 2, 3, 4, 6, 12). Isso ocorre porque a Pesquisa do Azure divide previamente cada índice em 12 fragmentos, para que possam ser distribuídos em partes iguais entre todas as partições. Por exemplo, se o serviço tem três partições e criar um índice, cada partição conterá quatro fragmentos de índice hello. Como a pesquisa do Azure fragmenta um índice é um detalhe de implementação, toochange assunto em versões futuras. Embora Olá número 12 hoje, não espere que número tooalways ser 12 no hello futuras.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Fórmula de cobrança para recursos de réplica e uma partição
fórmula de saudação para calcular quantas SUs é usado para combinações específicas é o produto de saudação de réplicas e partições, ou (R X P = SU). Por exemplo, três réplicas multiplicadas por três partições são cobradas como nove SUs.

Custo por SU é determinado pela camada de hello, com uma taxa de cobrança por unidade menor de básico que padrão. As taxas de cada camada podem ser encontradas em [Detalhes de Preço](https://azure.microsoft.com/pricing/details/search/).
