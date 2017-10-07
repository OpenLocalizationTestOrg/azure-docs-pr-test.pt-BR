---
title: "Olá aaaUsing 1.0 da CLI do Azure com o armazenamento do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure Interface de linha de comando (CLI do Azure) 1.0 com toocreate de armazenamento do Azure e gerencie contas de armazenamento e trabalhar com arquivos e blobs do Azure. Olá CLI do Azure é uma ferramenta de plataforma cruzada"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Usando Olá 1.0 da CLI do Azure com o armazenamento do Azure

## <a name="overview"></a>Visão geral

Olá CLI do Azure fornece um conjunto de software livre, multiplataforma comandos para trabalhar com hello plataforma Azure. Ele fornece grande parte da saudação mesma funcionalidade encontrada no hello [portal do Azure](https://portal.azure.com) funcionalidade de acesso a dados também é tão avançados.

Neste guia, exploraremos como toouse [Azure Interface de linha de comando (CLI do Azure)](../cli-install-nodejs.md) tooperform uma variedade de tarefas de administração e desenvolvimento com o armazenamento do Azure. É recomendável baixar e instalar ou atualizar toohello CLI do Azure mais recentes antes de usar este guia.

Este guia pressupõe que você entender os conceitos básicos de saudação do armazenamento do Azure. Guia de saudação fornece vários scripts toodemonstrate uso Olá Olá CLI do Azure com o armazenamento do Azure. Ser tooupdate-se de que variáveis de script hello com base na sua configuração antes de executar cada script.

> [!NOTE]
> Guia de saudação fornece exemplos de comando e script de CLI do Azure Olá para contas de armazenamento clássicos. Consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o gerenciamento de recursos do Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) para comandos de CLI do Azure para contas de armazenamento do Gerenciador de recursos.
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Introdução ao armazenamento do Azure e hello CLI do Azure em 5 minutos
Nos exemplos deste guia, usamos o Ubuntu, mas outras plataformas de sistema operacional devem funcionar de forma semelhante.

**Novo tooAzure:** obter uma assinatura Microsoft Azure e uma conta da Microsoft associada à assinatura. Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).

Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.

**Depois de criar uma assinatura e conta do Microsoft Azure:**

1. Baixe e instale Olá CLI do Azure seguindo as instruções de saudação descrita em [instalação Olá CLI do Azure](../cli-install-nodejs.md).
2. Quando hello CLI do Azure foi instalado, você será capaz de toouse hello azure comando de comandos de CLI do Azure sua interface de linha de comando (Bash, Terminal, prompt de comando) tooaccess hello. Saudação de tipo _azure_ comando e você verá Olá saída a seguir.

    ![Saída de comando do Azure][Image1]
3. Na interface de linha de comando hello, digite `azure storage` toolist todas Olá comandos de armazenamento do azure e obter uma primeira impressão de saudação de funcionalidades Olá CLI do Azure fornece. Você pode digitar o nome de comando com **-h** parâmetro (por exemplo, `azure storage share create -h`) toosee detalhes da sintaxe de comando.
4. Agora, vamos dar um script simples que mostra tooaccess de comandos de CLI do Azure básico armazenamento do Azure. script Hello primeiro solicitará tooset duas variáveis para a conta de armazenamento e a chave. Em seguida, script hello criará um novo contêiner nessa nova conta de armazenamento e carregar um contêiner de toothat de (blob) do arquivo de imagem existente. Depois que o script hello lista todos os blobs nesse contêiner, ele baixará Olá imagem arquivo toohello diretório de destino que existe no computador local hello.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. No computador local, abra o editor de texto de sua preferência (vim, por exemplo). Digite hello acima script em seu editor de texto.
6. Agora, você precisa de variáveis de script hello tooupdate com base em suas definições de configuração.

   * **< Storage_account_name >** usar Olá considerando o nome do script hello ou digitar um novo nome para sua conta de armazenamento. **Importante:** nome Olá Olá da conta de armazenamento deve ser exclusivo no Azure. Ele também deve ter somente letras minúsculas!
   * **< storage_account_key >** chave de acesso de saudação da sua conta de armazenamento.
   * **< Container_name >** Use Olá considerando o nome do script hello ou digite um novo nome para seu contêiner.
   * **< Image_to_upload >** inserir uma imagem de tooa caminho no computador local, como: "~ / images/HelloWorld.png".
   * **< Destination_folder >** Enter um arquivos de toostore de diretório local do caminho tooa baixado do armazenamento do Azure, como: "~/downloadImages".
7. Depois que você atualizou variáveis necessárias de saudação em vim, pressionar combinações de teclas `ESC`, `:`, `wq!` toosave script de saudação.
8. toorun esse script, simplesmente tipo hello script nome de arquivo no console do hello bash. Depois que esse script é executado, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado. Olá captura de tela a seguir mostra um exemplo de saída:

