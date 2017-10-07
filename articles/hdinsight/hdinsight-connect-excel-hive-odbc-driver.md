---
title: aaaConnect Excel tooHadoop com hello Hive ODBC Driver - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooset backup e use Olá Microsoft Hive ODBC driver para dados do Excel tooquery em clusters de HDInsight do Microsoft Excel."
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a>Conectar Excel tooHadoop no Azure HDInsight com hello Hive do Microsoft ODBC driver

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Solução de Big Data da Microsoft integra componentes do Microsoft Business Intelligence (BI) com clusters Apache Hadoop que foram implantados por hello Azure HDInsight. Um exemplo dessa integração é Olá capacidade tooconnect Excel toohello Hive do data warehouse de um cluster de Hadoop no HDInsight usando Olá Driver Microsoft Hive ODBC Open Database Connectivity ().

Também é possível tooconnect dados de Olá associados a um cluster HDInsight e outras fontes de dados, incluindo outra (não-HDInsight) Hadoop clusters do Excel usando Olá suplemento do Microsoft Power Query para Excel. Para obter informações sobre como instalar e usar o Power Query, consulte [tooHDInsight Excel conectar-se com o Power Query][hdinsight-power-query].

> [!NOTE]
> Enquanto Olá etapas neste artigo pode ser usado com qualquer um Linux ou cluster HDInsight baseados no Windows, o Windows é necessária para a estação de trabalho de cliente hello.
> 
> 

**Pré-requisitos**:

Antes de começar este artigo, você deve ter Olá itens a seguir:

* **Um cluster HDInsight**. toocreate um, consulte [Introdução ao Azure HDInsight][hdinsight-get-started].
* **estação de trabalho** com Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.

## <a name="install-microsoft-hive-odbc-driver"></a>Instalar o driver ODBC do Microsoft Hive
Baixe e instale o Microsoft ODBC Driver Hive da saudação [Centro de Download][hive-odbc-driver-download].

Este driver pode ser instalado em versões de 32 ou 64 bits do Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012. driver de saudação permite conexão tooAzure HDInsight (versão 1.6 e posterior) e o emulador de HDInsight do Azure (v.1.0.0.0 e posterior). Você deve instalar a versão de saudação que corresponde à versão de saudação do aplicativo hello onde você pode usar o driver ODBC hello. Para este tutorial, o driver de saudação é usado do Office Excel.

## <a name="create-hive-odbc-data-source"></a>Criar uma fonte de dados ODBC do Hive
Olá etapas a seguir mostram como toocreate uma fonte de dados ODBC Hive.

1. Windows 8 ou Windows 10, pressione a tela inicial do hello Windows tooopen chave hello e, em seguida, digite **fontes de dados**.
2. Clique em **Configurar fontes de dados ODBC (32 bits)** ou **Configurar fontes de dados ODBC (64 bits)**, dependendo da sua versão do Office. Se estiver usando o Windows 7, escolha **Fontes de Dados ODBC (32 bits)** ou **Fontes de Dados ODBC (64 bits)** em **Ferramentas Administrativas**. Você deverá ver Olá **administrador de fonte de dados ODBC** caixa de diálogo.
   
    ![Administrador de fonte de dados ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurar um DSN usando o Administrador de Fonte de Dados ODBC")

3. Do DNS do usuário, clique em **adicionar** tooopen Olá **criar nova fonte de dados** assistente.
4. Selecione **Driver ODBC do Microsoft Hive** e clique em **Concluir**. Você deverá ver Olá **Microsoft Hive ODBC Driver DNS instalação** caixa de diálogo.
5. Digite ou selecione Olá valores a seguir:
   
   | Propriedade | Descrição |
   | --- | --- |
   |  Nome da fonte de dados |Dê uma fonte de dados do nome tooyour |
   |  Host |Digite &lt;HDInsightClusterName>.azurehdinsight.net. Por exemplo, meu_Cluster_HDI.azurehdinsight.net |
   |  Port |Use <strong>443</strong>. (Essa porta foi alterada de 563 too443.) |
   |  Banco de dados |Use <strong>Padrão</strong>. |
   |  Mecanismo |Selecione <strong>Serviço do Azure HDInsight</strong> |
   |  Nome de usuário |Insira o nome de usuário HTTP do cluster HDInsight. é o nome de usuário do saudação padrão <strong>admin</strong>. |
   |  Senha |Insira a senha do usuário do cluster HDInsight. |
   
    </table>
   
    Há alguns parâmetros importantes toobe ciente de quando você clica em **opções avançadas de**:
   
   | Parâmetro | Descrição |
   | --- | --- |
   |  Use Consulta Nativa |Quando estiver selecionada, o driver ODBC Olá não tentará tooconvert TSQL em HiveQL. Você deverá usar essa opção somente se estiver 100% certo de que está enviando instruções HiveQL puras. Ao se conectar tooSQL servidor ou banco de dados do SQL Azure, deixe-a desmarcada. |
   |  Linhas buscadas por bloco |Ao buscar um grande número de registros, ajuste desse parâmetro pode ser o desempenho ideal de tooensure necessária. |
   |  Comprimento de coluna de cadeia de caracteres padrão, Comprimento da coluna binária e Escala da coluna decimal |tipo de dados de saudação comprimentos e precisões podem afetar como os dados são retornados. Que causem toobe informações incorretas retornado devido tooloss de precisão e/ou truncamento. |

    ![Opções avançadas](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opções de configuração de DSN avançadas")

1. Clique em **teste** tootest fonte de dados de saudação. Quando a fonte de dados hello está configurado corretamente, ele mostra *testes concluídos com êxito!*.
2. Clique em **Okey** caixa de diálogo de teste do tooclose hello. nova fonte de dados Olá deverá ser listado na Olá **administrador de fonte de dados ODBC**.
3. Clique em **Okey** tooexit Assistente de saudação.

## <a name="import-data-into-excel-from-hdinsight"></a>Importar dados do HDInsight para o Excel
Olá etapas a seguir descrevem Olá maneira tooimport dados de uma tabela de Hive em uma pasta de trabalho do Excel usando Olá fonte de dados ODBC que você criou na seção anterior hello.

1. Abra uma pasta de trabalho nova ou existente no Excel.
2. De saudação **dados** , clique em **obter dados**, clique em **de outras fontes**e, em seguida, clique em **do ODBC** toolaunch Olá  **Assistente de Conexão de dados**.
   
    ![Abrir assistente de conexão de dados](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Abrir assistente de conexão de dados")
4. Nome que você criou na seção última Olá de fonte de dados de Select hello e, em seguida, clique em **Okey**.
5. Insira o nome de usuário do Hadoop (nome da saudação padrão é admin) Olá senha e, em seguida, clique em **conectar**.
6. No Navegador, expanda **HIVE**, expanda **padrão**, clique em **hivesampletable** e clique em **Carregar**. Levará alguns segundos antes de dados obtém tooExcel importado.

    ![Navegador do ODBC Hive do HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Assistente para conexão de dados aberto")


## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse Olá dados do Hive do Microsoft ODBC driver tooretrieve de saudação HDInsight Service no Excel. Da mesma forma, você pode recuperar dados de saudação HDInsight Service no banco de dados SQL. Também é dados tooupload possíveis em um HDInsight Service. toolearn mais, consulte:

* [Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-data]
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Use o Sqoop com o HDInsight][hdinsight-use-sqoop]

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


