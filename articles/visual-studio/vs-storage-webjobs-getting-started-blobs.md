---
title: "aaaGet de Introdução ao armazenamento de blob e o Visual Studio serviços conectados (projetos WebJob) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de Blob em um projeto do WebJob depois de se conectar tooan armazenamento do Azure usando o Visual Studio conectada a serviços."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Introdução ao armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos WebJob)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Este artigo fornece c# exemplos de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado. exemplos de código Olá usam Olá [SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x. Quando você adiciona um projeto WebJob de tooa de conta de armazenamento usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo, pacote de NuGet de armazenamento do Azure apropriado hello está instalado, referências de .NET apropriadas Olá são toohello adicionado projeto e cadeias de caracteres de conexão para a conta de armazenamento Olá são atualizadas no arquivo App. config de saudação.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Como tootrigger uma função quando um blob é criado ou atualizado
Esta seção mostra como Olá toouse **BlobTrigger** atributo.

 **Observação:** Olá toowatch de arquivos de log SDK do WebJobs verificações para blobs novos ou alterados. Esse processo é inerentemente lento; uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado.  Se seu aplicativo precisa tooprocess blobs imediatamente, Olá recomendado método é toocreate uma mensagem da fila ao criar blob hello e usar Olá [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo em vez da saudação **BlobTrigger** atributo na função hello processa blob hello.

### <a name="single-placeholder-for-blob-name-with-extension"></a>Espaço reservado único para nome de blob com extensão
Olá exemplo de código a seguir copia blobs de texto que aparecem no hello *entrada* contêiner toohello *saída* contêiner:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome do contêiner hello e um espaço reservado para nome do blob hello. Neste exemplo, se um blob denominado *Blob1.txt* é criado no hello *entrada* contêiner, a função hello cria um blob denominado *Blob1.txt* em Olá *saída*  contêiner.

Você pode especificar um padrão de nome com um espaço reservado para nome de blob hello, conforme mostrado no hello exemplo de código a seguir:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Esse código copia somente os blobs que têm nomes que começam com "original-". Por exemplo, *original Blob1.txt* em Olá *entrada* contêiner é copiado muito*cópia Blob1.txt* em Olá *saída* contêiner.

Se você precisar toospecify um padrão de nome para nomes de blob que têm chaves no nome hello, clique duas vezes chaves hello. Por exemplo, se você quiser toofind blobs Olá *imagens* contêiner que têm nomes como este:

        {20140101}-soundfile.mp3

Use o seguinte para o padrão:

        images/{{20140101}}-{name}

No exemplo hello, Olá *nome* seria o valor de espaço reservado *soundfile.mp3*.

### <a name="separate-blob-name-and-extension-placeholders"></a>Separar espaços reservados de nome de blob e extensão
Olá alterações de exemplo de código seguinte Olá extensão de arquivo como ele copia blobs que aparecem no hello *entrada* contêiner toohello *saída* contêiner. código Olá logs extensão Olá Olá *entrada* de blob e define a extensão de saudação do hello *saída* blob muito*. txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-tooblobs"></a>Tipos que você pode associar tooblobs
Você pode usar o hello **BlobTrigger** atributo Olá tipos a seguir:

* **string**
* **TextReader**
* **Fluxo**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Outros tipos desserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Se você desejar toowork diretamente com hello conta de armazenamento do Azure, você também pode adicionar uma **CloudStorageAccount** assinatura de método do parâmetro toohello.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Ao obter conteúdo de blob de texto por toostring de associação
Se os blobs de texto são esperados, **BlobTrigger** podem ser aplicada tooa **cadeia de caracteres** parâmetro. Olá, exemplo de código a seguir associa um tooa de blob de texto **cadeia de caracteres** parâmetro denominado **logMessage**. função Hello usa esse conteúdo parâmetro toowrite Olá Olá blob toohello painel do SDK do WebJobs.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder
Olá, exemplo de código a seguir usa uma classe que implementa **ICloudBlobStreamBinder** tooenable Olá **BlobTrigger** toobind toohello um blob de atributo **WebImage** tipo.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Olá **WebImage** código de associação é fornecido em um **WebImageBinder** classe que deriva de **ICloudBlobStreamBinder**.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-toohandle-poison-blobs"></a>Como os blobs de inviabilização toohandle
Quando um **BlobTrigger** função falhar, Olá SDK chamá-lo novamente, no caso de Olá falha foi causada por um erro transitório. Se a falha de saudação é causada por conteúdo de saudação do blob Olá, função hello falha toda vez que ele tenta tooprocess blob de saudação. Por padrão, a saudação SDK chama uma função too5 horas para um determinado blob. Se tentar quinto Olá falhar, Olá SDK adiciona uma fila de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*.

Olá o número máximo de repetições é configurável. Olá mesmo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuração é usada para o tratamento de blob suspeita e a manipulação de mensagens suspeitas de fila.

mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:

* FunctionId (no formato de saudação *{nome do trabalho Web}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" ou "PageBlob")
* ContainerName
* BlobName
* ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

Seguir Olá amostra de código, hello **CopyBlob** função tiver um código que faz com que ele toofail toda vez que ele é chamado. Depois de saudação SDK chamá-lo para o número máximo de saudação de novas tentativas, será criada uma mensagem na fila de blob suspeitas hello e essa mensagem é processada pelo Olá **LogPoisonBlob** função.

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Olá SDK automaticamente desserializa a mensagem de saudação do JSON. Aqui está a saudação **PoisonBlobMessage** classe:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Algoritmo de sondagem de blob
Olá SDK do WebJobs examina todos os contêineres especificados por **BlobTrigger** atributos no início do aplicativo. Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e as funções **BlobTrigger** sejam executadas.

toodetect blobs nova ou alterada após a inicialização do aplicativo, logs de saudação que SDK lê periodicamente saudação do armazenamento de blob. Olá blob logs são armazenados no buffer e obtenham fisicamente gravadas somente a cada 10 minutos ou assim, portanto pode haver um atraso significativo após um blob é criado ou atualizado antes da saudação correspondente **BlobTrigger** função é executada.

Há uma exceção para blobs que você cria usando Olá **Blob** atributo. Quando Olá SDK do WebJobs cria um novo blob, ele passa o novo blob de saudação imediatamente correspondência tooany **BlobTrigger** funções. Portanto, se você tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência. Porém, se você quiser que haja baixa latência ao executar as funções de processamento para blobs criados ou atualizados por outros meios, é recomendável usar **QueueTrigger** em vez de **BlobTrigger**.

### <a name="blob-receipts"></a>Recebimentos de blob
Olá SDK do WebJobs garante que nenhum **BlobTrigger** função é chamada mais de uma vez para Olá mesmo novo ou atualizado blob. Ele faz isso, mantendo *recebimentos de blob* em ordem toodetermine se uma versão de determinado blob tiver sido processada.

Recebimentos de blob são armazenados em um contêiner chamado *hosts de trabalhos Web do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de caracteres de conexão. Confirmação de blob tem Olá informações a seguir:

* Olá função que foi chamada para o blob de saudação ("*{nome do trabalho Web}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")
* nome do contêiner Olá
* tipo de blob Hello ("BlockBlob" ou "PageBlob")
* nome do blob Olá
* Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

Se você quiser tooforce reprocessamento de um blob, você poderá excluir manualmente a confirmação de blob de Olá para o blob de saudação *hosts de trabalhos Web do azure* contêiner.

## <a name="related-topics-covered-by-hello-queues-article"></a>Tópicos relacionados cobertos pelo artigo de filas de saudação
Para obter informações sobre como o processamento de blob toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não tooblob específico de processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Tópicos relacionados abordados nesse artigo incluem seguinte hello:

* Funções assíncronas
* Várias instâncias
* Desligamento normal
* Usar atributos de SDK do WebJobs no corpo de saudação de uma função
* Defina cadeias de caracteres de conexão do hello SDK no código.
* Definir valores para parâmetros do construtor do SDK WebJobs no código
* Configure **MaxDequeueCount** para tratamento de blob suspeito.
* Disparar uma função manualmente
* Gravar logs

## <a name="next-steps"></a>Próximas etapas
Este artigo fornece exemplos de código que mostram como blobs de cenários comuns de toohandle para trabalhar com o Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

