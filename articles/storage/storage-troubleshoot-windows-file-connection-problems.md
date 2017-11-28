---
title: "Solução de problemas de Armazenamento de Arquivos do Azure no Windows | Microsoft Docs"
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
ms.openlocfilehash: 71a8f4edf7776556b383f446e5aad007748ef090
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="b7673-103">Solução de problemas de Armazenamento de Arquivos do Azure File no Windows</span><span class="sxs-lookup"><span data-stu-id="b7673-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="b7673-104">Este artigo lista os problemas comuns relacionados ao Armazenamento de Arquivos do Microsoft Azure quando você se conecta a partir de clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="b7673-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="b7673-105">Ele também fornece possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="b7673-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="b7673-106">Além das etapas de solução de problemas neste artigo, você também pode usar o [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para garantir que o ambiente de cliente do Windows possui os pré-requisitos corretos.</span><span class="sxs-lookup"><span data-stu-id="b7673-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="b7673-107">O AzFileDiagnostics automatiza a detecção da maioria dos sintomas mencionados neste artigo e ajuda a configurar seu ambiente para obter um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="b7673-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="b7673-108">Você também pode encontrar essas informações na [Solução de problemas de Compartilhamentos de Arquivos do Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que fornece as etapas para ajudar você a resolver problemas de conexão/mapeamento/montagem de Compartilhamentos de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7673-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="b7673-109">Erro 53, Erro 67 ou Erro 87 ao montar ou desmontar um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b7673-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="b7673-110">Quando você tenta montar um compartilhamento de arquivos do local ou de um datacenter diferente, você poderá receber os seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="b7673-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="b7673-111">Ocorreu um erro de sistema 53.</span><span class="sxs-lookup"><span data-stu-id="b7673-111">System error 53 has occurred.</span></span> <span data-ttu-id="b7673-112">O caminho da rede não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="b7673-112">The network path was not found.</span></span>
- <span data-ttu-id="b7673-113">Ocorreu um erro de sistema 67.</span><span class="sxs-lookup"><span data-stu-id="b7673-113">System error 67 has occurred.</span></span> <span data-ttu-id="b7673-114">O nome de rede não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="b7673-114">The network name cannot be found.</span></span>
- <span data-ttu-id="b7673-115">Ocorreu um erro de sistema 87.</span><span class="sxs-lookup"><span data-stu-id="b7673-115">System error 87 has occurred.</span></span> <span data-ttu-id="b7673-116">O parâmetro está incorreto.</span><span class="sxs-lookup"><span data-stu-id="b7673-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="b7673-117">Causa 1: Canal de comunicação não criptografado</span><span class="sxs-lookup"><span data-stu-id="b7673-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="b7673-118">Por motivos de segurança, as conexões para compartilhamentos de arquivos do Azure são bloqueadas se o canal de comunicação não está criptografado e a tentativa de conexão não é feita do mesmo datacenter onde residem os compartilhamentos de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7673-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="b7673-119">A criptografia de canal de comunicação é fornecida somente quando o sistema operacional do cliente do usuário não dá suporte à criptografia SMB.</span><span class="sxs-lookup"><span data-stu-id="b7673-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="b7673-120">O Windows 8, o Windows Server 2012 e versões posteriores de cada solicitação de negociação de sistema que inclua o SMB 3.0, que dá suporte à criptografia.</span><span class="sxs-lookup"><span data-stu-id="b7673-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="b7673-121">Solução para a causa 1</span><span class="sxs-lookup"><span data-stu-id="b7673-121">Solution for cause 1</span></span>

<span data-ttu-id="b7673-122">Conecte-se a partir de um cliente que faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b7673-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="b7673-123">Atende aos requisitos do Windows 8 e Windows Server 2012 ou versões posteriores</span><span class="sxs-lookup"><span data-stu-id="b7673-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="b7673-124">Conecta-se a partir de uma máquina virtual no mesmo datacenter como a conta de armazenamento do Azure que é usada para o compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b7673-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="b7673-125">Causa 2: A porta 445 está bloqueada</span><span class="sxs-lookup"><span data-stu-id="b7673-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="b7673-126">Pode ocorrer um erro de sistema 53 ou erro de sistema 67 se a comunicação de saída na porta 445 para o datacenter do Armazenamento de Arquivos do Azure estiver bloqueada.</span><span class="sxs-lookup"><span data-stu-id="b7673-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="b7673-127">Para ver o resumo de ISPs que permitem ou proíbem o acesso a partir da porta 445, vá para [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7673-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="b7673-128">Para entender se esse é o motivo da mensagem "Erro de sistema 53", você pode usar o Portqry para consultar o ponto de extremidade TCP:445.</span><span class="sxs-lookup"><span data-stu-id="b7673-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="b7673-129">Se o ponto de extremidade TCP:445 é exibido como filtrado, a porta TCP está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="b7673-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="b7673-130">Veja um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="b7673-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="b7673-131">Se a porta TCP 445 está sendo bloqueado por uma regra ao longo do caminho de rede, você verá a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="b7673-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="b7673-132">Para saber mais sobre como usar Portqry, confira [Descrição do utilitário de linha de comando Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="b7673-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="b7673-133">Solução para a causa 2</span><span class="sxs-lookup"><span data-stu-id="b7673-133">Solution for cause 2</span></span>

