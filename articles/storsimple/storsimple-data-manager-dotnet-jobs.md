---
title: Usar o SDK do .NET para trabalhos do Gerenciador de Dados do Microsoft Azure StorSimple | Microsoft Docs
description: "Saiba como usar o SDK do .NET para iniciar trabalhos do Gerenciador de Dados StorSimple (visualização particular)"
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
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="7ca0f-103">Usar o SDK do .net para iniciar a transformação de dados (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="7ca0f-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="7ca0f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7ca0f-104">Overview</span></span>

<span data-ttu-id="7ca0f-105">Este artigo explica como você pode usar o recurso de transformação de dados dentro do serviço do Gerenciador de Dados StorSimple para transformar os dados do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="7ca0f-106">Os dados transformados, em seguida, são consumidos por outros serviços do Azure na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="7ca0f-107">O artigo também tem um passo a passo para ajudar a criar um aplicativo de console do .NET de exemplo a fim de iniciar um trabalho de transformação de dados e acompanhar a sua conclusão.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ca0f-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ca0f-108">Prerequisites</span></span>

<span data-ttu-id="7ca0f-109">Antes de começar, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="7ca0f-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="7ca0f-110">Um sistema com o Visual Studio 2012, 2013, 2015 ou 2017 instalado.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="7ca0f-111">Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-111">Azure Powershell installed.</span></span> <span data-ttu-id="7ca0f-112">[Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="7ca0f-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="7ca0f-113">Definições de configuração para inicializar o trabalho de Transformação de Dados (as instruções para obter essas configurações estão incluídas aqui).</span><span class="sxs-lookup"><span data-stu-id="7ca0f-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="7ca0f-114">Uma definição de trabalho que foi configurada corretamente em um recurso de dados híbrido dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="7ca0f-115">Todas as dlls necessárias.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-115">All the required dlls.</span></span> <span data-ttu-id="7ca0f-116">Baixe essas dlls do [repositório GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="7ca0f-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="7ca0f-117">Um `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="7ca0f-118">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="7ca0f-118">Step-by-step</span></span>

<span data-ttu-id="7ca0f-119">Execute as seguintes etapas para usar o .NET e iniciar um trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="7ca0f-120">Para recuperar os parâmetros de configuração, execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ca0f-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="7ca0f-121">Baixe o `Get-ConfigurationParams.ps1` do script do repositório GitHub no local `C:\DataTransformation`.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="7ca0f-122">Execute o script `Get-ConfigurationParams.ps1` do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="7ca0f-123">Digite o seguinte comando: </span><span class="sxs-lookup"><span data-stu-id="7ca0f-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="7ca0f-124">Você pode passar em todos os valores para ActiveDirectoryKey e AppName.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="7ca0f-125">Esse script gera como saída os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="7ca0f-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="7ca0f-126">Id do Cliente</span><span class="sxs-lookup"><span data-stu-id="7ca0f-126">Client ID</span></span>
    * <span data-ttu-id="7ca0f-127">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="7ca0f-127">Tenant ID</span></span>
    * <span data-ttu-id="7ca0f-128">Chave do Active Directory (a mesma inserida acima)</span><span class="sxs-lookup"><span data-stu-id="7ca0f-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="7ca0f-129">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="7ca0f-129">Subscription ID</span></span>

3. <span data-ttu-id="7ca0f-130">Usando o Visual Studio 2012, 2013 ou 2015, crie um aplicativo de console do .NET em C#.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="7ca0f-131">Inicie o **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="7ca0f-132">Clique em **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="7ca0f-133">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="7ca0f-134">Selecione **Aplicativo de console** na lista de tipos de projetos à direita.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="7ca0f-135">Digite **DataTransformationApp** como **Nome**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="7ca0f-136">Selecione **C:\DataTransformation** como **Local**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="7ca0f-137">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="7ca0f-138">Agora, adicione todas as DLLs que estão na pasta [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) como **Referências** no projeto que você criou.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="7ca0f-139">Para baixar os arquivos dll, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7ca0f-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="7ca0f-140">No Visual Studio, vá para **Modo de Exibição > Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="7ca0f-141">Clique na seta à esquerda do projeto do Aplicativo de Transformação de Dados.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="7ca0f-142">Clique em **Referências** e clique com o botão direito do mouse em **Adicionar Referência**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="7ca0f-143">Navegue até o local da pasta de pacotes, selecione todas as DLLs e clique em **Adicionar**e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="7ca0f-144">Adicione as seguintes declarações **using** ao arquivo de origem (Program.cs) no projeto.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="7ca0f-145">O código a seguir inicializa a instância do trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="7ca0f-146">Adicione isso ao **Método principal**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-146">Add this in the **Main method**.</span></span> <span data-ttu-id="7ca0f-147">Substitua os valores dos parâmetros de configuração como obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="7ca0f-148">Conecte os valores de **Nome do Grupo de Recursos** e **Nome do Recurso de Dados Híbrido**.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="7ca0f-149">O **Nome do Grupo de Recursos** é aquele que hospeda o Recurso de Dados Híbrido no qual a definição de trabalho foi configurada.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="7ca0f-150">Especifique os parâmetros com os quais a definição de trabalho precisa ser executada</span><span class="sxs-lookup"><span data-stu-id="7ca0f-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="7ca0f-151">(OU)</span><span class="sxs-lookup"><span data-stu-id="7ca0f-151">(OR)</span></span>

    <span data-ttu-id="7ca0f-152">Se você quiser alterar os parâmetros de definição de trabalho durante o tempo de execução, adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="7ca0f-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="7ca0f-153">Após a inicialização, adicione o código a seguir para disparar um trabalho de transformação de dados na definição de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="7ca0f-154">Use o plug-in do **Nome de Definição do Trabalho** apropriado.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="7ca0f-155">Esse trabalho carrega os arquivos correspondentes presentes no diretório raiz do volume do StorSimple no contêiner especificado.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="7ca0f-156">Quando um arquivo é carregado, uma mensagem é descartada da fila (na mesma conta de armazenamento que o contêiner) com o mesmo nome da definição de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="7ca0f-157">Essa mensagem pode ser usada como um disparador para iniciar o processamento do arquivo.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="7ca0f-158">Depois que o trabalho é disparado, adicione o código a seguir para acompanhar o trabalho até a conclusão.</span><span class="sxs-lookup"><span data-stu-id="7ca0f-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="7ca0f-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ca0f-159">Next steps</span></span>

<span data-ttu-id="7ca0f-160">[Use a interface do usuário do Gerenciador de Dados StorSimple para transformar seus dados](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="7ca0f-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
