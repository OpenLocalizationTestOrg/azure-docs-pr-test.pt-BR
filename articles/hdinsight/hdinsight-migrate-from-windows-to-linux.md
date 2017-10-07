---
title: aaaMigrate do HDInsight baseados em Windows com base em tooLinux HDInsight - Azure | Microsoft Docs
description: Saiba como toomigrate de um HDInsight baseados em Windows cluster tooa cluster de HDInsight baseados em Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Migrar de um cluster HDInsight baseados em Windows cluster tooa baseados em Linux

Este documento fornece detalhes sobre as diferenças de saudação entre HDInsight no Windows e Linux e orientação sobre como cluster de baseados em Linux do toomigrate existente cargas de trabalho tooa.

Enquanto HDInsight baseados em Windows fornece um toouse de maneira fácil Hadoop na nuvem hello, talvez seja necessário toomigrate tooa baseados em Linux cluster. Por exemplo, tootake proveito das ferramentas baseadas em Linux e tecnologias que são necessárias para sua solução. Muitas coisas no ecossistema do Hadoop Olá são desenvolvidas em sistemas baseados em Linux e podem não estar disponíveis para uso com o HDInsight baseados no Windows. Além disso, muitos livros, vídeos e outros materiais de treinamento supõem que você esteja usando um sistema Linux quando trabalha com o Hadoop.

> [!NOTE]
> Clusters HDInsight usam suporte de longo prazo Ubuntu (LTS) como sistema operacional de saudação para nós de saudação em cluster hello. Para obter informações sobre a versão de saudação do Ubuntu disponível com o HDInsight, juntamente com outras informações de controle de versão do componente, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Tarefas de migração

fluxo de trabalho geral para a migração Olá é da seguinte maneira.

