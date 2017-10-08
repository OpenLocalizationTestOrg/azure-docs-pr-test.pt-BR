---
title: aaaRun um Hadoop de trabalho usando o banco de dados do Azure Cosmos e HDInsight | Microsoft Docs
description: Saiba como toorun um simple Hive, Pig e MapReduce trabalho com o banco de dados do Azure Cosmos e HDInsight do Azure.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Executar um trabalho do Apache Hive, Pig ou Hadoop usando o Azure Cosmos DB e o HDInsight
Este tutorial mostra como toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], e [Apache Hadoop] [ apache-hadoop] Trabalhos MapReduce no Azure HDInsight com o conector para Hadoop do Cosmos DB. Conector para Hadoop do cosmos do banco de dados permite tooact DB Cosmos como uma origem e um coletor para trabalhos Hive, Pig e MapReduce. Este tutorial usará DB Cosmos como fonte de dados de saudação e de destino para trabalhos de Hadoop.

Após concluir este tutorial, você será capaz de tooanswer Olá perguntas a seguir:

* Como fazer para carregar dados do Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?
* Como fazer para armazenar dados no Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?

É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde é executado por meio de um trabalho de Hive usando o banco de dados do Cosmos e HDInsight.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Em seguida, retorne toothis artigo, onde você receberá detalhes completos de saudação em como você pode executar trabalhos de análise em seus dados de banco de dados do Cosmos.

> [!TIP]
> Este tutorial presume que você tenha experiência anterior com o uso do Apache Hadoop, Hive e/ou Pig. Se você for novo tooApache Hadoop, Hive e Pig, recomendamos que você visite Olá [documentação do Apache Hadoop][apache-hadoop-doc]. Este tutorial também pressupõe que você tenha experiência anterior com o Cosmos DB e tenha uma conta do Cosmos DB. Se você estiver tooCosmos novo banco de dados ou você não tem uma conta de banco de dados do Cosmos, Confira nosso [Introdução] [ getting-started] página.
>
>

Você não tem tempo toocomplete Olá tutorial e deseja apenas scripts do PowerShell de exemplo completo tooget Olá para Hive, Pig e MapReduce? Sem problemas, elas estão [aqui][hdinsight-samples]. download de saudação também contém arquivos hql, pig e java Olá esses exemplos.

## <a name="NewestVersion"></a>Versão Mais Recente
<table border='1'>
    <tr><th>Versão do Conector para Hadoop</th>
        <td>1.2.0</td></tr>
    <tr><th>URI do script</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Data da Modificação</th>
        <td>26/04/2016</td></tr>
    <tr><th>Versões do HDInsight para as quais há suporte</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Log de alterações</th>
        <td>Cosmos atualizada do Azure DB Java SDK too1.6.0</br>
            Suporte adicionado para coleções particionadas como uma fonte e coletor</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Pré-requisitos
Antes de seguir as instruções de saudação neste tutorial, certifique-se de que você tenha a seguinte hello:

* Uma conta do Cosmos DB, um banco de dados e uma coleção com documentos. Para obter mais informações, consulte [Introdução ao Cosmos DB][getting-started]. Importar dados de exemplo para a conta de banco de dados do Cosmos com hello [ferramenta de importação de banco de dados do Cosmos][import-data].
* Produtividade. Leituras e gravações do HDInsight serão contabilizadas de acordo com suas unidades de solicitação alocadas para suas coleções.
* Capacidade para um procedimento armazenado adicional dentro de cada coleção de saída. procedimentos armazenado de Hello são usados para a transferência de documentos resultantes.
* Capacidade para documentos resultantes de saudação de trabalhos de Hive, Pig e MapReduce hello.
* [*Opcional*] Capacidade para uma coleção adicional.

> [!WARNING]
> Em ordem tooavoid Olá a criação de uma nova coleção durante qualquer um dos trabalhos hello, você pode imprimir Olá resultados toostdout, salvar o contêiner do hello saída tooyour WASB ou especifique uma coleção já existente. No caso de saudação da especificação de uma coleção existente, novos documentos serão criados dentro da coleção de saudação e documentos já existentes serão afetados apenas se houver um conflito na *ids*. **conector de saudação substituirá automaticamente os documentos existentes com conflitos de id**. Você pode desativar esse recurso definindo Olá upsert opção toofalse. Se upsert é falso e um conflito ocorre, o trabalho do Hadoop Olá falhará; relatar um erro de conflito de id.
>
>

## <a name="ProvisionHDInsight"></a>Etapa 1: criar um novo cluster HDInsight
Este tutorial usa o Script de ação de saudação do Portal Azure toocustomize seu cluster HDInsight. Neste tutorial, usaremos hello Azure Portal toocreate seu cluster HDInsight. Para obter instruções sobre como os cmdlets do PowerShell toouse ou hello HDInsight .NET SDK, check-out de [HDInsight personalizar clusters usando a ação de Script] [ hdinsight-custom-provision] artigo.

