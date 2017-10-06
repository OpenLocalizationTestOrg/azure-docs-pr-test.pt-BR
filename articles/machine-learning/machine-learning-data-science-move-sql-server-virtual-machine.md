---
title: "aaaMove dados tooSQL Server em uma máquina virtual do Azure | Microsoft Docs"
description: Move os dados de arquivos simples ou de um tooSQL do SQL Server local Server na VM do Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Mover dados tooSQL Server em uma máquina virtual do Azure
Este tópico descreve as opções de saudação de movimentação de dados de arquivos simples (formatos CSV ou TSV) ou de um tooSQL do SQL Server local Server em uma máquina virtual do Azure. Essas tarefas para mover dados na nuvem toohello fazem parte da saudação processo de ciência de dados de equipe.

Para um tópico que descreve as opções de saudação para mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md).

Olá **menu** abaixo tootopics links que descrevem como dados tooingest em outros ambientes de destino onde os dados saudação podem ser armazenados e processados durante Olá processo de ciência de dados da equipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Olá tabela a seguir resume as opções de saudação para mover dados tooSQL Server em uma máquina virtual do Azure.

| <b>FONTE</b> | <b>DESTINO: SQL Server na VM do Azure</b> |
| --- | --- |
| <b>Arquivo simples</b> |1. <a href="#insert-tables-bcp">Utilitário de BCP (cópia em massa de linha de comando)</a><br> 2. <a href="#insert-tables-bulkquery">Consulta SQL de inserção em massa </a><br> 3. <a href="#sql-builtin-utilities">Utilitários gráficos internos no SQL Server</a> |
| <b>SQL Server local</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server</a><br> 2. <a href="#export-flat-file">Exportar tooa simples de arquivo</a><br> 3. <a href="#sql-migration">Assistente de Migração de Banco de Dados SQL</a> <br> 4. <a href="#sql-backup">Backup e restauração de banco de dados</a><br> |

Observe que este documento pressupõe que os comandos SQL sejam executados no SQL Server Management Studio ou no Gerenciador de Banco de Dados do Visual Studio.

