---
title: "Visão geral de referência de banco de dados SQL aaaAzure"
description: "Este tópico descreve Olá referencial de banco de dados do SQL Azure usado para medir o desempenho de saudação do banco de dados do SQL Azure."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Visão geral do parâmetro de comparação do Banco de Dados SQL do Azure
## <a name="overview"></a>Visão geral
O Banco de Dados SQL do Microsoft Azure oferece três [camadas de serviço](sql-database-service-tiers.md) com vários níveis de desempenho. Cada nível de desempenho fornece um crescente conjunto de recursos ou 'power' projetado toodeliver progressivos de produtividade.

É importante toobe tooquantify capaz de como o aumento de capacidade de cada nível de desempenho Olá resulta em desempenho de banco de dados maior. toodo isso, a Microsoft desenvolveu hello Azure SQL banco de dados do parâmetro de comparação (ASDB). Olá referencial coloca em prática uma combinação de operações básicas encontradas em todas as cargas de trabalho OLTP. Medimos a taxa de transferência de saudação obtida para bancos de dados em execução em cada nível de desempenho.

Olá recursos e capacidade de cada nível de desempenho e da camada de serviço são expressos em termos de [unidades de transação do banco de dados (DTUs)](sql-database-what-is-a-dtu.md). DTUs fornecem uma maneira toodescribe capacidade relativa do hello de um nível de desempenho com base em uma medida combinada de CPU, memória e leitura e gravação taxas oferecidas por cada nível de desempenho. Duplicar a classificação da DTU Olá de um banco de dados é igual a toodoubling power de banco de dados de saudação. Olá referencial nos permite impacto de saudação tooassess sobre o desempenho do banco de dados de Olá aumento oferecida por cada nível de desempenho fazendo com que as operações de banco de dados real, ao expandir o tamanho do banco de dados, o número de usuários e as taxas de transação em proporção de capacidade recursos de toohello fornecidos toohello banco de dados.

Ao expressar a taxa de transferência de saudação da camada de serviço básico do hello usando transações por hora, a camada de serviço Standard hello usando transações por minuto e a camada de serviço Premium Olá usando transações por segundo, ele torna mais fácil tooquickly relacionar Olá potencial de desempenho de cada camada toohello de serviço de um aplicativo.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Correlacionar o desempenho de banco de dados do parâmetro de comparação resultados tooreal mundo
Ele é importante toounderstand que ASDB, como todos os parâmetros de comparação, só é representativo e indicativo. Olá transação taxas obtidas com o aplicativo de benchmark hello não será ser Olá mesmo que pode ser obtida com outros aplicativos. parâmetro de comparação de saudação consiste em uma coleção de tipos são executados em um esquema que contém uma variedade de tipos de dados e tabelas de transação diferente. Enquanto os exercícios de benchmark Olá Olá mesmas operações básicas comuns cargas de trabalho OLTP de tooall, ele não representa uma classe específica de banco de dados ou aplicativo. meta de saudação do parâmetro de comparação de saudação é tooprovide um guia razoável toohello relativo de desempenho de um banco de dados que pode ser esperado quando o dimensionamento para cima ou para baixo entre níveis de desempenho. Na realidade, os bancos de dados de diferentes tamanhos e complexidade, lidam com combinações diferentes de cargas de trabalho e responderão de formas diferentes. Por exemplo, um aplicativo de E/S intensiva pode atingir os limites de E/S mais cedo ou um aplicativo de uso intensivo de CPU pode atingir os limites de CPU mais cedo. Não há nenhuma garantia de que qualquer banco de dados específico se dimensionará Olá que mesma forma como parâmetro de comparação de saudação em aumento de carga.

Olá referencial e sua metodologia são descritos em mais detalhes abaixo.

## <a name="benchmark-summary"></a>Resumo do parâmetro de comparação
ASDB mede o desempenho de saudação de uma combinação de operações de banco de dados básicos que ocorrem com mais frequência em cargas de trabalho (OLTP) de processamento de transações online. Embora benchmark Olá destina-se com a nuvem de computação em mente, transações, preenchimento de dados e esquema de banco de dados de saudação foram projetada toobe amplamente representativos dos elementos básicos de hello mais comumente usados em cargas de trabalho OLTP.