1. Entrar toohello [Portal do Azure][azure-portal].
2. Clique em **+ novo** na parte superior de saudação do hello barra de navegação esquerda, procure por **HDInsight** na barra de pesquisa de saudação na nova folha de saudação.
3. **HDInsight** publicado por **Microsoft** aparecerá na parte superior de saudação do hello resultados. Clique nele, em seguida, clique em **Criar**.
4. No novo HDInsight Cluster de saudação criar folha, insira seu **nome do Cluster** e selecione hello **assinatura** deseja tooprovision esse recurso em.

    <table border='1'>
        <tr><td>Nome do cluster</td><td>Cluster de saudação do nome.<br/>
O nome DNS deve começar e terminar com um número alfanumérico e pode conter traços.<br/>
campo de saudação deve ser uma cadeia de caracteres entre 3 e 63 caracteres.</td></tr>
        <tr><td>Nome da assinatura</td>
            <td>Se você tiver mais de uma assinatura do Azure, selecione a assinatura de saudação que irá hospedar o seu cluster HDInsight. </td></tr>
    </table>
5.Clique em **Selecionar tipo de Cluster** e valores especificados de saudação do conjunto de propriedades toohello a seguir.

    <table border='1'>
        <tr><td>Tipo de cluster</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Nível do cluster</td><td><strong>Standard</strong></td></tr>
        <tr><td>Sistema operacional</td><td><strong>Windows</strong></td></tr>
        <tr><td>Versão</td><td>última versão</td></tr>
    </table>

    Agora, clique em **SELECT**.

    ![Fornecer detalhes do cluster HDInsight inicial do Hadoop][image-customprovision-page1]
6. Clique em **credenciais** tooset seu logon e credenciais de acesso remoto. Escolha o **Nome de Usuário de Logon do Cluster** e a **Senha de Logon do Cluster**.

    Se você desejar tooremote em seu cluster, selecione *Sim* na parte inferior da saudação da folha de saudação e forneça um nome de usuário e senha.
7. Clique em **fonte de dados** tooset acessar o local para os dados. Escolha Olá **método de seleção** e especificar uma conta de armazenamento já existente ou crie um novo.
8. Olá folha mesmo em, especifique um **contêiner padrão** e um **local**. Clique em **SELECT**.

   > [!NOTE]
   > Selecione tooyour de fechar um local DB Cosmos região da conta para melhorar o desempenho
   >
   >
9. Clique em **preços** tooselect Olá número e tipo de nós. Você pode manter configuração padrão de saudação e Olá aumenta o número de nós de trabalho mais tarde.
10. Clique em **configuração opcional**, em seguida, **ações de Script** no hello folha de configuração opcional.

     Em ações de Script, digite Olá toocustomize informações a seguir seu cluster HDInsight.

     <table border='1'>
         <tr><th>Propriedade</th><th>Valor</th></tr>
         <tr><td>Nome</td>
             <td>Especifique um nome para a ação de script hello.</td></tr>
         <tr><td>URI do script</td>
             <td>Especifique Olá URI toohello script que é invocado toocustomize Olá cluster.</br></br>
Insira: </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Principal</td>
             <td>Clique em Olá toorun da caixa de seleção Olá script do PowerShell para o nó de cabeçalho hello.</br></br>
             <strong>Marque essa caixa de seleção</strong>.</td></tr>
         <tr><td>Trabalho</td>
             <td>Clique em Olá caixa de seleção toorun Olá PowerShell script no nó de trabalho hello.</br></br>
             <strong>Marque essa caixa de seleção</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Clique em script do PowerShell Olá caixa de seleção toorun Olá para Olá Zookeeper.</br></br>
             <strong>Não é necessário</strong>.
             </td></tr>
         <tr><td>parâmetros</td>
             <td>Especifica parâmetros de hello, se exigido pelo script hello.</br></br>
             <strong>Nenhum parâmetro necessário</strong>.</td></tr>
     </table>
11. Criar um novo **Grupo de Recursos** ou use um Grupo de Recursos existente em sua Assinatura do Azure.
12. Agora, verifique **Pin toodashboard** tootrack sua implantação e clique em **criar**!

## <a name="InstallCmdlets"></a>Etapa 2: instalar e configurar o Azure PowerShell
1. Instale o PowerShell do Azure. As instruções podem ser encontradas [aqui][powershell-install-configure].

   > [!NOTE]
   > Como alternativa, só para consultas Hive, você pode usar o Editor de Hive online do HDInsight. toodo assim, entrar toohello [Portal do Azure][azure-portal], clique em **HDInsight** tooview de painel esquerdo Olá em uma lista de seus clusters HDInsight. Clique em cluster Olá você deseja que as consultas de Hive toorun em e, em seguida, clique em **Console de consulta**.
   >
   >
