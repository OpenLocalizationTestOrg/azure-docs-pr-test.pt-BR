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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Alterar um caminho de blob do caminho padrão de saudação (visualização particular)

Este artigo descreve como tooset backup do Azure funciona toorename um caminho de arquivo de blob padrão. 

## <a name="prerequisites"></a>Pré-requisitos

Verifique se você tem uma definição de trabalho que foi configurada corretamente em um recurso de dados híbridos dentro de um grupo de recursos.

## <a name="create-an-azure-function"></a>Criar uma função do Azure

toocreate uma função do Azure, Olá a seguir:

1. Vá toohello [portal do Azure](http://portal.azure.com/).

2. Na parte superior de saudação do painel esquerdo do hello, clique em **novo**. 

3. Em Olá **pesquisa** , digite **aplicativo função**, e pressione Enter.

    ![Digite "Função de aplicativo" na caixa de pesquisa de saudação](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. Em Olá **resultados** lista, clique em **aplicativo função**.

    ![Selecione o recurso de aplicativo hello função na lista de resultados de saudação](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Olá **aplicativo função** janela será aberta.

5. Clique em **Criar**.

    ![botão de "Criar" Hello aplicativo função janela](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Em Olá **aplicativo função** folha de configuração, Olá a seguir:

    a. Em Olá **nome do aplicativo** caixa, nome do tipo de aplicativo hello.
    
    b. Em Olá **assinatura** caixa, digite o nome de saudação de assinatura de saudação.

    c. Em **grupo de recursos**, clique em **criar novo**e, em seguida, tipo de nome Olá Olá do grupo de recursos.

    d. Em Olá **plano de hospedagem** , digite **consumo planejar**.

    e. Em Olá **local** caixa tipo hello local.

    f. Em **Conta de armazenamento**, selecione uma conta de armazenamento existente ou crie uma nova. Uma conta de armazenamento é usada internamente para a função hello.

    ![Inserir dados de configuração do novo Aplicativo de Funções](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Clique em **Criar**.  
    Olá função aplicativo é criado.

8. No painel esquerdo do hello, clique em **mais serviços**e, em seguida, Olá a seguir:
    
    a. Em Olá **filtro** , digite **serviços de aplicativos**.
    
    b. Clique em **Serviços de Aplicativos**. 

    ![Link "Mais serviços" no painel esquerdo da saudação](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Na lista de saudação de serviços de aplicativos, clique nome de saudação do aplicativo de função hello.  
    Abre a página de aplicativo de função Hello.

10. No painel esquerdo do hello, clique em **nova função**e, em seguida, Olá a seguir: 

    a. Em Olá **idioma** lista, selecione **c#**.
    
    b. Na matriz de saudação dos blocos de modelo, selecione **QueueTrigger CSharp**.

    c. Em Olá **nomear a função** , digite um nome para sua função.

    d. Em Olá **nome de fila** , digite seu nome de definição do trabalho de transformação de dados.

    e. Em **conexão da conta de armazenamento**, clique em **novo**e selecione conta Olá correspondente toohello trabalho de transformação de dados.  
        Anote o nome de conexão do hello. é necessário o nome de Hello mais tarde no hello função do Azure.

       ![Criar uma nova função do C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Clique em **Criar**.  
    Olá **função** janela será aberta.

11. Em Olá **função** janela, execute _. CSx_ de arquivo e, em seguida, Olá a seguir:

    a. Cole Olá código a seguir:

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

    b. Substitua **STORAGE_CONNECTIONNAME** na linha 11 pela conexão da conta de armazenamento (consulte o ponto 8c).

    c. Olá parte superior esquerda, clique em **salvar**.

    ![Salvar função](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete Olá função, adicione mais um arquivo hello seguinte:

    a. Clique em **Exibir arquivos**.

       ![Olá link "Exibir arquivos"](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Clique em **Adicionar**.
    
    c. Digite **project.json** e pressione Enter.
    
    d. Em Olá **Project** de arquivo, cole Olá código a seguir:

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

    e. Clique em **Salvar**.

Você criou uma função do Azure. Essa função é acionada sempre que um novo blob é gerado pelo trabalho de transformação de dados hello.

## <a name="next-steps"></a>Próximas etapas

[Use os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md)
