---
title: "Solução de problemas de armazenamento de Arquivos do Azure no Linux | Microsoft Docs"
description: "Solução de problemas de armazenamento de Arquivos do Azure no Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 0cab2e3540afdbdc64cb77fca4b9219c77258166
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="79c87-103">Solucionar problemas de armazenamento de Arquivos do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="79c87-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="79c87-104">Este artigo lista os problemas comuns relacionados ao armazenamento de Arquivos do Microsoft Azure quando você se conecta em clientes Linux.</span><span class="sxs-lookup"><span data-stu-id="79c87-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="79c87-105">Também fornece as possíveis causas e resoluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="79c87-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="79c87-106">“[permissão negada] Cota de disco excedida” ao tentar abrir um arquivo</span><span class="sxs-lookup"><span data-stu-id="79c87-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="79c87-107">No Linux, você recebe uma mensagem de erro semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="79c87-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="79c87-108">**<filename> [permissão negada] Cota de disco excedida**</span><span class="sxs-lookup"><span data-stu-id="79c87-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="79c87-109">Causa</span><span class="sxs-lookup"><span data-stu-id="79c87-109">Cause</span></span>

<span data-ttu-id="79c87-110">Você atingiu o limite máximo de identificadores abertos simultâneos permitidos para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="79c87-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="79c87-111">Solução</span><span class="sxs-lookup"><span data-stu-id="79c87-111">Solution</span></span>

<span data-ttu-id="79c87-112">Reduza o número de identificadores abertos simultâneos fechando alguns deles e repita a operação.</span><span class="sxs-lookup"><span data-stu-id="79c87-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="79c87-113">Para obter mais informações, consulte [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79c87-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="79c87-114">Cópia de arquivos bidirecional lenta no armazenamento de Arquivos do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="79c87-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="79c87-115">Se você não tem um requisito de tamanho de E/S mínimo específico, recomendamos que você use 1 MB de tamanho de E/S para um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="79c87-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="79c87-116">Se você sabe o tamanho final de um arquivo que está estendendo com gravações e o software não apresenta problemas de compatibilidade quando a parte final não escrita do arquivo contém zeros, defina o tamanho do arquivo antecipadamente, em vez de realizar cada gravação como uma gravação de extensão.</span><span class="sxs-lookup"><span data-stu-id="79c87-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="79c87-117">Use o método de cópia correto:</span><span class="sxs-lookup"><span data-stu-id="79c87-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="79c87-118">Use o [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="79c87-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="79c87-119">Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre compartilhamentos de arquivos e um computador local.</span><span class="sxs-lookup"><span data-stu-id="79c87-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="79c87-120">“Erro de montagem (112): o host está inativo” devido a um tempo limite de reconexão</span><span class="sxs-lookup"><span data-stu-id="79c87-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="79c87-121">Um erro de montagem “112” ocorre no cliente Linux quando o cliente ficou ocioso por um longo período.</span><span class="sxs-lookup"><span data-stu-id="79c87-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="79c87-122">Após um tempo ocioso estendido, o cliente se desconecta e a conexão atinge o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="79c87-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="79c87-123">Causa</span><span class="sxs-lookup"><span data-stu-id="79c87-123">Cause</span></span>

<span data-ttu-id="79c87-124">A conexão pode ficar ociosa pelos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="79c87-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="79c87-125">Falhas de comunicação de rede que impedem o restabelecimento de uma conexão TCP com o servidor quando a opção de montagem “reversível” padrão é usada</span><span class="sxs-lookup"><span data-stu-id="79c87-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="79c87-126">Correções de reconexão recentes que não estão presentes nos kernels mais antigos</span><span class="sxs-lookup"><span data-stu-id="79c87-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="79c87-127">Solução</span><span class="sxs-lookup"><span data-stu-id="79c87-127">Solution</span></span>

<span data-ttu-id="79c87-128">Esse problema de reconexão no kernel do Linux agora foi corrigido como parte das seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="79c87-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- [<span data-ttu-id="79c87-129">Corrigir a reconexão para não adiar a sessão smb3 por muito tempo após a reconexão do soquete</span><span class="sxs-lookup"><span data-stu-id="79c87-129">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="79c87-130">Chamar o serviço de eco imediatamente após a reconexão do soquete</span><span class="sxs-lookup"><span data-stu-id="79c87-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="79c87-131">CIFS: corrigir uma possível corrupção de memória durante a reconexão</span><span class="sxs-lookup"><span data-stu-id="79c87-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="79c87-132">CIFS: corrigir um possível bloqueio duplo de mutex durante a reconexão (para kernel v4.9 e posterior)</span><span class="sxs-lookup"><span data-stu-id="79c87-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="79c87-133">No entanto, essas alterações ainda podem não ter sido portadas para todas as distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="79c87-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="79c87-134">Essa correção e outras correções de reconexão foram feitas nos seguintes kernels populares do Linux: 4.4.40, 4.8.16 e 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="79c87-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="79c87-135">Obtenha essa correção fazendo upgrade para uma dessas versões recomendadas de kernel.</span><span class="sxs-lookup"><span data-stu-id="79c87-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="79c87-136">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="79c87-136">Workaround</span></span>

