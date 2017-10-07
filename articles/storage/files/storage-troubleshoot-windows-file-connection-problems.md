---
title: problemas de armazenamento de arquivo do Azure aaaTroubleshoot no Windows | Microsoft Docs
description: "Solução de problemas de Armazenamento de Arquivos do Azure File no Windows"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="02256-103">Solução de problemas de Armazenamento de Arquivos do Azure File no Windows</span><span class="sxs-lookup"><span data-stu-id="02256-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="02256-104">Este artigo lista os problemas comuns que estão relacionada tooMicrosoft armazenamento de arquivo do Azure durante a conexão de clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="02256-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="02256-105">Também fornece as possíveis causas e resoluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="02256-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="02256-106">Além de solução de problemas de toohello as etapas neste artigo, você também pode usar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para garantir que Windows hello o ambiente do cliente tem pré-requisitos corretos.</span><span class="sxs-lookup"><span data-stu-id="02256-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="02256-107">AzFileDiagnostics automatiza a detecção da maioria dos sintomas Olá mencionados neste artigo e ajuda a configurar o desempenho ideal do ambiente tooget.</span><span class="sxs-lookup"><span data-stu-id="02256-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="02256-108">Você também pode encontrar essas informações no hello [solução de problemas de compartilhamentos de arquivos do Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que fornece etapas tooassist com problemas de compartilhamentos de arquivos do Azure conectando/mapeamento/montagem.</span><span class="sxs-lookup"><span data-stu-id="02256-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="02256-109">Erro 53, Erro 67 ou Erro 87 ao montar ou desmontar um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="02256-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="02256-110">Quando você tenta toomount um compartilhamento de arquivos do local ou de um datacenter diferente, você poderá receber Olá os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="02256-111">Ocorreu um erro de sistema 53.</span><span class="sxs-lookup"><span data-stu-id="02256-111">System error 53 has occurred.</span></span> <span data-ttu-id="02256-112">caminho de rede Olá não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="02256-112">hello network path was not found.</span></span>
- <span data-ttu-id="02256-113">Ocorreu um erro de sistema 67.</span><span class="sxs-lookup"><span data-stu-id="02256-113">System error 67 has occurred.</span></span> <span data-ttu-id="02256-114">nome da rede Olá não pode ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="02256-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="02256-115">Ocorreu um erro de sistema 87.</span><span class="sxs-lookup"><span data-stu-id="02256-115">System error 87 has occurred.</span></span> <span data-ttu-id="02256-116">Olá parâmetro está incorreto.</span><span class="sxs-lookup"><span data-stu-id="02256-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="02256-117">Causa 1: Canal de comunicação não criptografado</span><span class="sxs-lookup"><span data-stu-id="02256-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="02256-118">Por motivos de segurança, conexões tooAzure compartilhamentos de arquivos estão bloqueados se o canal de comunicação Olá não é criptografado e tentativa de conexão de saudação não é feita de Olá mesmo datacenter onde residem os compartilhamentos de arquivos do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="02256-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="02256-119">Criptografia de canal de comunicação é fornecida apenas se o sistema operacional do cliente do usuário Olá dá suporte a criptografia SMB.</span><span class="sxs-lookup"><span data-stu-id="02256-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="02256-120">O Windows 8, o Windows Server 2012 e versões posteriores de cada solicitação de negociação de sistema que inclua o SMB 3.0, que dá suporte à criptografia.</span><span class="sxs-lookup"><span data-stu-id="02256-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="02256-121">Solução para a causa 1</span><span class="sxs-lookup"><span data-stu-id="02256-121">Solution for cause 1</span></span>

