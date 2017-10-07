---
title: "Ação de Script de aaaUse tooinstall Solr no cluster de Hadoop - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight cluster com Solr usando a ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Instalar e usar o Solr em clusters HDInsight baseados no Windows

Saiba como toocustomize HDInsight baseados em Windows cluster com Solr usando a ação de Script e toouse Solr toosearch dados.

> [!IMPORTANT]
> Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows. O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obter informações sobre como usar o Solr com um cluster baseado no Linux, consulte [Instalar e usar o Solr em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md).


Você pode instalar o Solr em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*. Tooinstall um script de exemplo Solr em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

script de exemplo Hello funciona apenas com a versão 3.1 do cluster HDInsight. Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).

script de exemplo Hello usado neste tópico cria um cluster de Solr baseados no Windows com uma configuração específica. Se desejar que o cluster de Solr tooconfigure Olá com diferentes coleções, fragmentos, esquemas, réplicas, etc., você deve modificar Solr binários e script hello adequadamente.

**Artigos relacionados**

* [Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-solr"></a>O que é Solr?
O <a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados. Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr fornece recursos de pesquisa de saudação tooquickly recupera dados de saudação.

## <a name="install-solr-using-portal"></a>Instalar o Solr usando o Portal
1. Começar a criar um cluster usando Olá **criação personalizada** opção, conforme descrito em [Hadoop criar clusters de HDInsight](hdinsight-provision-clusters.md).
2. Em Olá **ações de Script** página do Assistente de saudação, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:

    ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de ação de Script de Use um cluster")

    <table border='1'>
        <tr><th>Propriedade</th><th>Valor</th></tr>
        <tr><td>Nome</td>
            <td>Especifique um nome para a ação de script hello. Por exemplo, <b>Instalar o Solr</b>.</td></tr>
        <tr><td>URI do script</td>
            <td>Especifique o script hello de toohello de identificador de recurso uniforme (URI) que é invocado toocustomize Olá cluster. Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo de nó</td>
            <td>Especifica Olá nós em que o script de personalização de saudação é executado. Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.
        <tr><td>parâmetros</td>
            <td>Especifica parâmetros de hello, se exigido pelo script hello. Olá script tooinstall Solr não requer nenhum parâmetro, você poderá deixar isso em branco.</td></tr>
    </table>

    Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello. Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.

## <a name="use-solr"></a>Usar o Solr
Você deve começar com indexação Solr, com alguns arquivos de dados. Você pode usar consultas de pesquisa do Solr toorun nos dados hello indexado. Execute Olá etapas toouse Solr em um cluster do HDInsight a seguir:

1. **Usar protocolo de área de trabalho remota (RDP) tooremote em cluster do HDInsight Olá com Solr instalado**. De Olá portal do Azure, habilite área de trabalho remota para cluster Olá criado com o cluster de saudação instalado e, em seguida, remoto em Solr. Para obter instruções, consulte [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Indexar o Solr carregando arquivos de dados**. Quando você indexar Solr, você colocar os documentos que talvez seja necessário toosearch em. tooindex Solr, use tooremote RDP em cluster Olá, navegue toohello área de trabalho, abra a linha de comando do Hadoop hello e navegar muito**C:\apps\dist\solr-4.7.2\example\exampledocs**. Execute Olá comando a seguir:

        java -jar post.jar solr.xml monitor.xml

    Você verá Olá saída a seguir no console de saudação:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Utilitário de post.jar Olá índices Solr com dois documentos de exemplo, **solr.xml** e **monitor.xml**. Utilitário de post.jar Hello e documentos de exemplo hello estão disponíveis com a instalação do Solr.
3. **Use Olá Solr painel toosearch em hello indexado documentos**. Em Olá RDP sessão toohello HDInsight cluster, abra o Internet Explorer e iniciar Olá Solr painel em **solr/http://headnodehost:8983 / #/**. No painel esquerdo hello, de saudação **Core seletor** lista suspensa, selecione **collection1**e dentro dele, clique em **consulta**. Como um exemplo, tooselect e retornar todos os documentos de saudação em Solr, fornecer Olá valores a seguir:

   * Em Olá **p** texto, digite  **\*:**\*. Isso retornará todos os documentos de saudação que são indexados Solr. Se você quiser toosearch para uma cadeia de caracteres específica dentro de documentos hello, você pode inserir essa cadeia de caracteres aqui.
   * Em Olá **wt** caixa de texto, selecione Olá formato de saída. O padrão é **json**. Clique em **Executar consulta**.

     ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "executar uma consulta no painel Solr")

     saída de Hello retorna Olá dois documentos que foram usados para indexação Solr. saída de Hello é semelhante a seguinte hello:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Recomendado: Backup hello indexado dados de Solr tooAzure armazenamento Blob associado do cluster do HDInsight Olá**. Como uma prática recomendada, você deve fazer backup de dados indexado de saudação de nós de cluster Solr Olá para o armazenamento de BLOBs do Azure. Execute Olá toodo as etapas a seguir para:

   1. Da sessão RDP hello, abra o Internet Explorer e toohello de ponto de URL a seguir:

           http://localhost:8983/solr/replication?command=backup

       Você verá uma resposta semelhante a essa:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. Na sessão remota do hello, navegue muito {SOLR_HOME}\{coleção} \data. Para o cluster Olá criado por meio do script de exemplo hello, esta deve ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. Nesse local, você deve ver uma pasta de instantâneo criada com um nome semelhante muito**instantâneo.* carimbo de hora** *.
   3. Compacte a pasta de instantâneo hello e carregá-lo tooAzure o armazenamento de Blob. Na linha de comando do Hadoop hello, navegar toohello local da pasta de instantâneo hello usando Olá comando a seguir:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       Este comando cópias Olá instantâneo muito / / dados de exemplo/no contêiner Olá no padrão de saudação armazenamento conta associada Olá cluster.

## <a name="install-solr-using-aure-powershell"></a>Instalar o Solr usando o Azure PowerShell
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Instalar o Solr usando o SDK do .NET
Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK. Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Consulte também
* [Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight
* [Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.
* [Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)
* [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.
* [Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.
* [Instalar Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
