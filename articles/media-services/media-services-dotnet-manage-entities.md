---
title: Ativos de aaaManaging e entidades relacionadas com o SDK do Media Services .NET
description: Saiba como ativos de toomanage e entidades relacionadas com hello SDK do Media Services para .NET.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="a9bc5-103">Gerenciamento dos ativos e entidades relacionadas com o .NET SDK dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a9bc5-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9bc5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a9bc5-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="a9bc5-105">REST</span><span class="sxs-lookup"><span data-stu-id="a9bc5-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="a9bc5-106">Este tópico mostra como toomanage Azure Media Services entidades com .NET.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="a9bc5-107">Começando em 1 de abril de 2017, qualquer registro de trabalho em sua conta mais de 90 dias será excluído automaticamente, junto com seus registros de tarefas associados, mesmo se Olá o número total de registros é abaixo de cota máximo hello.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="a9bc5-108">Por exemplo, no dia 1º de abril de 2017, qualquer registro de Trabalho em sua conta que seja mais antigo do que 31 de dezembro de 2016 será excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="a9bc5-109">Se precisar de informações de trabalho/tarefa do tooarchive hello, você pode usar código Olá descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9bc5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a9bc5-110">Prerequisites</span></span>

<span data-ttu-id="a9bc5-111">Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="a9bc5-112">Obter uma referência de ativo</span><span class="sxs-lookup"><span data-stu-id="a9bc5-112">Get an Asset Reference</span></span>
<span data-ttu-id="a9bc5-113">Uma tarefa frequente é tooget um ativo existente de tooan de referência nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="a9bc5-114">saudação de exemplo de código a seguir mostra como obter uma referência de ativo do conjunto de ativos de saudação no servidor de saudação objeto de contexto, com base em uma saudação de ID ativo usa de exemplo de código a seguir um Linq consulta tooget um objeto de IAsset referência tooan existente.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="a9bc5-115">Listar todos os ativos</span><span class="sxs-lookup"><span data-stu-id="a9bc5-115">List All Assets</span></span>
<span data-ttu-id="a9bc5-116">Conforme aumenta Olá número de ativos que você tem no armazenamento, é útil toolist seus ativos.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="a9bc5-117">saudação de exemplo de código a seguir mostra como tooiterate por meio de Olá coleção ativos no objeto de contexto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="a9bc5-118">Com cada ativo, o exemplo de código Olá também grava alguns seu console de toohello de valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="a9bc5-119">Por exemplo, cada ativo pode conter vários arquivos de mídia.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="a9bc5-120">exemplo de código Hello grava todos os arquivos associados a cada ativo.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-120">hello code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a><span data-ttu-id="a9bc5-121">Obter uma referência de trabalho</span><span class="sxs-lookup"><span data-stu-id="a9bc5-121">Get a Job Reference</span></span>

