---
title: Como usar o armazenamento de blob do Azure com o SDK de Trabalhos Web
description: "Saiba como usar o armazenamento de blob do Azure com o SDK de Trabalhos Web. Dispare um processo quando um novo blob aparecer em um contêiner e identificador 'poison blobs'."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="8d89a-104">Como usar o armazenamento de blob do Azure com o SDK de Trabalhos Web</span><span class="sxs-lookup"><span data-stu-id="8d89a-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="8d89a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8d89a-105">Overview</span></span>
<span data-ttu-id="8d89a-106">Este guia fornece exemplos de código c# que mostram como disparar um processo quando um blob do Azure é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="8d89a-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="8d89a-107">Os exemplos de código usam o [SDK WebJobs](websites-dotnet-webjobs-sdk.md) versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="8d89a-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="8d89a-108">Para obter exemplos de código que mostram como criar blobs, consulte [Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8d89a-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="8d89a-109">Este guia pressupõe que você sabe [como criar um projeto WebJob no Visual Studio com cadeias de conexão que apontam para sua conta de armazenamento](websites-dotnet-webjobs-sdk-get-started.md) ou para [várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8d89a-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="8d89a-110"><a id="trigger"></a> Como disparar uma função quando um blob é criado ou atualizado</span><span class="sxs-lookup"><span data-stu-id="8d89a-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="8d89a-111">Esta seção mostra como usar o atributo `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="8d89a-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="8d89a-112">O SDK dos Trabalhos Web verifica os arquivos de log para observar blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="8d89a-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="8d89a-113">Esse processo não ocorre em tempo real; uma função não poderá ser disparada até vários minutos ou mais depois que o blob for criado.</span><span class="sxs-lookup"><span data-stu-id="8d89a-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="8d89a-114">Além disso, os [logs de armazenamento são criados com base nos "melhores esforços"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; não há nenhuma garantia de que todos os eventos serão capturados.</span><span class="sxs-lookup"><span data-stu-id="8d89a-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="8d89a-115">Sob algumas condições, logs poderão ser perdidos.</span><span class="sxs-lookup"><span data-stu-id="8d89a-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="8d89a-116">Se as limitações de velocidade e confiabilidade de gatilhos de blob não forem aceitáveis para o seu aplicativo, o método recomendado será criar uma mensagem de fila ao criar o blob e usar o atributo [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) em vez do atributo `BlobTrigger` na função que processa o blob.</span><span class="sxs-lookup"><span data-stu-id="8d89a-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="8d89a-117">Espaço reservado único para nome de blob com extensão</span><span class="sxs-lookup"><span data-stu-id="8d89a-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="8d89a-118">O seguinte exemplo de código copia blobs de texto que aparecem no contêiner de *entrada* para o contêiner de *saída*:</span><span class="sxs-lookup"><span data-stu-id="8d89a-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="8d89a-119">O construtor de atributo utiliza um parâmetro de cadeia de caracteres que especifica o nome do contêiner e um espaço reservado para o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="8d89a-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="8d89a-120">Neste exemplo, se um blob denominado *Blob1.txt* for criado no contêiner de *entrada*, a função criará um blob denominado *Blob1.txt* no contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="8d89a-121">Você pode especificar um padrão de nome com o espaço reservado de nome de blob, conforme é mostrado no seguinte exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="8d89a-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="8d89a-122">Esse código copia somente os blobs que têm nomes que começam com "original-".</span><span class="sxs-lookup"><span data-stu-id="8d89a-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="8d89a-123">Por exemplo, *original-Blob1.txt* no contêiner de *entrada* é copiado para *copy-Blob1.txt* no contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="8d89a-124">Se você precisar especificar um padrão de nome para nomes de blob que têm chaves no nome, duplique as chaves.</span><span class="sxs-lookup"><span data-stu-id="8d89a-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="8d89a-125">Por exemplo, para localizar blobs no contêiner *imagens* que têm nomes como este:</span><span class="sxs-lookup"><span data-stu-id="8d89a-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="8d89a-126">Use o seguinte para o padrão:</span><span class="sxs-lookup"><span data-stu-id="8d89a-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="8d89a-127">No exemplo, o valor do espaço reservado para *nome* seria *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="8d89a-128">Separar espaços reservados de nome de blob e extensão</span><span class="sxs-lookup"><span data-stu-id="8d89a-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="8d89a-129">O exemplo de código a seguir altera a extensão do arquivo à medida que ele copia blobs que aparecem no contêiner de *entrada* para o contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="8d89a-130">O código registra a extensão do blob de *entrada* e define a extensão do blob de *saída* como *.txt*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="8d89a-131"><a id="types"></a> Tipos que você pode associar a blobs</span><span class="sxs-lookup"><span data-stu-id="8d89a-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="8d89a-132">Você pode usar o atributo `BlobTrigger` nos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="8d89a-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="8d89a-133">Outros tipos desserializados por [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="8d89a-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="8d89a-134">Para trabalhar diretamente com a conta de Armazenamento do Azure, você também pode adicionar um parâmetro `CloudStorageAccount` à assinatura do método.</span><span class="sxs-lookup"><span data-stu-id="8d89a-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="8d89a-135">Para obter exemplos, veja o [código de associação de blob no repositório azure-webjobs-sdk no GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="8d89a-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="8d89a-136"><a id="string"></a> Obtendo o conteúdo do blob de texto associando à cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8d89a-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="8d89a-137">Se blobs de texto forem esperados, `BlobTrigger`  poderá ser aplicado a um parâmetro `string`.</span><span class="sxs-lookup"><span data-stu-id="8d89a-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="8d89a-138">O exemplo de código a seguir associa um blob de texto a um parâmetro `string` denominado `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="8d89a-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="8d89a-139">A função usa esse parâmetro para gravar o conteúdo do blob no painel do SDK de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="8d89a-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="8d89a-140"><a id="icbsb"></a> Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="8d89a-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="8d89a-141">O exemplo de código a seguir usa uma classe que implementa `ICloudBlobStreamBinder` para habilitar o atributo `BlobTrigger` para associar um blob ao tipo `WebImage`.</span><span class="sxs-lookup"><span data-stu-id="8d89a-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="8d89a-142">O código de associação `WebImage` é fornecido em uma classe `WebImageBinder` que é derivada de `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="8d89a-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="8d89a-143">Obtendo o caminho do blob para o blob de gatilho</span><span class="sxs-lookup"><span data-stu-id="8d89a-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="8d89a-144">Para obter o nome do contêiner e o nome do blob que disparou a função, inclua um parâmetro de cadeia de caracteres `blobTrigger` na assinatura da função.</span><span class="sxs-lookup"><span data-stu-id="8d89a-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="8d89a-145"><a id="poison"></a> Como manipular blobs suspeitos</span><span class="sxs-lookup"><span data-stu-id="8d89a-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="8d89a-146">Quando uma função `BlobTrigger` falha, o SDK a chama novamente, caso a falha tenha sido causada por um erro transitório.</span><span class="sxs-lookup"><span data-stu-id="8d89a-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="8d89a-147">Se a falha for causada pelo conteúdo do blob, a função falhará sempre que tentar processar o blob.</span><span class="sxs-lookup"><span data-stu-id="8d89a-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="8d89a-148">Por padrão, o SDK chama uma função até cinco vezes para um blob específico.</span><span class="sxs-lookup"><span data-stu-id="8d89a-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="8d89a-149">Se a quinta tentativa falhar, o SDK adicionará uma mensagem a uma fila denominada *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="8d89a-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="8d89a-150">O número máximo de novas tentativas é configurável.</span><span class="sxs-lookup"><span data-stu-id="8d89a-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="8d89a-151">A mesma [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) é usada para manipular blob suspeitos e manipular mensagens de filas suspeitas.</span><span class="sxs-lookup"><span data-stu-id="8d89a-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="8d89a-152">A mensagem da fila para blobs suspeitos é um objeto JSON que contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="8d89a-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="8d89a-153">FunctionId (no formato *{Nome do Trabalho Web}*.Functions.*{Nome da função}*, por exemplo: Trabalho Web1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="8d89a-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="8d89a-154">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="8d89a-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="8d89a-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="8d89a-155">ContainerName</span></span>
* <span data-ttu-id="8d89a-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="8d89a-156">BlobName</span></span>
* <span data-ttu-id="8d89a-157">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="8d89a-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="8d89a-158">No exemplo de código a seguir, a função `CopyBlob` tem código que faz com que ela falhe sempre que for chamada.</span><span class="sxs-lookup"><span data-stu-id="8d89a-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="8d89a-159">Depois que o SDK a chamar pelo número máximo de tentativas, será criada uma mensagem na fila de blobs suspeitos, e essa mensagem será processada pela função `LogPoisonBlob` .</span><span class="sxs-lookup"><span data-stu-id="8d89a-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="8d89a-160">O SDK automaticamente desserializa a mensagem JSON.</span><span class="sxs-lookup"><span data-stu-id="8d89a-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="8d89a-161">Aqui está a classe `PoisonBlobMessage` :</span><span class="sxs-lookup"><span data-stu-id="8d89a-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="8d89a-162"><a id="polling"></a> Algoritmo de sondagem de blob</span><span class="sxs-lookup"><span data-stu-id="8d89a-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="8d89a-163">O SDK de Trabalhos Web examina todos os contêineres especificados por atributos `BlobTrigger` ao iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d89a-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="8d89a-164">Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e funções `BlobTrigger` sejam executadas.</span><span class="sxs-lookup"><span data-stu-id="8d89a-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="8d89a-165">Para detectar blobs novos ou alterados após a inicialização do aplicativo, o SDK lê periodicamente dos logs do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="8d89a-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="8d89a-166">Os logs de blob são armazenados em buffer e são gravados fisicamente apenas a cada 10 minutos, aproximadamente. Portanto, pode haver um atraso significativo após um blob ser criado ou atualizado antes que a função `BlobTrigger` correspondente seja executada.</span><span class="sxs-lookup"><span data-stu-id="8d89a-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="8d89a-167">Há uma exceção para blobs que você cria usando o atributo `Blob` .</span><span class="sxs-lookup"><span data-stu-id="8d89a-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="8d89a-168">Quando o SDK de Trabalhos Web cria um novo blob, ele passa o novo blob imediatamente para quaisquer funções `BlobTrigger` correspondentes.</span><span class="sxs-lookup"><span data-stu-id="8d89a-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="8d89a-169">Portanto, se você tiver uma cadeia de entradas e saídas de blob, o SDK poderá processá-las com eficiência.</span><span class="sxs-lookup"><span data-stu-id="8d89a-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="8d89a-170">Porém, se você quer que haja baixa latência ao executar as funções de processamento de blob para blobs criados ou atualizados por outros meios, é recomendável usar `QueueTrigger` em vez de `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="8d89a-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="8d89a-171"><a id="receipts"></a> Recebimentos de blob</span><span class="sxs-lookup"><span data-stu-id="8d89a-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="8d89a-172">O SDK de Trabalhos Web garante que nenhuma função `BlobTrigger` seja chamada mais de uma vez para o mesmo blob novo ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="8d89a-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="8d89a-173">Ele faz isso mantendo *recebimentos de blob* para determinar se uma versão de determinado blob foi processada.</span><span class="sxs-lookup"><span data-stu-id="8d89a-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="8d89a-174">Os recebimentos de blob são armazenados em um contêiner denominado *azure-webjobs-hosts* na conta de armazenamento do Azure especificada pela cadeia de conexão AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="8d89a-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="8d89a-175">Um recebimento de blob tem as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8d89a-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="8d89a-176">A função que foi chamada para o blob ("*{Nome do Trabalho Web}*.Functions.*{Nome da função}*", por exemplo: "Trabalho Web1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="8d89a-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="8d89a-177">O nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="8d89a-177">The container name</span></span>
* <span data-ttu-id="8d89a-178">O tipo de blob ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="8d89a-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="8d89a-179">O nome do blob</span><span class="sxs-lookup"><span data-stu-id="8d89a-179">The blob name</span></span>
* <span data-ttu-id="8d89a-180">O ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="8d89a-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="8d89a-181">Para forçar o reprocessamento de um blob, você pode excluir manualmente o recebimento desse blob do contêiner *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="8d89a-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="8d89a-182"><a id="queues"></a>Tópicos relacionados abordados no artigo sobre filas</span><span class="sxs-lookup"><span data-stu-id="8d89a-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="8d89a-183">Para obter informações sobre como lidar com o processamento de blob disparado por uma mensagem da fila ou para cenários do SDK de Trabalhos Web não específicos do processamento de blob, consulte [Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="8d89a-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="8d89a-184">Os tópicos relacionados abordados neste artigo incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8d89a-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="8d89a-185">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="8d89a-185">Async functions</span></span>
* <span data-ttu-id="8d89a-186">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="8d89a-186">Multiple instances</span></span>
* <span data-ttu-id="8d89a-187">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="8d89a-187">Graceful shutdown</span></span>
* <span data-ttu-id="8d89a-188">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="8d89a-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="8d89a-189">Definir as cadeias de conexão do SDK no código.</span><span class="sxs-lookup"><span data-stu-id="8d89a-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="8d89a-190">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="8d89a-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="8d89a-191">Configurar `MaxDequeueCount` para manipulação de blobs suspeitos.</span><span class="sxs-lookup"><span data-stu-id="8d89a-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="8d89a-192">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="8d89a-192">Trigger a function manually</span></span>
* <span data-ttu-id="8d89a-193">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="8d89a-193">Write logs</span></span>

## <span data-ttu-id="8d89a-194"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d89a-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="8d89a-195">Este guia forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d89a-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="8d89a-196">Para obter mais informações sobre como usar os Trabalhos Web do Azure e o SDK de Trabalhos Web, consulte [Trabalhos Web do Azure – Recursos recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="8d89a-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

