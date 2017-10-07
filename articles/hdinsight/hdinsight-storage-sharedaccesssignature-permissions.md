---
title: acesso de aaaRestrict usando assinaturas de acesso compartilhado - HDInsight do Azure | Microsoft Docs
description: Saiba como toouse assinaturas de acesso compartilhado toorestrict HDInsight acessar toodata armazenado em blobs de armazenamento do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Usar assinaturas de acesso compartilhado do Azure Storage toorestrict acesso toodata no HDInsight

HDInsight tem acesso completo toodata nas contas de armazenamento do Azure Olá associadas Olá cluster. Você pode usar assinaturas de acesso compartilhado em dados de toohello Olá blob contêiner toorestrict acesso. Por exemplo, tooprovide acesso somente leitura toohello dados. Assinaturas de acesso compartilhado (SAS) são um recurso de contas de armazenamento do Azure que permite que você toolimit toodata de acesso. Por exemplo, fornecendo acesso somente leitura toodata.

> [!IMPORTANT]
> Para uma solução que usa o Apache Ranger, considere usar HDInsight ingressado em domínio. Para obter mais informações, consulte Olá [configurar domínio HDInsight](hdinsight-domain-joined-configure.md) documento.

> [!WARNING]
> HDInsight deve ter acesso completo toohello padrão armazenamento Olá cluster.

## <a name="requirements"></a>Requisitos

* Uma assinatura do Azure
* C# ou Python. O código de exemplo do C# é fornecido como uma solução do Visual Studio.

  * A versão do Visual Studio deve ser a 2013, 2015 ou 2017
  * A versão do Python deverá ser a 2.7 ou superior

