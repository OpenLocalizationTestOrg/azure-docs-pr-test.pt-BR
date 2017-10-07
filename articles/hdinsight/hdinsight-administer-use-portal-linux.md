---
title: clusters de aaaManage Hadoop no HDInsight usando o portal do Azure | Microsoft Docs
description: "Saiba como toocreate e gerencie clusters HDInsight usando Olá portal do Azure."
services: hdinsight
documentationcenter: 
author: mumian
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
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gerenciar clusters Hadoop em HDInsight usando Olá portal do Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Usando Olá [portal do Azure][azure-portal], você pode gerenciar clusters Hadoop em HDInsight do Azure. Use o seletor de tabulação Olá para obter informações sobre como gerenciar clusters Hadoop em HDInsight usando outras ferramentas.

**Pré-requisitos**

Antes de começar este artigo, você deve ter Olá itens a seguir:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Portal de saudação aberto
1. Entrar muito[https://portal.azure.com](https://portal.azure.com).
2. Depois de abrir o portal hello, você pode:

   * Clique em **novo** de saudação menu esquerdo toocreate um novo cluster:

       ![novo botão do cluster HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Clique em **Clusters HDInsight** de saudação toolist menu esquerdo Olá clusters existentes

       ![Botão do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Se você não vir o cluster HDInsight, clique em **mais serviços** Olá parte inferior da lista de saudação e, em seguida, clique em **clusters HDInsight** em Olá **Intelligence + análise** seção.


## <a name="create-clusters"></a>Criar clusters
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

O HDInsight trabalha com uma ampla variedade de componentes do Hadoop. Para Olá a lista de componentes de saudação que foram verificadas e suporte, consulte [é qual versão do Hadoop no HDInsight do Azure](hdinsight-component-versioning.md). Para obter informações de criação de cluster geral da saudação, consulte [Hadoop criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Requisitos de controle de acesso

Você deve especificar uma assinatura do Azure, quando você cria um cluster HDInsight. Este cluster pode ser criado em um novo grupo de recursos do Azure ou em um grupo de recursos existente. Você pode usar o hello tooverify as etapas a seguir suas permissões para criar clusters de HDInsight:

- toouse um grupo de recursos existente.

    1. Entrar toohello [portal do Azure](https://portal.azure.com).
    2. Clique em **grupos de recursos** Olá menu esquerdo toolist Olá dos grupos de recursos.
    3. Clique em grupo de recursos de saudação deseja toouse para criar seu cluster HDInsight.
    4. Clique em **(IAM) do controle de acesso**e verificar se você (ou um grupo que pertencem a) têm Olá pelo menos o grupo de recursos de toohello de acesso de Colaborador.

- toocreate um novo grupo de recursos

    1. Entrar toohello [portal do Azure](https://portal.azure.com).
    2. Clique em **assinatura** no menu esquerdo hello. Ele tem um ícone amarelo de chave. Você verá uma lista de assinaturas.
    3. Clique na assinatura de saudação que você use toocreate clusters. 
    4. Clique em **Minhas permissões**.  Ele mostra o [função](../active-directory/role-based-access-control-what-is.md#built-in-roles) assinatura hello. É necessário pelo menos cluster do HDInsight de toocreate de acesso de Colaborador.

Se você receber o erro de NoRegisteredProviderFound hello ou Olá MissingSubscriptionRegistration, consulte [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Listar e mostrar clusters
1. Entrar muito[https://portal.azure.com](https://portal.azure.com).
2. Clique em **Clusters HDInsight** de saudação toolist menu esquerdo Olá clusters existentes.
3. Clique no nome do cluster de saudação. Se a lista de clusters Olá for longa, você pode usar o filtro na parte superior de saudação da página de saudação.
4. Clique em um cluster de página de visão geral do hello lista toosee hello:

    ![Fundamentos do cluster HDInsight do portal do Azure](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Painel**: abre Olá painel do cluster, que é o Ambari Web para clusters baseados em Linux.
    * **Secure Shell**: cluster mostra Olá instruções tooconnect toohello usando conexão Secure Shell (SSH).
    * **Dimensionar o Cluster**: permite que você toochange número de saudação de nós de trabalho para este cluster.
    * **Excluir**: cluster de saudação de exclusões.
    * **Logs de Atividade**: mostrar e consultar logs de atividade.
    * **Controle de Acesso (IAM)**: usar atribuições de função.  Consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md).
    * **Marcas**: permite que você tooset chave/valor pares toodefine uma taxonomia personalizada dos serviços de nuvem. Por exemplo, você pode criar uma chave chamada **projeto**e usar um valor comum para todos os serviços associados a um projeto específico.
    * **Diagnosticar e resolver problemas**: exibir informações de solução de problemas.
    * **Bloqueia**: Adicionar bloqueio tooprevent Olá cluster que está sendo modificada ou excluída.
    * **Script de automação**: exibir e exportar modelo de Gerenciador de recursos do Azure Olá para cluster hello. No momento, você só pode exportar a conta de armazenamento do Azure dependentes hello. Consulte [Criar clusters Hadoop baseados em Linux no HDInsight usando modelos do Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Início Rápido**: exibe informações que o ajudamo a começar a usar o HDInsight.
    * **Ferramentas para HDInsight**: informações de ajuda para ferramentas relacionadas ao HDInsight.
    * **Logon de cluster**: exibir informações de logon de cluster hello.
    * **Assinatura de uso do núcleo**: exibição Olá núcleos usados e disponíveis para sua assinatura.
    * **Dimensionar o Cluster**: aumentar e diminuir Olá número de nós de trabalho do cluster. Consulte [Dimensionar clusters](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: cluster mostra Olá instruções tooconnect toohello usando conexão Secure Shell (SSH). Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Parceiro HDInsight**: Adicionar/remover Olá parceiro HDInsight atual.
    * **Os Metastores externos**: Exibir hello os metastores Hive e Oozie. Olá metastores só pode ser configurados durante o processo de criação de cluster hello. Consulte [usar metastore do Hive/Oozie](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Ações de script**: Bash executar scripts em cluster hello. Confira [Personalizar clusters HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).
    * **Aplicativos**: adicionar ou remover aplicativos do HDInsight.  Consulte [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md).
    * **Propriedades**: exibir as propriedades do cluster hello.
    * **Contas de armazenamento**: exibir contas de armazenamento hello e chaves de saudação. contas de armazenamento Olá são configuradas durante o processo de criação de cluster hello.
    * **Identidade do AAD do Cluster**:
    * **Nova solicitação de suporte**: permite que você toocreate um tíquete de suporte com o suporte da Microsoft.
    
6. Clique em **Propriedades**:

    Olá propriedades são:

   * **Nome do host**: nome do cluster.
   * **URL do Cluster**. Olá URL para a interface do hello Ambari web.
   * **Status**: incluindo Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Região**: local do Azure. Para obter uma lista dos locais do Azure com suporte, consulte Olá **região** caixa de listagem suspensa em [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Data de criação**.
   * **Sistema operacional**: **Windows** ou **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versão**. Consulte [versões do HDInsight](hdinsight-component-versioning.md)
   * **Assinatura**: nome da assinatura.
   * **Fonte de dados padrão**: Olá sistema de arquivos de cluster padrão.
   * **Tamanho dos nós de trabalho**.
   * **Tamanho do nó de cabeçalho**.

## <a name="delete-clusters"></a>Excluir clusters
Excluir um cluster não excluir conta de armazenamento padrão de saudação ou contas de armazenamento vinculado. Você pode recriar o cluster de saudação usando Olá mesmas contas de armazenamento e Olá metastores mesmo. É recomendável toouse um novo contêiner de Blob padrão quando você cria o cluster Olá novamente.

1. Entrar toohello [Portal][azure-portal].
2. Clique em **Clusters HDInsight** no menu esquerdo hello. Se você não vir **Clusters HDInsight**, clique primeiro em **Mais serviços**.
3. Clique em cluster Olá que você deseja toodelete.
4. Clique em **excluir** do menu superior hello e, em seguida, siga as instruções do hello.

Consulte também [Pausar/desligar clusters](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Adicionar outras contas de armazenamento

Depois de criar um cluster, você pode adicionar outras contas do Armazenamento do Azure e contas do Azure Data Lake Store. Para obter mais informações, consulte [adicionar tooHDInsight de contas de armazenamento adicional](./hdinsight-hadoop-add-storage.md).

## <a name="scale-clusters"></a>Dimensionar clusters
dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.

> [!NOTE]
> Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis. Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.  Confira [Listar e mostrar clusters](#list-and-show-clusters).
>
>

impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:

* O Hadoop

    Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução. Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento. Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.

    Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados. Esse comportamento faz com que a execução de todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento. No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.
* HBase

    Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução. Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação. No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon em toohello um nó principal do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Para obter mais informações sobre como usar o shell do HBase hello, consulte]
* Storm

    Sem problemas, você pode adicionar ou remover o cluster de profusão de tooyour de nós de dados enquanto ele está em execução. Mas, após a conclusão bem-sucedida da operação de dimensionamento de saudação, você precisará de topologia de saudação toorebalance.

    A redistribuição pode ser feita de duas maneiras:

  * Interface da Web Storm
  * Ferramenta CLI (interface de linha de comando)

    Consulte toohello [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.

    Interface da web Hello Storm está disponível no cluster do HDInsight hello:

    ![Redistribuir escala do Storm do HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clusters de tooscale**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **Clusters HDInsight** no menu esquerdo hello.
3. Clique em cluster Olá tooscale desejado.
3. Clique em **Dimensionar Cluster**.
4. Insira o **Número de Nós de Trabalho**. Olá limite número Olá de nós de cluster varia entre as assinaturas do Azure. Você pode contatar o limite de saudação de tooincrease suporte de cobrança.  informações de custo Olá refletem as alterações de saudação feitas toohello número de nós.

    ![HDInsight hadoop hbase storm spark dimensionar](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Pausar/desligar clusters

A maioria dos trabalhos do Hadoop é composta por trabalhos em lotes que só são executados ocasionalmente. Para a maioria dos clusters de Hadoop, há grandes períodos de tempo cluster Olá não está sendo usado para processamento. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso.
Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso.

Há muitas maneiras que você pode programar o processo de saudação:

* Use o Azure Data Factory. Veja [Criar clusters Hadoop baseados em Linux sob demanda usando o Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) para criar serviços vinculados do HDInsight sob demanda.
* Use o Azure PowerShell.  Consulte [Analisar dados de atraso de voo](hdinsight-analyze-flight-delay-data.md).
* Use a CLI do Azure. Consulte [Gerenciar clusters HDInsight usando a CLI do Azure](hdinsight-administer-use-command-line.md)
* Use o SDK .NET do HDInsight. Consulte [Enviar trabalhos do Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Para Olá informações sobre preços, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete um cluster do hello Portal, consulte [excluir clusters](#delete-clusters)


## <a name="upgrade-clusters"></a>Atualizar clusters

Consulte [versão mais recente do HDInsight atualizar cluster tooa](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Alterar senhas
Um cluster HDInsight pode ter duas contas de usuário. Olá (também conhecido como a conta de usuário de cluster do HDInsight Conta de usuário HTTP) e Olá SSH conta de usuário são criadas durante o processo de criação de saudação. Você pode usar o hello Ambari web da interface do usuário toochange Olá cluster conta de usuário e senha e script ações toochange Olá conta de usuário SSH

### <a name="change-hello-cluster-user-password"></a>Alterar senha de usuário de cluster Olá
Você pode usar a senha de usuário de Cluster Olá da interface do usuário do Ambari Web toochange hello. toolog em tooAmbari, você deve usar senha e nome de usuário do cluster existente hello.

> [!NOTE]
> Alterar senha de usuário (admin) de cluster de saudação pode causar ações executadas em relação a esse cluster toofail do script. Se você tiver as ações de script persistentes que nós de trabalho de destino, esses scripts podem falhar quando você adicionar nós toohello cluster por meio de operações de redimensionamento. Para saber mais sobre as Ações de Script, confira [Personalizar clusters HDInsight usando ações de Script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Entrar usando o Ambari Web UI toohello Olá credenciais de usuário de cluster HDInsight. é o nome de usuário do saudação padrão **admin**. Olá URL é **https://&lt;nome do Cluster HDInsight > cluster>.azurehdinsight.NET**.
2. Clique em **Admin** menu Olá superior e, em seguida, clique em "Gerenciar Ambari".
3. No menu à esquerda do hello, clique em **usuários**.
4. Clique em **Administrador**.
5. Clique em **Alterar Senha**.

Ambari, em seguida, altera a senha de saudação em todos os nós no cluster de saudação.

### <a name="change-hello-ssh-user-password"></a>Alterar senha de usuário SSH Olá
1. Usando um editor de texto, salve Olá texto a seguir como um arquivo chamado **changepassword.sh**.

   > [!IMPORTANT]
   > Você deve usar um editor que usa LF como final de linha de saudação. Se o editor de saudação usa CRLF, em seguida, Olá script não funciona.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Carregar Olá tooa local de armazenamento que pode ser acessado de HDInsight usando um endereço HTTP ou HTTPS. Por exemplo, um repositório de arquivos público como o OneDrive ou o Armazenamento de Blobs do Azure. Salve o arquivo de toohello URI (endereço HTTP ou HTTPS) de hello, conforme esse URI é necessário na próxima etapa do hello.
3. De Olá portal do Azure, clique em **Clusters HDInsight**.
4. Clique em seu cluster HDInsight.
4. Clique em **Ações de Script**.
4. De saudação **ações de Script** folha, selecione **enviar novo**. Olá quando **enviar ação de script** folha for exibida, insira Olá informações a seguir:

   | Campo | Valor |
   | --- | --- |
   | Nome |Alterar senha SSH |
   | URI do script Bash |arquivo de changepassword.sh Olá URI toohello |
   | Nós (Principal, Trabalho, Nimbus, Supervisor, Zookeeper etc.) |✓ para todos os tipos de nós listados |
   | parâmetros |Digite nome de usuário SSH hello e, em seguida, Olá nova senha. Deve haver um espaço entre o nome de usuário de saudação e a senha de saudação. |
   | Persistir esta ação de script... |Deixe este campo desmarcado. |
5. Selecione **criar** tooapply script de saudação. Quando termina de script hello, você é capaz de tooconnect toohello cluster usando o SSH com a nova senha hello.

## <a name="grantrevoke-access"></a>Conceder/revogar acesso
Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Por padrão, esses serviços são concedidos para acesso. Você pode revogar/conceder Olá acesso usando [CLI do Azure](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) e [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Localizar a ID de assinatura de saudação

**toofind suas IDs de assinatura do Azure**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **Assinaturas**. Cada assinatura tem um nome e uma ID.

Cada cluster é associado tooan assinatura do Azure. Olá assinatura ID é mostrado no cluster Olá **essencial** lado a lado. Confira [Listar e mostrar clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Localizar o grupo de recursos de saudação
No modo do Azure Resource Manager Olá, cada cluster HDInsight é criada com um grupo do Gerenciador de recursos do Azure. grupo de Gerenciador de recursos de saudação que um cluster pertence tooappears em:

* Olá cluster lista tem um **grupo de recursos** coluna.
* Bloco **Fundamentos** do cluster.  

Confira [Listar e mostrar clusters](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Localizar a conta de armazenamento saudação padrão
Cada cluster HDInsight tem uma conta de armazenamento padrão. Olá conta de armazenamento padrão e as chaves para um cluster é exibido em **contas de armazenamento**. Confira [Listar e mostrar clusters](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Execute consultas Hive
Você não pode executar o trabalho de Hive diretamente do hello portal do Azure, mas você pode usar o hello Hive exibir na interface do usuário do Ambari Web.

**consultas de Hive toorun usando o modo de exibição de Hive do Ambari**

1. Entrar usando o Ambari Web UI toohello Olá credenciais de usuário de cluster HDInsight. é o nome de usuário do saudação padrão **admin**. Olá URL é **https://&lt;nome do Cluster HDInsight > cluster>.azurehdinsight.NET**.
2. Abrir modo de exibição de Hive conforme Olá captura de tela a seguir:  

    ![Exibição do Hive do HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Clique em **consulta** no menu superior hello.
4. Insira uma consulta Hive no **Editor de Consultas**, em seguida, clique em **Executar**.

## <a name="monitor-jobs"></a>Monitorar trabalhos
Consulte [HDInsight gerenciar clusters usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Procurar arquivos
Usando Olá portal do Azure, você pode procurar conteúdo de saudação do contêiner padrão de saudação.

1. Entrar muito[https://portal.azure.com](https://portal.azure.com).
2. Clique em **Clusters HDInsight** de saudação toolist menu esquerdo Olá clusters existentes.
3. Clique no nome do cluster de saudação. Se a lista de clusters Olá for longa, você pode usar o filtro na parte superior de saudação da página de saudação.
4. Clique em **contas de armazenamento** no menu à esquerda do cluster hello.
5. Clique em uma conta de Armazenamento.
7. Clique em Olá **Blobs** lado a lado.
8. Clique em nome do contêiner de saudação padrão.

## <a name="monitor-cluster-usage"></a>Monitorar o uso do cluster
Olá **uso** seção da folha de cluster do HDInsight Olá exibe informações sobre o número de saudação de uma assinatura de núcleos tooyour disponíveis para uso com o HDInsight, bem como o número de saudação de núcleos alocados toothis cluster e como eles são alocada para nós Olá neste cluster. Confira [Listar e mostrar clusters](#list-and-show-clusters).

> [!IMPORTANT]
> Serviços de saudação toomonitor fornecido pela Olá cluster HDInsight, você deve usar o Ambari Web ou Olá Ambari REST API. Para saber mais sobre como usar o Ambari, consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="connect-tooa-cluster"></a>Conecte-se o cluster tooa

* [Usar o Hive com o HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Use o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu algumas funções administrativas básicas. toolearn mais, consulte Olá artigos a seguir:

* [Administrar o HDInsight usando o PowerShell do Azure](hdinsight-administer-use-powershell.md)
* [Administrar o HDInsight usando a CLI do Azure](hdinsight-administer-use-command-line.md)
* [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Usar o Hive no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig no HDInsight](hdinsight-use-pig.md)
* [Usar o Sqoop no HDInsight](hdinsight-use-sqoop.md)
* [Introdução ao Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Qual versão do Hadoop está no Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Linha de comando do Hadoop"