## <a name="schema"></a>Esquema
esquema de saudação é projetado toohave suficiente toosupport variedade e complexidade uma ampla gama de operações. Olá execuções em relação a um banco de dados composto por seis tabelas. tabelas de saudação se enquadram em três categorias: tamanho fixo, expansão e progressão. Há duas tabelas de tamanho fixo; três tabelas em escala e uma tabela crescente. As tabelas de tamanho fixo têm um número constante de linhas. Tabelas de expansão têm uma cardinalidade que é proporcional toodatabase desempenho, mas não é alterado durante a comparação de saudação. Olá, aumentando a tabela é dimensionada como uma tabela de expansão na carga inicial, mas altera cardinalidade de saudação do curso Olá executando benchmark hello como linhas são inseridas e excluídas.

esquema Hello inclui uma mistura de tipos de dados, incluindo inteiros, numéricos, caracteres e data/hora. esquema de saudação inclui chaves primária e secundária, mas não as chaves estrangeiras - ou seja, há nenhuma restrição de integridade referencial entre tabelas.

Um programa de geração de dados gera dados de saudação para o banco de dados de saudação inicial. Os dados numéricos e inteiros são gerados com várias estratégias. Em alguns casos, os valores são distribuídos aleatoriamente em um intervalo. Em outros casos, um conjunto de valores é aleatoriamente permutado tooensure que uma distribuição específica seja mantida. Campos de texto são gerados a partir de uma lista ponderada de palavras tooproduce dados de aparência realista.

banco de dados de saudação é dimensionado com base em um "fator de escala". fator de escala de saudação (abreviado como SF) determina a cardinalidade Olá Olá expansão e progressão tabelas. Conforme descrito abaixo em Olá seção usuários e o ritmo, tamanho do banco de dados de saudação, o número de usuários e o desempenho máximo são dimensionados em proporção tooeach outros.

## <a name="transactions"></a>Transações
carga de trabalho Olá consiste em tipos de transação nove, conforme mostrado na tabela de saudação abaixo. Cada transação é projetado toohighlight um conjunto específico de características do sistema em hardware de mecanismo e o sistema de banco de dados hello, com alto contraste do hello outras transações. Essa abordagem torna mais fácil impacto de saudação tooassess de desempenho de toooverall componentes diferentes. Por exemplo, a transação de hello "Leitura intensa" gera um número significativo de operações de leitura de disco.

| Tipo de transação | Descrição |
| --- | --- |
| Leitura Simples |SELECT; na memória; somente leitura |
| Leitura Média |SELECT; maior parte na memória; somente leitura |
| Leitura Intensa |SELECT; maior parte fora da memória; somente leitura |
| Atualização Simples |UPDATE; na memória; leitura/gravação |
| Atualização Intensa |UPDATE; maior parte fora da memória; leitura/gravação |
| Inserção Simples |INSERT; na memória; leitura/gravação |
| Inserção Intensa |INSERT; maior parte fora da memória; leitura/gravação |
| Excluir |DELETE; combinação de na memória e não na memória; leitura/gravação |
| CPU Intensa |SELECT; na memória; carga de CPU relativamente intensa; somente leitura |

## <a name="workload-mix"></a>Combinação de carga de trabalho
As transações são selecionadas aleatoriamente de uma distribuição ponderada com hello combinação geral a seguir. Olá, combinação geral tem uma taxa de leitura/gravação de aproximadamente 2:1.

| Tipo de transação | % de combinação |
| --- | --- |
| Leitura Simples |35 |
| Leitura Média |20 |
| Leitura Intensa |5 |
| Atualização Simples |20 |
| Atualização Intensa |3 |
| Inserção Simples |3 |
| Inserção Intensa |2 |
| Excluir |2 |
| CPU Intensa |10 |

## <a name="users-and-pacing"></a>Usuários e definição
carga de trabalho de parâmetro de comparação de saudação é orientada por uma ferramenta que envia transações através de um conjunto de comportamento das conexões toosimulate Olá de um número de usuários simultâneos. Embora todas as transações e conexões de saudação são gerada de máquina, para manter a simplicidade fazemos referência conexões toothese como "usuários". Embora cada usuário opere independentemente de todos os outros usuários, todos os usuários executam Olá mesmo ciclo de etapas abaixo:

