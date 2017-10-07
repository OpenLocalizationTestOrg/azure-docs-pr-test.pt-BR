---
title: "aaaTutorial - Olá Use SDK de lote do Azure para Python | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do lote do Azure e criar uma solução simple usando Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Introdução ao Olá lote SDK para Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Conheça os fundamentos de saudação do [do Azure Batch] [ azure_batch] e hello [lote Python] [ py_azure_sdk] cliente discutir um pequeno aplicativo lote escrito em Python. Vamos examinar como duas amostras scripts use Olá lote serviço tooprocess uma carga de trabalho paralela em máquinas virtuais do Linux na nuvem hello e como eles interagem com [armazenamento do Azure](../storage/common/storage-introduction.md) para preparação de arquivo e de recuperação. Você vai aprender um fluxo de trabalho de aplicativo comuns em lotes e obter uma compreensão básica de Olá principais componentes do lote, como trabalhos, tarefas, pools de e nós de computação.

![Fluxo de trabalho da solução do Lote (básico)][11]<br/>

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha um conhecimento prático do Python e que esteja familiarizado com o Linux. Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá lote e serviços de armazenamento.

### <a name="accounts"></a>Contas
* **Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure][azure_free_account].
* **Conta do Lote**: quando você tiver uma assinatura do Azure, [crie uma conta do Lote do Azure](batch-account-create-portal.md).
* **Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Exemplo de código
tutorial de Python Olá [exemplo de código] [ github_article_samples] é uma saudação muitos exemplos de código do lote encontrados no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub. Você pode baixar todos os exemplos de saudação clicando **Clone ou download > baixar ZIP** na home page do repositório de hello, ou clicando em Olá [azure lote-exemplos master.zip] [ github_samples_zip]link de download direto. Depois de extrair o conteúdo de saudação do arquivo ZIP de saudação, scripts Olá dois para este tutorial são encontrados em Olá `article_samples` diretório:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Ambiente do Python
Olá toorun *python_tutorial_client.py* script de exemplo em sua estação de trabalho local, é necessário um **intérprete Python** compatível com a versão **2.7** ou **3.3 +**. script Hello foi testado no Linux e Windows.

### <a name="cryptography-dependencies"></a>dependências de criptografia
Você deve instalar dependências Olá Olá [criptografia] [ crypto] biblioteca, exigida pelo Olá `azure-batch` e `azure-storage` pacotes Python. Execute uma saudação após operações adequadas para sua plataforma, ou consulte toohello [instalação criptografia] [ crypto_install] detalhes para obter mais informações:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Se a instalação da Python 3.3 + no Linux, use equivalentes de python3 Olá dependências de Python Olá. Por exemplo, no Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Pacotes do Azure
Em seguida, instalar Olá **do Azure Batch** e **armazenamento do Azure** pacotes Python. Você pode instalar os dois pacotes usando **pip** e hello *requirements.txt* encontrado aqui:

`/azure-batch-samples/Python/Batch/requirements.txt`

Problema a seguir **pip** tooinstall Olá lote e armazenamento de pacotes de comando:

`pip install -r requirements.txt`

Ou, você pode instalar Olá [do azure batch] [ pypi_batch] e [armazenamento do azure] [ pypi_storage] Python pacotes manualmente:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Se você estiver usando uma conta sem privilégios, talvez seja necessário tooprefix seus comandos com `sudo`. Por exemplo: `sudo pip install -r requirements.txt`. Para saber mais sobre como instalar pacotes Python, veja [Installing Packages][pypi_install] (Instalando pacotes) em python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Exemplo de código do tutorial do Python do Lote
exemplo de tutorial código Python de lote Hello consiste em dois scripts Python e alguns arquivos de dados.

