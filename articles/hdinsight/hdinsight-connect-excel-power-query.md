---
title: aaaConnect Excel tooHadoop com o Power Query - HDInsight do Azure | Microsoft Docs
description: Saiba como tootake vantagem dos componentes do business intelligence e use o Power Query para dados do Excel tooaccess armazenados no Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.openlocfilehash: 1213849f1bc04e0ed206750b80766ff2268664b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-by-using-power-query"></a>Conectar Excel tooHadoop usando o Power Query
Um recurso importante da solução de dados grandes do Microsoft hello é a integração de saudação de componentes do Microsoft business intelligence (BI) com clusters Hadoop em HDInsight do Azure. Um exemplo principal é Olá capacidade tooconnect Excel toohello conta de armazenamento do Azure que contém dados de saudação associados ao cluster de Hadoop usando Olá Microsoft Power Query para Excel no. Este artigo o orienta como tooset backup e usar dados do Power Query tooquery associados a um cluster de Hadoop gerenciavam com HDInsight.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter Olá itens a seguir:

* **Um cluster HDInsight**. tooconfigure um, consulte [Introdução ao Azure HDInsight][hdinsight-get-started].
* **estação de trabalho** que esteja executando Windows 7, Windows Server 2008 R2 ou um sistema operacional posterior.
* **Office 2016, Office 2013 Professional Plus, Office 365 ProPlus, Excel 2013 autônomo ou Office 2010 Professional Plus**.

## <a name="install-power-query"></a>Instalar o Power Query
O Power Query pode importar dados que foram retornados ou que foram gerados por um trabalho Hadoop em execução em um cluster HDInsight.

No Excel 2016, o Power Query foi integrado à faixa de opções de dados de saudação em Olá Get & Transform seção. Para versões anteriores do Excel, baixe o Microsoft Power Query para Excel de Olá [Microsoft Download Center] [ powerquery-download] e instalá-lo.

## <a name="import-hdinsight-data-into-excel"></a>Importar dados do HDInsight para o Excel
Olá suplemento do Power Query para Excel torna fácil tooimport dados do seu cluster HDInsight no Excel, onde as ferramentas de BI como PowerPivot e Power mapa podem ser tooinspect usado, analisar e apresentar dados hello.

**tooimport dados de um cluster do HDInsight**

1. Abra o Excel.
2. Crie uma nova pasta de trabalho em branco.
3. Execute Olá etapas com base na versão do Excel Olá a seguir:

    - Excel 2016

        - Clique em Olá **dados** menu, clique em **obter dados** de saudação **obter & transformar dados** de faixa de opções, clique em **do Azure**e, em seguida, clique em  **Do Azure HDInsight(HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Clique em Olá **Power Query** menu, clique em **do Azure**e, em seguida, clique em **do Microsoft Azure HDInsight**.
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Observação:** se você não vir Olá **Power Query** menu Ir muito**arquivo** > **opções** > **suplementos**e selecione **suplementos COM** na lista suspensa Olá **gerenciar** caixa Olá inferior da página de saudação. Selecione Olá **ir...**  botão e verifique se essa caixa Olá para hello Power Query para Excel em foi verificada.
       
        **Observação:** Power Query também permite que você tooimport dados do HDFS clicando **de outras fontes**.
4. Para **nome da conta**, insira Olá nome da conta de armazenamento de BLOBs do Azure Olá associada ao cluster e, em seguida, clique em **Okey**. Essa conta pode ser Olá [conta de armazenamento padrão](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) ou uma conta de armazenamento vinculada.  formato de saudação é *https://&lt;StorageAccountName >.blob.core.windows.net/*.
5. Para **chave de conta**, insira a chave Olá Olá conta de armazenamento de Blob e, em seguida, clique em **salvar**. (Necessário tooenter Olá conta informações somente Olá primeira vez que você acessa esse repositório.)
6. Em Olá **navegador** painel Olá à esquerda do Editor de consultas de saudação, clique duas vezes no nome do contêiner de armazenamento de Blob de saudação. Por padrão, o nome de contêiner Olá é Olá mesmo nome como o nome do cluster hello.
7. Localize **HiveSampleData.txt** em Olá **nome** coluna (Olá caminho da pasta é **... / hive/warehouse/hivesampletable/**) e, em seguida, clique em **binário** esquerda de saudação do HiveSampleData.txt. HiveSampleData.txt vem com todos os cluster de saudação. Se desejar, você pode usar seu próprio arquivo.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Se desejar, você pode renomear os nomes de coluna hello. Quando estiver pronto, clique em **Fechar e Carregar**.  dados de saudação foi carregado tooyour de pasta de trabalho:
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse dados do Power Query tooretrieve do HDInsight para o Excel. Da mesma forma, você pode recuperar dados do HDInsight no banco de dados SQL do Azure. Também é dados tooupload possíveis no HDInsight. toolearn mais, consulte Olá artigos a seguir:

* [Conectar Excel tooHDInsight com hello Microsoft ODBC Driver Hive][hdinsight-ODBC]
* [Carregar dados tooHDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689