<span data-ttu-id="02256-122">Conecte-se de um cliente que executa um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="02256-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="02256-123">Atende aos requisitos de saudação do Windows 8 e Windows Server 2012 ou versões posteriores</span><span class="sxs-lookup"><span data-stu-id="02256-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="02256-124">Conecta-se em uma máquina virtual no hello mesmo datacenter como Olá conta de armazenamento do Azure que é usada para compartilhamento de arquivos do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="02256-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="02256-125">Causa 2: A porta 445 está bloqueada</span><span class="sxs-lookup"><span data-stu-id="02256-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="02256-126">Erro de sistema 53 ou sistema 67 pode ocorrer se a porta 445 comunicação de saída tooan arquivo do Azure storage datacenter está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="02256-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="02256-127">Resumo de saudação toosee de provedores que permitir ou impedir o acesso de porta 445, ir muito[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="02256-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="02256-128">toounderstand se essa é a razão de saudação atrás de mensagem de "Erro de sistema 53" Olá, você pode usar o ponto de extremidade do Portqry tooquery Olá TCP:445.</span><span class="sxs-lookup"><span data-stu-id="02256-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="02256-129">Se o ponto de extremidade do hello TCP:445 é exibido como filtrado, Olá a porta TCP será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="02256-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="02256-130">Veja um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="02256-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="02256-131">Se a porta TCP 445 está bloqueada por uma regra de caminho de rede hello, você verá Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="02256-132">Para obter mais informações sobre como toouse Portqry, consulte [descrição do utilitário de linha de comando do hello Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="02256-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="02256-133">Solução para a causa 2</span><span class="sxs-lookup"><span data-stu-id="02256-133">Solution for cause 2</span></span>

