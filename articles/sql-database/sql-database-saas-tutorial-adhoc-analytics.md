---
title: "consultas de análise ad hoc aaaRun em vários bancos de dados SQL do Azure | Microsoft Docs"
description: "Execute consultas de análise ad hoc em vários bancos de dados do SQL no aplicativo do hello Wingtip SaaS multilocatário."
keywords: tutorial do banco de dados SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Executar consultas de análise ad hoc em todos os locatários SaaS Wingtip

Neste tutorial, você executar consultas distribuídas em todo o conjunto de bancos de dados de locatário Olá tooenable ad-hoc análises. Consulta elástica é usado tooenable distribuído de consultas, que requer um banco de dados de análise adicional for implantado (servidor de catálogo toohello). Essas consultas podem extrair insights ocultos em dados operacionais diárias de saudação do aplicativo de SaaS Wingtip hello.


Neste tutorial, você aprende:

> [!div class="checklist"]

> * Sobre exibições global de saudação em cada banco de dados, que permitem a consulta eficiente entre locatários
> * Como toodeploy um banco de dados de análise ad hoc
> * Como toorun consultas distribuídas em todos os bancos de dados de locatário



toocomplete neste tutorial, verifique Olá se os pré-requisitos a seguir são concluídas:

* Olá Wingtip SaaS aplicativo é implantado. toodeploy em menos de cinco minutos, consulte [implantar e explorar o aplicativo de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* O Azure PowerShell está instalado. Para obter detalhes, consulte [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* O SSMS (SQL Server Management Studio) está instalado. toodownload e instale o SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Padrão de análise ad hoc

Um dos grandes oportunidades Olá com aplicativos SaaS é toouse Olá enorme quantidade de dados de locatário armazenadas centralmente em nuvem hello. Use este insights toogain de dados em operação hello e uso de seu aplicativo, seus locatários, seus usuários, preferências, comportamentos, etc. Essas informações podem guiar o desenvolvimento do recurso, aprimoramentos de usabilidade e outros investimentos no aplicativo e nos serviços.

É fácil acessar esses dados em um único banco de dados multilocatário, mas não tão fácil quando são distribuídos em escala por, potencialmente, milhares de bancos de dados. Uma abordagem é toouse [consulta Elástico](sql-database-elastic-query-overview.md), que habilita a consulta em um conjunto distribuído de bancos de dados com um esquema comum. Elástica consulta usa um único *head* banco de dados no qual as tabelas externas são definidas que espelho tabelas ou exibições Olá distribuído bancos de dados (Locatário). As consultas enviadas toothis principal de banco de dados é compilado tooproduce um plano de consulta distribuída, com partes de saudação consulta propagados toohello bancos de dados de locatário, conforme necessário. Consulta elástica usa o mapa do fragmento Olá no local de saudação de tooprovide Olá catálogo banco de dados de bancos de dados de locatário de saudação. A instalação e a consulta são diretas usando o [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) padrão e dá suporte para consultas ad hoc de ferramentas, como o Power BI e o Excel.

Distribuindo consultas em bancos de dados de locatário hello, consulta Elástico fornece ideias imediatas sobre dados de produção. No entanto, como a consulta Elástico extrai dados de vários bancos de dados, consulta latência às vezes pode ser maior do que para consultas equivalentes enviados tooa único banco de dados de vários locatários. Tenha cuidado ao projetar consultas dados saudação toominimize que são retornados. Consulta elástica é geralmente mais adequada para consultar pequenas quantidades de dados em tempo real, relatórios, as consultas analíticas complexas ou toobuilding contrário usados com frequência. Se as consultas não executam bem, examinar Olá [plano de execução](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee qual parte da consulta Olá foi pressionado toohello banco de dados remoto e a quantidade de dados está sendo retornado. Consultas que exigem processamento analítico complexo podem ser melhor atendidas em alguns casos extraindo dados de locatário em um banco de dados dedicado ou data warehouse otimizado para consultas de análise. Esse padrão é explicado em Olá [tutorial de análise de locatário](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Obter scripts de aplicativo hello Wingtip

Hello Wingtip SaaS scripts e código fonte do aplicativo estão disponíveis no hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório github. [As etapas de scripts de SaaS Wingtip Olá toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Criar dados de vendas de ingresso

toorun as consultas em um conjunto de dados mais interessante, crie dados de vendas de tíquete executando o gerador de tíquete hello.

1. Em Olá *PowerShell ISE*, abra hello... \\Módulos de aprendizado\\análise operacional\\análise ad hoc\\*AdhocAnalytics.ps1 demonstração* script e definir Olá valores a seguir:
   * **$DemoScenario** = 1, **Comprar ingressos de eventos em todos os locais**.
2. Pressione **F5** para executar o script hello e gerar vendas de tíquete. Durante a execução de script hello, continue com as etapas de saudação neste tutorial. dados de tíquete de saudação são consultados em Olá *executar consultas ad hoc distribuída* seção, aguarde até Olá tíquete gerador toocomplete se ele ainda está em execução quando você obter toothat exercício.

## <a name="explore-hello-global-views"></a>Explore os modos de exibição globais Olá

Olá aplicativo SaaS Wingtip é criado usando um modelo de locatário por banco de dados, portanto o esquema de banco de dados de locatário Olá é definida de uma perspectiva de único locatário. As informações específicas do locatário existem em uma tabela, *Local*, que sempre tem uma única linha e é implementada como um heap, sem uma chave primária. Outras tabelas no esquema de saudação não é necessário toobe relacionada toohello *foro* tabela, porque em uso normal, nunca há alguma dúvida quais dados de saudação do locatário pertencem.

No entanto, ao consultar em todos os bancos de dados, é importante que consulta Elástico pode tratar dados saudação como se faz parte de um único banco de dados lógico fragmentado por locatário. tooachieve isso, um conjunto de exibições 'globais' são toohello adicionado locatário banco de dados do projeto uma id de locatário em cada uma das tabelas de saudação que são consultadas globalmente. Por exemplo, Olá *VenueEvents* exibição adiciona um computada *VenueId* toohello colunas projetadas de saudação *eventos* tabela. Definindo a tabela externa Olá no banco de dados principal Olá sobre *VenueEvents* (em vez da saudação subjacente *eventos* tabela), consulta Elástico é capaz de toopush para baixo de junções com base em *VenueId* para que eles podem ser executados em paralelo em cada banco de dados remoto (e não no banco de dados principal Olá). Isso drasticamente reduz a quantidade de saudação de dados que são retornados, o que resulta em um aumento significativo no desempenho para várias consultas. Essas exibições globais foram pré-criadas em todos os bancos de dados de locatário (e em *basetenantdb*).

1. Abra o SSMS e [conectar toohello tenants1 -&lt;usuário&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Expanda **Bancos de Dados**, clique com botão direito do mouse em **contosoconcerthall**e selecione **Nova Consulta**.
3. Execute Olá diferença de saudação tooexplore consultas entre tabelas de único locatário hello e modos de exibição globais Olá a seguir:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

Esses modos de exibição, Olá *VenueId* é calculado como um hash do nome de local de hello, mas qualquer abordagem pode ser usado toointroduce um valor exclusivo. Essa abordagem é semelhante maneira toohello chave de locatário Olá é calculado para uso no catálogo de saudação.

definição de saudação tooexamine de saudação *locais* exibição:

1. Em **Gerenciador de Objeto**, expanda **contosoconcethall** > **Exibições**:

   ![Modos de exibição](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Clique com botão direito do mouse em **dbo.Venues**.
3. Selecione **Modo de Exibição de Script como** > **CRIAR para** > **Janela do Editor Nova Consulta**

Script de qualquer um dos outros Olá *foro* exibições toosee como adicionam Olá *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Implantar banco de dados de saudação usado para consultas distribuída ad hoc

Este exercício implanta Olá *adhocanalytics* banco de dados. Isso é o banco de dados principal do hello que conterá o esquema de saudação usado para consultar em todos os bancos de dados de locatário. banco de dados de saudação é implantado toohello existente do servidor de catálogo, que é o servidor de saudação usado para todos os relacionadas ao gerenciamento de bancos de dados no aplicativo de exemplo hello.

1. Abrir... \\Módulos de aprendizado\\análise operacional\\análise ad hoc\\*demonstração AdhocAnalytics.ps1* em Olá *PowerShell ISE* e hello conjunto os valores a seguir:
   * **$DemoScenario** = 2, **Implantar banco de dados de análise Ad hoc**.

2. Pressione **F5** toorun Olá script e criar hello *adhocanalytics* banco de dados.

Na próxima seção, Olá, adicionar o banco de dados do esquema toohello que ela possa ser usada toorun distribuída consultas.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Configurar Olá banco de dados para executar consultas distribuídas

Este exercício adiciona o esquema (fonte de dados externa hello e definições de tabela externa) toohello ad-hoc análise banco de dados que habilita a consulta em todos os bancos de dados de locatário.

1. Abra o SQL Server Management Studio e conecte toohello banco de dados de análise ad hoc que você criou na etapa anterior hello. nome de saudação do banco de dados de saudação será adhocanalytics.
2. Abra ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* no SSMS.
3. Examine o script SQL Olá e observe Olá seguinte:

   Elástica consulta usa uma credencial no escopo do banco de dados tooaccess cada um dos bancos de dados de locatário hello. Essa credencial precisa toobe disponível em todos os bancos de dados hello e normalmente deve ser concedida direitos mínimos Olá necessário tooenable essas consultas ad hoc.

    ![criar credencial](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Hello fonte de dados externa, que é definido pelo mapa do fragmento toouse Olá locatário no banco de dados de catálogo hello. Usando isso como fonte de dados externa hello, as consultas são bancos de dados distribuído tooall registrados no catálogo de saudação quando Olá consulta for executada. Como nomes de servidor são diferentes para cada implantação, esse script de inicialização obtém o local de saudação do banco de dados de catálogo Olá recuperando o servidor atual hello (@@servername) onde o script hello é executada.

    ![Criar fonte de dados externa](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   Olá tabelas externas que fazem referência a saudação modos de exibição globais descrito na seção anterior hello e definido com **distribuição = SHARDED(VenueId)**. Como cada *VenueId* mapeia tooa único banco de dados, isso melhora o desempenho para muitos cenários conforme mostrado na próxima seção, Olá.

    ![criar tabelas externas](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   tabela local Olá *VenueTypes* que é criada e preenchida. Essa tabela de dados de referência é comum em todos os bancos de dados de locatário, portanto ele pode ser representado como uma tabela local e preenchida com dados comuns hello. Para algumas consultas que isso pode reduzir Olá quantidade de dados movidos entre bancos de dados de locatário hello e hello *adhocanalytics* banco de dados.

    ![criar tabela](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Se você incluir tabelas de referência dessa maneira, ser dados e o esquema da tabela Olá tooupdate-se de que sempre que você atualizar bancos de dados de locatário hello.

4. Pressione **F5** toorun Olá script e inicializar Olá *adhocanalytics* banco de dados. 

Agora você pode executar consultas distribuídas e reunir informações entre todos os locatários!

## <a name="run-ad-hoc-distributed-queries"></a>Executar consultas distribuídas ad hoc

Agora que Olá *adhocanalytics* banco de dados está configurado, vá em frente e execute algumas consultas distribuídas. Inclua plano de execução de saudação para melhor compreender onde o processamento de consulta hello está acontecendo. 

Ao inspecionar o plano de execução hello, passe o mouse sobre os ícones de plano Olá para obter detalhes. 

Toonote importante, é a configuração **distribuição = SHARDED(VenueId)** quando definimos fonte de dados externa hello, melhora o desempenho para muitos cenários. Como cada *VenueId* mapeia tooa único banco de dados, a filtragem é dados facilmente concluído remotamente, retornando Olá somente é necessário.

1. Abra... \\Módulos de Aprendizado\\Análise Operacional\\Análise Ad Hoc\\*Demo-AdhocAnalyticsQueries.sql* no SSMS.
2. Certifique-se de que você está conectado toohello **adhocanalytics** banco de dados.
3. Selecione Olá **consulta** menu e clique em **incluir plano de execução real**
4. Realçar Olá *quais locais são registrados no momento?* consulta e pressione **F5**.

   consulta de saudação retorna a lista de local inteiro de hello, ilustrando como rápido e é fácil tooquery em todos os locatários e retornar dados de cada locatário.

   Inspecionar o plano de saudação e vê que o custo total por Olá é consulta remota Olá porque estamos simplesmente o banco de dados de locatário de tooeach contínuo e selecionando informações de local de saudação.

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. Consulta seguinte Olá selecione e pressione **F5**.

   Essa consulta une dados de bancos de dados de locatário hello e Olá local *VenueTypes* tabela (local, como ela é uma tabela em Olá *adhocanalytics* banco de dados).

   Inspecionar plano hello e ver que Olá maioria de custo é consulta remota Olá porque estamos consultar informações de local de cada locatário (dbo. Locais), e, em seguida, faça uma junção de local rápida com hello local *VenueTypes* nome amigável da tabela toodisplay hello.

   ![Unir dados remotos e locais](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Agora selecione Olá *em qual dia foram Olá a maioria dos tíquetes vendidas?* consulta e pressione **F5**.

   Essa consulta faz uma união e uma agregação um pouco mais complexas. O que é toonote importante é que a maioria do processamento de saudação é feita remotamente, e novamente, estamos trazer de volta somente as linhas Olá que necessária, retornando apenas uma única linha para contagem de venda de tíquete de agregação de cada local por dia.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a:

> [!div class="checklist"]

> * Executar consultas distribuídas entre todos os bancos de dados de locatário
> * Implantar um banco de dados de análise ad hoc e adicionar esquema tooit toorun distribuída consultas.


Agora tente Olá [tutorial de análise de locatário](sql-database-saas-tutorial-tenant-analytics.md) tooexplore extrair o banco de dados do data tooa análise separada para o processamento de análise mais complexo...

## <a name="additional-resources"></a>Recursos adicionais

* Adicionais [tutoriais que se baseiam na Olá aplicativo SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Consulta elástica](sql-database-elastic-query-overview.md)
