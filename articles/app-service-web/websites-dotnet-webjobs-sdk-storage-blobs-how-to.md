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
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="dd182-104">Como toouse Azure blob storage com hello SDK do WebJobs</span><span class="sxs-lookup"><span data-stu-id="dd182-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="dd182-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dd182-105">Overview</span></span>
<span data-ttu-id="dd182-106">Este guia fornece c# exemplos de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="dd182-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="dd182-107">uso de exemplos de código de saudação [SDK do WebJobs](websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="dd182-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="dd182-108">Para obter exemplos de código que mostram como toocreate blobs, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="dd182-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="dd182-109">Guia de saudação pressupõe que você sabe [como toocreate um projeto do WebJob no Visual Studio com conexão cadeias de caracteres essa conta de armazenamento de ponto tooyour](websites-dotnet-webjobs-sdk-get-started.md) ou muito[várias contas de armazenamento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="dd182-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="dd182-110"><a id="trigger"></a>Como tootrigger uma função quando um blob é criado ou atualizado</span><span class="sxs-lookup"><span data-stu-id="dd182-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="dd182-111">Esta seção mostra como Olá toouse `BlobTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="dd182-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd182-112">Olá toowatch de arquivos de log SDK do WebJobs verificações para blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="dd182-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="dd182-113">Esse processo não está em tempo real; uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado.</span><span class="sxs-lookup"><span data-stu-id="dd182-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="dd182-114">Além disso, os [logs de armazenamento são criados com base nos "melhores esforços"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; não há nenhuma garantia de que todos os eventos serão capturados.</span><span class="sxs-lookup"><span data-stu-id="dd182-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="dd182-115">Sob algumas condições, logs poderão ser perdidos.</span><span class="sxs-lookup"><span data-stu-id="dd182-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="dd182-116">Se Olá limitações de velocidade e a confiabilidade dos disparadores do blob não são aceitáveis para seu aplicativo, Olá recomendado método é toocreate uma mensagem da fila ao criar blob hello e usar Olá [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) de atributo, em vez de Olá `BlobTrigger` atributo na função hello processa blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd182-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="dd182-117">Espaço reservado único para nome de blob com extensão</span><span class="sxs-lookup"><span data-stu-id="dd182-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="dd182-118">Olá exemplo de código a seguir copia blobs de texto que aparecem no hello *entrada* contêiner toohello *saída* contêiner:</span><span class="sxs-lookup"><span data-stu-id="dd182-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="dd182-119">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome do contêiner hello e um espaço reservado para nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd182-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="dd182-120">Neste exemplo, se um blob denominado *Blob1.txt* é criado no hello *entrada* contêiner, a função hello cria um blob denominado *Blob1.txt* em Olá *saída*  contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd182-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="dd182-121">Você pode especificar um padrão de nome com um espaço reservado para nome de blob hello, conforme mostrado no hello exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd182-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="dd182-122">Esse código copia somente os blobs que têm nomes que começam com "original-".</span><span class="sxs-lookup"><span data-stu-id="dd182-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="dd182-123">Por exemplo, *original Blob1.txt* em Olá *entrada* contêiner é copiado muito*cópia Blob1.txt* em Olá *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd182-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="dd182-124">Se você precisar toospecify um padrão de nome para nomes de blob que têm chaves no nome hello, clique duas vezes chaves hello.</span><span class="sxs-lookup"><span data-stu-id="dd182-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="dd182-125">Por exemplo, se você quiser toofind blobs Olá *imagens* contêiner que têm nomes como este:</span><span class="sxs-lookup"><span data-stu-id="dd182-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="dd182-126">Use o seguinte para o padrão:</span><span class="sxs-lookup"><span data-stu-id="dd182-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="dd182-127">No exemplo hello, Olá *nome* seria o valor de espaço reservado *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="dd182-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="dd182-128">Separar espaços reservados de nome de blob e extensão</span><span class="sxs-lookup"><span data-stu-id="dd182-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="dd182-129">Olá alterações de exemplo de código seguinte Olá extensão de arquivo como ele copia blobs que aparecem no hello *entrada* contêiner toohello *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd182-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="dd182-130">código Olá logs extensão Olá Olá *entrada* de blob e define a extensão de saudação do hello *saída* blob muito*. txt*.</span><span class="sxs-lookup"><span data-stu-id="dd182-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <span data-ttu-id="dd182-131"><a id="types"></a>Tipos que você pode associar tooblobs</span><span class="sxs-lookup"><span data-stu-id="dd182-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="dd182-132">Você pode usar o hello `BlobTrigger` atributo Olá tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd182-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

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
* <span data-ttu-id="dd182-133">Outros tipos desserializados por [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="dd182-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="dd182-134">Se você desejar toowork diretamente com hello conta de armazenamento do Azure, você também pode adicionar um `CloudStorageAccount` a assinatura do método toohello parâmetro.</span><span class="sxs-lookup"><span data-stu-id="dd182-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="dd182-135">Para obter exemplos, consulte Olá [blob código de associação no repositório do sdk do azure webjobs Olá em GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="dd182-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="dd182-136"><a id="string"></a>Ao obter conteúdo de blob de texto por toostring de associação</span><span class="sxs-lookup"><span data-stu-id="dd182-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="dd182-137">Se os blobs de texto são esperados, `BlobTrigger` podem ser aplicada tooa `string` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="dd182-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="dd182-138">Olá, exemplo de código a seguir associa um tooa de blob de texto `string` parâmetro denominado `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="dd182-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="dd182-139">função Hello usa esse conteúdo parâmetro toowrite Olá Olá blob toohello painel do SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="dd182-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="dd182-140"><a id="icbsb"></a> Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="dd182-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="dd182-141">Olá, exemplo de código a seguir usa uma classe que implementa `ICloudBlobStreamBinder` tooenable Olá `BlobTrigger` toobind toohello um blob de atributo `WebImage` tipo.</span><span class="sxs-lookup"><span data-stu-id="dd182-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

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

<span data-ttu-id="dd182-142">Olá `WebImage` código de associação é fornecido em um `WebImageBinder` classe que deriva de `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="dd182-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="dd182-143">Obter o caminho de blob Olá Olá disparo blob</span><span class="sxs-lookup"><span data-stu-id="dd182-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="dd182-144">nome do contêiner Olá tooget e nome de blob do blob de saudação que acionou a função hello, incluem um `blobTrigger` parâmetro na assinatura de função de saudação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="dd182-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="dd182-145"><a id="poison"></a>Como os blobs de inviabilização toohandle</span><span class="sxs-lookup"><span data-stu-id="dd182-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="dd182-146">Quando um `BlobTrigger` função falhar, Olá SDK chamá-lo novamente, no caso de Olá falha foi causada por um erro transitório.</span><span class="sxs-lookup"><span data-stu-id="dd182-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="dd182-147">Se a falha de saudação é causada por conteúdo de saudação do blob Olá, função hello falha toda vez que ele tenta tooprocess blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd182-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="dd182-148">Por padrão, a saudação SDK chama uma função too5 horas para um determinado blob.</span><span class="sxs-lookup"><span data-stu-id="dd182-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="dd182-149">Se tentar quinto Olá falhar, Olá SDK adiciona uma fila de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="dd182-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="dd182-150">Olá o número máximo de repetições é configurável.</span><span class="sxs-lookup"><span data-stu-id="dd182-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="dd182-151">Olá mesmo [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuração é usada para o tratamento de blob suspeita e a manipulação de mensagens suspeitas de fila.</span><span class="sxs-lookup"><span data-stu-id="dd182-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="dd182-152">mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd182-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="dd182-153">FunctionId (no formato de saudação *{nome do trabalho Web}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="dd182-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="dd182-154">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="dd182-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="dd182-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="dd182-155">ContainerName</span></span>
* <span data-ttu-id="dd182-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="dd182-156">BlobName</span></span>
* <span data-ttu-id="dd182-157">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="dd182-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="dd182-158">Seguir Olá amostra de código, hello `CopyBlob` função tiver um código que faz com que ele toofail toda vez que ele é chamado.</span><span class="sxs-lookup"><span data-stu-id="dd182-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="dd182-159">Depois de saudação SDK chamá-lo para o número máximo de saudação de novas tentativas, será criada uma mensagem na fila de blob suspeitas hello e essa mensagem é processada pelo Olá `LogPoisonBlob` função.</span><span class="sxs-lookup"><span data-stu-id="dd182-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="dd182-160">Olá SDK automaticamente desserializa a mensagem de saudação do JSON.</span><span class="sxs-lookup"><span data-stu-id="dd182-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="dd182-161">Aqui está a saudação `PoisonBlobMessage` classe:</span><span class="sxs-lookup"><span data-stu-id="dd182-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="dd182-162"><a id="polling"></a> Algoritmo de sondagem de blob</span><span class="sxs-lookup"><span data-stu-id="dd182-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="dd182-163">Olá SDK do WebJobs examina todos os contêineres especificados pelo `BlobTrigger` atributos no início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd182-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="dd182-164">Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e funções `BlobTrigger` sejam executadas.</span><span class="sxs-lookup"><span data-stu-id="dd182-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="dd182-165">toodetect blobs nova ou alterada após a inicialização do aplicativo, logs de saudação que SDK lê periodicamente saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="dd182-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="dd182-166">Olá blob logs são armazenados no buffer e obtenham fisicamente gravadas somente a cada 10 minutos ou assim, portanto pode haver um atraso significativo após um blob é criado ou atualizado antes da saudação correspondente `BlobTrigger` função é executada.</span><span class="sxs-lookup"><span data-stu-id="dd182-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="dd182-167">Há uma exceção para blobs que você cria usando Olá `Blob` atributo.</span><span class="sxs-lookup"><span data-stu-id="dd182-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="dd182-168">Quando Olá SDK do WebJobs cria um novo blob, ele passa o novo blob de saudação imediatamente tooany correspondência `BlobTrigger` funções.</span><span class="sxs-lookup"><span data-stu-id="dd182-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="dd182-169">Portanto, se você tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência.</span><span class="sxs-lookup"><span data-stu-id="dd182-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="dd182-170">Porém, se você quer que haja baixa latência ao executar as funções de processamento de blob para blobs criados ou atualizados por outros meios, é recomendável usar `QueueTrigger` em vez de `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="dd182-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="dd182-171"><a id="receipts"></a> Recebimentos de blob</span><span class="sxs-lookup"><span data-stu-id="dd182-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="dd182-172">Olá SDK do WebJobs garante que nenhum `BlobTrigger` função é chamada mais de uma vez para Olá mesmo novo ou atualizado blob.</span><span class="sxs-lookup"><span data-stu-id="dd182-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="dd182-173">Ele faz isso, mantendo *recebimentos de blob* em ordem toodetermine se uma versão de determinado blob tiver sido processada.</span><span class="sxs-lookup"><span data-stu-id="dd182-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="dd182-174">Recebimentos de blob são armazenados em um contêiner chamado *hosts de trabalhos Web do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="dd182-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="dd182-175">Confirmação de blob tem Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd182-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="dd182-176">Olá função que foi chamada para o blob de saudação ("*{nome do trabalho Web}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="dd182-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="dd182-177">nome do contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="dd182-177">hello container name</span></span>
* <span data-ttu-id="dd182-178">tipo de blob Hello ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="dd182-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="dd182-179">nome do blob Olá</span><span class="sxs-lookup"><span data-stu-id="dd182-179">hello blob name</span></span>
* <span data-ttu-id="dd182-180">Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="dd182-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="dd182-181">Se você quiser tooforce reprocessamento de um blob, você poderá excluir manualmente a confirmação de blob de Olá para o blob de saudação *hosts de trabalhos Web do azure* contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd182-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="dd182-182"><a id="queues"></a>Tópicos relacionados cobertos pelo artigo de filas de saudação</span><span class="sxs-lookup"><span data-stu-id="dd182-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="dd182-183">Para obter informações sobre como o processamento de blob toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não tooblob específico de processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="dd182-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="dd182-184">Tópicos relacionados abordados nesse artigo incluem seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="dd182-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="dd182-185">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="dd182-185">Async functions</span></span>
* <span data-ttu-id="dd182-186">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="dd182-186">Multiple instances</span></span>
* <span data-ttu-id="dd182-187">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="dd182-187">Graceful shutdown</span></span>
* <span data-ttu-id="dd182-188">Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="dd182-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="dd182-189">Defina cadeias de caracteres de conexão do hello SDK no código.</span><span class="sxs-lookup"><span data-stu-id="dd182-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="dd182-190">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="dd182-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="dd182-191">Configurar `MaxDequeueCount` para manipulação de blobs suspeitos.</span><span class="sxs-lookup"><span data-stu-id="dd182-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="dd182-192">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="dd182-192">Trigger a function manually</span></span>
* <span data-ttu-id="dd182-193">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="dd182-193">Write logs</span></span>

## <span data-ttu-id="dd182-194"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd182-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="dd182-195">Este guia fornece exemplos de código que mostram como blobs de cenários comuns de toohandle para trabalhar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="dd182-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="dd182-196">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos recomendada do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="dd182-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

