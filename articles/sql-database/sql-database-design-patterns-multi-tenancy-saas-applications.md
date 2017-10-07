---
title: "padrões de aaaDesign para aplicativos SaaS de multilocatários e de banco de dados do SQL Azure | Microsoft Docs"
description: "Este artigo discute os requisitos de saudação e padrões comuns de arquitetura de dados de aplicativos de banco de dados multilocatário em execução em um ambiente de nuvem precisam tooconsider e Olá compensações vários associadas com esses padrões. Ele também explica como o Banco de Dados SQL do Azure com seus pools elásticos e suas ferramentas elásticas ajudam a atender a esses requisitos sem comprometimento."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Padrões de design para aplicativos SaaS multilocatários e o Banco de Dados SQL do Azure
Neste artigo, você pode aprender sobre os requisitos de saudação e padrões comuns de arquitetura de dados do software de vários locatários como aplicativos de banco de dados um serviço (SaaS) que são executados em um ambiente de nuvem. Ele também explica os fatores de Olá necessário tooconsider e Olá vantagens e desvantagens dos padrões de design diferentes. O pool elástico e as ferramentas elásticas no Banco de Dados SQL podem ajudar você a atender os requisitos específicos sem comprometer outros objetivos.

Às vezes, os desenvolvedores fazem escolhas que trabalham em seus interesses a longo prazo quando criam modelos de aluguel para as camadas de dados de saudação de aplicativos de multilocação. Inicialmente, pelo menos, um desenvolvedor pode perceber facilidade de desenvolvimento e reduzir custos de provedor de serviço de nuvem como o mais importante do que a escalabilidade de isolamento ou saudação do locatário de um aplicativo. Essa opção pode ocasionar preocupações de satisfação toocustomer uma correção de curso cara mais tarde.

Um aplicativo multilocatário é um aplicativo hospedado em um ambiente de nuvem e que fornece Olá mesmo conjunto de serviços toohundreds ou milhares de locatários que não compartilham ou ver dados uns dos outros. Um exemplo é um aplicativo SaaS que fornece serviços tootenants em um ambiente hospedado na nuvem.

## <a name="multi-tenant-applications"></a>Aplicativos multilocatários
Em aplicativos multilocatários, os dados e a carga de trabalho podem ser facilmente particionados. Você pode particionar dados e carga de trabalho, por exemplo, com limites de locatário, porque a maioria das solicitações ocorrem dentro dos limites de saudação de um locatário. Essa propriedade é inerente em dados saudação e carga de trabalho hello e ele favorece padrões de aplicativo hello discutidos neste artigo.

Os desenvolvedores usam esse tipo de aplicativo em todo o espectro de aplicativos baseados em nuvem, incluindo hello:

* Aplicativos de banco de dados do parceiro que estão sendo toohello transição de nuvem como aplicativos SaaS
* Aplicativos SaaS criados para a nuvem de saudação do hello o plano de
* Aplicativos diretos voltados para o cliente
* Aplicativos empresariais voltados para funcionários

Aplicativos SaaS que são projetados para nuvem hello e aqueles com raízes como aplicativos de banco de dados do parceiro normalmente são aplicativos de vários locatários. Esses aplicativos SaaS entregam um aplicativo especializado como um locatários tootheir de serviço. Locatários podem acessar o serviço de aplicativo hello e ter propriedade completa dos dados associados armazenados como parte do aplicativo hello. Mas tootake proveito dos benefícios de saudação do SaaS, locatários deve devolvê-algum controle sobre seus próprios dados. Elas têm confiança tookeep de provedor de serviço de SaaS Olá seus dados isolados dos dados de outros locatários e seguros. MYOB, SnelStart e Salesforce.com são exemplos desse tipo de aplicativo SaaS multilocatário. Cada um desses aplicativos pode ser particionada em limites de locatário e padrões de design de aplicativo hello suporte que discutimos neste artigo.

