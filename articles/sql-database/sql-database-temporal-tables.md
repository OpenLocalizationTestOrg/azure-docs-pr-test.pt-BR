---
title: "Introdução às Tabelas Temporais no Banco de Dados SQL do Azure | Microsoft Docs"
description: "Saiba como começar a usar as Tabelas Temporais no Banco de Dados SQL do Azure."
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="ed8c3-103">Introdução às Tabelas Temporais no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed8c3-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="ed8c3-104">As Tabelas Temporais são um novo recurso de programação do Banco de Dados SQL do Azure que permite controlar e analisar o histórico completo de alterações em seus dados, sem a necessidade de codificação personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="ed8c3-105">As Tabelas Temporais mantêm os dados relacionados ao contexto de tempo, de forma que os fatos armazenados possam ser interpretados como válidos apenas no período específico.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="ed8c3-106">Essa propriedade das Tabelas Temporais permite uma análise eficiente baseada em tempo e a obtenção de informações da evolução dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="ed8c3-107">Cenário Temporal</span><span class="sxs-lookup"><span data-stu-id="ed8c3-107">Temporal Scenario</span></span>
<span data-ttu-id="ed8c3-108">Este artigo ilustra as etapas para utilizar as Tabelas Temporais em um cenário de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="ed8c3-109">Suponha que você queira acompanhar a atividade de usuário em um novo site que está sendo desenvolvido do zero ou em um site existente que você deseja estender com análises de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="ed8c3-110">Neste exemplo simplificado, estamos supondo que o número de páginas da Web visitadas durante um período é um indicador do que precisa ser capturado e monitorado no banco de dados do site hospedado no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="ed8c3-111">O objetivo da análise do histórico da atividade de usuário é obter entradas para reprojetar o site e fornecer uma experiência melhor para os visitantes.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="ed8c3-112">O modelo de banco de dados para esse cenário é muito simples: a métrica de atividade do usuário é representada por um único campo de inteiro, **PageVisited**, e é capturada com informações básicas no perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="ed8c3-113">Além disso, para a análise baseada em tempo, você manteria uma série de linhas para cada usuário, onde cada linha representa o número de páginas visitadas por um usuário específico em um período específico.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Esquema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="ed8c3-115">Felizmente, você não precisa fazer qualquer esforço em seu aplicativo para manter essas informações de atividade.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="ed8c3-116">Com as Tabelas Temporais, esse processo é automatizado - oferecendo flexibilidade total durante o design do site e mais tempo para se concentrar na análise de dados.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="ed8c3-117">A única coisa que você precisa fazer é garantir que a tabela **WebSiteInfo** seja configurada como [temporal versionada pelo sistema](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="ed8c3-118">As etapas exatas para utilizar as Tabelas Temporais neste cenário são descritas abaixo.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="ed8c3-119">Etapa 1: configurar tabelas como temporais</span><span class="sxs-lookup"><span data-stu-id="ed8c3-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="ed8c3-120">Dependendo se você estiver iniciando um novo desenvolvimento ou atualizando um aplicativo existente, você criará tabelas temporais ou modificará as existentes ao adicionar atributos temporais.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="ed8c3-121">Em geral, seu cenário pode ser uma combinação dessas duas opções.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="ed8c3-122">Execute estas ações usando o [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), o [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou qualquer outra ferramenta de desenvolvimento do Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed8c3-123">Recomendamos que você sempre use a versão mais recente do Management Studio a fim de permanecer sincronizado com as atualizações no Microsoft Azure e no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="ed8c3-124">[Atualizar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="ed8c3-125">Criar nova tabela</span><span class="sxs-lookup"><span data-stu-id="ed8c3-125">Create new table</span></span>
<span data-ttu-id="ed8c3-126">Use o item de menu de contexto "Nova Tabela Versionada pelo Sistema” no Pesquisador de Objetos do SSMS para abrir o editor de consulta com um script modelo de tabela temporal e então use “Especificar Valores para Parâmetros de Modelo” (Ctrl+Shift+M) para preencher o modelo:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="ed8c3-128">No SSDT, você escolheu o modelo "Tabela Temporal (Versionada pelo Sistema)" ao adicionar novos itens ao projeto de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="ed8c3-129">Isso abrirá o designer de tabela e permitirá que você especifique o layout da tabela com facilidade:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="ed8c3-131">Você também pode criar uma tabela temporal ao especificar diretamente as instruções Transact-SQL, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="ed8c3-132">Observe que os elementos obrigatórios de todas as tabelas temporais são a definição PERIOD e a cláusula SYSTEM_VERSIONING com uma referência a outra tabela de usuário que armazenará versões de linha de histórico:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="ed8c3-133">Quando você cria a tabela temporal versionada pelo sistema, a tabela de histórico que acompanha este artigo com a configuração padrão é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="ed8c3-134">A tabela de histórico padrão contém um índice de árvore B clusterizado nas colunas de período (fim, início) com a compactação de página habilitada.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="ed8c3-135">Essa configuração é ideal para a maioria dos cenários em que as tabelas temporais são usadas, especialmente para a [auditoria de dados](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="ed8c3-136">Neste caso em particular, temos o objetivo de realizar análises de tendências baseadas em tempo ao longo de um histórico de dados maior e com conjuntos de dados maiores, de forma que a opção de armazenamento para a tabela de histórico seja um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="ed8c3-137">Um columnstore clusterizado oferece compactação e desempenho ótimos para consultas analíticas.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="ed8c3-138">As Tabelas Temporais oferecem a flexibilidade de configurar os índices nas tabelas atuais e temporais de forma totalmente independente.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="ed8c3-139">Os índices columnstore só estão disponíveis na camada de serviço premium.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="ed8c3-140">O script a seguir mostra como o índice padrão na tabela de histórico pode ser alterado para o columnstore clusterizado:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="ed8c3-141">As Tabelas Temporais são representadas no Pesquisador de Objetos com o ícone específico para facilitar sua identificação, enquanto sua tabela de histórico é exibida como um nó filho.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="ed8c3-143">Alterar uma tabela existente para temporal</span><span class="sxs-lookup"><span data-stu-id="ed8c3-143">Alter existing table to temporal</span></span>
<span data-ttu-id="ed8c3-144">Vamos abordar o cenário alternativo no qual a tabela WebsiteUserInfo já existe, mas que não foi projetada para manter um histórico de alterações.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="ed8c3-145">Nesse caso, você pode simplesmente estender a tabela existente para se tornar temporal, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="ed8c3-146">Etapa 2: executar sua carga de trabalho regularmente</span><span class="sxs-lookup"><span data-stu-id="ed8c3-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="ed8c3-147">A principal vantagem das Tabelas Temporais é que você não precisa alterar ou ajustar seu site de alguma maneira para executar o controle de alterações.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="ed8c3-148">Depois de criadas, as Tabelas Temporais fazem as versões de linha persistirem de forma transparente sempre que você executa modificações em seus dados.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="ed8c3-149">Para aproveitar o controle de alterações automático deste cenário em particular, iremos atualizar apenas a coluna **PagesVisited** sempre que um usuário finalizar sua sessão no site:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="ed8c3-150">É importante observar que a consulta de atualizações não precisa saber a hora exata em que a operação real ocorreu nem como os dados históricos serão preservados para análise futura.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="ed8c3-151">Ambos os aspectos são tratados automaticamente pelo Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="ed8c3-152">O diagrama a seguir ilustra como os dados históricos estão sendo gerados em cada atualização.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="ed8c3-154">Etapa 3: executar a análise de dados históricos</span><span class="sxs-lookup"><span data-stu-id="ed8c3-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="ed8c3-155">Agora, quando o versionamento pelo sistema temporal estiver habilitado, a análise dos dados históricos estará a apenas uma consulta de distância de você.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="ed8c3-156">Neste artigo, mostraremos alguns exemplos que tratam dos cenários comuns da análise. Para obter todos os detalhes, explore as diversas opções introduzidas com a cláusula [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="ed8c3-157">Para ver os 10 principais usuários ordenados pelo número de páginas da Web visitadas na última hora, execute esta consulta:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="ed8c3-158">Você pode modificar facilmente essa consulta para analisar as visitas ao site no dia anterior, no mês anterior ou em qualquer ponto no passado desejado.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="ed8c3-159">Para executar a análise estatística básica do dia anterior, use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="ed8c3-160">Para procurar atividades de um usuário específico, em um período de tempo, use a cláusula CONTAINED IN:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="ed8c3-161">A visualização gráfica é especialmente conveniente para consultas temporais porque você pode mostrar com muita facilidade tendências e padrões de uso de uma maneira intuitiva:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="ed8c3-163">Aprimoramento do esquema de tabela</span><span class="sxs-lookup"><span data-stu-id="ed8c3-163">Evolving table schema</span></span>
<span data-ttu-id="ed8c3-164">Normalmente, você precisará alterar o esquema de tabela temporal enquanto estiver fazendo o desenvolvimento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="ed8c3-165">Para isso, bastará executar as instruções ALTER TABLE normais e o Banco de Dados SQL do Azure propagará adequadamente as alterações na tabela de histórico.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="ed8c3-166">O script a seguir mostra como você pode adicionar outros atributos ao controle:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="ed8c3-167">Da mesma forma, você pode alterar a definição de coluna enquanto sua carga de trabalho está ativa:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="ed8c3-168">Por fim, você pode remover uma coluna que já não precisa.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="ed8c3-169">Como alternativa, use o [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) mais recente para alterar o esquema de tabela temporal enquanto estiver conectado ao banco de dados (modo online) ou como parte do projeto do banco de dados (modo offline).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="ed8c3-170">Controle de retenção de dados históricos</span><span class="sxs-lookup"><span data-stu-id="ed8c3-170">Controlling retention of historical data</span></span>
<span data-ttu-id="ed8c3-171">Com as tabelas temporais versionadas pelo sistema, a tabela de histórico pode aumentar o tamanho do banco de dados mais do que as tabelas normais.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="ed8c3-172">Uma tabela de histórico grande e sempre crescente pode se tornar um problema devido aos custos puros de armazenamento, além de impor um imposto de desempenho sobre as consultas temporais.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="ed8c3-173">Portanto, o desenvolvimento de uma política de retenção de dados para o gerenciamento de dados na tabela de histórico é um aspecto importante do planejamento e do gerenciamento do ciclo de vida de cada tabela temporal.</span><span class="sxs-lookup"><span data-stu-id="ed8c3-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="ed8c3-174">Com o Banco de Dados SQL do Azure, você tem as seguintes abordagens para o gerenciamento dos dados históricos na tabela temporal:</span><span class="sxs-lookup"><span data-stu-id="ed8c3-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="ed8c3-175">Particionamento de tabela</span><span class="sxs-lookup"><span data-stu-id="ed8c3-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="ed8c3-176">Script de Limpeza Personalizado</span><span class="sxs-lookup"><span data-stu-id="ed8c3-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="ed8c3-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed8c3-177">Next steps</span></span>
<span data-ttu-id="ed8c3-178">Para obter informações detalhadas sobre as Tabelas Temporais, confira a [documentação do MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="ed8c3-179">Visite o Channel 9 para ouvir uma [história de sucesso real de implementação temporal do cliente](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e assista uma [demonstração temporal dinâmica](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="ed8c3-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

