---
title: "aaaAzure SQL Data Warehouse - Introdução tutorial | Microsoft Docs"
description: "Este tutorial ensina como tooprovision e carregar dados no Azure SQL Data Warehouse. Você também aprenderá noções básicas de saudação sobre dimensionamento, pausa e ajuste."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Introdução ao SQL Data Warehouse

Este tutorial mostra como tooprovision e carregar dados no Azure SQL Data Warehouse. Você também aprenderá noções básicas de saudação sobre dimensionamento, pausa e ajuste. Quando você terminar, você usará tooquery pronto e explorar seu data warehouse.

**Estimado tempo toocomplete:** este é um tutorial de ponta a ponta com o código de exemplo que usa toocomplete cerca de 30 minutos depois que você atingiu os pré-requisitos de saudação. 

## <a name="prerequisites"></a>Pré-requisitos

tutorial de saudação pressupõe que você esteja familiarizado com os conceitos básicos do SQL Data Warehouse. Se você precisar de uma introdução, consulte [O que é SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>Inscreva-se no Microsoft Azure
Se você ainda não tiver uma conta do Microsoft Azure, você precisa toosign para um toouse desse serviço. Se já tiver uma conta, você poderá ignorar esta etapa. 

1. Navegar pelas páginas de conta toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Crie uma conta gratuita do Azure ou uma conta de compra.
3. Siga as instruções de saudação

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Instalar os devidos drivers e ferramentas do cliente SQL

A maioria das ferramentas de cliente SQL pode se conectar a tooSQL Data Warehouse usando JDBC, ODBC ou ADO.NET. Devido a toohello grande número de recursos de T-SQL que oferece suporte a SQL Data Warehouse, alguns aplicativos cliente não são totalmente compatíveis com o SQL Data Warehouse.

Se você estiver executando um sistema operacional do Windows, recomendamos o uso do [Visual Studio] ou do [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Criar um SQL Data Warehouse

Um SQL Data Warehouse é um tipo especial de banco de dados que foi projetado para o processamento extremamente paralelo. banco de dados de saudação é distribuído em vários nós e processa consultas em paralelo. SQL Data Warehouse tem um nó de controle que orquestra as atividades de saudação de todos os nós de saudação. nós Olá se usam toomanage de banco de dados SQL seus dados.  

> [!NOTE]
> A criação de um SQL Data Warehouse pode resultar em um novo serviço faturável.  Para obter mais informações, confira [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Criar um data warehouse

1. O logon no hello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** > **Bancos de dados** > **SQL Data Warehouse**.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Preencher os detalhes da implantação

    **Nome do banco de dados**: escolha qualquer item que desejar. Se você tiver vários depósitos de dados, é recomendável que os nomes de incluem detalhes como região hello, ambiente, por exemplo *westus mydw-teste 1*.

    **Assinatura:** sua assinatura do Azure

    **Grupo de Recursos**: crie um grupo de recursos ou use um grupo de recursos existente.
    > [!NOTE]
    > Grupos de recursos são úteis para a administração de recursos como controle de acesso de escopo e implantação de modelo. Leia mais sobre grupos de recursos do Azure e as práticas recomendadas [aqui](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)

    **Origem**: banco de dados em branco

    **Servidor**: servidor de saudação selecione que você criou na [pré-requisitos].

    **Agrupamento**: deixe o agrupamento padrão de saudação SQL_Latin1_General_CP1_CI_AS.

    **Selecione desempenho**: É recomendável começar com 400DWU de saudação padrão.

4. Escolha **Pin toodashboard** ![tooDashboard de Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Aguarde e aguarde até que seu toodeploy de depósito de dados! É normal para este processo tootake vários minutos. portal de saudação notifica quando o data warehouse é toouse pronto. 

## <a name="connect-toosql-data-warehouse"></a>Conecte-se tooSQL do Data Warehouse

Este tutorial usa tooconnect toohello data warehouse de SQL Server Management Studio (SSMS). Você pode se conectar tooSQL Data Warehouse por esses conectores com suporte: ADO.NET, JDBC, ODBC e PHP. Lembre-se, a funcionalidade pode ser limitada para as ferramentas sem suporte pela Microsoft.


### <a name="get-connection-information"></a>Obter informações de conexão

data warehouse de tooconnect tooyour, você precisa tooconnect por meio de saudação lógico do SQL server criado na [pré-requisitos].

1. Selecione o data warehouse no painel de saudação ou procure-a em seus recursos.

    ![Painel do SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Localize o nome completo Olá Olá lógico do SQL server.

    ![Selecionar o nome do servidor](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Abra o SSMS e usar o objeto explorer tooconnect toothis server usando credenciais de administrador de servidor de saudação criado no [pré-requisitos]

    ![Conectar com SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Se tudo correr corretamente, você deve agora ser tooyour conectado lógica SQL server. Desde que você fez logon como Olá administrador do servidor, você pode se conectar a banco de dados de tooany hospedado pelo servidor de saudação, inclusive o banco de dados mestre hello. 

Há apenas um servidor conta de administrador e tem Olá a maioria dos privilégios de qualquer usuário. Tenha cuidado não tooallow muitas pessoas em sua senha de administrador organização tooknow hello. 

Você também pode ter uma conta do administrador do Azure Active Directory. Não fornecemos detalhes Olá aqui. Se você quiser toolearn mais sobre como usar a autenticação do Active Directory do Azure, consulte [autenticação do Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Em seguida, exploraremos a criação de logons e usuários adicionais.


## <a name="create-a-database-user"></a>Criar um usuário do banco de dados

Nesta etapa, você criará um tooaccess de conta de usuário o data warehouse. Também mostramos como toogive que toorun de capacidade de saudação do usuário consultas com uma grande quantidade de memória e recursos de CPU.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Observações sobre classes de recursos para alocar recursos tooqueries

- tookeep seus dados seguros, não use consultas de toorun de administração de servidor de saudação em seus bancos de dados de produção. Ele tem Olá a maioria dos privilégios de qualquer usuário e usá-lo tooperform operações nos dados de usuário coloca seus dados em risco. Além disso, desde que o administrador do servidor de saudação deve tooperform operações de gerenciamento, ele é executado operações com apenas uma pequena alocação de memória e recursos de CPU. 

- SQL Data Warehouse usa funções de banco de dados predefinido, chamado de classes de recursos, tooallocate diferentes quantidades de memória, os recursos de CPU e toousers de slots de simultaneidade. Cada usuário pode pertencer a classe de recurso de pequeno, médio, grande ou extra grande tooa. Olá classe de recurso do usuário determina Olá recursos Olá usuário tem toorun consultas e operações de carregamento.

- Para a compactação de dados ideal, Olá talvez ele tenha tooload com grande ou extra grande alocações. Leia mais sobre classes de recursos [aqui](./sql-data-warehouse-develop-concurrency.md#resource-classes):

### <a name="create-an-account-that-can-control-a-database"></a>Criar uma conta que pode controlar um banco de dados

Como você está conectado no Olá administrador do servidor, você tem permissões toocreate logons e usuários.

1. Usando o SSMS ou outro cliente de consulta, abra uma nova consulta para o **mestre**.

    ![Nova consulta no mestre](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nova consulta em Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. Na janela de consulta hello, execute este toocreate de comando T-SQL um logon denominado MedRCLogin e um usuário chamado LoadingUser. Este logon pode se conectar a toohello lógica SQL server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Consultar agora Olá *banco de dados do SQL Data Warehouse*, crie um usuário de banco de dados com base em Olá logon criado tooaccess e executar operações no banco de dados de saudação.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Atribuir Olá banco de dados usuário controle permissões toohello banco de dados chamado NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Se o nome do banco de dados contiver hifens, ser toowrap-se de que ele entre colchetes! 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Dê Olá usuário médio alocações

1. Execute este toomake de comando T-SQL it um membro da classe de recurso médios hello, que é chamado mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Clique em [aqui](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn mais sobre classes de simultaneidade e recursos! 
    >

2. Conecte-se o servidor lógico toohello com as novas credenciais Olá

    ![Fazer logon com o novo logon](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Carregar dados do armazenamento de blob do Azure

Agora você está dados tooload pronto para o data warehouse. Esta etapa mostra como dados de cab do tooload cidade de Nova York táxi de um armazenamento do Azure público de blob. 

- Uma maneira comum de dados tooload no SQL Data Warehouse são toofirst mover o armazenamento de blob Olá dados tooAzure e, em seguida, carregá-lo em seu data warehouse. toomake-lo mais fácil toounderstand como tooload, temos Nova York táxi cab dados já está hospedados em um blob de armazenamento do Azure públicos. 

- Para referência futura, toolearn como tooget tooAzure seus dados de blob de armazenamento ou tooload-lo diretamente da fonte no SQL Data Warehouse, consulte Olá [visão geral de carregamento](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Definir dados externos

1. Crie uma chave mestra. Você só precisa toocreate uma chave mestra de uma vez por banco de dados. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Defina o local de saudação do hello BLOBs do Azure que contém dados de cab táxi Olá.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Definir Olá formatos de arquivo externo

    Olá ```CREATE EXTERNAL FILE FORMAT``` comando é toospecify usado o formato de arquivos que contêm dados externos hello. Eles contêm texto separado por um ou mais caracteres denominados delimitadores. Para fins de demonstração, os dados de cab do táxi de saudação são armazenados como dados não compactados e dados gzip compactado.

    Execute esses comandos do T-SQL toodefine dois formatos diferentes: descompactado e compactado.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Crie um esquema para o formato de arquivo externo. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Crie hello tabelas externas. Essas tabelas fazem referência aos dados colocados no armazenamento de blobs do Azure. Execute Olá toocreate de comandos T-SQL a seguir várias tabelas externas que toohello de ponto de todos os BLOBs do Azure definimos anteriormente na nossa fonte de dados externa.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Importar dados de saudação do armazenamento de BLOBs do Azure.

O SQL Data Warehouse oferece suporte a uma instrução de chave chamada CREATE TABLE AS SELECT (CTAS). Essa instrução cria uma nova tabela com base nos resultados de saudação de uma instrução select. Olá nova tabela tem Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello.  Isso é um tooimport de maneira elegante de dados do armazenamento de BLOBs do Azure no SQL Data Warehouse.

1. Execute este script tooimport seus dados.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Exiba os dados enquanto eles são carregados.

   Você está carregando vários GBs de dados e compactando-os em índices columnstore de cluster de alto desempenho. Execute Olá consulta a seguir que usa um status de saudação do gerenciamento dinâmico DMVs (exibições) tooshow de carga hello. Depois de iniciar a consulta hello, pegue um café e um lanche enquanto SQL Data Warehouse faz algum trabalho pesado.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Exiba todas as consultas do sistema.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Veja os dados carregados sem problemas no Azure SQL Data Warehouse.

    ![Ver dados carregados](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Melhorar o desempenho da consulta

Há vários modos tooimprove consulta de desempenho e tooachieve Olá alta velocidade que o SQL Data Warehouse é projetada tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Consulte o efeito de saudação do dimensionamento de desempenho de consulta 

Desempenho de consulta de uma maneira tooimprove é tooscale recursos alterando o nível de serviço DWU Olá para o data warehouse. Cada nível de serviço custa mais, mas você pode reduzir ou pausar recursos a qualquer momento. 

Nesta etapa, você compara o desempenho em suas configurações diferentes de DWU.

Primeiro, vamos dimensionar dimensionamento Olá para baixo too100 DWU para obter uma ideia de como um nó de computação pode executar por conta própria.

1. Vá toohello portal e selecione seu SQL Data Warehouse.

2. Selecione escala na folha do hello SQL Data Warehouse. 

    ![Dimensionar DW no portal](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Reduzir o desempenho de saudação barra too100 DWU e clique em Salvar.

    ![Dimensionar e salvar](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Aguarde o toofinish de operação de escala.

    > [!NOTE]
    > Não é possível executar consultas ao alterar a escala de saudação. O dimensionamento **elimina** suas consultas em execução no momento. Você pode reiniciá-los quando Olá operação é concluída.
    >
    
5. Faça uma operação de verificação nos dados de viagem hello, selecionando Olá entradas principais de milhões para todas as colunas de saudação. Se você está adiantado toomove rapidamente, sinta-se livre tooselect menos linhas. Anote Olá tempo toorun esta operação.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Dimensionar seu data warehouse too400 DWU de volta. Lembre-se de que cada DWU 100 é adicionar outra tooyour de nó de computação do Azure SQL Data Warehouse.

7. Execute novamente a consulta de Olá! Você deve notar uma diferença significativa. 

    > [!NOTE]
    > Como consulta Olá retorna muitos dados, a disponibilidade de largura de banda de saudação da máquina Olá executando o SSMS pode ser um afunilamento de desempenho. Isso pode resultar em nenhuma melhoria de desempenho!

> [!NOTE]
> Como o SQL Data Warehouse usa processamento paralelo massivo. As consultas que digitalizar ou executam funções analíticas em milhões de linhas sofrer verdadeiro poder saudação do Azure SQL Data Warehouse.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Ver o efeito de saudação de estatísticas sobre o desempenho de consulta

1. Executar uma consulta de junções Olá tabela de data por viagem Olá

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Essa consulta demorada porque o SQL Data Warehouse tem dados tooshuffle antes de executar associação de saudação. Junções não têm dados tooshuffle se forem dados toojoin projetado Olá mesma forma que ele seja distribuído. Esse é um assunto mais profundo. 

2. Estatísticas fazem a diferença. 
3. Execute essa instrução de estatísticas de toocreate em colunas de junção hello.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > O SQL DW não gerencia automaticamente as estatísticas para você. As estatísticas são importantes para o desempenho da consulta, e é altamente recomendável criar e atualizar as estatísticas.
    > 
    > **Você obtém maior benefício Olá fazendo com que as estatísticas em colunas envolvidas em relações, colunas usadas em Olá onde cláusula e colunas encontrado no GROUP BY.**
    >

3. Execute a consulta de saudação de pré-requisitos novamente e observar as diferenças de desempenho. Enquanto não será drásticas quanto o dimensionamento das diferenças de saudação de desempenho de consulta, você deve observar uma velocidade. 

## <a name="next-steps"></a>Próximas etapas

Você agora está pronto tooquery e explora. Confira nossas melhores práticas recomendadas ou dicas.

Se você está explorando por dia hello, torne toopause-se de que sua instância! Em produção, você pode experimentar grande economia, pausa e dimensionamento toomeet suas necessidades de negócios.

![Pausar](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Leituras úteis

[Gerenciamento de simultaneidade e carga de trabalho][]

[Práticas recomendadas para o Azure SQL Data Warehouse][]

[Consultar monitoramento][]

[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala][]

[Migrando dados tooAzure SQL Data Warehouse][]

[Gerenciamento de simultaneidade e carga de trabalho]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Práticas recomendadas para o Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Consultar monitoramento]: sql-data-warehouse-manage-monitor.md
[Dez principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrando dados tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[pré-requisitos]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