Após a execução do script hello, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Gerenciar contas de armazenamento com hello CLI do Azure
### <a name="connect-tooyour-azure-subscription"></a>Conecte-se tooyour assinatura do Azure
Embora a maioria dos comandos de armazenamento Olá funcione sem uma assinatura do Azure, recomendamos que você tooconnect tooyour assinatura Olá CLI do Azure. tooconfigure Olá CLI do Azure toowork com sua assinatura, execute as etapas de saudação em [conectar tooan assinatura do Azure do hello CLI do Azure](../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Criar uma nova conta de armazenamento
toouse armazenamento do Azure, você precisará de uma conta de armazenamento. Depois de configurar sua assinatura do computador tooconnect tooyour, você pode criar uma nova conta de armazenamento do Azure.

```azurecli
azure storage account create <account_name>
```

nome de saudação da sua conta de armazenamento deve ter entre 3 e 24 caracteres de comprimento e usar números e letras minúsculas apenas.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Definir uma conta de armazenamento padrão do Azure nas variáveis de ambiente
Você pode ter várias contas de armazenamento na sua assinatura. Você pode escolher um deles e defini-la no hello variáveis de ambiente para todo o armazenamento Olá comandos no hello mesmo sessão. Isso permite que você toorun armazenamento de CLI do Azure Olá comandos sem especificar o armazenamento de saudação de conta e chave explicitamente.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Outra maneira tooset uma conta de armazenamento padrão está usando a cadeia de caracteres de conexão. Em primeiro lugar, obter cadeia de caracteres de conexão de saudação pelo comando:

```azurecli
azure storage account connectionstring show <account_name>
```

Copie a cadeia de caracteres de conexão de saída hello e defina-a como tooenvironment variável:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Criar e gerenciar blobs
Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS. Esta seção pressupõe que você já esteja familiarizado com conceitos de armazenamento de BLOBs do Azure hello. Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).

### <a name="create-a-container"></a>Criar um contêiner
Todos os blobs no armazenamento do Azure devem residir em um contêiner. Você pode criar um contêiner privado usando Olá `azure storage container create` comando:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**. tooprevent anônimo acessar tooblobs, Olá permissão parâmetro muito**Off**. Por padrão, o novo contêiner de saudação é particular e pode ser acessado somente pelo proprietário da conta hello. público anônimo tooallow leitura tooblob acessar os recursos, mas não toocontainer metadados ou toohello a lista de blobs no contêiner Olá, defina o parâmetro de permissão de saudação muito**Blob**. público completo tooallow leitura tooblob acessar os recursos, os metadados de contêiner e lista de saudação de blobs no contêiner de saudação, defina o parâmetro de permissão de saudação muito**contêiner**. Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas. Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).

blobs tooupload tooa contêiner, você pode usar o hello `azure storage blob upload`. Por padrão, esse comando carrega o blob de blocos de tooa Olá arquivos locais. tipo de saudação toospecify blob Olá, você pode usar Olá `--blobtype` parâmetro.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Baixar blobs de um contêiner
saudação de exemplo a seguir demonstra como toodownload blobs de um contêiner.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Copiar blobs
É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.

Olá exemplo a seguir demonstra como blobs de toocopy do armazenamento de uma conta tooanother. Neste exemplo, podemos criar um contêiner onde os blobs podem ser acessados pública e anonimamente.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

Neste exemplo, é executada uma cópia assíncrona. Você pode monitorar o status de saudação de cada operação de cópia executando Olá `azure storage blob copy show` operação.

Observe que Olá URL de origem fornecido para uma operação de cópia de saudação deve ser acessível publicamente ou incluir um token SAS (assinatura de acesso compartilhado).

### <a name="delete-a-blob"></a>Excluir um blob
toodelete um blob, use Olá comando abaixo:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Criar e gerenciar compartilhamentos de arquivos
Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam protocolo SMB padrão de saudação. As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados. Você pode gerenciar compartilhamentos de arquivos e dados de arquivo por meio de saudação CLI do Azure. Para obter mais informações sobre o armazenamento de arquivo do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](storage-dotnet-how-to-use-files.md) ou [como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Criar um compartilhamento de arquivos
Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure. Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos. Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, se os limites de capacidade toohello Olá da conta de armazenamento. Olá, exemplo a seguir cria um compartilhamento de arquivos chamado **MeuCompartilhamento**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Criar um diretório
Um diretório fornece uma estrutura hierárquica opcional para um compartilhamento de arquivos do Azure. Olá, exemplo a seguir cria um diretório chamado **myDir** no compartilhamento de arquivo hello.

```azurecli
azure storage directory create myshare myDir
```

Observe que esse caminho de diretório pode incluir vários níveis, *por exemplo*: **a/b**. No entanto, você deve garantir a existência de todos os diretórios pai. Por exemplo, para o caminho **a/b**, você deve criar o diretório **a** primeiro e, em seguida, o diretório **b**.

### <a name="upload-a-local-file-toodirectory"></a>Carregar um arquivo local toodirectory
Olá, exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** toohello **myDir** directory. Edite o caminho do arquivo hello para que ele aponte tooa de arquivo válido no computador local:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Observe que pode ser um arquivo no compartilhamento de saudação até too1 TB de tamanho.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Listar arquivos Olá na raiz do compartilhamento de saudação ou diretório
Você pode listar arquivos hello e subdiretórios em uma compartilhamento de raiz ou um diretório usando o comando a seguir de saudação:

```azurecli
azure storage file list myshare myDir
```

Observe que esse nome de diretório Olá é opcional para Olá operação de listagem. Se omitido, o comando de saudação lista conteúdo de saudação do diretório raiz de saudação do compartilhamento de saudação.

### <a name="copy-files"></a>Copiar arquivos
Começando com a versão 0.9.8 da CLI do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob. Abaixo, demonstraremos como tooperform esses copiam operações usando os comandos CLI. toocopy um novo diretório de arquivo toohello:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy um diretório de arquivo de blob tooa:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Próximas etapas

Você pode encontrar a referência de comandos da CLI 1.0 do Azure para trabalhar com recursos de Armazenamento aqui:

* [Comandos da CLI do Azure no modo Resource Manager](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Comandos da CLI do Azure no modo Gerenciamento de Serviços do Azure](../cli-install-nodejs.md)

Pode também desejar Olá tootry [2.0 do CLI do Azure](storage-azure-cli.md), nosso CLI de última geração escritos em Python, para uso com o modelo de implantação do Gerenciador de recursos de saudação.

[Image1]: ./media/storage-azure-cli/azure_command.png
