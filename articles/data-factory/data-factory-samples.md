---
title: aaaAzure Data Factory - exemplos
description: "Fornece detalhes sobre os exemplos fornecidos com hello serviço do Azure Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Azure Data Factory - Exemplos
## <a name="samples-on-github"></a>Exemplos no GitHub
Olá [repositório GitHub do Azure-DataFactory](https://github.com/azure/azure-datafactory) contém vários exemplos que ajudam você rapidamente de aprendizado com o serviço do Azure Data Factory (ou) modificar scripts hello e usá-lo no próprio aplicativo. pasta de Samples\JSON Olá contém trechos de código JSON para cenários comuns.

| Amostra | Descrição |
|:--- |:--- |
| [Passo a passo do ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |Este exemplo fornece uma passo a passo de ponta a ponta para o processamento de arquivos de log usando os dados do Azure Data Factory tooturn dos arquivos de log em tooinsights. <br/><br/>Neste passo a passo, pipeline da fábrica de dados Olá coleta logs de exemplo, processos e enriquece dados Olá logs com os dados de referência e transforma Olá dados tooevaluate Olá a eficácia de uma campanha de marketing que foi iniciada recentemente. |
| [Exemplos JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |Este exemplo fornece exemplos JSON para cenários comuns. |
| [Exemplo de HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Este exemplo apresenta download de dados de um ponto de extremidade HTTP tooAzure armazenamento de Blob usando a atividade personalizada do .NET. |
| [Exemplo de atividade AppDomain Dot Net](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Este exemplo permite que você tooauthor uma atividade personalizada do .NET que não é restrita versões tooassembly usadas pelo iniciador do ADF hello (por exemplo, v 4.3.0 do windowsazure v6.0.x newtonsoft. JSON, etc.). |
| [Executar script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Este exemplo inclui Olá Data Factory atividade personalizada que pode ser usado tooinvoke RScript.exe. Esse exemplo funciona apenas no seu próprio cluster HDInsight (não sob demanda) que já tenha o R instalado nele. |
| [Invocar trabalhos Spark no cluster Hadoop do HDInsight](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |Este exemplo mostra como toouse MapReduce atividade tooinvoke um programa Spark. programa de spark Olá apenas copia dados de um tooanother de contêiner de BLOBs do Azure. |
| 
            [Análise do Twitter usando a Atividade de Pontuação em Lotes do Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |Este exemplo mostra como modelo toouse AzureMLBatchScoringActivity tooinvoke o aprendizado de máquina do Azure que executa a análise de sentimento do twitter, pontuação, previsão etc. |
| [Análise do Twitter usando a atividade personalizada](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Este exemplo mostra como toouse uma tooinvoke de atividade .NET personalizado um modelo de aprendizado de máquina do Azure que executa twitter análise de sentimento, pontuação, previsão etc. |
| 
            [Pipelines com parâmetros para o Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |exemplo Hello fornece uma ponta a ponta c# código toodeploy N pipelines para classificar e treinamento, cada um com um parâmetro de região diferente onde lista Olá de regiões vem de um arquivo parameters.txt, que é incluído com este exemplo. |
| [Atualização de dados de referência para trabalhos de Stream Analytics do Azure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |Este exemplo mostra como a atualização de toouse fábrica de dados do Azure e o Azure Stream Analytics toorun juntos Olá consultas com hello de configuração e dados de referência para os dados de referência em uma agenda. |
| [Pipeline híbrido com Hadoop Hortonworks local](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |exemplo Hello usa um cluster de Hadoop local como um destino de computação para trabalhos em execução no fábrica de dados exatamente como você poderia adicionar outros destinos de computação como um HDInsight com base em cluster de Hadoop na nuvem. |
| [Ferramenta de conversão JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |Essa ferramenta permite que você tooconvert JSON da versão anterior too2015-07-01-preview toolatest ou 2015-07-01-preview (padrão). |
| [Arquivo de entrada de exemplo U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Este é um arquivo de exemplo usado por uma atividade U-SQL. |
| [Excluir arquivo de blob](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | Este exemplo demonstra um arquivo c# que pode ser usado como parte do ADF .net atividade toodelete arquivos personalizados de fonte Olá local de Blob do Azure quando Olá arquivos foram copiados.|

## <a name="azure-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Azure
Você pode encontrar hello Azure Resource Manager modelos a seguir fábrica de dados no GitHub.

| Modelo | Descrição |
| --- | --- |
| [Copiar do armazenamento de BLOBs do Azure tooAzure banco de dados SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Implantar este modelo cria uma fábrica de dados do Azure com um pipeline que copia dados da saudação especificado banco de dados SQL do Azure toohello de armazenamento de BLOBs do Azure |
| [Copiar da equipe de vendas tooAzure armazenamento de Blob](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Implantar este modelo cria uma fábrica de dados do Azure com um pipeline que copia dados da saudação especificado armazenamento de BLOBs do Azure de toohello de conta Salesforce. |
| [Transformar dados executando o script Hive em um cluster do Azure HDInsight](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |Implantar este modelo cria uma fábrica de dados do Azure com um pipeline que transforma os dados, executando o script de Hive do exemplo hello em um cluster de Hadoop de HDInsight do Azure. |

## <a name="samples-in-azure-portal"></a>Exemplos no portal do Azure
Você pode usar o hello **pipelines de exemplo** lado a lado na página inicial do hello seus pipelines de exemplo de toodeploy de fábrica de dados e suas entidades associadas (conjuntos de dados e serviços vinculados) tooyour fábrica de dados.

1. Crie uma data factory ou abra uma existente. Consulte [copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para etapas toocreate uma fábrica de dados.
2. Em Olá **DATA FACTORY** folha Olá fábrica de dados, clique em Olá **pipelines de exemplo** lado a lado.

    ![Bloco Pipelines de exemplo](./media/data-factory-samples/SamplePipelinesTile.png)
3. Em Olá **pipelines de exemplo** folha, clique em Olá **exemplo** que você deseja toodeploy.

    ![Folha Pipelines de exemplo](./media/data-factory-samples/SampleTile.png)
4. Especifica definições de configuração de exemplo hello. Por exemplo, sua chave e nome da conta de armazenamento do Azure, o nome do SQL Server do Azure, banco de dados, ID de usuário e senha etc.

    ![Folha Exemplo](./media/data-factory-samples/SampleBlade.png)
5. Depois que você especificar configurações de saudação, clique em **criar** toocreate/implantar Olá pipelines de exemplo e usadas pelo pipelines Olá serviços/tabelas vinculadas.
6. Você ver o status de saudação de implantação no bloco do exemplo hello clicado anteriormente Olá **pipelines de exemplo** folha.

    ![Status da Implantação](./media/data-factory-samples/DeploymentStatus.png)
7. Quando você vir Olá **implantação bem-sucedida** mensagem no bloco de saudação do exemplo hello, Olá fechar **pipelines de exemplo** folha.  
8. Em **DATA FACTORY** folha, consulte serviços vinculados, conjuntos de dados e pipelines são adicionados tooyour fábrica de dados.  

    ![Folha Data Factory](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Exemplos no Visual Studio
### <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte Olá instalado em seu computador:

* Visual Studio 2013 ou Visual Studio 2015
* Baixe o SDK do Azure para Visual Studio 2013 ou Visual Studio de 2015. Navegue muito[página de Download do Azure](https://azure.microsoft.com/downloads/) e clique em **VS 2013** ou **VS 2015** em Olá **.NET** seção.
* Baixar hello mais recente do Azure Data Factory plug-in para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Se você estiver usando o Visual Studio 2013, você também pode atualizar o plug-in de saudação fazendo Olá etapas a seguir: Olá menu, clique em **ferramentas** -> **extensões e atualizações**  ->  **Online** -> **Galeria do Visual Studio** -> **ferramentas de fábrica de dados do Microsoft Azure para Visual Studio**  ->  **Atualização**.

### <a name="use-data-factory-templates"></a>Use modelos de Data Factory
1. Clique em **arquivo** no menu de hello, aponte muito**novo**e clique em **projeto**.
2. Em Olá **novo projeto** caixa de diálogo caixa, Olá seguintes etapas:

   1. Selecione **DataFactory** em **Modelos**.
   2. Selecione **modelos de fábrica de dados** no painel direito da saudação.
   3. Insira um **nome** para projeto de saudação.
   4. Selecione um **local** para projeto de saudação.
   5. Clique em **OK**.

      ![Caixa de diálogo Novo projeto](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. Em Olá **modelos de fábrica de dados** caixa de diálogo, o modelo de exemplo hello select de saudação **modelos de caso de uso** seção e, em seguida, clique em **próximo**. Olá etapas a seguir orientam usando Olá **criação de perfil de cliente** modelo. As etapas são semelhantes para Olá outros exemplos.

    ![Caixa de diálogo Modelos de Data Factory](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. Em Olá **configuração de fábrica de dados** caixa de diálogo, clique em **próximo** em Olá **Noções básicas de fábrica de dados** página.
5. Em Olá **fábrica de dados configurar** página, Olá seguintes etapas:
   1. Selecione **Criar Nova Fábrica de Dados**. Você também pode selecionar **Usar data factory existente**.
   2. Insira um **nome** Olá fábrica de dados.
   3. Selecione Olá **assinatura do Azure** no qual você deseja Olá toobe de fábrica de dados criado.
   4. Selecione Olá **grupo de recursos** Olá fábrica de dados.
   5. Selecione Olá **Oeste dos EUA**, **Leste dos EUA**, ou **Norte da Europa** para Olá **região**.
   6. Clique em **Avançar**.
6. Em Olá **configurar armazenamentos de dados** página, especifique um existente **banco de dados do SQL Azure** e **conta de armazenamento do Azure** (ou) criar/armazenamento de banco de dados e clique em Avançar.
7. Em Olá **configurar computação** página, selecione os padrões e clique em **próximo**.
8. Em Olá **resumo** página, examine todas as configurações e clique em **próximo**.
9. Em Olá **Status da implantação** , aguarde até que a implantação Olá for concluída e, em **concluir**.
10. Clique com botão direito no Gerenciador de soluções do hello e, em seguida, clique em **publicar**.
11. Se você vir **entrar na conta da Microsoft de tooyour** caixa de diálogo, insira suas credenciais de conta de saudação que tenha a assinatura do Azure e clique em **entrar**.
12. Você deve ver Olá caixa de diálogo a seguir:

    ![Caixa de diálogo Publicar](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. Em Olá **fábrica de dados configurar** página, Olá seguintes etapas:

    1. Confirme a opção **Usar data factory existente** .
    2. Selecione Olá **fábrica de dados** tinha select ao usar o modelo de saudação.
    3. Clique em **próximo** tooswitch toohello **publicar itens** página. (Pressione **guia** toomove fora Olá Olá de tooif do campo de nome **próximo** botão será desabilitado.)
14. Em Olá **publicar itens** página, certifique-se de que todos os Olá fábricas de dados de entidades são selecionadas e clique em **próximo** tooswitch toohello **resumo** página.     
15. Revise o resumo de saudação e clique em **próximo** Olá de processo e o modo de exibição de implantação de saudação do toostart **Status da implantação**.
16. Em Olá **Status da implantação** página, você deve ver o status de Olá Olá do processo de implantação. Após a conclusão da implantação de saudação, clique em Concluir.

Consulte [criar sua primeira fábrica de dados (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) para obter detalhes sobre o uso de entidades de fábrica de dados do Visual Studio tooauthor e publicá-los tooAzure.          
