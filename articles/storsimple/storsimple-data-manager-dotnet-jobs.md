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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Use Olá .net SDK tooinitiate transformação de dados (visualização particular)

## <a name="overview"></a>Visão geral

Este artigo explica como você pode usar o recurso de transformação de dados hello dentro Olá StorSimple Data Manager serviço tootransform os dados do dispositivo StorSimple. Olá dados transformados são consumidos por outros serviços do Azure na nuvem hello. artigo Olá também tem um toohelp passo a passo criar um trabalho de transformação de dados de um tooinitiate de aplicativo de console do exemplo .NET e acompanhe-o para a conclusão.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você tem:
*   Um sistema com o Visual Studio 2012, 2013, 2015 ou 2017 instalado.
*   Azure Powershell instalado. [Baixar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Configuração tooinitialize Olá transformação de dados trabalho de configurações (instruções tooobtain essas configurações são incluídas aqui).
*   Uma definição de trabalho que foi configurada corretamente em um recurso de dados híbrido dentro de um grupo de recursos.
*   Todas as dlls de saudação necessária. Baixar essas dlls de saudação [repositório GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) do repositório do github hello.

## <a name="step-by-step"></a>Passo a passo

Execute Olá seguindo as etapas toouse .NET toolaunch um trabalho de transformação de dados.

1. parâmetros de configuração do tooretrieve hello, Olá seguintes etapas:
    1. Baixar Olá `Get-ConfigurationParams.ps1` do script de repositório github Olá em `C:\DataTransformation` local.
    1. Executar Olá `Get-ConfigurationParams.ps1` script do repositório do github hello. Digite hello comando a seguir:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        Você pode passar em todos os valores hello ActiveDirectoryKey e AppName.


2. Esse script gera Olá valores a seguir:
    * ID do cliente
    * ID do locatário
    * Chave de diretório ativo (mesmo que Olá fornecido acima)
    * ID da assinatura

3. Usando o Visual Studio 2012, 2013 ou 2015, crie um aplicativo de console do .NET em C#.

    1. Inicie o **Visual Studio 2012/2013/2015**.
    1. Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.
    2. Expanda **Modelos** e selecione **Visual C#**.
    3. Selecione **aplicativo de Console** da lista de saudação de tipos de projeto em saudação à direita.
    4. Digite **DataTransformationApp** para Olá **nome**.
    5. Selecione **C:\DataTransformation** para Olá **local**.
    6. Clique em **Okey** toocreate projeto de saudação.

4.  Agora, adicione todas as DLLs presentes no hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) pasta **referências** no projeto de saudação que você criou. arquivos de dll do toodownload hello, Olá a seguir:

    1. No Visual Studio, vá muito**exibição > Gerenciador de soluções**.
    1. Clique em Olá seta toohello esquerda de projeto de aplicativo de transformação de dados. Clique em **referências** e, em seguida, clique com botão direito muito**adicionar referência**.
    2. Procurar toohello local da pasta de pacotes de saudação, selecione todas as DLLs de saudação e clique em **adicionar**e, em seguida, clique em **Okey**.

5. Adicione o seguinte Olá **usando** arquivo de origem toohello instruções (Program.cs) no projeto de saudação.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. saudação de código a seguir inicializa a instância de trabalho de transformação de dados hello. Este suplemento Olá **método Main**. Substitua valores hello dos parâmetros de configuração como obtido anteriormente. Plug-in valores hello **nome do grupo de recursos** e **nome do recurso de dados híbrido**. Olá **nome do grupo de recursos** é hello que hospeda Olá híbrida dados recurso no qual Olá definição de trabalho foi configurada.

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

7. Especifique a saudação parâmetros com quais Olá a definição de trabalho precisa toobe executados

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (OU)

    Parâmetros de definição do trabalho de saudação toochange durante o tempo de execução, em seguida, adicione Olá código a seguir:

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

8. Após a inicialização do hello, adicione Olá código tootrigger um trabalho de transformação de dados na definição de trabalho Olá a seguir. Plug-in Olá apropriado **nome de definição de trabalho**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Esse trabalho carrega arquivos de saudação correspondida presentes no diretório raiz de saudação no contêiner especificado de toohello Olá de volume StorSimple. Quando um arquivo é carregado, uma mensagem é descartada na fila de saudação (em Olá mesma conta de armazenamento como contêiner Olá) com hello mesmo nome como definição de trabalho hello. Essa mensagem pode ser usada como um tooinitiate gatilho qualquer processamento do arquivo hello.

10. Depois que o trabalho Olá foi disparado, adicione Olá após o trabalho de saudação do código tootrack para conclusão.

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


## <a name="next-steps"></a>Próximas etapas

[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).