* **python_tutorial_client.py**: interage com tooexecute de serviços de lote e armazenamento Olá uma carga de trabalho paralela em nós de computação (máquinas virtuais). Olá *python_tutorial_client.py* script é executado na sua estação de trabalho local.
* **python_tutorial_task.py**: script hello executado em nós de computação no trabalho do Azure tooperform Olá real. No exemplo hello, *python_tutorial_task.py* analisa Olá texto em um arquivo baixado do armazenamento do Azure (arquivo de entrada hello). Em seguida, ele produz um arquivo de texto (arquivo de saída de hello) que contém uma lista de palavras de três principais Olá que aparecem no arquivo de entrada hello. Depois que ele cria o arquivo de saída de hello, *python_tutorial_task.py* carregamentos Olá arquivo tooAzure armazenamento. Isso disponibiliza download toohello script de cliente em execução em sua estação de trabalho. Olá *python_tutorial_task.py* script será executado em paralelo em vários nós de computação em Olá serviço de lote.
* **./Data/taskdata\*. txt**: esses arquivos de três texto fornecem entrada Olá para tarefas de saudação que são executados em Olá nós de computação.

Olá diagrama a seguir ilustra as operações primário Olá executadas pelos scripts de cliente e a tarefa de saudação. Esse fluxo de trabalho básico é típico de muitas soluções de computação criadas com o Lote. Embora não demonstra todos os recursos disponíveis no serviço de lote de hello, quase todos os cenários de lote incluem partes desse fluxo de trabalho.

![Fluxo de trabalho de exemplo do Lote][8]<br/>

