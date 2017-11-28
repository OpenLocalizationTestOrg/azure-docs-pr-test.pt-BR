---
title: problemas de armazenamento de arquivo do Azure aaaTroubleshoot no Linux | Microsoft Docs
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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="db78b-103">Solucionar problemas de armazenamento de Arquivos do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="db78b-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="db78b-104">Este artigo lista os problemas comuns que estão relacionada tooMicrosoft armazenamento de arquivo do Azure durante a conexão de clientes do Linux.</span><span class="sxs-lookup"><span data-stu-id="db78b-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="db78b-105">Também fornece as possíveis causas e resoluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="db78b-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="db78b-106">"cota de disco [permissão negada] excedida" ao tentar tooopen um arquivo</span><span class="sxs-lookup"><span data-stu-id="db78b-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="db78b-107">No Linux, você recebe uma mensagem de erro semelhante a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="db78b-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="db78b-108">**<filename> [permissão negada] Cota de disco excedida**</span><span class="sxs-lookup"><span data-stu-id="db78b-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="db78b-109">Causa</span><span class="sxs-lookup"><span data-stu-id="db78b-109">Cause</span></span>

<span data-ttu-id="db78b-110">Você atingiu o limite superior de saudação de identificadores abertos simultâneos permitidas para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="db78b-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="db78b-111">Solução</span><span class="sxs-lookup"><span data-stu-id="db78b-111">Solution</span></span>

