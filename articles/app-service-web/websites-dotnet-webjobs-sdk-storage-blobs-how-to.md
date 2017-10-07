---
title: aaaHow toouse armazenamento de BLOBs do Azure com hello SDK do WebJobs
description: "Saiba como toouse Azure blob storage com hello SDK do WebJobs. Dispare um processo quando um novo blob aparecer em um contêiner e identificador 'poison blobs'."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>Como toouse Azure blob storage com hello SDK do WebJobs
## <a name="overview"></a>Visão geral
Este guia fornece c# exemplos de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado. uso de exemplos de código de saudação [SDK do WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.

Para obter exemplos de código que mostram como toocreate blobs, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou muito[várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Como tootrigger uma função quando um blob é criado ou atualizado
Esta seção mostra como Olá toouse `BlobTrigger` atributo. 

> [!NOTE]
> Olá toowatch de arquivos de log SDK do WebJobs verificações para blobs novos ou alterados. Esse processo não está em tempo real; uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado. Além disso, os [logs de armazenamento são criados com base nos "melhores esforços"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; não há nenhuma garantia de que todos os eventos serão capturados. Sob algumas condições, logs poderão ser perdidos. Se Olá limitações de velocidade e a confiabilidade dos disparadores do blob não são aceitáveis para seu aplicativo, Olá recomendado método é toocreate uma mensagem da fila ao criar blob hello e usar Olá [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) de atributo, em vez de Olá `BlobTrigger` atributo na função hello processa blob hello.
> 
> 

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

## <a id="types"></a>Tipos que você pode associar tooblobs
Você pode usar o hello `BlobTrigger` atributo Olá tipos a seguir:

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* Outros tipos desserializados por [ICloudBlobStreamBinder](#icbsb) 

Se você desejar toowork diretamente com hello conta de armazenamento do Azure, você também pode adicionar um `CloudStorageAccount` a assinatura do método toohello parâmetro.

Para obter exemplos, consulte Olá [blob código de associação no repositório do sdk do azure webjobs Olá em GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Ao obter conteúdo de blob de texto por toostring de associação
Se os blobs de texto são esperados, `BlobTrigger` podem ser aplicada tooa `string` parâmetro. Olá, exemplo de código a seguir associa um tooa de blob de texto `string` parâmetro denominado `logMessage`. função Hello usa esse conteúdo parâmetro toowrite Olá Olá blob toohello painel do SDK do WebJobs. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder
Olá, exemplo de código a seguir usa uma classe que implementa `ICloudBlobStreamBinder` tooenable Olá `BlobTrigger` toobind toohello um blob de atributo `WebImage` tipo.

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

Olá `WebImage` código de associação é fornecido em um `WebImageBinder` classe que deriva de `ICloudBlobStreamBinder`.

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>Obter o caminho de blob Olá Olá disparo blob
nome do contêiner Olá tooget e nome de blob do blob de saudação que acionou a função hello, incluem um `blobTrigger` parâmetro na assinatura de função de saudação de cadeia de caracteres.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Como os blobs de inviabilização toohandle
Quando um `BlobTrigger` função falhar, Olá SDK chamá-lo novamente, no caso de Olá falha foi causada por um erro transitório. Se a falha de saudação é causada por conteúdo de saudação do blob Olá, função hello falha toda vez que ele tenta tooprocess blob de saudação. Por padrão, a saudação SDK chama uma função too5 horas para um determinado blob. Se tentar quinto Olá falhar, Olá SDK adiciona uma fila de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*.

Olá o número máximo de repetições é configurável. Olá mesmo [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuração é usada para o tratamento de blob suspeita e a manipulação de mensagens suspeitas de fila. 

mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:

* FunctionId (no formato de saudação *{nome do trabalho Web}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" ou "PageBlob")
* ContainerName
* BlobName
* ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

Seguir Olá amostra de código, hello `CopyBlob` função tiver um código que faz com que ele toofail toda vez que ele é chamado. Depois de saudação SDK chamá-lo para o número máximo de saudação de novas tentativas, será criada uma mensagem na fila de blob suspeitas hello e essa mensagem é processada pelo Olá `LogPoisonBlob` função. 

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

Olá SDK automaticamente desserializa a mensagem de saudação do JSON. Aqui está a saudação `PoisonBlobMessage` classe: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> Algoritmo de sondagem de blob
Olá SDK do WebJobs examina todos os contêineres especificados pelo `BlobTrigger` atributos no início do aplicativo. Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e funções `BlobTrigger` sejam executadas.

toodetect blobs nova ou alterada após a inicialização do aplicativo, logs de saudação que SDK lê periodicamente saudação do armazenamento de blob. Olá blob logs são armazenados no buffer e obtenham fisicamente gravadas somente a cada 10 minutos ou assim, portanto pode haver um atraso significativo após um blob é criado ou atualizado antes da saudação correspondente `BlobTrigger` função é executada. 

Há uma exceção para blobs que você cria usando Olá `Blob` atributo. Quando Olá SDK do WebJobs cria um novo blob, ele passa o novo blob de saudação imediatamente tooany correspondência `BlobTrigger` funções. Portanto, se você tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência. Porém, se você quer que haja baixa latência ao executar as funções de processamento de blob para blobs criados ou atualizados por outros meios, é recomendável usar `QueueTrigger` em vez de `BlobTrigger`.

### <a id="receipts"></a> Recebimentos de blob
Olá SDK do WebJobs garante que nenhum `BlobTrigger` função é chamada mais de uma vez para Olá mesmo novo ou atualizado blob. Ele faz isso, mantendo *recebimentos de blob* em ordem toodetermine se uma versão de determinado blob tiver sido processada.

Recebimentos de blob são armazenados em um contêiner chamado *hosts de trabalhos Web do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de caracteres de conexão. Confirmação de blob tem Olá informações a seguir:

* Olá função que foi chamada para o blob de saudação ("*{nome do trabalho Web}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")
* nome do contêiner Olá
* tipo de blob Hello ("BlockBlob" ou "PageBlob")
* nome do blob Olá
* Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")

Se você quiser tooforce reprocessamento de um blob, você poderá excluir manualmente a confirmação de blob de Olá para o blob de saudação *hosts de trabalhos Web do azure* contêiner.

## <a id="queues"></a>Tópicos relacionados cobertos pelo artigo de filas de saudação
Para obter informações sobre como o processamento de blob toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não tooblob específico de processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tópicos relacionados abordados nesse artigo incluem seguinte hello:

* Funções assíncronas
* Várias instâncias
* Desligamento normal
* Usar atributos de SDK do WebJobs no corpo de saudação de uma função
* Defina cadeias de caracteres de conexão do hello SDK no código.
* Definir valores para parâmetros do construtor do SDK WebJobs no código
* Configurar `MaxDequeueCount` para manipulação de blobs suspeitos.
* Disparar uma função manualmente
* Gravar logs

## <a id="nextsteps"></a> Próximas etapas
Este guia fornece exemplos de código que mostram como blobs de cenários comuns de toohandle para trabalhar com o Azure. Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

