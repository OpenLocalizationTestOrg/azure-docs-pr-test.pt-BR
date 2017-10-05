---
title: "Solução de problemas de ativação de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Fornece as etapas de solução de problemas para corrigir problemas de ativação de máquina virtual do Windows no Azure"
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
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="f870d-103">Solucionar problemas de ativação de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f870d-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f870d-104">Se você tiver problemas durante a ativação da máquina virtual do Windows Azure (VM) que é criada a partir de uma imagem personalizada, você pode usar as informações fornecidas neste documento para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="f870d-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="f870d-105">Sintoma</span><span class="sxs-lookup"><span data-stu-id="f870d-105">Symptom</span></span>

<span data-ttu-id="f870d-106">Quando você tentar ativar uma VM do Windows Azure, você recebe uma mensagem de erro semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f870d-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="f870d-107">**Erro: 0xC004F074 O Serviço de Licenciamento do Software relatou que o computador não pode ser ativado. Não foi possível fazer contato com nenhum Serviço de Gerenciamento de Chaves (KMS). Consulte o Log de Eventos do Aplicativo para obter informações adicionais.**</span><span class="sxs-lookup"><span data-stu-id="f870d-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="f870d-108">Causa</span><span class="sxs-lookup"><span data-stu-id="f870d-108">Cause</span></span>
<span data-ttu-id="f870d-109">Em geral, problemas de ativação da VM do Azure ocorrem se a VM do Windows não está configurada usando a chave de instalação de cliente do KMS adequada, ou a VM do Windows tem um problema de conectividade com o serviço KMS do Azure (kms.core.windows.net, porta 1668).</span><span class="sxs-lookup"><span data-stu-id="f870d-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="f870d-110">Solução</span><span class="sxs-lookup"><span data-stu-id="f870d-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="f870d-111">Se você estiver usando uma VPN site a site e túnel forçado, consulte [Usar rotas personalizadas para habilitar a ativação KMS com túnel forçado](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="f870d-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="f870d-112">Se você estiver usando o ExpressRoute e você tiver uma rota padrão publicada, consulte [A VM do Azure pode falhar ao ser ativada pela ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="f870d-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="f870d-113">Etapa 1 Configurar a chave de instalação de cliente KMS adequada (para Windows Server 2016 e Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="f870d-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="f870d-114">Para a VM que é criada a partir de uma imagem personalizada do Windows Server 2016 ou Windows Server 2012 R2, você deve configurar a chave de instalação de cliente KMS adequada para a VM.</span><span class="sxs-lookup"><span data-stu-id="f870d-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="f870d-115">Esta etapa não é aplicável ao Windows 2012 ou Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="f870d-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="f870d-116">Ela usa o recurso de Ativação de Máquina Virtual de Automação (AVMA), que é suportado apenas pelo Windows Server 2016 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f870d-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="f870d-117">Execute **slmgr.vbs /dlv** em um prompt de comando elevado.</span><span class="sxs-lookup"><span data-stu-id="f870d-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="f870d-118">Verifique o valor de descrição na saída e, em seguida, determine se ele foi criado a partir da mídia de licença de varejo (canal RETAIL) ou de volume (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="f870d-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="f870d-119">Se **slmgr.vbs /dlv** mostrar o canal RETAIL, execute os seguintes comandos para definir a [chave de instalação de cliente KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) para a versão do Windows Server que está sendo usada e forçá-la para efetuar a ativação novamente:</span><span class="sxs-lookup"><span data-stu-id="f870d-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="f870d-120">Por exemplo, para o Datacenter do Windows Server 2016, você executaria o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f870d-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="f870d-121">Etapa 2 Verificar a conectividade entre o serviço KMS do Azure e de VM</span><span class="sxs-lookup"><span data-stu-id="f870d-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="f870d-122">Baixe e extraia a ferramenta [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) em uma pasta local na VM que não ativa.</span><span class="sxs-lookup"><span data-stu-id="f870d-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="f870d-123">Vá para Iniciar, pesquise no Windows PowerShell, clique com o botão direito no Windows PowerShell e, em seguida, selecione Executar como administrador.</span><span class="sxs-lookup"><span data-stu-id="f870d-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="f870d-124">Certifique-se de que a VM está configurada para usar o servidor correto do KMS do Azure.</span><span class="sxs-lookup"><span data-stu-id="f870d-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="f870d-125">Para fazer isso, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f870d-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="f870d-126">O comando deve retornar: Nome da máquina do Serviço de Gerenciamento de Chaves definido como kms.core.windows.net:1688 com sucesso.</span><span class="sxs-lookup"><span data-stu-id="f870d-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="f870d-127">Verifique usando Psping que você tem conectividade ao servidor KMS.</span><span class="sxs-lookup"><span data-stu-id="f870d-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="f870d-128">Alterne para a pasta onde você extraiu o download de Pstools.zip e, em seguida, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f870d-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="f870d-129">Na penúltima linha da saída, certifique-se de que você vê: Sent = 4, Received = 4, Lost = 0 (0% de perda).</span><span class="sxs-lookup"><span data-stu-id="f870d-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="f870d-130">Se Lost for maior que 0 (zero), a VM não tem conectividade com o servidor KMS.</span><span class="sxs-lookup"><span data-stu-id="f870d-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="f870d-131">Nessa situação, se a VM estiver em uma rede virtual e tiver um servidor DNS especificado, certifique-se de que o servidor DNS é capaz de resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f870d-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="f870d-132">Ou então, altere o servidor DNS para um que resolva kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f870d-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="f870d-133">Observe que, se você remover todos os servidores DNS de uma rede virtual, as VMs usam o serviço DNS interno do Azure.</span><span class="sxs-lookup"><span data-stu-id="f870d-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="f870d-134">Esse serviço pode resolver kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f870d-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="f870d-135">Também verifique se o firewall do convidado não foi configurado de forma que impediria as tentativas de ativação.</span><span class="sxs-lookup"><span data-stu-id="f870d-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="f870d-136">Depois de verificar a conectividade com sucesso para kms.core.windows.net, execute o seguinte comando no prompt do Windows PowerShell com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="f870d-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="f870d-137">Esse comando tenta a ativação várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f870d-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="f870d-138">Uma ativação bem-sucedida retorna informações semelhantes à seguinte:</span><span class="sxs-lookup"><span data-stu-id="f870d-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="f870d-139">**Ativando o Windows(R), edição ServerDatacenter (12345678-1234-1234-1234-12345678)... Produto ativado com sucesso.**</span><span class="sxs-lookup"><span data-stu-id="f870d-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="f870d-140">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f870d-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="f870d-141">Criei o Windows Server 2016 a partir do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f870d-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="f870d-142">É necessário configurar a chave KMS para ativação do Windows Server 2016?</span><span class="sxs-lookup"><span data-stu-id="f870d-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="f870d-143">Não.</span><span class="sxs-lookup"><span data-stu-id="f870d-143">No.</span></span> <span data-ttu-id="f870d-144">A imagem no Azure Marketplace já possui a chave de instalação de cliente KMS adequada configurada.</span><span class="sxs-lookup"><span data-stu-id="f870d-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="f870d-145">A ativação do Windows funciona da mesma maneira independentemente se a VM estiver usando o Benefício de Uso Híbrido do Azure (HUB) ou não?</span><span class="sxs-lookup"><span data-stu-id="f870d-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="f870d-146">Sim.</span><span class="sxs-lookup"><span data-stu-id="f870d-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="f870d-147">O que acontece se o período de ativação do Windows expirar?</span><span class="sxs-lookup"><span data-stu-id="f870d-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="f870d-148">Quando o período de cortesia expirar e o Windows ainda não está ativado, o Windows Server 2008 R2 e versões posteriores do Windows mostrarão notificações adicionais sobre a ativação.</span><span class="sxs-lookup"><span data-stu-id="f870d-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="f870d-149">O papel de parede da área de trabalho permanece preto e o Windows Update instalará somente as atualizações de segurança e críticas, mas não as atualizações opcionais.</span><span class="sxs-lookup"><span data-stu-id="f870d-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="f870d-150">Consulte a seção de Notificações na parte inferior da página [Condições de Licenciamento](http://technet.microsoft.com/en-us/library/ff793403.aspx).</span><span class="sxs-lookup"><span data-stu-id="f870d-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="f870d-151">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="f870d-151">Need help?</span></span> <span data-ttu-id="f870d-152">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="f870d-152">Contact support.</span></span>
<span data-ttu-id="f870d-153">Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f870d-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>