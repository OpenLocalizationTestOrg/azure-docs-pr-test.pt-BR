---
title: aaaUse ScaleR e SparkR com o Azure HDInsight | Microsoft Docs
description: Usar ScaleR e SparkR com R Server e HDInsight
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>Combinar o ScaleR e o SparkR no HDInsight

Este artigo mostra como toopredict flight atrasos de chegada usando um **ScaleR** associada do modelo de regressão logística dos dados em atrasos de voo e o clima **SparkR**. Este cenário demonstra os recursos de saudação do ScaleR para manipulação de dados no Spark usado com o Microsoft R Server para análise. combinação de Olá dessas tecnologias permite que você os recursos mais recentes do tooapply Olá no processamento distribuído.

Embora ambos os pacotes são executados no mecanismo de execução do Hadoop Spark, eles são bloqueados do compartilhamento de dados na memória já que cada um deles exige suas próprias respectivas sessões Spark. Até que esse problema é resolvido em uma versão futura do R Server, solução de saudação é toomaintain sessões de Spark sem sobreposição e tooexchange dados por meio de arquivos intermediários. instruções de saudação aqui mostram que esses requisitos são tooachieve simples.

Podemos usar um exemplo aqui inicialmente compartilhado em uma conversa em segmentos 2016 Mario Inchiosa e Roni Burd que também está disponível por meio de saudação webinar [criação de uma plataforma escalonável de ciência de dados com R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). exemplo hello usa SparkR toojoin Olá conjunto de dados conhecidos airlines chegada atraso com dados de clima em aeroportos de saída e entrada. dados Olá associados são usados como modelo de regressão logística ScaleR tooa entrada para a previsão de atraso de chegada de voo.

saudação de código, passo a passo foi gravado originalmente para R Server em execução no Spark em um cluster HDInsight no Azure. Mas o conceito de saudação de misturar o uso de saudação do SparkR e ScaleR em um script também é válido no contexto de saudação de ambientes locais. No seguinte Olá, podemos supor que um nível intermediário de dados de Conhecimento de R e R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) biblioteca do servidor do R. Também apresentamos o uso de [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) ao percorrer esse cenário.

## <a name="hello-airline-and-weather-datasets"></a>Olá aérea e clima conjuntos de dados

