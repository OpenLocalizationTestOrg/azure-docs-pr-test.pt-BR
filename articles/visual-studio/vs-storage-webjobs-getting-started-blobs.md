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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="a499e-103">Introdução ao armazenamento de Blob do Azure e aos serviços conectados do Visual Studio (projetos WebJob)</span><span class="sxs-lookup"><span data-stu-id="a499e-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a499e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a499e-104">Overview</span></span>
<span data-ttu-id="a499e-105">Este artigo fornece c# exemplos de código que mostram como tootrigger um processo quando um blob do Azure é criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="a499e-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="a499e-106">exemplos de código Olá usam Olá [SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versão 1. x.</span><span class="sxs-lookup"><span data-stu-id="a499e-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="a499e-107">Quando você adiciona um projeto WebJob de tooa de conta de armazenamento usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo, pacote de NuGet de armazenamento do Azure apropriado hello está instalado, referências de .NET apropriadas Olá são toohello adicionado projeto e cadeias de caracteres de conexão para a conta de armazenamento Olá são atualizadas no arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="a499e-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="a499e-108">Como tootrigger uma função quando um blob é criado ou atualizado</span><span class="sxs-lookup"><span data-stu-id="a499e-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="a499e-109">Esta seção mostra como Olá toouse **BlobTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="a499e-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="a499e-110">**Observação:** Olá toowatch de arquivos de log SDK do WebJobs verificações para blobs novos ou alterados.</span><span class="sxs-lookup"><span data-stu-id="a499e-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="a499e-111">Esse processo é inerentemente lento; uma função não poderá obter disparada até vários minutos ou mais depois Olá blob é criado.</span><span class="sxs-lookup"><span data-stu-id="a499e-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="a499e-112">Se seu aplicativo precisa tooprocess blobs imediatamente, Olá recomendado método é toocreate uma mensagem da fila ao criar blob hello e usar Olá [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo em vez da saudação **BlobTrigger** atributo na função hello processa blob hello.</span><span class="sxs-lookup"><span data-stu-id="a499e-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="a499e-113">Espaço reservado único para nome de blob com extensão</span><span class="sxs-lookup"><span data-stu-id="a499e-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="a499e-114">Olá exemplo de código a seguir copia blobs de texto que aparecem no hello *entrada* contêiner toohello *saída* contêiner:</span><span class="sxs-lookup"><span data-stu-id="a499e-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a499e-115">o construtor de atributo Olá leva um parâmetro de cadeia de caracteres que especifica o nome do contêiner hello e um espaço reservado para nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="a499e-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="a499e-116">Neste exemplo, se um blob denominado *Blob1.txt* é criado no hello *entrada* contêiner, a função hello cria um blob denominado *Blob1.txt* em Olá *saída*  contêiner.</span><span class="sxs-lookup"><span data-stu-id="a499e-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="a499e-117">Você pode especificar um padrão de nome com um espaço reservado para nome de blob hello, conforme mostrado no hello exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a499e-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a499e-118">Esse código copia somente os blobs que têm nomes que começam com "original-".</span><span class="sxs-lookup"><span data-stu-id="a499e-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="a499e-119">Por exemplo, *original Blob1.txt* em Olá *entrada* contêiner é copiado muito*cópia Blob1.txt* em Olá *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="a499e-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="a499e-120">Se você precisar toospecify um padrão de nome para nomes de blob que têm chaves no nome hello, clique duas vezes chaves hello.</span><span class="sxs-lookup"><span data-stu-id="a499e-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="a499e-121">Por exemplo, se você quiser toofind blobs Olá *imagens* contêiner que têm nomes como este:</span><span class="sxs-lookup"><span data-stu-id="a499e-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="a499e-122">Use o seguinte para o padrão:</span><span class="sxs-lookup"><span data-stu-id="a499e-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="a499e-123">No exemplo hello, Olá *nome* seria o valor de espaço reservado *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="a499e-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="a499e-124">Separar espaços reservados de nome de blob e extensão</span><span class="sxs-lookup"><span data-stu-id="a499e-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="a499e-125">Olá alterações de exemplo de código seguinte Olá extensão de arquivo como ele copia blobs que aparecem no hello *entrada* contêiner toohello *saída* contêiner.</span><span class="sxs-lookup"><span data-stu-id="a499e-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="a499e-126">código Olá logs extensão Olá Olá *entrada* de blob e define a extensão de saudação do hello *saída* blob muito*. txt*.</span><span class="sxs-lookup"><span data-stu-id="a499e-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="a499e-127">Tipos que você pode associar tooblobs</span><span class="sxs-lookup"><span data-stu-id="a499e-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="a499e-128">Você pode usar o hello **BlobTrigger** atributo Olá tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a499e-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="a499e-129">**string**</span><span class="sxs-lookup"><span data-stu-id="a499e-129">**string**</span></span>
* <span data-ttu-id="a499e-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="a499e-130">**TextReader**</span></span>
* <span data-ttu-id="a499e-131">**Fluxo**</span><span class="sxs-lookup"><span data-stu-id="a499e-131">**Stream**</span></span>
* <span data-ttu-id="a499e-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="a499e-132">**ICloudBlob**</span></span>
* <span data-ttu-id="a499e-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="a499e-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="a499e-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="a499e-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="a499e-135">Outros tipos desserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="a499e-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="a499e-136">Se você desejar toowork diretamente com hello conta de armazenamento do Azure, você também pode adicionar uma **CloudStorageAccount** assinatura de método do parâmetro toohello.</span><span class="sxs-lookup"><span data-stu-id="a499e-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="a499e-137">Ao obter conteúdo de blob de texto por toostring de associação</span><span class="sxs-lookup"><span data-stu-id="a499e-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="a499e-138">Se os blobs de texto são esperados, **BlobTrigger** podem ser aplicada tooa **cadeia de caracteres** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a499e-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="a499e-139">Olá, exemplo de código a seguir associa um tooa de blob de texto **cadeia de caracteres** parâmetro denominado **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="a499e-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="a499e-140">função Hello usa esse conteúdo parâmetro toowrite Olá Olá blob toohello painel do SDK do WebJobs.</span><span class="sxs-lookup"><span data-stu-id="a499e-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="a499e-141">Obtendo conteúdo de blob serializado usando ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="a499e-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="a499e-142">Olá, exemplo de código a seguir usa uma classe que implementa **ICloudBlobStreamBinder** tooenable Olá **BlobTrigger** toobind toohello um blob de atributo **WebImage** tipo.</span><span class="sxs-lookup"><span data-stu-id="a499e-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="a499e-143">Olá **WebImage** código de associação é fornecido em um **WebImageBinder** classe que deriva de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="a499e-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="a499e-144">Como os blobs de inviabilização toohandle</span><span class="sxs-lookup"><span data-stu-id="a499e-144">How toohandle poison blobs</span></span>
<span data-ttu-id="a499e-145">Quando um **BlobTrigger** função falhar, Olá SDK chamá-lo novamente, no caso de Olá falha foi causada por um erro transitório.</span><span class="sxs-lookup"><span data-stu-id="a499e-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="a499e-146">Se a falha de saudação é causada por conteúdo de saudação do blob Olá, função hello falha toda vez que ele tenta tooprocess blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="a499e-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="a499e-147">Por padrão, a saudação SDK chama uma função too5 horas para um determinado blob.</span><span class="sxs-lookup"><span data-stu-id="a499e-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="a499e-148">Se tentar quinto Olá falhar, Olá SDK adiciona uma fila de tooa mensagem denominada *webjobs-blobtrigger-suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="a499e-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="a499e-149">Olá o número máximo de repetições é configurável.</span><span class="sxs-lookup"><span data-stu-id="a499e-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="a499e-150">Olá mesmo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuração é usada para o tratamento de blob suspeita e a manipulação de mensagens suspeitas de fila.</span><span class="sxs-lookup"><span data-stu-id="a499e-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="a499e-151">mensagem da fila Olá para blobs suspeitas é um objeto JSON que contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="a499e-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="a499e-152">FunctionId (no formato de saudação *{nome do trabalho Web}*. Funções. *{Nome da função}*, por exemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="a499e-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="a499e-153">BlobType ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a499e-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a499e-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="a499e-154">ContainerName</span></span>
* <span data-ttu-id="a499e-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="a499e-155">BlobName</span></span>
* <span data-ttu-id="a499e-156">ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a499e-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a499e-157">Seguir Olá amostra de código, hello **CopyBlob** função tiver um código que faz com que ele toofail toda vez que ele é chamado.</span><span class="sxs-lookup"><span data-stu-id="a499e-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="a499e-158">Depois de saudação SDK chamá-lo para o número máximo de saudação de novas tentativas, será criada uma mensagem na fila de blob suspeitas hello e essa mensagem é processada pelo Olá **LogPoisonBlob** função.</span><span class="sxs-lookup"><span data-stu-id="a499e-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="a499e-159">Olá SDK automaticamente desserializa a mensagem de saudação do JSON.</span><span class="sxs-lookup"><span data-stu-id="a499e-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="a499e-160">Aqui está a saudação **PoisonBlobMessage** classe:</span><span class="sxs-lookup"><span data-stu-id="a499e-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="a499e-161">Algoritmo de sondagem de blob</span><span class="sxs-lookup"><span data-stu-id="a499e-161">Blob polling algorithm</span></span>
<span data-ttu-id="a499e-162">Olá SDK do WebJobs examina todos os contêineres especificados por **BlobTrigger** atributos no início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a499e-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="a499e-163">Em uma conta de armazenamento grande, essa verificação pode levar algum tempo. Portanto, pode demorar um pouco até que novos blobs sejam encontrados e as funções **BlobTrigger** sejam executadas.</span><span class="sxs-lookup"><span data-stu-id="a499e-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="a499e-164">toodetect blobs nova ou alterada após a inicialização do aplicativo, logs de saudação que SDK lê periodicamente saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="a499e-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="a499e-165">Olá blob logs são armazenados no buffer e obtenham fisicamente gravadas somente a cada 10 minutos ou assim, portanto pode haver um atraso significativo após um blob é criado ou atualizado antes da saudação correspondente **BlobTrigger** função é executada.</span><span class="sxs-lookup"><span data-stu-id="a499e-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="a499e-166">Há uma exceção para blobs que você cria usando Olá **Blob** atributo.</span><span class="sxs-lookup"><span data-stu-id="a499e-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="a499e-167">Quando Olá SDK do WebJobs cria um novo blob, ele passa o novo blob de saudação imediatamente correspondência tooany **BlobTrigger** funções.</span><span class="sxs-lookup"><span data-stu-id="a499e-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="a499e-168">Portanto, se você tiver uma cadeia de blob entradas e saídas, Olá SDK pode processá-los com eficiência.</span><span class="sxs-lookup"><span data-stu-id="a499e-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="a499e-169">Porém, se você quiser que haja baixa latência ao executar as funções de processamento para blobs criados ou atualizados por outros meios, é recomendável usar **QueueTrigger** em vez de **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="a499e-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="a499e-170">Recebimentos de blob</span><span class="sxs-lookup"><span data-stu-id="a499e-170">Blob receipts</span></span>
<span data-ttu-id="a499e-171">Olá SDK do WebJobs garante que nenhum **BlobTrigger** função é chamada mais de uma vez para Olá mesmo novo ou atualizado blob.</span><span class="sxs-lookup"><span data-stu-id="a499e-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="a499e-172">Ele faz isso, mantendo *recebimentos de blob* em ordem toodetermine se uma versão de determinado blob tiver sido processada.</span><span class="sxs-lookup"><span data-stu-id="a499e-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="a499e-173">Recebimentos de blob são armazenados em um contêiner chamado *hosts de trabalhos Web do azure* na conta de armazenamento do Azure Olá especificada pelo Olá AzureWebJobsStorage cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="a499e-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="a499e-174">Confirmação de blob tem Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a499e-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="a499e-175">Olá função que foi chamada para o blob de saudação ("*{nome do trabalho Web}*. Funções. *{Nome da função}*", por exemplo:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="a499e-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="a499e-176">nome do contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="a499e-176">hello container name</span></span>
* <span data-ttu-id="a499e-177">tipo de blob Hello ("BlockBlob" ou "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a499e-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a499e-178">nome do blob Olá</span><span class="sxs-lookup"><span data-stu-id="a499e-178">hello blob name</span></span>
* <span data-ttu-id="a499e-179">Olá ETag (um identificador de versão de blob, por exemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a499e-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a499e-180">Se você quiser tooforce reprocessamento de um blob, você poderá excluir manualmente a confirmação de blob de Olá para o blob de saudação *hosts de trabalhos Web do azure* contêiner.</span><span class="sxs-lookup"><span data-stu-id="a499e-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="a499e-181">Tópicos relacionados cobertos pelo artigo de filas de saudação</span><span class="sxs-lookup"><span data-stu-id="a499e-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="a499e-182">Para obter informações sobre como o processamento de blob toohandle disparada por uma mensagem da fila, ou para WebJobs cenários do SDK não tooblob específico de processamento, consulte [como toouse Azure fila de armazenamento com hello SDK do WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a499e-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="a499e-183">Tópicos relacionados abordados nesse artigo incluem seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a499e-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="a499e-184">Funções assíncronas</span><span class="sxs-lookup"><span data-stu-id="a499e-184">Async functions</span></span>
* <span data-ttu-id="a499e-185">Várias instâncias</span><span class="sxs-lookup"><span data-stu-id="a499e-185">Multiple instances</span></span>
* <span data-ttu-id="a499e-186">Desligamento normal</span><span class="sxs-lookup"><span data-stu-id="a499e-186">Graceful shutdown</span></span>
* <span data-ttu-id="a499e-187">Usar atributos de SDK do WebJobs no corpo de saudação de uma função</span><span class="sxs-lookup"><span data-stu-id="a499e-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="a499e-188">Defina cadeias de caracteres de conexão do hello SDK no código.</span><span class="sxs-lookup"><span data-stu-id="a499e-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="a499e-189">Definir valores para parâmetros do construtor do SDK WebJobs no código</span><span class="sxs-lookup"><span data-stu-id="a499e-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="a499e-190">Configure **MaxDequeueCount** para tratamento de blob suspeito.</span><span class="sxs-lookup"><span data-stu-id="a499e-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="a499e-191">Disparar uma função manualmente</span><span class="sxs-lookup"><span data-stu-id="a499e-191">Trigger a function manually</span></span>
* <span data-ttu-id="a499e-192">Gravar logs</span><span class="sxs-lookup"><span data-stu-id="a499e-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="a499e-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a499e-193">Next steps</span></span>
<span data-ttu-id="a499e-194">Este artigo fornece exemplos de código que mostram como blobs de cenários comuns de toohandle para trabalhar com o Azure.</span><span class="sxs-lookup"><span data-stu-id="a499e-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="a499e-195">Para obter mais informações sobre como toouse WebJobs do Azure e hello WebJobs SDK, consulte [recursos de documentação do Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a499e-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

