---
title: aaaScaling-out com o banco de dados do SQL Azure | Microsoft Docs
description: "Software como um desenvolvedor de serviço (SaaS) pode criar facilmente Elástico, bancos de dados escalonáveis hello usando essas ferramentas de nuvem"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Escalando horizontalmente com o Banco de Dados SQL do Azure
Você pode expandir facilmente bancos de dados do SQL Azure usando Olá **banco de dados Elástico** ferramentas. Essas ferramentas e recursos permitem que você use Olá praticamente ilimitada recursos de banco de dados **banco de dados do SQL Azure** soluções toocreate para cargas de trabalho transacionais e especialmente Software como um aplicativo de serviço (SaaS). Recursos de banco de dados Elásticos são compostos de seguir hello:

* [Biblioteca de cliente de banco de dados elástica](sql-database-elastic-database-client-library.md): biblioteca de saudação do cliente é um recurso que permite que você toocreate e manter bancos de dados fragmentados.  Consulte [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).
* [Ferramenta de mesclagem/divisão do Banco de Dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md): move dados entre bancos de dados fragmentados. Isso é útil para mover dados de um multilocatário banco de dados tooa único locatário banco de dados (ou vice-versa). Consulte [Tutorial de ferramenta da Divisão de Mesclagem do Banco de Dados Elástico](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Trabalhos do banco de dados Elásticos](sql-database-elastic-jobs-overview.md) (visualização): Use trabalhos toomanage grandes números de bancos de dados do SQL Azure. Execute operações administrativas facilmente, alterações de esquema, gerenciamento de credenciais, atualizações de dados de referência, desempenho de coleta de dados ou coleção de telemetria do locatário (cliente), usando trabalhos.
* [Consulta de banco de dados elástica](sql-database-elastic-query-overview.md) (visualização): permite que você consulta toorun um Transact-SQL que abrange vários bancos de dados. Isso permite que ferramentas de tooreporting de conexão, como Excel, Power BI, Tableau, etc.
* [Transações Elásticos](sql-database-elastic-transactions-overview.md): este recurso permite que você toorun transações que abrangem vários bancos de dados no banco de dados do SQL Azure. Transações de banco de dados Elástico estão disponíveis para aplicativos .NET usando o ADO .NET e integrar com experiência programação familiar hello usando Olá [classes Transaction](https://msdn.microsoft.com/library/system.transactions.aspx).

gráfico de saudação abaixo mostra uma arquitetura que inclui Olá **recursos de banco de dados Elástico** na coleção de tooa de relação de bancos de dados.

Neste gráfico, as cores de banco de dados de saudação representam esquemas. Bancos de dados com hello mesmo compartilhamento de cor Olá mesmo esquema.

1. Um conjunto de **bancos de dados SQL do Azure** é hospedado no Azure usando a arquitetura de fragmentação.
2. Olá **biblioteca de cliente do banco de dados Elástico** é definido toomanage usado um fragmento.
3. Um subconjunto de bancos de dados de saudação são colocados em um **pool Elástico**. (Consulte [O que é um pool?](sql-database-elastic-pool.md)).
4. Um **trabalho de Banco de Dados Elástico** executa scripts T-SQL agendados ou ad-hoc em todos os bancos de dados.
5. Olá **ferramenta de mesclagem de divisão** toomove usados são dados de um fragmento tooanother.
6. Olá **consulta de banco de dados Elástico** permite que você toowrite uma consulta que abrange todos os bancos de dados no conjunto de fragmentos de saudação.
7. **Transações Elásticos** permite que você toorun transações que abrangem vários bancos de dados. 

![Ferramentas de Banco de Dados Elástico][1]

## <a name="why-use-hello-tools"></a>Por que usar ferramentas Olá?
Obter elasticidade e escalonamento para aplicativos em nuvem foi fácil para armazenamento de blobs e VMs – basta adicionar ou subtrair unidades ou aumentar a potência. Mas continuou sendo um desafio para processamento de dados com estado em bancos de dados relacionais. Desafios surgiram nesses cenários:

* Ampliando e reduzindo a capacidade para parte do banco de dados relacional de saudação da carga de trabalho.
* Gerenciar hotspots que podem surgir afetando um subconjunto específico de dados, como cliente final especialmente movimentado (locatário).

Tradicionalmente, cenários como eles foram resolvidos investindo no aplicativo do banco de dados de grande escala servidores toosupport hello. No entanto, essa opção é limitada em nuvem Olá em que todo o processamento ocorre em hardware de mercadoria predefinidos. Em vez disso, distribuição de dados e processamento em vários bancos de dados estruturado de forma idêntica (um padrão de expansão conhecido como "fragmentação") fornece uma alternativa tootraditional abordagens de expansão em termos de custo e resiliência.

## <a name="horizontal-and-vertical-scaling"></a>Dimensionamento horizontal e vertical
Olá figura a seguir mostra a saudação dimensões horizontais e verticais do dimensionamento, que são formas básicas de saudação bancos de dados Elástico Olá podem ser expandidos.

![Escala horizontal versus vertical][2]

Escalonamento horizontal refere-se tooadding ou remover bancos de dados na capacidade de tooadjust de ordem ou o desempenho geral. Isso também é chamado de “escalar horizontalmente”. A fragmentação, no qual os dados são particionados em um conjunto de bancos de dados estruturados de forma idêntica, é um tooimplement de maneira comum horizontal dimensionamento.  

Dimensionamento vertical refere-se tooincreasing ou diminuir o nível de desempenho de saudação de um banco de dados individual, isso também é conhecido como "até".

A maioria dos aplicativos de banco de dados de escala de nuvem usará uma combinação dessas duas estratégias. Por exemplo, um Software como um aplicativo de serviço pode usar horizontal dimensionamento tooprovision novos clientes finais e vertical dimensionamento tooallow do cada-cliente final banco de dados toogrow ou redução recursos conforme necessário por cargas de trabalho de saudação.

* Escalonamento horizontal é gerenciada usando Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md).
* A expansão vertical é feita usando a camada de serviço saudação do toochange de cmdlets do PowerShell do Azure, ou colocando os bancos de dados em um pool Elástico.

