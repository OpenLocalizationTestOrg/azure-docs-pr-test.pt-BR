---
title: "Olá processo de ciência de dados de equipe em ação: usando o SQL Data Warehouse | Microsoft Docs"
description: "Processo e Tecnologia de Análise Avançada em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Olá processo de ciência de dados de equipe em ação: usando o SQL Data Warehouse
Neste tutorial, nós o conduziremos durante a criação e implantação de um modelo de aprendizado de máquina usando o SQL Data Warehouse (SQL DW) para um conjunto de dados disponível publicamente – hello [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados. modelo de classificação binária Olá construído prevê ou não uma dica é pago para uma viagem, e modelos de regressão e de classificação multiclasse também são discutidos que preveem distribuição Olá para valores de dica de saudação pagos.

procedimento de saudação segue Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) fluxo de trabalho. Vamos mostrar como toosetup um ambiente de ciência de dados, como tooload Olá dados no data Warehouse do SQL e como usar o data Warehouse do SQL ou uma saudação de tooexplore bloco de anotações do IPython em dados e engenharia a toomodel recursos. Em seguida, mostramos como toobuild e implantar um modelo de aprendizado de máquina do Azure.

## <a name="dataset"></a>Olá NYC táxi viagens dataset
Olá dados NYC táxi Trip consiste em cerca de 20GB de arquivos compactados de CSV (~ 48GB descompactado), registrar mais de milhões de 173 hello e viagens individuais é pago para cada viagem. Cada registro de viagem inclui locais de retirada e redistribuição hello e vezes, anônimas invadir o número de licença (do driver) e Olá número medallion (id exclusiva do táxi). dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:

1. Olá **trip_data.csv** arquivo contém os detalhes de viagem, como o número de passageiros, pontos de retirada e redução, duração da viagem e comprimento de viagem. Aqui estão alguns exemplos de registros:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Olá **trip_fare.csv** arquivo contém detalhes da tarifa Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga. Aqui estão alguns exemplos de registros:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Olá **chave exclusiva** usado viagem toojoin\_dados e viagem\_passagens é composta de saudação três campos a seguir:

* medallion,
* hack\_license e
* pickup\_datetime.

## <a name="mltasks"></a>Resolver três tipos de tarefas de previsão
Podemos formular três problemas de previsão com base em Olá *dica\_quantidade* tooillustrate três tipos de tarefas de modelagem:

1. **Classificação binária**: toopredict ou não uma dica foi pago para uma viagem, ou seja, um *dica\_quantidade* que é maior que $0 é um exemplo positivo, enquanto um *dica\_quantidade* $ 0 é um exemplo de negativo.
2. **Classificação multiclasse**: intervalo de saudação toopredict de dica de pago para viagem hello. Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.  

## <a name="setup"></a>Configurar o ambiente de ciência de dados do Azure Olá para análises avançadas
tooset seu ambiente de ciência de dados do Azure, siga estas etapas.

**Crie sua própria conta de armazenamento de blobs do Azure.**

* Quando você provisionar seu próprio armazenamento de BLOBs do Azure, escolha uma localização geográfica para o armazenamento de BLOBs do Azure em ou mais próximo possível muito**Centro Sul dos EUA**, que é onde Olá dados NYC táxi está armazenado. dados de saudação serão copiados usando AzCopy do contêiner de tooa de contêiner de armazenamento de blob público Olá em sua própria conta de armazenamento. Olá aproximando-se o armazenamento de BLOBs do Azure é tooSouth centro dos EUA, hello mais rápido essa tarefa (etapa 4) será concluída.
* toocreate conta seu próprio armazenamento do Azure, Olá siga as etapas descritas em [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md). Ser se notas toomake sobre valores hello seguintes credenciais de conta de armazenamento será necessário mais tarde neste passo a passo.
  
  * **Nome da Conta de Armazenamento**
  * **Chave da conta de armazenamento**
  * **Nome do contêiner** (que você deseja Olá toobe de dados armazenado em Olá armazenamento de BLOBs do Azure)

