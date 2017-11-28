---
title: "código do arquivo de evento para o banco de dados SQL do aaaXEvent | Microsoft Docs"
description: "Fornece o PowerShell e Transact-SQL para obter um exemplo de código em duas fases que demonstra o destino de arquivo de evento de saudação em um evento estendido no banco de dados do SQL Azure. O Armazenamento do Azure é uma parte obrigatória deste cenário."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="e1d60-104">Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="e1d60-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="e1d60-105">Você deseja um exemplo de código completo para informações de toocapture e relatório de maneira robusta para um evento estendido.</span><span class="sxs-lookup"><span data-stu-id="e1d60-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="e1d60-106">No Microsoft SQL Server, Olá [destino de arquivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) é usado toostore saídas de eventos em um arquivo de disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="e1d60-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="e1d60-107">Mas esses arquivos não estão disponível tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e1d60-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="e1d60-108">Em vez disso, usamos o destino de arquivo de evento Olá do toosupport de serviço de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e1d60-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="e1d60-109">Este tópico apresenta um exemplo de código em duas fases:</span><span class="sxs-lookup"><span data-stu-id="e1d60-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="e1d60-110">PowerShell, um contêiner de armazenamento do Azure na nuvem de saudação do toocreate.</span><span class="sxs-lookup"><span data-stu-id="e1d60-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="e1d60-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="e1d60-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="e1d60-112">destino de arquivo de evento do tooan contêiner do tooassign Olá armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d60-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="e1d60-113">toocreate e reinicie a sessão de evento Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="e1d60-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1d60-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1d60-114">Prerequisites</span></span>

