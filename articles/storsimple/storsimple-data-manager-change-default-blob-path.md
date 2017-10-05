---
title: "Alterar o caminho de blob padrão | Microsoft Docs"
description: "Saiba como configurar uma função do Azure para renomear um caminho de arquivo de blob (visualização particular)"
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
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="9c4f7-103">Alterar o caminho de blob padrão (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="9c4f7-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="9c4f7-104">Este artigo descreve como configurar uma função do Azure para renomear um caminho de arquivo de blob padrão.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9c4f7-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9c4f7-105">Prerequisites</span></span>

<span data-ttu-id="9c4f7-106">Verifique se você tem uma definição de trabalho que foi configurada corretamente em um recurso de dados híbridos dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="9c4f7-107">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="9c4f7-107">Create an Azure function</span></span>

<span data-ttu-id="9c4f7-108">Para criar uma função do Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="9c4f7-109">Vá para o [Portal do Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c4f7-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="9c4f7-110">Na parte superior do painel esquerdo, clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="9c4f7-111">Na caixa **Pesquisa**, digite **Aplicativo de Funções** e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Digite “Aplicativo de Funções” na caixa Pesquisa](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="9c4f7-113">Na lista **Resultados**, clique em **Aplicativo de Funções**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-113">In the **Results** list, click **Function App**.</span></span>

    ![Selecione o recurso de aplicativo de funções na lista de resultados](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="9c4f7-115">A janela **Aplicativo de Funções** é aberta.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="9c4f7-116">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-116">Click **Create**.</span></span>

    ![O botão “Criar” da janela Aplicativo de Funções](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="9c4f7-118">Na folha de configuração **Aplicativo de Funções**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="9c4f7-119">a.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-119">a.</span></span> <span data-ttu-id="9c4f7-120">Na caixa **Nome do aplicativo**, digite o nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="9c4f7-121">b.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-121">b.</span></span> <span data-ttu-id="9c4f7-122">Na caixa **Assinatura**, digite o nome da assinatura.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="9c4f7-123">c.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-123">c.</span></span> <span data-ttu-id="9c4f7-124">Em **Grupo de Recursos**, clique em **Criar novo** e digite o nome do novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="9c4f7-125">d.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-125">d.</span></span> <span data-ttu-id="9c4f7-126">Na caixa **Plano de Hospedagem**, digite **Plano de Consumo**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="9c4f7-127">e.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-127">e.</span></span> <span data-ttu-id="9c4f7-128">Na caixa **Local**, digite o local.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="9c4f7-129">f.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-129">f.</span></span> <span data-ttu-id="9c4f7-130">Em **Conta de armazenamento**, selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="9c4f7-131">Uma conta de armazenamento é usada internamente para a função.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-131">A storage account is used internally for the function.</span></span>

    ![Inserir dados de configuração do novo Aplicativo de Funções](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="9c4f7-133">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-133">Click **Create**.</span></span>  
    <span data-ttu-id="9c4f7-134">O aplicativo de funções é criado.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-134">The function app is created.</span></span>

8. <span data-ttu-id="9c4f7-135">No painel esquerdo, clique em **Mais serviços** e, em seguida, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="9c4f7-136">a.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-136">a.</span></span> <span data-ttu-id="9c4f7-137">Na caixa **Filtro**, digite **Serviços de aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="9c4f7-138">b.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-138">b.</span></span> <span data-ttu-id="9c4f7-139">Clique em **Serviços de Aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-139">Click **App Services**.</span></span> 

    ![Link “Mais serviços” no painel esquerdo](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="9c4f7-141">Na lista de serviços de aplicativos, clique no nome do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="9c4f7-142">A página do aplicativo de funções é aberta.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-142">The function app page opens.</span></span>

10. <span data-ttu-id="9c4f7-143">No painel esquerdo, clique em **Nova Função** e, em seguida, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="9c4f7-144">a.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-144">a.</span></span> <span data-ttu-id="9c4f7-145">Na lista **Linguagem**, selecione **C#**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="9c4f7-146">b.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-146">b.</span></span> <span data-ttu-id="9c4f7-147">Na matriz de blocos de modelo, selecione **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="9c4f7-148">c.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-148">c.</span></span> <span data-ttu-id="9c4f7-149">Na caixa **Dê um nome à sua função**, digite um nome para a função.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="9c4f7-150">d.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-150">d.</span></span> <span data-ttu-id="9c4f7-151">Na caixa **Nome da fila**, digite o nome da definição de trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="9c4f7-152">e.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-152">e.</span></span> <span data-ttu-id="9c4f7-153">Em **Conexão da conta de armazenamento**, clique em **Nova** e, em seguida, selecione a conta que corresponde ao trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="9c4f7-154">Anote o nome da conexão.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-154">Make a note of the connection name.</span></span> <span data-ttu-id="9c4f7-155">Esse nome será necessário mais tarde na função do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-155">The name is required later in the Azure function.</span></span>

       ![Criar uma nova função do C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="9c4f7-157">f.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-157">f.</span></span> <span data-ttu-id="9c4f7-158">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-158">Click **Create**.</span></span>  
    <span data-ttu-id="9c4f7-159">A janela **Função** é aberta.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="9c4f7-160">Na janela **Função**, execute o arquivo _.csx_ e, em seguida, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="9c4f7-161">a.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-161">a.</span></span> <span data-ttu-id="9c4f7-162">Cole o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-162">Paste the following code:</span></span>

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

        // Create the blob client.
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
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
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

    <span data-ttu-id="9c4f7-163">b.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-163">b.</span></span> <span data-ttu-id="9c4f7-164">Substitua **STORAGE_CONNECTIONNAME** na linha 11 pela conexão da conta de armazenamento (consulte o ponto 8c).</span><span class="sxs-lookup"><span data-stu-id="9c4f7-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="9c4f7-165">c.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-165">c.</span></span> <span data-ttu-id="9c4f7-166">Na parte superior esquerda, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-166">At the top left, click **Save**.</span></span>

    ![Salvar função](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="9c4f7-168">Para concluir a função, adicione mais um arquivo fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="9c4f7-169">a.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-169">a.</span></span> <span data-ttu-id="9c4f7-170">Clique em **Exibir arquivos**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-170">Click **View files**.</span></span>

       ![O link “Exibir arquivos”](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="9c4f7-172">b.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-172">b.</span></span> <span data-ttu-id="9c4f7-173">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-173">Click **Add**.</span></span>
    
    <span data-ttu-id="9c4f7-174">c.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-174">c.</span></span> <span data-ttu-id="9c4f7-175">Digite **project.json** e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="9c4f7-176">d.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-176">d.</span></span> <span data-ttu-id="9c4f7-177">No arquivo **project.json**, cole o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="9c4f7-177">In the **project.json** file, paste the following code:</span></span>

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

    <span data-ttu-id="9c4f7-178">e.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-178">e.</span></span> <span data-ttu-id="9c4f7-179">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-179">Click **Save**.</span></span>

<span data-ttu-id="9c4f7-180">Você criou uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-180">You have created an Azure function.</span></span> <span data-ttu-id="9c4f7-181">Essa função é disparada sempre que um novo blob é gerado pelo trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="9c4f7-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c4f7-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c4f7-182">Next steps</span></span>

[<span data-ttu-id="9c4f7-183">Usar a interface do usuário do Gerenciador de Dados StorSimple para transformar seus dados</span><span class="sxs-lookup"><span data-stu-id="9c4f7-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