1. Estabeleça uma conexão de banco de dados.
2. Repita até tooexit sinalizado:
   * Selecione uma transação aleatoriamente (de uma distribuição ponderada).
   * Execute transações Olá selecionado e medir o tempo de resposta hello.
   * Aguarde uma definição de atraso.
3. Feche a conexão de banco de dados de saudação.
4. Sair.

Olá definição dos atrasos (na etapa 2c) é selecionado aleatoriamente, mas com uma distribuição cuja média é de 1,0 segundo. Portanto, cada usuário pode, em média, gerar no máximo uma transação por segundo.

## <a name="scaling-rules"></a>Regras de dimensionamento
número de saudação de usuários é determinado pelo tamanho do banco de dados de saudação (em unidades de fator de escala). Há um usuário para cada cinco unidades de fator de escala. Devido à definição de atrasos de hello, um usuário pode gerar no máximo uma transação por segundo, em média.

Por exemplo, um fator de escala de 500 (SF = 500) bancos de dados terá 100 usuários e pode atingir uma taxa máxima de 100 TPS. toodrive uma taxa TPS mais alta exige mais usuários e um banco de dados maior.

Olá tabela a seguir mostra o número de saudação de usuários realmente mantidos para cada nível de desempenho e da camada de serviço.

| Camada de serviço (nível de desempenho) | Usuários | Tamanho do banco de dados |
| --- | --- | --- |
| Basic |5 |720 MB |
| Standard (S0) |10 |1 GB |
| Standard (S1) |20 |2,1 GB |
| Standard (S2) |50 |7,1 GB |
| Premium (P1) |100 |14 GB |
| Premium (P2) |200 |28 GB |
| Premium (P6/P3) |800 |114 GB |

## <a name="measurement-duration"></a>Duração da medida
Uma execução válida do parâmetro de comparação exige uma duração da medida permanente de pelo menos uma hora.

## <a name="metrics"></a>Métricas
as principais métricas de saudação benchmark Olá são tempo de resposta e a taxa de transferência.

* Taxa de transferência é medida de desempenho essencial Olá benchmark hello. A taxa de transferência é informada em transações por unidade de tempo, contando todos os tipos de transação.
* O tempo de resposta é uma medida da previsibilidade do desempenho. restrição de tempo de resposta de saudação varia de acordo com a classe de serviço, com classes superiores de serviço tem um requisito de tempo de resposta mais rigoroso, conforme mostrado abaixo.

| Classe de serviço | Medida de taxa de transferência | Requisito de tempo de resposta |
| --- | --- | --- |
| Premium |Transações por segundo |95º percentil em 0,5 segundo |
| Standard |Transações por minuto |90º percentil em 1,0 segundo |
| Basic |Transações por hora |80º percentil em 2,0 segundos |

## <a name="conclusion"></a>Conclusão
Olá referencial de banco de dados do SQL Azure mede o desempenho relativo de saudação do banco de dados do SQL Azure em execução em um intervalo de saudação de camadas de serviço disponíveis e níveis de desempenho. Olá referencial coloca em prática uma combinação de operações de banco de dados básicos que ocorrem com mais frequência em cargas de trabalho (OLTP) de processamento de transações online. Medindo o desempenho real, o referencial de saudação fornece uma avaliação mais significativa do impacto de saudação na taxa de transferência de alterar o nível de desempenho de saudação que é possível listando apenas recursos Olá fornecidos por cada nível, como velocidade da CPU, tamanho da memória e IOPS . Olá futuras, vamos continuar tooevolve Olá benchmark toobroaden seu escopo e expandir Olá dados fornecidos.

## <a name="resources"></a>Recursos
[Introdução tooSQL banco de dados](sql-database-technical-overview.md)

[Camadas de serviço e níveis de desempenho](sql-database-service-tiers.md)

[Diretrizes de desempenho para bancos de dados únicos](sql-database-performance-guidance.md)
