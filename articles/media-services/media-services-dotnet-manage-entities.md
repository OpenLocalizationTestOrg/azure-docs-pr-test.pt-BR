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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Gerenciamento dos ativos e entidades relacionadas com o .NET SDK dos Serviços de Mídia
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Este tópico mostra como toomanage Azure Media Services entidades com .NET. 

>[!NOTE]
> Começando em 1 de abril de 2017, qualquer registro de trabalho em sua conta mais de 90 dias será excluído automaticamente, junto com seus registros de tarefas associados, mesmo se Olá o número total de registros é abaixo de cota máximo hello. Por exemplo, no dia 1º de abril de 2017, qualquer registro de Trabalho em sua conta que seja mais antigo do que 31 de dezembro de 2016 será excluído automaticamente. Se precisar de informações de trabalho/tarefa do tooarchive hello, você pode usar código Olá descrito neste tópico.

## <a name="prerequisites"></a>Pré-requisitos

Configurar seu ambiente de desenvolvimento e preencher o arquivo App. config de saudação com informações de conexão, conforme descrito em [desenvolvimento de serviços de mídia com o .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Obter uma referência de ativo
Uma tarefa frequente é tooget um ativo existente de tooan de referência nos serviços de mídia. saudação de exemplo de código a seguir mostra como obter uma referência de ativo do conjunto de ativos de saudação no servidor de saudação objeto de contexto, com base em uma saudação de ID ativo usa de exemplo de código a seguir um Linq consulta tooget um objeto de IAsset referência tooan existente.

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

## <a name="list-all-assets"></a>Listar todos os ativos
Conforme aumenta Olá número de ativos que você tem no armazenamento, é útil toolist seus ativos. saudação de exemplo de código a seguir mostra como tooiterate por meio de Olá coleção ativos no objeto de contexto do servidor de saudação. Com cada ativo, o exemplo de código Olá também grava alguns seu console de toohello de valores de propriedade. Por exemplo, cada ativo pode conter vários arquivos de mídia. exemplo de código Hello grava todos os arquivos associados a cada ativo.

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

## <a name="get-a-job-reference"></a>Obter uma referência de trabalho

Quando você trabalhar com tarefas de processamento em código de serviços de mídia, muitas vezes é preciso tooget um trabalho existente de referência tooan com base em uma saudação de ID. exemplo de código a seguir mostra como os objetos de coleção de trabalhos de saudação tooget tooan uma referência IJob.

Você pode precisar tooget uma referência de trabalho ao iniciar um trabalho de codificação de longa execução e precisa de status do trabalho Olá toocheck em um thread. Em casos como esse, quando o método hello retorna de um thread, você precisa tooretrieve um trabalho de tooa Referência atualizada.

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

## <a name="list-jobs-and-assets"></a>Listar trabalhos e ativos
Uma tarefa relacionada importante é ativos toolist com seu trabalho associado nos serviços de mídia. Olá exemplo de código a seguir mostra como toolist cada objeto IJob e, em seguida, para cada trabalho, exibe propriedades sobre trabalho hello, todas as tarefas relacionadas, todas as entrada ativos e todos os ativos de saída. código neste exemplo Hello pode ser útil para muitas outras tarefas. Por exemplo, se você quiser toolist Olá ativos de saída de um ou mais trabalhos de codificação que você executou anteriormente, esse código mostra como tooaccess Olá ativos de saída. Quando você tiver um ativo de saída de tooan de referência, você poderá fornecer Olá tooother conteúdo usuários ou aplicativos baixando-o ou fornecendo URLs. 

Para obter mais informações sobre as opções de entrega de ativos, consulte [entregar ativos com o SDK do Media Services para .NET de saudação](media-services-deliver-streaming-content.md).

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

## <a name="list-all-access-policies"></a>Listar todas as políticas de acesso
Nos serviços de mídia, você pode definir uma política de acesso em um ativo ou seus arquivos. Uma política de acesso define permissões de saudação para um arquivo ou um ativo (o tipo de acesso e a duração de saudação). Em seu código de serviços de mídia, você normalmente define uma política de acesso criando um objeto IAccessPolicy e associá-la a um ativo existente. Em seguida, você pode criar um objeto de ILocator, que permite que você forneça acesso direto tooassets nos serviços de mídia. projeto do Visual Studio Olá que acompanha esta série de documentação contém vários exemplos de código que mostram como toocreate e atribuir acessam tooassets políticas e os localizadores.

Olá mostra exemplo de código a seguir como toolist todas as políticas de acesso no servidor de saudação e mostra o tipo de saudação de permissões associadas a cada. As políticas de acesso outra forma útil tooview é toolist todos os objetos de ILocator no servidor de saudação e, em seguida, para cada localizador, você pode listar sua política de acesso associada usando sua propriedade AccessPolicy.

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
    
## <a name="limit-access-policies"></a>Limitar as políticas de acesso 

>[!NOTE]
> Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). 

