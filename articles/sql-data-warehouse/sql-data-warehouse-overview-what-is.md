---
title: "aaaWhat é o Azure SQL Data Warehouse? | Microsoft Docs"
description: "Banco de dados distribuído de nível corporativo com capacidade de processar volumes de petabytes de dados relacionais e não relacionais. É primeiro nuvem do data warehouse do setor Olá com expansão, diminuir e pausar em segundos."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>O que é o SQL Data Warehouse do Azure?
O SQL Data Warehouse do Azure é um banco de dados relacional, baseado em nuvem, expansível e de processamento paralelo massivo com capacidade de processar volumes imensos de dados. 

SQL Data Warehouse:

* Combina o banco de dados relacional do SQL Server Olá com recursos de expansão de nuvem do Azure. 
* Separa o armazenamento da computação.
* Habilita o aumento, a diminuição, a pausa ou a continuação da computação. 
* Integra-se em Olá plataforma Windows Azure.
* Utiliza o SQL Server Transact-SQL (T-SQL) e ferramentas.
* Compatível com diversos requisitos legais e de segurança de negócios como SOC e ISO.

Este artigo descreve os principais recursos de saudação do SQL Data Warehouse.

## <a name="massively-parallel-processing-architecture"></a>Arquitetura de processamento paralelo maciço
SQL Data Warehouse é um sistema de banco de dados distribuído de processamento extremamente paralelo (MPP). Em segundo plano Olá, o SQL Data Warehouse se espalha seus dados em diversos armazenamento compartilhado nada e unidades de processamento. Olá dados são armazenados em uma camada de armazenamento localmente redundante Premium sobre quais nós de computação dinamicamente vinculados executam consultas. Usa SQL Data Warehouse que carrega um toorunning de abordagem "dividir e superar" e consultas complexas. As solicitações são recebidas por um nó de controle, otimizado para distribuição e, em seguida, passado tooCompute nós toodo seus trabalhos em paralelo.

Com computação e armazenamento separado, o SQL Data Warehouse pode:

* Aumentar ou reduzir o tamanho do armazenamento de forma independente à computação.
* Aumentar ou reduzir o poder da computação sem mover dados.
* Pausar a capacidade de computação deixando os dados intactos, pagando somente o armazenamento.
* Retomar a capacidade de computação durante horas operacionais.

Olá diagrama a seguir mostra a arquitetura de saudação em mais detalhes.

![Arquitetura do SQL Data Warehouse][1]

**Nó de controle:** nó de controle Olá gerencia e otimiza a consultas. É Olá front-end que interage com todas as conexões e aplicativos. No SQL Data Warehouse, nó de controle de saudação é alimentado por banco de dados SQL e conectar tooit parece e funcionalidades Olá mesmo. Na superfície de hello, nó de controle Olá coordena todas as a movimentação de dados hello e computação necessária toorun de consultas paralelas em seus dados distribuídos. Quando você envia um tooSQL de consulta T-SQL Data Warehouse, o nó de controle Olá a transforma em consultas separadas que são executados em cada nó de computação em paralelo.

**Nós de computação:** nós de computação Olá servem como power Olá por trás do SQL Data Warehouse. Eles são Bancos de Dados SQL que armazenam seus dados e processam sua consulta. Quando você adiciona dados, o SQL Data Warehouse distribui nós de computação Olá linhas tooyour. nós de computação Olá são operadores de saudação que executam consultas paralelas Olá em seus dados. Após o processamento, eles passam de nó de controle de backup toohello Olá resultados. consulta de saudação toofinish, nó de controle Olá agrega os resultados de saudação e retorna Olá resultado final.

**Armazenamento:** os dados são armazenados no Armazenamento de Blobs do Azure. Quando nós de computação interagem com seus dados, eles gravam e leem tooand diretamente do armazenamento de blob. Como o armazenamento do Azure expande transparente e muito, o SQL Data Warehouse pode fazer Olá mesmo. Como a computação e o armazenamento são independentes, o SQL Data Warehouse pode expandir automaticamente o armazenamento, separadamente da expansão da computação, e vice-versa. Armazenamento de BLOBs do Azure também é totalmente tolerante a falhas, e simplifica Olá backup e restauração de processo.

**Serviço de movimentação de dados:** serviço de movimentação de dados (DMS) move dados entre os nós de saudação. DMS fornece nós de computação de saudação acesso toodata que eles precisam para junções e agregações. DMS não é um serviço do Azure. É um serviço do Windows que é executado com o banco de dados SQL em todos os nós de saudação. DMS é um processo em segundo plano com o qual não é possível interagir diretamente. No entanto, você pode examinar planos de consulta toosee quando operações de DMS ocorrem, como a movimentação de dados é necessário toorun cada consulta em paralelo.