[**Etapa 1.**](#step-1-create-storage-containers) Crie **contêineres** no Armazenamento de Blobs do Azure.<br/>
[**Etapa 2.**](#step-2-upload-task-script-and-data-files) Carregar toocontainers de arquivos de script e a entrada de tarefa.<br/>
[**Etapa 3.**](#step-3-create-batch-pool) Criar um **pool** do Lote.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Olá pool **StartTask** downloads Olá tarefa script (python_tutorial_task.py) toonodes ao entrarem pool hello.<br/>
[**Etapa 4.**](#step-4-create-batch-job) Crie um **trabalho** do Lote.<br/>
[**Etapa 5.**](#step-5-add-tasks-to-job) Adicionar **tarefas** toohello trabalho.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** tarefas de saudação são agendado tooexecute em nós.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Cada tarefa baixa seus dados de entrada do Armazenamento do Azure e então inicia a execução.<br/>
[**Etapa 6.**](#step-6-monitor-tasks) Monitore as tarefas.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Como as tarefas são concluídas, carregar seu dados de saída tooAzure armazenamento.<br/>
[**Etapa 7.**](#step-7-download-task-output) Baixe a saída da tarefa do Armazenamento.

Como mencionado, nem todas as soluções do Lote executam essas etapas exatas, e elas podem incluir muitas outras, mas este exemplo demonstra os processos comuns encontrados em uma solução do Lote.

## <a name="prepare-client-script"></a>Preparar o script de cliente
Antes de executar o exemplo hello, adicione suas credenciais de conta de armazenamento e de lote muito*python_tutorial_client.py*. Se você não tiver feito isso, abra o arquivo de saudação em seu favorito Olá editor e a atualização de linhas com as credenciais a seguir.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Você pode encontrar suas credenciais de conta de lote e armazenamento na folha da conta de saudação de cada serviço em Olá [portal do Azure][azure_portal]:

![As credenciais no portal de saudação do lote][9]
![credenciais de armazenamento no portal de saudação][10]<br/>

Olá seções a seguir, podemos analisar etapas Olá usadas pelo Olá scripts tooprocess uma carga de trabalho no serviço de lote de saudação. Recomendamos que você regularmente toorefer toohello scripts em seu editor enquanto você vai restantes de saudação do artigo hello.

Navegue toohello a seguinte linha no **python_tutorial_client.py** toostart com a etapa 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Etapa 1: Criar contêineres do Armazenamento
![Criar contêineres no Armazenamento do Azure][1]
<br/>

O Lote inclui suporte interno para a interação com o Armazenamento do Azure. Contêineres em sua conta de armazenamento fornecerá arquivos Olá necessários para tarefas de saudação que são executados em sua conta do lote. contêineres de saudação também fornecem um lugar toostore Olá dados da saída tarefas Olá produzem. primeiro Olá Olá *python_tutorial_client.py* script faz é criar três contêineres [armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md#blob-storage):

* **aplicativo**: este contêiner armazena script de Python Olá executado pelas tarefas de saudação *python_tutorial_task.py*.
* **entrada**: tarefas baixarão tooprocess de arquivos de dados de saudação do hello *entrada* contêiner.
* **saída**: quando tarefas concluir o processamento do arquivo de entrada, eles carregará Olá resultados toohello *saída* contêiner.

Em ordem toointeract com um armazenamento de conta e criar contêineres, usamos Olá [armazenamento do azure] [ pypi_storage] pacote toocreate um [BlockBlobService] [ py_blockblobservice] objeto - Olá "cliente blob". Em seguida, podemos criar três contêineres na conta de armazenamento hello usando o cliente do blob Olá.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Depois que criar contêineres de hello, aplicativo hello agora pode carregar arquivos de saudação que serão usados pelas tarefas de saudação.

> [!TIP]
> [Como toouse armazenamento de BLOBs do Azure do Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fornece uma boa visão geral de como trabalhar com contêineres de armazenamento do Azure e blobs. Como começar a trabalhar com o lote, ele deve ser superior Olá da sua lista de leitura.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Etapa 2: Carregar o script de tarefa e os arquivos de dados
![Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)][2]
<br/>

Operação, de carregamento no arquivo hello *python_tutorial_client.py* primeiro define coleções de **aplicativo** e **entrada** caminhos de arquivo que existem no computador local hello. Em seguida, ele carrega esses contêineres de toohello de arquivos que você criou na etapa anterior hello.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Usando a compreensão da lista, Olá `upload_file_to_container` função é chamada para cada arquivo em coleções de saudação e dois [ResourceFile] [ py_resource_file] coleções são preenchidas. Olá `upload_file_to_container` função é exibida abaixo:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
Um [ResourceFile] [ py_resource_file] fornece tarefas em lote com o arquivo de tooa URL Olá no armazenamento do Azure que é baixado tooa nó de computação para que essa tarefa seja executada. Olá [ResourceFile][py_resource_file]. **blob_source** propriedade especifica a URL completa do arquivo Olá Olá conforme ela existe no armazenamento do Azure. Olá URL também pode incluir uma assinatura de acesso compartilhado (SAS) que fornece acesso seguro toohello arquivo. A maioria dos tipos de tarefas do Lote tem uma propriedade *ResourceFiles* , incluindo:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Este exemplo não usa Olá JobPreparationTask ou tipos de tarefa JobReleaseTask, mas você pode ler mais sobre eles em [nós de computação de tarefas de preparação e conclusão de trabalho de execução em lote do Azure](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Assinatura de acesso compartilhado (SAS)
Assinaturas de acesso compartilhado são cadeias de caracteres que fornecem acesso seguro toocontainers e blobs no armazenamento do Azure. Olá *python_tutorial_client.py* script usa ambos os BLOBs e contêiner assinaturas de acesso compartilhado e demonstra como tooobtain esses compartilhado acessar cadeias de caracteres de assinatura de saudação serviço de armazenamento.

* **Assinaturas de acesso compartilhado de blob**: usa de StartTask do pool de saudação ao baixar arquivos de dados Olá tarefa script e a entrada do armazenamento de blob assinaturas de acesso compartilhado (consulte [etapa 3](#step-3-create-batch-pool) abaixo). Olá `upload_file_to_container` funcionar em *python_tutorial_client.py* contém código Olá que obtém a assinatura de acesso compartilhado de cada blob. Isso é feito chamando [BlockBlobService.make_blob_url] [ py_make_blob_url] no módulo de armazenamento de saudação.
* **Assinatura de acesso compartilhado do contêiner**: como cada tarefa termina o trabalho no nó de computação hello, ele carrega sua toohello do arquivo de saída *saída* contêiner no armazenamento do Azure. toodo, *python_tutorial_task.py* usa uma assinatura de acesso compartilhado do contêiner que fornece acesso de gravação toohello contêiner. Olá `get_container_sas_token` funcionar em *python_tutorial_client.py* obtém a assinatura de acesso compartilhado do contêiner hello, que é passada como tarefas de toohello um argumento de linha de comando. Etapa 5 de # [trabalho de tooa adicionar tarefas](#step-5-add-tasks-to-job), discute o uso de saudação do SAS do contêiner hello.

> [!TIP]
> Check-out da série de duas partes da saudação em assinaturas de acesso compartilhado, [parte 1: modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: criar e usar uma SAS com hello serviço Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn mais sobre como fornecer acesso seguro toodata em sua conta de armazenamento.
>
>

## <a name="step-3-create-batch-pool"></a>Etapa 3: Criar pool do Lote
![Criar um pool do Lote][3]
<br/>

Um **pool** do Lote é uma coleção de nós de computação (máquinas virtuais) nos quais o Lote executa as tarefas de um trabalho.

Depois que ele carrega Olá tarefa script e dados de arquivos toohello conta de armazenamento, *python_tutorial_client.py* inicia sua interação com o serviço de lote hello usando o módulo de lote Python hello. toodo, um [BatchServiceClient] [ py_batchserviceclient] é criada:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Em seguida, um conjunto de nós de computação é criado na conta do lote com uma chamada de saudação muito`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Quando você cria um pool, você define uma [PoolAddParameter] [ py_pooladdparam] que especifica as várias propriedades de pool de saudação:

* **ID** do pool de saudação (*id* - obrigatório)<p/>Como acontece com a maioria das entidades no Lote, seu novo pool deverá ter uma ID exclusiva em sua conta do Lote. Seu código refere-se usando sua ID do pool de toothis, e é assim que você identifica pool Olá no hello Azure [portal][azure_portal].
* **Número de nós de computação** (*target_dedicated* – obrigatório)<p/>Essa propriedade especifica como muitas máquinas virtuais devem ser implantados no pool de saudação. É importante toonote todas as contas de lote têm um padrão **cota** limites Olá inúmeros **núcleos** (e, portanto, nós de computação) em uma conta de lote. Você pode encontrar as cotas de padrão de saudação e instruções sobre como muito[aumentar cota](batch-quota-limit.md#increase-a-quota) (como o número máximo de saudação de núcleos em sua conta em lotes) em [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md). Se você estiver se perguntando "Por que meu pool não alcança mais do que X nós?", Essa cota de núcleos pode ser a causa de saudação.
* **Sistema operacional** para nós (*virtual_machine_configuration* **ou** *cloud_service_configuration* – obrigatório)<p/>Em *python_tutorial_client.py*, podemos criar um pool de nós do Linux usando um [VirtualMachineConfiguration][py_vm_config]. Olá `select_latest_verified_vm_image_with_node_agent_sku` funcionar em `common.helpers` simplifica o trabalho com [Marketplace de máquinas virtuais do Azure] [ vm_marketplace] imagens. Veja [Provisionar nós de computação do Linux em pools do Lote do Azure](batch-linux-nodes.md) para saber mais sobre o uso de imagens do Marketplace.
* **Tamanho de nós de computação** (*vm_size* – obrigatório)<p/>Já que estamos especificando nós do Linux para a nossa [VirtualMachineConfiguration][py_vm_config], especificamos um tamanho de VM (neste exemplo, `STANDARD_A1`) de [Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Novamente, veja [Provisionar nós de computação Linux em pools do Lote do Azure](batch-linux-nodes.md) para saber mais.
* **Iniciar tarefa** (*start_task* – não obrigatório)<p/>Juntamente com hello acima de propriedades de nó físico, você também pode especificar um [StartTask] [ py_starttask] para pool de saudação (não é necessário). Olá StartTask executa em cada nó como nó une pool Olá, e cada vez que um nó é reiniciado. Olá StartTask é especialmente útil para preparar nós de computação para execução de saudação de tarefas, como aplicativos de saudação que executam as tarefas de instalação.<p/>Neste aplicativo de exemplo, Olá StartTask copia arquivos de saudação que baixa de armazenamento (que é especificado por meio da saudação StartTask **resource_files** propriedade) do hello StartTask *dodiretóriodetrabalho* toohello *compartilhado* diretório que podem acessar todas as tarefas em execução no nó de saudação. Essencialmente, isso copia `python_tutorial_task.py` toohello diretório compartilhado em cada nó como nó Olá une pool hello, para que as tarefas que são executados no nó Olá podem acessá-lo.

Você pode perceber Olá chamada toohello `wrap_commands_in_shell` função auxiliar. Essa função usa um conjunto de comandos separados e cria uma única linha de comando apropriada para a propriedade de linha de comando da tarefa.

Também notável no trecho de código Olá acima é use Olá das duas variáveis de ambiente no hello **linha_de_comando** propriedade Olá StartTask: `AZ_BATCH_TASK_WORKING_DIR` e `AZ_BATCH_NODE_SHARED_DIR`. Cada nó de computação em um pool de lote é automaticamente configurado com diversas variáveis de ambiente que são tooBatch específico. Qualquer processo que é executado por uma tarefa tem acesso toothese as variáveis de ambiente.

> [!TIP]
> toofind mais informações sobre variáveis de ambiente Olá que estão disponíveis em nós de computação em um pool de lote, bem como informações sobre pastas de trabalho de tarefas, consulte **configurações de ambiente para tarefas** e **arquivos e diretórios**  em Olá [visão geral dos recursos do Azure Batch](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Etapa 4: Criar o trabalho do Lote
![Criar trabalho do Lote][4]<br/>

Um **trabalho** do Lote é uma coleção de tarefas associadas a um pool de nós de computação. tarefas de saudação em um trabalho executar em nós de computação do pool Olá associado.

Você pode usar um trabalho, não apenas para a organização e controle de tarefas em cargas de trabalho relacionadas, mas também para impor certas restrições – como Olá tempo de execução máximo para o trabalho de saudação (e, por extensão, suas tarefas) e a prioridade do trabalho em trabalhos de tooother de relação no hello conta do lote. No entanto, neste exemplo, o trabalho de saudação é associado apenas ao pool de saudação que foi criado na etapa &#3;. Nenhuma propriedade adicional será configurada.

Todos os trabalhos do Lotes estão associados a um pool específico. Essa associação indica quais nós executar tarefas do trabalho Olá no. Especificar o pool Olá usando Olá [PoolInformation] [ py_poolinfo] propriedade, conforme mostrado no trecho de código Olá abaixo.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Agora que um trabalho tiver sido criado, as tarefas são adicionadas tooperform trabalho de saudação.

## <a name="step-5-add-tasks-toojob"></a>Etapa 5: Adicionar tarefas toojob
![Adicionar tarefas toojob][5]<br/>
*(1) as tarefas são adicionadas toohello trabalho, tarefas de saudação (2) são agendado toorun em nós e tarefas de saudação (3) Baixar Olá tooprocess de arquivos de dados*

Lote **tarefas** são nós de computação Olá unidades individuais de trabalho que executam em hello. Uma tarefa tem uma linha de comando e executa os scripts de saudação ou executáveis que você especificar na linha de comando.

tooactually executar o trabalho, tarefas devem ser adicionadas tooa trabalho. Cada [CloudTask] [ py_task] é configurado com uma propriedade de linha de comando e [ResourceFiles] [ py_resource_file] (assim como acontece com StartTask do pool Olá) que Olá tarefa baixa toohello nó antes de sua linha de comando é executada automaticamente. Exemplo hello, cada tarefa processa apenas um arquivo. Portanto, sua coleção ResourceFiles contém um único elemento.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Quando eles acessar variáveis de ambiente, como `$AZ_BATCH_NODE_SHARED_DIR` ou executar um aplicativo não encontrado no nó de saudação `PATH`, linhas de comando da tarefa deve chamar hello shell explicitamente, como com `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Esse requisito é desnecessário se suas tarefas de executar um aplicativo no nó de saudação `PATH` e não referenciam as variáveis de ambiente.
>
>

Dentro de saudação `for` loop no trecho de código Olá acima, você pode ver que a linha de comando Olá para tarefa de saudação é construída com cinco argumentos de linha de comando que são passados muito*python_tutorial_task.py*:

1. **FilePath**: Este é o arquivo de toohello de caminho local do hello existente no nó de saudação. Olá quando o objeto ResourceFile no `upload_file_to_container` foi criado na etapa 2 acima, o nome do arquivo hello foi usado para esta propriedade (Olá `file_path` parâmetro no construtor de ResourceFile Olá). Isso indica que esse arquivo hello pode ser encontrado no hello mesmo diretório no nó hello como *python_tutorial_task.py*.
2. **NUMWORDS**: superior Olá *N* palavras devem ser escritas toohello arquivo de saída.
3. **storageaccount**: nome de saudação do hello conta de armazenamento que possui a saída da tarefa Olá Olá contêiner toowhich deve ser carregado.
4. **storagecontainer**: nome de saudação do Olá Olá de toowhich do contêiner de armazenamento de saída de arquivos devem ser carregados.
5. **sastoken**: assinatura de acesso compartilhado da saudação (SAS) que fornece acesso de gravação toohello **saída** contêiner no armazenamento do Azure. Olá *python_tutorial_task.py* script usa essa assinatura de acesso compartilhado quando cria sua referência BlockBlobService. Isso fornece acesso de gravação toohello contêiner sem a necessidade de uma chave de acesso para a conta de armazenamento hello.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Etapa 6: Monitorar tarefas
![Monitorar tarefas][6]<br/>
*Olá tarefas de saudação do script monitores (1) para o status de conclusão e tarefas (2) Olá carregar dados de resultado tooAzure armazenamento*

Quando tarefas são adicionadas tooa trabalho, eles são automaticamente na fila e agendados para execução em nós de computação no pool de saudação associado ao trabalho hello. Com base nas configurações de saudação que você especificar, lote trata enfileiramento de mensagens todas as tarefas, agendamento, repetir e outras tarefas de administração de tarefa para você.

Há muitas abordagens toomonitoring a execução da tarefa. Olá `wait_for_tasks_to_complete` funcionar em *python_tutorial_client.py* fornece um exemplo simples de tarefas de monitoramento para um determinado estado, nesse caso, hello [concluída] [ py_taskstate] estado.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Etapa 7: Baixar a saída da tarefa
![Baixar a saída da tarefa do Armazenamento][7]<br/>

Agora que hello trabalho é concluído, saída de hello das tarefas de saudação pode ser baixada do armazenamento do Azure. Isso é feito com uma chamada muito`download_blobs_from_container` na *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Olá chamada muito`download_blobs_from_container` na *python_tutorial_client.py* Especifica que arquivos Olá devem ser o diretório base tooyour baixado. Sinta-se livre toomodify este local de saída.
>
>

## <a name="step-8-delete-containers"></a>Etapa 8: Excluir contêineres
Como você é cobrado pelos dados que residem no armazenamento do Azure, é sempre tooremove uma boa ideia que todos os blobs que não é mais necessário para seus trabalhos em lotes. Em *python_tutorial_client.py*, isso é feito com três chamadas muito[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Etapa 9: Excluir trabalho hello e pool Olá
Na etapa final do hello, você está toodelete solicitadas Olá trabalho Olá pool e que foram criados pelo Olá *python_tutorial_client.py* script. Embora você não seja cobrado pelos trabalhos e pelas tarefas, *será* cobrado pelos nós de computação. Portanto, recomendamos que você aloque os nós conforme necessário. A exclusão de pools não utilizados pode fazer parte de seu processo de manutenção.

Olá BatchServiceClient [JobOperations] [ py_job] e [PoolOperations] [ py_pool] têm métodos correspondentes de exclusão, que são chamado se Confirmar exclusão:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Tenha em mente que você será cobrado pelos recursos de computação, a exclusão dos pools não utilizados reduzirá o custo. Além disso, esteja ciente que a exclusão do pool de exclui todos os nós de computação no pool, e que os dados em nós hello serão irrecuperáveis depois Olá pool é excluído.
>
>

## <a name="run-hello-sample-script"></a>Execute o script de exemplo hello
Quando você executa Olá *python_tutorial_client.py* script tutorial Olá [exemplo de código][github_article_samples], saída do console Olá é a seguir toohello semelhante. Há uma pausa em `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` enquanto nós de computação do pool de saudação são criados, iniciado, e comandos Olá na tarefa de início do pool de saudação são executados. Saudação de uso [portal do Azure] [ azure_portal] toomonitor seu pool, nós de computação, trabalhos e tarefas durante e após a execução. Saudação de uso [portal do Azure] [ azure_portal] ou hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview Olá os recursos de armazenamento (contêineres e blobs) que são criados pelo aplicativo hello.

> [!TIP]
> Executar Olá *python_tutorial_client.py* script de dentro de saudação `azure-batch-samples/Python/Batch/article_samples` directory. Ele usa um caminho relativo para Olá `common.helpers` importação do módulo, para que você pode ver `ImportError: No module named 'common'` se você não executar o script de saudação do dentro dessa pasta.
>
>

Tempo de execução típico é **cerca de 5 a 7 minutos** quando você executar o exemplo hello em sua configuração padrão.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Próximas etapas
Sinta-se livre toomake alterações muito*python_tutorial_client.py* e *python_tutorial_task.py* tooexperiment com diferentes cenários de computação. Por exemplo, tente adicionar um atraso de execução muito*python_tutorial_task.py* toosimulate demoradas tarefas e monitorá-los no portal de saudação. Tente adicionar mais tarefas ou ajustar Olá número de nós de computação. Adicionar lógica toocheck para e permitir o uso de saudação de um tempo de execução toospeed pool existente.

Agora que você está familiarizado com o fluxo de trabalho básico de uma solução de lote Olá, é hora toodig em toohello de recursos adicionais do serviço de lote de saudação.

* Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.
* Início na Olá outros artigos de desenvolvimento de lote em **desenvolvimento detalhado** em Olá [de aprendizado em lotes][batch_learning_path].
* Check-out de uma implementação de processamento de carga de trabalho do hello "top N palavras" com o lote em Olá [TopNWords] [ github_topnwords] exemplo.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Criar contêineres no Armazenamento do Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Toocontainers de arquivos de tarefa de carregamento de aplicativo e de entrada (dados)"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Criar pool do Lote"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Criar trabalho em lotes"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Adicionar tarefas toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorar tarefas"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Baixar a saída da tarefa do Armazenamento"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Fluxo de trabalho da solução do Lote (diagrama completo)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Credenciais do Lote no Portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Credenciais do Armazenamento no Portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Fluxo de trabalho da solução do Lote (diagrama mínimo)"