![Diagrama do fluxo de trabalho da migração](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Leia cada seção deste documento toounderstand alterações que podem ser necessárias ao migrar seu fluxo de trabalho existente, trabalhos, cluster baseado em Linux de tooa etc.

2. Crie um cluster baseado em Linux como um ambiente de teste/controle de qualidade. Para saber mais sobre como criar um cluster baseado em Linux, confira [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Cópia existente de trabalhos, fontes de dados e coletores toohello novo ambiente.

4. Execute testes toomake se os trabalhos funcionam conforme esperado no cluster novo Olá de validação.

Depois de ter verificado que tudo está funcionando conforme o esperado, agende o tempo de inatividade para migração de saudação. Durante esse tempo de inatividade, execute Olá ações a seguir:

1. Fazer backup dos dados transitórios armazenados localmente em nós de cluster de saudação. Por exemplo, se você tiver dados armazenados diretamente em um nó principal.

2. Exclua Olá baseados em Windows cluster.

3. Crie um cluster baseado em Linux usando Olá mesmo padrão que o repositório de dados que Olá cluster baseado em Windows usado. cluster de saudação do Linux pode continuar trabalhando em relação aos dados de produção existente.

4. Importe o backup de todos os dados transitórios.

5. Iniciar trabalhos/continuar o processamento usando o novo cluster de saudação.

### <a name="copy-data-toohello-test-environment"></a>Ambiente de teste de toohello de dados de cópia

Há muitos métodos toocopy Olá dados e, porém Olá dois discutidas nesta seção são hello mais simples métodos toodirectly move arquivos tooa cluster de teste.

#### <a name="hdfs-copy"></a>Cópia do HDFS

Dados toocopy as etapas a seguir de saudação do uso de cluster de teste toohello do cluster de produção de hello. Essas etapas usam Olá `hdfs dfs` utilitário que está incluído no HDInsight.

1. Localize Olá armazenamento padrão contêiner informações de conta e o cluster existente. saudação de exemplo a seguir usa tooretrieve PowerShell essas informações:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate um ambiente de teste, siga as etapas de saudação em clusters baseados em Linux criar de saudação no documento de HDInsight. Parar antes de criar o cluster hello e, em vez disso, selecione **configuração opcional**.

3. Na folha de configuração opcional hello, selecione **contas de armazenamento vinculadas**.

4. Selecione **adicionar uma chave de armazenamento**e quando solicitado, selecione a conta de armazenamento de saudação que foi retornada pelo Olá script do PowerShell na etapa 1. Clique em **Selecionar** em cada folha. Finalmente, crie o cluster hello.

5. Depois que o cluster Olá tiver sido criado, se conectar usando tooit **SSH.** Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

6. Da sessão SSH hello, use Olá seguir arquivos do comando toocopy de saudação vinculada armazenamento conta toohello nova conta de armazenamento padrão. Substitua o CONTÊINER com informações de contêiner hello retornadas pelo PowerShell. Substituir __conta__ com o nome da conta de saudação. Substitua saudação caminho toodata com arquivo de dados do hello caminho tooa.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Se a estrutura de diretórios de saudação que contém dados de saudação não existe no ambiente de teste hello, você pode criar usando Olá comando a seguir:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Olá `-p` switch permite a criação de saudação de todos os diretórios no caminho de saudação.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Cópia direta entre blobs do Armazenamento do Azure

Como alternativa, convém Olá toouse `Start-AzureStorageBlobCopy` Azure PowerShell cmdlet toocopy blobs entre contas de armazenamento fora do HDInsight. Para obter mais informações, consulte como Olá toomanage seção Blobs do Azure usando o PowerShell do Azure com o armazenamento do Azure.

## <a name="client-side-technologies"></a>Tecnologias do lado do cliente

Tecnologias do lado do cliente, como [cmdlets do PowerShell do Azure](/powershell/azureps-cmdlets-docs), [CLI do Azure](../cli-install-nodejs.md), ou hello [SDK .NET para Hadoop](https://hadoopsdk.codeplex.com/) continuar toowork baseados em Linux clusters. Essas tecnologias dependem REST APIs que são Olá mesmo em ambos os tipos de sistema operacional do cluster.

## <a name="server-side-technologies"></a>Tecnologias do lado do servidor

Olá, a tabela a seguir fornece orientação sobre migração componentes do lado do servidor que são específicos do Windows.

| Se estiver usando esta tecnologia... | Execute esta ação... |
| --- | --- |
| **PowerShell** (scripts do lado do servidor, incluindo as Ações de Script usadas durante a criação do cluster) |Reescreva-os como scripts Bash. Para as Ações de Script, confira [Personalizar clusters HDInsight baseados em Linux usando as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md) e [Desenvolvimento de ação de script com o HDInsight](hdinsight-hadoop-script-actions-linux.md). |
| **CLI do Azure** (scripts de servidor) |Enquanto Olá CLI do Azure está disponível no Linux, ela não vêm pré-instalados em nós do principal de cluster do HDInsight hello. Para obter mais informações sobre como instalar Olá CLI do Azure, consulte [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Componentes do .NET** |O .NET tem suporte no HDInsight do Linux por meio do [Mono](https://mono-project.com). Para obter mais informações, consulte [soluções .NET migrar com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Componentes do Win32 ou de outra tecnologia exclusiva do Windows** |Depende do componente de saudação ou tecnologia. Pode ser capaz de toofind uma versão compatível com Linux, ou pode precisar toofind uma solução alternativa ou reescrever esse componente. |

> [!IMPORTANT]
> gerenciamento de HDInsight Olá SDK não é totalmente compatível com Mono. Ele não deve ser usado como parte das soluções implantadas toohello HDInsight cluster no momento.

## <a name="cluster-creation"></a>Criação do cluster

Esta seção fornece informações sobre as diferenças na criação do cluster.

### <a name="ssh-user"></a>Usuário do SSH

Clusters de HDInsight baseados em Linux usam Olá **Secure Shell (SSH)** tooprovide nós de cluster de toohello de acesso remoto de protocolo. Ao contrário dos clusters baseados em Área de Trabalho Remota para Windows, a maioria dos clientes SSH não fornecem uma experiência gráfica ao usuário. Em vez disso, os clientes SSH fornecem uma linha de comando que permite que você toorun comandos de cluster hello. Alguns clientes (como [MobaXterm](http://mobaxterm.mobatek.net/)) fornecem um navegador de sistema de arquivos gráficos na linha de comando remoto adição tooa.

Durante a criação do cluster, você deve fornecer um usuário SSH e uma **senha** ou um **certificado de chave pública** para autenticação.

É recomendável usar um certificado de chave pública, pois é mais seguro do que usar uma senha. Autenticação de certificado funciona, gerando um par de chaves pública/privada assinado e fornecendo a chave pública Olá durante a criação de cluster hello. Ao conectar o servidor toohello usando SSH, a chave privada Olá no cliente Olá fornece autenticação para conexão hello.

Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Personalização do cluster

**Ações de Script** usadas com clusters baseados em Linux devem ser escritas no script Bash. Enquanto as ações de Script pode ser usadas durante a criação de cluster, para clusters baseados em Linux, eles também podem ser usados tooperform personalização após um cluster e está em execução. Para obter mais informações, confira [Personalizar clusters HDInsight baseados em Linux usando as Ação de Script](hdinsight-hadoop-customize-cluster-linux.md) e [Desenvolvimento de ação de script com o HDInsight](hdinsight-hadoop-script-actions-linux.md).

Outro recurso de personalização é a **inicialização**. Para clusters do Windows, esse recurso permite que você toospecify Olá local das bibliotecas adicionais para uso com o Hive. Após a criação do cluster, essas bibliotecas ficam automaticamente disponíveis para uso com consultas de Hive sem Olá necessidade toouse `ADD JAR`.

recurso de inicialização Olá para clusters baseados em Linux não fornece essa funcionalidade. Em vez disso, use a ação de script documentada em [Adicionar bibliotecas do Hive durante a criação do cluster](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Redes Virtuais

Os clusters HDInsight baseados em Windows funcionam apenas com Rede Virtuais Clássicas, enquanto os clusters HDInsight baseados em Linux exigem Redes Virtuais do Resource Manager. Se você tiver recursos uma rede Virtual clássica Olá cluster HDInsight Linux deve se conectar ao, consulte [conexão tooa uma rede Virtual clássica Gerenciador de recursos de redes virtuais](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Para saber mais sobre os requisitos de configuração para usar as Redes Virtuais do Azure com o HDInsight, confira [Extend HDInsight capabilities by using a Virtual Network](hdinsight-extend-hadoop-virtual-network.md)(Estender os recursos do HDInsight usando uma Rede Virtual).

## <a name="management-and-monitoring"></a>Gerenciamento e monitoramento

Muitas das Olá web interfaces de usuário que você pode ter usado com HDInsight baseados no Windows, como o histórico de trabalho ou Yarn da interface do usuário, estão disponíveis por meio do Ambari. Além disso, Olá Ambari Hive exibição fornece uma maneira toorun consultas do Hive usando seu navegador da web. Saudação da interface do usuário do Ambari Web está disponível em clusters baseados em Linux em https://CLUSTERNAME.azurehdinsight.net.

Para obter mais informações sobre como trabalhar com Ambari, consulte Olá documentos a seguir:

* [Ambari Web](hdinsight-hadoop-manage-ambari.md)
* [API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Alertas do Ambari

Ambari tem um sistema de alerta que pode informar você sobre possíveis problemas com o cluster de saudação. Alertas são exibidos como vermelhas ou amarelas entradas no hello Ambari Web da interface do usuário, no entanto, você também pode recuperá-las por meio da API REST de saudação.

> [!IMPORTANT]
> Os alertas do Ambari indicam que *pode* haver um problema, e não que *há* um problema. Por exemplo, você pode receber um alerta de que HiveServer2 não pode ser acessado, mesmo que consiga acessá-lo normalmente.
>
> Vários alertas são implementados como consultas baseadas em intervalo em um serviço e esperam uma resposta por um período específico. Para que o alerta de saudação não significa necessariamente que Olá serviço está inativo, apenas se ele não retornou resultados em intervalo de tempo de saudação esperado.

Antes de tomar alguma medida, você deve avaliar se um alerta vem ocorrendo por um longo período ou se representa problemas do usuário que foram relatados.

## <a name="file-system-locations"></a>Locais do sistema de arquivos

saudação de sistema de arquivos do cluster Linux é disposta Diferentemente de clusters HDInsight baseados no Windows. Use Olá toofind usado arquivos de dados da tabela a seguir.

| Preciso de toofind... | Está localizado em... |
| --- | --- |
| Configuração |`/etc`. Por exemplo, `/etc/hadoop/conf/core-site.xml` |
| Arquivos de log |`/var/logs` |
| HDP (Hortonworks Data Platform) |`/usr/hdp`. Há dois diretórios localizado aqui, um que seja a versão atual de HDP Olá e `current`. Olá `current` diretório contém links simbólicos toofiles e pastas localizadas no diretório de número de versão de saudação. Olá `current` diretório é fornecido como uma maneira conveniente de acessar arquivos HDP desde Olá número de versão muda conforme Olá HDP versão é atualizada. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

Em geral, se você souber o nome de saudação do arquivo hello, você pode usar o hello comando a seguir de um caminho de arquivo do SSH sessão toofind hello:

    find / -name FILENAME 2>/dev/null

Você também pode usar caracteres curinga com o nome de arquivo hello. Por exemplo, `find / -name *streaming*.jar 2>/dev/null` retorna Olá caminho tooany arquivos jar que contêm a palavra hello streaming como parte do nome de arquivo hello.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig e MapReduce

Cargas de trabalho do Pig e do MapReduce são muito semelhantes em clusters baseados em Linux. No entanto, os clusters HDInsight baseados em Linux podem ser criados usando versões mais recentes do Hadoop, Hive e Pig. Essas diferenças de versão podem introduzir alterações no funcionamento das suas soluções existentes. Para obter mais informações sobre versões de saudação de componentes incluídos no HDInsight, consulte [o controle de versão do HDInsight componente](hdinsight-component-versioning.md).

O HDInsight baseado em Linux não oferece a funcionalidade de área de trabalho remota. Em vez disso, você pode usar SSH tooremotely conectar toohello nós de cabeçalho do cluster. Para obter mais informações, consulte Olá documentos a seguir:

* [Usar Hive com SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Usar o Pig com o SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Usar o MapReduce com o SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Se você usar um metastore Hive externo, você deve fazer backup Olá metastore antes de usá-lo com HDInsight baseados em Linux. O HDInsight baseado em Linux está disponível com versões mais recentes do Hive, o que pode trazer incompatibilidades com metastores criados por versões anteriores.

Olá gráfico a seguir fornece orientação sobre como migrar suas cargas de trabalho de Hive.

| Com base no Windows, uso... | Com base no Linux... |
| --- | --- |
| **Editor de Hive** |[Modo de Exibição do Hive no Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez é o mecanismo de execução padrão Olá para clusters baseados em Linux, para a instrução set de saudação não for mais necessário. |
| Funções C# definidas pelo usuário | Para obter informações sobre a validação dos componentes c# com HDInsight baseados em Linux, consulte [soluções .NET migrar com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Arquivos CMD ou scripts no servidor de saudação chamado como parte de um trabalho de Hive |Scripts Bash |
| `hive` na Área de Trabalho Remota |O [Beeline](hdinsight-hadoop-use-hive-beeline.md) ou o [Hive em uma sessão do SSH](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Com base no Windows, uso... | Com base no Linux... |
| --- | --- |
| Funções C# definidas pelo usuário | Para obter informações sobre a validação dos componentes c# com HDInsight baseados em Linux, consulte [soluções .NET migrar com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Arquivos CMD ou scripts no servidor de saudação chamado como parte de um trabalho de Pig |Scripts Bash |

### <a name="mapreduce"></a>MapReduce

| Com base no Windows, uso... | Com base no Linux... |
| --- | --- |
| Componentes mapeador e redutor de C# | Para obter informações sobre a validação dos componentes c# com HDInsight baseados em Linux, consulte [soluções .NET migrar com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Arquivos CMD ou scripts no servidor de saudação chamado como parte de um trabalho de Hive |Scripts Bash |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Se você usar um Oozie metastore externo, você deve fazer backup Olá metastore antes de usá-lo com HDInsight baseados em Linux. O HDInsight baseado em Linux está disponível com versões mais recentes do Oozie, o que pode trazer incompatibilidades com metastores criados por versões anteriores.

Fluxos de trabalho do Oozie permitem realizar ações de shell. Ações de shell usam shell padrão de saudação para comandos de linha de comando do toorun Olá sistema operacional. Se você tiver Oozie fluxos de trabalho que dependem de saudação do shell do Windows, você deve reescrever Olá toorely de fluxos de trabalho no ambiente de shell do Linux hello (Bash). Para obter mais informações sobre como usar ações de shell com Oozie, consulte [Extensão da ação de shell do Oozie](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).

Se você tiver fluxos de trabalho do Oozie que dependem de aplicativos C# invocados por meio de ações do shell, valide esses aplicativos em um ambiente Linux. Para obter mais informações, consulte [soluções .NET migrar com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Com base no Windows, uso... | Com base no Linux... |
| --- | --- |
| Painel Storm |Olá profusão de painel não está disponível. Consulte [topologias de implantar e gerenciar Storm no HDInsight baseados em Linux](hdinsight-storm-deploy-monitor-topology-linux.md) para topologias de toosubmit maneiras |
| Interface do Usuário do Storm |Olá profusão de interface do usuário está disponível em https://CLUSTERNAME.azurehdinsight.net/stormui |
| Toocreate do Visual Studio, implantar e gerenciar o c# ou híbrido topologias |O Visual Studio pode ser usado toocreate, implantar e gerenciar c# (SCP.NET) ou topologias híbridas no Storm baseados em Linux em clusters de HDInsight criado após 10/28/2016. |

## <a name="hbase"></a>HBase

Em clusters baseados em Linux, é pai do hello znode HBase `/hbase-unsecure`. Defina esse valor na configuração de saudação para qualquer aplicativo de cliente de Java que usam a API do Java HBase nativo.

Confira [Build a Java-based HBase application](hdinsight-hbase-build-java-maven.md) (Criar aplicativo HBase baseado em Java) para obter um exemplo de cliente que defina esse valor.

## <a name="spark"></a>Spark

Os clusters Spark estavam disponíveis em clusters do Windows durante a visualização. O Spark GA só está disponível em clusters baseados em Linux. Não há nenhum caminho de migração de um cluster Spark baseados em Windows visualização cluster tooa versão Spark baseados em Linux.

## <a name="known-issues"></a>Problemas conhecidos

### <a name="azure-data-factory-custom-net-activities"></a>Atividades personalizadas do .NET no Azure Data Factory

Atualmente, atividades personalizadas do .NET no Azure Data Factory não são compatíveis com clusters HDInsight baseados em Linux. Em vez disso, você deve usar uma saudação atividades personalizadas de tooimplement métodos a seguir como parte do pipeline ADF.

* Execute atividades do .NET no pool do Lote do Azure. Consulte a seção de serviço vinculado do uso do Azure Batch saudação de [usar atividades personalizadas em um pipeline da fábrica de dados do Azure](../data-factory/data-factory-use-custom-activities.md)
* Implementar a atividade de saudação como uma atividade MapReduce. Para obter mais informações, consulte [Invocar programas do MapReduce por meio do Data Factory](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Terminações de linha

No geral, as terminações de linha em sistemas baseados no Windows usam CRLF, enquanto os sistemas baseados no Linux usam LF. Se você gera ou espera, dados com terminações de linha CRLF, talvez seja necessário toowork de produtores ou os consumidores de saudação de toomodify com terminação de linha hello LF.

Por exemplo, o HDInsight em um cluster baseado no Windows usando o Azure PowerShell tooquery retorna dados com CRLF. Olá, mesma consulta com um cluster baseado em Linux retorna LF. Você deve testar toosee se terminação de linha hello faz com que um problema com sua solutuion antes de migrar tooa baseados em Linux cluster.

Se você tiver scripts que são executados diretamente em nós do cluster Linux hello, você sempre deve usar LF como final de linha de saudação. Se você usar CRLF, você pode ver erros ao executar scripts de saudação em um cluster baseado em Linux.

Se você souber que os scripts de saudação não contêm cadeias de caracteres com caracteres CR inseridos, você pode em massa terminações de linha de saudação de alteração usando um dos métodos a seguir de saudação:

* **Antes de carregar o cluster toohello**: Olá Use seguir terminações de linha de saudação do PowerShell instruções toochange de tooLF CRLF antes de carregar o cluster de toohello script hello.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Depois de carregar o cluster toohello**: comando a seguir de saudação uso de uma sessão SSH toohello script de saudação toomodify cluster baseado em Linux.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Próximas etapas

* [Saiba como toocreate HDInsight baseados em Linux clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Usar SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Gerenciar um cluster baseado em Linux usando o Ambari](hdinsight-hadoop-manage-ambari.md)