## <a name="optimized-for-data-warehouse-workloads"></a>Otimizado para cargas de trabalho do data warehouse
Olá abordagem MPP é facilitada por várias otimizações de data warehouse específicas de desempenho, incluindo:

* Um otimizador de consulta distribuída e um conjunto de estatísticas complexas em todos os dados. Usando informações sobre a distribuição e o tamanho dos dados, o serviço de saudação é toooptimize capaz de consultas por avaliar o custo de saudação de operações de consulta distribuída específico.
* Técnicas e algoritmos avançados integrados em dados saudação movimentação processo tooefficiently mover dados entre os recursos de computação como consulta de saudação tooperform necessário. Essas operações de movimentação de dados são criadas e todas as otimizações toohello serviço de movimentação de dados ocorre automaticamente.
* Índices **columnstore** clusterizados por padrão. Usando armazenamento baseado em coluna, o SQL Data Warehouse obtém ganhos de compactação em média 5 x sobre o armazenamento tradicional orientado por linha e backup too10x ou mais ganhos de desempenho de consulta. Consultas de análise que precisa tooscan um grande número de linhas funciona melhor com índices columnstore.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Desempenho previsível e dimensionável com Unidades de Data Warehouse
O SQL Data Warehouse é criado com tecnologias semelhantes às do Banco de Dados SQL, que significa que os usuários podem esperar um desempenho consistente e previsível para consultas analíticas. Os usuários devem ter escala de desempenho toosee linearmente quando adicionam ou subtrair nós de computação. Alocação de recursos tooyour SQL Data Warehouse é medida em unidades de dados do Warehouse (DWUs). DWUs são uma medida de recursos subjacentes, como CPU, memória, IOPS, que são alocados tooyour SQL Data Warehouse. Aumentar o número de saudação do DWUs aumenta o desempenho e recursos. Especificamente, as DWUs ajudam a garantir que:

* Você está tooscale capaz de seu data warehouse sem se preocupar em software ou hardware subjacente hello.
* Você pode prever o aperfeiçoamento de desempenho para um nível DWU antes de alterar a computação de saudação do data warehouse.
* Olá subjacente de hardware e software da sua instância podem alterar ou mover sem afetar o desempenho da carga de trabalho.
* Olá subjacente a arquitetura do serviço de saudação sem afetar o desempenho de saudação da carga de trabalho pode melhorar o Microsoft.
* Microsoft rapidamente pode melhorar o desempenho no SQL Data Warehouse, de forma que seja escalável e uniformemente efeitos Olá sistema.

As Unidades de Data Warehouse fornecem uma medida de três métricas altamente correlacionadas ao desempenho da carga de trabalho do Data Warehouse. a seguir Olá chave escala de métricas de carga de trabalho linearmente com hello DWUs.

**Verificação/Agregação:** uma consulta de Data Warehouse padrão que verifica um grande número de linhas e, em seguida, executa uma agregação complexa. Essa é uma operação que exige bastante E/S e CPU.

**Carregamento:** Olá dados de tooingest de capacidade para o serviço de saudação. As cargas são realizadas da melhor forma com o PolyBase no Azure Storage Blobs ou Azure Data Lake. Essa métrica é a rede toostress projetado e aspectos de CPU do serviço de saudação.

**Criar tabela como Select (CTAS):** CTAS mede Olá capacidade toocopy uma tabela. Isso envolve a leitura de dados de armazenamento, distribuí-lo em nós de saudação do dispositivo hello e gravar toostorage novamente. É uma operação com uso intenso de CPU, rede e E/S.

## <a name="built-on-sql-server"></a>Desenvolvido a partir do SQL Server
SQL Data Warehouse é baseado no mecanismo de banco de dados relacional do SQL Server hello e inclui muitos dos recursos de saudação esperado de um data warehouse corporativo. Se você já souber o T-SQL, é fácil tootransfer tooSQL seu conhecimento do Data Warehouse. Se avançados ou apenas começando, exemplos de saudação em documentação Olá ajudam a começar. Em geral, você pode pensar sobre maneira Olá que nós já construída elementos de linguagem de saudação do SQL Data Warehouse da seguinte maneira:

* O SQL Data Warehouse usa a sintaxe do T-SQL para várias operações. Ele também oferece suporte a um amplo conjunto de construtores SQL tradicionais, como procedimentos armazenados, funções definidas pelo usuário, particionamento de tabelas, índices e agrupamentos.
* O SQL Data Warehouse também contém vários recursos recentes do SQL Server, incluindo índices **columnstore** clusterizados, integração de PolyBase e auditoria de dados (completo com avaliação de ameaças).
* Determinados elementos de linguagem T-SQL que são menos comuns para data warehouse cargas de trabalho, ou que são mais recente tooSQL Server, podem não estar disponíveis no momento. Para obter mais informações, consulte Olá [documentação de migração][Migration documentation].

