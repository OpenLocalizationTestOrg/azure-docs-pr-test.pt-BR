---
title: "extensões de PostgreSQL aaaUsing no banco de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve a funcionalidade de saudação do hello capacidade tooextend do banco de dados usando as extensões no banco de dados do Azure para PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Extensões de PostgreSQL no Banco de Dados do Azure para PostgreSQL
PostgreSQL fornece a funcionalidade de saudação do hello capacidade tooextend do banco de dados usando as extensões. Extensões permitir várias toobe de objetos SQL relacionada agrupada em um único pacote e podem ser carregadas ou removidas do banco de dados com um único comando. Extensões de uma vez carregadas no banco de dados de saudação podem funcionar como recursos incorporados no. Para saber mais sobre extensões PostgreSQL, consulte [Empacotar objetos relacionados em uma extensão](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>Como toouse PostgreSQL extensões?
Extensões de PostgreSQL necessário toobe instalado para seu banco de dados antes de você pode usá-los. tooinstall uma extensão específica, execute o [criar extensão](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) comando psql tooload de ferramenta Olá empacotados objetos no banco de dados.

O Banco de Dados do Azure para PostgreSQL oferece suporte a um subconjunto de extensões de chave, conforme listado aqui. Além da saudação daqueles listados, não há suporte para outras extensões. Não é possível criar sua própria extensão com o Banco de Dados do Azure para o serviço PostgreSQL.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Extensões com suporte do Banco de Dados do Azure para PostgreSQL
lista Olá PostgreSQL extensões padrão que são atualmente suportadas pelo banco de dados do Azure para PostgreSQL tabelas a seguir de saudação. Você também pode obter essas informações consultando pg\_available\_extensions. 

### <a name="data-types-extensions"></a>Extensões de tipos de dados

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Fornece um tipo de cadeia de caracteres que diferencia maiúsculas de minúsculas |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Fornece o tipo de dados para armazenar conjuntos de pares de chave/valor |

### <a name="functions-extensions"></a>Extensões de funções

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Fornece várias semelhanças de toodetermine de funções e a distância entre cadeias de caracteres. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Fornece funções e operadores para manipular matrizes de inteiros sem nulos. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Fornece funções de criptografia |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Gerencia as tabelas particionadas por hora ou ID |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Fornece funções e operadores para determinar a similaridade de saudação do texto alfanumérico, com base na correspondência de trigram |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Gerar identificadores universais exclusivos (UUIDs) |

### <a name="full-text-search-extensions"></a>Extensões de pesquisa de texto completo

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
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
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Linguagem de procedimento carregável PL/pgSQL |

### <a name="miscellaneous-extensions"></a>Extensões diversas

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Fornece uma maneira de examinar o que está acontecendo no cache de buffer Olá compartilhado em tempo real. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Fornece uma maneira tooload relação de dados no cache de buffer de saudação. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Fornece um meio para rastrear as estatísticas de execução de todas as instruções SQL executadas por um servidor. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Wrapper de dados externo usado tooaccess dados armazenados em servidores PostgreSQL externos |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Extensão** | **Descrição** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Objetos espaciais e geográficos para PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Tooparse usado um endereço em elementos constituintes. Usado a etapa de normalização toosupport geocodificação endereço. |
| [pgrouting](http://pgrouting.org/) | Estende Olá PostGIS / PostgreSQL geoespaciais tooprovide geoespaciais funcionalidade de roteamento de banco de dados. |

## <a name="next-steps"></a>Próximas etapas
Não vê uma extensão que você gostaria que toouse? Fale conosco. Vote em solicitações existentes ou crie novos comentários e desejos em nosso [Fórum de comentários do cliente](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
