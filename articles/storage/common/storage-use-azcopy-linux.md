---
title: aaaCopy ou mover dados tooAzure armazenamento com AzCopy no Linux | Microsoft Docs
description: "Use Olá AzCopy Linux utilitário toomove ou copiar dados tooor do blob e o arquivo de conteúdo. Copiar dados tooAzure armazenamento de arquivos locais, ou copie dados dentro ou entre contas de armazenamento. Migre facilmente o armazenamento de tooAzure de dados."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Transferir dados com o AzCopy no Linux
AzCopy no Linux é um utilitário de linha de comando projetado para copiar dados tooand do armazenamento de BLOBs do Microsoft Azure e o arquivo usando comandos simples com um desempenho ideal. Você pode copiar dados de um tooanother de objeto dentro de sua conta de armazenamento, ou entre contas de armazenamento.

Há duas versões do AzCopy que podem ser baixadas. O AzCopy no Linux se baseia no .NET Core Framework, que se destina a plataformas Linux que oferecem opções de linha de comando no estilo POSIX. O [AzCopy no Windows](../storage-use-azcopy.md) se baseia no .NET Framework e oferece opções de linha de comando no estilo Windows. Este artigo aborda o AzCopy no Linux.

## <a name="download-and-install-azcopy"></a>Baixar e instalar o AzCopy
### <a name="installation-on-linux"></a>Instalação no Linux

AzCopy no Linux requer o framework .NET Core na plataforma de saudação. Consulte as instruções de instalação de saudação em Olá [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) página.