<span data-ttu-id="b7673-134">Trabalhar com o seu departamento de TI para abrir a porta 445 com saída para [intervalos de IP do Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="b7673-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="b7673-135">Causa 3: NTLMv1 está habilitado</span><span class="sxs-lookup"><span data-stu-id="b7673-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="b7673-136">O erro de sistema 53 ou erro de sistema 87 também pode ocorrer se a comunicação NTLMv1 está habilitada no cliente.</span><span class="sxs-lookup"><span data-stu-id="b7673-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="b7673-137">O Armazenamento de Arquivos do Azure dá suporte apenas à autenticação NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="b7673-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="b7673-138">Ter NTLMv1 habilitado faz com que o cliente esteja menos seguro.</span><span class="sxs-lookup"><span data-stu-id="b7673-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="b7673-139">Portanto, a comunicação será bloqueada para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7673-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="b7673-140">Para verificar se essa é a causa do erro, verifique se a seguinte subchave do registro está definida como um valor de 3:</span><span class="sxs-lookup"><span data-stu-id="b7673-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="b7673-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="b7673-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="b7673-142">Para saber mais, confira o tópico [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) no TechNet.</span><span class="sxs-lookup"><span data-stu-id="b7673-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="b7673-143">Solução para a causa 3</span><span class="sxs-lookup"><span data-stu-id="b7673-143">Solution for cause 3</span></span>

<span data-ttu-id="b7673-144">Reverter o valor **LmCompatibilityLevel** para o valor padrão de 3 na seguinte subchave do registro:</span><span class="sxs-lookup"><span data-stu-id="b7673-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="b7673-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="b7673-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="b7673-146">Erro 1816 "Não há cota suficiente disponível para processar este comando" quando você copia para um compartilhamento de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b7673-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="b7673-147">Causa</span><span class="sxs-lookup"><span data-stu-id="b7673-147">Cause</span></span>

<span data-ttu-id="b7673-148">O Erro 1816 ocorre quando você atingir o limite superior de identificadores abertos simultâneos permitidos para um arquivo no computador onde o compartilhamento de arquivos está sendo montado.</span><span class="sxs-lookup"><span data-stu-id="b7673-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="b7673-149">Solução</span><span class="sxs-lookup"><span data-stu-id="b7673-149">Solution</span></span>

<span data-ttu-id="b7673-150">Reduza o número de identificadores abertos simultâneos fechando alguns identificadores e tentando novamente.</span><span class="sxs-lookup"><span data-stu-id="b7673-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="b7673-151">Para obter mais informações, veja [Lista de verificação de escalabilidade e desempenho do Armazenamento do Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="b7673-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="b7673-152">Cópia de arquivos mais lenta para e do Armazenamento de Arquivos do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="b7673-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="b7673-153">Você pode ver o desempenho lento ao tentar transferir arquivos para o Serviço de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7673-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="b7673-154">Se você não tem um requisito de tamanho de E/S mínimo específico, recomendamos que você use 1 MB de tamanho de E/S para um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="b7673-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="b7673-155">Se você sabe o tamanho final de um arquivo que você está estendendo com gravações e o seu software não tem problemas de compatibilidade com o final ainda não escrito desse arquivo que contém zeros, defina o tamanho do arquivo antecipadamente em vez de realizar cada gravação como uma gravação de extensão.</span><span class="sxs-lookup"><span data-stu-id="b7673-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="b7673-156">Use o método de cópia correto:</span><span class="sxs-lookup"><span data-stu-id="b7673-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="b7673-157">Use o [AzCopy](storage-use-azcopy.md#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b7673-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="b7673-158">Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre um compartilhamento de arquivos e um computador local.</span><span class="sxs-lookup"><span data-stu-id="b7673-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="b7673-159">Considerações para Windows 8.1 ou Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b7673-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="b7673-160">Para clientes que estão executando o Windows 8.1 ou o Windows Server 2012 R2, verifique se o hotfix [KB3114025](https://support.microsoft.com/help/3114025) está instalado.</span><span class="sxs-lookup"><span data-stu-id="b7673-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="b7673-161">Esse hotfix melhora o desempenho dos identificadores de criação e fechamento.</span><span class="sxs-lookup"><span data-stu-id="b7673-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="b7673-162">Você pode executar o script abaixo para verificar se o hotfix foi instalado:</span><span class="sxs-lookup"><span data-stu-id="b7673-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="b7673-163">Se o hotfix foi instalado, a seguinte saída será exibida:</span><span class="sxs-lookup"><span data-stu-id="b7673-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="b7673-164">As imagens do Windows Server 2012 R2 no Azure Marketplace têm o hotfix KB3114025 instalado por padrão desde dezembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="b7673-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="b7673-165">Nenhuma pasta com uma letra de unidade em **Meu Computador**</span><span class="sxs-lookup"><span data-stu-id="b7673-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="b7673-166">Se você mapear um compartilhamento de arquivos do Azure como administrador por meio do uso de rede, o compartilhamento parece estar ausente.</span><span class="sxs-lookup"><span data-stu-id="b7673-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="b7673-167">Causa</span><span class="sxs-lookup"><span data-stu-id="b7673-167">Cause</span></span>

<span data-ttu-id="b7673-168">Por padrão, o Explorador de Arquivos do Windows não é executado como administrador.</span><span class="sxs-lookup"><span data-stu-id="b7673-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="b7673-169">Se você executar net use em um prompt de comando de administrador, mapeará a unidade de rede como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b7673-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="b7673-170">Como as unidades mapeadas são focadas no usuário, a conta de usuário que está conectada não exibe as unidades se eles estão montadas em uma conta de usuário diferente.</span><span class="sxs-lookup"><span data-stu-id="b7673-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="b7673-171">Solução</span><span class="sxs-lookup"><span data-stu-id="b7673-171">Solution</span></span>
<span data-ttu-id="b7673-172">Monte o compartilhamento de uma linha de comando de não administrador.</span><span class="sxs-lookup"><span data-stu-id="b7673-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="b7673-173">Como alternativa, você pode seguir [este tópico TechNet](https://technet.microsoft.com/library/ee844140.aspx) para configurar o valor do registro **EnableLinkedConnections**.</span><span class="sxs-lookup"><span data-stu-id="b7673-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="b7673-174">O comando net use falha se a conta de armazenamento contém uma barra</span><span class="sxs-lookup"><span data-stu-id="b7673-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="b7673-175">Causa</span><span class="sxs-lookup"><span data-stu-id="b7673-175">Cause</span></span>

<span data-ttu-id="b7673-176">O comando net use interpreta uma barra (/) como uma opção de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b7673-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="b7673-177">Se o nome da sua conta de usuário começa com uma barra, o mapeamento da unidade falhará.</span><span class="sxs-lookup"><span data-stu-id="b7673-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="b7673-178">Solução</span><span class="sxs-lookup"><span data-stu-id="b7673-178">Solution</span></span>

<span data-ttu-id="b7673-179">Você pode usar qualquer uma das seguintes etapas para contornar o problema:</span><span class="sxs-lookup"><span data-stu-id="b7673-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="b7673-180">Execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b7673-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="b7673-181">A partir de um arquivo em lotes, você pode executar o comando desta forma:</span><span class="sxs-lookup"><span data-stu-id="b7673-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="b7673-182">Colocando aspas duplas em torno da chave para contornar esse problema, a menos que a barra seja o primeiro caractere.</span><span class="sxs-lookup"><span data-stu-id="b7673-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="b7673-183">Se for, use o modo interativo e digite sua senha separadamente ou regenere as chaves para obter uma chave que não comece com uma barra.</span><span class="sxs-lookup"><span data-stu-id="b7673-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="b7673-184">O aplicativo ou serviço não pode acessar a unidade montada dos Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="b7673-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="b7673-185">Causa</span><span class="sxs-lookup"><span data-stu-id="b7673-185">Cause</span></span>

<span data-ttu-id="b7673-186">As unidades são montadas por usuário.</span><span class="sxs-lookup"><span data-stu-id="b7673-186">Drives are mounted per user.</span></span> <span data-ttu-id="b7673-187">Se o seu aplicativo ou serviço estiver em execução em uma conta de usuário diferente da que montou a unidade, o aplicativo não verá a unidade.</span><span class="sxs-lookup"><span data-stu-id="b7673-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="b7673-188">Solução</span><span class="sxs-lookup"><span data-stu-id="b7673-188">Solution</span></span>

<span data-ttu-id="b7673-189">Utilize uma das seguintes soluções:</span><span class="sxs-lookup"><span data-stu-id="b7673-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="b7673-190">Monte a unidade a partir da mesma conta de usuário que contém o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7673-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="b7673-191">Você pode usar uma ferramenta como o PsExec.</span><span class="sxs-lookup"><span data-stu-id="b7673-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="b7673-192">Passe o nome da conta de armazenamento e a chave nos parâmetros de nome do usuário e senha do comando net use.</span><span class="sxs-lookup"><span data-stu-id="b7673-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="b7673-193">Depois de seguir estas instruções, você pode receber a seguinte mensagem de erro quando você executa o net use para a conta de serviço de rede/sistema: "Ocorreu um erro de sistema 1312.</span><span class="sxs-lookup"><span data-stu-id="b7673-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="b7673-194">Uma sessão de logon especificada não existe.</span><span class="sxs-lookup"><span data-stu-id="b7673-194">A specified logon session does not exist.</span></span> <span data-ttu-id="b7673-195">Talvez ela já tenha sido finalizada.”</span><span class="sxs-lookup"><span data-stu-id="b7673-195">It may already have been terminated."</span></span> <span data-ttu-id="b7673-196">Se isso ocorrer, verifique se o nome de usuário que é passado para net use inclui informações de domínio (por exemplo: "[nome da conta de armazenamento].file.core.windows.net").</span><span class="sxs-lookup"><span data-stu-id="b7673-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="b7673-197">Erro "Você está copiando um arquivo para um destino que não dá suporte à criptografia"</span><span class="sxs-lookup"><span data-stu-id="b7673-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="b7673-198">Quando um arquivo é copiado pela rede, o arquivo é descriptografado no computador de origem, transmitido em texto não criptografado e criptografado novamente no destino.</span><span class="sxs-lookup"><span data-stu-id="b7673-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="b7673-199">No entanto, você pode ver o seguinte erro quando estiver tentando copiar um arquivo criptografado: "Você está copiando o arquivo para um destino que não dá suporte à criptografia".</span><span class="sxs-lookup"><span data-stu-id="b7673-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="b7673-200">Causa</span><span class="sxs-lookup"><span data-stu-id="b7673-200">Cause</span></span>
<span data-ttu-id="b7673-201">Esse problema pode ocorrer se você estiver usando o sistema de arquivos com criptografia (EFS).</span><span class="sxs-lookup"><span data-stu-id="b7673-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="b7673-202">Os arquivos criptografados pelo BitLocker podem ser copiados para o Armazenamento de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7673-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="b7673-203">No entanto, o Armazenamento de Arquivos do Azure não dá suporte a EFS NTFS.</span><span class="sxs-lookup"><span data-stu-id="b7673-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="b7673-204">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="b7673-204">Workaround</span></span>
<span data-ttu-id="b7673-205">Para copiar um arquivo pela rede, você deve primeiro descriptografá-lo.</span><span class="sxs-lookup"><span data-stu-id="b7673-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="b7673-206">Use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="b7673-206">Use one of the following methods:</span></span>

- <span data-ttu-id="b7673-207">Use o comando **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="b7673-207">Use the **copy /d** command.</span></span> <span data-ttu-id="b7673-208">Ele permite que os arquivos criptografados sejam salvos como arquivos descriptografados no destino.</span><span class="sxs-lookup"><span data-stu-id="b7673-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="b7673-209">Defina a seguinte chave do registro:</span><span class="sxs-lookup"><span data-stu-id="b7673-209">Set the following registry key:</span></span>
  - <span data-ttu-id="b7673-210">Caminho = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="b7673-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="b7673-211">Tipo de valor = DWORD</span><span class="sxs-lookup"><span data-stu-id="b7673-211">Value type = DWORD</span></span>
  - <span data-ttu-id="b7673-212">Name = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="b7673-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="b7673-213">Value = 1</span><span class="sxs-lookup"><span data-stu-id="b7673-213">Value = 1</span></span>

<span data-ttu-id="b7673-214">Observe que a definição da chave do registro afeta todas as operações de cópia que são feitas para compartilhamentos de rede.</span><span class="sxs-lookup"><span data-stu-id="b7673-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="b7673-215">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="b7673-215">Need help?</span></span> <span data-ttu-id="b7673-216">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="b7673-216">Contact support.</span></span>
<span data-ttu-id="b7673-217">Caso ainda precise de ajuda, [contate o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="b7673-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
