---
title: "Código do Arquivo de Evento de XEvent para o Banco de Dados SQL | Microsoft Docs"
description: "Fornece PowerShell e Transact-SQL para um exemplo de código de duas fases que demonstra o destino de Arquivo de evento em um evento estendido no Banco de Dados SQL do Azure. O Armazenamento do Azure é uma parte obrigatória deste cenário."
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
ms.openlocfilehash: e8c7a9af11ac4c22be00426337ab7c8b8ff0860f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="8f899-104">Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="8f899-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="8f899-105">Você deseja um exemplo de código completo para uma maneira robusta de capturar e relatar informações para um evento estendido.</span><span class="sxs-lookup"><span data-stu-id="8f899-105">You want a complete code sample for a robust way to capture and report information for an extended event.</span></span>

<span data-ttu-id="8f899-106">No Microsoft SQL Server, o [destino de Arquivo de Evento](http://msdn.microsoft.com/library/ff878115.aspx) é usado para armazenar as saídas de eventos em um arquivo do disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="8f899-106">In Microsoft SQL Server, the [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used to store event outputs into a local hard drive file.</span></span> <span data-ttu-id="8f899-107">Porém, esses arquivos não estão disponíveis para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-107">But such files are not available to Azure SQL Database.</span></span> <span data-ttu-id="8f899-108">Em vez disso, usamos o serviço de Armazenamento do Azure para oferecer suporte ao destino de Arquivo de evento.</span><span class="sxs-lookup"><span data-stu-id="8f899-108">Instead we use the Azure Storage service to support the Event File target.</span></span>

<span data-ttu-id="8f899-109">Este tópico apresenta um exemplo de código em duas fases:</span><span class="sxs-lookup"><span data-stu-id="8f899-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="8f899-110">PowerShell, a fim de criar o contêiner de Armazenamento do Azure na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8f899-110">PowerShell, to create an Azure Storage container in the cloud.</span></span>
* <span data-ttu-id="8f899-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="8f899-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="8f899-112">Para atribuir o contêiner de Armazenamento do Azure a um destino de Arquivo de evento.</span><span class="sxs-lookup"><span data-stu-id="8f899-112">To assign the Azure Storage container to an Event File target.</span></span>
  * <span data-ttu-id="8f899-113">Para criar e iniciar a sessão de evento etc.</span><span class="sxs-lookup"><span data-stu-id="8f899-113">To create and start the event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f899-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f899-114">Prerequisites</span></span>

* <span data-ttu-id="8f899-115">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-115">An Azure account and subscription.</span></span> <span data-ttu-id="8f899-116">Você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f899-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8f899-117">Qualquer banco de dados no qual você possa criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8f899-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="8f899-118">Como alternativa, você pode [criar um banco de dados de demonstração do **AdventureWorksLT**](sql-database-get-started.md) em questão minutos.</span><span class="sxs-lookup"><span data-stu-id="8f899-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="8f899-119">O SQL Server Management Studio (ssms.exe), idealmente na sua versão de atualização mensal mais recente.</span><span class="sxs-lookup"><span data-stu-id="8f899-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="8f899-120">Você pode baixar o ssms.exe mais recente de:</span><span class="sxs-lookup"><span data-stu-id="8f899-120">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="8f899-121">Tópico [Baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f899-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="8f899-122">Um link direto para o download.</span><span class="sxs-lookup"><span data-stu-id="8f899-122">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="8f899-123">Você deve ter os [módulos do Azure PowerShell](http://go.microsoft.com/?linkid=9811175) instalados.</span><span class="sxs-lookup"><span data-stu-id="8f899-123">You must have the [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="8f899-124">Os módulos fornecem comandos como: **New-AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="8f899-124">The modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="8f899-125">Fase 1: código do PowerShell para o contêiner de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8f899-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="8f899-126">Esse PowerShell é a fase 1 do exemplo de código de duas fases.</span><span class="sxs-lookup"><span data-stu-id="8f899-126">This PowerShell is phase 1 of the two-phase code sample.</span></span>

<span data-ttu-id="8f899-127">O script começa com comandos para limpeza após uma possível execução anterior e é reutilizável.</span><span class="sxs-lookup"><span data-stu-id="8f899-127">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="8f899-128">Cole o script do PowerShell em um editor de texto simples, como o Notepad.exe, e salve o script como um arquivo com a extensão **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8f899-128">Paste the PowerShell script into a simple text editor such as Notepad.exe, and save the script as a file with the extension **.ps1**.</span></span>
2. <span data-ttu-id="8f899-129">Inicie o ISE do PowerShell como Administrador.</span><span class="sxs-lookup"><span data-stu-id="8f899-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="8f899-130">No prompt, digite</span><span class="sxs-lookup"><span data-stu-id="8f899-130">At the prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="8f899-131">e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="8f899-131">and then press Enter.</span></span>
4. <span data-ttu-id="8f899-132">No ISE do PowerShell, abra seu arquivo **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="8f899-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="8f899-133">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="8f899-133">Run the script.</span></span>
5. <span data-ttu-id="8f899-134">Primeiro, o script inicia uma nova janela para efetuar logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-134">The script first starts a new window in which you log in to Azure.</span></span>
   
   * <span data-ttu-id="8f899-135">Se você executar novamente o script sem interromper a sessão, terá a opção conveniente de comentar o comando **Add-AzureAccount** .</span><span class="sxs-lookup"><span data-stu-id="8f899-135">If you rerun the script without disrupting your session, you have the convenient option of commenting out the **Add-AzureAccount** command.</span></span>

![ISE do PowerShell, com o módulo do Azure instalado e pronto para executar o script.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="8f899-137">Código do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f899-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after the first run.
# Current PowerShell environment retains the successful outcome.

'Expect a pop-up window in which you log in to Azure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit the values assigned to these variables, especially the first few!
'

# Ensure the current date is between
# the Expiry and Start time values that you edit here.

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


# The ending display lists your Azure subscriptions.
# One should match the $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for the current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up the old Azure Storage Account after any previous run, 
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
Get the primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# The context will be needed to create a container within the storage account.

'Create a context object from the storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within the storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy to be applied to the SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for the container.
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


'Display the values that YOU must edit into the Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here to delete your Azure Storage account. See the preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift to the Transact-SQL portion of the two-part code sample!'

# EOFile
```


<span data-ttu-id="8f899-138">Anote os valores nomeados que o script do PowerShell imprime quando termina.</span><span class="sxs-lookup"><span data-stu-id="8f899-138">Take note of the few named values that the PowerShell script prints when it ends.</span></span> <span data-ttu-id="8f899-139">Você deve editar esses valores no script Transact-SQL na fase 2.</span><span class="sxs-lookup"><span data-stu-id="8f899-139">You must edit those values into the Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="8f899-140">Fase 2: código Transact-SQL que usa o contêiner de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8f899-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="8f899-141">Na fase 1 deste exemplo de código, você executou um script PowerShell para criar um contêiner de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-141">In phase 1 of this code sample, you ran a PowerShell script to create an Azure Storage container.</span></span>
* <span data-ttu-id="8f899-142">Em seguida na fase 2, o script Transact-SQL a seguir deverá usar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="8f899-142">Next in phase 2, the following Transact-SQL script must use the container.</span></span>

<span data-ttu-id="8f899-143">O script começa com comandos para limpeza após uma possível execução anterior e é reutilizável.</span><span class="sxs-lookup"><span data-stu-id="8f899-143">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="8f899-144">O script PowerShell imprimiu alguns valores nomeados quando terminou.</span><span class="sxs-lookup"><span data-stu-id="8f899-144">The PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="8f899-145">Você precisa editar o script Transact-SQL a fim de usar esses valores.</span><span class="sxs-lookup"><span data-stu-id="8f899-145">You must edit the Transact-SQL script to use those values.</span></span> <span data-ttu-id="8f899-146">Localize **TODO** no script Transact-SQL para localizar os pontos de edição.</span><span class="sxs-lookup"><span data-stu-id="8f899-146">Find **TODO** in the Transact-SQL script to locate the edit points.</span></span>

1. <span data-ttu-id="8f899-147">Abra o SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="8f899-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="8f899-148">Conecte-se ao seu Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-148">Connect to your Azure SQL Database database.</span></span>
3. <span data-ttu-id="8f899-149">Clique para abrir um novo painel de consulta.</span><span class="sxs-lookup"><span data-stu-id="8f899-149">Click to open a new query pane.</span></span>
4. <span data-ttu-id="8f899-150">Cole o script Transact-SQL a seguir no painel de consulta.</span><span class="sxs-lookup"><span data-stu-id="8f899-150">Paste the following Transact-SQL script into the query pane.</span></span>
5. <span data-ttu-id="8f899-151">Localize todos os **TODO** no script e faça as edições apropriadas.</span><span class="sxs-lookup"><span data-stu-id="8f899-151">Find every **TODO** in the script and make the appropriate edits.</span></span>
6. <span data-ttu-id="8f899-152">Salve e execute o script.</span><span class="sxs-lookup"><span data-stu-id="8f899-152">Save, and then run the script.</span></span>


> [!WARNING]
> <span data-ttu-id="8f899-153">O valor da chave de SAS gerada pelo script do PowerShell anterior pode começar com um '?' (ponto de interrogação).</span><span class="sxs-lookup"><span data-stu-id="8f899-153">The SAS key value generated by the preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="8f899-154">Quando você usa a chave de SAS no script T-SQL a seguir, deve *remover os '?' iniciais*.</span><span class="sxs-lookup"><span data-stu-id="8f899-154">When you use the SAS key in the following T-SQL script, you must *remove the leading '?'*.</span></span> <span data-ttu-id="8f899-155">Caso contrário, seus esforços poderão ser bloqueados pela segurança.</span><span class="sxs-lookup"><span data-stu-id="8f899-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="8f899-156">Transact-SQL code</span><span class="sxs-lookup"><span data-stu-id="8f899-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run the PowerShell portion of this two-part code sample.
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
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in the long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  The event session has an event with an action,
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
            -- TODO: Assign AzureStorageAccount name, and the associated Container name.
            -- Also, tweak the .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start the event session.  ----------------
------  Issue the SQL Update statements that will be traced.
------  Then stop the session.

------  Note: If the target fails to attach,
------  the session must be stopped and restarted.

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


-------------- Step 5.  Select the results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and the associated Container name.
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
    -- TODO: Assign AzureStorageAccount name, and the associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount to delete your Azure Storage account!';
GO
```


<span data-ttu-id="8f899-157">Se o destino não for anexado durante a execução, você deverá parar e reiniciar a sessão de eventos:</span><span class="sxs-lookup"><span data-stu-id="8f899-157">If the target fails to attach when you run, you must stop and restart the event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="8f899-158">Saída</span><span class="sxs-lookup"><span data-stu-id="8f899-158">Output</span></span>

<span data-ttu-id="8f899-159">Após a conclusão do script Transact-SQL, clique em uma célula sob o cabeçalho da coluna **event_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="8f899-159">When the Transact-SQL script completes, click a cell under the **event_data_XML** column header.</span></span> <span data-ttu-id="8f899-160">Um elemento **<event>** é exibido mostrando uma instrução UPDATE.</span><span class="sxs-lookup"><span data-stu-id="8f899-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="8f899-161">Veja um elemento **<event>** gerado durante o teste:</span><span class="sxs-lookup"><span data-stu-id="8f899-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="8f899-162">O script Transact-SQL anterior usou a função de sistema a seguir para ler event_file:</span><span class="sxs-lookup"><span data-stu-id="8f899-162">The preceding Transact-SQL script used the following system function to read the event_file:</span></span>

* [<span data-ttu-id="8f899-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="8f899-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="8f899-164">Há uma explicação das opções avançadas para a visualização de dados de eventos estendidos disponível em:</span><span class="sxs-lookup"><span data-stu-id="8f899-164">An explanation of advanced options for the viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="8f899-165">Exibição avançada de dados de destino de eventos estendidos</span><span class="sxs-lookup"><span data-stu-id="8f899-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-the-code-sample-to-run-on-sql-server"></a><span data-ttu-id="8f899-166">Convertendo o exemplo de código para execução no SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f899-166">Converting the code sample to run on SQL Server</span></span>

<span data-ttu-id="8f899-167">Vamos supor que você queira executar o exemplo anterior de Transact-SQL no Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f899-167">Suppose you wanted to run the preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="8f899-168">Para manter a simplicidade, convém substituir completamente o uso do contêiner de Armazenamento do Azure por um arquivo simples, como **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="8f899-168">For simplicity, you would want to completely replace use of the Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="8f899-169">O arquivo seria gravado no disco rígido local do computador que hospeda o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f899-169">The file would be written to the local hard drive of the computer that hosts SQL Server.</span></span>
* <span data-ttu-id="8f899-170">Você não precisaria de nenhuma variante de instrução Transact-SQL para **CREATE MASTER KEY** e **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="8f899-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="8f899-171">Na instrução **CREATE EVENT SESSION**, em sua cláusula **ADD TARGET**, você pode substituir o valor de Http atribuído a **filename=** por uma cadeia de caracteres de caminho completo, como **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="8f899-171">In the **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace the Http value assigned made to **filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="8f899-172">Não é necessário envolver qualquer conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f899-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="8f899-173">Mais informações</span><span class="sxs-lookup"><span data-stu-id="8f899-173">More information</span></span>

<span data-ttu-id="8f899-174">Para saber mais sobre contas e contêineres no serviço de Armazenamento do Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="8f899-174">For more info about accounts and containers in the Azure Storage service, see:</span></span>

* [<span data-ttu-id="8f899-175">Como usar o Armazenamento de blob do .NET</span><span class="sxs-lookup"><span data-stu-id="8f899-175">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="8f899-176">Nomeando e referenciando contêineres, blobs e metadados</span><span class="sxs-lookup"><span data-stu-id="8f899-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="8f899-177">Trabalhando com o contêiner raiz</span><span class="sxs-lookup"><span data-stu-id="8f899-177">Working with the Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="8f899-178">Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure</span><span class="sxs-lookup"><span data-stu-id="8f899-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="8f899-179">Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="8f899-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