> [!TIP]
> Como alternativa, você pode usar [do Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate e agendar um pipeline que irá mover dados tooa VM do SQL Server no Azure. Para obter mais informações, consulte [Copiar dados com o Azure Data Factory (Atividade de Cópia)](../data-factory/data-factory-data-movement-activities.md).
>
>

## <a name="prereqs"></a>Pré-requisitos
Este tutorial presume que você tenha:

* Uma **assinatura do Azure**. Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Uma **conta de armazenamento do Azure**. Você usará uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial. Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo. Depois que você criou a conta de armazenamento hello, você precisará conta de saudação tooobtain chave usada tooaccess armazenamento de saudação. Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* **SQL Server em uma VM do Azure**provisionado. Para obter instruções, consulte [Configurar uma máquina virtual do SQL Server do Azure como um servidor do IPython Notebook para análises avançadas](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* **Azure PowerShell** instalado e configurado localmente. Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Movimentação de dados de uma fonte de arquivo simples tooSQL Server em uma VM do Azure
Se os dados estiverem em um arquivo simples (organizado em um formato de linha ou coluna), ele pode ser movido tooSQL Server VM no Azure por meio de saudação métodos a seguir:

1. [Utilitário de BCP (cópia em massa de linha de comando)](#insert-tables-bcp)
2. [Consulta SQL de inserção em massa ](#insert-tables-bulkquery)
3. [Utilitários gráficos internos no SQL Server (Importar/Exportar, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Utilitário de BCP (cópia em massa de linha de comando)
BCP é um utilitário de linha de comando instalado com o SQL Server e é um dos dados de toomove maneiras mais rápidos de saudação. Ele funciona em todas as três variantes do SQL Server (SQL Server local, SQL Azure e VM do SQL Server no Azure).

> [!NOTE]
> **Onde os dados devem estar para o BCP?**  
> Embora não seja necessário, com arquivos que contêm dados de origem localizados no mesmo computador que o SQL Server de destino Olá permite transferências mais rápidas (velocidade vs local disco rede velocidade de e/s) de saudação. Você pode mover Olá simples arquivos contendo máquina toohello de dados onde o SQL Server está instalado usando cópia de arquivo de várias ferramentas, como [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) ou copie/cole do windows via remoto Protocolo de área de trabalho (RDP).
>
>

1. Certifique-se de que banco de dados de saudação e tabelas de saudação são criadas no banco de dados do SQL Server Olá destino. Aqui está um exemplo de como toodo que usar Olá `Create Database` e `Create Table` comandos:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Gere Olá arquivo de formato que descreve o esquema Olá Olá da tabela emitindo Olá comando a seguir de saudação de linha de comando da máquina Olá onde bcp está instalado.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Inserir dados de saudação no banco de dados de saudação usando o comando bcp de saudação da seguinte maneira. Supondo que hello do SQL Server está instalado no mesmo computador, isso deve funcionar de saudação de linha de comando:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Otimizando BCP insere** consulte Olá artigo a seguir ['Diretrizes para otimizar importação'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize tal insere.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Paralelização de inserções para movimentação de dados mais rápida
Se dados Olá que você está movendo forem grandes, você pode acelerar as coisas executando vários comandos BCP ao mesmo tempo em paralelo em um Script do PowerShell.

> [!NOTE]
> **Ingestão de grandes dados** toooptimize dados carregando para conjuntos de dados grandes e muito grande, partição suas tabelas de banco de dados lógico e físico usando várias tabelas de grupos de arquivos e de partição. Para obter mais informações sobre como criar e carregar dados toopartition tabelas, consulte [tabelas de partição do SQL carga paralela](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Olá abaixo de script do PowerShell de exemplo demonstram paralelas inserções usando bcp:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Consulta SQL de inserção em massa
[Em massa inserir consulta do SQL](https://msdn.microsoft.com/library/ms188365) podem ser usados tooimport dados no banco de dados de saudação de arquivos com base em linha ou coluna (Olá suporte para tipos são abordados a[preparar dados para exportação em massa ou importar (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tópico.

Aqui estão alguns comandos de exemplo para inserção em massa:  

1. Analisar os dados e definir opções personalizadas antes de importar toomake se que supõe que esse banco de dados do SQL Server Olá Olá mesmo formato para os campos especiais, como datas. Aqui está um exemplo de como data de saudação tooset Formatar como ano-mês-dia (se seus dados contiverem date de hello no formato ano-mês-dia):

        SET DATEFORMAT ymd;    
2. Importe dados usando as instruções de importação em massa:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Utilitários internos no SQL Server
Você pode usar dados do SQL Server integrações Services (SSIS) tooimport em VM do SQL Server no Azure de um arquivo simples.
O SSIS está disponível em dois ambientes de estúdio. Para obter detalhes, consulte [Ambientes do Integration Services (SSIS) e Estúdio](https://technet.microsoft.com/library/ms140028.aspx):

* Para obter detalhes sobre SQL Server Data Tools, consulte [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* Para obter detalhes sobre o Assistente de importação/exportação de saudação, consulte [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Movimentação de dados de local do SQL Server tooSQL Server em uma VM do Azure
Você também pode usar o hello estratégias de migração a seguir:

1. [Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [Exportar arquivo de tooFlat](#export-flat-file)
3. [Assistente de Migração de Banco de Dados SQL](#sql-migration)
4. [Backup e restauração de banco de dados](#sql-backup)

Descrevemos cada um deles abaixo:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server
Olá **implantar um Assistente de VM do Microsoft Azure do banco de dados do SQL Server tooa** é um modo simples e recomendada toomove os dados de um tooSQL de instância do SQL Server local Server em uma VM do Azure. Para obter etapas detalhadas, bem como uma discussão sobre outras alternativas, consulte [migrar um banco de dados tooSQL Server em uma VM do Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>Exportar arquivo de tooFlat
Vários métodos podem ser usado toobulk exportar dados do servidor SQL local conforme documentado no hello [importação e exportação de dados (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tópico. Este documento aborda Olá programa de cópia em massa (BCP) como um exemplo. Quando dados são exportados em um arquivo simples, ele poderá ser importado tooanother SQL server usando a importação em massa.

1. Exportar dados de saudação do local do SQL Server tooa arquivo usando o utilitário bcp de saudação da seguinte maneira

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Criar banco de dados de saudação e a tabela de saudação na VM do SQL Server no Azure usando Olá `create database` e `create table` para o esquema da tabela Olá exportada na etapa 1.
3. Crie um arquivo de formato para descrever o esquema de tabela de saudação de dados hello está sendo exportado/importado. Detalhes do arquivo de formato de saudação são descritos em [criar um arquivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Geração de arquivo de formato quando executar o BCP do hello máquina do SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Geração de arquivo de formato ao executar o BCP remotamente em um SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Use qualquer um dos métodos de saudação descritos na seção [movendo dados de origem de arquivo](#filesource_to_sqlonazurevm) toomove dados de saudação em arquivos simples tooa do SQL Server.

### <a name="sql-migration"></a>Assistente de Migração de Banco de Dados SQL
[Assistente de migração de banco de dados do SQL Server](http://sqlazuremw.codeplex.com/) fornece uma maneira fácil de usar toomove dados entre duas instâncias do SQL server. Ele permite que o esquema de dados de Olá Olá usuário toomap entre as origens e tabelas de destino, escolha tipos de coluna e várias outras funcionalidades. Ele usa a cópia em massa (BCP) sob as coberturas de saudação. Uma captura de tela de saudação bem-vindo à tela hello migração de banco de dados SQL assistente é mostrado abaixo.  

![Assistente de Migração do SQL Server][2]

### <a name="sql-backup"></a>Backup e restauração de banco de dados
O SQL Server dá suporte a:

1. [O banco de dados fazer backup e restaurar a funcionalidade](https://msdn.microsoft.com/library/ms187048.aspx) (ambos os tooa local bacpac ou arquivo de exportação tooblob) e [aplicativos da camada de dados](https://msdn.microsoft.com/library/ee210546.aspx) (usando bacpac).
2. Capacidade toodirectly criar VMs do SQL Server no Azure com um banco de dados copiado ou cópia tooan SQL Azure banco de dados existente. Para obter mais detalhes, consulte [Olá Use o Assistente para cópia de banco de dados](https://msdn.microsoft.com/library/ms188664.aspx).

Backup/restauração de uma captura de tela de volta do banco de dados de saudação opções do SQL Server Management Studio é mostrado abaixo.

![Ferramenta de Importação do SQL Server][1]

## <a name="resources"></a>Recursos
[Migrar um banco de dados tooSQL Server em uma VM do Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Visão geral do SQL Server em máquinas virtuais do Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
