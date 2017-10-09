---
title: "caminho de blob aaaChange do padrão de saudação | Microsoft Docs"
description: "Saiba como tooset backup do Azure funciona toorename um caminho de arquivo de blob (visualização particular)"
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="145ed-103">Alterar um caminho de blob do caminho padrão de saudação (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="145ed-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="145ed-104">Este artigo descreve como tooset backup do Azure funciona toorename um caminho de arquivo de blob padrão.</span><span class="sxs-lookup"><span data-stu-id="145ed-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="145ed-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="145ed-105">Prerequisites</span></span>

<span data-ttu-id="145ed-106">Verifique se você tem uma definição de trabalho que foi configurada corretamente em um recurso de dados híbridos dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="145ed-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="145ed-107">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="145ed-107">Create an Azure function</span></span>

<span data-ttu-id="145ed-108">toocreate uma função do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="145ed-109">Vá toohello [portal do Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="145ed-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="145ed-110">Na parte superior de saudação do painel esquerdo do hello, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="145ed-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="145ed-111">Em Olá **pesquisa** , digite **aplicativo função**, e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="145ed-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Digite "Função de aplicativo" na caixa de pesquisa de saudação](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="145ed-113">Em Olá **resultados** lista, clique em **aplicativo função**.</span><span class="sxs-lookup"><span data-stu-id="145ed-113">In hello **Results** list, click **Function App**.</span></span>

    ![Selecione o recurso de aplicativo hello função na lista de resultados de saudação](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="145ed-115">Olá **aplicativo função** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="145ed-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="145ed-116">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-116">Click **Create**.</span></span>

    ![botão de "Criar" Hello aplicativo função janela](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="145ed-118">Em Olá **aplicativo função** folha de configuração, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="145ed-119">a.</span><span class="sxs-lookup"><span data-stu-id="145ed-119">a.</span></span> <span data-ttu-id="145ed-120">Em Olá **nome do aplicativo** caixa, nome do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="145ed-121">b.</span><span class="sxs-lookup"><span data-stu-id="145ed-121">b.</span></span> <span data-ttu-id="145ed-122">Em Olá **assinatura** caixa, digite o nome de saudação de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="145ed-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="145ed-123">c.</span><span class="sxs-lookup"><span data-stu-id="145ed-123">c.</span></span> <span data-ttu-id="145ed-124">Em **grupo de recursos**, clique em **criar novo**e, em seguida, tipo de nome Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="145ed-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="145ed-125">d.</span><span class="sxs-lookup"><span data-stu-id="145ed-125">d.</span></span> <span data-ttu-id="145ed-126">Em Olá **plano de hospedagem** , digite **consumo planejar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="145ed-127">e.</span><span class="sxs-lookup"><span data-stu-id="145ed-127">e.</span></span> <span data-ttu-id="145ed-128">Em Olá **local** caixa tipo hello local.</span><span class="sxs-lookup"><span data-stu-id="145ed-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="145ed-129">f.</span><span class="sxs-lookup"><span data-stu-id="145ed-129">f.</span></span> <span data-ttu-id="145ed-130">Em **Conta de armazenamento**, selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="145ed-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="145ed-131">Uma conta de armazenamento é usada internamente para a função hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-131">A storage account is used internally for hello function.</span></span>

    ![Inserir dados de configuração do novo Aplicativo de Funções](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="145ed-133">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-133">Click **Create**.</span></span>  
    <span data-ttu-id="145ed-134">Olá função aplicativo é criado.</span><span class="sxs-lookup"><span data-stu-id="145ed-134">hello function app is created.</span></span>

8. <span data-ttu-id="145ed-135">No painel esquerdo do hello, clique em **mais serviços**e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="145ed-136">a.</span><span class="sxs-lookup"><span data-stu-id="145ed-136">a.</span></span> <span data-ttu-id="145ed-137">Em Olá **filtro** , digite **serviços de aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="145ed-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="145ed-138">b.</span><span class="sxs-lookup"><span data-stu-id="145ed-138">b.</span></span> <span data-ttu-id="145ed-139">Clique em **Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="145ed-139">Click **App Services**.</span></span> 

    ![Link "Mais serviços" no painel esquerdo da saudação](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="145ed-141">Na lista de saudação de serviços de aplicativos, clique nome de saudação do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="145ed-142">Abre a página de aplicativo de função Hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-142">hello function app page opens.</span></span>

10. <span data-ttu-id="145ed-143">No painel esquerdo do hello, clique em **nova função**e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="145ed-144">a.</span><span class="sxs-lookup"><span data-stu-id="145ed-144">a.</span></span> <span data-ttu-id="145ed-145">Em Olá **idioma** lista, selecione **c#**.</span><span class="sxs-lookup"><span data-stu-id="145ed-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="145ed-146">b.</span><span class="sxs-lookup"><span data-stu-id="145ed-146">b.</span></span> <span data-ttu-id="145ed-147">Na matriz de saudação dos blocos de modelo, selecione **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="145ed-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="145ed-148">c.</span><span class="sxs-lookup"><span data-stu-id="145ed-148">c.</span></span> <span data-ttu-id="145ed-149">Em Olá **nomear a função** , digite um nome para sua função.</span><span class="sxs-lookup"><span data-stu-id="145ed-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="145ed-150">d.</span><span class="sxs-lookup"><span data-stu-id="145ed-150">d.</span></span> <span data-ttu-id="145ed-151">Em Olá **nome de fila** , digite seu nome de definição do trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="145ed-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="145ed-152">e.</span><span class="sxs-lookup"><span data-stu-id="145ed-152">e.</span></span> <span data-ttu-id="145ed-153">Em **conexão da conta de armazenamento**, clique em **novo**e selecione conta Olá correspondente toohello trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="145ed-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="145ed-154">Anote o nome de conexão do hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-154">Make a note of hello connection name.</span></span> <span data-ttu-id="145ed-155">é necessário o nome de Hello mais tarde no hello função do Azure.</span><span class="sxs-lookup"><span data-stu-id="145ed-155">hello name is required later in hello Azure function.</span></span>

       ![Criar uma nova função do C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="145ed-157">f.</span><span class="sxs-lookup"><span data-stu-id="145ed-157">f.</span></span> <span data-ttu-id="145ed-158">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-158">Click **Create**.</span></span>  
    <span data-ttu-id="145ed-159">Olá **função** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="145ed-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="145ed-160">Em Olá **função** janela, execute _. CSx_ de arquivo e, em seguida, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="145ed-161">a.</span><span class="sxs-lookup"><span data-stu-id="145ed-161">a.</span></span> <span data-ttu-id="145ed-162">Cole Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-162">Paste hello following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="145ed-163">b.</span><span class="sxs-lookup"><span data-stu-id="145ed-163">b.</span></span> <span data-ttu-id="145ed-164">Substitua **STORAGE_CONNECTIONNAME** na linha 11 pela conexão da conta de armazenamento (consulte o ponto 8c).</span><span class="sxs-lookup"><span data-stu-id="145ed-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="145ed-165">c.</span><span class="sxs-lookup"><span data-stu-id="145ed-165">c.</span></span> <span data-ttu-id="145ed-166">Olá parte superior esquerda, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-166">At hello top left, click **Save**.</span></span>

    ![Salvar função](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="145ed-168">toocomplete Olá função, adicione mais um arquivo hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="145ed-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="145ed-169">a.</span><span class="sxs-lookup"><span data-stu-id="145ed-169">a.</span></span> <span data-ttu-id="145ed-170">Clique em **Exibir arquivos**.</span><span class="sxs-lookup"><span data-stu-id="145ed-170">Click **View files**.</span></span>

       ![Olá link "Exibir arquivos"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="145ed-172">b.</span><span class="sxs-lookup"><span data-stu-id="145ed-172">b.</span></span> <span data-ttu-id="145ed-173">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-173">Click **Add**.</span></span>
    
    <span data-ttu-id="145ed-174">c.</span><span class="sxs-lookup"><span data-stu-id="145ed-174">c.</span></span> <span data-ttu-id="145ed-175">Digite **project.json** e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="145ed-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="145ed-176">d.</span><span class="sxs-lookup"><span data-stu-id="145ed-176">d.</span></span> <span data-ttu-id="145ed-177">Em Olá **Project** de arquivo, cole Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="145ed-177">In hello **project.json** file, paste hello following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="145ed-178">e.</span><span class="sxs-lookup"><span data-stu-id="145ed-178">e.</span></span> <span data-ttu-id="145ed-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="145ed-179">Click **Save**.</span></span>

<span data-ttu-id="145ed-180">Você criou uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="145ed-180">You have created an Azure function.</span></span> <span data-ttu-id="145ed-181">Essa função é acionada sempre que um novo blob é gerado pelo trabalho de transformação de dados hello.</span><span class="sxs-lookup"><span data-stu-id="145ed-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="145ed-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="145ed-182">Next steps</span></span>

[<span data-ttu-id="145ed-183">Use os dados de interface de usuário de Gerenciador de dados StorSimple tootransform</span><span class="sxs-lookup"><span data-stu-id="145ed-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