Os aplicativos que fornecem um serviço direto toocustomers ou tooemployees dentro de uma organização (geralmente chamados tooas usuários, em vez de locatários) são outra categoria no espectro de aplicativo multilocatário hello. Os clientes assinar o serviço de toohello e não possuem dados Olá Olá provedor de serviços de coletam e armazenam. Provedores de serviços têm menos rigorosa tookeep de requisitos isolados uns dos outros além regulamentos governamentais privacidade de dados de seus clientes. Exemplos desse tipo de aplicativo multilocatário voltado para o cliente são provedores de conteúdo de mídia como Netflix, Spotify e Xbox LIVE. Outros exemplos de aplicativos facilmente particionáveis são aplicativos de escala da Internet voltados para clientes ou aplicativos IoT (Internet das Coisas) em que cada cliente ou dispositivo pode servir como uma partição. Limites de partição podem separar usuários e dispositivos.

Nem todos os aplicativos são particionados facilmente com uma única propriedade, como o locatário, cliente, usuário ou dispositivo. Um aplicativo de ERP (planejamento de recursos da empresa) complexo, por exemplo, tem produtos, pedidos e clientes. Ele normalmente tem um esquema complexo com milhares de tabelas altamente interconectadas.

Nenhuma estratégia de partição única pode aplicar tabelas tooall e funcionam em cargas de trabalho do aplicativo. Este artigo se concentra em aplicativos multilocatários que possuem dados e cargas de trabalho facilmente particionáveis.

## <a name="multi-tenant-application-design-trade-offs"></a>Compensações do design de aplicativo multilocatário
padrão de design de saudação que um desenvolvedor de aplicativos de multilocação escolhe normalmente é baseado em uma consideração de saudação fatores a seguir:

* **Isolamento de locatário**. desenvolvedor de saudação precisa tooensure que nenhum locatário tem dados de locatários de tooother acesso não desejado. requisito de isolamento Olá estende tooother propriedades, como fornecer proteção de vizinhos ruídos, sendo toorestore capaz de dados de um locatário e implementar as personalizações de específico de locatário.
* **Custo de recursos de nuvem**. Um aplicativo de SaaS precisa toobe custo competitivas. Um desenvolvedor de aplicativos de multilocação pode escolha toooptimize para reduzir o custo em uso de saudação de recursos de nuvem, como o armazenamento e os custos de computação.
* **Facilidade de Operações de Desenvolvimento**. Um desenvolvedor de aplicativos de multilocação precisa tooincorporate proteção de isolamento, manter e monitorar a integridade de saudação do seu aplicativo e o esquema de banco de dados e solucionar problemas de locatário. Complexidade no desenvolvimento de aplicativos e operação diretamente converte tooincreased custo e desafios de satisfação do locatário.
* **Escalabilidade**. Olá capacidade tooincrementally adicionar mais capacidade para locatários que exigem é imperativo tooa operação de SaaS com êxito e locatários.

Cada um desses fatores tem vantagens e desvantagens em comparação com tooanother. nuvem de menor custo Olá podem não oferecer a experiência de desenvolvimento mais conveniente de saudação da oferta. É importante para um desenvolvedor toomake informado opções sobre essas opções e suas vantagens e desvantagens durante o processo de design de aplicativo hello.

Um padrão de populares de desenvolvimento é toopack vários locatários em um ou alguns bancos de dados. Olá benefícios dessa abordagem são um custo menor porque você paga por alguns bancos de dados e relativa simplicidade Olá de trabalhar com um número limitado de bancos de dados. No entanto, ao longo do tempo, um desenvolvedor de aplicativo SaaS multilocatário perceberá que essa opção tem desvantagens significativas no isolamento de locatários e na escalabilidade. Se o isolamento de locatários se torna importante, esforço adicional é necessário tooprotect locatário dados no armazenamento compartilhado contra acesso não autorizado ou vizinhos com ruídos. Esse esforço adicional pode aumentar significativamente os esforços de desenvolvimento e os custos de manutenção do isolamento. Da mesma forma, se for necessário adicionando locatários, esse padrão de design normalmente requer dados de conhecimento do locatário tooredistribute pela camada de dados de saudação do bancos de dados tooproperly escala de um aplicativo.  

