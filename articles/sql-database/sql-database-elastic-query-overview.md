---
title: "Visão geral de consulta Elástico de banco de dados SQL do aaaAzure | Microsoft Docs"
description: "Visão geral do recurso de consulta Elástico Olá"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Visão geral da consulta elástica do Banco de Dados SQL do Azure (visualização)
recurso de consulta Elástico Hello (em visualização) permite que você toorun uma consulta Transact-SQL que abrange vários bancos de dados no banco de dados do SQL Azure. Isso permite consultas de bancos de dados de tooperform tooaccess tabelas remotas e tooconnect Microsoft e terceiros tooquery de ferramentas (Excel, Power BI, Tableau, etc.) em camadas de dados com vários bancos de dados. Usando esse recurso, você pode dimensionar as camadas de dados toolarge consultas no banco de dados SQL e visualizar os resultados de saudação em relatórios de business intelligence (BI).


## <a name="why-use-elastic-queries"></a>Por que usar consultas elásticas?

**Banco de Dados SQL do Azure**

Consulte em bancos de dados SQL do Azure totalmente em T-SQL. Isso permite consultas somente leitura de bancos de dados remotos. Isso fornece uma opção para o local atual para aplicativos de toomigrate de clientes do SQL Server usando nomes de três e quatro partes ou de servidor vinculado tooSQL banco de dados.

**Disponível no nível Standard**

Há suporte para consulta de elástica no nível de desempenho padrão Olá na camada de desempenho adição toohello Premium. Consulte Olá seção limitações da visualização abaixo sobre limitações de desempenho para os níveis de desempenho inferiores.

**Bancos de dados por push tooremote**

Consultas Elásticos agora podem enviar parâmetros toohello remotos bancos de dados SQL para execução.

**Execução de procedimento armazenado**

Execute chamadas remotas de procedimento armazenado ou funções remotas usando [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714).

**Flexibilidade**

Tabelas externas com elástica consulta podem referenciar tabelas tooremote com um esquema diferente ou nome de tabela.

## <a name="elastic-query-scenarios"></a>Cenários de consulta elástica

meta de saudação é toofacilitate consultando cenários onde vários bancos de dados contribuem linhas em um único resultado geral. consulta de saudação ou pode ser composta por Olá usuário ou aplicativo a diretamente ou indiretamente por meio de ferramentas que estão conectados toohello banco de dados. Isso é especialmente útil ao criar relatórios usando as ferramentas comerciais de BI ou de integração de dados, ou então qualquer aplicativo que não possa ser alterado. Com uma consulta elástica, você pode consultar em vários bancos de dados usando a experiência de conectividade do SQL Server familiar Olá em ferramentas como o Excel, Power BI, Tableau ou Cognos.
Uma consulta elástica permite o fácil acesso tooan toda coleção de bancos de dados por meio de consultas emitidas pelo SQL Server Management Studio ou Visual Studio e facilita a consulta de bancos de dados do Entity Framework ou outros ambientes de ORM. A Figura 1 mostra um cenário em que aplicativos de nuvem existente (que usa Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md)) camada compilações em um dados expandidos e uma consulta elástica é usada para bancos de dados de relatório.

**Figura 1** Consulta elástica usada na camada de dados escalada horizontalmente

![Consulta elástica usada na camada de dados escalada horizontalmente][1]

Cenários de cliente para consulta Elástico são caracterizados por Olá topologias a seguir:

* **Particionamento vertical - consultas de bancos de dados** (topologia 1): dados saudação são particionados verticalmente entre vários bancos de dados em uma camada de dados. Geralmente, diferentes conjuntos de tabelas residem em bancos de dados diferentes. Isso significa que esse esquema Olá é diferente em bancos de dados diferentes. Por exemplo, todas as tabelas de inventário estão em um banco de dados, enquanto todas as tabelas relacionadas à contabilidade estão em um segundo banco de dados. Casos de uso comuns com essa topologia requerem um tooquery em ou relatórios toocompile entre tabelas em vários bancos de dados.
* **Particionamento horizontal - fragmentação** (topologia 2): os dados são particionados horizontalmente de camada toodistribute linhas em uma expansão de dados. Com essa abordagem, o esquema de saudação é idêntica em todos os bancos de dados participantes. Essa abordagem também é chamada de “fragmentação”. Fragmentação pode ser executada e gerenciados usando bibliotecas de ferramentas de banco de dados Elástico hello (1) ou (2) autofragmentação. Uma consulta elástica é relatórios tooquery ou compilação usados em vários fragmentos.

