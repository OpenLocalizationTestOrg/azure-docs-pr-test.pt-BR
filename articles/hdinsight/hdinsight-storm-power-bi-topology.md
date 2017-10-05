---
title: "Usar Apache Storm com Power BI – HDInsight do Azure | Microsoft Docs"
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a>Usar o Power BI para visualizar dados de uma topologia do Apache Storm

O Power BI permite a exibição visual dos dados como relatórios. Este documento fornece um exemplo de como usar o Apache Storm no HDInsight para gerar dados para o Power BI.

> [!NOTE]
> As etapas neste documento dependem de um ambiente de desenvolvimento do Windows com Visual Studio. O projeto compilado pode ser enviado para um cluster do HDInsight baseados em Linux. Somente os clusters baseados em Linux criados depois de 28/10/2016 são compatíveis com as topologias do SCP.NET.
>
> Para usar uma topologia do C# com um cluster baseado em Linux, atualize o pacote NuGet Microsoft.SCP.Net.SDK usado pelo seu projeto para a versão 0.10.0.6 ou superior. A versão do pacote também deve coincidir com a versão principal do Storm instalada no HDInsight. Por exemplo, o HDInsight versões 3.3 e 3.4 usam o Storm versão 0.10.x, enquanto o HDInsight 3.5 usa o Storm 1.0. x.
>
> As topologias C# em clusters baseados em Linux devem usar o .NET 4.5 e o Mono para execução no cluster HDInsight. A maioria das coisas funciona. No entanto, você deve verificar o documento [Compatibilidade do Mono](http://www.mono-project.com/docs/about-mono/compatibility/) em busca de possíveis incompatibilidades.
>
> Para obter uma versão Java deste projeto, que funciona com HDInsight baseado em Windows ou Linux, confira [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Pré-requisitos

* Um usuário do Azure Active Directory com acesso ao [Power BI](https://powerbi.com).
* Um cluster HDInsight. Para obter mais informações, confira [Introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (uma das seguintes versões a seguir)

  * Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (qualquer edição)

* Ferramentas do HDInsight para o Visual Studio: consulte [Comece a usar as Ferramentas do HDInsight para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre a instalação.

## <a name="how-it-works"></a>Como ele funciona

Este exemplo contém uma topologia do Storm em C# que gera aleatoriamente dados de log do IIS (Serviços de Informações da Internet). Esses dados são gravados em um Banco de Dados SQL e, por meio dele, são usados para gerar relatórios no Power BI.

Os arquivos a seguir implementam a funcionalidade principal desse exemplo:

* **SqlAzureBolt.cs**: grava informações produzidas na topologia do Storm no Banco de Dados SQL.
* **IISLogsTable.sql**: as instruções Transact-SQL usadas para gerar o banco de dados no qual os dados são armazenados.

> [!WARNING]
> Criar a tabela no Banco de Dados SQL antes de iniciar a topologia em seu cluster HDInsight.

## <a name="download-the-example"></a>Baixar o exemplo

Baixe o [exemplo do Power BI do Storm em C# do HDInsight](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). Para baixá-lo, use uma bifurcação/clone-o usando [git](http://git-scm.com/)ou use o link de **Download** link para baixar um .zip do arquivo.

## <a name="create-a-database"></a>Criar um banco de dados

1. Use as etapas no documento [Tutorial do Banco de Dados SQL](../sql-database/sql-database-get-started.md) para criar um novo banco de dados.

2. Conecte-se ao banco de dados seguindo as etapas no documento [Conectar-se ao Banco de Dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md).

3. No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados e selecione **Nova Consulta**. Cole o conteúdo do arquivo **IISLogsTable.sql** incluído no projeto baixado na janela de consulta e use Ctrl + Shift + E para executar a consulta. Você deve receber uma mensagem de que os comandos foram concluídos com êxito.

## <a name="configure-the-sample"></a>Configurar o exemplo

1. No [Portal do Azure](https://portal.azure.com), selecione seu Banco de Dados SQL. Na seção **Fundamentos** da folha Banco de Dados SQL, selecione **Mostrar cadeias de conexão de banco de dados**. Na lista exibida, copie as informações de **ADO.NET (autenticação do SQL)** .

2. Abra o exemplo no Visual Studio. No **Gerenciador de Soluções**, abra o arquivo **App.config** e localize a seguinte entrada:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Substitua o valor **##TOBEFILLED##** valor pela cadeia de conexão de banco de dados copiada na etapa anterior. Substitua **{your\_username}** e **{your\_password}** pelo nome de usuário e pela senha do banco de dados.

3. Salve e feche os arquivos.

## <a name="deploy-the-sample"></a>Implantar o exemplo

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **StormToSQL** e selecione **Enviar para o Storm no HDInsight**. Selecione o cluster HDInsight no menu suspenso **Cluster Storm** .

   > [!NOTE]
   > Pode levar alguns segundos para a lista suspensa **Cluster Storm** ser populada com os nomes de servidor.
   >
   > Se solicitado, insira as credenciais de logon para sua assinatura do Azure. Se você tiver mais de uma assinatura, faça o logon naquela que contém seu Storm no cluster HDInsight.

2. Depois que a topologia é enviada, o __Visualizador de Topologia__ é exibido. Para exibir essa topologia, selecione a entrada SqlAzureWriterTopology na lista.

    ![As topologias, com a topologia selecionada](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Você pode usar esta exibição para ver informações sobre a topologia ou clicar duas vezes em uma entrada (como SqlAzureBolt) para ver as informações específicas de um componente na topologia.

3. Depois que a topologia estiver executado por alguns minutos, volte para a janela de consulta do SQL usada para criar o banco de dados. Substitua as instruções existentes pela seguinte consulta:

        select * from iislogs;

    Use Ctrl + Shift + E para executar a consulta e deverá receber resultados semelhantes aos dados a seguir:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Esses dados foram gravados da topologia do Storm.

## <a name="create-a-report"></a>Criar um relatório

1. Conecte-se ao [conector do Banco de Dados SQL do Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI. 

2. Dentro de **Bancos de Dados**, selecione **Obter**.

3. Selecione **Banco de Dados SQL do Azure** e **Conectar**.

    > [!NOTE]
    > Você poderá ser solicitado a baixar o Power BI Desktop para continuar. Nesse caso, siga estas etapas para se conectar:
    >
    > 1. Abra o Power BI Desktop e selecione __Obter dados__.
    > 2 Selecione __Azure__ e, em seguida, __banco de dados SQL do Azure__.

4. Insira as informações para se conectar ao seu Banco de Dados SQL do Azure. Você pode encontrar essas informações visitando o [Portal do Azure](https://portal.azure.com) e selecionando o Banco de Dados SQL.

   > [!NOTE]
   > Você também pode definir o intervalo de atualização e filtros personalizados usando **Habilitar Opções Avançadas** na caixa de diálogo de conexão.

5. Depois de ter se conectado, você verá um novo conjunto de dados com o mesmo nome que o banco de dados ao qual está conectado. Selecione o conjunto de dados para começar a criar um relatório.

6. Em **Campos**, expanda a entrada **IISLOGS**. Para criar um relatório que liste as derivações do URI, marque a caixa de seleção para **URISTEM**.

    ![Criando um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Em seguida, arraste **METHOD** para o relatório. O relatório é atualizado para listar as derivações e o método HTTP correspondente usado para a solicitação HTTP.

    ![adicionando os dados de método](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Na coluna **Visualizações**, selecione o ícone **Campos** e selecione a seta para baixo ao lado de **METHOD** na seção **Valores**. Para exibir uma contagem de quantas vezes um URI pode ser acessado, selecione **Contagem**.

    ![Mudando para uma contagem de métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. Em seguida, selecione o **Gráfico de colunas empilhadas** para alterar como as informações são exibidas.

    ![Mudando para um gráfico empilhado](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. Para salvar o relatório, selecione **Salvar** e digite um nome para o relatório.

## <a name="stop-the-topology"></a>Parar a topologia

A topologia continuará sendo executada até você interrompê-la ou excluir o Storm no cluster HDInsight. Para interromper a topologia, execute as seguintes etapas:

1. No Visual Studio, volte ao visualizador de topologia e selecione a topologia.

2. Selecione o botão **Eliminar** para interromper a topologia.

    ![Botão Eliminar no resumo da topologia](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu como enviar dados de uma topologia do Storm para o Banco de Dados SQL e exibir os dados usando o Power BI. Para obter informações sobre como trabalhar com outras tecnologias do Azure usando o Storm no HDInsight, consulte o seguinte documento:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
