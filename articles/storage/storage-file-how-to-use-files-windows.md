---
title: aaaMount um compartilhamento de arquivos do Azure e hello de acesso de compartilhamento no Windows | Microsoft Docs
description: "Monte um compartilhamento de saudação de acesso no Windows e o compartilhamento de arquivos do Azure."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="aa3bc-103">Montar um compartilhamento de saudação de acesso no Windows e o compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="aa3bc-104">[Armazenamento de arquivo do Azure](storage-dotnet-how-to-use-files.md) é o sistema de arquivos de nuvem da Microsoft toouse fácil.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="aa3bc-105">Os compartilhamentos de arquivos do Azure podem ser montados no Windows e no Windows Server.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="aa3bc-106">Este artigo mostra três toomount de formas diferentes um compartilhamento de arquivos do Azure no Windows: com hello arquivo Explorer da interface do usuário, por meio do PowerShell e por meio de saudação de Prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="aa3bc-107">Ordem toomount de um arquivo do Azure compartilhar fora Olá região do Azure está hospedado no, como no local ou em uma região do Azure diferente, Olá SO deve oferecer suporte a SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="aa3bc-108">O compartilhamento de Arquivos do Azure pode ser montado no computador Windows do local ou na VM do Azure, dependendo da versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="aa3bc-109">Tabela abaixo ilustra Olá</span><span class="sxs-lookup"><span data-stu-id="aa3bc-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="aa3bc-110">Versão do Windows</span><span class="sxs-lookup"><span data-stu-id="aa3bc-110">Windows Version</span></span>        | <span data-ttu-id="aa3bc-111">Versão do SMB</span><span class="sxs-lookup"><span data-stu-id="aa3bc-111">SMB Version</span></span> |<span data-ttu-id="aa3bc-112">Montável na VM do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-112">Mountable On Azure VM</span></span>|<span data-ttu-id="aa3bc-113">Montável no local</span><span class="sxs-lookup"><span data-stu-id="aa3bc-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="aa3bc-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="aa3bc-114">Windows 7</span></span>              | <span data-ttu-id="aa3bc-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="aa3bc-115">SMB 2.1</span></span>     | <span data-ttu-id="aa3bc-116">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-116">Yes</span></span>                 | <span data-ttu-id="aa3bc-117">Não</span><span class="sxs-lookup"><span data-stu-id="aa3bc-117">No</span></span>                  |
| <span data-ttu-id="aa3bc-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="aa3bc-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="aa3bc-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="aa3bc-119">SMB 2.1</span></span>     | <span data-ttu-id="aa3bc-120">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-120">Yes</span></span>                 | <span data-ttu-id="aa3bc-121">Não</span><span class="sxs-lookup"><span data-stu-id="aa3bc-121">No</span></span>                  |
| <span data-ttu-id="aa3bc-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="aa3bc-122">Windows 8</span></span>              | <span data-ttu-id="aa3bc-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="aa3bc-123">SMB 3.0</span></span>     | <span data-ttu-id="aa3bc-124">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-124">Yes</span></span>                 | <span data-ttu-id="aa3bc-125">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-125">Yes</span></span>                 |
| <span data-ttu-id="aa3bc-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="aa3bc-126">Windows Server 2012</span></span>    | <span data-ttu-id="aa3bc-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="aa3bc-127">SMB 3.0</span></span>     | <span data-ttu-id="aa3bc-128">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-128">Yes</span></span>                 | <span data-ttu-id="aa3bc-129">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-129">Yes</span></span>                 |
| <span data-ttu-id="aa3bc-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aa3bc-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="aa3bc-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="aa3bc-131">SMB 3.0</span></span>     | <span data-ttu-id="aa3bc-132">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-132">Yes</span></span>                 | <span data-ttu-id="aa3bc-133">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-133">Yes</span></span>                 |
| <span data-ttu-id="aa3bc-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="aa3bc-134">Windows 10</span></span>             | <span data-ttu-id="aa3bc-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="aa3bc-135">SMB 3.0</span></span>     | <span data-ttu-id="aa3bc-136">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-136">Yes</span></span>                 | <span data-ttu-id="aa3bc-137">Sim</span><span class="sxs-lookup"><span data-stu-id="aa3bc-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="aa3bc-138">É sempre recomendável fazer Olá KB mais recente para a sua versão do Windows.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="aa3bc-139"></a>Pré-requisitos para montar o compartilhamento de arquivos do Azure com o Windows</span><span class="sxs-lookup"><span data-stu-id="aa3bc-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="aa3bc-140">**Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="aa3bc-141">**Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário).</span><span class="sxs-lookup"><span data-stu-id="aa3bc-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="aa3bc-142">Atualmente, as chaves SAS não têm suporte para montagem.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="aa3bc-143">**Certifique-se de que a porta 445 esteja aberta**: o armazenamento de arquivos do Azure usa o protocolo SMB.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="aa3bc-144">SMB se comunica pela porta TCP 445 - Verifique toosee se o firewall não está bloqueando as portas TCP 445 do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="aa3bc-145">Montar o compartilhamento de arquivos do Azure Olá Explorador de arquivos</span><span class="sxs-lookup"><span data-stu-id="aa3bc-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="aa3bc-146">Observe que Olá instruções a seguir são mostradas no Windows 10 e podem diferir ligeiramente em versões mais antigas.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="aa3bc-147">**Abra o Explorador de arquivos**: isso pode ser feito, a abertura da saudação Menu Iniciar, ou pressionando atalho Win + E.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="aa3bc-148">**Navegue de item de "Este PC" toohello no lado esquerdo da saudação da janela de saudação. Isso alterará a menus de saudação disponíveis na faixa de opções de saudação. No menu de computador Olá, selecione "Mapear unidade de rede"**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Uma captura de tela de hello "Mapear unidade de rede" menu suspenso](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="aa3bc-150">**Caminho UNC de saudação de cópia de painel "Conectar-se" Olá Olá portal do Azure**: uma descrição detalhada de como toofind essas informações podem ser encontradas [aqui](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="aa3bc-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![caminho UNC de saudação no painel de conectar-se de armazenamento de arquivo do Azure Olá](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="aa3bc-152">**Selecione a letra da unidade hello e insira o caminho UNC hello.**</span><span class="sxs-lookup"><span data-stu-id="aa3bc-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Uma captura de tela da caixa de diálogo hello "Mapear unidade de rede"](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="aa3bc-154">**Saudação de usar o nome de conta de armazenamento anexado com `Azure\` como saudação de nome de usuário e uma chave de conta de armazenamento como senha hello.**</span><span class="sxs-lookup"><span data-stu-id="aa3bc-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Uma captura de tela da caixa de diálogo de credenciais de rede Olá](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="aa3bc-156">**Use o compartilhamento de arquivos do Azure como quiser**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-156">**Use Azure File share as desired**.</span></span>
    
    ![O compartilhamento de arquivos do Azure já está montado](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="aa3bc-158">**Quando você estiver pronto toodismount (ou desconecta) compartilhamento de arquivo do Azure hello, você pode fazer isso, clique com o botão direito na entrada Olá para compartilhamento de saudação em hello "locais de rede" no Explorador de arquivos e selecionando "Desconectar"**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="aa3bc-159">Montar o compartilhamento de arquivo do Azure Olá com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa3bc-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="aa3bc-160">**Compartilhamento de arquivo do Azure Olá toomount do comando de uso a seguir de saudação**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="aa3bc-161">**Compartilhamento de arquivo do Azure Use Olá conforme desejado**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="aa3bc-162">**Quando tiver terminado, desmontar o compartilhamento de arquivo do Azure hello usando o comando a seguir de saudação**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="aa3bc-163">Você pode usar o hello `-Persist` parâmetro `New-PSDrive` toomake Olá restante de toohello visíveis de compartilhamento de arquivo do Azure do hello SO enquanto montado.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="aa3bc-164">Montar o compartilhamento de arquivos do Azure Olá Prompt de comando</span><span class="sxs-lookup"><span data-stu-id="aa3bc-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="aa3bc-165">**Compartilhamento de arquivo do Azure Olá toomount do comando de uso a seguir de saudação**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="aa3bc-166">**Compartilhamento de arquivo do Azure Use Olá conforme desejado**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="aa3bc-167">**Quando tiver terminado, desmontar o compartilhamento de arquivo do Azure hello usando o comando a seguir de saudação**.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="aa3bc-168">Você pode configurar hello Azure arquivo compartilhamento tooautomatically reconectar-se na reinicialização pelas credenciais de saudação persistentes no Windows.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="aa3bc-169">saudação de comando a seguir será mantido credenciais hello:</span><span class="sxs-lookup"><span data-stu-id="aa3bc-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="aa3bc-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa3bc-170">Next steps</span></span>
<span data-ttu-id="aa3bc-171">Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3bc-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="aa3bc-172">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="aa3bc-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="aa3bc-173">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="aa3bc-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="aa3bc-174">Artigos e vídeos conceituais</span><span class="sxs-lookup"><span data-stu-id="aa3bc-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="aa3bc-175">Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="aa3bc-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="aa3bc-176">Como toouse armazenamento de arquivo do Azure com Linux</span><span class="sxs-lookup"><span data-stu-id="aa3bc-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="aa3bc-177">Suporte de ferramentas para o armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="aa3bc-178">Usando o PowerShell do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="aa3bc-179">Como toouse AzCopy com o armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="aa3bc-180">Usando Olá CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="aa3bc-181">Solução de problemas do armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="aa3bc-182">Postagens no blog</span><span class="sxs-lookup"><span data-stu-id="aa3bc-182">Blog posts</span></span>
* [<span data-ttu-id="aa3bc-183">O Armazenamento de arquivos do Azure agora está disponível ao público geral</span><span class="sxs-lookup"><span data-stu-id="aa3bc-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="aa3bc-184">Por dentro do Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="aa3bc-185">Apresentando o serviço de arquivo do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aa3bc-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="aa3bc-186">Migrando dados tooAzure arquivo</span><span class="sxs-lookup"><span data-stu-id="aa3bc-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="aa3bc-187">Referência</span><span class="sxs-lookup"><span data-stu-id="aa3bc-187">Reference</span></span>
* [<span data-ttu-id="aa3bc-188">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="aa3bc-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="aa3bc-189">Referência à API REST do serviço de arquivos</span><span class="sxs-lookup"><span data-stu-id="aa3bc-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