* <span data-ttu-id="e1d60-115">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d60-115">An Azure account and subscription.</span></span> <span data-ttu-id="e1d60-116">Você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1d60-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e1d60-117">Qualquer banco de dados no qual você possa criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e1d60-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="e1d60-118">Como alternativa, você pode [criar um banco de dados de demonstração do **AdventureWorksLT**](sql-database-get-started.md) em questão minutos.</span><span class="sxs-lookup"><span data-stu-id="e1d60-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="e1d60-119">O SQL Server Management Studio (ssms.exe), idealmente na sua versão de atualização mensal mais recente.</span><span class="sxs-lookup"><span data-stu-id="e1d60-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="e1d60-120">Você pode baixar Olá o ssms.exe mais recentes de:</span><span class="sxs-lookup"><span data-stu-id="e1d60-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="e1d60-121">Tópico [Baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1d60-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="e1d60-122">Download de toohello um link direto.</span><span class="sxs-lookup"><span data-stu-id="e1d60-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="e1d60-123">Você deve ter Olá [módulos do PowerShell do Azure](http://go.microsoft.com/?linkid=9811175) instalado.</span><span class="sxs-lookup"><span data-stu-id="e1d60-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="e1d60-124">módulos de saudação fornecem comandos como - **AzureStorageAccount novo**.</span><span class="sxs-lookup"><span data-stu-id="e1d60-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="e1d60-125">Fase 1: código do PowerShell para o contêiner de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e1d60-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="e1d60-126">Este PowerShell é a fase 1 Olá em duas fases do exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="e1d60-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="e1d60-127">script Hello é iniciado com comandos tooclean depois de uma possível anterior executar e rerunnable.</span><span class="sxs-lookup"><span data-stu-id="e1d60-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="e1d60-128">Cole o script do PowerShell Olá em um editor de texto simples como Notepad.exe e salve o script hello como um arquivo com extensão Olá **. ps1**.</span><span class="sxs-lookup"><span data-stu-id="e1d60-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="e1d60-129">Inicie o ISE do PowerShell como Administrador.</span><span class="sxs-lookup"><span data-stu-id="e1d60-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="e1d60-130">No prompt de hello, digite</span><span class="sxs-lookup"><span data-stu-id="e1d60-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="e1d60-131">e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="e1d60-131">and then press Enter.</span></span>
4. <span data-ttu-id="e1d60-132">No ISE do PowerShell, abra seu arquivo **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="e1d60-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="e1d60-133">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="e1d60-133">Run hello script.</span></span>
5. <span data-ttu-id="e1d60-134">script Hello iniciado pela primeira vez uma nova janela na qual você fez logon no tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1d60-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="e1d60-135">Se você executar novamente o script hello sem interromper a sessão, você tem a opção de conveniente de saudação do comentando Olá **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="e1d60-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![ISE do PowerShell, com o módulo do Azure instalado, script toorun pronto.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="e1d60-137">Código do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1d60-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="e1d60-138">Anote Olá alguns valores nomeados que o script do PowerShell Olá imprime quando ele termina.</span><span class="sxs-lookup"><span data-stu-id="e1d60-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="e1d60-139">Você deve editar esses valores em Olá script Transact-SQL que segue a fase 2.</span><span class="sxs-lookup"><span data-stu-id="e1d60-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="e1d60-140">Fase 2: código Transact-SQL que usa o contêiner de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e1d60-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="e1d60-141">Na etapa 1 deste exemplo de código, você executou um toocreate de script do PowerShell um contêiner de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d60-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="e1d60-142">Em seguida na fase 2, hello script Transact-SQL a seguir deve usar o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1d60-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="e1d60-143">script Hello é iniciado com comandos tooclean depois de uma possível anterior executar e rerunnable.</span><span class="sxs-lookup"><span data-stu-id="e1d60-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="e1d60-144">Olá script do PowerShell impressas alguns valores nomeados quando ele foi encerrado.</span><span class="sxs-lookup"><span data-stu-id="e1d60-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="e1d60-145">Você deve editar Olá Transact-SQL script toouse esses valores.</span><span class="sxs-lookup"><span data-stu-id="e1d60-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="e1d60-146">Localizar **TODO** saudação do hello Transact-SQL script toolocate Editar pontos.</span><span class="sxs-lookup"><span data-stu-id="e1d60-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="e1d60-147">Abra o SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="e1d60-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="e1d60-148">Conecte-se o banco de dados do tooyour banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e1d60-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="e1d60-149">Clique em tooopen um novo painel de consulta.</span><span class="sxs-lookup"><span data-stu-id="e1d60-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="e1d60-150">Colar Olá script Transact-SQL a seguir no painel de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="e1d60-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="e1d60-151">Localizar cada **TODO** em Olá script e faça edições de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="e1d60-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="e1d60-152">Salve e execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="e1d60-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="e1d60-153">Olá valor de chave de SAS gerado pelo Olá precede o script do PowerShell pode começar com um '?' (ponto de interrogação).</span><span class="sxs-lookup"><span data-stu-id="e1d60-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="e1d60-154">Quando você usa a chave de SAS Olá em Olá script T-SQL a seguir, você deve *remover à esquerda de saudação '?'* .</span><span class="sxs-lookup"><span data-stu-id="e1d60-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="e1d60-155">Caso contrário, seus esforços poderão ser bloqueados pela segurança.</span><span class="sxs-lookup"><span data-stu-id="e1d60-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="e1d60-156">Transact-SQL code</span><span class="sxs-lookup"><span data-stu-id="e1d60-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="e1d60-157">Se o destino de saudação falhar tooattach quando você executa, pare e reinicie a sessão de evento hello:</span><span class="sxs-lookup"><span data-stu-id="e1d60-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="e1d60-158">Saída</span><span class="sxs-lookup"><span data-stu-id="e1d60-158">Output</span></span>

<span data-ttu-id="e1d60-159">Quando Olá script Transact-SQL é concluída, clique em uma célula em Olá **event_data_XML** cabeçalho de coluna.</span><span class="sxs-lookup"><span data-stu-id="e1d60-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="e1d60-160">Um elemento **<event>** é exibido mostrando uma instrução UPDATE.</span><span class="sxs-lookup"><span data-stu-id="e1d60-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="e1d60-161">Veja um elemento **<event>** gerado durante o teste:</span><span class="sxs-lookup"><span data-stu-id="e1d60-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="e1d60-162">Olá Olá de script usado Transact-SQL anterior sistema função tooread Olá event_file a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1d60-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="e1d60-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="e1d60-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="e1d60-164">Obter uma explicação das opções avançadas para a exibição de saudação de dados de eventos estendidos está disponível em:</span><span class="sxs-lookup"><span data-stu-id="e1d60-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="e1d60-165">Exibição avançada de dados de destino de eventos estendidos</span><span class="sxs-lookup"><span data-stu-id="e1d60-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="e1d60-166">Convertendo Olá toorun de exemplo de código no SQL Server</span><span class="sxs-lookup"><span data-stu-id="e1d60-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="e1d60-167">Suponha que você desejava Olá toorun precede o exemplo de Transact-SQL no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e1d60-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="e1d60-168">Para simplificar, você desejaria toocompletely substituir use hello Azure do contêiner de armazenamento com um arquivo simples como **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="e1d60-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="e1d60-169">arquivo Hello seria toohello as unidade de disco rígido local do computador de Olá que hospeda o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e1d60-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="e1d60-170">Você não precisaria de nenhuma variante de instrução Transact-SQL para **CREATE MASTER KEY** e **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="e1d60-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="e1d60-171">Em Olá **CREATE EVENT SESSION** instrução, no seu **Adicionar destino** cláusula, você poderia substituir valor de Http Olá atribuído feitas muito**filename =** com uma cadeia de caracteres de caminho completo como  **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="e1d60-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="e1d60-172">Não é necessário envolver qualquer conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d60-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="e1d60-173">Mais informações</span><span class="sxs-lookup"><span data-stu-id="e1d60-173">More information</span></span>

<span data-ttu-id="e1d60-174">Para obter mais informações sobre contas e os contêineres Olá serviço de armazenamento do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="e1d60-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="e1d60-175">Como toouse armazenamento de BLOBs no .NET</span><span class="sxs-lookup"><span data-stu-id="e1d60-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e1d60-176">Nomeando e referenciando contêineres, blobs e metadados</span><span class="sxs-lookup"><span data-stu-id="e1d60-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="e1d60-177">Trabalhando com hello contêiner raiz</span><span class="sxs-lookup"><span data-stu-id="e1d60-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="e1d60-178">Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="e1d60-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="e1d60-179">Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="e1d60-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