## <a name="sharding"></a>Fragmentação
*Fragmentação* é uma técnica toodistribute grandes quantidades de dados estruturado de forma idêntica em vários bancos de dados independentes. É especialmente popular com desenvolvedores de nuvem que estão criando ofertas de SaaS (software como serviço) para clientes finais ou empresas. Esses clientes finais costumam ser chamados tooas "locatários". Fragmentação pode ser necessária por vários motivos:  

* quantidade total de saudação de dados é muito grande toofit dentro das restrições de saudação de um único banco de dados
* taxa de transferência de transações de saudação do hello carga de trabalho geral excede recursos de saudação de um único banco de dados
* Inquilinos podem exigir isolamento físico entre si, para que bancos de dados separados são necessários para cada locatário
* Seções diferentes de um banco de dados podem precisar tooreside em regiões diferentes para questões geopolíticas, de desempenho ou de conformidade.

Em outros cenários, como a inclusão de dados de dispositivos distribuídos, fragmentação pode ser usado toofill um conjunto de bancos de dados que são organizados temporariamente. Por exemplo, um banco de dados pode ser dedicado tooeach dia ou semana. Nesse caso, a chave de fragmentação Olá pode ser um inteiro representando hello (presente em todas as linhas de tabelas fragmentadas Olá) e consultas para recuperar informações de um intervalo de datas devem ser roteadas por toohello subconjunto aplicativo hello bancos de dados que abrangem o intervalo de saudação em pergunta.

Fragmentação funciona melhor quando todas as transações em um aplicativo podem ser restrito tooa único valor de uma chave de fragmentação. Isso garante que todas as transações serão tooa local de banco de dados específico.

## <a name="multi-tenant-and-single-tenant"></a>Multilocatário e único locatário
Alguns aplicativos usam a abordagem mais simples de saudação de criação de um banco de dados separado para cada locatário. Isso é hello **padrão de fragmentação de locatário único** que fornece isolamento, capacidade de backup/restauração e recurso de dimensionamento na granularidade de saudação do locatário hello. Com a fragmentação de locatário único, cada banco de dados está associado um valor de ID de locatário específico (ou valor de chave de cliente), mas essa chave não deve sempre estar presente em dados Olá em si. Tooroute de responsabilidade do aplicativo é Olá cada solicitação toohello banco de dados apropriado - e biblioteca de saudação do cliente pode simplificar isso.

![Único locatário versus multilocatários][4]

Outros cenários de vários locatários pack juntos em bancos de dados, em vez de isolá-los em bancos de dados separados. Isso é típico **padrão de fragmentação de multilocatário** - e pode ser orientada pelo fato Olá que um aplicativo gerencia grandes números de locatários muito pequenos. Na fragmentação de multilocatária, linhas de saudação em tabelas de banco de dados de saudação são projetados toocarry uma chave que identifica a chave de identificação ou fragmentação de locatário hello. Novamente, camada de aplicativo hello é responsável pelo roteamento solicitação toohello banco de dados apropriado do locatário, e isso pode ser compatível com a biblioteca de cliente do banco de dados Elástico Olá. Além disso, a segurança em nível de linha pode ser usado toofilter quais linhas de cada locatário pode acessar - para obter detalhes, consulte [aplicativos multilocatários com segurança em nível de linha e ferramentas de banco de dados Elástico](sql-database-elastic-tools-multi-tenant-row-level-security.md). Redistribuir dados entre bancos de dados pode ser necessários com padrão de fragmentação de multilocatário hello e isso é facilitado pela ferramenta de mesclagem de divisão de banco de dados Elástico hello. toolearn mais informações sobre padrões de design para aplicativos SaaS usando pools Elásticos, consulte [padrões de Design para aplicativos de SaaS multilocatário com o Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Mover dados de vários bancos de dados de aluguel toosingle
Ao criar um aplicativo SaaS, é clientes potenciais típico toooffer uma versão de avaliação do hello software. Nesse caso, é econômico toouse um banco de dados multilocatário para dados de saudação. No entanto, quando um cliente em potencial se torna um cliente, um banco de dados de um único locatário é melhor, já que fornece maior desempenho. Se o cliente Olá criado dados durante o período de avaliação Olá, usar Olá [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md) toomove dados Olá Olá multilocatário toohello novo locatário único banco de dados.

## <a name="next-steps"></a>Próximas etapas
Para um aplicativo de exemplo que demonstra a biblioteca de saudação do cliente, consulte [Introdução às ferramentas Elástico Datababase](sql-database-elastic-scale-get-started.md).

tooconvert existente toouse ferramentas de saudação de bancos de dados, consulte [existente Migrar bancos de dados fora de tooscale](sql-database-elastic-convert-to-use-elastic-tools.md).

especificações de saudação toosee do pool Elástico do hello, consulte [considerações de preço e desempenho para um pool Elástico](sql-database-elastic-pool.md), ou criar um novo pool com [pools Elásticos](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

