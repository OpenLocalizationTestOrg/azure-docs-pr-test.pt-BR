---
title: "Introdução ao armazenamento de blob e aos serviços conectados do Visual Studio (projetos de Trabalho Web) | Microsoft Docs"
description: "Como começar a usar o armazenamento de Blob em um projeto WebJob depois de se conectar a um armazenamento do Azure usando os serviços conectados do Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 7fec890590302a99bbc96f46f24ae440c041580c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="6d76c-103">Introdução ao armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos WebJob)</span><span class="sxs-lookup"><span data-stu-id="6d76c-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6d76c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6d76c-104">Overview</span></span>
<span data-ttu-id="6d76c-105">Este artigo fornece exemplos de código C# que mostram como disparar um processo quando um blob do Azure é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="6d76c-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="6d76c-106">Os exemplos de código usam o [SDK WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1.x.</span><span class="sxs-lookup"><span data-stu-id="6d76c-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="6d76c-107">Quando você adiciona uma conta de armazenamento a um projeto de WebJob usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio, o pacote do NuGet do Armazenamento do Azure apropriado é instalado, as referências apropriadas .NET são adicionadas ao projeto e cadeias de conexão para a conta de armazenamento são atualizadas no arquivo App.config.</span><span class="sxs-lookup"><span data-stu-id="6d76c-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="6d76c-108">Como disparar uma função quando um blob é criado ou atualizado</span><span class="sxs-lookup"><span data-stu-id="6d76c-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="6d76c-109">Esta seção mostra como usar o atributo **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="6d76c-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="6d76c-110">**Observação:** o SDK dos trabalhos Web verifica os arquivos de log para observar blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="6d76c-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="6d76c-111">Esse processo é inerentemente lento; uma função não poderá ser disparada até vários minutos ou mais depois que o blob for criado.</span><span class="sxs-lookup"><span data-stu-id="6d76c-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="6d76c-112">Se seu aplicativo precisar processar blobs imediatamente, o método recomendado é criar uma mensagem da fila ao criar o blob e usar o atributo [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) em vez do atributo **BlobTrigger** na função que processa o blob.</span><span class="sxs-lookup"><span data-stu-id="6d76c-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="6d76c-113">Espaço reservado único para nome de blob com extensão</span><span class="sxs-lookup"><span data-stu-id="6d76c-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="6d76c-114">O seguinte exemplo de código copia blobs de texto que aparecem no contêiner de *entrada* para o contêiner de *saída*:</span><span class="sxs-lookup"><span data-stu-id="6d76c-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6d76c-115">O construtor de atributo utiliza um parâmetro de cadeia de caracteres que especifica o nome do contêiner e um espaço reservado para o nome do blob.</span><span class="sxs-lookup"><span data-stu-id="6d76c-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="6d76c-116">Neste exemplo, se um blob denominado *Blob1.txt* for criado no contêiner de *entrada*, a função criará um blob denominado *Blob1.txt* no contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="6d76c-117">Você pode especificar um padrão de nome com o espaço reservado de nome de blob, conforme é mostrado no seguinte exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="6d76c-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6d76c-118">Esse código copia somente os blobs que têm nomes que começam com "original-".</span><span class="sxs-lookup"><span data-stu-id="6d76c-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="6d76c-119">Por exemplo, *original-Blob1.txt* no contêiner de *entrada* é copiado para *copy-Blob1.txt* no contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="6d76c-120">Se você precisar especificar um padrão de nome para nomes de blob que têm chaves no nome, duplique as chaves.</span><span class="sxs-lookup"><span data-stu-id="6d76c-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="6d76c-121">Por exemplo, para localizar blobs no contêiner *imagens* que têm nomes como este:</span><span class="sxs-lookup"><span data-stu-id="6d76c-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="6d76c-122">Use o seguinte para o padrão:</span><span class="sxs-lookup"><span data-stu-id="6d76c-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="6d76c-123">No exemplo, o valor do espaço reservado para *nome* seria *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="6d76c-124">Separar espaços reservados de nome de blob e extensão</span><span class="sxs-lookup"><span data-stu-id="6d76c-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="6d76c-125">O exemplo de código a seguir altera a extensão do arquivo à medida que ele copia blobs que aparecem no contêiner de *entrada* para o contêiner de *saída*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="6d76c-126">O código registra a extensão do blob de *entrada* e define a extensão do blob de *saída* como *.txt*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="6d76c-127">Tipos que você pode associar a blobs</span><span class="sxs-lookup"><span data-stu-id="6d76c-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="6d76c-128">Você pode usar o atributo **BlobTrigger** nos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="6d76c-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="6d76c-129">**string**</span><span class="sxs-lookup"><span data-stu-id="6d76c-129">**string**</span></span>
* <span data-ttu-id="6d76c-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="6d76c-130">**TextReader**</span></span>
* <span data-ttu-id="6d76c-131">**Fluxo**</span><span class="sxs-lookup"><span data-stu-id="6d76c-131">**Stream**</span></span>
* <span data-ttu-id="6d76c-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="6d76c-132">**ICloudBlob**</span></span>
* <span data-ttu-id="6d76c-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="6d76c-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="6d76c-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="6d76c-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="6d76c-135">Outros tipos desserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="6d76c-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="6d76c-136">Se quer trabalhar diretamente com a conta de armazenamento do Azure, você também pode adicionar um parâmetro **CloudStorageAccount** à assinatura do método.</span><span class="sxs-lookup"><span data-stu-id="6d76c-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="6d76c-137">Obtendo o conteúdo do blob de texto associando à cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6d76c-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="6d76c-138">Se blobs de texto forem esperados, **BlobTrigger** poderá ser aplicado a um parâmetro **string**.</span><span class="sxs-lookup"><span data-stu-id="6d76c-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="6d76c-139">O exemplo de código a seguir associa um blob de texto a um parâmetro **string** denominado **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="6d76c-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="6d76c-140">A função usa esse parâmetro para gravar o conteúdo do blob no painel do SDK de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="6d76c-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="6d76c-141">Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="6d76c-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="6d76c-142">O exemplo de código a seguir usa uma classe que implementa **ICloudBlobStreamBinder** para permitir que o atributo **BlobTrigger** associe um blob ao tipo **WebImage**.</span><span class="sxs-lookup"><span data-stu-id="6d76c-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

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