Olá **AirOnTime08to12CSV** pública companhias aéreas de conjunto de dados contém informações sobre a chegada de voo e detalhes de partida para todas as voos comerciais em Olá EUA, de tooDecember de 1987 de outubro de 2012. Esse é um conjunto de dados grande: há quase 150 milhões de registros no total. Tem pouco menos de 4 GB quando descompactado. Ele está disponível no hello [arquivos mortos do governo dos EUA](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Mais conveniente, ele está disponível como um arquivo zip (AirOnTimeCSV.zip) que contém um conjunto de 303 separado mensal CSV arquivos Olá [repositório de conjunto de dados do Revolution Analytics](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

efeitos de saudação toosee de clima em atrasos de voo, é preciso também dados de tempo de saudação em cada aeroportos hello. Esses dados podem ser baixados como arquivos zip na forma bruta, por mês, de saudação [repositório oceânico nacional e administração atmosféricas](http://www.ncdc.noaa.gov/orders/qclcd/). Para fins de Olá deste exemplo, podemos extrair dados de tempo de maio de 2007 – dezembro de 2012 e arquivos de dados por hora hello dentro de cada zips de mensal 68 Olá usados. arquivos zip mensal de saudação também contêm um mapeamento (YYYYMMstation.txt) entre a estação de clima Olá ID (WBAN), aeroporto Olá que é associado (prefixo) e Olá deslocamento de fuso horário do aeroporto do UTC (fuso horário). Todas essas informações é necessária ao ingressar com dados de atraso e o clima aérea hello.

## <a name="setting-up-hello-spark-environment"></a>Configurando o ambiente do Spark Olá

Olá primeira etapa é tooset o ambiente do Spark hello. Começamos apontando toohello diretório que contém os diretórios de dados de entrada, criando um contexto de computação Spark e criando uma função de registro em log para o log informativa toohello console:

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Em seguida, adicionar caminho de pesquisa de toohello de "Spark_Home" para pacotes de R para que possamos usar SparkR e inicializar uma sessão de SparkR:

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>Preparando dados de clima Olá

tooprepare os dados de clima hello, podemos subconjunto-toohello colunas necessárias para modelagem: 

- "Visibilidade"
- "DryBulbCelsius"
- "DewPointCelsius"
- "RelativeHumidity"
- "WindSpeed"
- "Altímetro"

Em seguida, adicionamos um código do aeroporto associado com a estação de clima Olá e converter medidas de saudação do tooUTC de hora local.

Vamos começar criando um código de aeroporto arquivo toomap Olá clima estação (WBAN) informações tooan. Foi possível obter esse correlação saudação do arquivo de mapeamento incluído com os dados de clima hello. Por Olá mapeamento *prefixo* (por exemplo, LAX) campo no arquivo de dados de clima Olá muito*origem* nos dados de passagens áreas hello. No entanto, acabamos de toohave outro disponível mapeamento que mapeia *WBAN* muito*AirportID* (por exemplo, 12892 para LAX) e inclui *fuso horário* que foi salvo tooa Arquivo CSV chamado "wban-para-aeroporto-id-tz. CSV"que podemos usar. Por exemplo:

| AirportID | WBAN | timeZone
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

Olá seguindo o código lê cada dos dados de clima processados por hora Olá arquivos, colunas de toohello subconjuntos é necessário, mescla o arquivo de mapeamento de estação de clima hello, ajusta Olá DateTimes de medidas tooUTC e, em seguida, grava uma nova versão do arquivo hello:

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>Importando Olá aérea e clima dados tooSpark quadros de dados

Agora podemos usar Olá SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) função tooimport Olá clima e aérea dados tooSpark quadros de dados. Essa função, assim como muitos outros métodos do Spark, é executada lentamente, o que significa que eles são enfileirados para execução, mas não executados até que isso seja necessário.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Limpeza de dados e transformação

Em seguida, fazemos uma limpeza em dados de passagens áreas Olá já importamos toorename colunas. Apenas manter Olá variáveis necessárias e tempos de saída agendado para baixo toohello mais próximo de hora tooenable a mesclagem com dados mais recentes de clima Olá na saída de ida e volta:

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Agora podemos realizar operações semelhantes em dados de tempo de saudação:

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Associação de dados de clima e aérea Olá

Agora podemos usar Olá SparkR [JOIN ()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) função toodo uma junção externa esquerda dos dados de aérea e previsão do tempo de saudação pela saída AirportID e datetime. junção externa Olá nos permite tooretain todos os dados de passagens áreas Olá registra mesmo se não houver nenhum dado de tempo correspondente. Após a associação de Olá, remover algumas colunas redundantes e renomear Olá mantido tooremove Olá entrada DataFrame prefixo de colunas introduzido pela junção hello.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

De maneira semelhante, podemos unir dados de clima e aérea de saudação com base na chegada AirportID e a data e hora:

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Salvar resultados tooCSV para o exchange com ScaleR

Isso conclui junções Olá precisamos toodo com SparkR. É salvar dados de saudação do hello final Spark DataFrame "joinedDF5" tooa CSV para entrada tooScaleR e Fechar sessão de SparkR hello. Dizemos explicitamente SparkR toosave Olá CSV resultante no paralelismo suficientes do tooenable 80 partições separadas no processamento de ScaleR:

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>Importar tooXDF para uso por ScaleR

Podemos usar arquivo CSV Olá aérea associada e como os dados de clima-é para modelagem por meio de uma fonte de dados de texto ScaleR. Mas, importá-lo tooXDF primeiro, pois ela é mais eficiente ao executar várias operações no conjunto de dados hello:

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Dividindo dados para treinamento e teste

Podemos usar toosplit rxDataStep os dados de 2012 Olá para testar e manter rest Olá para treinamento:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Treinar e testar um modelo de regressão logística

Agora estamos pronto toobuild um modelo. influência de saudação toosee de dados de clima no atraso no tempo de chegada de saudação, usamos rotina de regressão logística da ScaleR. Nós usamos toomodel se um atraso de chegada de mais de 15 minutos é influenciado pelo tempo Olá em aeroportos de saída e entrada hello:

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Agora vamos ver como ele em Olá testar dados fazendo algumas previsões e examinando ROC e AUC.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Pontuação em outro lugar

Podemos também pode usar o modelo de saudação para dados de pontuação em outra plataforma. Salvando-o arquivo RDS tooan e, em seguida, transferir e importando que RDS em um ambiente, como o SQL Server R Services a pontuação de destino. É importante tooensure que níveis de fator de saudação de Olá dados toobe classificado correspondam no qual Olá modelo foi criado. Que correspondência pode ser obtida por meio da extração e salvar informações de coluna Olá associado Olá modelagem de dados por meio do ScaleR `rxCreateColInfo()` função e, em seguida, aplicar essa fonte de dados de entrada coluna informações toohello para previsão. Seguir Olá podemos salvar algumas linhas de conjunto de dados de teste de saudação e extrair e usar informações de coluna Olá deste exemplo no script de previsão hello:

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Resumo

Neste artigo, mostramos como é usar os possíveis toocombine do SparkR para manipulação de dados com ScaleR para o desenvolvimento de modelos no Hadoop Spark. Esse cenário requer que você mantenha sessões do Spark separadas, executando somente uma sessão por vez e que troque dados por meio de arquivos CSV. Embora seja simples, esse processo deve ser mais fácil em uma versão futura do R Server, quando SparkR e ScaleR puderem compartilhar uma sessão do Spark e, assim, compartilhar Spark DataFrames.

## <a name="next-steps-and-more-information"></a>Próximas etapas e mais informações

- Para obter mais informações sobre o uso do servidor de R no Spark, consulte Olá [guia de Introdução do MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- Para obter informações gerais sobre o R Server, consulte Olá [começar com R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) artigo.

- Para obter informações sobre o R Server no HDInsight, consulte [Visão geral do R Server no Azure HDInsight](hdinsight-hadoop-r-server-overview.md) e [R Server no Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).

Para obter mais informações sobre o uso de SparkR, veja:

- [Documento Apache SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [Visão geral do SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) da Databricks
