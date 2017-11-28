---
title: aaaUse SDK .NET para trabalhos do Gerenciador de dados do Microsoft Azure StorSimple | Microsoft Docs
description: "Saiba como o SDK .NET de toouse toolaunch StorSimple Data Manager trabalhos (visualização particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="67380-103">Use Olá .net SDK tooinitiate transformação de dados (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="67380-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="67380-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="67380-104">Overview</span></span>

<span data-ttu-id="67380-105">Este artigo explica como você pode usar o recurso de transformação de dados hello dentro Olá StorSimple Data Manager serviço tootransform os dados do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="67380-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="67380-106">Olá dados transformados são consumidos por outros serviços do Azure na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="67380-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="67380-107">artigo Olá também tem um toohelp passo a passo criar um trabalho de transformação de dados de um tooinitiate de aplicativo de console do exemplo .NET e acompanhe-o para a conclusão.</span><span class="sxs-lookup"><span data-stu-id="67380-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67380-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67380-108">Prerequisites</span></span>

<span data-ttu-id="67380-109">Antes de começar, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="67380-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="67380-110">Um sistema com o Visual Studio 2012, 2013, 2015 ou 2017 instalado.</span><span class="sxs-lookup"><span data-stu-id="67380-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="67380-111">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="67380-111">Azure Powershell installed.</span></span> <span data-ttu-id="67380-112">[Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="67380-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="67380-113">Configuração tooinitialize Olá transformação de dados trabalho de configurações (instruções tooobtain essas configurações são incluídas aqui).</span><span class="sxs-lookup"><span data-stu-id="67380-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="67380-114">Uma definição de trabalho que foi configurada corretamente em um recurso de dados híbrido dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="67380-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="67380-115">Todas as dlls de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="67380-115">All hello required dlls.</span></span> <span data-ttu-id="67380-116">Baixar essas dlls de saudação [repositório GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="67380-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="67380-117">`Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) do repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="67380-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="67380-118">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="67380-118">Step-by-step</span></span>

<span data-ttu-id="67380-119">Execute Olá seguindo as etapas toouse .NET toolaunch um trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="67380-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="67380-120">parâmetros de configuração do tooretrieve hello, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="67380-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="67380-121">Baixar Olá `Get-ConfigurationParams.ps1` do script de repositório github Olá em `C:\DataTransformation` local.</span><span class="sxs-lookup"><span data-stu-id="67380-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="67380-122">Executar Olá `Get-ConfigurationParams.ps1` script do repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="67380-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="67380-123">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="67380-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="67380-124">Você pode passar em todos os valores hello ActiveDirectoryKey e AppName.</span><span class="sxs-lookup"><span data-stu-id="67380-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="67380-125">Esse script gera Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="67380-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="67380-126">ID do cliente</span><span class="sxs-lookup"><span data-stu-id="67380-126">Client ID</span></span>
    * <span data-ttu-id="67380-127">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="67380-127">Tenant ID</span></span>
    * <span data-ttu-id="67380-128">Chave de diretório ativo (mesmo que Olá fornecido acima)</span><span class="sxs-lookup"><span data-stu-id="67380-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="67380-129">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="67380-129">Subscription ID</span></span>

3. <span data-ttu-id="67380-130">Usando o Visual Studio 2012, 2013 ou 2015, crie um aplicativo de console do .NET em C#.</span><span class="sxs-lookup"><span data-stu-id="67380-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="67380-131">Inicie o **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="67380-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="67380-132">Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="67380-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="67380-133">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="67380-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="67380-134">Selecione **aplicativo de Console** da lista de saudação de tipos de projeto em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="67380-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="67380-135">Digite **DataTransformationApp** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="67380-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="67380-136">Selecione **C:\DataTransformation** para Olá **local**.</span><span class="sxs-lookup"><span data-stu-id="67380-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="67380-137">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="67380-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="67380-138">Agora, adicione todas as DLLs presentes no hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) pasta **referências** no projeto de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="67380-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="67380-139">arquivos de dll do toodownload hello, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="67380-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="67380-140">No Visual Studio, vá muito**exibição > Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="67380-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="67380-141">Clique em Olá seta toohello esquerda de projeto de aplicativo de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="67380-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="67380-142">Clique em **referências** e, em seguida, clique com botão direito muito**adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="67380-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="67380-143">Procurar toohello local da pasta de pacotes de saudação, selecione todas as DLLs de saudação e clique em **adicionar**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="67380-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="67380-144">Adicione o seguinte Olá **usando** arquivo de origem toohello instruções (Program.cs) no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="67380-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="67380-145">saudação de código a seguir inicializa a instância de trabalho de transformação de dados hello.</span><span class="sxs-lookup"><span data-stu-id="67380-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="67380-146">Este suplemento Olá **método Main**.</span><span class="sxs-lookup"><span data-stu-id="67380-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="67380-147">Substitua valores hello dos parâmetros de configuração como obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="67380-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="67380-148">Plug-in valores hello **nome do grupo de recursos** e **nome do recurso de dados híbrido**.</span><span class="sxs-lookup"><span data-stu-id="67380-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="67380-149">Olá **nome do grupo de recursos** é hello que hospeda Olá híbrida dados recurso no qual Olá definição de trabalho foi configurada.</span><span class="sxs-lookup"><span data-stu-id="67380-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="67380-150">Especifique a saudação parâmetros com quais Olá a definição de trabalho precisa toobe executados</span><span class="sxs-lookup"><span data-stu-id="67380-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="67380-151">(OU)</span><span class="sxs-lookup"><span data-stu-id="67380-151">(OR)</span></span>

    <span data-ttu-id="67380-152">Parâmetros de definição do trabalho de saudação toochange durante o tempo de execução, em seguida, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="67380-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="67380-153">Após a inicialização do hello, adicione Olá código tootrigger um trabalho de transformação de dados na definição de trabalho Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="67380-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="67380-154">Plug-in Olá apropriado **nome de definição de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="67380-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="67380-155">Esse trabalho carrega arquivos de saudação correspondida presentes no diretório raiz de saudação no contêiner especificado de toohello Olá de volume StorSimple.</span><span class="sxs-lookup"><span data-stu-id="67380-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="67380-156">Quando um arquivo é carregado, uma mensagem é descartada na fila de saudação (em Olá mesma conta de armazenamento como contêiner Olá) com hello mesmo nome como definição de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="67380-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="67380-157">Essa mensagem pode ser usada como um tooinitiate gatilho qualquer processamento do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="67380-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="67380-158">Depois que o trabalho Olá foi disparado, adicione Olá após o trabalho de saudação do código tootrack para conclusão.</span><span class="sxs-lookup"><span data-stu-id="67380-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="67380-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67380-159">Next steps</span></span>

<span data-ttu-id="67380-160">[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="67380-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
