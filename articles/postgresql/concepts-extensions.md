---
title: "Usar as extensões de PostgreSQL no Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve a capacidade de estender a funcionalidade de seu banco de dados usando as extensões no Banco de Dados para PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/28/2017
ms.openlocfilehash: f02588495e7107b34dac7e076cf3612de12b51d4
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/29/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Extensões de PostgreSQL no Banco de Dados do Azure para PostgreSQL
O PostgreSQL fornece a capacidade de estender a funcionalidade de seu banco de dados usando as extensões. As extensões permitem o agrupamento de vários objetos SQL relacionados em um único pacote que pode ser carregado ou removido de seu banco de dados com um único comando. Depois de ser carregada no banco de dados, as extensões podem funcionar como recursos internos. Para saber mais sobre extensões PostgreSQL, consulte [Empacotar objetos relacionados em uma extensão](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-to-use-postgresql-extensions"></a>Como usar as extensões PostgreSQL
As extensões PostgreSQL devem ser instaladas no banco de dados para que você possa usá-las. Para instalar uma extensão específica, execute o comando [CREATE EXTENSION](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) na ferramenta psql para carregar os objetos empacotados em seu banco de dados.

No momento, o Banco de Dados do Azure para PostgreSQL dá suporte a um subconjunto de extensões de chave, como é listado abaixo. As extensões além das listadas não têm suporte, não é possível criar sua própria extensão com o serviço de Banco de Dados do Azure para PostgreSQL.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Extensões com suporte do Banco de Dados do Azure para PostgreSQL
As tabelas a seguir listam as extensões PostgreSQL padrão que têm suporte atualmente do Banco de Dados do Azure para PostgreSQL. Essas informações também estão disponíveis por meio da consulta de `pg\_available\_extensions`.

### <a name="data-types-extensions"></a>Extensões de tipos de dados

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [chkpass](https://www.postgresql.org/docs/9.6/static/chkpass.html) | Fornece um tipo de dados para as senhas criptografadas automaticamente. |
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Fornece um tipo de cadeia de caracteres que não diferencia maiúsculas de minúsculas. |
| [cube](https://www.postgresql.org/docs/9.6/static/cube.html) | Fornece um tipo de dados para cubos multidimensionais. |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Fornece um tipo de dados para armazenar conjuntos de pares chave-valor. |
| [isn](https://www.postgresql.org/docs/9.6/static/isn.html) | Fornece tipos de dados para padrões de numeração de produto internacionais. |
| [ltree](https://www.postgresql.org/docs/9.6/static/ltree.html) | Fornece um tipo de dados para estruturas semelhantes a árvores hierárquicas. |

### <a name="functions-extensions"></a>Extensões de funções

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [earthdistance](https://www.postgresql.org/docs/9.6/static/earthdistance.html) | Fornece um meio para calcular as distância ortodrômicas na superfície da Terra. |
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Fornece várias funções para determinar semelhanças e a distância entre cadeias de caracteres. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Fornece funções e operadores para manipular matrizes de inteiros sem nulos. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Fornece funções de criptografia. |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Gerencia as tabelas de partição por hora ou ID. |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Fornece funções e operadores para determinar a semelhança de texto alfanumérico, com base na correspondência de trigram. |
| [tablefunc](https://www.postgresql.org/docs/9.6/static/tablefunc.html) | Fornece funções que manipulam tabelas inteiras, incluindo a tabela de referência cruzada. |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Gera UUIDs (identificadores exclusivos universais). |

### <a name="full-text-search-extensions"></a>Extensões de pesquisa de texto completo

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [dict\_int](https://www.postgresql.org/docs/9.6/static/dict-int.html) | Fornece um modelo de dicionário de pesquisa de texto para números inteiros. |
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Um dicionário de pesquisa de texto que remove acentos (sinais diacríticos) dos lexemas. |

### <a name="index-types-extensions"></a>Extensões de tipos de índice

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Fornece classes de operador GIN de exemplo que implementam um comportamento como da árvore B para certos tipos de dados. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Fornece classes de operador de índice GiST que implementam a árvore B. |

### <a name="language-extensions"></a>Extensões de linguagem

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Linguagem de procedimento carregável PL/pgSQL. |

### <a name="miscellaneous-extensions"></a>Extensões diversas

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Fornece um meio para examinar o que está acontecendo no cache do buffer compartilhado em tempo real. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Fornece uma maneira para carregar dados de relação no cache de buffer. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Fornece um meio para rastrear as estatísticas de execução de todas as instruções SQL executadas por um servidor. |
| [pgrowlocks](https://www.postgresql.org/docs/9.6/static/pgrowlocks.html) | Fornece um meio para mostrar informações de bloqueio de nível de linha. |
| [pgstattuple](https://www.postgresql.org/docs/9.6/static/pgstattuple.html) | Fornece um meio para mostrar estatísticas em nível de tupla. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Wrapper de dados externos usado para acessar dados armazenados em servidores PostgreSQL externos. |

### <a name="postgis-extensions"></a>Extensões PostGIS

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Objetos espaciais e geográficos para PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Usado para analisar um endereço em elementos constituintes. Usado para oferecer suporte à etapa de normalização de endereços de geocodificação. |
| [pgrouting](http://pgrouting.org/) | Estende o banco de dados geoespacial PostGIS/PostgreSQL para fornecer a funcionalidade de roteamento geoespacial. |

## <a name="next-steps"></a>Próximas etapas
Se você não vir uma extensão que gostaria de usar, fale conosco. Vote em solicitações existentes ou crie novos comentários e solicitações em nosso [Fórum de comentários do cliente](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