**Provisione sua instância do Azure SQL DW.**
Siga a documentação de saudação em [criar um SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision uma instância do SQL Data Warehouse. Certifique-se de que você faça notações em Olá credenciais SQL Data Warehouse que serão usadas nas próximas etapas a seguir.

* **Nome do Servidor**: <server Name>.database.windows.net
* **Nome do SQLDW (Banco de Dados)**
* **Nome de Usuário**
* **Senha**

**Instale o Visual Studio e o SQL Server Data Tools.** Para obter instruções, confira [Instalar o Visual Studio 2015 e/ou SSDT (SQL Server Data Tools) para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Conecte-se tooyour DW do SQL Azure com o Visual Studio.** Para obter instruções, consulte as etapas 1 e 2 na [conectar tooAzure SQL Data Warehouse com o Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Execução hello seguinte consulta SQL no banco de dados de saudação criado no Data Warehouse do SQL (conexão de tópico, em vez da saudação consulta fornecida na etapa 3 do hello) muito**criar uma chave mestra**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Crie um espaço de trabalho de Azure Machine Learning em sua assinatura do Azure.** Para obter instruções, confira [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md).

## <a name="getdata"></a>Saudação de carregar dados no SQL Data Warehouse
Abra um console de comando do Windows PowerShell. Execute seguinte Olá comandos do PowerShell toodownload Olá exemplo arquivos de script SQL que compartilha com você no GitHub tooa diretório local que você especificar com parâmetro hello *- dirdestino*. Você pode alterar o valor de saudação do parâmetro *- dirdestino* tooany diretório de local. Se *- dirdestino* não existir, ele será criado pelo script do PowerShell de saudação.

> [!NOTE]
> Talvez seja necessário muito**executar como administrador** ao executar Olá script do PowerShell a seguir se seu *dirdestino* directory precisa tooit de toocreate ou toowrite de privilégio de administrador.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Após a execução bem-sucedida, o diretório de trabalho atual muda muito*- dirdestino*. Você deve ser capaz de tela de toosee abaixo:

![][19]

No seu *- dirdestino*, execute Olá script do PowerShell no modo de administrador a seguir:

    ./SQLDW_Data_Import.ps1

Quando Olá script do PowerShell é executado para Olá primeira vez, você deverá tooinput informações de saudação do seu DW do SQL Azure e sua conta de armazenamento de BLOBs do Azure. Quando este script do PowerShell é concluído em execução para Olá primeira vez, as credenciais de saudação você entrada será foram gravada o arquivo de configuração de tooa SQLDW.conf no diretório de trabalho presente hello. Hello execução futuras desse arquivo de script do PowerShell tem Olá opção tooread necessárias de todos os parâmetros deste arquivo de configuração. Se você precisar toochange alguns parâmetros, você pode escolher tooinput parâmetros Olá na tela hello no prompt, exclua esse arquivo de configuração e inserindo valores de parâmetros de saudação conforme solicitado ou valores de parâmetro hello toochange editando o arquivo de SQLDW.conf Olá no seu *- dirdestino* directory.

> [!NOTE]
> Em ordem tooavoid esquema nome está em conflito com aqueles que já existem no seu Azure SQL DW ao ler parâmetros diretamente do arquivo de SQLDW.conf Olá, um número aleatório de 3 dígitos é adicionado toohello nome do esquema de arquivo de SQLDW.conf hello como nome do esquema padrão Olá para cada execução. saudação de script do PowerShell pode solicitar um nome de esquema: Olá nome pode ser especificado a critério do usuário.
> 
> 

Isso **script do PowerShell** arquivo conclui Olá tarefas a seguir:

* **Baixa e instala o AzCopy**, caso ele ainda não esteja instalado
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Copia a conta de armazenamento de blob particular dados tooyour** de blob público de saudação com AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Carrega dados usando o Polybase (executando LoadDataToSQLDW.sql) tooyour Azure SQL DW** de sua conta de armazenamento de blob particular com hello comandos a seguir.
  
  * Criar um esquema
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Criar uma credencial com escopo de banco de dados
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Criar uma fonte de dados externa para um blob de armazenamento do Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Criar um formato de arquivo externo para um arquivo csv. Dados não são compactados e os campos são separados com o caractere de pipe hello.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Criar tabelas externas de tarifas e corridas para o conjunto de dados Táxi de NYC na conta de Armazenamento de Blobs do Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Carregar dados de tabelas externas no tooSQL de armazenamento de BLOBs do Azure Data Warehouse

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Criar uma tabela de dados de exemplo (NYCTaxi_Sample) e inserir dados tooit de selecionar consultas SQL nas tabelas de viagem e passagens hello. (Algumas etapas deste passo a passo precisa toouse essa tabela de exemplo.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

localização geográfica de saudação de suas contas de armazenamento afeta os tempos de carregamento.

> [!NOTE]
> Dependendo da localização geográfica de saudação da sua conta de armazenamento de blob particular, Olá processo de copiar dados de uma conta de armazenamento particular de tooyour de blob público pode levar cerca de 15 minutos ou processar ainda mais e hello de carregamento de dados de sua conta de armazenamento tooyour Azure SQL DW pode levar 20 minutos ou mais.  
> 
> 

Você terá que toodecide o que fazer se você tiver arquivos de destino e origem duplicada.

> [!NOTE]
> Se toobe de arquivos. csv Olá copiado da conta de armazenamento de blob particular Olá blob público armazenamento tooyour já existe em sua conta de armazenamento de blob particular, AzCopy perguntará se você quer toooverwrite-los. Se você não quiser toooverwrite-los, entrada  **n**  quando solicitado. Se você quiser toooverwrite **todos os** , entrada **um** quando solicitado. Você também pode inserir **y** . toooverwrite CSV arquivos individualmente.
> 
> 

![Plotar nº 21][21]

Você pode usar seus próprios dados. Se os dados estiverem em sua máquina local em seu aplicativo da vida real, você ainda pode usar o armazenamento de BLOBs do Azure privada AzCopy tooupload local dados tooyour. Você só precisa Olá toochange **fonte** local, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, no hello comando AzCopy de saudação do PowerShell script arquivo toohello diretório local que contém os dados.

> [!TIP]
> Se os dados já estão em seu armazenamento de BLOBs do Azure privada em seu aplicativo da vida real, você poderá ignorar Olá AzCopy etapa Olá script do PowerShell e carregar diretamente Olá tooAzure de dados SQL DW. Isso exigirá adicionais edita de saudação script tootailor-toohello formato de seus dados.
> 
> 

Este script do Powershell também conecta-se em Olá informações do Azure SQL DW Olá dados exploração exemplo arquivos SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py para que esses três arquivos são toobe pronto testada instantaneamente Após a conclusão da saudação script do PowerShell.

Após a execução bem-sucedida, você verá uma tela parecida com a seguinte:

![][20]

## <a name="dbexplore"></a>Exploração de dados e engenharia de recursos no SQL Data Warehouse do Azure
Nesta seção, executamos a exploração de dados e a geração de recursos por meio da execução de consultas SQL no Azure SQL DW usando diretamente o **Visual Studio Data Tools**. Todas as consultas SQL usadas nesta seção podem ser encontradas no script de exemplo hello chamado *SQLDW_Explorations.sql*. Este arquivo já foi baixado tooyour o diretório local pelo script do PowerShell hello. Você também pode recuperá-lo no [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Mas o arquivo hello no GitHub não tem informações de DW do SQL Azure Olá conectadas.

Conecte-se tooyour DW do SQL Azure usando o Visual Studio com o nome de logon do SQL DW hello e a senha e abra a saudação **Pesquisador de objetos SQL** tabelas e o banco de dados do tooconfirm Olá foram importadas. Recuperar Olá *SQLDW_Explorations.sql* arquivo.

> [!NOTE]
> tooopen um editor de consultas do Parallel Data Warehouse (PDW), use Olá **nova consulta** comando enquanto o PDW estiver selecionado na Olá **Pesquisador de objetos SQL**. Não há suporte para o editor de consultas SQL padrão Olá no PDW.
> 
> 

Aqui estão tipo hello de dados executadas as tarefas de geração de exploração e recurso nesta seção:

* Explorar as distribuições de dados de alguns campos em períodos diferentes.
* Investigue a qualidade dos dados dos campos de longitude e latitude hello.
* Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.
* Gerar recursos e computar/comparar as distâncias de viagem.
* Unir Olá duas tabelas e extrair uma amostra aleatória que será usado toobuild modelos.

### <a name="data-import-verification"></a>Verificação de importação de dados
Essas consultas fornecem uma rápida verificação do número de saudação de linhas e colunas em Olá importar tabelas preenchidas anteriormente usando o bulk paralelo do Polybase,

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Saída:** o resultado deve ser 173.179.759 linhas e 14 colunas.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploração: distribuição de corridas por licença
Este exemplo de consulta identifica medallions hello (números de táxi) concluídas mais de 100 viagens dentro de um período de tempo especificado. consulta de saudação pode se beneficiar do acesso à tabela de saudação particionada porque ele está condicionado pelo esquema de partição de saudação do **retirada\_datetime**. Consultar o conjunto de dados completo Olá também fará com que o uso de tabela particionada hello e/ou verificação de índice.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Saída:** consulta Olá deve retornar uma tabela com linhas especificando medallions Olá 13,369 (táxis) e Olá número de viagem concluído por eles em 2013. Olá última coluna contém a contagem de saudação do número de saudação de viagens concluída.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploração: distribuição de corridas por medallion e hack_license
Este exemplo identifica medallions hello (táxi números) e hack_license números (drivers) concluídas mais de 100 viagens dentro de um período de tempo especificado.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Saída:** consulta Olá deve retornar uma tabela com 13,369 linhas especificando Olá 13,369 carro/driver IDs que foram concluídas mais que 100 viagens 2013. Olá última coluna contém a contagem de saudação do número de saudação de viagens concluída.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Avaliação de qualidade de dados: verificar registros com longitude e/ou latitude incorretos
Este exemplo examina se qualquer um dos campos de longitude e/ou latitude Olá conter um valor inválido (graus de radianos devem estar entre -90 e 90), ou ter (0, 0) coordenadas.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Saída:** consulta Olá retorna 837,467 viagens que têm campos inválidos de longitude e/ou latitude.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploração: distribuição de corridas com gorjeta versus sem gorjeta
Este exemplo localiza o número de saudação de viagens foram Oblíquo versus o número de saudação não foram Oblíquo em um período de tempo especificado (ou Olá conjunto de dados completo se abrangendo ano hello como ela é configurada aqui). Essa distribuição reflete Olá rótulo binário distribuição toobe usado posteriormente para modelagem de classificação binária.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Saída:** Olá consulta deve seguir Olá retorno dica frequências para ano Olá Oblíquo 2013: 90,447,622 e 82,264,709-Oblíquo não.

### <a name="exploration-tip-classrange-distribution"></a>Exploração: distribuição de classe/intervalo de gorjetas
Esse exemplo calcula distribuição Olá de intervalos de dica em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá). Isso é a distribuição de saudação de classes de rótulo de saudação que serão usados posteriormente para modelagem de classificação multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Saída:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Exploração: calcular e comparar a distância da corrida
Este exemplo converte a longitude de retirada e redistribuição hello e Geografia do latitude tooSQL pontos, calcula a distância de viagem hello usando o SQL geography pontos diferença e retorna uma amostra aleatória de resultados Olá para comparação. exemplo Hello limita os resultados de saudação toovalid coordena usando apenas a consulta de avaliação de qualidade dados Olá coberta anteriormente.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Engenharia de recursos usando funções SQL
Às vezes, as funções SQL podem ser uma opção eficiente para a engenharia de recursos. Neste passo a passo, definimos uma SQL função toocalculate Olá direta distância entre os locais de retirada e redução de saudação. Você pode executar Olá scripts SQL a seguir **ferramentas de dados do Visual Studio**.

Aqui está o script SQL Olá que define a função de distância hello.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Aqui está um exemplo toocall recursos de toogenerate essa função na consulta SQL:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Saída:** essa consulta gera uma tabela (com 2,803,538 linhas) com retirada e redução latitudes e longitudes e Olá correspondente direto distâncias em milhas. Estes são os resultados de saudação para primeiro 3 linhas:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>Preparar dados para criação de modelo
saudação de junções de consulta a seguir Olá **nyctaxi\_viagem** e **nyctaxi\_passagens** tabelas, gera um rótulo de classificação binária **Oblíquo**, um rótulo de classificação multiclasse **dica\_classe**e extrai um exemplo de hello ingressado no conjunto de dados completo. amostragem de saudação é feita por recuperar um subconjunto de viagens de saudação com base na hora de retirada.  Essa consulta pode ser copiada e colada diretamente no hello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta da instância de banco de dados do SQL Olá no Azure. consulta de saudação exclui registros com incorreto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Quando você estiver pronto tooproceed tooAzure aprendizado de máquina, você pode:  

1. Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, ou
2. Persistir Olá amostrada e dados de engenharia planejar toouse para modelo de criação de um novo SQL DW tabela e usam a nova tabela de saudação em Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure. Olá script do PowerShell na etapa anterior tenha feito isso para você. Você pode ler diretamente a partir dessa tabela no módulo de importação de dados de saudação.

## <a name="ipnb"></a>Exploração de dados e engenharia de recursos no IPython Notebook
Nesta seção, vamos realizar exploração de dados e geração de recurso usando ambos os Python e consultas SQL em relação a saudação SQL DW criado anteriormente. Um bloco de anotações de IPython de exemplo chamado **SQLDW_Explorations.ipynb** e um arquivo de script de Python **SQLDW_Explorations_Scripts.py** ter sido baixado tooyour diretório de local. Eles também estão disponíveis no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Esses dois arquivos são idênticos em scripts Python. arquivo de script de Python Olá é fornecido tooyou caso você não tiver um servidor de bloco de anotações do IPython. Esses dois de exemplo de arquivo Python são criados no **Python 2.7**.

Olá informações necessárias do Azure SQL DW no exemplo hello bloco de anotações do IPython e Olá Python máquina local do script arquivo baixado tooyour foi conectada pelo script do PowerShell Olá anteriormente. Eles são executáveis sem qualquer modificação.

Se você já tiver configurado um espaço de trabalho do AzureML, você pode carregar exemplo hello serviço do bloco de anotações do IPython toohello AzureML IPython Notebook diretamente e iniciar a execução. Aqui estão Olá etapas tooupload tooAzureML serviço do bloco de anotações do IPython:

1. Faça logon no espaço de trabalho de AzureML tooyour, clique "Studio" na parte superior do hello e clique em "NOTEBOOKS" no lado esquerdo de saudação da página da web de saudação.
   
    ![Plotar nº 22][22]
2. Clique em "Novo" no canto inferior esquerdo Olá Olá web página e selecione "Python 2". Em seguida, fornecer um bloco de anotações de toohello de nome e clique em Olá marca de seleção toocreate Olá nova em branco bloco de anotações do IPython.
   
    ![Plotar nº 23][23]
3. Clique Olá símbolo de "Jupyter" no canto superior esquerdo de saudação do hello novo bloco de anotações do IPython.
   
    ![Plotar nº 24][24]
4. Arrastar e soltar Olá exemplo bloco de anotações do IPython toohello **árvore** página do seu serviço de bloco de anotações do AzureML IPython e clique em **carregar**. Em seguida, o exemplo hello bloco de anotações do IPython será carregado toohello serviço AzureML IPython Notebook.
   
    ![Plotar nº 25][25]

Na saudação de toorun de ordem de exemplo do bloco de anotações do IPython ou Olá o arquivo de script de Python, hello pacotes Python a seguir são necessários. Se você estiver usando o serviço de bloco de anotações do AzureML IPython hello, esses pacotes foram previamente instalados.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Olá recomendado sequência ao compilar soluções analíticas avançadas em AzureML com dados grandes é seguir hello:

* Ler em uma pequena amostra dos dados de saudação em um quadro de dados na memória.
* Execute algumas visualizações e explorações usando Olá dados amostrados.
* Testar usando dados de amostra de saudação de engenharia de recurso.
* Para exploração de dados maior, manipulação de dados e de engenharia de recurso, use consultas de SQL do Python tooissue diretamente contra Olá SQL DW.
* Decida toobe de tamanho de exemplo de hello adequado para a criação do modelo de aprendizado de máquina do Azure.

Estes de saudação são alguns exploração, visualização de dados e exemplos de engenharia de recurso. Mais explorações de dados podem ser encontradas no exemplo hello bloco de anotações do IPython e o arquivo de script de Python de exemplo hello.

### <a name="initialize-database-credentials"></a>Inicializar as credenciais de banco de dados
Inicialize as configurações de conexão de banco de dados em Olá variáveis a seguir:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Criar conexão de banco de dados
Aqui está a cadeia de caracteres de conexão de saudação que cria Olá conexão toohello banco de dados.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Relatar o número de linhas e colunas na tabela <nyctaxi_trip>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Relatar o número de linhas e colunas na tabela <nyctaxi_fare>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Leitura-em uma amostra de dados pequenos de saudação banco de dados do SQL Data Warehouse
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabela de exemplo do tempo tooread Olá é 14.096495 segundos.  
Número de linhas e colunas recuperadas = (1000, 21).

### <a name="descriptive-statistics"></a>Estatísticas descritivas
Agora você está pronto tooexplore dados de saudação de amostra. Vamos começar com olhando algumas estatísticas descritivas para Olá **viagem\_distância** (ou todos os outros campos que você escolher toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualização: exemplo de plotagem da caixa
Em seguida, vamos examinar diagrama em caixa Olá para Olá trip distância toovisualize Olá quantis.

    df1.boxplot(column='trip_distance',return_type='dict')

![Plotar nº 1][1]

### <a name="visualization-distribution-plot-example"></a>Visualização: exemplo de plotagem de distribuição
Gráficos que visualizam distribuição hello e um histograma para Olá amostragem distâncias de viagem.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plotar nº 2][2]

### <a name="visualization-bar-and-line-plots"></a>Visualização: plotagens de barra e linha
Neste exemplo, podemos guardar a distância de viagem de saudação em cinco compartimentos e visualizar Olá compartimentação de resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Podemos plotar Olá acima distribuição bin em uma barra ou linha plotagem com:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plotar nº 3][3]

e

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plotar nº 4][4]

### <a name="visualization-scatterplot-examples"></a>Visualização: exemplo de plotagem de dispersão
Vamos mostrar gráfico de dispersão entre **viagem\_tempo\_na\_s** e **viagem\_distância** toosee se há qualquer correlação

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plotar nº 6][6]

Da mesma forma, é possível verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plotar nº 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Exploração de dados em exemplos de dados usando consultas SQL no notebook IPython
Nesta seção, exploraremos distribuições de dados usando dados de amostra de saudação que são persistidos em nova tabela de saudação criado anteriormente. Observe que explorações semelhantes podem ser realizadas usando tabelas originais hello.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Exploração: Número de linhas e colunas de saudação do relatório tabela de amostra
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Exploração: distribuição de corridas com gorjeta e sem gorjeta
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Exploração: distribuição de classe de gorjetas
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Exploração: Plotar a distribuição de dica Olá pela classe
    tip_class_dist['tip_freq'].plot(kind='bar')

![Plotar nº 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Exploração: distribuição diária de corridas
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploração: distribuição de corridas por licença
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Exploração: distribuição de corridas por medalhão e carteira de habilitação
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Exploração: distribuição de horário das corridas
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Exploração: distribuição da distância das corridas
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Exploração: distribuição do tipo de pagamento
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verifique se a forma final de saudação da tabela de featurized Olá
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## 
            <a name="mlmodel">
            </a>Compilar modelos no Azure Machine Learning
Agora, estamos prontos tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net). saudação de dados é pronto toobe usada em qualquer um dos problemas de previsão Olá identificados anteriormente, ou seja:

1. **Classificação binária**: toopredict ou não uma dica foi pago uma viagem.
2. **Classificação multiclasse**: intervalo de saudação toopredict de dica pago, de acordo com toohello classes definidas anteriormente.
3. **Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.  

toobegin Olá exercício de modelagem, faça logon no tooyour **aprendizado de máquina do Azure** espaço de trabalho. Se você ainda não tiver criado uma espaço de trabalho de aprendizado de máquina, consulte [Criar um espaço de trabalho de AM do Azure](machine-learning-create-workspace.md).

1. tooget iniciado com o aprendizado de máquina do Azure, consulte [o que é o estúdio de aprendizado de máquina do Azure?](machine-learning-what-is-ml-studio.md)
2. Faça logon no muito[estúdio de aprendizado de máquina do Azure](https://studio.azureml.net).
3. Olá Studio Home page do fornece uma grande quantidade de informações, vídeos, tutoriais, links toohello Referência de módulos e outros recursos. Para obter mais informações sobre o aprendizado de máquina do Azure, consulte Olá [Centro de documentação do aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Uma experiência de treinamento típico consiste Olá etapas a seguir:

1. Criar uma experiência **+NEW** .
2. Obter dados de saudação no Azure ML.
3. Pré-processar, transformar e manipular dados saudação conforme necessário.
4. Gerar recursos conforme necessário.
5. Dividir dados saudação em conjuntos de dados de treinamento / / teste de validação (ou têm conjuntos de dados separados para cada).
6. Selecione um ou mais algoritmos dependendo Olá toosolve problema de aprendizado de aprendizado de máquina. Por exemplo, classificação binária, classificação multiclasse ou regressão.
7. Treine um ou mais modelos usando o conjunto de dados de treinamento hello.
8. Classificar o conjunto de dados de validação de saudação usando modelos treinados hello.
9. Avalie Olá modelos toocompute Olá relevante de métricas para Olá problema de aprendizado.
10. Ajuste Olá modelo (s) e selecione Olá melhor modelo toodeploy.

Neste exercício, podemos ter já explorados engenharia dados Olá no SQL Data Warehouse e decidido Olá tooingest de tamanho de exemplo no Azure ML. Aqui está o hello procedimento toobuild um ou mais dos modelos de previsão hello:

1. Obter dados de saudação no Azure ML usando Olá [importar dados] [ import-data] módulo, disponível no hello **dados de entrada e saída** seção. Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência de módulo.
   
    ![Dados de Importação de AM do Azure][17]
2. Selecione **banco de dados do SQL Azure** como Olá **fonte de dados** em Olá **propriedades** painel.
3. Digite o nome DNS de banco de dados de saudação em Olá **nome do servidor de banco de dados** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Digite hello **nome do banco de dados** no campo correspondente do hello.
5. Digite hello *nome de usuário do SQL* em Olá **nome de conta de usuário do servidor**e hello *senha* em Olá **senha de conta de usuário do servidor**.
6. Verificar Olá **aceitar qualquer certificado de servidor** opção.
7. Em Olá **consulta de banco de dados** editar a área de texto, cole a consulta Olá extrai Olá necessário campos (incluindo quaisquer campos calculados como rótulos de saudação) de banco de dados e para baixo amostras de tamanho de exemplo hello dados toohello desejado.

É um exemplo de um experimento de classificação binária ler dados diretamente do banco de dados do SQL Data Warehouse Olá figura de saudação abaixo (Lembre-se de tooreplace Olá nomes de tabelas nyctaxi_trip e nyctaxi_fare pelo esquema Olá nome e hello nomes de tabela usado no seu instruções passo a passo). Experimentos semelhantes podem ser construídos por meio de classificação multiclasse e problemas de regressão.

![Treino do AM do Azure][10]

> [!IMPORTANT]
> Em Olá modelagem de extração de dados e exemplos de consulta fornecidos nas seções anteriores, de amostragem **todos os rótulos para os exercícios de modelagem Olá três são incluídos na consulta Olá**. Uma etapa importante (obrigatório) em cada Olá exercícios de modelagem é muito**excluir** Olá rótulos desnecessários para Olá outros dois problemas e qualquer outro **vazamentos de destino**. Por exemplo, ao usar classificação binária, use o rótulo de saudação **Oblíquo** e excluir campos Olá **dica\_classe**, **dica\_quantidade**, e **total\_quantidade**. Olá último vazamentos de destino já que eles implicam dica Olá pagas.
> 
> tooexclude quaisquer colunas desnecessárias ou vazamentos de destino, você pode usar o hello [selecionar colunas no conjunto de dados] [ select-columns] módulo ou hello [editar metadados] [ edit-metadata]. Para saber mais, veja as páginas de referência [Selecionar Colunas no Conjunto de Dados][select-columns] e [Editar Metadados][edit-metadata].
> 
> 

## 
            <a name="mldeploy">
            </a>Implantar modelos no Azure Machine Learning
Quando o modelo estiver pronto, pode facilmente implantá-lo como um serviço web diretamente do experimento hello. Para obter mais informações sobre como implantar os serviços Web do AM do Azure, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy um novo serviço da web, você precisa:

1. Criar um experimento de pontuação.
2. Implante o serviço web de saudação.

toocreate experiência de uma pontuação de um **concluído** experiência de treinamento, clique em **criar experiência de PONTUAÇÃO** na barra de ação inferior hello.

![Pontuação do Azure][18]

O aprendizado de máquina do Azure tentará toocreate uma experiência de pontuação com base nos componentes de saudação da experiência de treinamento hello. Em especial, ele vai:

1. Salvar modelo treinado hello e remover os módulos de treinamento de modelo de saudação.
2. Identificar uma lógica **porta de entrada** toorepresent Olá esperado o esquema de dados de entrada.
3. Identificar uma lógica **porta de saída** o esquema de saída de serviço do toorepresent Olá web esperado.

Quando Olá experimento de pontuação é criado, examiná-la e fazer ajuste conforme necessário. Um ajuste típico é tooreplace Olá dataset de entrada e/ou consulta com uma que exclui os campos de rótulo, como eles não estarão disponíveis quando Olá serviço é chamado. Também é que um tamanho de saudação tooreduce uma boa prática de saudação tooa de consulta e/ou conjunto de dados de entrada suficientes esquema de entrada hello tooindicate de alguns registros. Para a porta de saída de hello, é tooexclude comuns entrados todos os campos e incluir apenas Olá **rótulos de pontuação** e **probabilidades pontuadas** em Olá saída usando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.

Um exemplo de experiência de pontuação é fornecido na Figura Olá a seguir. Quando estiver pronto toodeploy, clique em Olá **publicar WEB SERVICE** botão na barra de ação inferior hello.

![Publicação do AM do Azure][11]

## <a name="summary"></a>Resumo
toorecap que fizemos neste tutorial passo a passo, você criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados grande público, colocá-lo por meio de saudação processo de ciência de dados de equipe, todo caminho de saudação do treinamento de toomodel de aquisição de dados e, em seguida, implantação de toohello de um serviço web de aprendizado de máquina do Azure.

### <a name="license-information"></a>Informações de licença
Este exemplo passo a passo e seu que acompanha scripts e IPython notebook(s) são compartilhados pela Microsoft sob a licença do MIT hello. Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.

## <a name="references"></a>Referências
•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
