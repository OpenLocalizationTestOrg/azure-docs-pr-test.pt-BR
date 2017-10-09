---
title: "aaaBuild e implantar um modelo de aprendizado de máquina usando o SQL Server em uma VM do Azure | Microsoft Docs"
description: "Processo e Tecnologia de Análise Avançada em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Olá processo de ciência de dados de equipe em ação: usando o SQL Server
Neste tutorial, você pode percorrer Olá processo de criação e implantação de um modelo de aprendizado de máquina usando o SQL Server e um conjunto de dados disponível publicamente – hello [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados. procedimento de saudação segue um fluxo de trabalho de ciência de dados padrão: ingestão e explorar dados Olá, engenheiro de aprendizado de toofacilitate de recursos, em seguida, compilar e implantar um modelo.

## <a name="dataset"></a>Descrição do conjunto de dados Corridas de Táxi em NYC
Olá dados NYC táxi viagem é cerca de 20GB de arquivos compactados de CSV (~ 48GB descompactado), que inclui mais de milhões de 173 hello e viagens individuais é pago para cada viagem. Cada registro de viagem inclui Olá retirada e entrega local e a hora, hack anônimos (driver) o número de licença e número medallion (id exclusiva do táxi). dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:

1. Olá 'trip_data' CSV contém detalhes da visita, como o número de passageiros, coleta e pontos de redução, duração da viagem e comprimento de viagem. Aqui estão alguns exemplos de registros:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Olá 'trip_fare' CSV contém detalhes de passagens Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga. Aqui estão alguns exemplos de registros:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de campos de saudação: medallion, ataques\_licença e retirada\_datetime.

## <a name="mltasks"></a>Exemplos de tarefas de previsão
Podemos será formular três problemas de previsão com base em Olá *dica\_quantidade*, ou seja:

1. Classificação binária: prever ou não se uma gorjeta foi paga por uma corrida, ou seja, um *tip\_amount* maior que US$ 0 é um exemplo positivo, enquanto um *tip\_amount* de US$ 0 é um exemplo negativo.
2. Classificação multiclasse: intervalo de saudação toopredict de dica de pago para viagem hello. Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Tarefa de regressão: o valor de saudação toopredict de dica pago para uma viagem.  

## <a name="setup"></a>Configurando ambiente de ciência de saudação dados do Azure para análise avançada
Como você pode ver da saudação [planejar seu ambiente](machine-learning-data-science-plan-your-environment.md) guia, há vários toowork opções com hello NYC táxi viagens conjunto de dados no Azure:

* Trabalhar com dados de saudação em blobs do Azure e o modelo no aprendizado de máquina do Azure
* Saudação de carregar dados em um banco de dados do SQL Server e o modelo no aprendizado de máquina do Azure

Neste tutorial, tentaremos demonstrar a importação em massa paralela de saudação tooa de dados do SQL Server, exploração de dados, o recurso de engenharia e para baixo de amostragem usando o SQL Server Management Studio, bem como usar o bloco de anotações do IPython. [Scripts de exemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e [notebooks IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) são compartilhados no GitHub. Um toowork de bloco de anotações do IPython exemplo com dados de saudação em blobs do Azure também está disponível no hello mesmo local.

tooset seu ambiente de ciência de dados do Azure:

1. [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md)
2. 
            [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md)
3. [Provisione uma Máquina Virtual de Ciência de Dados](machine-learning-data-science-setup-sql-server-virtual-machine.md), que fornece um SQL Server e um servidor do IPython Notebook.
   
   > [!NOTE]
   > scripts de exemplo Hello e anotações do IPython será baixado tooyour máquina de virtual de ciência de dados durante o processo de instalação hello. Quando for concluído Olá script de pós-instalação de VM, exemplos de saudação será na biblioteca de documentos da VM:  
   > 
   > * Scripts de exemplo: `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Exemplo de IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` é o nome de logon do Windows da VM. Chamaremos toohello pastas de exemplo como **Scripts de exemplo** e **exemplo de anotações do IPython**.
   > 
   > 

Com base no tamanho do conjunto de dados Olá, local de fonte de dados e ambiente de destino do Azure selecionada Olá, este cenário é semelhante muito[cenário \#5: SQL Server em VM do Azure de destino do conjunto de dados grande em arquivos de locais,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Obter Olá dados de origem pública
Olá tooget [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados de seu local público, você pode usar qualquer um dos métodos de saudação descritos em [tooand de mover dados do armazenamento de BLOBs do Azure](machine-learning-data-science-move-azure-blob.md) toocopy Olá dados tooyour nova máquina virtual.

dados de saudação toocopy usando AzCopy:

1. Faça logon na máquina virtual de tooyour (VM)
2. Criar um novo diretório em disco de dados da VM hello (Observação: não use Olá disco temporário que vem com hello VM como um disco de dados).
3. Em uma janela de Prompt de comando, execute Olá Azcopy linha de comando a seguir, substituindo < path_to_data_folder > com a pasta de dados criada na (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Quando Olá AzCopy é concluída, um total de 24 compactado arquivos CSV (12 para viagem\_dados e 12 para viagem\_passagens) devem estar na pasta de dados de saudação.
4. Descompacte arquivos de saudação baixado. Anote a pasta de saudação onde residem os arquivos de saudação descompactado. Esta pasta será chamado tooas hello < caminho\_para\_dados\_arquivos\>.

## <a name="dbload"></a>Importação de dados em massa para o Banco de Dados do SQL Server
saudação de carregamento/transferir grandes quantidades de banco de dados do SQL data tooan e as consultas subsequentes possível melhorar o desempenho usando *tabelas particionadas e exibições*. Nesta seção, vamos seguir as instruções de saudação descritas em [paralelo em massa dados de importação usando partição tabelas SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate um novo banco de dados e carregar Olá dados em tabelas particionadas em paralelo.

1. Enquanto estiver conectado tooyour VM, iniciar **SQL Server Management Studio**.
2. Conecte-se usando a Autenticação do Windows.
   
    ![Conexão SSMS][12]
3. Se você ainda não tiver alterado o modo de autenticação do SQL Server hello e criado um novo usuário de logon do SQL, abra o arquivo de script de Olá chamado **alterar\_auth.sql** em Olá **Scripts de exemplo** pasta. Alterar nome de usuário saudação padrão e a senha. Clique em **! Execute** no script de Olá Olá barra de ferramentas toorun.
   
    ![Executar Script][13]
4. Verificar e/ou alterar o saudação padrão banco de dados e log pastas tooensure que bancos de dados recém-criados será armazenado em um disco de dados do SQL Server. imagem de VM do SQL Server de saudação que é otimizada para cargas de datawarehousing é pré-configurado com discos de dados e de log. Se sua VM não incluiu um disco de dados e você adicionou novos discos rígidos virtuais durante a saudação processo de configuração VM, altere pastas padrão de saudação da seguinte maneira:
   
   * Nome de SQL Server Olá com o botão direito no hello esquerda do painel e clique em **propriedades**.
     
       ![Propriedades do SQL Server][14]
   * Selecione **configurações de banco de dados** de saudação **selecionar uma página** lista toohello esquerda.
   * Verificar e/ou alterar Olá **locais padrão do banco de dados** toohello **disco de dados** locais de sua escolha. É onde os novos bancos de dados residem se criado com as configurações de local de padrão de saudação.
     
       ![Padrões de banco de dados SQL][15]  
5. toocreate um novo banco de dados e um conjunto de grupos de arquivos toohold Olá tabelas particionadas, abra o script de exemplo hello **criar\_db\_default.sql**. script Hello criará um novo banco de dados denominado **TaxiNYC** e 12 grupos de arquivos no local de dados padrão de saudação. Cada grupo de arquivos conterá um mês de dados trip\_data e trip\_fare. Modificar o nome do banco de dados de hello, se desejado. Clique em **! Executar** toorun script de saudação.
6. Em seguida, crie duas tabelas de partição, uma para viagem Olá\_dados e outro para viagem Olá\_passagens. Abra o script de exemplo hello **criar\_particionada\_table.sql**, que será:
   
   * Crie uma partição de saudação de toosplit de função de dados por mês.
   * Crie um toomap de esquema de partição de dados tooa grupo de arquivos diferente cada mês.
   * Criar esquema de partição do duas tabelas particionadas toohello mapeado: **nyctaxi\_viagem** armazenará trip Olá\_dados e **nyctaxi\_passagens** armazenará trip Olá \_passagens de dados.
     
     Clique em **! Executar** toorun Olá script e criar tabelas particionada de saudação.
7. Em Olá **Scripts de exemplo** pasta, há dois scripts de PowerShell de exemplo fornecidos toodemonstrate importações em massa paralela tooSQL servidor de tabelas de dados.
   
   * **BCP\_paralela\_generic.ps1** é um script genérico tooparallel importar em massa dados em uma tabela. Modifique este variáveis de entrada e de destino de saudação do tooset script conforme indicado nas linhas de comentário hello no script hello.
   * **BCP\_paralela\_nyctaxi.ps1** é uma versão previamente configurada do script genérico hello e pode ser usado tootooload ambas as tabelas para dados de NYC táxi viagens hello.  
8. Saudação de atalho **bcp\_paralela\_nyctaxi.ps1** nome do script e clique em **editar** tooopen no PowerShell. Saudação de revisão predefinição variáveis e modificar o nome de banco de dados selecionado do acordo tooyour, pasta de dados de entrada, pasta de log de destino e arquivos de formato de exemplo caminhos toohello **nyctaxi_trip.xml** e **nyctaxi\_ fare.XML** (fornecido no hello **Scripts de exemplo** pasta).
   
    ![Importação em massa de dados][16]
   
    Você também pode selecionar o modo de autenticação hello, o padrão é a autenticação do Windows. Clique a seta verde de saudação Olá toorun de barra de ferramentas. script Hello iniciará 24 operações de importação em massa em paralelo, 12 para cada tabela particionada. É possível monitorar o progresso de importação de dados Olá abrindo a pasta de dados de padrão saudação do SQL Server conforme definido acima.
9. relatórios de script do PowerShell Olá Olá horas inicial e final. Quando todos em massa importações completa, Olá hora de término é relatado. Verifique o hello destino log pasta tooverify que importações em massa de saudação foram bem-sucedidas, ou seja, nenhum erro relatado na pasta de log de destino hello.
10. O banco de dados agora está pronto para exploração, engenharia de recursos e outras operações conforme desejado. Como tabelas de saudação são particionadas de acordo com o toohello **retirada\_datetime** campo, consultas que incluem **retirada\_datetime** condições em Olá  **ONDE** cláusula se beneficiarão do esquema de partição hello.
11. Em **SQL Server Management Studio**, explore o script de exemplo hello fornecido **exemplo\_queries.sql**. toorun qualquer uma das consultas de exemplo hello, realce Olá linhas de consulta e clique em **! Executar** na barra de ferramentas de saudação.
12. Olá dados NYC táxi viagens é carregado em duas tabelas separadas. operações de junção tooimprove, é altamente recomendável tooindex tabelas de saudação. Olá script de exemplo **criar\_particionada\_index.sql** cria índices particionados na chave de junção composto Olá **medallion, ataques\_licença e retirada\_datetime**.

## <a name="dbexplore"></a>Exploração de dados e engenharia de recursos no SQL Server
Nesta seção, vamos realizar exploração e recurso de geração de dados, executando consultas SQL diretamente em Olá **SQL Server Management Studio** usar o banco de dados do SQL Server Olá criado anteriormente. Um script de exemplo chamado **exemplo\_queries.sql** é fornecido no hello **Scripts de exemplo** pasta. Modificar o nome de banco de dados do Olá Olá script toochange, se ele for diferente do padrão de saudação: **TaxiNYC**.

Neste exercício, você vai:

* Conecte-se muito**SQL Server Management Studio** usando a autenticação do Windows ou autenticação do SQL e hello nome de logon do SQL e a senha.
* Explorar as distribuições de dados de alguns campos em períodos diferentes.
* Investigue a qualidade dos dados dos campos de longitude e latitude hello.
* Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.
* Gerar recursos e computar/comparar as distâncias de viagem.
* Unir Olá duas tabelas e extrair uma amostra aleatória que será usado toobuild modelos.

Quando você estiver pronto tooproceed tooAzure aprendizado de máquina, você pode:  

1. Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, ou
2. Persistir Olá amostrada e planejar toouse para criar um novo banco de dados de modelo de dados de engenharia de tabela e usam a nova tabela de saudação em Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.

Esta seção é salvará Olá consulta final tooextract e Olá dados de exemplo. método segundo Hello é demonstrado no hello [exploração de dados e de engenharia de recurso no bloco de anotações do IPython](#ipnb) seção.

Para uma verificação rápida do número de saudação de linhas e colunas de saudação tabelas populadas anteriormente usando a importação em massa em paralelo,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Exploração: distribuição de corridas por licença
Este exemplo identifica medallion hello (números de táxi) com mais de 100 viagens dentro de um determinado período de tempo. consulta de saudação pode se beneficiar do acesso à tabela de saudação particionada porque ele está condicionado pelo esquema de partição de saudação do **retirada\_datetime**. Consultar o conjunto de dados completo Olá também fará com que o uso de tabela particionada hello e/ou verificação de índice.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploração: distribuição de corridas por medallion e hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Avaliação de qualidade de dados: verificar registros com longitude e/ou latitude incorretos
Este exemplo examina se qualquer um dos campos de longitude e/ou latitude Olá conter um valor inválido (graus de radianos devem estar entre -90 e 90), ou ter (0, 0) coordenadas.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploração: distribuição de corridas com gorjeta versus sem gorjeta
Este exemplo localiza o número de saudação de viagens foram Oblíquo versus não-Oblíquo em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá). Essa distribuição reflete Olá rótulo binário distribuição toobe usado posteriormente para modelagem de classificação binária.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Exploração: distribuição de classe/intervalo de gorjetas
Esse exemplo calcula distribuição Olá de intervalos de dica em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá). Isso é a distribuição de saudação de classes de rótulo de saudação que serão usados posteriormente para modelagem de classificação multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Exploração: calcular e comparar distância de viagem
Este exemplo converte a longitude de retirada e redistribuição hello e Geografia do latitude tooSQL pontos, calcula a distância de viagem hello usando o SQL geography pontos diferença e retorna uma amostra aleatória de resultados Olá para comparação. exemplo Hello limita os resultados de saudação toovalid coordena usando apenas a consulta de avaliação de qualidade dados Olá coberta anteriormente.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Engenharia de recursos em consultas SQL
Olá rótulo geração e Geografia conversão exploração consultas também podem ser usado toogenerate rótulos/recursos removendo Olá parte de contagem. São fornecidos exemplos SQL engenharia de recurso adicional Olá [exploração de dados e de engenharia de recurso no bloco de anotações do IPython](#ipnb) seção. É mais eficiente toorun Olá recurso geração consultas na Olá conjunto de dados completo ou um grande subconjunto dela usando consultas SQL que são executados diretamente na instância de banco de dados do SQL Server de saudação. Olá consultas podem ser executadas no **SQL Server Management Studio**, bloco de anotações do IPython ou qualquer ferramenta/ambiente de desenvolvimento que pode acessar Olá banco de dados local ou remotamente.

#### <a name="preparing-data-for-model-building"></a>Preparando dados para criação de modelo
saudação de junções de consulta a seguir Olá **nyctaxi\_viagem** e **nyctaxi\_passagens** tabelas, gera um rótulo de classificação binária **Oblíquo**, um rótulo de classificação multiclasse **dica\_classe**e extrai uma amostra aleatória de 1% da saudação ingressado no conjunto de dados completo. Essa consulta pode ser copiada e colada diretamente no hello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta do banco de dados do SQL Server Olá instância no Azure. consulta de saudação exclui registros com incorreto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Exploração de dados e engenharia de recursos no IPython Notebook
Nesta seção, vamos realizar exploração de dados e geração de recurso usando consultas Python e SQL no banco de dados do SQL Server Olá criado anteriormente. Um bloco de anotações de IPython de exemplo chamado **machine-Learning-data-science-process-sql-story.ipynb** é fornecido no hello **de anotações do IPython exemplo** pasta. Este caderno também está disponível no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Olá sequência recomendada ao trabalhar com dados grandes é seguir hello:

* Ler em uma pequena amostra dos dados de saudação em um quadro de dados na memória.
* Execute algumas visualizações e explorações usando Olá dados amostrados.
* Testar usando dados de amostra de saudação de engenharia de recurso.
* Para exploração de dados maior, manipulação de dados e de engenharia de recurso, use os Python tooissue SQL consultas diretamente no banco de dados do SQL Server Olá Olá VM do Azure.
* Decida Olá toouse de tamanho de exemplo para criação de modelo de aprendizado de máquina do Azure.

Quando estiver pronto tooproceed tooAzure aprendizado de máquina, você pode ser:  

1. Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure. Esse método é demonstrado no hello [criando modelos no aprendizado de máquina do Azure](#mlmodel) seção.    
2. Manter Olá amostradas e os dados de engenharia planejar toouse para criar uma nova tabela de banco de dados de modelo e usar a nova tabela de saudação no hello [importar dados] [ import-data] módulo.

Olá seguem alguns exploração de dados, visualização de dados e exemplos de engenharia de recurso. Para obter mais exemplos, consulte o bloco de anotações do IPython SQL de exemplo de hello no hello **de anotações do IPython exemplo** pasta.

#### <a name="initialize-database-credentials"></a>Inicializar as credenciais de banco de dados
Inicialize as configurações de conexão de banco de dados em Olá variáveis a seguir:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Criar conexão de banco de dados
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Relatar o número de linhas e colunas na tabela nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Leitura-em uma amostra de dados pequenos de saudação banco de dados do SQL Server
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabela de exemplo do tempo tooread Olá é 6.492000 segundos  
Número de linhas e colunas recuperadas = (84952, 21)

#### <a name="descriptive-statistics"></a>Estatísticas Descritivas
Agora são dados de amostra de saudação tooexplore pronto. Vamos começar com olhando estatísticas descritivas para Olá **viagem\_distância** (ou qualquer outro) campos:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualização: exemplo de plotagem da caixa
Em seguida, examinar diagrama em caixa Olá para Olá trip distância toovisualize Olá quantis

    df1.boxplot(column='trip_distance',return_type='dict')

![Plotar nº 1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualização: exemplo de plotagem de distribuição
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plotar nº 2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualização: plotagens de barra e linha
Neste exemplo, podemos guardar a distância de viagem de saudação em cinco compartimentos e visualizar Olá compartimentação de resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Pode plotar Olá acima distribuição bin em uma barra ou gráfico como abaixo da linha

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plotar nº 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plotar nº 4][4]

#### <a name="visualization-scatterplot-example"></a>Visualização: exemplo de plotagem de dispersão
Vamos mostrar gráfico de dispersão entre **viagem\_tempo\_na\_s** e **viagem\_distância** toosee se há qualquer correlação

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plotar nº 6][6]

Da mesma forma, é possível verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plotar nº 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Saudação de amostragem sub dados no SQL
Ao preparar dados para o modelo de criação no [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net), ou pode decidir Olá **toouse de consulta SQL diretamente no módulo de importação de dados de saudação** ou manter Olá engenharia e de amostra dados em uma nova tabela, você pode usar em Olá [importar dados] [ import-data] módulo com um simples **selecione * FROM < seu\_novo\_tabela\_nome >**.

Nesta seção, vamos criar um novo toohold Olá da tabela de amostra e dados de engenharia. Um exemplo de uma consulta SQL direto para a construção de modelo é fornecido no hello [exploração de dados e de engenharia de recurso no SQL Server](#dbexplore) seção.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Crie uma tabela de exemplo e preencher com % 1 de saudação Unido tabelas. Descartar a tabela primeiro se ela existir.
Nesta seção, podemos unir tabelas Olá **nyctaxi\_viagem** e **nyctaxi\_passagens**, extrair uma amostra aleatória de 1% e manter dados de saudação de amostra em um novo nome de tabela  **nyctaxi\_um\_%**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Exploração de dados usando consultas SQL em IPython Notebook
Nesta seção, exploraremos distribuições de dados usando dados de % 1 de amostra de saudação que são mantidos em nova tabela de saudação criado anteriormente. Observe que explorações semelhantes podem ser realizadas usando tabelas originais do hello, opcionalmente usando **TABLESAMPLE** tooa dado período de tempo usando Olá resultados da exploração de saudação de toolimit exemplo ou limitando Olá **retirada \_datetime** partições, conforme ilustrado na Olá [exploração de dados e de engenharia de recurso no SQL Server](#dbexplore) seção.

#### <a name="exploration-daily-distribution-of-trips"></a>Exploração: distribuição diária de corridas
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploração: distribuição de corridas por licença
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Geração de recursos usando consultas SQL no IPython Notebook
Nesta seção gerar novos rótulos e recursos diretamente usando consultas SQL, operando na tabela de amostra de 1% Olá criada na seção anterior hello.

#### <a name="label-generation-generate-class-labels"></a>Geração de rótulo: gerar rótulos de classe
Saudação de exemplo a seguir, geramos dois conjuntos de toouse de rótulos para modelagem:

1. Rótulos de classe binária **tipped** (prevendo se uma gorjeta será fornecida)
2. Rótulos multiclasse **dica\_classe** (prevendo bin de dica de saudação ou intervalo)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Engenharia de recurso: recursos de contagem de colunas categóricas
Este exemplo transforma um campo de categoria em um campo numérico, substituindo cada categoria por contagem de saudação de suas ocorrências nos dados de saudação.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Engenharia de recurso: recursos de compartimento para colunas numéricas
Este exemplo transforma um campo numérico contínuo em intervalos de categoria predefinidos, ou seja, transformação de campo numérico em um campo de categoria.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Recurso de engenharia: extrair recursos de local de latitude/longitude decimal
Este exemplo divide representação decimal de saudação de um campo de latitude e/ou de longitude em vários campos de região de granularidade diferente, como país, cidade, cidade, bloquear, etc. Observe que Olá novos geo-campos não mapeados tooactual locais. Para saber mais sobre o mapeamento de locais de codificação geográfica, veja [Serviços REST do Bing Mapas](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verifique se a forma final de saudação da tabela de featurized Olá
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Agora, estamos prontos tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net). dados de saudação estão prontos para qualquer Olá previsão problemas identificados anteriormente, ou seja:

1. Classificação binária: toopredict ou não uma dica foi pago uma viagem.
2. Classificação multiclasse: intervalo de saudação toopredict de dica pago, de acordo com toohello classes definidas anteriormente.
3. Tarefa de regressão: o valor de saudação toopredict de dica pago para uma viagem.  

## 
            <a name="mlmodel">
            </a>Criando modelos no Azure Machine Learning
toobegin Olá exercício de modelagem, faça logon no espaço de trabalho do tooyour aprendizado de máquina do Azure. Se ainda não tiver criado um espaço de trabalho do Machine Learning, consulte [Criar um espaço de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget iniciado com o aprendizado de máquina do Azure, consulte [o que é o estúdio de aprendizado de máquina do Azure?](machine-learning-what-is-ml-studio.md)
2. Faça logon no muito[estúdio de aprendizado de máquina do Azure](https://studio.azureml.net).
3. Olá Studio Home page do fornece uma grande quantidade de informações, vídeos, tutoriais, links toohello Referência de módulos e outros recursos. Para obter mais informações sobre o aprendizado de máquina do Azure, consulte Olá [Centro de documentação do aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Uma experiência de treinamento típico consiste em seguir hello:

1. Criar uma experiência **+NEW** .
2. Obter dados de saudação tooAzure aprendizado de máquina.
3. Pré-processar, transformar e manipular dados saudação conforme necessário.
4. Gerar recursos conforme necessário.
5. Dividir dados saudação em conjuntos de dados de treinamento / / teste de validação (ou têm conjuntos de dados separados para cada).
6. Selecione um ou mais algoritmos dependendo Olá toosolve problema de aprendizado de aprendizado de máquina. Por exemplo, classificação binária, classificação multiclasse ou regressão.
7. Treine um ou mais modelos usando o conjunto de dados de treinamento hello.
8. Classificar o conjunto de dados de validação de saudação usando modelos treinados hello.
9. Avalie Olá modelos toocompute Olá relevante de métricas para Olá problema de aprendizado.
10. Ajuste Olá modelo (s) e selecione Olá melhor modelo toodeploy.

Neste exercício, nós já explorados e engenharia dados Olá no SQL Server e decidir sobre tooingest de tamanho de exemplo hello no aprendizado de máquina do Azure. toobuild um ou mais dos modelos de previsão Olá decidimos:

1. Obter dados de saudação tooAzure aprendizado de máquina usando Olá [importar dados] [ import-data] módulo, disponível no hello **dados de entrada e saída** seção. Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência de módulo.
   
    ![Importar Dados no Azure Machine Learning][17]
2. Selecione **banco de dados do SQL Azure** como Olá **fonte de dados** em Olá **propriedades** painel.
3. Digite o nome DNS de banco de dados de saudação em Olá **nome do servidor de banco de dados** campo. Formato: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Digite hello **nome do banco de dados** no campo correspondente do hello.
5. Digite hello **nome de usuário SQL** em hello * * aqccount nome de usuário e senha Olá Olá **senha de conta de usuário do servidor**.
6. Marque a opção **Aceitar qualquer certificado do servidor** .
7. Em Olá **consulta de banco de dados** editar a área de texto, cole a consulta Olá extrai Olá necessário campos (incluindo quaisquer campos calculados como rótulos de saudação) de banco de dados e para baixo amostras de tamanho de exemplo hello dados toohello desejado.

É um exemplo de um experimento de classificação binária ler dados diretamente do banco de dados do SQL Server Olá figura de saudação abaixo. Experimentos semelhantes podem ser construídos por meio de classificação multiclasse e problemas de regressão.

![Treinamento do Azure Machine Learning][10]

> [!IMPORTANT]
> Em Olá modelagem de extração de dados e exemplos de consulta fornecidos nas seções anteriores, de amostragem **todos os rótulos para os exercícios de modelagem Olá três são incluídos na consulta Olá**. Uma etapa importante (obrigatório) em cada Olá exercícios de modelagem é muito**excluir** Olá rótulos desnecessários para Olá outros dois problemas e qualquer outro **vazamentos de destino**. Para por exemplo, ao usar a classificação binária, use rótulo Olá **Oblíquo** e excluir campos Olá **dica\_classe**, **dica\_quantidade**, e **total\_quantidade**. Olá último vazamentos de destino já que eles implicam dica Olá pagas.
> 
> as colunas desnecessárias tooexclude e/ou vazamentos de destino, você pode usar o hello [selecionar colunas no conjunto de dados] [ select-columns] módulo ou hello [editar metadados] [ edit-metadata]. Para saber mais, veja as páginas de referência [Selecionar Colunas no Conjunto de Dados][select-columns] e [Editar Metadados][edit-metadata].
> 
> 

## 
            <a name="mldeploy">
            </a>Implantando modelos no Azure Machine Learning
Quando o modelo estiver pronto, pode facilmente implantá-lo como um serviço web diretamente do experimento hello. Para obter mais informações sobre como implantar os serviços Web do Azure Machine Learning, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy um novo serviço da web, você precisa:

1. Criar um experimento de pontuação.
2. Implante o serviço web de saudação.

toocreate experiência de uma pontuação de um **concluído** experiência de treinamento, clique em **criar experiência de PONTUAÇÃO** na barra de ação inferior hello.

![Pontuação do Azure][18]

O aprendizado de máquina do Azure tentará toocreate uma experiência de pontuação com base nos componentes de saudação da experiência de treinamento hello. Em especial, ele vai:

1. Salvar modelo treinado hello e remover os módulos de treinamento de modelo de saudação.
2. Identificar uma lógica **porta de entrada** toorepresent Olá esperado o esquema de dados de entrada.
3. Identificar uma lógica **porta de saída** o esquema de saída de serviço do toorepresent Olá web esperado.

Quando Olá experimento de pontuação é criado, examiná-la e ajustar conforme necessário. Um ajuste típico é tooreplace Olá dataset de entrada e/ou consulta com uma que exclui os campos de rótulo, como eles não estarão disponíveis quando Olá serviço é chamado. Também é que um tamanho de saudação tooreduce uma boa prática de saudação tooa de consulta e/ou conjunto de dados de entrada suficientes esquema de entrada hello tooindicate de alguns registros. Para a porta de saída de hello, é tooexclude comuns entrados todos os campos e incluir apenas Olá **rótulos de pontuação** e **probabilidades pontuadas** em Olá saída usando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.

É um exemplo de experiência de pontuação na figura abaixo a saudação. Quando estiver pronto toodeploy, clique em Olá **publicar WEB SERVICE** botão na barra de ação inferior hello.

![Publicação do Azure Machine Learning][11]

toorecap, neste tutorial passo a passo, você criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados público entre grande todo caminho de saudação do toomodel de aquisição de dados de treinamento e a implantação de um serviço web de aprendizado de máquina do Azure.

### <a name="license-information"></a>Informações de Licença
Este exemplo passo a passo e seu que acompanha scripts e IPython notebook(s) são compartilhados pela Microsoft sob a licença do MIT hello. Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.

### <a name="references"></a>Referências
•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
