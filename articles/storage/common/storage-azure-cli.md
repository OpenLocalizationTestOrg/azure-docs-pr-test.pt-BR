---
title: "Olá aaaUsing 2.0 do CLI do Azure com o armazenamento do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure Interface de linha de comando (CLI do Azure) 2.0 com toocreate de armazenamento do Azure e gerencie contas de armazenamento e trabalhar com arquivos e blobs do Azure. Olá 2.0 do CLI do Azure é uma ferramenta de plataforma cruzada escrita em Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Usando Olá 2.0 do CLI do Azure com o armazenamento do Azure

Olá código-fonte, a plataforma cruzada do Azure CLI 2.0 fornece um conjunto de comandos para trabalhar com hello plataforma Windows Azure. Ele fornece grande parte da saudação mesma funcionalidade encontrada no hello [portal do Azure](https://portal.azure.com), incluindo o acesso de dados avançados.

Neste guia, mostramos como Olá toouse [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform várias tarefas trabalhando com recursos em sua conta de armazenamento do Azure. É recomendável baixar e instalar ou atualizar a versão mais recente toohello de saudação CLI 2.0 antes de usar este guia.

exemplos de saudação guia Olá assumem uso Olá Olá shell Bash no Ubuntu, mas outras plataformas devem ser executadas da mesma forma. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este guia pressupõe que você entender os conceitos básicos de saudação do armazenamento do Azure. Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá serviço de armazenamento.

### <a name="accounts"></a>Contas
* **Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure](https://azure.microsoft.com/free/).
* **Conta de armazenamento**: veja [Criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Instalar Olá 2.0 do CLI do Azure

Baixe e instale o hello Azure CLI 2.0 seguindo as instruções Olá descritas no [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Se você tiver problemas com a instalação Olá, confira Olá [solução de problemas de instalação](/cli/azure/install-az-cli2#installation-troubleshooting) seção do artigo hello e hello [instalar de solução de problemas](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guia no GitHub.
>

## <a name="working-with-hello-cli"></a>Trabalhando com hello CLI

Depois de instalar a saudação CLI, você pode usar o hello `az` comando em seus comandos de CLI do Azure de saudação de tooaccess de interface de linha de comando (Bash, Terminal, Prompt de comando). Saudação de tipo `az` toosee comando uma lista completa de comandos de base hello (Olá saída de exemplo a seguir foi truncada):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

Na sua interface de linha de comando, execute o comando Olá `az storage --help` Olá toolist `storage` subgrupos de comando. descrições de saudação de subgrupos de saudação fornecem uma visão geral da saudação de funcionalidade Olá que CLI do Azure fornece para trabalhar com seus recursos de armazenamento.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Conecte-se Olá CLI tooyour assinatura do Azure

toowork com recursos de saudação na sua assinatura do Azure, você deve primeiro fazer logon no tooyour conta do Azure com `az login`. Há várias maneiras de fazer logon:

* **Logon Interativo**: `az login`
* **Faça logon com o nome de usuário e senha**: `az login -u johndoe@contoso.com -p VerySecret`
  * Isso não funciona com contas da Microsoft ou contas que usam autenticação multifator.
* **Faça logon com uma entidade de serviço**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Script de exemplo da CLI do Azure 2.0

Em seguida, trabalharemos com um script de shell pequeno que emite alguns toointeract básica de comandos 2.0 do CLI do Azure com recursos de armazenamento do Azure. script Hello primeiro cria um novo contêiner na conta de armazenamento, em seguida, carrega um contêiner existente de toothat de arquivo (como um blob). Ele listará todos os blobs no contêiner Olá e por fim, baixa Olá arquivo tooa de destino no computador local que você especificar.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configurar e executar o script hello**

1. Abra o editor de texto favorito, copiar e colar Olá precede o script no editor de saudação.

2. Em seguida, atualize as configurações de tooreflect de variáveis do script hello. Substitua Olá valores conforme especificado a seguir:

   * **\<storage_account_name\>**  nome de saudação da sua conta de armazenamento.
   * **\<storage_account_key\>**  chave de acesso primária ou secundária Olá para sua conta de armazenamento.
   * **\<container_name\>**  um nome hello novo toocreate de contêiner, como "azure-cli-exemplo-container".
   * **\<blob_name\>**  um nome para o blob de destino Olá no contêiner de saudação.
   * **\<file_to_upload\>**  Olá caminho toosmall arquivo no computador local, como "~ / images/HelloWorld.png".
   * **\<destination_file\>**  Olá o caminho do arquivo de destino, como "~ / downloadedImage.png".

3. Depois que você atualizou variáveis necessárias Olá, Salvar script hello e sair de seu editor. as próximas etapas Olá supõem nomear seu script **my_storage_sample.sh**.

4. Marque o script hello como executável, se necessário:`chmod +x my_storage_sample.sh`

5. Execute o script hello. Por exemplo, no Bash:`./my_storage_sample.sh`

Você deve ver saída semelhante toohello seguinte e Olá  **\<destination_file\>**  especificado no hello script deve aparecer no computador local.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Olá anterior de saída é em **tabela** formato. Você pode especificar qual saída formato toouse especificando Olá `--output` argumento em seus comandos de CLI ou definido globalmente usando `az configure`.
>

## <a name="manage-storage-accounts"></a>Gerenciar contas de armazenamento

### <a name="create-a-new-storage-account"></a>Criar uma nova conta de armazenamento
toouse armazenamento do Azure, você precisa de uma conta de armazenamento. Você pode criar uma nova conta de armazenamento do Azure depois que você tiver configurado seu computador muito[conectar assinatura tooyour](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` [Obrigatório]: local. Por exemplo, “Oeste dos EUA”.
* `--name`[Obrigatório]: nome de conta de armazenamento hello. Olá nome deve ter 3 caracteres too24 e usar apenas caracteres alfanuméricos minúsculos.
* `--resource-group` [Obrigatório]: nome do grupo de recursos.
* `--sku`[Obrigatório]: Olá SKU de conta de armazenamento. Valores permitidos:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Definir as variáveis de ambiente da conta de armazenamento padrão do Azure
Você pode ter várias contas de armazenamento na sua assinatura do Azure. tooselect um deles toouse para armazenamento subsequentes todos os comandos, você pode definir essas variáveis de ambiente:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

É uma conta de armazenamento padrão tooset de outra forma usando uma cadeia de caracteres de conexão. Primeiro, obtenha a cadeia de caracteres de conexão de saudação com hello `show-connection-string` comando:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Em seguida, Olá de cópia de saída de cadeia de caracteres de conexão e defina Olá `AZURE_STORAGE_CONNECTION_STRING` variável de ambiente (talvez seja necessário tooenclose cadeia de conexão Olá entre aspas):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Todos os exemplos na Olá seções deste artigo a seguir pressupõem que você definiu Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` variáveis de ambiente.
>

## <a name="create-and-manage-blobs"></a>Criar e gerenciar blobs
Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Esta seção pressupõe que você esteja familiarizado com o conceitos de Armazenamento de Blobs do Azure. Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts) (Conceitos do serviço Blob).

### <a name="create-a-container"></a>Criar um contêiner
Todos os blobs no armazenamento do Azure devem residir em um contêiner. Você pode criar um contêiner usando Olá `az storage container create` comando:

```azurecli
az storage container create --name <container_name>
```

Você pode definir um dos três níveis de acesso de leitura para um novo contêiner especificando Olá opcional `--public-access` argumento:

* `off`(padrão): os dados do contêiner são privado toohello proprietário da conta.
* `blob`: acesso de leitura público para blobs.
* `container`: Leitura e listagem acesso toohello todo contêiner público.

Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Carregar um contêiner de blob tooa
O Armazenamento de Blobs do Azure dá suporte a blobs de blocos, anexos e páginas. Carregar blobs tooa contêiner usando Olá `blob upload` comando:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Por padrão, Olá `blob upload` comando carrega os blobs de toopage arquivos VHD ou outra forma de blobs de bloco. toospecify outro tipo quando você carregar um blob, você pode usar o hello `--type` argumento--os valores permitido são `append`, `block`, e `page`.

 Para obter mais informações sobre tipos de blob diferente hello, consulte [Compreendendo Blobs de bloco, Blobs de acréscimo e Blobs de página](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Baixar um blob de um contêiner
Este exemplo demonstra como toodownload um blob de um contêiner:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner

Listar blobs Olá em um contêiner com hello [lista de blob de armazenamento az](/cli/azure/storage/blob#list) comando.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Copiar blobs
É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.

Olá exemplo a seguir demonstra como blobs de toocopy do armazenamento de uma conta tooanother. Primeiro criamos um contêiner na conta de armazenamento de origem hello, especificando o acesso de leitura público para seus blobs. Em seguida, podemos carregar um contêiner de toohello de arquivo e, finalmente, copiar o blob de saudação do contêiner em um contêiner na conta de armazenamento de destino hello.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

Em Olá exemplo acima, o contêiner de destino Olá já deve existir na conta de armazenamento de destino Olá para Olá toosucceed de operação de cópia. Além disso, Olá blob de origem especificado no hello `--source-uri` argumento deve incluir um token de assinatura (SAS) de acesso compartilhado ou ser acessíveis publicamente, como neste exemplo.

### <a name="delete-a-blob"></a>Excluir um blob
toodelete um blob, use Olá `blob delete` comando:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Criar e gerenciar compartilhamentos de arquivos
Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam o protocolo de bloco de mensagens de servidor (SMB) saudação. As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados. Você pode gerenciar compartilhamentos de arquivos e dados de arquivo por meio de saudação CLI do Azure. Para obter mais informações sobre o armazenamento de arquivo do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../storage-dotnet-how-to-use-files.md) ou [como toouse armazenamento de arquivo do Azure com Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Criar um compartilhamento de arquivos
Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure. Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos. Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, se os limites de capacidade toohello Olá da conta de armazenamento. Olá, exemplo a seguir cria um compartilhamento de arquivos chamado **MeuCompartilhamento**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Criar um diretório
Um diretório fornece uma estrutura hierárquica para um compartilhamento de arquivos do Azure. Olá, exemplo a seguir cria um diretório chamado **myDir** no compartilhamento de arquivo hello.

```azurecli
az storage directory create --name myDir --share-name myshare
```

O caminho de um diretório pode incluir vários níveis, por exemplo **dir1/dir2**. No entanto, você deve garantir a existência de todos os diretórios pai antes de criar um subdiretório. Por exemplo, para o caminho **dir1/dir2**, você deve primeiro criar o diretório **dir1**, em seguida, criar o diretório **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Carregar um compartilhamento de arquivo local tooa
Olá, exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** tooroot de saudação **MeuCompartilhamento** compartilhamento de arquivos. Olá `--source` argumento especifica tooupload de arquivo local existente hello.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Assim como acontece com a criação de diretório, você pode especificar um caminho de diretório Dentro Olá compartilhamento tooupload Olá arquivo tooan diretório existente no compartilhamento de saudação:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Pode ser um arquivo no compartilhamento de saudação até too1 TB de tamanho.

### <a name="list-hello-files-in-a-share"></a>Listar Olá arquivos em um compartilhamento
Você pode listar arquivos e diretórios em um compartilhamento usando Olá `az storage file list` comando:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Copiar arquivos      
Você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob. Por exemplo, um arquivo tooa diretório em um compartilhamento diferente de toocopy:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Próximas etapas
Aqui estão alguns recursos adicionais para aprender mais sobre como trabalhar com hello 2.0 do CLI do Azure.

* [Introdução à CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Referência de comandos da CLI do Azure 2.0](/cli/azure)
* [CLI do Azure 2.0 no GitHub](https://github.com/Azure/azure-cli)
