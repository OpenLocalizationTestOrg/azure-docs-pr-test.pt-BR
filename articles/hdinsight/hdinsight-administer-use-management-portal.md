---
title: "clusters de Hadoop baseado em Windows aaaManage HDInsight usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como tooadminister HDInsight Service. Crie um cluster HDInsight, console interativo de JavaScript Olá aberto e console de comando do Hadoop Olá aberto."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Gerenciar clusters baseados no Windows Hadoop em HDInsight usando Olá portal do Azure

Usando Olá [portal do Azure][azure-portal], você pode criar clusters baseados no Windows Hadoop no HDInsight do Azure, altere a senha do usuário Hadoop e habilitar o protocolo de área de trabalho remota (RDP) para que você possa acessar Olá Hadoop console de comando em cluster hello.

informações de saudação neste artigo só se aplica a clusters de HDInsight baseados em tooWindow. Para obter informações sobre como gerenciar clusters baseados em Linux, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Conta de armazenamento do Azure** -HDInsight um cluster usa um contêiner de armazenamento de BLOBs do Azure como sistema de arquivos padrão de saudação. Para obter mais informações sobre como o Armazenamento de Blob do Azure fornece uma experiência perfeita com os clusters HDInsight, consulte [Usar o Armazenamento de Blob do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md). Para obter detalhes sobre como criar uma conta de armazenamento do Azure, consulte [como uma conta de armazenamento do tooCreate](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Olá abrir Portal
1. Entrar muito[https://portal.azure.com](https://portal.azure.com).
2. Depois de abrir o portal hello, você pode:

   * Clique em **novo** de saudação menu esquerdo toocreate um novo cluster:

       ![novo botão do cluster HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Clique em **Clusters HDInsight** no menu esquerdo hello.

       ![Botão do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Se **HDInsight** não aparecer no menu esquerdo hello, clique em **procurar**.

     ![Botão Procurar cluster do Portal do Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Criar clusters
Para instruções de criação de saudação usando Olá Portal, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md).

O HDInsight trabalha com uma ampla variedade de componentes do Hadoop. Para Olá a lista de componentes de saudação que foram verificadas e suporte, consulte [é qual versão do Hadoop no HDInsight do Azure](hdinsight-component-versioning.md). Você pode personalizar o HDInsight usando uma saudação as opções a seguir:

* Use Script ação toorun scripts personalizados que podem personalizar um cluster tooeither alterar a configuração de cluster ou instalar componentes personalizados, como Giraph ou Solr. Para obter mais informações, consulte [Personalizar cluster HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md).
* Use parâmetros de personalização de cluster Olá Olá HDInsight .NET SDK ou do PowerShell do Azure durante a criação do cluster. Essas alterações de configuração, em seguida, são preservadas por tempo de vida de saudação do cluster hello e não são afetadas por reimages de nó de cluster que periodicamente realiza a plataforma Windows Azure para manutenção. Para obter mais informações sobre como usar parâmetros de personalização de cluster hello, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md).
* Alguns componentes de Java nativo, como Mahout e em cascata, podem ser executados no cluster hello como arquivos JAR. Esses arquivos JAR podem ser distribuída tooAzure armazenamento de Blob e enviada tooHDInsight clusters por meio de mecanismos de envio de trabalho do Hadoop. Para obter mais informações, consulte [Enviar trabalhos do Hadoop de forma programática](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > Se você tiver problemas de implantação de clusters de tooHDInsight arquivos JAR ou chamar arquivos JAR em clusters de HDInsight, entre em contato com [Microsoft Support](https://azure.microsoft.com/support/options/).
  >
  > O Cascading não tem suporte do HDInsight e não é qualificado para o Suporte da Microsoft. Para listas de componentes com suporte, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).
  >
  >

Não há suporte para a instalação de software personalizadas no cluster hello usando a Conexão de área de trabalho remota. Evite armazenar arquivos em unidades de saudação do nó principal do hello, como eles serão perdidos se você precisar toore-criar clusters de saudação. É recomendável armazenar os arquivos no armazenamento de Blob do Azure. O armazenamento de Blob é persistente.

## <a name="list-and-show-clusters"></a>Listar e mostrar clusters
1. Entrar muito[https://portal.azure.com](https://portal.azure.com).
2. Clique em **Clusters HDInsight** no menu esquerdo hello.
3. Clique no nome do cluster de saudação. Se a lista de clusters Olá for longa, você pode usar o filtro na parte superior de saudação da página de saudação.
4. Clique duas vezes em um cluster de detalhes da saudação Olá lista tooshow.

    **Menu e fundamentos**:

    ![Fundamentos do cluster HDInsight do portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * menu de Olá toocustomize, clique em qualquer lugar no menu hello e, em seguida, clique em **personalizar**.
   * **Configurações de** e **todas as configurações**: Olá exibe **configurações** folha para cluster hello, que permite que você tooaccess informações detalhadas de configuração de cluster de saudação.
   * **Painel**, **painel Cluster** e **URL: essas são todas as maneiras tooaccess Olá painel do cluster, que é o Ambari Web para clusters baseados em Linux. -**Seguro Shell * *: Mostra o cluster do hello instruções tooconnect toohello usando conexão Secure Shell (SSH).
   * **Dimensionar o Cluster**: permite que você toochange número de saudação de nós de trabalho para este cluster.
   * **Excluir**: cluster de saudação de exclusões.
   * **Início Rápido**: exibe informações que o ajudarão a começar a usar o HDInsight.
   * * * Os usuários: Permite a você permissões de tooset para *management portal* deste cluster para outros usuários na sua assinatura do Azure.

     > [!IMPORTANT]
     > Isso *somente* afeta o acesso e permissões cluster toothis no hello portal do Azure, e não tem efeito sobre quem pode se conectar a cluster do HDInsight tooor enviar trabalhos toohello.
     >
     >
   * **Marcas**: as marcas permitem que você tooset chave/valor pares toodefine uma taxonomia personalizada dos serviços de nuvem. Por exemplo, você pode criar uma chave chamada **projeto**e usar um valor comum para todos os serviços associados a um projeto específico.
   * **Modos de exibição do Ambari**: Links tooAmbari da Web.

     > [!IMPORTANT]
     > Serviços de saudação toomanage fornecido pela Olá cluster HDInsight, você deve usar o Ambari Web ou Olá Ambari REST API. Para saber mais sobre como usar o Ambari, consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Uso**:

     ![Uso do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Clique em **Configurações**.

    ![Uso do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Propriedades**: exibir as propriedades do cluster hello.
   * **Identidade do AAD do Cluster**:
   * **Chaves de armazenamento do Azure**: exibir a conta de armazenamento padrão hello e sua chave. conta de armazenamento Olá é a configuração durante o processo de criação de cluster hello.
   * **Logon de cluster**: alterar o nome de usuário de cluster HTTP hello e a senha.
   * **Os Metastores externos**: Exibir hello os metastores Hive e Oozie. Olá metastores só pode ser configurados durante o processo de criação de cluster hello.
   * **Dimensionar o Cluster**: aumentar e diminuir Olá número de nós de trabalho do cluster.
   * **Área de trabalho remota**: habilitar e desabilitar o acesso de área de trabalho remota (RDP) e configurar o nome de usuário RDP hello.  nome de usuário RDP Olá deve ser diferente do nome de usuário HTTP hello.
   * **Parceiro de Registro**:

     > [!NOTE]
     > Esta é uma lista genérica de configurações disponíveis; nem todas elas estarão presentes para todos os tipos de cluster.
     >
     >
6. Clique em **Propriedades**:

    seção de propriedades de saudação lista a seguir hello:

   * **Nome do host**: nome do cluster.
   * **URL do Cluster**.
   * **Status**: incluindo Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization
   * **Região**: local do Azure. Para obter uma lista dos locais do Azure com suporte, consulte Olá **região** caixa de listagem suspensa em [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Dados criados**.
   * **Sistema operacional**: **Windows** ou **Linux**.
   * **Tipo**: Hadoop, HBase, Storm, Spark.
   * **Versão**. Consulte [versões do HDInsight](hdinsight-component-versioning.md)
   * **Assinatura**: nome da assinatura.
   * <seg>
  **ID da assinatura**.</seg>
   * **Fonte de dados primária**. Olá conta de armazenamento de BLOBs do Azure usado como padrão de saudação sistema de arquivos Hadoop.
   * **Faixa de preço dos nós de trabalho**.
   * **Faixa de preço do nó de cabeça**.

## <a name="delete-clusters"></a>Excluir clusters
Excluir um cluster não excluirá a conta de armazenamento padrão de saudação ou contas de armazenamento vinculado. Você pode recriar o cluster de saudação usando Olá mesmas contas de armazenamento e Olá metastores mesmo.

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **excluir** do menu superior hello e, em seguida, siga as instruções do hello.

Consulte também [Pausar/desligar clusters](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Dimensionar clusters
dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.

> [!NOTE]
> Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis. Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.  Confira [Listar e mostrar clusters](#list-and-show-clusters).
>
>

impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:

* O Hadoop

    Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução. Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento. Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.

    Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados. Isso faz com que todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento. No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.
* HBase

    Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução. Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação. No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon no nó principal de saudação do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:

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

    ![HDInsight storm dimensionar novo balanceamento](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**clusters de tooscale**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **configurações** no menu superior hello e clique **Cluster de escala**.
4. Insira o **Número de Nós de Trabalho**. limite de Olá no número de saudação do nó de cluster varia entre as assinaturas do Azure. Você pode contatar o limite de saudação de tooincrease suporte de cobrança.  informações de custo Olá refletirá Olá alterações toohello número de nós.

    ![HDInsight Hadoop HBase Storm Spark scale](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Pausar/desligar clusters
A maioria dos trabalhos do Hadoop é composta por trabalhos em lotes que só são executados ocasionalmente. Para a maioria dos clusters de Hadoop, há grandes períodos de tempo cluster Olá não está sendo usado para processamento. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso.
Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso.

Há muitas maneiras que você pode programar o processo de saudação:

* Use o Azure Data Factory. Consulte [Serviços Vinculados ao Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) e [Transformar e analisar usando o Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) para saber mais sobre os serviços sob demanda e autodefinidos vinculados ao HDInsight.
* Use o Azure PowerShell.  Consulte [Analisar dados de atraso de voo](hdinsight-analyze-flight-delay-data.md).
* Use a CLI do Azure. Consulte [Gerenciar clusters HDInsight usando a CLI do Azure](hdinsight-administer-use-command-line.md)
* Use o SDK .NET do HDInsight. Consulte [Enviar trabalhos do Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).

Para Olá informações sobre preços, consulte [preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete um cluster do hello Portal, consulte [excluir clusters](#delete-clusters)

## <a name="change-cluster-username"></a>Alterar nome de usuário do cluster
Um cluster HDInsight pode ter duas contas de usuário. saudação de conta de usuário de cluster do HDInsight é criada durante o processo de criação de saudação. Você também pode criar uma conta de usuário RDP para acessar o cluster Olá via RDP. Consulte [Habilitar área de trabalho remota](#connect-to-hdinsight-clusters-by-using-rdp).

**senha e nome de usuário do cluster toochange Olá HDInsight**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **configurações** no menu superior hello e clique **logon de Cluster**.
4. Se **logon de Cluster** foi habilitado, você deve clicar em **desabilitar**e, em seguida, clique em **habilitar** antes de poder alterar Olá username e password.
5. Saudação de alteração **nome de logon de Cluster** e/ou Olá **senha de logon de Cluster**e, em seguida, clique em **salvar**.

    ![HDInsight change cluster user username password http user](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Conceder/revogar acesso
Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Por padrão, esses serviços são concedidos para acesso. Você pode revogar/conceder o acesso de saudação do hello portal do Azure.

> [!NOTE]
> Revogando concedendo/acesso hello, redefinirá senha e nome de usuário de cluster hello.
>
>

**acesso de serviços da web HTTP toogrant/revoke**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **configurações** no menu superior hello e clique **logon de Cluster**.
4. Se **logon de Cluster** foi habilitado, você deve clicar em **desabilitar**e, em seguida, clique em **habilitar** antes de poder alterar Olá username e password.
5. Para **nome de usuário de logon de Cluster** e **senha de logon de Cluster**, digite Olá novo nome de usuário e senha (respectivamente) para o cluster de saudação.
6. Clique em **SALVAR**.

    ![HDInsight grand remove http web service access](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Localizar a conta de armazenamento saudação padrão
Cada cluster HDInsight tem uma conta de armazenamento padrão. Olá conta de armazenamento padrão e as chaves para um cluster é exibido em **configurações**/**propriedades**/**as chaves de armazenamento do Azure**. Confira [Listar e mostrar clusters](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Localizar o grupo de recursos de saudação
No modo do Azure Resource Manager hello, cada cluster HDInsight é criada com um grupo de recursos do Azure. grupo de recursos do Azure de saudação que um cluster pertence tooappears em:

* Olá cluster lista tem um **grupo de recursos** coluna.
* Bloco **Fundamentos** do cluster.  

Consulte [Listar e mostrar clusters](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Abrir o console de Consulta do HDInsight
Olá console de consulta de HDInsight inclui Olá recursos a seguir:

* **Editor Hive**: uma interface GUI da Web para enviar trabalhos do Hive.  Consulte [Hive executar consultas usando Olá Console de consulta](hdinsight-hadoop-use-hive-query-console.md).

    ![Editor de hive do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Histórico de trabalhos**: monitore trabalhos do Hadoop.  

    ![histórico de trabalhos do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Clique em **nome de consulta** tooshow detalhes de saudação incluindo propriedades do trabalho, **consulta de trabalho**, e * * saída de trabalho. Você também pode baixar consulta hello e Olá saída tooyour estação de trabalho.
* **Navegador de arquivo**: procurar a conta de armazenamento padrão hello e Olá contas de armazenamento vinculada.

    ![Pesquisa do navegador de arquivos do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    Na captura de tela hello, Olá  **<Account>**  tipo indica o item de saudação é uma conta de armazenamento do Azure.  Clique em Olá conta nome toobrowse Olá arquivos.
* **IU do Hadoop**.

    ![Interface do usuário do Hadoop do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    Na **IU do Hadoop*, você pode procurar arquivos e verificar logs.
* **IU do Yarn**.

    ![Interface do usuário do YARN do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Execute consultas Hive
trabalhos de Hive tooran de saudação Portal, clique em **Editor Hive** na Olá consulta HDInsight console. Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Monitorar trabalhos
trabalhos de toomonitor de saudação Portal, clique em **histórico de trabalho** na Olá consulta HDInsight console. Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Procurar arquivos
arquivos toobrowse e armazenados na conta de armazenamento padrão Olá Olá contas de armazenamento vinculada, clique em **navegador de arquivo** na Olá consulta HDInsight console. Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

Você também pode usar o hello **procurar o sistema de arquivos Olá** utility do hello **Hadoop UI** no console do HDInsight hello.  Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Monitorar o uso do cluster
Olá **uso** seção da folha de cluster do HDInsight Olá exibe informações sobre o número de saudação de uma assinatura de núcleos tooyour disponíveis para uso com o HDInsight, bem como o número de saudação de núcleos alocados toothis cluster e como eles são alocada para nós Olá neste cluster. Confira [Listar e mostrar clusters](#list-and-show-clusters).

> [!IMPORTANT]
> Serviços de saudação toomonitor fornecido pela Olá cluster HDInsight, você deve usar o Ambari Web ou Olá Ambari REST API. Para saber mais sobre como usar o Ambari, consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)
>
>

## <a name="open-hadoop-ui"></a>Abrir a IU do Hadoop
cluster de saudação toomonitor, sistema de arquivos de saudação procurar e verifique os logs, clique em **Hadoop UI** na Olá consulta HDInsight console. Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Abrir a IU do Yarn
toouse interface de usuário do Yarn, clique em **Yarn UI** na Olá consulta HDInsight console. Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Conecte-se tooclusters usando o RDP
as credenciais de saudação para cluster Olá que você forneceu na sua criação, conceda acesso toohello serviços em cluster hello, mas não toohello próprio cluster por meio da área de trabalho remota. Você pode ativar o acesso de Área de Trabalho Remota ao provisionar um cluster ou depois que um cluster for provisionado. Para obter instruções sobre como habilitar a área de trabalho remota no momento da criação Olá, consulte [cluster HDInsight criar](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable área de trabalho remota**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **configurações** no menu superior hello e clique **área de trabalho remota**.
4. Insira **Expira em**, **Nome de Usuário de Área de Trabalho Remota** e **Senha de Área de Trabalho Remota** e clique em **Habilitar**.

    ![Habilitar/desabilitar configuração de área de trabalho remota do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    valores padrão de saudação para expira em é uma semana.

   > [!NOTE]
   > Você também pode usar o hello HDInsight .NET SDK tooenable área de trabalho remota em um cluster. Saudação de uso **EnableRdp** método no objeto de cliente Olá HDInsight no hello maneira a seguir: **cliente. EnableRdp (clustername, local, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**. Da mesma forma, toodisable área de trabalho remota no cluster hello, você pode usar **cliente. DisableRdp (clustername, local)**. Para obter mais informações sobre esses métodos, consulte [Referência do SDK do .NET HDInsight](http://go.microsoft.com/fwlink/?LinkId=529017). Isso é aplicável apenas a clusters do HDInsight em execução no Windows.
   >
   >

**tooconnect tooa cluster usando o RDP**

1. Entrar toohello [Portal][azure-portal].
2. Clique em **procurar todos os** menu Olá esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.
3. Clique em **configurações** no menu superior hello e clique **área de trabalho remota**.
4. Clique em **conectar** e siga as instruções de saudação. Se Conectar estiver desabilitado, você deverá habilitá-lo primeiro. Certifique-se usando a área de trabalho remota Olá de usuário e senha.  Você não pode usar as credenciais de usuário de Cluster hello.

## <a name="open-hadoop-command-line"></a>Abrir a linha de comando do Hadoop
cluster de toohello tooconnect usando a área de trabalho remota e de linha de comando do Hadoop de saudação de uso, você precisa primeiro ativar cluster de toohello de acesso de área de trabalho remota conforme descrito na seção anterior hello.

**tooopen uma linha de comando do Hadoop**

1. Conecte-se toohello cluster usando a área de trabalho remota.
2. Na área de trabalho hello, clique duas vezes em **linha de comando do Hadoop**.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Para obter mais informações sobre os comandos Hadoop, consulte [Referência de comandos Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

Captura de tela anterior Olá, nome da pasta Olá tem número de versão do Hadoop Olá inserido. número de versão de Hello pode versão alterados Olá com base em componentes de Hadoop de saudação instalado no cluster de saudação. Você pode usar pastas do Hadoop ambiente variáveis toorefer toothose. Por exemplo:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toocreate um cluster HDInsight usando Olá Portal e como tooopen Olá a ferramenta de linha de comando do Hadoop. toolearn mais, consulte Olá artigos a seguir:

* [Administrar o HDInsight usando o PowerShell do Azure](hdinsight-administer-use-powershell.md)
* [Administrar o HDInsight usando a CLI do Azure](hdinsight-administer-use-command-line.md)
* [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Enviar trabalhos Hadoop de forma programática](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Introdução ao Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Qual versão do Hadoop está no Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Linha de comando do Hadoop"