<span data-ttu-id="db78b-112">Reduza o número de saudação de identificadores abertos simultâneos fechando alguns identificadores e, em seguida, repita a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="db78b-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="db78b-113">Para obter mais informações, consulte [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="db78b-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="db78b-114">Arquivos lenta copiando tooand do armazenamento de arquivo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="db78b-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="db78b-115">Se você não tiver um requisito de tamanho de e/s mínimo específico, é recomendável que você use 1 MB como Olá tamanho de e/s para o desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="db78b-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="db78b-116">Se você conhece Olá o tamanho final de um arquivo que você estiver estendendo usando gravações, e o software não ter problemas de compatibilidade quando uma final não gravada no arquivo hello contém zeros, em seguida, definir o tamanho do arquivo de Olá antecipadamente, em vez de fazer cada gravação uma extensão gravação.</span><span class="sxs-lookup"><span data-stu-id="db78b-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="db78b-117">Use o método de cópia de direito de saudação:</span><span class="sxs-lookup"><span data-stu-id="db78b-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="db78b-118">Use o [AzCopy](storage-use-azcopy.md#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="db78b-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="db78b-119">Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre compartilhamentos de arquivos e um computador local.</span><span class="sxs-lookup"><span data-stu-id="db78b-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="db78b-120">“Erro de montagem (112): o host está inativo” devido a um tempo limite de reconexão</span><span class="sxs-lookup"><span data-stu-id="db78b-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="db78b-121">Ocorrerá um erro de montagem "112" no cliente do Linux hello quando o cliente Olá ficar ocioso por um longo tempo.</span><span class="sxs-lookup"><span data-stu-id="db78b-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="db78b-122">Após um longo tempo ocioso, Olá cliente se desconecta e conexão Olá expire.</span><span class="sxs-lookup"><span data-stu-id="db78b-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="db78b-123">Causa</span><span class="sxs-lookup"><span data-stu-id="db78b-123">Cause</span></span>

<span data-ttu-id="db78b-124">conexão Olá pode ficar ociosa para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="db78b-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="db78b-125">Falhas de comunicação de rede que impedem a estabelecer novamente um servidor de toohello de conexão TCP quando a opção de montagem "soft" hello padrão é usada</span><span class="sxs-lookup"><span data-stu-id="db78b-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="db78b-126">Correções de reconexão recentes que não estão presentes nos kernels mais antigos</span><span class="sxs-lookup"><span data-stu-id="db78b-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="db78b-127">Solução</span><span class="sxs-lookup"><span data-stu-id="db78b-127">Solution</span></span>

<span data-ttu-id="db78b-128">Esse problema de reconexão do kernel do Linux Olá agora é fixo como parte da saudação as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="db78b-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="db78b-129">Correção de reconexão toonot adiar smb3 sessão reconectar depois reconectar-se do soquete</span><span class="sxs-lookup"><span data-stu-id="db78b-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="db78b-130">Chamar o serviço de eco imediatamente após a reconexão do soquete</span><span class="sxs-lookup"><span data-stu-id="db78b-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="db78b-131">CIFS: corrigir uma possível corrupção de memória durante a reconexão</span><span class="sxs-lookup"><span data-stu-id="db78b-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="db78b-132">CIFS: corrigir um possível bloqueio duplo de mutex durante a reconexão (para kernel v4.9 e posterior)</span><span class="sxs-lookup"><span data-stu-id="db78b-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="db78b-133">No entanto, essas alterações não podem ser movidas ainda tooall Olá distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="db78b-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="db78b-134">Essa correção e outras correções de reconexão são feitas no hello populares kernels do Linux a seguir: 4.4.40, 4.8.16 e 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="db78b-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="db78b-135">Você pode obter essa correção atualizando tooone dessas versões de kernel recomendado.</span><span class="sxs-lookup"><span data-stu-id="db78b-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="db78b-136">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="db78b-136">Workaround</span></span>

<span data-ttu-id="db78b-137">Resolva esse problema especificando uma montagem rígida.</span><span class="sxs-lookup"><span data-stu-id="db78b-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="db78b-138">Isso força Olá cliente toowait até que uma conexão seja estabelecida ou até que ela seja interrompida explicitamente e pode ser usado tooprevent erros devido a tempos limite de rede.</span><span class="sxs-lookup"><span data-stu-id="db78b-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="db78b-139">No entanto, essa solução alternativa pode causar esperas indefinidas.</span><span class="sxs-lookup"><span data-stu-id="db78b-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="db78b-140">Ser preparados toostop conexões conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="db78b-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="db78b-141">Se você não pode atualizar versões mais recentes de kernel toohello, você pode contornar esse problema mantendo um arquivo em um compartilhamento de arquivo do Azure Olá gravar tooevery 30 segundos ou menos.</span><span class="sxs-lookup"><span data-stu-id="db78b-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="db78b-142">Isso deve ser uma operação de gravação, como reconfiguração Olá criado ou data de modificação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="db78b-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="db78b-143">Caso contrário, você pode obter resultados em cache e a operação não pode disparar a reconexão hello.</span><span class="sxs-lookup"><span data-stu-id="db78b-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="db78b-144">“Erro de montagem (115): operação em andamento” durante a montagem do armazenamento de Arquivos do Azure usando o SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="db78b-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="db78b-145">Causa</span><span class="sxs-lookup"><span data-stu-id="db78b-145">Cause</span></span>

<span data-ttu-id="db78b-146">Algumas distribuições do Linux não ainda dão suporte a recursos de criptografia do SMB 3.0 e os usuários podem receber uma mensagem de erro "115" se tentarem toomount armazenamento de arquivo do Azure usando o SMB 3.0 devido a um recurso ausente.</span><span class="sxs-lookup"><span data-stu-id="db78b-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="db78b-147">Solução</span><span class="sxs-lookup"><span data-stu-id="db78b-147">Solution</span></span>

<span data-ttu-id="db78b-148">O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="db78b-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="db78b-149">Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure.</span><span class="sxs-lookup"><span data-stu-id="db78b-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="db78b-150">Em tempo de saudação da publicação, essa funcionalidade foi backported tooUbuntu 17.04 e 16.10 do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="db78b-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="db78b-151">Se o cliente SMB Linux não dá suporte à criptografia, montar o armazenamento de arquivo do Azure usando o SMB 2.1 de uma VM do Linux do Azure que está em Olá mesmo data center como Olá conta de armazenamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="db78b-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="db78b-152">Desempenho lento em um compartilhamento de arquivos do Azure montado em uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="db78b-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="db78b-153">Causa</span><span class="sxs-lookup"><span data-stu-id="db78b-153">Cause</span></span>

<span data-ttu-id="db78b-154">Uma possível causa da lentidão no desempenho é o cache desabilitado.</span><span class="sxs-lookup"><span data-stu-id="db78b-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="db78b-155">Solução</span><span class="sxs-lookup"><span data-stu-id="db78b-155">Solution</span></span>

<span data-ttu-id="db78b-156">toocheck se o cache é desabilitado, procure Olá **cache =** entrada.</span><span class="sxs-lookup"><span data-stu-id="db78b-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="db78b-157">**Cache=none** indica que o cache está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="db78b-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="db78b-158">Remontagem Olá compartilhamento usando o comando de montagem saudação padrão ou adicione explicitamente Olá **cache = estrito** opção toohello montagem comando tooensure padrão cache ou "estrito" modo de cache está habilitado.</span><span class="sxs-lookup"><span data-stu-id="db78b-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="db78b-159">Em alguns cenários, Olá **serverino** a opção de montagem pode causar Olá **ls** stat no comando toorun em cada entrada de diretório.</span><span class="sxs-lookup"><span data-stu-id="db78b-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="db78b-160">Esse comportamento resulta na degradação do desempenho quando você está listando um diretório grande.</span><span class="sxs-lookup"><span data-stu-id="db78b-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="db78b-161">Você pode verificar as opções de montagem de saudação em seu **/etc/fstab** entrada:</span><span class="sxs-lookup"><span data-stu-id="db78b-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="db78b-162">Você também pode verificar se as opções corretas de saudação estão sendo usadas executando Olá **sudo montagem | grep cifs** comando e a verificação de sua saída, como Olá saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="db78b-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="db78b-163">Se hello **cache = estrito** ou **serverino** opção é não apresentar, desmontar e montar o armazenamento de arquivo do Azure novamente, executando o comando de montagem de saudação do hello [documentação](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="db78b-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="db78b-164">Em seguida, verificar que Olá **/etc/fstab** entrada tem opções corretas de saudação.</span><span class="sxs-lookup"><span data-stu-id="db78b-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="db78b-165">Os carimbos de hora foram perdidos ao copiar arquivos do Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="db78b-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="db78b-166">Em plataformas Unix/Linux, Olá **cp -p** comando falhará se o arquivo 1 e 2 pertencentes a diferentes usuários.</span><span class="sxs-lookup"><span data-stu-id="db78b-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="db78b-167">Causa</span><span class="sxs-lookup"><span data-stu-id="db78b-167">Cause</span></span>

<span data-ttu-id="db78b-168">Olá sinalizador force **f** em COPYFILE resulta em execução **cp -p -f** em Unix.</span><span class="sxs-lookup"><span data-stu-id="db78b-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="db78b-169">Este comando também falha toopreserve Olá carimbo de data do arquivo hello que você não possui.</span><span class="sxs-lookup"><span data-stu-id="db78b-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="db78b-170">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="db78b-170">Workaround</span></span>

<span data-ttu-id="db78b-171">Use o usuário da conta de armazenamento Olá para copiar arquivos de saudação:</span><span class="sxs-lookup"><span data-stu-id="db78b-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="db78b-172">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="db78b-172">Need help?</span></span> <span data-ttu-id="db78b-173">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="db78b-173">Contact support.</span></span>

<span data-ttu-id="db78b-174">Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget o problema foi resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="db78b-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