> [!NOTE]
> Consulta elástica funciona melhor para cenários de relatórios ocasionais em que a maioria do processamento de saudação pode ser executada na camada de dados de saudação. Para os cenários de cargas de trabalho de relatórios pesadas ou data warehouse com consultas mais complexas, considere também usar o [SQL Data Warehouse do Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Particionamento vertical - consultas entre bancos de dados

toobegin de codificação, consulte [Introdução à consulta de bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).

Uma consulta elástica pode ser usado toomake dados localizados no banco de dados disponível tooother SQL bancos de dados SQL. Isso permite consultas de tootables de toorefer um banco de dados em qualquer outro SQL banco de dados remoto. Olá primeira etapa é toodefine uma fonte de dados externa para cada banco de dados remoto. fonte de dados externa Olá é definido no banco de dados local saudação do qual você deseja toogain acesso tootables localizado no banco de dados remoto hello. Não são necessárias alterações no banco de dados remoto hello. Para verticais particionamentos cenários típicos onde os bancos de dados diferentes têm esquemas diferentes, Elásticos consultas podem ser usada tooimplement casos de uso comuns, como acessar os dados tooreference e entre bancos de dados consultando.

> [!IMPORTANT]
> Você deve ter a permissão para ALTERAR QUALQUER FONTE DE DADOS EXTERNA. Essa permissão é incluída com a permissão ALTER DATABASE hello. Permissões ALTER ANY EXTERNAL DATA SOURCE são necessários toorefer toohello subjacente da fonte de dados.
>

**Dados de referência**: topologia Olá é usada para gerenciamento de dados de referência. Na Figura Olá abaixo, duas tabelas (T1 e T2) com dados de referência são mantidas em um banco de dados dedicado. Usando uma consulta elástica, agora você pode acessar tabelas T1 e T2 remotamente de outros bancos de dados, conforme mostrado na Figura hello. Use a topologia 1 se as tabelas de referência forem pequenas ou se as consultas remotas na tabela de referência tiverem predicados seletivos.

**Figura 2** particionamento Vertical - usando dados de referência tooquery consulta Elástico

![Particionamento vertical - usando dados de referência tooquery consulta Elástico][3]

**Consultas entre bancos de dados**: as consultas elásticas habilitam casos de uso que exigem consultas em vários Bancos de Dados SQL. A Figura 3 mostra quatro bancos de dados diferentes: CRM, Inventário, RH e Produtos. Consultas executadas em um banco de dados de saudação também precisam acessar tooone ou Olá a todos os outros bancos de dados. Usando uma consulta elástica, você pode configurar seu banco de dados para esse caso, executando algumas instruções DDL simples em cada um dos quatro bancos de dados de saudação. Após essa configuração, a tabela remota de tooa de acesso é tão simple quanto referindo-se a tabela local tooa de suas consultas T-SQL ou de suas ferramentas de BI. Essa abordagem é recomendada se consultas remotas Olá não retornam resultados grandes.

**Figura 3** particionamento Vertical - usando consulta Elástico tooquery entre vários bancos de dados

![Particionamento vertical - usando consulta Elástico tooquery entre vários bancos de dados][4]

etapas a seguir Hello configuram consultas de banco de dados Elástico para cenários de particionamentos verticais que requerem a tabela do access tooa localizado em bancos de dados SQL remotos com hello mesmo esquema:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource do tipo **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Após a execução de instruções de DDL Olá, você pode acessar a tabela de remota hello "mytable" como se fosse uma tabela local. Banco de dados SQL do Azure automaticamente abre a conexão toohello banco de dados remoto, processa sua solicitação no banco de dados remoto hello e retorna resultados de saudação.

## <a name="horizontal-partitioning---sharding"></a>Particionamento horizontal - fragmentação
Usando a consulta Elástico tooperform relatórios de tarefas fragmentado, ou seja, horizontalmente particionadas, camada de dados requer um [mapa de fragmentos de banco de dados Elástico](sql-database-elastic-scale-shard-map-management.md) toorepresent Olá bancos de dados da camada de dados de saudação. Normalmente, somente um mapa do fragmento único é usado neste cenário e um banco de dados dedicado com recursos de consulta Elástico (nó principal) serve como ponto de entrada hello para consultas de relatórios. Somente esse banco de dados dedicado precisa de mapa do fragmento toohello acesso. A Figura 4 ilustra essa topologia e sua configuração com o mapa de fragmentos e de banco de dados de consulta Elástico hello. bancos de dados de saudação na camada de dados Olá podem ser de qualquer banco de dados SQL versão ou edição. Para obter mais informações sobre a biblioteca de cliente do banco de dados Elástico hello e criar mapas de fragmento, consulte [gerenciamento de mapa do fragmento](sql-database-elastic-scale-shard-map-management.md).

**Figura 4** Particionamento horizontal - Usando a consulta elástica para relatórios de camadas de dados fragmentados

![Particionamento horizontal - Usando a consulta elástica para relatórios de camadas de dados fragmentados][5]

> [!NOTE]
> Consulta de banco de dados Elástico (nó principal) pode ser separado do banco de dados, ou pode ser Olá mesmo esse mapa de fragmentos de saudação de hosts de banco de dados. Qualquer configuração que você escolher, verifique se essa camada de serviço e o desempenho do banco de dados é a quantidade de saudação esperada de toohandle alta o suficiente de solicitações de logon/consulta.

Olá etapas a seguir configuram consultas de banco de dados Elástico para horizontais cenários particionamentos que requerem acesso tooa conjunto da tabela que estão localizados em (normalmente) vários remotos bancos de dados SQL:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Criar um [mapa do fragmento](sql-database-elastic-scale-shard-map-management.md) que representa sua camada de dados usando a biblioteca de cliente do banco de dados Elástico hello.   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource do tipo **SHARD_MAP_MANAGER**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Depois de executar essas etapas, você pode acessar a tabela particionada horizontalmente de hello "mytable" como se fosse uma tabela local. Banco de dados SQL do Azure automaticamente abre várias conexões paralela toohello bancos de dados remotos em que tabelas Olá são armazenadas fisicamente, processa as solicitações de saudação em bancos de dados remotos hello e retorna resultados de saudação.
Obter mais informações sobre Olá etapas necessárias para o cenário de particionamento horizontal Olá pode ser encontrado em [consulta elástica para particionamento horizontal](sql-database-elastic-query-horizontal-partitioning.md).

toobegin de codificação, consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>Consultas T-SQL
Depois que você tiver definido suas fontes de dados externas e tabelas externas, você pode usar regulares do SQL Server conexão cadeias de caracteres tooconnect toohello bancos de dados em que você definiu as tabelas externas. Você pode executar instruções T-SQL em tabelas externas em que a conexão com limitações Olá descritas abaixo. Você pode encontrar mais informações e exemplos de consultas T-SQL nos tópicos da documentação de saudação para [particionamento horizontal](sql-database-elastic-query-horizontal-partitioning.md) e [particionamento vertical](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Conectividade de ferramentas
Você pode usar tooconnect regular de cadeias de caracteres de conexão do SQL Server, seus aplicativos e dados ou BI toodatabases ferramentas integração que têm tabelas externas. Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta. Uma vez conectado, consulte toohello consulta Elástico banco de dados e hello tabelas externas no banco de dados exatamente como você faria com qualquer outro banco de dados do SQL Server que você se conecte toowith sua ferramenta.

> [!IMPORTANT]
> Atualmente não há suporte para a autenticação usando o Azure Active Directory com consultas elásticas.
> 
> 

## <a name="cost"></a>Custo
Consulta elástica está incluída no custo de saudação de bancos de dados do SQL Azure. Observe que há suporte para topologias onde seus bancos de dados remotos estão em um data center diferente de Olá ponto de extremidade de consulta Elástico, mas saída de dados de bancos de dados remotos são cobrados regular [taxas do Azure](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Limitações de visualização
* Executando a primeira consulta elástica pode demorar até tooa alguns minutos na camada de desempenho padrão hello. Esse tempo é funcionalidade de consulta Elástico de saudação tooload necessário; melhora o desempenho do carregamento com níveis mais altos de desempenho.
* Ainda não há suporte para scripts de fontes de dados externas ou de tabelas externas do SSMS ou SSDT.
* A Importação/Exportação do Banco de Dados SQL ainda não dá suporte a tabelas externas e fontes de dados externas. Se você precisar toouse importação/exportação, remover esses objetos antes de exportar e, em seguida, recriá-los após a importação.
* Elástica consulta atualmente suporta apenas tabelas de tooexternal acesso somente leitura. No entanto, você pode usar a funcionalidade completa do T-SQL no banco de dados de saudação onde a tabela externa Olá é definida. Isso pode ser útil para, por exemplo, manter os resultados temporários usando, por exemplo, selecione < column_list > em < local_table > ou toodefine procedimentos armazenados no banco de dados de consulta Elástico de saudação que se referem a tabelas tooexternal.
* Exceto nvarchar(max), não há suporte para tipos LOB em definições de tabela externa. Como alternativa, você pode criar um modo de exibição no banco de dados remoto do hello que converte o tipo LOB Olá em nvarchar (max), definir sua tabela externa Olá exibição em vez de tabela base hello e convertido no tipo original de LOB Olá em suas consultas.
* Atualmente, não há suporte para estatísticas de coluna em tabelas externas. Estatísticas de tabelas têm suporte, mas precisam toobe criado manualmente.

## <a name="feedback"></a>Comentários
Compartilhe os comentários sobre sua experiência com consultas Elásticos em Disqus abaixo, fóruns do MSDN hello, ou em Stackoverflow. Estamos interessados em todos os tipos de comentários sobre o serviço de saudação (defeitos, bordas irregulares, intervalos de recurso).

## <a name="next-steps"></a>Próximas etapas

* Para obter um tutorial sobre particionamento vertical, consulte [Introdução à consulta entre bancos de dados (particionamento vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Para sintaxe e amostras de consultas para dados particionados verticalmente, consulte [Consultando dados particionados verticalmente)](sql-database-elastic-query-vertical-partitioning.md)
* Para um tutorial sobre particionamento horizontal (fragmentação), consulte [Introdução à consulta elástica para particionamento horizontal (fragmentação)](sql-database-elastic-query-getting-started.md).
* Para sintaxe e amostras de consultas para dados particionados horizontalmente, consulte [Consultando dados particionados horizontalmente)](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para um procedimento armazenado que executa uma instrução Transact-SQL em um único Banco de Dados SQL do Azure remoto ou um conjunto de bancos de dados que serve como fragmentos em um esquema de particionamento horizontal.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