* Um cluster HDInsight baseados em Linux ou [Azure PowerShell] [ powershell] -se você tiver um cluster existente com base em Linux, você pode usar o Ambari tooadd um cluster de toohello de assinatura de acesso compartilhado. Caso contrário, você pode usar o Azure PowerShell toocreate um cluster e adicionar uma assinatura de acesso compartilhado durante a criação do cluster.

    > [!IMPORTANT]
    > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Olá arquivos de exemplo do [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Esse repositório contém Olá itens a seguir:

  * Um projeto do Visual Studio que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight
  * Um script Python que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight
  * Um script do PowerShell que pode criar um HDInsight de cluster e configurá-lo toouse Olá SAS.

## <a name="shared-access-signatures"></a>As Assinaturas de Acesso Compartilhado

Há duas formas de Assinaturas de Acesso Compartilhado:

* Ad hoc: Olá hora de início, hora de expiração e as permissões para Olá SAS são especificados no URI SAS de saudação.

* Política de acesso armazenada: uma política de acesso armazenada é definida em um contêiner de recurso, como um contêiner de blob. Uma política pode ser usado toomanage restrições para uma ou mais assinaturas de acesso compartilhado. Quando você associa uma SAS com uma política de acesso armazenada, Olá SAS herda restrições Olá - Olá hora de início, hora de expiração e permissões - definidas para a política de acesso Olá armazenado.

Olá diferença entre formulários Olá dois é importante para um cenário de chave: revogação. Uma SAS é uma URL, portanto qualquer pessoa que obtém Olá SAS pode usá-lo, independentemente de quem solicitou toobegin com. Se uma SAS é publicada publicamente, ele pode ser usado por qualquer pessoa no Olá, mundo. Uma SAS distribuída será válida até que ocorra um destes quatro fatores:

1. tempo de expiração de saudação especificado em Olá que SAS é atingido.

2. tempo de expiração de saudação especificado na política de acesso Olá armazenado referenciada por Olá que SAS é atingido. cenários a seguir Hello causam um tempo de expiração Olá toobe atingido:

    * intervalo de tempo de saudação expirou.
    * política de acesso de saudação armazenada é modificado toohave um tempo de expiração em Olá anterior. Alterar o tempo de expiração de saudação é uma maneira toorevoke Olá SAS.

3. Olá armazenado referenciada por Olá que SAS é excluído, que é Olá toorevoke de outra maneira SAS de política de acesso. Se você recriar a política de acesso de saudação armazenada com hello mesmo nome, todos os tokens SAS para diretiva anterior Olá são válidas (se o tempo de expiração saudação em Olá SAS não passou). Se você pretende toorevoke Olá SAS, ser toouse se um nome diferente se você recriar a política de acesso de saudação com um tempo de expiração em Olá futuras.

4. Olá a chave de conta que foi usado toocreate Olá SAS é regenerada. Regenerando chave Olá faz com que todos os aplicativos que usam a autenticação de chave toofail anterior hello. Atualize todos os componentes toohello nova chave.

> [!IMPORTANT]
> Um URI de assinatura de acesso compartilhado é associado à assinatura de Olá Olá conta chave toocreate usado e Olá associados a política de acesso armazenada (se houver). Se nenhuma política de acesso armazenada for especificada, hello toorevoke de maneira somente uma assinatura de acesso compartilhado é toochange Olá conta chave.

É recomendável sempre usar políticas de acesso armazenadas. Ao usar as diretivas armazenadas, você pode revogar assinaturas ou estender a data de expiração de saudação conforme necessário. Olá etapas deste documento usam políticas de acesso armazenada toogenerate SAS.

Para obter mais informações sobre assinaturas de acesso compartilhado, consulte [modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Criar uma política armazenada e uma SAS usando C\#

1. Abra a solução de saudação no Visual Studio.

2. No Gerenciador de soluções, clique com botão direito em Olá **SASToken** do projeto e selecione **propriedades**.

3. Selecione **configurações** e adicionar valores para Olá entradas a seguir:

   * StorageConnectionString: conexão Olá string hello conta de armazenamento que você deseja toocreate uma política armazenada e a SAS para. saudação de formato deve ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` onde `myaccount` é o nome da saudação da sua conta de armazenamento e `mykey` é chave Olá Olá conta de armazenamento.

   * ContainerName: contêiner de saudação na conta de armazenamento de saudação que você deseja toorestrict access.

   * SASPolicyName: Olá nome toouse para Olá armazenados toocreate de política.

   * FileToUpload: Olá caminho tooa arquivo que é carregado toohello contêiner.

4. Execute projeto hello. Informações toohello semelhante texto a seguir é exibida depois Olá SAS foi gerada:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Salve o token de política SAS Olá, nome da conta de armazenamento e nome do contêiner. Esses valores são usados ao associar a conta de armazenamento Olá seu cluster HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Criar uma política armazenada e uma SAS usando Python

1. Abrir o arquivo de SASToken.py hello e alterar Olá valores a seguir:

   * diretiva\_nome: Olá nome toouse para Olá armazenados toocreate de política.

   * armazenamento\_conta\_name: nome de saudação da sua conta de armazenamento.

   * armazenamento\_conta\_chave: Olá chave Olá conta de armazenamento.

   * armazenamento\_contêiner\_nome: contêiner de saudação na conta de armazenamento de saudação que você deseja toorestrict access.

   * exemplo\_arquivo\_caminho: Olá caminho tooa arquivo contêiner toohello carregado.

2. Execute o script hello. Ele exibe o saudação SAS token semelhante toohello texto a seguir quando Olá script é concluído:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Salve o token de política SAS Olá, nome da conta de armazenamento e nome do contêiner. Esses valores são usados ao associar a conta de armazenamento Olá seu cluster HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Usar Olá SAS com HDInsight

Ao criar um cluster HDInsight, você deverá especificar uma conta de armazenamento primária e, opcionalmente, poderá especificar contas de armazenamento adicionais. Ambos os métodos de adição de armazenamento exigem contas de armazenamento toohello acesso completo e contêineres que são usados.

toouse um contêiner de tooa de acesso de toolimit de assinatura de acesso compartilhado, adicione uma entrada personalizada toohello **site principal** configuração de cluster de saudação.

* Para **baseados no Windows** ou **baseados em Linux** clusters de HDInsight, você pode adicionar a entrada de saudação durante a criação de cluster usando o PowerShell.
* Para **baseados em Linux** clusters de HDInsight, alterar a configuração de saudação após a criação de cluster usando o Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Criar um cluster que usa Olá SAS

Um exemplo de como criar um cluster HDInsight que Olá usa SAS está incluído no hello `CreateCluster` diretório de repositório de saudação. toouse-lo, use Olá seguindo as etapas:

1. Olá abrir `CreateCluster\HDInsightSAS.ps1` do arquivo em um editor de texto e modifique Olá valores no início de saudação do documento de saudação a seguir.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Por exemplo, alterar `'mycluster'` toohello nome de cluster Olá você deseja toocreate. valores SAS Olá devem corresponder valores hello de etapas anteriores Olá ao criar uma conta de armazenamento e o token SAS.

    Depois que você tiver alterado os valores hello, salve arquivo hello.

2. Abra um novo prompt do Azure PowerShell. Se você não estiver familiarizado com o Azure PowerShell ou se não o tiver instalado, consulte [Instalar e configurar o Azure PowerShell][powershell].

1. No prompt de hello, use Olá comando tooauthenticate tooyour assinatura do Azure a seguir:

    ```powershell
    Login-AzureRmAccount
    ```

    Quando solicitado, faça logon com a conta Olá para sua assinatura do Azure.

    Se sua conta estiver associada a várias assinaturas do Azure, talvez seja necessário toouse `Select-AzureRmSubscription` tooselect assinatura de saudação desejar toouse.

4. No prompt de hello, altere diretórios toohello `CreateCluster` diretório que contém o arquivo de HDInsightSAS.ps1 hello. Em seguida, usar Olá após o script do comando toorun Olá

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Como Olá script é executado, ele registra prompt do PowerShell toohello saída enquanto cria recursos Olá contas de grupo e de armazenamento. Você está tooenter solicitada ao usuário Olá HTTP Olá cluster HDInsight. Essa conta é usada toosecure cluster de toohello de acesso HTTP/s.

    Se você estiver criando um cluster baseado em Linux, também será solicitado que você forneça um nome de conta de usuário SSH e uma senha. Essa conta é usado tooremotely login toohello cluster.

   > [!IMPORTANT]
   > Quando solicitado Olá HTTP/s ou SSH nome de usuário e senha, você deve fornecer uma senha que atenda a saudação critérios a seguir:
   >
   > * Deve ter pelo menos 10 caracteres de comprimento
   > * Deve conter pelo menos um dígito
   > * Deve conter pelo menos um caractere não alfanumérico
   > * Deve conter pelo menos uma letra maiúscula ou minúscula

Leva algum tempo para esse script toocomplete, normalmente em torno de 15 minutos. Quando o script de saudação é concluído sem erros, Olá cluster foi criado.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Usar Olá SAS com um cluster existente

Se você tiver um cluster existente com base em Linux, você pode adicionar Olá SAS toohello **site principal** configuração usando Olá etapas a seguir:

1. Abra Olá Ambari web da interface do usuário para seu cluster. endereço de saudação para essa página é https://YOURCLUSTERNAME.azurehdinsight.net. Quando solicitado, autentique toohello cluster usando o nome do administrador de saudação (administrador) e senha que você usou quando criar o cluster de saudação.

2. Olá lado esquerdo da interface da web hello Ambari, selecione **HDFS** e, em seguida, selecione Olá **configurações** guia no meio de saudação da página de saudação.

3. Selecione Olá **avançado** guia e, em seguida, role até encontrar hello **site personalizado core** seção.

4. Expanda Olá **site personalizado core** seção, em seguida, final de toohello de rolagem e selecione Olá **adicionar propriedade...**  link. A seguir Olá Use valores de saudação **chave** e **valor** campos:

   * **Chave**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Valor**: Olá SAS retornado por Olá aplicativo c# ou Python que você executou anteriormente

     Substituir **CONTAINERNAME** com o nome do contêiner de saudação usada com o aplicativo hello de c# ou SAS. Substituir **STORAGEACCOUNTNAME** com o nome de conta de armazenamento Olá usado.

5. Clique em Olá **adicionar** toosave nesse chave e valor e clique em Olá **salvar** botão toosave alterações de configuração de saudação. Quando solicitado, adicione uma descrição da alteração da saudação ("adicionar acesso de armazenamento SAS" por exemplo) e, em seguida, clique em **salvar**.

    Clique em **Okey** quando Olá alterações foram concluídas.

   > [!IMPORTANT]
   > Você deve reiniciar vários serviços para que Olá alteração entra em vigor.

6. No Olá Ambari web da interface do usuário, selecione **HDFS** na lista Olá Olá à esquerda e, em seguida, selecione **reiniciar todos os** de saudação **ações de serviço** suspensa lista saudação à direita. Quando solicitado, selecione **Ativar o modo de manutenção** e selecione __Conforme Reiniciar Todos".

    Repita esse processo para MapReduce2 e YARN.

7. Depois de reiniciar serviços hello, selecione cada uma e desabilitar o modo de manutenção de saudação **ações de serviço** lista suspensa.

## <a name="test-restricted-access"></a>Testar o acesso restrito

tooverify restringir o acesso, use Olá métodos a seguir:

* Para **baseados no Windows** clusters de HDInsight, use o cluster de toohello tooconnect área de trabalho remota. Para obter mais informações, consulte [se conectar usando o RDP de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Uma vez conectado, use Olá **Hadoop de linha de comando** ícone Olá desktop tooopen um prompt de comando.

* Para **baseados em Linux** clusters de HDInsight, usar SSH tooconnect toohello cluster. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Uma vez conectado toohello cluster, use Olá tooverify etapas que você pode somente leitura e a lista de itens na conta de armazenamento SAS Olá a seguir:

1. conteúdo de saudação toolist do contêiner hello, use Olá comando a seguir no prompt de saudação de: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Substituir **SASCONTAINER** com o nome de saudação do contêiner Olá criado para conta de armazenamento SAS de saudação. Substituir **SASACCOUNTNAME** com nome Olá Olá da conta de armazenamento usada para Olá SAS.

    lista de saudação inclui arquivo hello carregado quando o contêiner de saudação e a SAS foram criados.

2. Use Olá tooverify de comando que você pode ler o conteúdo de saudação do arquivo hello a seguir. Substituir saudação **SASCONTAINER** e **SASACCOUNTNAME** como na etapa anterior hello. Substituir **FILENAME** pelo nome de saudação do arquivo de saudação exibido no comando anterior hello:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Esse comando lista os conteúdos de saudação do arquivo hello.

3. Saudação de usar o sistema de arquivos local do comando toodownload Olá arquivo toohello a seguir:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Este comando downloads Olá tooa local arquivo denominado **Testfile**.

4. A seguir use Olá comando tooupload Olá arquivo local tooa novo arquivo denominado **testupload.txt** em Olá armazenamento SAS:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Você receberá um toohello semelhante mensagem texto a seguir:

        put: java.io.IOException

    Esse erro ocorre porque o local de armazenamento de saudação é leitura + lista. Use Olá seguindo os dados de saudação do comando tooput no armazenamento padrão da saudação para cluster hello, que é gravável:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Neste momento, Olá operação deve ser concluída com êxito.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="a-task-was-canceled"></a>Uma tarefa foi cancelada

**Sintomas**: ao criar um cluster usando o script do PowerShell hello, você pode receber Olá a seguinte mensagem de erro:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Causa**: este erro pode ocorrer se você usar uma senha de usuário de administração/HTTP Olá para cluster hello, ou (para clusters baseados em Linux) usuário SSH hello.

**Resolução**: Use uma senha que atenda a saudação critérios a seguir:

* Deve ter pelo menos 10 caracteres de comprimento
* Deve conter pelo menos um dígito
* Deve conter pelo menos um caractere não alfanumérico
* Deve conter pelo menos uma letra maiúscula ou minúscula

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como tooadd acesso limitado armazenamento tooyour cluster HDInsight, aprender toowork outras maneiras com dados em seu cluster:

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
