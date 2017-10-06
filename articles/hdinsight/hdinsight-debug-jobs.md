---
title: "Depurar o Hadoop no HDInsight: exibir logs e interpretar mensagens de erro – Azure | Microsoft Docs"
description: "Saiba mais sobre mensagens de erro Olá que você pode receber ao administrar HDInsight usando o PowerShell e etapas que você pode tomar toorecover."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Analisar logs do HDInsight
Cada cluster Hadoop no HDInsight do Azure tem uma conta de armazenamento do Azure usada como padrão do sistema de arquivo hello. conta de armazenamento Olá é conhecida como conta de armazenamento saudação padrão. Cluster usa hello armazenamento de tabela do Azure e armazenamento de Blob de saudação em toostore de conta de armazenamento saudação padrão seus logs.  toofind conta de armazenamento padrão Olá para o cluster, consulte [Hadoop gerenciar clusters de HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). Olá logs reter no Olá conta de armazenamento, mesmo depois que o cluster Olá é excluído.

## <a name="logs-written-tooazure-tables"></a>Logs gravados tooAzure tabelas
Olá logs gravados tooAzure tabelas fornecem um nível de informações sobre o que está acontecendo com um cluster HDInsight.

Quando você cria um cluster HDInsight, 6 tabelas são criadas automaticamente para clusters baseados em Linux no armazenamento de tabela saudação padrão:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Três tabelas são criadas para clusters baseados no Windows:

* setuplog: log de eventos/exceções encontrados no provisionamento/configuração de clusters do HDInsight.
* hadoopinstalllog: Log de eventos/exceções encontradas durante a instalação do Hadoop no cluster de saudação. Esta tabela pode ser úteis na depuração de problemas relacionados a tooclusters criado com parâmetros personalizados.
* hadoopservicelog: log de eventos/exceções registrados por todos os serviços do Hadoop. Essa tabela pode ser útil na depuração de problemas relacionados toojob falhas em clusters de HDInsight.

nomes de arquivo Hello tabela são **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Essas tabelas contém Olá campos a seguir:

* ClusterDnsName
* ComponentName
* EventTimestamp
* Host
* MALoggingHash
* Mensagem
* N
* PreciseTimeStamp
* Função
* RowIndex
* Locatário
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Ferramentas para acessar logs de saudação
Há muitas ferramentas disponíveis para acesso dos dados nessas tabelas:

* Visual Studio
* Gerenciador de Armazenamento do Azure
* Power Query para Excel

