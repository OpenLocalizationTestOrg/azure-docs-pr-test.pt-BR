---
title: "aaaTroubleshoot problemas de ativação de máquina virtual Windows no Azure | Microsoft Docs"
description: "Fornece Olá solucionar as etapas para corrigir problemas de ativação de máquina virtual do Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="5cb9f-103">Solucionar problemas de ativação de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="5cb9f-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5cb9f-104">Se você tiver problemas durante a ativação do Azure máquina virtual do Windows (VM) que é criada a partir de uma imagem personalizada, você pode usar informações de saudação fornecidas nesta edição do documento tootroubleshoot hello.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="5cb9f-105">Sintoma</span><span class="sxs-lookup"><span data-stu-id="5cb9f-105">Symptom</span></span>

<span data-ttu-id="5cb9f-106">Quando você tenta tooactivate uma VM do Windows Azure, você recebe um erro de mensagem é semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="5cb9f-107">**Erro: Olá 0xC004F074 LicensingService de Software relatado que computador Olá não pôde ser ativado. Não foi possível fazer contato com nenhum Serviço de Gerenciamento de Chaves (KMS). Consulte Olá Log de eventos do aplicativo para obter informações adicionais.**</span><span class="sxs-lookup"><span data-stu-id="5cb9f-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="5cb9f-108">Causa</span><span class="sxs-lookup"><span data-stu-id="5cb9f-108">Cause</span></span>
<span data-ttu-id="5cb9f-109">Em geral, problemas de ativação da máquina virtual do Azure ocorrerem se Olá VM do Windows não está configurado por usando Olá a chave de instalação de cliente KMS adequada ou Olá VM do Windows tem um problema de conectividade toohello serviço KMS do Azure (kms.core.windows.net, porta 1668).</span><span class="sxs-lookup"><span data-stu-id="5cb9f-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="5cb9f-110">Solução</span><span class="sxs-lookup"><span data-stu-id="5cb9f-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="5cb9f-111">Se você estiver usando uma VPN site a site e forçada de túneis, consulte [Use Azure personalizado roteia a ativação do KMS tooenable com túnel forçado](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="5cb9f-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="5cb9f-112">Se você estiver usando o rota expressa e você tiver uma rota padrão publicados, consulte [VM do Azure pode falhar tooactivate ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="5cb9f-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="5cb9f-113">Etapa 1 Configurar Olá chave KMS adequada cliente instalação (para Windows Server 2016 e Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="5cb9f-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="5cb9f-114">Para Olá VM é criada a partir de uma imagem personalizada do Windows Server 2016 ou Windows Server 2012 R2, você deve configurar Olá chave KMS adequada cliente instalação para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="5cb9f-115">Essa etapa não se aplica tooWindows 2012 ou Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="5cb9f-116">Ele usa o recurso de ativação de máquina Virtual de automação (AVMA) hello, que é suportado apenas pelo Windows Server 2016 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="5cb9f-117">Execute **slmgr.vbs /dlv** em um prompt de comando elevado.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="5cb9f-118">Verifique Olá valor descrição na saída de hello e, em seguida, determine se ele foi criado de varejo (canal de varejo) ou mídia de licença de volume (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="5cb9f-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="5cb9f-119">Se **slmgr.vbs /dlv** mostra o canal de varejo, executar Olá Olá de tooset comandos a seguir [chave de instalação de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) para a versão de saudação do Windows Server que está sendo usado e forçá-lo tooretry ativação:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="5cb9f-120">Por exemplo, para Windows Server 2016 Datacenter, você executaria Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="5cb9f-121">Verifique a etapa 2 Olá conectividade entre Olá VM e o serviço KMS do Azure</span><span class="sxs-lookup"><span data-stu-id="5cb9f-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="5cb9f-122">Baixe e extraia Olá [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) pasta local do tooa ferramenta no hello VM não ativa.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="5cb9f-123">Vá tooStart, pesquisar no Windows PowerShell, com o botão direito do Windows PowerShell e, em seguida, selecione Executar como administrador.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="5cb9f-124">Certifique-se de que Olá que VM é configurada toouse Olá correto KMS do Azure do servidor.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="5cb9f-125">toodo isso, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="5cb9f-126">Olá comando deve retornar: nome de máquina do serviço de gerenciamento de chaves definido tookms.core.windows.net:1688 com êxito.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="5cb9f-127">Verificar usando Psping que você tenha conectividade toohello KMS servidor.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="5cb9f-128">Alternar toohello pasta onde você extraiu o download de Pstools.zip hello e, em seguida, execute o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="5cb9f-129">Na linha do segundo ao último Olá da saída de hello, certifique-se de que você vê: enviados = 4, recebidos = 4, perdidos = 0 (0% de perda).</span><span class="sxs-lookup"><span data-stu-id="5cb9f-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="5cb9f-130">Se perdidos for maior que 0 (zero), Olá VM não tem servidor do KMS toohello conectividade.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="5cb9f-131">Nessa situação, se hello VM estiver em uma rede virtual e tiver um servidor DNS personalizado especificado, você deve verificar se esse servidor DNS é capaz de tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="5cb9f-132">Ou então, alterar Olá DNS server tooone que resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="5cb9f-133">Observe que, se você remover todos os servidores DNS de uma rede virtual, as VMs usam o serviço DNS interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="5cb9f-134">Esse serviço pode resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="5cb9f-135">Também verifique se o que firewall Olá convidado não foi configurado de forma que impediriam a tentativas de ativação.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="5cb9f-136">Depois de verificar tookms.core.windows.net conectividade bem-sucedida, execute Olá comando solicitados com privilégios elevados do Windows PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="5cb9f-137">Esse comando tenta a ativação várias vezes.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="5cb9f-138">Uma ativação bem-sucedida retorna informações semelhantes a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="5cb9f-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="5cb9f-139">**Ativando o Windows(R), edição ServerDatacenter (12345678-1234-1234-1234-12345678)... Produto ativado com sucesso.**</span><span class="sxs-lookup"><span data-stu-id="5cb9f-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="5cb9f-140">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="5cb9f-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="5cb9f-141">Criei Olá Windows Server 2016 do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="5cb9f-142">É necessário tooconfigure chave do KMS para ativação Olá Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="5cb9f-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="5cb9f-143">Não.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-143">No.</span></span> <span data-ttu-id="5cb9f-144">imagem de saudação no Azure Marketplace tem Olá chave KMS adequada cliente instalação já configurado.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="5cb9f-145">Trabalho de ativação do Windows hello mesmo maneira independentemente se Olá VM estiver usando o Azure híbrido Use benefício (HUB) ou não?</span><span class="sxs-lookup"><span data-stu-id="5cb9f-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="5cb9f-146">Sim.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="5cb9f-147">O que acontece se o período de ativação do Windows expirar?</span><span class="sxs-lookup"><span data-stu-id="5cb9f-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="5cb9f-148">Quando o período de cortesia de saudação expirou e o Windows ainda não está ativado, Windows Server 2008 R2 e versões posteriores do Windows mostrará notificações adicionais sobre a ativação.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="5cb9f-149">papel de parede da área de trabalho Olá permanece preto e Windows Update instalará a segurança e apenas atualizações críticas, mas as atualizações não opcionais.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="5cb9f-150">Olá notificações seção final Olá Olá [condições de licenciamento](http://technet.microsoft.com/en-us/library/ff793403.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="5cb9f-151">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="5cb9f-151">Need help?</span></span> <span data-ttu-id="5cb9f-152">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-152">Contact support.</span></span>
<span data-ttu-id="5cb9f-153">Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="5cb9f-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
