---
title: "Validar a taxa de transferência VPN tooa rede Virtual do Microsoft Azure | Microsoft Docs"
description: "Olá, a finalidade deste documento é toohelp um usuário validar a taxa de transferência de rede de saudação de seu recursos de local tooan máquina virtual do Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="cee0b-103">Como rede virtual do tooa toovalidate VPN taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="cee0b-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="cee0b-104">Uma conexão de gateway VPN permite a conectividade entre locais seguras, tooestablish entre sua rede Virtual no Azure e seu local infraestrutura de TI.</span><span class="sxs-lookup"><span data-stu-id="cee0b-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="cee0b-105">Este artigo mostra como toovalidate taxa de transferência de rede de saudação local recursos tooan máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="cee0b-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="cee0b-106">Ele também fornece diretrizes de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="cee0b-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="cee0b-107">Este artigo destina-se toohelp diagnosticar e corrigir problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="cee0b-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="cee0b-108">Se você estiver toosolve não é possível problema de saudação usando Olá seguintes informações, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="cee0b-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="cee0b-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cee0b-109">Overview</span></span>

<span data-ttu-id="cee0b-110">Olá conexão de gateway VPN envolve Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee0b-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="cee0b-111">Dispositivo VPN local (exibir uma lista de [dispositivos VPN validados)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="cee0b-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="cee0b-112">Internet pública</span><span class="sxs-lookup"><span data-stu-id="cee0b-112">Public Internet</span></span>
- <span data-ttu-id="cee0b-113">Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="cee0b-113">Azure VPN gateway</span></span>
- <span data-ttu-id="cee0b-114">Máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="cee0b-114">Azure virtual machine</span></span>

<span data-ttu-id="cee0b-115">Olá diagrama a seguir mostra a conectividade lógica saudação de uma rede de local tooan rede virtual do Azure por meio de VPN.</span><span class="sxs-lookup"><span data-stu-id="cee0b-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![TooMSFT lógica de conectividade de rede do cliente de rede usando VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="cee0b-117">Calcular Olá máximo esperado de entrada/saída</span><span class="sxs-lookup"><span data-stu-id="cee0b-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="cee0b-118">Determine os requisitos da taxa de transferência de linha de base do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cee0b-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="cee0b-119">Determine os limites de taxa de transferência de gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="cee0b-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="cee0b-120">Para obter ajuda, consulte a seção hello "taxa de transferência agregada por tipo SKU e VPN" [de planejamento e design para o Gateway de VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="cee0b-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="cee0b-121">Determinar Olá [orientação de taxa de transferência de VM do Azure](../virtual-machines/virtual-machines-windows-sizes.md) para o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="cee0b-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="cee0b-122">Determine a largura de banda do Provedor de Serviços de Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="cee0b-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="cee0b-123">Calcule sua taxa de transferência esperada - Menor largura de banda de (VM, Gateway, ISP) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="cee0b-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="cee0b-124">Se a taxa de transferência calculada não atende aos requisitos de taxa de transferência de linha de base do seu aplicativo, você precisará tooincrease largura de banda de saudação do recurso de saudação que você identificou como gargalo hello.</span><span class="sxs-lookup"><span data-stu-id="cee0b-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="cee0b-125">tooresize um Gateway de VPN do Azure, consulte [alterando um SKU de gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="cee0b-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="cee0b-126">tooresize uma máquina virtual, consulte [redimensionar uma VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="cee0b-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="cee0b-127">Se não houver largura de banda de Internet esperada, talvez também seja toocontact seu ISP.</span><span class="sxs-lookup"><span data-stu-id="cee0b-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="cee0b-128">Validar a taxa de transferência de rede usando as ferramentas de desempenho</span><span class="sxs-lookup"><span data-stu-id="cee0b-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="cee0b-129">Essa validação deve ser executada durante o horário de pico, já que a saturação de taxa de transferência de túnel VPN durante o teste não apresenta resultados precisos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="cee0b-130">ferramenta de saudação que usamos para este teste é iPerf, que funciona no Windows e Linux e tem modos de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="cee0b-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="cee0b-131">Ele é limitado too3 Gbps para máquinas virtuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="cee0b-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="cee0b-132">Essa ferramenta não executa qualquer toodisk de operações de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="cee0b-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="cee0b-133">Somente será gerado automaticamente o tráfego de TCP de uma toohello final outros.</span><span class="sxs-lookup"><span data-stu-id="cee0b-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="cee0b-134">Ela gerada estatísticas com base em experimentação que mede a largura de banda de saudação disponível entre os nós de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="cee0b-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="cee0b-135">Ao testar entre dois nós, um atua como servidor de saudação e hello como um cliente.</span><span class="sxs-lookup"><span data-stu-id="cee0b-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="cee0b-136">Depois que esse teste é concluído, é recomendável que você reverter Olá funções tootest ambos upload e download de taxa de transferência em ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="cee0b-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="cee0b-137">Baixar iPerf</span><span class="sxs-lookup"><span data-stu-id="cee0b-137">Download iPerf</span></span>
<span data-ttu-id="cee0b-138">Baixar [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="cee0b-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="cee0b-139">Para obter detalhes, consulte a [Documentação iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="cee0b-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="cee0b-140">produtos de terceiros Olá neste artigo são fabricados por empresas que são independentes da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cee0b-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="cee0b-141">Microsoft não dá nenhuma garantia, implícita ou não, sobre o desempenho de saudação ou confiabilidade desses produtos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="cee0b-142">Executar iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="cee0b-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="cee0b-143">Habilite uma regra ACL/NSG permitindo o tráfego de saudação (para o endereço IP público de teste na VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="cee0b-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="cee0b-144">Em ambos os nós, habilite uma exceção de firewall para a porta 5001.</span><span class="sxs-lookup"><span data-stu-id="cee0b-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="cee0b-145">**Windows:** comando a seguir de saudação executar como administrador:</span><span class="sxs-lookup"><span data-stu-id="cee0b-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="cee0b-146">regra de saudação tooremove durante o teste estiver concluída, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="cee0b-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="cee0b-147">**Linux do Azure:** as imagens do Linux do Azure têm firewalls permissivos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="cee0b-148">Se houver um aplicativo de escuta em uma porta, o tráfego de saudação é permitido pelo.</span><span class="sxs-lookup"><span data-stu-id="cee0b-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="cee0b-149">Imagens personalizadas que são protegidas podem precisar de portas abertas explicitamente.</span><span class="sxs-lookup"><span data-stu-id="cee0b-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="cee0b-150">Os firewalls da camada de OS do Linux comuns incluem `iptables`, `ufw`, ou `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="cee0b-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="cee0b-151">No nó do servidor de saudação, altere o diretório de toohello onde iperf3.exe são extraídos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="cee0b-152">Em seguida, execute iPerf no modo de servidor e defina-toolisten na porta 5001 como Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee0b-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="cee0b-153">No nó do cliente hello, altere o diretório de toohello onde ferramenta iperf é extraída e, em seguida, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee0b-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="cee0b-154">cliente de saudação é induzindo tráfego no servidor de toohello 5001 porta para 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="cee0b-155">Olá sinalizador '-P ' que indica que estamos usando o nó do servidor de toohello de conexões simultâneas 32.</span><span class="sxs-lookup"><span data-stu-id="cee0b-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="cee0b-156">Olá, tela a seguir mostra a saída de hello neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="cee0b-156">hello following screen shows hello output from this example:</span></span>

    ![Saída](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="cee0b-158">Saudação (opcional) toopreserve teste resultados, executados este comando:</span><span class="sxs-lookup"><span data-stu-id="cee0b-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="cee0b-159">Depois de concluir as etapas anteriores hello, execute Olá mesmas etapas com as funções hello revertidas, para que hello nó do servidor agora será cliente hello e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="cee0b-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="cee0b-160">Solucionar problemas com cópia de arquivo lenta</span><span class="sxs-lookup"><span data-stu-id="cee0b-160">Address slow file copy issues</span></span>
<span data-ttu-id="cee0b-161">É possível que você tenha experiência com cópia de arquivo lenta ao utilizar o Windows Explorer ou ao arrastar e soltar por meio de uma sessão RDP.</span><span class="sxs-lookup"><span data-stu-id="cee0b-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="cee0b-162">Esse problema é normalmente devido tooone ou ambos Olá fatores a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee0b-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="cee0b-163">Os aplicativos de cópia de arquivo, como o Windows Explorer e o RDP não usam múltiplos threads ao copiar arquivos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="cee0b-164">Para obter melhor desempenho, use um aplicativo de cópia de arquivo multithread como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy arquivos usando threads de 16 ou 32.</span><span class="sxs-lookup"><span data-stu-id="cee0b-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="cee0b-165">número de threads toochange Olá para cópia de arquivo em Richcopy, clique em **ação** > **opções de cópia** > **cópia do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="cee0b-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="cee0b-166">
![Problemas com cópia de arquivo lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="cee0b-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="cee0b-167">Velocidade de leitura/gravação de disco de VM insuficiente.</span><span class="sxs-lookup"><span data-stu-id="cee0b-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="cee0b-168">Para obter mais informações, consulte [Solução de Problemas de Armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cee0b-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="cee0b-169">Interface externa do dispositivo local</span><span class="sxs-lookup"><span data-stu-id="cee0b-169">On-premises device external facing interface</span></span>
<span data-ttu-id="cee0b-170">Se Olá endereço IP da Internet de dispositivo VPN está incluído no hello ao local [rede local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definição no Azure, você pode enfrentar dificuldades toobring Olá desconecta de VPN, esporádica ou problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="cee0b-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="cee0b-171">Verificação de latência</span><span class="sxs-lookup"><span data-stu-id="cee0b-171">Checking latency</span></span>
<span data-ttu-id="cee0b-172">Use o tracert tootrace tooMicrosoft Azure borda dispositivo toodetermine se houver atrasos exceder 100 ms entre saltos.</span><span class="sxs-lookup"><span data-stu-id="cee0b-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="cee0b-173">Na rede do local de hello, execute *tracert* toohello VIP de hello Azure Gateway ou a VM.</span><span class="sxs-lookup"><span data-stu-id="cee0b-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="cee0b-174">Depois que você veja apenas * retornado, você sabe Olá borda do Azure foi atingido.</span><span class="sxs-lookup"><span data-stu-id="cee0b-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="cee0b-175">Quando você vir nomes DNS que incluem "MSN" retornada, você sabe que você tenha atingido o backbone de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="cee0b-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="cee0b-176">
![Verificação de Latência](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="cee0b-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cee0b-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cee0b-177">Next steps</span></span>
<span data-ttu-id="cee0b-178">Para obter mais informações ou Ajuda, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee0b-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="cee0b-179">Otimizar a taxa de transferência de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="cee0b-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="cee0b-180">Suporte da Microsoft</span><span class="sxs-lookup"><span data-stu-id="cee0b-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