<span data-ttu-id="02256-134">Trabalhar com a porta de tooopen do departamento de IT 445 saída muito[intervalos de IP do Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="02256-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="02256-135">Causa 3: NTLMv1 está habilitado</span><span class="sxs-lookup"><span data-stu-id="02256-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="02256-136">Erro de sistema 53 ou sistema 87 pode ocorrer se a comunicação NTLMv1 está habilitada no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="02256-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="02256-137">O Armazenamento de Arquivos do Azure dá suporte apenas à autenticação NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="02256-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="02256-138">Ter NTLMv1 habilitado faz com que o cliente esteja menos seguro.</span><span class="sxs-lookup"><span data-stu-id="02256-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="02256-139">Portanto, a comunicação será bloqueada para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="02256-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="02256-140">toodetermine se esta é a causa Olá Olá erro, verifique se esse Olá seguinte subchave do registro está definida tooa valor de 3:</span><span class="sxs-lookup"><span data-stu-id="02256-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="02256-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="02256-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="02256-142">Para obter mais informações, consulte Olá [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tópico no TechNet.</span><span class="sxs-lookup"><span data-stu-id="02256-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="02256-143">Solução para a causa 3</span><span class="sxs-lookup"><span data-stu-id="02256-143">Solution for cause 3</span></span>

<span data-ttu-id="02256-144">Reverter Olá **LmCompatibilityLevel** toohello valor padrão 3 na seguinte subchave do registro de saudação do valor:</span><span class="sxs-lookup"><span data-stu-id="02256-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="02256-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="02256-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="02256-146">Erro 1816 "não há cota suficiente está disponível tooprocess este comando" quando você copia tooan compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="02256-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="02256-147">Causa</span><span class="sxs-lookup"><span data-stu-id="02256-147">Cause</span></span>

<span data-ttu-id="02256-148">Erro 1816 ocorre quando você atingir o limite superior de saudação de identificadores abertos simultâneos permitidas para um arquivo no computador de saudação em que o compartilhamento de arquivo hello está sendo montado.</span><span class="sxs-lookup"><span data-stu-id="02256-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="02256-149">Solução</span><span class="sxs-lookup"><span data-stu-id="02256-149">Solution</span></span>

<span data-ttu-id="02256-150">Reduzir o número de saudação de identificadores abertos simultâneos fechando alguns identificadores e, em seguida, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="02256-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="02256-151">Para obter mais informações, consulte [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02256-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="02256-152">Arquivos lenta copiando tooand do armazenamento de arquivo do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="02256-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="02256-153">Você pode ver o desempenho lento ao tentar tootransfer arquivos toohello serviço arquivo do Azure.</span><span class="sxs-lookup"><span data-stu-id="02256-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="02256-154">Se você não tiver um requisito de tamanho de e/s mínimo específico, é recomendável que você use 1 MB como Olá tamanho de e/s para o desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="02256-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="02256-155">Se você souber o tamanho final de saudação de um arquivo que você estiver estendendo com grava e o software não tem problemas de compatibilidade quando final não gravada no arquivo hello hello contém zeros, em seguida, conjunto Olá tamanho do arquivo com antecedência, em vez de fazer cada gravação uma gravação estendendo.</span><span class="sxs-lookup"><span data-stu-id="02256-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="02256-156">Use o método de cópia de direito de saudação:</span><span class="sxs-lookup"><span data-stu-id="02256-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="02256-157">Use o [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="02256-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="02256-158">Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre um compartilhamento de arquivos e um computador local.</span><span class="sxs-lookup"><span data-stu-id="02256-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="02256-159">Considerações para Windows 8.1 ou Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="02256-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="02256-160">Para clientes que executam o Windows 8.1 ou Windows Server 2012 R2, certifique-se de que Olá [KB3114025](https://support.microsoft.com/help/3114025) hotfix foi instalado.</span><span class="sxs-lookup"><span data-stu-id="02256-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="02256-161">Este hotfix melhora o desempenho de saudação de criar e fechar identificadores.</span><span class="sxs-lookup"><span data-stu-id="02256-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="02256-162">Você pode executar Olá toocheck de script a seguir se Olá hotfix foi instalado:</span><span class="sxs-lookup"><span data-stu-id="02256-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="02256-163">Se o hotfix foi instalado, hello seguinte saída é exibida:</span><span class="sxs-lookup"><span data-stu-id="02256-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="02256-164">As imagens do Windows Server 2012 R2 no Azure Marketplace têm o hotfix KB3114025 instalado por padrão desde dezembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="02256-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="02256-165">Nenhuma pasta com uma letra de unidade em **Meu Computador**</span><span class="sxs-lookup"><span data-stu-id="02256-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="02256-166">Se você mapear um compartilhamento de arquivos do Azure como administrador por meio do uso de rede, o compartilhamento de saudação aparece toobe ausente.</span><span class="sxs-lookup"><span data-stu-id="02256-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="02256-167">Causa</span><span class="sxs-lookup"><span data-stu-id="02256-167">Cause</span></span>

<span data-ttu-id="02256-168">Por padrão, o Explorador de Arquivos do Windows não é executado como administrador.</span><span class="sxs-lookup"><span data-stu-id="02256-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="02256-169">Se você executar o uso de rede em um prompt de comando administrativo, Mapear unidade de rede hello como um administrador.</span><span class="sxs-lookup"><span data-stu-id="02256-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="02256-170">Como unidades mapeadas são centrado no usuário, conta de usuário de saudação que está conectada não exibe Olá unidades se eles estão montados em uma conta de usuário diferente.</span><span class="sxs-lookup"><span data-stu-id="02256-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="02256-171">Solução</span><span class="sxs-lookup"><span data-stu-id="02256-171">Solution</span></span>
<span data-ttu-id="02256-172">Compartilhamento de saudação montagem de uma linha de comando não administrador.</span><span class="sxs-lookup"><span data-stu-id="02256-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="02256-173">Como alternativa, você pode seguir [neste tópico TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure Olá **EnableLinkedConnections** o valor do registro.</span><span class="sxs-lookup"><span data-stu-id="02256-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="02256-174">Comando NET use falhará se a conta de armazenamento Olá contém uma barra invertida</span><span class="sxs-lookup"><span data-stu-id="02256-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="02256-175">Causa</span><span class="sxs-lookup"><span data-stu-id="02256-175">Cause</span></span>

<span data-ttu-id="02256-176">comando net use de saudação interpreta uma barra invertida (/) como uma opção de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="02256-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="02256-177">Se o nome da sua conta de usuário começa com uma barra invertida, o mapeamento de unidade Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="02256-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="02256-178">Solução</span><span class="sxs-lookup"><span data-stu-id="02256-178">Solution</span></span>

<span data-ttu-id="02256-179">Você pode usar o hello etapas toowork problema Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="02256-180">Execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="02256-181">De um arquivo em lotes, você pode executar o comando de saudação desta forma:</span><span class="sxs-lookup"><span data-stu-id="02256-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="02256-182">Coloque aspas duplas em torno de saudação toowork de chave alternativa para esse problema – a menos que a barra de saudação é Olá primeiro caractere.</span><span class="sxs-lookup"><span data-stu-id="02256-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="02256-183">Se for, usar o modo interativo hello e insira sua senha separadamente ou regenerar sua chaves tooget uma chave que não começa com uma barra invertida.</span><span class="sxs-lookup"><span data-stu-id="02256-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="02256-184">O aplicativo ou serviço não pode acessar a unidade montada dos Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="02256-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="02256-185">Causa</span><span class="sxs-lookup"><span data-stu-id="02256-185">Cause</span></span>

<span data-ttu-id="02256-186">As unidades são montadas por usuário.</span><span class="sxs-lookup"><span data-stu-id="02256-186">Drives are mounted per user.</span></span> <span data-ttu-id="02256-187">Se seu aplicativo ou serviço estiver em execução sob uma conta de usuário diferente de saudação que Olá unidade montada, o aplicativo hello não verá unidade hello.</span><span class="sxs-lookup"><span data-stu-id="02256-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="02256-188">Solução</span><span class="sxs-lookup"><span data-stu-id="02256-188">Solution</span></span>

<span data-ttu-id="02256-189">Use uma saudação soluções a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="02256-190">Montar a unidade de saudação do hello mesma conta de usuário que contém o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="02256-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="02256-191">Você pode usar uma ferramenta como o PsExec.</span><span class="sxs-lookup"><span data-stu-id="02256-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="02256-192">Passe o nome de conta de armazenamento hello e a chave nos parâmetros de nome e senha de usuário de saudação do comando net use de saudação.</span><span class="sxs-lookup"><span data-stu-id="02256-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="02256-193">Depois de seguir estas instruções, você poderá receber Olá a seguinte mensagem de erro quando você executa o uso de rede para a conta de serviço de rede do sistema Olá: "Erro de sistema 1312 ocorreu.</span><span class="sxs-lookup"><span data-stu-id="02256-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="02256-194">Uma sessão de logon especificada não existe.</span><span class="sxs-lookup"><span data-stu-id="02256-194">A specified logon session does not exist.</span></span> <span data-ttu-id="02256-195">Talvez ela já tenha sido finalizada.”</span><span class="sxs-lookup"><span data-stu-id="02256-195">It may already have been terminated."</span></span> <span data-ttu-id="02256-196">Se isso ocorrer, verifique se esse nome de usuário de saudação que é passado toonet uso inclui informações de domínio (por exemplo: "[nome de conta de armazenamento]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="02256-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="02256-197">Erro "Você está copiando um arquivo de destino de tooa que não dá suporte à criptografia"</span><span class="sxs-lookup"><span data-stu-id="02256-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="02256-198">Quando um arquivo é copiado pela rede hello, arquivo hello é descriptografado no computador de origem hello, transmitidas em texto não criptografado e criptografados novamente no destino hello.</span><span class="sxs-lookup"><span data-stu-id="02256-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="02256-199">No entanto, você poderá ver o erro a seguir quando estiver tentando toocopy um arquivo criptografado de saudação: "Você está copiando destino Olá de tooa de arquivo que não dá suporte à criptografia".</span><span class="sxs-lookup"><span data-stu-id="02256-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="02256-200">Causa</span><span class="sxs-lookup"><span data-stu-id="02256-200">Cause</span></span>
<span data-ttu-id="02256-201">Esse problema pode ocorrer se você estiver usando o sistema de arquivos com criptografia (EFS).</span><span class="sxs-lookup"><span data-stu-id="02256-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="02256-202">Arquivos criptografados pelo BitLocker podem ser copiados tooAzure o armazenamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="02256-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="02256-203">No entanto, o Armazenamento de Arquivos do Azure não dá suporte a EFS NTFS.</span><span class="sxs-lookup"><span data-stu-id="02256-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="02256-204">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="02256-204">Workaround</span></span>
<span data-ttu-id="02256-205">toocopy um arquivo pela rede hello, você deve primeiro descriptografá-lo.</span><span class="sxs-lookup"><span data-stu-id="02256-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="02256-206">Use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="02256-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="02256-207">Saudação de uso **copiar /d** comando.</span><span class="sxs-lookup"><span data-stu-id="02256-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="02256-208">Olá criptografado permite que arquivos toobe salvo como arquivos descriptografados no destino hello.</span><span class="sxs-lookup"><span data-stu-id="02256-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="02256-209">Saudação de conjunto de chave do registro a seguir:</span><span class="sxs-lookup"><span data-stu-id="02256-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="02256-210">Caminho = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="02256-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="02256-211">Tipo de valor = DWORD</span><span class="sxs-lookup"><span data-stu-id="02256-211">Value type = DWORD</span></span>
  - <span data-ttu-id="02256-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="02256-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="02256-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="02256-213">Value = 1</span></span>

<span data-ttu-id="02256-214">Lembre-se de que essa chave de registro de saudação configuração afeta todas as operações de cópia que ficam toonetwork compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="02256-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="02256-215">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="02256-215">Need help?</span></span> <span data-ttu-id="02256-216">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="02256-216">Contact support.</span></span>
<span data-ttu-id="02256-217">Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget o problema foi resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="02256-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
