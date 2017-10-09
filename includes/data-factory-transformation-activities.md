A fábrica de dados do Azure oferece suporte a saudação seguintes atividades de transformação que podem ser adicionado toopipelines individualmente ou encadeada com outra atividade.

| Atividades de transformação de dados | Ambiente de computação |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Streaming do Hadoop](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Atividades de Machine Learning: execução do Lote e recurso de atualização](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |VM do Azure |
| [Procedimento armazenado](../articles/data-factory/data-factory-stored-proc-activity.md) |SQL Azure, Azure SQL Data Warehouse ou SQL Server |
| [U-SQL da Análise Data Lake](../articles/data-factory/data-factory-usql-activity.md) |Análise Azure Data Lake |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] ou Lote do Azure |

> [!NOTE]
> Você pode usar programas de Spark MapReduce atividade toorun no seu cluster HDInsight Spark. Consulte [Invoke Spark programs from Azure Data Factory (Invocar programas Spark da Azure Data Factory)](../articles/data-factory/data-factory-spark.md) para obter detalhes.
> Você pode criar uma atividade personalizada toorun R scripts em seu cluster HDInsight com R instalado. Veja [Executar scripts R usando o Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).
> 
> 