<span data-ttu-id="6d76c-143">O código de associação **WebImage** é fornecido em uma classe **WebImageBinder** que deriva de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="6d76c-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="6d76c-144">Como manipular blobs suspeitos</span><span class="sxs-lookup"><span data-stu-id="6d76c-144">How to handle poison blobs</span></span>
<span data-ttu-id="6d76c-145">Quando uma função **BlobTrigger** falha, o SDK a chama novamente caso a falha tenha sido causada por um erro transitório.</span><span class="sxs-lookup"><span data-stu-id="6d76c-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="6d76c-146">Se a falha for causada pelo conteúdo do blob, a função falhará sempre que tentar processar o blob.</span><span class="sxs-lookup"><span data-stu-id="6d76c-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="6d76c-147">Por padrão, o SDK chama uma função até cinco vezes para um blob específico.</span><span class="sxs-lookup"><span data-stu-id="6d76c-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="6d76c-148">Se a quinta tentativa falhar, o SDK adicionará uma mensagem a uma fila denominada *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6d76c-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="6d76c-149">O número máximo de novas tentativas é configurável.</span><span class="sxs-lookup"><span data-stu-id="6d76c-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="6d76c-150">A mesma [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) é usada para manipular blob suspeitos e manipular mensagens de filas suspeitas.</span><span class="sxs-lookup"><span data-stu-id="6d76c-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="6d76c-151">A mensagem da fila para blobs suspeitos é um objeto JSON que contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="6d76c-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="6d76c-152">FunctionId (no formato *{Nome do Trabalho Web}*.Functions.*{Nome da função}*, por exemplo: Trabalho Web1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="6d76c-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="6d76c-153">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6d76c-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6d76c-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="6d76c-154">ContainerName</span></span>
* <span data-ttu-id="6d76c-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="6d76c-155">BlobName</span></span>
* <span data-ttu-id="6d76c-156">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6d76c-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6d76c-157">No exemplo de código a seguir, a função **CopyBlob** tem código que faz com que ela falhe sempre que for chamada.</span><span class="sxs-lookup"><span data-stu-id="6d76c-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="6d76c-158">Depois que o SDK a chamar pelo número máximo de tentativas, será criada uma mensagem na fila de blobs suspeitos, e essa mensagem será processada pela função **LogPoisonBlob** .</span><span class="sxs-lookup"><span data-stu-id="6d76c-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="6d76c-159">O SDK automaticamente desserializa a mensagem JSON.</span><span class="sxs-lookup"><span data-stu-id="6d76c-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="6d76c-160">Veja aqui a classe **PoisonBlobMessage** :</span><span class="sxs-lookup"><span data-stu-id="6d76c-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="6d76c-161">Algoritmo de sondagem de blob</span><span class="sxs-lookup"><span data-stu-id="6d76c-161">Blob polling algorithm</span></span>
<span data-ttu-id="6d76c-162">O SDK de Trabalhos Web examina todos os contêineres especificados pelos atributos **BlobTrigger** na inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6d76c-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="6d76c-163">Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e as funções **BlobTrigger** sejam executadas.</span><span class="sxs-lookup"><span data-stu-id="6d76c-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="6d76c-164">Para detectar blobs novos ou alterados após a inicialização do aplicativo, o SDK lê periodicamente dos logs do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="6d76c-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="6d76c-165">Os logs de blob são armazenados em buffer e gravados fisicamente apenas a cada 10 minutos, aproximadamente. Portanto, pode haver um atraso significativo depois que um blob é criado ou atualizado antes que a função **BlobTrigger** correspondente seja executada.</span><span class="sxs-lookup"><span data-stu-id="6d76c-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="6d76c-166">Há uma exceção para blobs que você cria usando o atributo **Blob** .</span><span class="sxs-lookup"><span data-stu-id="6d76c-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="6d76c-167">Quando o SDK de WebJobs cria um novo blob, ele passa o novo blob imediatamente para quaisquer funções **BlobTrigger** correspondentes.</span><span class="sxs-lookup"><span data-stu-id="6d76c-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="6d76c-168">Portanto, se você tiver uma cadeia de entradas e saídas de blob, o SDK poderá processá-las com eficiência.</span><span class="sxs-lookup"><span data-stu-id="6d76c-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="6d76c-169">Porém, se você quiser que haja baixa latência ao executar as funções de processamento para blobs criados ou atualizados por outros meios, é recomendável usar **QueueTrigger** em vez de **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="6d76c-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="6d76c-170">Recebimentos de blob</span><span class="sxs-lookup"><span data-stu-id="6d76c-170">Blob receipts</span></span>
<span data-ttu-id="6d76c-171">O SDK de WebJobs garante que nenhuma função **BlobTrigger** seja chamada mais de uma vez para o mesmo blob novo ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="6d76c-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="6d76c-172">Ele faz isso mantendo *recebimentos de blob* para determinar se uma versão de determinado blob foi processada.</span><span class="sxs-lookup"><span data-stu-id="6d76c-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="6d76c-173">Os recebimentos de blob são armazenados em um contêiner denominado *azure-webjobs-hosts* na conta de armazenamento do Azure especificada pela cadeia de conexão AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="6d76c-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="6d76c-174">Um recebimento de blob tem as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="6d76c-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="6d76c-175">A função que foi chamada para o blob ("*{Nome do Trabalho Web}*.Functions.*{Nome da função}*", por exemplo: "Trabalho Web1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="6d76c-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="6d76c-176">O nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="6d76c-176">The container name</span></span>
* <span data-ttu-id="6d76c-177">O tipo de blob ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6d76c-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6d76c-178">O nome do blob</span><span class="sxs-lookup"><span data-stu-id="6d76c-178">The blob name</span></span>
* <span data-ttu-id="6d76c-179">O ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6d76c-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6d76c-180">Para forçar o reprocessamento de um blob, você pode excluir manualmente o recebimento desse blob do contêiner *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="6d76c-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="6d76c-181">Tópicos relacionados abordados no artigo sobre filas</span><span class="sxs-lookup"><span data-stu-id="6d76c-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="6d76c-182">Para obter informações sobre como lidar com o processamento de blob disparado por uma mensagem da fila ou para cenários do SDK de Trabalhos Web não específicos do processamento de blob, consulte [Como usar o armazenamento de fila do Azure com o SDK de Trabalhos Web](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6d76c-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="6d76c-183">Os tópicos relacionados abordados neste artigo incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d76c-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="6d76c-184">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="6d76c-184">Async functions</span></span>
* <span data-ttu-id="6d76c-185">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="6d76c-185">Multiple instances</span></span>
* <span data-ttu-id="6d76c-186">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="6d76c-186">Graceful shutdown</span></span>
* <span data-ttu-id="6d76c-187">Usar atributos do SDK de Trabalhos Web no corpo de uma função</span><span class="sxs-lookup"><span data-stu-id="6d76c-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="6d76c-188">Definir as cadeias de conexão do SDK no código.</span><span class="sxs-lookup"><span data-stu-id="6d76c-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="6d76c-189">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="6d76c-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6d76c-190">Configure **MaxDequeueCount** para tratamento de blob suspeito.</span><span class="sxs-lookup"><span data-stu-id="6d76c-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="6d76c-191">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="6d76c-191">Trigger a function manually</span></span>
* <span data-ttu-id="6d76c-192">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="6d76c-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d76c-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d76c-193">Next steps</span></span>
<span data-ttu-id="6d76c-194">Este artigo forneceu exemplos de código que mostram como lidar com cenários comuns para trabalhar com blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6d76c-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="6d76c-195">Para obter mais informações sobre como usar o Azure WebJobs e o SDK do WebJobs, consulte [Recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6d76c-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