#### <a name="use-power-query-for-excel"></a>Usar o Power Query para Excel
O Power Query pode ser instalado a partir do site [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Consulte Olá a página de download para os requisitos de sistema Olá

**toouse Power Query tooopen e analisar o log do serviço Olá**

1. Abra o **Microsoft Excel**.
2. De saudação **Power Query** menu, clique em **do Azure**e, em seguida, clique em **armazenamento de tabela do Microsoft Azure**.
   
    ![HDInsight Hadoop Excel PowerQuery abrir o Armazenamento de Tabelas do Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Insira o nome de conta de armazenamento hello. Isso pode ser o nome curto do hello ou Olá FQDN.
4. Insira a chave de conta de armazenamento hello. Você verá uma lista de tabelas:
   
    ![Logs do HDInsight Hadoop armazenados no Armazenamento de Tabelas do Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Tabela de hadoopservicelog Olá com o botão direito no hello **navegador** painel e selecione **editar**. Você deverá ver quatro colunas. Opcionalmente, excluir Olá **chave de partição**, **chave de linha**, e **Timestamp** colunas selecionando-os e clicando em **remover colunas** Opções de saudação na faixa de opções de saudação.
6. Clique em Olá expanda ícone Olá coluna toochoose Olá colunas que você deseja tooimport na planilha do Excel de saudação de conteúdo. Para esta demonstração, escolhi TraceLevel e ComponentName: elas podem me dar algumas informações básicas sobre quais componentes apresentaram problemas.
   
    ![Logs do HDInsight Hadoop escolher colunas](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Clique em **Okey** tooimport dados de saudação.
8. Selecione Olá **TraceLevel**, função, e **ComponentName** colunas e clique **Group By** controle na faixa de opções de saudação.
9. Clique em **Okey** Olá Group By caixa
10. Clique em **Aplicar e Fechar**.

Agora você pode usar o Excel toofilter e classificação conforme necessário. Obviamente, talvez você queira tooinclude outras colunas (por exemplo, a mensagem) na ordem toodrill para baixo em problemas quando eles ocorrem, mas selecionar e agrupar Olá colunas descritas acima oferece um panorama razoável do que está acontecendo com os serviços Hadoop. Olá mesmo ideia pode ser aplicado toohello setuplog e hadoopinstalllog tabelas.

#### <a name="use-visual-studio"></a>Usar o Virtual Studio
**toouse Visual Studio**

1. Abra o Visual Studio.
2. De saudação **exibição** menu, clique em **Cloud Explorer**. Ou simplesmente clique em **CTRL+\, CTRL+X**.
3. No **Gerenciador de Nuvem**, selecione **Tipos de Recurso**.  Olá outra opção disponível é **grupos de recursos**.
4. Expanda **contas de armazenamento**, Olá conta de armazenamento padrão para o cluster e, em seguida, **tabelas**.
5. Clique duas vezes em **hadoopservicelog**.
6. Adicione um filtro. Por exemplo:
   
        TraceLevel eq 'ERROR'
   
    ![Logs do HDInsight Hadoop escolher colunas](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Para obter mais informações sobre como construir filtros, consulte [construir cadeias de caracteres de filtro para Olá Designer de tabela](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Logs gravadas tooAzure armazenamento de Blob
[Olá logs tooAzure escrito tabelas](#log-written-to-azure-tables) fornecem um nível de informações sobre o que está acontecendo com um cluster HDInsight. No entanto, essas tabelas não fornecem logs no nível da tarefa, que podem ser úteis para a análise mais detalhada dos problemas, quando eles ocorrerem. tooprovide próximo nível de detalhe, HDInsight clusters são configurado a conta de armazenamento de Blob de tooyour toowrite tarefas logs para qualquer trabalho que é enviado por meio de Templeton. Praticamente, isso significa que os trabalhos enviados usando cmdlets do PowerShell do Microsoft Azure hello ou hello APIs de envio de trabalho do .NET, não os trabalhos enviados por meio de RDP/linha de comando toohello cluster de acesso. 

tooview Olá logs, consulte [logs do aplicativo de acesso YARN no HDInsight baseados em Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Para saber mais sobre os logs de aplicativos, confira [Como simplificar o gerenciamento de logs do usuário e o acesso no YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Exibir logs de trabalho e integridade do cluster
### <a name="access-hadoop-ui"></a>Acessar a interface de usuário do Hadoop
De Olá portal do Azure, clique em uma folha de cluster HDInsight cluster nome tooopen hello. Na folha de cluster hello, clique em **painel**.

![Iniciar painel do cluster](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Quando solicitado, insira as credenciais de administrador de cluster hello. No hello Console de consulta que é aberta, clique em **Hadoop UI**.

![Iniciar a interface do usuário do Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Saudação de acesso Yarn da interface do usuário
De Olá portal do Azure, clique em uma folha de cluster HDInsight cluster nome tooopen hello. Na folha de cluster hello, clique em **painel**. Quando solicitado, insira as credenciais de administrador de cluster hello. No hello Console de consulta que é aberta, clique em **YARN UI**.

Você pode usar o seguinte de Olá Olá YARN da interface do usuário toodo:

* **Obter o status do cluster**. No painel esquerdo do hello, expanda **Cluster**e clique em **sobre**. Detalhes de status como total alocada memória, núcleos usados, estado do Gerenciador de recursos de cluster de saudação do cluster neste momento, o cluster versão etc.
  
    ![Iniciar painel do cluster](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Obtenha o status do nó**. No painel esquerdo do hello, expanda **Cluster**e clique em **nós**. Lista todos os nós de saudação em cluster hello, o endereço HTTP de cada nó, o nó de tooeach alocado de recursos, etc.
* **Monitore o status do trabalho**. No painel esquerdo do hello, expanda **Cluster**e, em seguida, clique em **aplicativos** toolist todos os trabalhos no cluster de saudação de hello. Se você quiser toolook em trabalhos em um determinado estado (por exemplo, execução enviada, novo, etc.), clique em link apropriado de saudação em **aplicativos**. Ainda mais, você pode clicar Olá trabalho nome toofind mais informações sobre o trabalho de saudação tais incluindo saída de hello, logs, etc.

### <a name="access-hello-hbase-ui"></a>Saudação de acesso HBase UI
De Olá portal do Azure, clique em uma folha de cluster do HDInsight HBase cluster nome tooopen hello. Na folha de cluster hello, clique em **painel**. Quando solicitado, insira as credenciais de administrador de cluster hello. No hello Console de consulta que é aberta, clique em **HBase UI**.

## <a name="hdinsight-error-codes"></a>Códigos de erro do HDInsight
Olá mensagens de erro detalhadas nesta seção são fornecidas toohelp usuários de saudação do Hadoop no HDInsight do Azure entendem possíveis condições de erro que eles podem encontrar durante a administração de serviço hello usando o PowerShell do Azure e tooadvise-los em etapas Olá que podem ser tomado toorecover de erro de saudação.

Algumas dessas mensagens de erro também podem ser exibidas no portal do Azure de saudação quando é usado toomanage clusters de HDInsight. Você pode encontrar outras mensagens de erro, mas há menos granular devido a restrições toohello Olá corretivas possíveis neste contexto. Outras mensagens de erro são fornecidas em contextos de saudação onde mitigação Olá é óbvia. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Descrição**: Forneça detalhes do banco de dados SQL do Azure para pelo menos um componente na ordem toouse configurações personalizadas para metastores Hive e Oozie.
* **Mitigação**: usuário Olá precisa toosupply um SQL Azure metastore e repita a operação Olá solicitação válida.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Descrição**: não foi possível criar o cluster na região *nameOfYourRegion*. Use uma região do HDInsight válida e repita a solicitação.
* **Mitigação**: cliente deve criar a região do cluster Olá atualmente com suporte: Sudeste da Ásia, Europa Ocidental, Norte da Europa, Leste dos EUA ou oeste dos EUA.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Descrição**: não foi possível localizar o servidor de saudação Olá solicitou o registro de cluster.  
* **Mitigação**: repita a operação de saudação.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Descrição**: o nome DNS do cluster *yourDnsName* é inválido. O nome deve começar e terminar com caracteres alfanuméricos e pode conter apenas o caractere especial '-'  
* **Mitigação**: Certifique-se de que você usou um nome DNS válido para o cluster que inicia e termina com alfanuméricos e não contém nenhum especial caracteres diferentes de traço Olá '-' e, em seguida, repita a operação de saudação.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Descrição**: o nome do Cluster *yourClusterName* não está disponível. Escolha outro nome.  
* **Mitigação**: Olá usuário deve especificar um clustername exclusivo e não existe e repita. Se estiver usando o usuário Olá Olá Portal, Olá interface do usuário será notificá-lo se um nome de cluster já está sendo usado durante a saudação criar etapas.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Descrição**: a senha do cluster é inválida. Senha deve ter pelo menos 10 caracteres e deve conter pelo menos um número, letra maiuscula, letra minúscula e caractere especial sem espaços e não deve conter o nome de usuário de hello como parte do mesmo.  
* **Mitigação**: forneça uma senha de cluster válido e repita a operação de saudação.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Description**: o nome de usuário do cluster é inválido. Verifique se o nome do usuário não contém caracteres especiais ou espaços.  
* **Mitigação**: forneça um nome de usuário de cluster válido e repita a operação de saudação.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Descrição**: o nome DNS do cluster *yourDnsClusterName é inválido* . O nome deve começar e terminar com caracteres alfanuméricos e pode conter apenas o caractere especial '-'  
* **Mitigação**: forneça um nome de usuário de cluster DNS válido e repita a operação de saudação.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Descrição**: nome do contêiner no URI *yourcontainerURI* e o nome DNS *yourDnsName* na solicitação de corpo deve ser Olá mesmo.  
* **Mitigação**: Certifique-se de que o nome do contêiner e seu nome DNS são Olá mesmo e repita a operação de saudação.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Descrição**: a configuração do cluster é inválida. Não é possível toofind quaisquer definições de nó de dados de tamanho de nó.  
* **Mitigação**: repita a operação de saudação.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Descrição**: Falha na exclusão de implantação para Olá Cluster  
* **Mitigação**: repita a operação de exclusão de saudação.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Descrição**: erro de configuração de serviço. Informações de mapeamento de DNS necessárias não encontradas.  
* **Atenuação**: exclua e crie um novo cluster.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Descrição**: tentativa de criação de contêiner de cluster duplicado. Existe um registro para *nameOfYourContainer* mas as Etags não coincidem.
* **Mitigação**: forneça um nome exclusivo para a operação de criação do contêiner hello e saudação de repetição.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Descrição**: o serviço hospedado *nameOfYourHostedService* já contém um cluster. Um serviço hospedado não pode conter vários clusters  
* **Mitigação**: serviço hospedado do cluster do Host Olá em outro.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Descrição**: servidor de saudação não foi possível atualizar o estado de Olá Olá da implantação do cluster.  
* **Mitigação**: repita a operação de saudação. Se isso acontecer várias vezes, entre em contato com o CSS.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Descrição**: o cluster *yourClusterName* foi excluído como parte da manutenção. Recrie o cluster hello.
* **Mitigação**: cluster de saudação de recriação.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Descrição**: a configuração do cluster é inválida. Configuração de nó de cabeçalho necessária não encontrada nos tamanhos de nós.
* **Mitigação**: repita a operação de saudação.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Descrição**: não é possível toocreate o serviço hospedado *nameOfYourHostedService*. Tente novamente a solicitação.  
* **Mitigação**: solicitação de saudação de repetição.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Descrição**: o serviço hospedado *nameOfYourHostedService* já contém uma implantação em produção. Um serviço hospedado não pode conter várias implantações em produção. Repita a solicitação de saudação com um nome de cluster diferente.
* **Mitigação**: Use um nome de cluster diferente e tente novamente a solicitação de saudação.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Descrição**: serviço hospedado *nameOfYourHostedService* para cluster Olá não foi encontrado.  
* **Mitigação**: se o cluster de saudação está em estado de erro, exclua-o e tente novamente.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Descrição**: o serviço hospedado *nameOfYourHostedService* não tem uma implantação associada.  
* **Mitigação**: se o cluster de saudação está em estado de erro, exclua-o e tente novamente.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Descrição**: Olá SubscriptionId *yourSubscriptionId* não tem o cluster de toocreate esquerdo núcleos *yourClusterName*. Obrigatório: *resourcesRequired*, Disponível: *resourcesAvailable*.  
* **Mitigação**: liberar recursos em sua assinatura ou aumentar a assinatura dos recursos de saudação toohello disponível e tente novamente o cluster de saudação toocreate.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Descrição**: ID de assinatura *yourSubscriptionId* não tem uma cota para um novo cluster toocreate HostedService *yourClusterName*.  
* **Mitigação**: liberar recursos em sua assinatura ou aumentar a assinatura dos recursos de saudação toohello disponível e tente novamente o cluster de saudação toocreate.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Descrição**: servidor de saudação encontrou um erro interno. Tente novamente a solicitação.  
* **Mitigação**: solicitação de saudação de repetição.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Descrição**: o local de armazenamento do Azure *dataRegionName* não é um local válido. Certifique-se de região hello está correto e repita a solicitação.
* **Mitigação**: selecione um local de armazenamento que oferece suporte ao HDInsight, verifique se o cluster está localizado e repita a operação de saudação.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Descrição**: o tamanho da VM é inválido para os nós de dados. Somente o tamanho 'VM Grande' tem suporte para todos os nós de dados.  
* **Mitigação**: especifique Olá suporte para tamanho de nó para nó de dados Olá e repita a operação de saudação.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Descrição**: o tamanho da VM é inválido para o nó de cabeçalho. Apenas o tamanho 'VM Extragrande' tem suporte para o nó de cabeçalho.  
* **Mitigação**: especificar tamanho de nó Olá tem suportada para o nó principal hello e repita a operação de saudação

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Descrição**: ID de assinatura *yourSubscriptionId* que está sendo usado não tem a operação de exclusão de tooexecute permissões suficientes para cluster *yourClusterName*.  
* **Mitigação**: se o cluster de saudação está em estado de erro, descarte-o e tente novamente.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Descrição**: o nome do contêiner de blob da conta de armazenamento externa *yourContainerName* é inválido. Verifique se o nome começa com uma letra e contém somente letras minúsculas, números e hífen.  
* **Mitigação**: Especifique um nome de contêiner de blob de conta de armazenamento válido e repita a operação de saudação.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Descrição**: configuração da conta de armazenamento externo de *yourStorageAccountName* é necessário toohave detalhes da chave de segredo toobe conjunto.  
* **Mitigação**: Especifique uma chave secreta válida para a conta de armazenamento hello e repita a operação de saudação.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Descrição**: a versão do cabeçalho *yourVersionHeader* não está no formato válido de aaaa-mm-dd.  
* **Mitigação**: especificar um formato válido para o cabeçalho de versão hello e repita a solicitação de saudação.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Descrição**: a configuração do cluster é inválida. Encontrada mais de uma configuração de nó de cabeçalho.  
* **Mitigação**: Editar configuração de saudação para que somente um nó principal for especificado.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Descrição**: não foi possível concluir a operação de saudação em Olá permitido tempo ou máximo de tentativas de saudação tentativas possíveis. Tente novamente a solicitação.  
* **Mitigação**: solicitação de saudação de repetição.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Descrição**: o parâmetro *yourParameterName* não pode ser nulo ou vazio.  
* **Mitigação**: Especifique um valor válido para o parâmetro hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Descrição**: um ou mais das entradas de solicitação de criação de cluster Olá não são válido. Verifique se os valores de entrada hello estão corretos e tente novamente a solicitação.  
* **Mitigação**: Verifique se os valores de entrada hello estão corretos e repita a solicitação.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Descrição**: a capacidade da região não está disponível para a região *seuNomeRegião* e a ID da Assinatura *suaIdAssinatura*.  
* **Atenuação**: especifique uma região que dê suporte a clusters HDInsight. regiões de saudação publicamente com suporte são: Sudeste da Ásia, Europa Ocidental, Norte da Europa, Leste dos EUA ou oeste dos EUA.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Descrição**: a conta de armazenamento *seuNomeContaArmazenamento* está na região *nomeRegiãoAtual*. Ele deve ser igual a região do cluster Olá *yourClusterRegionName*.  
* **Mitigação**: Especifique uma conta de armazenamento Olá mesma região que o cluster está em ou se seus dados já estão na conta de armazenamento hello, criar um novo cluster no hello mesma região da conta de armazenamento existente hello. Se você estiver usando o Portal de saudação, Olá da interface do usuário será notificado-los desse problema com antecedência.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Descrição**: a ID da assinatura *yourSubscriptionId* fornecida não está ativa.  
* **Atenuação**: reative sua assinatura ou obtenha uma nova assinatura válida.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Descrição**: a ID da assinatura *yourSubscriptionId* não pôde ser encontrada.  
* **Mitigação**: Verifique se a sua ID de assinatura é válida e repita a operação de saudação.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Descrição**: não é possível tooresolve DNS *yourDnsUrl*. Certifique-se de URL Olá totalmente qualificado para o ponto de extremidade de blob Olá é fornecido.  
* **Atenuação**: forneça uma URL de blob válida. Olá URL deve ser completamente válido, incluindo iniciar com *http://* e terminando em *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Descrição**: não é possível tooverify local do recurso *yourDnsUrl*. Certifique-se de URL Olá totalmente qualificado para o ponto de extremidade de blob Olá é fornecido.  
* **Atenuação**: forneça uma URL de blob válida. Olá URL deve ser completamente válido, incluindo iniciar com *http://* e terminando em *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Descrição**: a capacidade de versão não está disponível para a versão *versãoEspecificada* e a ID da Assinatura *suaIdAssinatura*.  
* **Mitigação**: escolha uma versão que está disponível e repita a operação de saudação.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Descrição**: não há suporte para a versão *specifiedVersion* .
* **Mitigação**: escolha uma versão com suporte e repita a operação de saudação.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Descrição**: a versão *versãoEspecificada* não está disponível na região do Azure *regiãoEspecificada*.  
* **Mitigação**: escolher uma versão com suporte na região de saudação especificado e repita a operação de saudação.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Descrição**: a configuração do cluster é inválida. Configuração da conta WASB necessária não encontrada em contas externas.  
* **Mitigação**: verificar se a conta de saudação existe e está especificada corretamente na operação de saudação de configuração e tente novamente.

## <a name="next-steps"></a>Próximas etapas
* [Usar exibições do Ambari toodebug Tez trabalhos no HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Habilitar despejos heap para serviços do Hadoop no HDInsight baseado em Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Gerenciar clusters HDInsight usando Olá Ambari Web UI](hdinsight-hadoop-manage-ambari.md)