Com hello Transact-SQL e associação de recurso entre Analytics Platform System, banco de dados SQL, SQL Data Warehouse e SQL Server, você pode desenvolver uma solução que atenda às suas necessidades de dados. Você pode decidir onde tookeep seus dados, com base no desempenho, segurança e requisitos de escala e, em seguida, transferir os dados conforme necessário entre sistemas diferentes.

## <a name="data-protection"></a>Proteção de dados
O SQL Data Warehouse armazena todos os dados no armazenamento com redundância local do Azure Premium. Várias cópias síncronas de dados saudação são mantidas no hello local tooguarantee transparente de dados proteção de dados contra falhas localizadas. Além disso, o SQL Data Warehouse faz o backup automaticamente dos bancos de dados ativos (sem pausa) em intervalos regulares usando Instantâneos de Armazenamento do Azure. toolearn mais informações sobre como fazer backup e restaurar funciona, consulte Olá [visão geral de Backup e restauração][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Integrado com as ferramentas da Microsoft
SQL Data Warehouse também integra a muitas das ferramentas de saudação que os usuários podem estar familiarizados com o SQL Server. Essas ferramentas incluem:

**Ferramentas tradicionais do SQL Server:** o SQL Data Warehouse é totalmente integrado ao SQL Server Analysis Services, aos serviços de integração e de relatório.


            **Ferramentas baseadas em nuvem:** o SQL Data Warehouse pode ser integrado com vários serviços no Azure, incluindo o Data Factory, o Stream Analytics, o Machine Learning e o Power BI. Para obter uma lista mais completa, confira [Visão geral das ferramentas integradas][Integrated tools overview].

**Ferramentas de terceiros:** vários provedores de ferramenta de terceiros têm integração certificada de suas ferramentas com o SQL Data Warehouse. Para obter uma lista completa, veja [Parceiros de solução do SQL Data Warehouse][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Cenários de fontes de dados híbridos
O Polybase permite que você tooleverage seus dados de origens diferentes usando os comandos conhecidos do T-SQL. O Polybase permite que você tooquery dados não relacionais mantidos no armazenamento de BLOBs do Azure, como se fosse uma tabela normal. Use tooquery dados não relacionais ou dados não relacionais tooimport no SQL Data Warehouse.

* PolyBase usa dados não relacionais de tooaccess tabelas externas. definições de tabela Olá são armazenadas no Data Warehouse do SQL e você pode acessá-los usando o SQL e ferramentas que você acessa dados relacionais normais.
* O Polybase não depende de sua integração. Ela expõe Olá os mesmos recursos e fontes de saudação de tooall de funcionalidade que ele suporta. dados de saudação lidos pelo Polybase podem ser em vários formatos, incluindo arquivos delimitados ou ORC.
* PolyBase pode ser usado tooaccess armazenamento de blob que também está sendo usado como armazenamento para um cluster HDInsight. Isso dá a você acessar toohello mesmo dados com ferramentas relacionais e não relacionais.

## <a name="sla"></a>Contrato de Nível de Serviço
O SQL Data Warehouse oferece um SLA (Contrato de Nível de Serviço) no nível do produto como parte do SLA do Microsoft Online Services. Para saber mais, visite [SLA para o SQL Data Warehouse][SLA for SQL Data Warehouse]. Para obter informações de SLA sobre todos os outros produtos, você pode visitar Olá [contratos de nível de serviço] Azure página ou baixá-los em Olá [licenciamento por Volume] [ Volume Licensing] página. 

## <a name="next-steps"></a>Próximas etapas
Agora que você conheça um pouco sobre o SQL Data Warehouse, saiba como tooquickly [criar um SQL Data Warehouse] [ create a SQL Data Warehouse] e [carregar dados de amostra][load sample data]. Se você for novo tooAzure, você pode achar Olá [Glossário do Azure] [ Azure glossary] úteis à medida que encontrar terminologia nova. Ou, dê uma olhada em alguns desses outros Recursos do SQL Data Warehouse.  

* [Histórias de sucesso de clientes]
* [Blogs]
* [Solicitações de recursos]
* [Vídeos]
* [Blogs da Equipe Consultoria para Clientes]
* [Criar um tíquete de suporte]
* [Fórum do MSDN]
* [Fórum Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Criar um tíquete de suporte]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Histórias de sucesso de clientes]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs da Equipe Consultoria para Clientes]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Solicitações de recursos]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Fórum do MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Fórum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[contratos de nível de serviço]: https://azure.microsoft.com/en-us/support/legal/sla/