<span data-ttu-id="a9bc5-122">Quando você trabalhar com tarefas de processamento em código de serviços de mídia, muitas vezes é preciso tooget um trabalho existente de referência tooan com base em uma saudação de ID. exemplo de código a seguir mostra como os objetos de coleção de trabalhos de saudação tooget tooan uma referência IJob.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="a9bc5-123">Você pode precisar tooget uma referência de trabalho ao iniciar um trabalho de codificação de longa execução e precisa de status do trabalho Olá toocheck em um thread.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="a9bc5-124">Em casos como esse, quando o método hello retorna de um thread, você precisa tooretrieve um trabalho de tooa Referência atualizada.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="a9bc5-125">Listar trabalhos e ativos</span><span class="sxs-lookup"><span data-stu-id="a9bc5-125">List Jobs and Assets</span></span>
<span data-ttu-id="a9bc5-126">Uma tarefa relacionada importante é ativos toolist com seu trabalho associado nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="a9bc5-127">Olá exemplo de código a seguir mostra como toolist cada objeto IJob e, em seguida, para cada trabalho, exibe propriedades sobre trabalho hello, todas as tarefas relacionadas, todas as entrada ativos e todos os ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="a9bc5-128">código neste exemplo Hello pode ser útil para muitas outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="a9bc5-129">Por exemplo, se você quiser toolist Olá ativos de saída de um ou mais trabalhos de codificação que você executou anteriormente, esse código mostra como tooaccess Olá ativos de saída.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="a9bc5-130">Quando você tiver um ativo de saída de tooan de referência, você poderá fornecer Olá tooother conteúdo usuários ou aplicativos baixando-o ou fornecendo URLs.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="a9bc5-131">Para obter mais informações sobre as opções de entrega de ativos, consulte [entregar ativos com o SDK do Media Services para .NET de saudação](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a><span data-ttu-id="a9bc5-132">Listar todas as políticas de acesso</span><span class="sxs-lookup"><span data-stu-id="a9bc5-132">List all Access Policies</span></span>
<span data-ttu-id="a9bc5-133">Nos serviços de mídia, você pode definir uma política de acesso em um ativo ou seus arquivos.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="a9bc5-134">Uma política de acesso define permissões de saudação para um arquivo ou um ativo (o tipo de acesso e a duração de saudação).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="a9bc5-135">Em seu código de serviços de mídia, você normalmente define uma política de acesso criando um objeto IAccessPolicy e associá-la a um ativo existente.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="a9bc5-136">Em seguida, você pode criar um objeto de ILocator, que permite que você forneça acesso direto tooassets nos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="a9bc5-137">projeto do Visual Studio Olá que acompanha esta série de documentação contém vários exemplos de código que mostram como toocreate e atribuir acessam tooassets políticas e os localizadores.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="a9bc5-138">Olá mostra exemplo de código a seguir como toolist todas as políticas de acesso no servidor de saudação e mostra o tipo de saudação de permissões associadas a cada.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="a9bc5-139">As políticas de acesso outra forma útil tooview é toolist todos os objetos de ILocator no servidor de saudação e, em seguida, para cada localizador, você pode listar sua política de acesso associada usando sua propriedade AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a><span data-ttu-id="a9bc5-140">Limitar as políticas de acesso</span><span class="sxs-lookup"><span data-stu-id="a9bc5-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="a9bc5-141">Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a9bc5-142">Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="a9bc5-143">Por exemplo, você pode criar um conjunto geral de políticas com hello seguindo o código que será executado somente uma vez em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="a9bc5-144">Você pode registrar o arquivo de log tooa IDs para uso posterior:</span><span class="sxs-lookup"><span data-stu-id="a9bc5-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="a9bc5-145">Em seguida, você pode usar o hello existentes IDs no seu código como este:</span><span class="sxs-lookup"><span data-stu-id="a9bc5-145">Then, you can use hello existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="a9bc5-146">Listar todos os localizadores</span><span class="sxs-lookup"><span data-stu-id="a9bc5-146">List All Locators</span></span>
<span data-ttu-id="a9bc5-147">Um localizador é uma URL que fornece um caminho direto tooaccess um ativo, juntamente com o ativo de toohello permissões conforme definido pela política de acesso associada do localizador hello.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="a9bc5-148">Cada ativo pode ter uma coleção de objetos ILocator associados a ele em sua propriedade de Localizadores.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="a9bc5-149">contexto de saudação do servidor também tem uma coleção de localizadores que contém todos os localizadores.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="a9bc5-150">Olá, exemplo de código a seguir lista todos os localizadores no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="a9bc5-151">Para cada localizador, ele mostra Olá Id de ativo relacionados hello e política de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="a9bc5-152">Ele também exibe o tipo de saudação de permissões, data de expiração hello e ativos de toohello de caminho completo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="a9bc5-153">Observe que um ativo de tooan de caminho do localizador é apenas um base ativo de toohello de URL.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="a9bc5-154">toocreate que tooindividual um caminho direto arquivos que um usuário ou aplicativo pode navegar, seu código deve adicionar caminho de localizador Olá arquivo específico caminho toohello.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="a9bc5-155">Para obter mais informações sobre como toodo isso, consulte o tópico de saudação [entregar ativos com o SDK do Media Services para .NET de saudação](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="a9bc5-156">Enumerar através de grandes coleções de entidades</span><span class="sxs-lookup"><span data-stu-id="a9bc5-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="a9bc5-157">Ao consultar entidades, há um limite de 1000 entidades retornadas ao mesmo tempo porque pública v2 do REST limita os resultados da consulta resultados too1000.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="a9bc5-158">Você precisará toouse Skip e Take ao enumerar através de grandes coleções de entidades.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="a9bc5-159">Olá função executa um loop em todos os trabalhos de Olá Olá fornecido a conta de serviços de mídia a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="a9bc5-160">Os Serviços de Mídia retornam 1.000 trabalhos da coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="a9bc5-161">função Hello faz usar ignorar e tomar toomake-se que todos os trabalhos são enumerados (caso você tenha mais de 1000 trabalhos em sua conta).</span><span class="sxs-lookup"><span data-stu-id="a9bc5-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a><span data-ttu-id="a9bc5-162">Excluir um ativo</span><span class="sxs-lookup"><span data-stu-id="a9bc5-162">Delete an Asset</span></span>
<span data-ttu-id="a9bc5-163">saudação de exemplo a seguir exclui um ativo.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="a9bc5-164">Excluir um trabalho</span><span class="sxs-lookup"><span data-stu-id="a9bc5-164">Delete a Job</span></span>
<span data-ttu-id="a9bc5-165">toodelete um trabalho, você deve verificar o estado de saudação do trabalho de saudação conforme indicado na propriedade de estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="a9bc5-166">Os Trabalhos que foram concluídos ou cancelados podem ser excluídos, enquanto os trabalhos que estão em alguns outros estados, como enfileirado, agendado ou em processamento devem ser cancelados primeiro e, em seguida, eles podem ser excluídos.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="a9bc5-167">Olá, exemplo de código a seguir mostra um método para excluir um trabalho de verificação de estados de trabalho e excluindo quando o estado de saudação é concluído ou cancelado.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="a9bc5-168">Esse código depende da seção anterior Olá neste tópico para obter um trabalho de tooa de referência: obter uma referência de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a><span data-ttu-id="a9bc5-169">Excluir uma política de acesso</span><span class="sxs-lookup"><span data-stu-id="a9bc5-169">Delete an Access Policy</span></span>
<span data-ttu-id="a9bc5-170">Hello exemplo de código a seguir mostra como tooget uma política de acesso de tooan de referência com base em uma Id de política e política de saudação toodelete.</span><span class="sxs-lookup"><span data-stu-id="a9bc5-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="a9bc5-171">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="a9bc5-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9bc5-172">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="a9bc5-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