Isolamento de locatários geralmente é um requisito fundamental em aplicativos SaaS de vários locatários que atendem toobusinesses e organizações. Os desenvolvedores podem ser tentados para as vantagens percebidas em relação a simplicidade e o custo sobre o isolamento de locatários e a escalabilidade. Essa compensação pode ser complexas e caras que serviço Olá cresce e os requisitos de isolamento de locatário se tornam mais importantes e gerenciado na camada de aplicativo hello. No entanto, em aplicativos de vários locatários que fornecem um serviço voltado ao consumidor direto toocustomers, isolamento de locatários pode ser uma prioridade inferior a otimização para o custo de recursos de nuvem.

## <a name="multi-tenant-data-models"></a>Modelos de dados de multilocatário
Práticas de design comuns para a colocação de dados de locatário seguem esses três modelos distintos, mostrados na Figura 1.

![Modelos de dados de aplicativo multilocatário](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Figura 1: Práticas comuns de design para modelos de dados de multilocatário

* **Banco de dados por locatário**. Cada locatário tem seu próprio banco de dados. Todos os dados específicos de locatário é o banco de dados do locatário toohello restrita e isolado de outros locatários e seus dados.
* **Banco de dados fragmentados compartilhados**. Vários inquilinos compartilham um de vários bancos de dados. Um conjunto distinto de locatários recebe tooeach banco de dados usando uma estratégia de particionamento, como hash, o intervalo ou o particionamento de lista. Essa estratégia de distribuição de dados geralmente é chamado tooas fragmentação.
* **Banco de dados individuais compartilhados**. Um banco de dados único, às vezes grande, contém dados para todos os locatários, sem ambiguidade em uma coluna de ID de locatário.

> [!NOTE]
> Um desenvolvedor de aplicativos pode escolher tooplace locatários diferentes nos esquemas de banco de dados diferente e use Olá esquema nome toodisambiguate Olá diferentes locatários. Não recomendamos essa abordagem porque geralmente requer o uso de saudação de SQL dinâmico, e não pode ser eficaz em cache de plano. Restante Olá deste artigo, vamos nos concentrar na abordagem de tabela Olá compartilhado para essa categoria de aplicativo multilocatário.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Modelos populares de dados multilocatários
É importante tooevaluate Olá diferentes tipos de modelos de dados multilocatário em termos de saudação aplicativo desvantagens do design que nós identificamos. Esses fatores ajudam caracterizam Olá três modelos de dados de multilocatário mais comuns descritos anteriormente e o uso do banco de dados, conforme mostrado na Figura 2.

* **Isolamento**. o grau de isolamento entre locatários Olá pode ser uma medida de quanto isolamento de locatários alcança um modelo de dados.
* **Custo de recursos de nuvem**. quantidade de saudação do compartilhamento de recursos entre locatários pode otimizar o custo de recursos de nuvem. Um recurso pode ser definido como computação hello e custos de armazenamento.
* **Custo de Operações de Desenvolvimento**. facilidade de saudação do desenvolvimento de aplicativos, implantação e gerenciamento reduz o custo geral de operação de SaaS.  

Na Figura 2, eixo Y da saudação mostra o nível de saudação do isolamento de locatários. eixo X da saudação mostra o nível de saudação do compartilhamento de recursos. cinza Hello, diagonal seta no meio de saudação indica direção de saudação do DevOps custos, tende a tooincrease ou diminuir.

![Padrões populares do design de aplicativo multilocatário](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Figura 2: Modelos populares de dados multilocatários

Olá, quadrante inferior direito na Figura 2 mostra um padrão de aplicativo que usa um potencialmente grande compartilhado único banco de dados e Olá compartilhada tabela (ou um esquema separado) abordagem. É recomendável para porque todos os locatários usam Olá mesmos recursos (CPU, memória, entrada/saída) em um único banco de dados do banco de dados de compartilhamento de recursos. No entanto, o isolamento de locatários é limitado. Talvez seja necessário locatários do tootake etapas adicionais tooprotect uns dos outros na camada de aplicativo hello. Estas etapas adicionais podem aumentar significativamente o custo de DevOps Olá de desenvolvimento e gerenciamento de aplicativo hello. Escalabilidade é limitada pela escala de saudação do hardware Olá que hospeda o banco de dados de saudação.

quadrante inferior esquerdo de saudação na Figura 2 ilustra vários locatários fragmentados em vários bancos de dados (normalmente, um hardware diferente unidade de escala). Cada banco de dados hospeda um subconjunto de locatários, que soluciona Olá problema de escalabilidade de outros padrões. Se mais capacidade é necessária para mais de locatários, você pode colocar facilmente locatários Olá nos novos bancos de dados alocados toonew unidades de escala de hardware. No entanto, a quantidade de saudação do compartilhamento de recursos é reduzida. Somente para locatários colocados em Olá mesmo unidades de escala compartilham recursos. Essa abordagem fornece isolamento de tootenant de aperfeiçoamento pouco porque muitos locatários ainda são colocados sem sendo protegidos automaticamente contra ações uns dos outros. A complexidade do aplicativo permanece alta.

quadrante superior esquerdo de saudação na Figura 2 é abordagem terceira hello. Ela coloca cada dado de locatário em seu próprio banco de dados. Essa abordagem tem ótimas propriedades de isolamento de locatário, mas limita o compartilhamento de recursos quando cada banco de dados tem seus próprios recursos dedicados. Essa será uma abordagem boa se todos os locatários tiverem cargas de trabalho previsíveis. Se as cargas de trabalho de locatário se tornam menos previsíveis, provedor Olá não pode otimizar o compartilhamento de recursos. Falta de previsibilidade é comum para aplicativos SaaS. provedor de saudação ou deve ter um provisionamento toomeet demandas ou recursos inferiores. Qualquer ação resultará em custos mais elevados ou diminuirá a satisfação do locatário. Um grau maior de recursos de compartilhamento entre locatários se torna a solução de saudação toomake desejável mais econômica. Número crescente de saudação de bancos de dados também aumenta DevOps custo toodeploy e manter o aplicativo hello. Apesar dessas questões, esse método fornece isolamento de melhor e mais fácil de saudação para locatários.

Esses fatores influenciam também padrão de design de saudação que um cliente escolher:

* **Propriedade dos dados de locatário**. Um aplicativo no qual inquilinos mantém a propriedade de seus próprios dados favorece padrão de saudação de um único banco de dados por locatário.
* **Escala**. Um aplicativo que se destina a centenas de milhares ou milhões de locatários favorece abordagens de compartilhamento de banco de dados, como a fragmentação. Os requisitos de isolamento ainda podem apresentar desafios.
* **Modelo de negócios e valor**. Se a receita por locatário de um aplicativo for pequena (menos de um dólar), os requisitos de isolamento se tornarão menos essenciais e o banco de dados compartilhado fará sentido. Se a receita por locatário for de alguns dólares ou mais, um modelo de banco de dados por locatário será mais viável. Ele poderá ajudar a reduzir os custos de desenvolvimento.

Um modelo ideal de multilocatário dado Olá desvantagens do design mostradas na Figura 2, precisa de propriedades de isolamento de locatário bom tooincorporate com compartilhamento entre locatários ideal de recursos. Esse modelo se ajusta a categoria de saudação descrita no quadrante de superior direito da saudação da Figura 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Suporte a multilocação no Banco de Dados SQL do Azure
O Banco de Dados SQL do Azure oferece suporte a todos os padrões de aplicativos multilocatários descritos na Figura 2. Com pools Elásticos, ele também dá suporte a um padrão de aplicativo que combina o compartilhamento de recursos boa e benefícios de isolamento de saudação do banco de dados por locatário Olá abordagem (consulte quadrante de superior direito da saudação na Figura 3). Ferramentas de banco de dados Elástico e recursos no banco de dados SQL ajudam a reduzir Olá custo toodevelop e operar um aplicativo que tem muitos bancos de dados (mostrados na área de saudação sombreada na Figura 3). Essas ferramentas podem ajudá-lo a criar e gerenciar aplicativos que usam qualquer um dos padrões de vários bancos de dados de saudação.

![Padrões no Banco de Dados SQL Azure](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Figura 3: Padrões de aplicativos multilocatários no Banco de Dados SQL do Azure

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Modelo de banco de dados por locatário com ferramentas e pools elásticos
Pools Elásticos no banco de dados SQL combinam o isolamento de locatários com recurso de compartilhamento entre o método de banco de dados por locatário locatário bancos de dados toobetter suporte hello. O Banco de Dados SQL é uma solução de camada de dados para provedores de SaaS que compilam aplicativos multilocatários. sobrecarga de saudação do recurso de compartilhamento entre locatários desloca da camada de serviço Olá aplicativos camada toohello banco de dados. complexidade de saudação do gerenciamento e consultar em grande escala em bancos de dados é simplificada com trabalhos Elásticos, consulta elástica, transações Elásticos e biblioteca de cliente do banco de dados Elástico hello.

| Requisitos do aplicativo | Recursos de Banco de Dados SQL |
| --- | --- |
| Isolamento de locatários e compartilhamento de recursos |[Pools Elásticos](sql-database-elastic-pool.md): alocar um pool de recursos de banco de dados SQL e compartilhamento de recursos de saudação entre vários bancos de dados. Além disso, bancos de dados individuais podem extrair os mesmos recursos de pool de hello como picos de demanda de capacidade necessária tooaccommodate toochanges vencimento em cargas de trabalho de locatário. pool Elástico de saudação em si pode ser dimensionado para cima ou para baixo conforme necessário. Pools Elásticos também fornecem a facilidade de gerenciamento e monitoramento e solução de problemas no nível do pool de saudação. |
| Facilidade de DevOps em bancos de dados |[Pools elásticos](sql-database-elastic-pool.md): conforme mencionado anteriormente. |
| | [Consulta elástica:](sql-database-elastic-query-horizontal-partitioning.md)consulta relatórios ou análises entre locatários nos bancos de dados. |
| | [Trabalhos Elásticos](sql-database-elastic-jobs-overview.md): pacote e implantar com confiança as operações de manutenção de banco de dados ou bancos de dados toomultiple de alterações de esquema de banco de dados. |
| | [Transações Elásticos](sql-database-elastic-transactions-overview.md): processo tooseveral bancos de dados é alterado de forma atômica e isolada. Transações elásticas são necessárias quando os aplicativos precisam de garantias de "tudo ou nada" sobre várias operações de banco de dados. |
| | [Biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md): gerenciar as distribuições de dados e toodatabases de locatários do mapa. |

## <a name="shared-models"></a>Modelos compartilhados
Conforme descrito anteriormente, para a maioria dos provedores de SaaS, uma abordagem de modelo compartilhado pode apresentar problemas com questões de isolamento de locatário e complexidades de desenvolvimento e manutenção do aplicativo. No entanto, para aplicativos multilocatários que fornecem um serviço diretamente locatário tooconsumers, requisitos de isolamento podem não ser como uma prioridade alta como minimizar os custos. Eles podem ser toopack capaz de locatários em um ou mais bancos de dados em um custo de tooreduce de alta densidade. Os modelos de banco de dados compartilhados usando um banco de dados individual ou vários bancos de dados fragmentados podem resultar em uma eficiência adicional no compartilhamento de recursos e na redução do custo geral. Banco de dados SQL do Azure fornece isolamento de segurança aprimorada e gerenciamento em escala na camada de dados de saudação de compilação de alguns recursos que ajudam os clientes.

| Requisitos do aplicativo | Recursos de Banco de Dados SQL |
| --- | --- |
| Recursos de isolamento de segurança |[Segurança em nível de linha](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Esquema de banco de dados](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Facilidade de DevOps em bancos de dados |[Consulta elástica](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Trabalhos elásticos](sql-database-elastic-jobs-overview.md) |
| | [Transações elásticas](sql-database-elastic-transactions-overview.md) |
| | [Biblioteca de cliente do banco de dados elástico](sql-database-elastic-database-client-library.md) |
| | [Divisão e mesclagem do banco de dados elástico](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Resumo
Os requisitos de isolamento de locatário são importantes para a maioria dos aplicativos SaaS multilocatários. isolamento do Hello melhor opção tooprovide apresenta muito em direção à abordagem de banco de dados por locatário hello. Olá, outras duas abordagens requerem investimentos em camadas de aplicativos complexos que exigem isolamento tooprovide da equipe de desenvolvimento habilidoso, que aumenta consideravelmente o custo e o risco. Se os requisitos de isolamento não são contabilizados no início do desenvolvimento de serviço hello, aperfeiçoamento-los pode ser ainda mais caro em modelos de dois primeiros hello. principais desvantagens de saudação associadas ao modelo de banco de dados por locatário Olá são relacionadas tooincreased custos de recursos de nuvem devido tooreduced compartilhamento e manter e gerenciar vários bancos de dados. Os desenvolvedores de aplicativos SaaS muitas vezes têm dificuldades ao fazer essas compensações.

Embora as compensações podem ser barreiras principais com a maioria dos provedores de serviço de banco de dados de nuvem, o banco de dados do SQL Azure elimina as barreiras de Olá com seus recursos de banco de dados Elástico e o pool Elástico. Os desenvolvedores de SaaS podem combinar as características de isolamento de saudação de um modelo de banco de dados por locatário e otimizar melhorias de gerenciamento de compartilhamento e hello de recurso de vários bancos de dados por meio de pools Elásticos e ferramentas associadas.

Provedores de aplicativos multilocatários que não têm requisitos de isolamento de locatário e são capazes de empacotar locatários em banco de dados em uma densidade alta podem considerar que os modelos de dados compartilhados resultam em eficiência adicional no compartilhamento de recursos e na redução do custo geral. As ferramentas de banco de dados elástico do Banco de Dados SQL do Azure, as bibliotecas de fragmentação e os recursos de segurança ajudam os provedores de SaaS a criar e gerenciar esses aplicativos multilocatários.

## <a name="next-steps"></a>Próximas etapas
[Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md) com um aplicativo de exemplo que demonstra a biblioteca de saudação do cliente.

Crie um [painel personalizado do pool elástico para SaaS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) com um aplicativo de exemplo que usa pools elásticos para uma solução de banco de dados econômica e escalonável.

Usar as ferramentas de banco de dados SQL do hello muito[migrar tooscale de bancos de dados existente out](sql-database-elastic-convert-to-use-elastic-tools.md).

toocreate usando um pool Elástico hello Azure portal, consulte [criar um pool Elástico](sql-database-elastic-pool-manage-portal.md).  

Saiba como muito[monitorar e gerenciar um pool Elástico](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Implantar e explorar um aplicativo multilocatário que usa o Banco de dados SQL do Azure - Wingtip SaaS](sql-database-saas-tutorial.md)
* [O que é um pool elástico do Azure?](sql-database-elastic-pool.md)
* [Escalando horizontalmente com o Banco de Dados SQL do Azure](sql-database-elastic-scale-introduction.md)
* [Aplicativos multilocatários com ferramentas de banco de dados elástico e segurança em nível de linha](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Autenticação em aplicativos multilocatários usando o Azure Active Directory e o OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplicativo Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Perguntas e solicitações de recursos

Para perguntas, encontre-nos em Olá [Fórum do banco de dados SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Adicionar uma solicitação de recurso no hello [Fórum de comentários do banco de dados SQL](https://feedback.azure.com/forums/217321-sql-database/).

