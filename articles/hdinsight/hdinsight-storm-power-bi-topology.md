---
title: aaaUse Apache Storm com o Power BI - HDInsight do Azure | Microsoft Docs
description: "Crie um relatório do Power BI usando dados de uma topologia C# em execução em um cluster do Apache Storm no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Usar dados do Power BI toovisualize de uma topologia do Apache Storm

Power BI permite toovisually exibir dados de relatórios. Este documento fornece um exemplo de como toouse Apache Storm em HDInsight toogenerate dados para o Power BI.

> [!NOTE]
> Olá etapas neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio. projeto compilado Olá pode ser enviado tooa cluster de HDInsight baseados em Linux. Somente os clusters baseados em Linux criados depois de 28/10/2016 são compatíveis com as topologias do SCP.NET.
>
> toouse uma topologia c# com um cluster baseado em Linux, saudação de atualização de pacote do Microsoft.SCP.Net.SDK NuGet usado pelo seu projeto tooversion 0.10.0.6 ou superior. versão de saudação do pacote de saudação também deve corresponder a versão principal de saudação do Storm instalado no HDInsight. Por exemplo, o HDInsight versões 3.3 e 3.4 usam o Storm versão 0.10.x, enquanto o HDInsight 3.5 usa o Storm 1.0. x.
>
> C# topologias em clusters baseados em Linux devem usar o .NET 4.5 e use toorun Mono no cluster do HDInsight hello. A maioria das coisas funciona. No entanto, você deve verificar Olá [Mono compatibilidade](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades.
>
> Para obter uma versão Java deste projeto, que funciona com HDInsight baseado em Windows ou Linux, confira [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Pré-requisitos

* Um usuário do Azure Active Directory com acesso ao [Power BI](https://powerbi.com).
* Um cluster HDInsight. Para obter mais informações, confira [Introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* O Visual Studio (um dos Olá versões a seguir)

  * Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (qualquer edição)

* Olá ferramentas HDInsight para Visual Studio: consulte [começar a usar as ferramentas do HDInsight Olá para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre informações de instalação.

## <a name="how-it-works"></a>Como ele funciona

Este exemplo contém uma topologia do Storm em C# que gera aleatoriamente dados de log do IIS (Serviços de Informações da Internet). Esses dados são gravados tooa banco de dados SQL e de lá é usado toogenerate relatórios no Power BI.

Olá arquivos implementam Olá funcionalidade principal deste exemplo a seguir:

* **SqlAzureBolt.cs**: grava informações produzidas no hello Storm topologia tooSQL banco de dados.
* **IISLogsTable.sql**: Olá Transact-SQL instruções usadas toogenerate Olá banco de dados que Olá dados são armazenados em.

> [!WARNING]
> Crie tabela de saudação no banco de dados SQL antes de iniciar a topologia de saudação no seu cluster HDInsight.

## <a name="download-hello-example"></a>Baixe o exemplo hello

Baixar Olá [exemplo HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, uma bifurcação/clone-o usando [git](http://git-scm.com/), ou use Olá **baixar** toodownload de link do arquivo hello. zip.

## <a name="create-a-database"></a>Criar um banco de dados

1. toocreate um banco de dados, use as etapas de Olá Olá [tutorial do banco de dados SQL](../sql-database/sql-database-get-started.md) documento.

2. Conectar o banco de dados de toohello por Olá seguir as etapas em Olá [conectar tooa banco de dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md) documento.

3. No Pesquisador de objetos, clique em banco de dados de saudação e selecione **nova consulta**. Cole o conteúdo Olá Olá **IISLogsTable.sql** arquivo incluído no hello baixou o projeto na janela de consulta hello e, em seguida, use Ctrl + Shift + a consulta de saudação tooexecute E. Você deve receber uma mensagem que Olá comandos foi concluídos com êxito.

## <a name="configure-hello-sample"></a>Configurar o exemplo hello

1. De saudação [portal do Azure](https://portal.azure.com), selecione o banco de dados SQL. De saudação **Essentials** seção da folha de banco de dados SQL hello, selecione **Mostrar cadeias de conexão de banco de dados**. Na lista de saudação que aparece, copie Olá **ADO.NET (autenticação do SQL)** informações.

2. Abra o exemplo hello no Visual Studio. De **Solution Explorer**, abra Olá **App. config** de arquivo e depois descobrir Olá a seguinte entrada:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Substituir saudação **TOBEFILLED # # # #** valor com a cadeia de conexão de banco de dados de saudação copiado na etapa anterior hello. Substituir **{sua\_nome de usuário}** e **{sua\_senha}** com hello nome de usuário e senha para o banco de dados de saudação.

3. Salvar e fechar arquivos hello.

## <a name="deploy-hello-sample"></a>Implantar o exemplo hello

1. De **Solution Explorer**, Olá atalho **StormToSQL** do projeto e selecione **enviar tooStorm no HDInsight**. Cluster do HDInsight Olá Select de saudação **Cluster Storm** caixa de diálogo de lista suspensa.

   > [!NOTE]
   > Pode levar alguns segundos para Olá **Cluster Storm** toopopulate suspensa com nomes de servidor.
   >
   > Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure. Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.

2. Quando a topologia de saudação tiver sido enviada, Olá __Visualizador de topologia__ é exibida. tooview essa topologia, a entrada de SqlAzureWriterTopology Olá selecione da lista de saudação.

    ![topologias de Hello, com a topologia de saudação selecionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Você pode usar essas informações de toosee de exibição na topologia hello, ou clique duas vezes um componente de tooa específico entrada (como Olá SqlAzureBolt) toosee informações na topologia de saudação.

3. Após a saudação topologia tem executado por alguns minutos, janela de consulta SQL toohello retorno usado o banco de dados do toocreate hello. Substitua instruções existentes Olá Olá consulta a seguir:

        select * from iislogs;

    Use Ctrl + Shift + E tooexecute Olá de consulta e você deve receber resultados toohello semelhante seguintes dados:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Esses dados foi escritos da topologia de profusão de saudação.

## <a name="create-a-report"></a>Criar um relatório

1. Conecte-se toohello [conector do Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI. 

2. Dentro de **Bancos de Dados**, selecione **Obter**.

3. Selecione **Banco de Dados SQL do Azure** e **Conectar**.

    > [!NOTE]
    > Talvez você seja solicitado toodownload Olá Power BI Desktop toocontinue. Nesse caso, use Olá tooconnect as etapas a seguir:
    >
    > 1. Abra o Power BI Desktop e selecione __Obter dados__.
    > 2 Selecione __Azure__ e, em seguida, __banco de dados SQL do Azure__.

4. Digite hello informações tooconnect tooyour banco de dados do SQL Azure. Você pode encontrar essas informações visitando Olá [portal do Azure](https://portal.azure.com) e selecionando o banco de dados SQL.

   > [!NOTE]
   > Você também pode definir o intervalo de atualização de saudação e filtros personalizados usando **habilitar opções avançadas** de saudação caixa de diálogo de conexão.

5. Depois de conectado, você verá um novo conjunto de dados com hello que mesmo nome como o banco de dados de saudação você se conectou. Selecione Olá toobegin de conjunto de dados criando um relatório.

6. De **campos**, expanda Olá **IISLOGS** entrada. toocreate origina-se um relatório que lista Olá URI, marque a caixa de seleção de saudação para **URISTEM**.

    ![Criando um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Em seguida, arraste **método** toohello relatório. Olá Olá de toolist de atualizações de relatório originário e método HTTP correspondente Olá usado para Olá solicitação HTTP.

    ![Adicionando dados de método hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. De saudação **visualizações** coluna, selecione Olá **campos** ícone e, em seguida, selecione Olá a seta para baixo próxima muito**método** em Olá **valores**seção. toodisplay uma contagem de quantas vezes um URI foi acessada, selecione **contagem**.

    ![Alterar tooa contagem dos métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. Em seguida, selecione Olá **gráfico de colunas empilhadas** toochange como Olá informações são exibidas.

    ![Gráfico de empilhado tooa alteração](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. relatório de saudação toosave, selecione **salvar** e digite um nome para o relatório de saudação.

## <a name="stop-hello-topology"></a>Parar a topologia de saudação

topologia Olá continua toorun até você interrompê-lo ou excluir Olá Storm no cluster HDInsight. toostop Olá topologia, execute Olá etapas a seguir:

1. No Visual Studio, retorne toohello Visualizador de topologia e selecione a topologia de saudação.

2. Selecione Olá **Kill** topologia de saudação do botão toostop.

    ![Kill botão na topologia de saudação resumida](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu como toosend dados de uma topologia de Storm tooSQL banco de dados, em seguida, visualizar dados hello usando o Power BI. Para obter informações sobre como toowork com outras tecnologias do Azure usando Storm no HDInsight, consulte Olá documento a seguir:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