2. Abra hello Azure PowerShell ambiente de script integrado:

   * Em um computador executando o Windows 8 ou o Windows Server 2012 ou posterior, você pode usar internas Olá pesquisa. Na tela de início do hello, digite **powershell ise** e clique em **Enter**.
   * Em um computador executando uma versão anterior ao Windows 8 ou Windows Server 2012, use o menu de início de saudação. Saudação do menu de início, digite **Prompt de comando** na caixa de pesquisa hello e, na lista de saudação de resultados, clique em **Prompt de comando**. No Prompt de comando do hello, digite **powershell_ise** e clique em **Enter**.
3. Adicione sua conta do Azure.

   1. Em Olá painel de Console, digite **Add-AzureAccount** e clique em **Enter**.
   2. Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.
   3. Digite a senha Olá para sua assinatura do Azure.
   4. Clique em **Entrar**.
4. Olá diagrama a seguir identifica as partes importantes de saudação do seu ambiente de script de PowerShell do Azure.

    ![Diagrama do PowerShell do Azure][azure-powershell-diagram]

## <a name="RunHive"></a>Etapa 3: Executar um trabalho do Hive usando o Cosmos DB e o HDInsight
> [!IMPORTANT]
> Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.
>
>

1. Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Vamos começar pela cadeia de caracteres de consulta. Vamos gravar uma consulta de Hive que leva os carimbos de hora gerada pelo sistema ( TS) e identificações exclusivas ( RID) de uma coleção de banco de dados do Azure Cosmos todos os documentos, também incluirá todos os documentos em um minuto hello e, em seguida, armazena os resultados de saudação volta para uma nova coleção de banco de dados do Azure Cosmos.</p>

    <p>Primeiro, vamos criar uma tabela Hive por meio da coleção do Azure Cosmos DB. Adicionar Olá toohello de trecho de código painel de Script do PowerShell a seguir <strong>depois</strong> trecho de código de saudação do #1. Certifique-se de que incluir Olá opcional DocumentDB.query parâmetro t trim nossos TS toojust de documentos e RID.</p>

   > [!NOTE]
   > **Ter nomeado o DocumentDB.inputCollections não foi um erro.** Sim, nós podemos adicionar várias coleções como entrada: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Em seguida, vamos criar uma tabela de Hive para a coleção de saída de hello. Propriedades de documento de saída Olá será mês hello, dia, hora, minuto e número total de saudação de ocorrências.

   > [!NOTE]
   > **Mais uma vez, ter nomeado o DocumentDB.outputCollections não foi um erro.** Sim, nós podemos adicionar várias coleções como saída: </br>
   > '*DocumentDB.outputCollections*' = '*\<Nome da Coleção de Saída do DocumentDB 1\>*,*\<Nome da Coleção de Saída do DocumentDB 2\>*' </br> nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula. </br></br>
   > Os documentos são distribuídos por round robin entre várias coleções. Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Por fim, vamos contagem Olá documentos por mês, dia, hora e minuto e inserir resultados Olá Olá no Hive tabela de saída.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Adicione Olá toocreate de trecho de código de script uma definição de trabalho de Hive a seguir da consulta anterior hello.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Você também pode usar hello - arquivo alternar toospecify um arquivo de script HiveQL no HDFS.
4. Adicione Olá após a hora de início do trecho toosave hello e enviar o trabalho de Hive hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Adicione Olá toowait para toocomplete de trabalho de Hive Olá a seguir.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Adicionar Olá após tooprint saudação padrão hello e saída de início e término.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Execute** seu novo script! **Clique em** verde Olá executar botão.
8. Verifique os resultados de saudação. O logon no hello [Portal do Azure][azure-portal].

   1. Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação. </br>
   2. Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação. </br>
   3. Localize e clique em <strong>Contas do Azure Cosmos DB</strong>. </br>
   4. Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em a consulta de Hive.</br>
   5. Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</br></p>

   Você verá os resultados de saudação de sua consulta de Hive.

   ![Resultados da consulta de Hive][image-hive-query-results]

## <a name="RunPig"></a>Etapa 4: Executar um trabalho do Pig usando o Cosmos DB e o HDInsight
> [!IMPORTANT]
> Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.
>
>

1. Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Vamos começar pela cadeia de caracteres de consulta. Vamos gravar uma consulta de Pig que usa todos os documentos gerada pelo sistema carimbos de hora ( TS) e identificações exclusivas ( RID) de uma coleção de banco de dados do Azure Cosmos, também incluirá todos os documentos em um minuto hello e, em seguida, armazena os resultados de saudação volta para uma nova coleção de banco de dados do Azure Cosmos.</p>
    <p>Primeiro, carregue documentos do Cosmos DB no HDInsight. Adicionar Olá toohello de trecho de código painel de Script do PowerShell a seguir <strong>depois</strong> trecho de código de saudação do #1. Certifique-se de tooadd um DocumentDB de consulta toohello tootrim de parâmetro de consulta opcional DocumentDB nossos TS toojust de documentos e RID.</p>

   > [!NOTE]
   > Sim, nós podemos adicionar várias coleções como entrada: </br>
   > '*\<Nome da Coleção de Entrada do DocumentDB 1\>*,*\<Nome da Coleção de Entrada do DocumentDB 2\>*'</br> nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula. </b>
   >
   >

    Os documentos são distribuídos por round robin entre várias coleções. Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Em seguida, vamos contar documentos Olá por mês hello, dia, hora, minuto e número total de saudação de ocorrências.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Por fim, vamos armazenar resultados Olá em nossa nova coleção de saída.

   > [!NOTE]
   > Sim, nós podemos adicionar várias coleções como saída: </br>
   > '\<Nome da Coleção de Saída do DocumentDB 1\>, \<Nome da Coleção de Saída do DocumentDB 2\>'</br> nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula.</br>
   > Documenta vai ser distribuído round robin em Olá várias coleções. Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Adicione Olá seguir toocreate de trecho de código de script uma definição de trabalho de Pig de consulta anterior hello.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Você também pode usar hello - arquivo alternar toospecify um arquivo de script Pig no HDFS.
6. Adicione Olá após a hora de início do trecho toosave hello e enviar o trabalho de Pig hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Adicione Olá toowait para toocomplete de trabalho de Pig Olá a seguir.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Adicionar Olá após tooprint saudação padrão hello e saída de início e término.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Execute** seu novo script! **Clique em** verde Olá executar botão.
10. Verifique os resultados de saudação. O logon no hello [Portal do Azure][azure-portal].

    1. Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação. </br>
    2. Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação. </br>
    3. Localize e clique em <strong>Contas do Azure Cosmos DB</strong>. </br>
    4. Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em a consulta de Pig.</br>
    5. Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</br></p>

    Você verá os resultados de saudação de sua consulta de Pig.

    ![Resultados da consulta de Pig][image-pig-query-results]

## <a name="RunMapReduce"></a>Etapa 5: executar um trabalho MapReduce usando o Azure Cosmos DB e o HDInsight
1. Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Executaremos um trabalho MapReduce que calcula o número de saudação de ocorrências para cada propriedade de documento da coleção de banco de dados do Azure Cosmos. Adicionar este trecho de código de script **depois** trecho de saudação acima.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar vem com instalação personalizada de saudação do hello Cosmos conector para Hadoop do banco de dados.
   >
   >
3. Adicione Olá trabalho MapReduce do comando toosubmit Olá a seguir.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Além disso toohello definição de trabalho MapReduce, você também fornecer nome do cluster HDInsight Olá onde você deseja o trabalho de MapReduce toorun hello e credenciais de saudação. Olá Start-AzureHDInsightJob é uma chamada assíncrona. conclusão de Olá toocheck de trabalho hello, use Olá *Wait-AzureHDInsightJob* cmdlet.
4. Adicione Olá toocheck de comando a seguir erros com a execução do trabalho MapReduce hello.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Execute** seu novo script! **Clique em** verde Olá executar botão.
6. Verifique os resultados de saudação. O logon no hello [Portal do Azure][azure-portal].

   1. Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação.
   2. Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação.
   3. Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.
   4. Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em o trabalho de MapReduce.
   5. Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.

      Você verá os resultados de saudação do seu trabalho de MapReduce.

      ![Resultados da consulta de MapReduce][image-mapreduce-query-results]

## <a name="NextSteps"></a>Próximas etapas
Parabéns! Você acaba de executar seus primeiros trabalhos do Hive, Pig e MapReduce usando o Azure Cosmos DB e o HDInsight.

Nós abrimos o código-fonte do nosso Conector do Hadoop. Se estiver interessado, você poderá contribuir com o [GitHub][github].

toolearn mais, consulte Olá artigos a seguir:

* [Desenvolver um aplicativo Java com o DocumentDB][documentdb-java-application]
* [Desenvolver programas Java MapReduce para Hadoop no HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Começar a usar Hadoop com Hive no uso de celular tooanalyze HDInsight][hdinsight-get-started]
* [Usar o MapReduce com o HDInsight][hdinsight-use-mapreduce]
* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Personalizar os clusters HDInsight usando a Ação de Script][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
