---
title: aaaGetting iniciado com tabelas temporais no banco de dados do SQL Azure | Microsoft Docs
description: Saiba como tooget iniciada com o uso de tabelas temporais no banco de dados do SQL Azure.
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="0ee62-103">Introdução às Tabelas Temporais no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0ee62-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="0ee62-104">Tabelas Temporais são um novo recurso de programabilidade do banco de dados do SQL Azure que permite que você tootrack e analisar o histórico completo de saudação de alterações em seus dados, sem necessidade de saudação de codificação personalizada.</span><span class="sxs-lookup"><span data-stu-id="0ee62-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="0ee62-105">Tabelas temporais manter dados tootime relacionadas contexto para que os fatos armazenados podem ser interpretados como válido somente dentro de um período específico hello.</span><span class="sxs-lookup"><span data-stu-id="0ee62-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="0ee62-106">Essa propriedade das Tabelas Temporais permite uma análise eficiente baseada em tempo e a obtenção de informações da evolução dos dados.</span><span class="sxs-lookup"><span data-stu-id="0ee62-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="0ee62-107">Cenário Temporal</span><span class="sxs-lookup"><span data-stu-id="0ee62-107">Temporal Scenario</span></span>
<span data-ttu-id="0ee62-108">Este artigo ilustra Olá etapas tooutilize tabelas temporais em um cenário de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0ee62-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="0ee62-109">Suponha que você queira tootrack atividade de usuário em um novo site que está sendo desenvolvido a partir do zero ou em um site existente que você deseja tooextend com a análise da atividade de usuário.</span><span class="sxs-lookup"><span data-stu-id="0ee62-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="0ee62-110">Neste exemplo simplificado, vamos supor que o número de saudação de páginas da web visitadas durante um período de tempo é um indicador que precisa toobe capturada e monitorado no banco de dados de site de saudação que é hospedado no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee62-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="0ee62-111">meta de saudação de análise histórica de saudação da atividade do usuário é tooget entradas tooredesign site e fornecer a melhor experiência para os visitantes hello.</span><span class="sxs-lookup"><span data-stu-id="0ee62-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="0ee62-112">modelo de banco de dados de saudação para este cenário é muito simple - métrica de atividade de usuário é representado por um campo único inteiro, **PageVisited**e é capturada juntamente com informações básicas sobre o perfil de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ee62-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="0ee62-113">Além disso, para análise de tempo com base, você mantém uma série de linhas para cada usuário, onde cada linha representa número de saudação de páginas de um determinado usuário visitou em um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="0ee62-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Esquema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="0ee62-115">Felizmente, você não precisa tooput qualquer esforço no seu aplicativo toomaintain essas informações de atividade.</span><span class="sxs-lookup"><span data-stu-id="0ee62-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="0ee62-116">Com tabelas temporais, este processo será automatizado - lhe oferece total flexibilidade durante o design do site e toofocus de tempo mais na análise de dados de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="0ee62-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="0ee62-117">Olá somente ter toodo é tooensure que **WebSiteInfo** tabela está configurada como [temporal com versão do sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="0ee62-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="0ee62-118">Olá as etapas exatas tooutilize tabelas temporais neste cenário são descritos abaixo.</span><span class="sxs-lookup"><span data-stu-id="0ee62-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="0ee62-119">Etapa 1: configurar tabelas como temporais</span><span class="sxs-lookup"><span data-stu-id="0ee62-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="0ee62-120">Dependendo se você estiver iniciando um novo desenvolvimento ou atualizando um aplicativo existente, você criará tabelas temporais ou modificará as existentes ao adicionar atributos temporais.</span><span class="sxs-lookup"><span data-stu-id="0ee62-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="0ee62-121">Em geral, seu cenário pode ser uma combinação dessas duas opções.</span><span class="sxs-lookup"><span data-stu-id="0ee62-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="0ee62-122">Execute estas ações usando o [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), o [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou qualquer outra ferramenta de desenvolvimento do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="0ee62-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ee62-123">É recomendável que você sempre use Olá versão mais recente do Management Studio tooremain sincronizado com atualizações tooMicrosoft Azure e banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="0ee62-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="0ee62-124">[Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ee62-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="0ee62-125">Criar nova tabela</span><span class="sxs-lookup"><span data-stu-id="0ee62-125">Create new table</span></span>
<span data-ttu-id="0ee62-126">Use o item de menu de contexto "Nova tabela com versão do sistema" no editor de consultas do Pesquisador de objetos do SSMS tooopen Olá com um script de modelo de tabela temporal e, em seguida, usar o modelo de saudação de toopopulate de "Especificar valores para parâmetros de modelo" (Ctrl + Shift + M):</span><span class="sxs-lookup"><span data-stu-id="0ee62-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="0ee62-128">No SSDT, escolher o modelo de "Tabela Temporal (versão do sistema)" ao adicionar novo projeto de banco de dados de toohello de itens.</span><span class="sxs-lookup"><span data-stu-id="0ee62-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="0ee62-129">Que serão o designer de tabela aberta e habilitar tooeasily você especificar Olá layout de tabela:</span><span class="sxs-lookup"><span data-stu-id="0ee62-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="0ee62-131">Você também pode uma tabela temporal criar especificando instruções Olá Transact-SQL diretamente, conforme mostrado no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="0ee62-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="0ee62-132">Observe que Olá elementos obrigatórios de cada tabela temporal são a definição de período hello e cláusula SYSTEM_VERSIONING de saudação com uma tabela de usuário de tooanother de referência que irão armazenar versões de linha de histórico:</span><span class="sxs-lookup"><span data-stu-id="0ee62-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="0ee62-133">Quando você cria a tabela temporal com versão do sistema, Olá que acompanha a tabela de histórico com a configuração padrão de saudação é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0ee62-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="0ee62-134">tabela de histórico padrão Olá contém um índice de árvore B clusterizado nas colunas de período hello (início, fim) com a compactação de página habilitada.</span><span class="sxs-lookup"><span data-stu-id="0ee62-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="0ee62-135">Essa configuração é ideal para a maioria de saudação de cenários em que as tabelas Temporais são usadas, especialmente para [dados de auditoria](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="0ee62-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="0ee62-136">Nesse caso específico, nosso objetivo é análise de tendência com base em tempo de tooperform um histórico de dados maior e com conjuntos de dados maiores, para a opção de armazenamento de Olá Olá tabela de histórico é um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="0ee62-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="0ee62-137">Um columnstore clusterizado oferece compactação e desempenho ótimos para consultas analíticas.</span><span class="sxs-lookup"><span data-stu-id="0ee62-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="0ee62-138">Temporal oferecem tabelas Olá índices de tooconfigure flexibilidade em Olá tabelas atuais e temporal completamente independentemente.</span><span class="sxs-lookup"><span data-stu-id="0ee62-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ee62-139">Índices ColumnStore só estão disponíveis na camada de serviço premium Olá.</span><span class="sxs-lookup"><span data-stu-id="0ee62-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="0ee62-140">saudação de script a seguir mostra como o índice padrão na tabela de histórico pode ser alterados toohello clusterizada columnstore:</span><span class="sxs-lookup"><span data-stu-id="0ee62-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="0ee62-141">Tabelas Temporais são representadas em Olá Pesquisador de objetos com ícone de saudação específico para facilitar sua identificação, enquanto sua tabela de histórico é exibida como um nó filho.</span><span class="sxs-lookup"><span data-stu-id="0ee62-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="0ee62-143">Alterar tootemporal de tabela existente</span><span class="sxs-lookup"><span data-stu-id="0ee62-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="0ee62-144">Vamos abordar o cenário de saudação alternativo no qual Olá WebsiteUserInfo tabela já existe, mas não foi projetado tookeep um histórico das alterações.</span><span class="sxs-lookup"><span data-stu-id="0ee62-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="0ee62-145">Nesse caso, você pode estender simplesmente Olá existente tabela toobecome temporal, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="0ee62-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="0ee62-146">Etapa 2: executar sua carga de trabalho regularmente</span><span class="sxs-lookup"><span data-stu-id="0ee62-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="0ee62-147">a principal vantagem Olá das tabelas temporais é que você não precisa toochange ou ajustar seu site em qualquer controle de alterações tooperform de maneira.</span><span class="sxs-lookup"><span data-stu-id="0ee62-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="0ee62-148">Depois de criadas, as Tabelas Temporais fazem as versões de linha persistirem de forma transparente sempre que você executa modificações em seus dados.</span><span class="sxs-lookup"><span data-stu-id="0ee62-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="0ee62-149">No controle de alterações automáticas ordem tooleverage para essa situação específica, vamos apenas atualizar coluna **PagesVisited** toda vez que quando o usuário termina Component sessão no site de saudação:</span><span class="sxs-lookup"><span data-stu-id="0ee62-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="0ee62-150">É importante toonotice que Olá consulta update não precisa de hora exata do tooknow hello quando a operação real Olá ocorreu nem como dados históricos serão preservados para análise futura.</span><span class="sxs-lookup"><span data-stu-id="0ee62-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="0ee62-151">Ambos os aspectos são tratados automaticamente pelo hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0ee62-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="0ee62-152">Olá diagrama a seguir ilustra como dados de histórico são gerados em cada atualização.</span><span class="sxs-lookup"><span data-stu-id="0ee62-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="0ee62-154">Etapa 3: executar a análise de dados históricos</span><span class="sxs-lookup"><span data-stu-id="0ee62-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="0ee62-155">Agora, quando o versionamento pelo sistema temporal estiver habilitado, a análise dos dados históricos estará a apenas uma consulta de distância de você.</span><span class="sxs-lookup"><span data-stu-id="0ee62-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="0ee62-156">Neste artigo, podemos fornecer alguns exemplos que abordam os cenários comuns de análise - toolearn todos os detalhes, explorar várias opções introduzidas com hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) cláusula.</span><span class="sxs-lookup"><span data-stu-id="0ee62-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="0ee62-157">toosee Olá top 10 usuários ordenados pelo número de saudação de páginas da web visitadas a partir de uma hora atrás, execute esta consulta:</span><span class="sxs-lookup"><span data-stu-id="0ee62-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="0ee62-158">Você pode modificar essa consulta tooanalyze Olá visitas ao site a partir de um dia atrás, há um mês ou em qualquer ponto Olá anterior se desejar.</span><span class="sxs-lookup"><span data-stu-id="0ee62-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="0ee62-159">análise estatística básica de tooperform para Olá dia anterior, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ee62-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="0ee62-160">toosearch atividades de um usuário específico, em um período de tempo, use Olá CONTAINED IN cláusula:</span><span class="sxs-lookup"><span data-stu-id="0ee62-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="0ee62-161">A visualização gráfica é especialmente conveniente para consultas temporais porque você pode mostrar com muita facilidade tendências e padrões de uso de uma maneira intuitiva:</span><span class="sxs-lookup"><span data-stu-id="0ee62-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="0ee62-163">Aprimoramento do esquema de tabela</span><span class="sxs-lookup"><span data-stu-id="0ee62-163">Evolving table schema</span></span>
<span data-ttu-id="0ee62-164">Normalmente, você precisará esquema de tabela temporal Olá toochange enquanto você estiver fazendo o desenvolvimento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0ee62-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="0ee62-165">Para fazer isso, basta executar instruções ALTER TABLE regulares e banco de dados do SQL Azure propagará adequadamente tabela de histórico de toohello de alterações.</span><span class="sxs-lookup"><span data-stu-id="0ee62-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="0ee62-166">Olá script a seguir mostra como você pode adicionar atributos adicionais para o controle:</span><span class="sxs-lookup"><span data-stu-id="0ee62-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="0ee62-167">Da mesma forma, você pode alterar a definição de coluna enquanto sua carga de trabalho está ativa:</span><span class="sxs-lookup"><span data-stu-id="0ee62-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="0ee62-168">Por fim, você pode remover uma coluna que já não precisa.</span><span class="sxs-lookup"><span data-stu-id="0ee62-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="0ee62-169">Como alternativa, use a versão mais recente [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal esquema de tabela enquanto você estiver conectado toohello banco de dados (modo online) ou como parte do projeto de banco de dados da saudação (modo offline).</span><span class="sxs-lookup"><span data-stu-id="0ee62-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="0ee62-170">Controle de retenção de dados históricos</span><span class="sxs-lookup"><span data-stu-id="0ee62-170">Controlling retention of historical data</span></span>
<span data-ttu-id="0ee62-171">Com tabelas temporais com versão do sistema, tabela de histórico de saudação pode aumentar o tamanho do banco de dados hello mais do que tabelas regulares.</span><span class="sxs-lookup"><span data-stu-id="0ee62-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="0ee62-172">Uma tabela de histórico grande e crescente pode se tornar um problema ambas toopure os custos de armazenamento, bem como por impor um desempenho imposto sobre consultas Temporais.</span><span class="sxs-lookup"><span data-stu-id="0ee62-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="0ee62-173">Portanto, o desenvolvimento de uma política de retenção de dados para o gerenciamento de dados na tabela de histórico de saudação é um aspecto importante do planejamento e gerenciamento do ciclo de vida de saudação de cada tabela temporal.</span><span class="sxs-lookup"><span data-stu-id="0ee62-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="0ee62-174">Banco de dados SQL Azure, você tem Olá abordagens para gerenciar dados históricos na tabela temporal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ee62-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="0ee62-175">Particionamento de tabela</span><span class="sxs-lookup"><span data-stu-id="0ee62-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="0ee62-176">Script de Limpeza Personalizado</span><span class="sxs-lookup"><span data-stu-id="0ee62-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="0ee62-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ee62-177">Next steps</span></span>
<span data-ttu-id="0ee62-178">Para obter informações detalhadas sobre as Tabelas Temporais, confira a [documentação do MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ee62-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="0ee62-179">Visite Channel 9 toohear um [real implementação temporal história de sucesso](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e inspecionar uma [live temporal demonstração](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="0ee62-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

