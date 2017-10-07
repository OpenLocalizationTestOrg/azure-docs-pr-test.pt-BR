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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Código de destino do Arquivo de evento para eventos estendidos no Banco de Dados SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Você deseja um exemplo de código completo para informações de toocapture e relatório de maneira robusta para um evento estendido.

No Microsoft SQL Server, Olá [destino de arquivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) é usado toostore saídas de eventos em um arquivo de disco rígido local. Mas esses arquivos não estão disponível tooAzure banco de dados SQL. Em vez disso, usamos o destino de arquivo de evento Olá do toosupport de serviço de armazenamento do Azure hello.

Este tópico apresenta um exemplo de código em duas fases:

* PowerShell, um contêiner de armazenamento do Azure na nuvem de saudação do toocreate.
* Transact-SQL:
  
  * destino de arquivo de evento do tooan contêiner do tooassign Olá armazenamento do Azure.
  * toocreate e reinicie a sessão de evento Olá e assim por diante.

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta e uma assinatura do Azure. Você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Qualquer banco de dados no qual você possa criar uma tabela.
  
  * Como alternativa, você pode [criar um banco de dados de demonstração do **AdventureWorksLT**](sql-database-get-started.md) em questão minutos.
* O SQL Server Management Studio (ssms.exe), idealmente na sua versão de atualização mensal mais recente. 
  Você pode baixar Olá o ssms.exe mais recentes de:
  
  * Tópico [Baixar o SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Download de toohello um link direto.](http://go.microsoft.com/fwlink/?linkid=616025)
* Você deve ter Olá [módulos do PowerShell do Azure](http://go.microsoft.com/?linkid=9811175) instalado.
  
  * módulos de saudação fornecem comandos como - **AzureStorageAccount novo**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Fase 1: código do PowerShell para o contêiner de Armazenamento do Azure

Este PowerShell é a fase 1 Olá em duas fases do exemplo de código.

script Hello é iniciado com comandos tooclean depois de uma possível anterior executar e rerunnable.

1. Cole o script do PowerShell Olá em um editor de texto simples como Notepad.exe e salve o script hello como um arquivo com extensão Olá **. ps1**.
2. Inicie o ISE do PowerShell como Administrador.
3. No prompt de hello, digite<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>e pressione Enter.
4. No ISE do PowerShell, abra seu arquivo **.ps1** . Execute o script hello.
5. script Hello iniciado pela primeira vez uma nova janela na qual você fez logon no tooAzure.
   
   * Se você executar novamente o script hello sem interromper a sessão, você tem a opção de conveniente de saudação do comentando Olá **Add-AzureAccount** comando.

![ISE do PowerShell, com o módulo do Azure instalado, script toorun pronto.][30_powershell_ise]


### <a name="powershell-code"></a>Código do PowerShell

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


Anote Olá alguns valores nomeados que o script do PowerShell Olá imprime quando ele termina. Você deve editar esses valores em Olá script Transact-SQL que segue a fase 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Fase 2: código Transact-SQL que usa o contêiner de Armazenamento do Azure

* Na etapa 1 deste exemplo de código, você executou um toocreate de script do PowerShell um contêiner de armazenamento do Azure.
* Em seguida na fase 2, hello script Transact-SQL a seguir deve usar o contêiner de saudação.

script Hello é iniciado com comandos tooclean depois de uma possível anterior executar e rerunnable.

Olá script do PowerShell impressas alguns valores nomeados quando ele foi encerrado. Você deve editar Olá Transact-SQL script toouse esses valores. Localizar **TODO** saudação do hello Transact-SQL script toolocate Editar pontos.

1. Abra o SQL Server Management Studio (ssms.exe).
2. Conecte-se o banco de dados do tooyour banco de dados SQL.
3. Clique em tooopen um novo painel de consulta.
4. Colar Olá script Transact-SQL a seguir no painel de consulta hello.
5. Localizar cada **TODO** em Olá script e faça edições de saudação apropriado.
6. Salve e execute o script hello.


> [!WARNING]
> Olá valor de chave de SAS gerado pelo Olá precede o script do PowerShell pode começar com um '?' (ponto de interrogação). Quando você usa a chave de SAS Olá em Olá script T-SQL a seguir, você deve *remover à esquerda de saudação '?'* . Caso contrário, seus esforços poderão ser bloqueados pela segurança.


### <a name="transact-sql-code"></a>Transact-SQL code

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


Se o destino de saudação falhar tooattach quando você executa, pare e reinicie a sessão de evento hello:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Saída

Quando Olá script Transact-SQL é concluída, clique em uma célula em Olá **event_data_XML** cabeçalho de coluna. Um elemento **<event>** é exibido mostrando uma instrução UPDATE.

Veja um elemento **<event>** gerado durante o teste:


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


Olá Olá de script usado Transact-SQL anterior sistema função tooread Olá event_file a seguir:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Obter uma explicação das opções avançadas para a exibição de saudação de dados de eventos estendidos está disponível em:

* [Exibição avançada de dados de destino de eventos estendidos](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Convertendo Olá toorun de exemplo de código no SQL Server

Suponha que você desejava Olá toorun precede o exemplo de Transact-SQL no Microsoft SQL Server.

* Para simplificar, você desejaria toocompletely substituir use hello Azure do contêiner de armazenamento com um arquivo simples como **C:\myeventdata.xel**. arquivo Hello seria toohello as unidade de disco rígido local do computador de Olá que hospeda o SQL Server.
* Você não precisaria de nenhuma variante de instrução Transact-SQL para **CREATE MASTER KEY** e **CREATE CREDENTIAL**.
* Em Olá **CREATE EVENT SESSION** instrução, no seu **Adicionar destino** cláusula, você poderia substituir valor de Http Olá atribuído feitas muito**filename =** com uma cadeia de caracteres de caminho completo como  **C:\myfile.xel**.
  
  * Não é necessário envolver qualquer conta de Armazenamento do Azure.

## <a name="more-information"></a>Mais informações

Para obter mais informações sobre contas e os contêineres Olá serviço de armazenamento do Azure, consulte:

* [Como toouse armazenamento de BLOBs no .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Nomeando e referenciando contêineres, blobs e metadados](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Trabalhando com hello contêiner raiz](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