Por exemplo, você pode criar um conjunto geral de políticas com hello seguindo o código que será executado somente uma vez em seu aplicativo. Você pode registrar o arquivo de log tooa IDs para uso posterior:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Em seguida, você pode usar o hello existentes IDs no seu código como este:

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

## <a name="list-all-locators"></a>Listar todos os localizadores
Um localizador é uma URL que fornece um caminho direto tooaccess um ativo, juntamente com o ativo de toohello permissões conforme definido pela política de acesso associada do localizador hello. Cada ativo pode ter uma coleção de objetos ILocator associados a ele em sua propriedade de Localizadores. contexto de saudação do servidor também tem uma coleção de localizadores que contém todos os localizadores.

Olá, exemplo de código a seguir lista todos os localizadores no servidor de saudação. Para cada localizador, ele mostra Olá Id de ativo relacionados hello e política de acesso. Ele também exibe o tipo de saudação de permissões, data de expiração hello e ativos de toohello de caminho completo de saudação.

Observe que um ativo de tooan de caminho do localizador é apenas um base ativo de toohello de URL. toocreate que tooindividual um caminho direto arquivos que um usuário ou aplicativo pode navegar, seu código deve adicionar caminho de localizador Olá arquivo específico caminho toohello. Para obter mais informações sobre como toodo isso, consulte o tópico de saudação [entregar ativos com o SDK do Media Services para .NET de saudação](media-services-deliver-streaming-content.md).

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

## <a name="enumerating-through-large-collections-of-entities"></a>Enumerar através de grandes coleções de entidades
Ao consultar entidades, há um limite de 1000 entidades retornadas ao mesmo tempo porque pública v2 do REST limita os resultados da consulta resultados too1000. Você precisará toouse Skip e Take ao enumerar através de grandes coleções de entidades. 

Olá função executa um loop em todos os trabalhos de Olá Olá fornecido a conta de serviços de mídia a seguir. Os Serviços de Mídia retornam 1.000 trabalhos da coleção de trabalhos. função Hello faz usar ignorar e tomar toomake-se que todos os trabalhos são enumerados (caso você tenha mais de 1000 trabalhos em sua conta).

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

## <a name="delete-an-asset"></a>Excluir um ativo
saudação de exemplo a seguir exclui um ativo.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Excluir um trabalho
toodelete um trabalho, você deve verificar o estado de saudação do trabalho de saudação conforme indicado na propriedade de estado de saudação. Os Trabalhos que foram concluídos ou cancelados podem ser excluídos, enquanto os trabalhos que estão em alguns outros estados, como enfileirado, agendado ou em processamento devem ser cancelados primeiro e, em seguida, eles podem ser excluídos.

Olá, exemplo de código a seguir mostra um método para excluir um trabalho de verificação de estados de trabalho e excluindo quando o estado de saudação é concluído ou cancelado. Esse código depende da seção anterior Olá neste tópico para obter um trabalho de tooa de referência: obter uma referência de trabalho.

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


## <a name="delete-an-access-policy"></a>Excluir uma política de acesso
Hello exemplo de código a seguir mostra como tooget uma política de acesso de tooan de referência com base em uma Id de política e política de saudação toodelete.

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



## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