Como exemplo, vamos instalar o .NET Core no Ubuntu 16.10. Guia de instalação mais recente hello, visite [.NET Core no Linux](https://www.microsoft.com/net/core#linuxubuntu) página de instalação.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Depois de instalar o .NET Core, baixe e instale o AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Você pode remover arquivos de saudação extraído quando AzCopy no Linux está instalado. Como alternativa se você não tem privilégios de superusuário, você também pode executar AzCopy usando script de shell Olá 'azcopy' na pasta extraída hello. 

### <a name="alternative-installation-on-ubuntu"></a>Instalação alternativa no Ubuntu

**Ubuntu 14.04**

Adicionar fonte de apt ao .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Adicionar fonte de apt ao .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Adicionar fonte de apt ao .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Adicionar fonte de apt ao repositório de produtos do Linux da Microsoft e instale o AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Como escrever seu primeiro comando do AzCopy
Olá a sintaxe básica para comandos do AzCopy é:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Olá exemplos a seguir demonstram vários cenários para copiar dados tooand de Blobs do Microsoft Azure e arquivos. Consulte toohello `azcopy --help` menu para obter uma explicação detalhada de parâmetros de saudação usados em cada exemplo.

## <a name="blob-download"></a>Blob: baixar
### <a name="download-single-blob"></a>Baixar um único blob

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se pasta Olá `/mnt/myfiles` não existir, downloads e cria AzCopy `abc.txt ` na nova pasta de saudação.

### <a name="download-single-blob-from-secondary-region"></a>Baixe um único blob de região secundária

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.

### <a name="download-all-blobs"></a>Baixar todos os blobs

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Suponha seguinte Olá blobs residem no contêiner especificado hello:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Após a operação de download de Olá Olá diretório `/mnt/myfiles` inclui Olá seguintes arquivos:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Se você não especificar a opção `--recursive`, nenhum blob será baixado.

### <a name="download-blobs-with-specified-prefix"></a>Baixar blobs com prefixo especificado

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Suponha seguinte Olá blobs residem no contêiner especificado hello. Todos os blobs que começam com o prefixo Olá `a` são baixados.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Após a operação de download de Olá Olá pasta `/mnt/myfiles` inclui Olá seguintes arquivos:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

prefixo de saudação aplica diretório virtual toohello, que constitui Olá primeira parte do nome do blob hello. Exemplo hello mostrado acima, diretório virtual Olá não coincide com prefixo especificado de hello, para que nenhum blob é baixado. Além disso, se hello opção `--recursive` não for especificado, AzCopy não baixar todos os blobs.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Definir a hora da última modificação Olá dos arquivos exportados toobe mesmo Olá blobs de origem

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Você também pode excluir blobs de operação de download de saudação com base em sua hora da última modificação. Por exemplo, se você quiser blobs tooexclude cuja hora da última modificação é hello igual ou mais recente do que o arquivo de destino hello, adicionar Olá `--exclude-newer` opção:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Ou se você quiser blobs tooexclude cuja hora da última modificação é hello mesmo ou mais antigo que o arquivo de destino hello, adicione Olá `--exclude-older` opção:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Blob: carregar
### <a name="upload-single-file"></a>Carregar um único arquivo

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se Olá contêiner de destino especificado não existe, AzCopy cria e carregamentos Olá arquivo nele.

### <a name="upload-single-file-toovirtual-directory"></a>Carregar arquivo único diretório toovirtual

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se Olá especificado não existe um diretório virtual, AzCopy carrega Olá arquivo tooinclude Olá diretório virtual no nome do blob hello (*, por exemplo,*, `vd/abc.txt` no exemplo hello acima).

### <a name="upload-all-files"></a>Carregar todos os arquivos

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Especificando a opção `--recursive` carregamentos conteúdo Olá Olá especificado diretório tooBlob armazenamento recursivamente, que significa que todas as subpastas e seus arquivos são carregados também. Por exemplo, suponha que a seguir Olá arquivos residem na pasta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Após a operação de carregamento de saudação contêiner Olá inclui Olá seguintes arquivos:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Olá quando a opção `--recursive` não for especificado, somente hello seguintes três arquivos são carregados:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Carregar arquivos que correspondam ao padrão especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Suponha seguinte Olá arquivos residem na pasta `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Após a operação de carregamento de saudação contêiner Olá inclui Olá seguintes arquivos:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Olá quando a opção `--recursive` não for especificado, AzCopy ignora os arquivos que estão em subpastas:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Especifique o tipo de conteúdo MIME Olá de um blob de destino
Por padrão, AzCopy define Olá de tipo de conteúdo de um blob de destino muito`application/octet-stream`. No entanto, você pode especificar explicitamente o tipo de conteúdo Olá por meio da opção Olá `--set-content-type [content-type]`. Essa sintaxe define o tipo de conteúdo Olá para todos os blobs em uma operação de carregamento.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Se hello opção `--set-content-type` for especificado sem um valor, AzCopy define cada blob ou arquivo do tipo de conteúdo de acordo com tooits extensão de arquivo.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Blob: copiar
### <a name="copy-single-blob-within-storage-account"></a>Copiar um único blob dentro da conta de armazenamento

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.

### <a name="copy-single-blob-across-storage-accounts"></a>Copiar um único blob entre contas de armazenamento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Quando você copia um blob sem a opção --sync-copy, uma operação de [cópia no servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) é executada.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiar um único blob da região de tooprimary região secundária

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Observe que você deve ter um armazenamento com redundância geográfica e acesso de leitura habilitado.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiar um único blob e seus instantâneos entre contas de armazenamento

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Após a operação de cópia hello, o contêiner de destino Olá inclui Olá blob e seus instantâneos. Olá, contêiner inclui Olá seguinte blob e seus instantâneos:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copiar blobs em regiões entre contas de armazenamento de forma síncrona.
O AzCopy por padrão copia dados entre dois pontos de extremidade de armazenamento assincronamente. Portanto, as execuções de operação de cópia Olá no plano de fundo de saudação utilizando a capacidade de largura de banda sobressalente com nenhum SLA em termos de rapidez com que um blob é copiado. 

Olá `--sync-copy` opção garante que a operação de cópia de saudação obtém velocidade consistente. AzCopy executa cópia síncrona Olá ao baixar blobs Olá toocopy de saudação especificado fonte toolocal da memória e, em seguida, carregá-las toohello destino de armazenamento de Blob.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`pode gerar saída adicional em comparação de custo tooasynchronous cópia. Olá a abordagem recomendada é toouse essa opção em uma VM do Azure, que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.

## <a name="file-download"></a>Arquivo: baixar
### <a name="download-single-file"></a>Baixar um único arquivo

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se Olá especificado fonte for um compartilhamento de arquivos do Azure, você deve especificar nome de arquivo exatos Olá, (*, por exemplo,* `abc.txt`) toodownload um único arquivo, ou especifique a opção `--recursive` toodownload todos os arquivos no compartilhamento de saudação recursivamente. Tentativa de toospecify um padrão de arquivo e a opção `--recursive` juntos resulta em erro.

### <a name="download-all-files"></a>Baixar todos os arquivos

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Observe que as pastas vazias não são baixadas.

## <a name="file-upload"></a>Arquivo: carregar
### <a name="upload-single-file"></a>Carregar um único arquivo

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Carregar todos os arquivos

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Observe que as pastas vazias não são carregadas.

### <a name="upload-files-matching-specified-pattern"></a>Carregar arquivos que correspondam ao padrão especificado

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Arquivo: copiar
### <a name="copy-across-file-shares"></a>Copiar entre compartilhamentos de arquivos

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando você copia um arquivo entre compartilhamentos de arquivos, é executada uma operação [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiar de tooblob de compartilhamento de arquivo

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando você copia um arquivo de tooblob de compartilhamento de arquivo, uma [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.

### <a name="copy-from-blob-toofile-share"></a>Copiar de blob toofile compartilhamento

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando você copia um arquivo de compartilhamento de toofile de blob, um [cópia do servidor](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operação é executada.

### <a name="synchronously-copy-files"></a>Copiar arquivos de forma síncrona
Você pode especificar Olá `--sync-copy` opção toocopy dados do armazenamento de arquivo tooFile armazenamento, de armazenamento de arquivo tooBlob armazenamento e de armazenamento de Blob tooFile armazenamento de forma síncrona. AzCopy executa esta operação por memória de toolocal de dados de origem Olá o download e, em seguida, carregá-lo toodestination. Nesse caso, se aplica o custo de saída padrão.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Ao copiar do armazenamento de arquivo tooBlob armazenamento, tipo de blob saudação padrão é o blob de blocos, o usuário pode especificar a opção `/BlobType:page` toochange tipo de blob de destino de saudação.

Observe que `--sync-copy` pode gerar saída adicional comparando cópia de tooasynchronous de custo. Olá a abordagem recomendada é toouse essa opção em uma VM do Azure, que está em Olá mesma região que o custo de egresso fonte armazenamento conta tooavoid.

## <a name="other-azcopy-features"></a>Outros recursos do AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copiar somente os dados que não existem no destino de saudação
Olá `--exclude-older` e `--exclude-newer` parâmetros permitem que os recursos de origem mais antiga ou mais recente de tooexclude que está sendo copiado, respectivamente. Se você desejar somente toocopy os recursos de origem que não existem no destino Olá, você pode especificar ambos os parâmetros em Olá AzCopy comando:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Usar parâmetros de linha de comando do arquivo toospecify uma configuração

```azcopy
azcopy --config-file "azcopy-config.ini"
```

É possível incluir qualquer parâmetro de linha de comando do AzCopy em um arquivo de configuração. AzCopy processos Olá parâmetros no arquivo hello como se eles tivessem sido especificados na linha de comando hello, executar uma substituição direta com o conteúdo de saudação do arquivo hello.

Suponha que um arquivo de configuração chamado `copyoperation`, que contém Olá linhas a seguir. Cada parâmetro do AzCopy pode ser especificado em uma única linha.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

ou, em linhas separadas:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy falhará se você dividir o parâmetro hello em duas linhas, conforme mostrado aqui para Olá `--source-key` parâmetro:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Especificar uma SAS

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Você também pode especificar uma SAS no URI do contêiner hello:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Observe que AzCopy atualmente suporta apenas Olá [SAS conta](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Pasta de arquivo de diário
Cada vez que você emitir um comando tooAzCopy, ele verifica se um arquivo de diário existe na pasta padrão de hello, ou se ela existir em uma pasta que você especificou com esta opção. Se o arquivo de diário Olá não existir em qualquer lugar, AzCopy trata operação hello como novo e gera um novo arquivo de diário.

Se existir um arquivo de diário hello, o AzCopy verifica se o hello linha de comando que você inserir coincide com a saudação de linha de comando no arquivo de diário hello. Se duas linhas de comando Olá corresponder, AzCopy reinicia a operação de incompleta de saudação. Se eles não corresponderem, AzCopy solicita usuário tooeither substituir Olá diário arquivo toostart uma nova operação ou a operação atual do toocancel hello.

Se desejar que o local do toouse saudação padrão para o arquivo de diário hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Se você omitir a opção `--resume`, ou especifique a opção `--resume` sem o caminho da pasta hello, como mostrado acima, AzCopy cria o arquivo de diário Olá no local padrão de saudação, que é `~\Microsoft\Azure\AzCopy`. Se já existir um arquivo de diário Olá, AzCopy retoma operação Olá com base no arquivo de diário hello.

Se você desejar toospecify um local personalizado para o arquivo de diário hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Este exemplo cria o arquivo de diário Olá se ele ainda não existir. Se ele existir, AzCopy retoma operação Olá com base no arquivo de diário hello.

Se você desejar tooresume uma operação AzCopy, repita Olá mesmo comando. Em seguida, o AzCopy no Linux solicitará a confirmação:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Logs detalhados de saída

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Saudação de número de operações simultâneas toostart
Opção `--parallel-level` Especifica o número de saudação de operações simultâneas de cópia. Por padrão, AzCopy inicia um determinado número de operações simultâneas tooincrease Olá transferência de transferência de dados. saudação de número de operações simultâneas é igual Olá de oito vezes o número de processadores que você tem. Se você estiver executando o AzCopy através de uma rede de baixa largura de banda, você pode especificar um número mais baixo para - falhas no nível de paralelo tooavoid causado por divisão dos recursos.

[!TIP]
>lista completa de saudação tooview AzCopy parâmetros, check-out 'azcopy – Ajuda' menu.

## <a name="known-issues-and-best-practices"></a>Problemas conhecidos e melhores práticas
### <a name="error-net-core-is-not-found-in-hello-system"></a>Erro: O .NET Core não é encontrado no sistema de saudação.
Se você encontrar um erro informando que o núcleo do .NET não está instalado no sistema hello, Olá binário de .NET Core toohello caminho `dotnet` podem estar ausentes.

Em ordem tooaddress esse problema, localize o binário do .NET Core Olá no sistema de saudação:
```bash
sudo find / -name dotnet
```

Isso retorna Olá caminho toohello dotnet binário. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Agora, adicione essa variável de caminho de toohello de caminho. Sudo, edite secure_path toocontain Olá caminho toohello dotnet binário:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

Neste exemplo, a variável secure_path é:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Para o usuário atual do hello, editar.bash_profile/.profile tooinclude Olá caminho toohello dotnet binário na variável PATH 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Verifique se o .NET Core agora está em PATH:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Erro ao instalar o AzCopy
Se você tiver problemas com a instalação de AzCopy, você pode tentar toorun AzCopy usando scripts de bash Olá em Olá extraído `azcopy` pasta.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limite gravações simultâneas durante a cópia de dados
Quando você copia blobs ou arquivos com AzCopy, tenha em mente que outro aplicativo esteja modificando dados saudação enquanto você estiver copiando-lo. Se possível, certifique-se de que dados Olá que você está copiando não está sendo modificados durante a operação de cópia de saudação. Por exemplo, ao copiar um VHD associado a uma máquina virtual do Azure, certifique-se de que nenhum outro aplicativo no momento está escrevendo toohello VHD. Toodo uma boa maneira trata concedendo Olá recurso toobe copiado. Como alternativa, você pode criar um instantâneo de saudação VHD primeiro e copie instantâneo hello.

Se você não pode impedir que outros aplicativos gravando tooblobs ou arquivos enquanto eles estão sendo copiados, em seguida, tenha em mente que, pelo trabalho de Olá Olá tempo termina, hello recursos copiados não podem mais ter paridade completa com os recursos de origem hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Execute uma instância de AzCopy em um computador.
AzCopy é projetado toomaximize Olá utilização sua máquina recurso tooaccelerate Olá de transferência de dados, é recomendável executar apenas uma instância de AzCopy em um computador e especificar a opção Olá `--parallel-level` se você precisar de operações simultâneas mais. Para obter mais detalhes, digite `AzCopy --help parallel-level` na linha de comando hello.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o armazenamento do Azure e AzCopy, consulte Olá recursos a seguir:

### <a name="azure-storage-documentation"></a>Documentação do Armazenamento do Azure:
* [Introdução tooAzure armazenamento](../storage-introduction.md)
* [Criar uma conta de armazenamento](../storage-create-storage-account.md)
* [Gerenciar blobs com o Gerenciador de Armazenamento](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Usando Olá 2.0 do CLI do Azure com o armazenamento do Azure](../storage-azure-cli.md)
* [Como toouse armazenamento de Blob de C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse armazenamento de Blob do Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Como toouse armazenamento de Blob do Node. js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Como toouse armazenamento de Blob do Python](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Postagens de blog de armazenamento do Azure:
* [Anunciando a Versão Prévia do AzCopy no Linux](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Apresentando a versão de visualização da biblioteca de movimentação de dados do armazenamento do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: Introducing synchronous copy and customized content type (AzCopy: introdução a cópia síncrona e tipo de conteúdo personalizado)](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support (AzCopy: anúncio de disponibilidade geral do AzCopy 3.0 mais versão de teste do AzCopy 4.0 com suporte para Tabela e Arquivo)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: Optimized for Large-Scale Copy Scenarios (AzCopy: otimizado para cenários de cópia em larga escala)](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: Support for read-access geo-redundant storage (AzCopy: suporte para o armazenamento com redundância geográfica com acesso de leitura)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: Transferir dados com o modo reiniciável e um token SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: Using cross-account Copy Blob (AzCopy: usando blob de cópia em várias contas)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Uploading/downloading files for Azure Blobs (AzCopy: Upload/download de arquivos para Blobs do Azure)](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