<span data-ttu-id="79c87-137">Resolva esse problema especificando uma montagem rígida.</span><span class="sxs-lookup"><span data-stu-id="79c87-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="79c87-138">Isso força o cliente a aguardar até que uma conexão seja estabelecida ou até que ela seja interrompida explicitamente e possa ser usada para evitar erros devido a tempos limite de rede.</span><span class="sxs-lookup"><span data-stu-id="79c87-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="79c87-139">No entanto, essa solução alternativa pode causar esperas indefinidas.</span><span class="sxs-lookup"><span data-stu-id="79c87-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="79c87-140">Esteja preparado para interromper conexões, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="79c87-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="79c87-141">Se você não pode atualizar para as últimas versões do kernel, resolva esse problema mantendo um arquivo no compartilhamento de arquivos do Azure no qual se grava a cada 30 segundos ou menos.</span><span class="sxs-lookup"><span data-stu-id="79c87-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="79c87-142">Essa deve ser uma operação de gravação, como regravar a data de criação ou de modificação no arquivo.</span><span class="sxs-lookup"><span data-stu-id="79c87-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="79c87-143">Caso contrário, você poderá obter resultados em cache e a operação poderá não disparar a reconexão.</span><span class="sxs-lookup"><span data-stu-id="79c87-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="79c87-144">“Erro de montagem (115): operação em andamento” durante a montagem do armazenamento de Arquivos do Azure usando o SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="79c87-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="79c87-145">Causa</span><span class="sxs-lookup"><span data-stu-id="79c87-145">Cause</span></span>

<span data-ttu-id="79c87-146">Algumas distribuições do Linux ainda não dão suporte para os recursos de criptografia do SMB 3.0, por isso os usuários poderão receber uma mensagem de erro “115” se tentarem montar o Armazenamento de Arquivos do Azure usando o SMB 3.0, devido a um recurso ausente.</span><span class="sxs-lookup"><span data-stu-id="79c87-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="79c87-147">Solução</span><span class="sxs-lookup"><span data-stu-id="79c87-147">Solution</span></span>

<span data-ttu-id="79c87-148">O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="79c87-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="79c87-149">Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure.</span><span class="sxs-lookup"><span data-stu-id="79c87-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="79c87-150">No momento da publicação deste artigo, essa funcionalidade foi retrocompatibilizada para o Ubuntu 17.04 e Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="79c87-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="79c87-151">Se seu cliente SMB do Linux não der suporte à criptografia, monte o Armazenamento de Arquivos do Azure usando o SMB 2.1 em uma VM Linux do Azure que esteja no mesmo datacenter que a conta de Armazenamento de Arquivos.</span><span class="sxs-lookup"><span data-stu-id="79c87-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="79c87-152">Desempenho lento em um compartilhamento de arquivos do Azure montado em uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="79c87-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="79c87-153">Causa</span><span class="sxs-lookup"><span data-stu-id="79c87-153">Cause</span></span>

<span data-ttu-id="79c87-154">Uma possível causa da lentidão no desempenho é o cache desabilitado.</span><span class="sxs-lookup"><span data-stu-id="79c87-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="79c87-155">Solução</span><span class="sxs-lookup"><span data-stu-id="79c87-155">Solution</span></span>

<span data-ttu-id="79c87-156">Para verificar se o cache está desabilitado, procure a entrada **cache=**.</span><span class="sxs-lookup"><span data-stu-id="79c87-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="79c87-157">**Cache=none** indica que o cache está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="79c87-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="79c87-158">Remonte o compartilhamento usando o comando de montagem padrão ou adicionando explicitamente a opção **cache=strict** ao comando de montagem para garantir que o modo de cache padrão ou de cache “strict” seja habilitado.</span><span class="sxs-lookup"><span data-stu-id="79c87-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="79c87-159">Em alguns cenários, a opção de montagem **serverino** pode fazer com que o comando **ls** execute stat em cada entrada do diretório.</span><span class="sxs-lookup"><span data-stu-id="79c87-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="79c87-160">Esse comportamento resulta na degradação do desempenho quando você está listando um diretório grande.</span><span class="sxs-lookup"><span data-stu-id="79c87-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="79c87-161">Verifique as opções de montagem na entrada **/etc/fstab**:</span><span class="sxs-lookup"><span data-stu-id="79c87-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="79c87-162">Também verifique se as opções corretas estão sendo usadas executando o comando **sudo mount | grep cifs** e verificando sua saída, como na seguinte saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="79c87-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="79c87-163">Se a opção **cache=strict** ou **serverino** não estiver presente, desmonte e monte o armazenamento de Arquivos do Azure novamente executando o comando de montagem da [documentação](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="79c87-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="79c87-164">Em seguida, verifique novamente se a entrada **/etc/fstab** tem as opções corretas.</span><span class="sxs-lookup"><span data-stu-id="79c87-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="79c87-165">Os carimbos de data/hora foram perdidos durante a cópia de arquivos do Windows para o Linux</span><span class="sxs-lookup"><span data-stu-id="79c87-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="79c87-166">Nas plataformas Unix/Linux, o comando **cp -p** falhará se os arquivos 1 e 2 pertencerem a diferentes usuários.</span><span class="sxs-lookup"><span data-stu-id="79c87-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="79c87-167">Causa</span><span class="sxs-lookup"><span data-stu-id="79c87-167">Cause</span></span>

<span data-ttu-id="79c87-168">O sinalizador de força **f** em COPYFILE resulta na execução de **cp -p -f** no Unix.</span><span class="sxs-lookup"><span data-stu-id="79c87-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="79c87-169">Esse comando também não preserva o carimbo de data/hora do arquivo que você não possui.</span><span class="sxs-lookup"><span data-stu-id="79c87-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="79c87-170">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="79c87-170">Workaround</span></span>

<span data-ttu-id="79c87-171">Use o usuário da conta de armazenamento para copiar os arquivos:</span><span class="sxs-lookup"><span data-stu-id="79c87-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="79c87-172">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="79c87-172">Need help?</span></span> <span data-ttu-id="79c87-173">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="79c87-173">Contact support.</span></span>

<span data-ttu-id="79c87-174">Caso ainda precise de ajuda, [contate o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="79c87-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
