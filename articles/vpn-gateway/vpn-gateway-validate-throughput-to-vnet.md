---
title: "Validar a taxa de transferência VPN para uma Rede Virtual do Microsoft Azure | Microsoft Docs"
description: "A finalidade deste documento é ajudar um usuário a validar a taxa de transferência de rede de seus recursos locais para uma máquina virtual do Azure."
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
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="6a5d5-103">Como validar a taxa de transferência VPN para uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="6a5d5-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="6a5d5-104">Uma conexão de gateway de VPN permite que você estabeleça conectividade entre instalações segura entre a sua Rede Virtual do Azure e sua infraestrutura de TI local.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="6a5d5-105">Este artigo mostra como validar a taxa de transferência de rede dos recursos locais para uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="6a5d5-106">Ele também fornece diretrizes de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="6a5d5-107">Este artigo destina-se a ajudar a diagnosticar e corrigir problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="6a5d5-108">Se você não conseguir solucionar o problema usando as informações a seguir, [contate o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="6a5d5-109">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6a5d5-109">Overview</span></span>

<span data-ttu-id="6a5d5-110">A conexão de gateway de VPN envolve os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="6a5d5-111">Dispositivo VPN local (exibir uma lista de [dispositivos VPN validados)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="6a5d5-112">Internet pública</span><span class="sxs-lookup"><span data-stu-id="6a5d5-112">Public Internet</span></span>
- <span data-ttu-id="6a5d5-113">Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d5-113">Azure VPN gateway</span></span>
- <span data-ttu-id="6a5d5-114">Máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d5-114">Azure virtual machine</span></span>

<span data-ttu-id="6a5d5-115">O diagrama a seguir mostra a conectividade lógica de uma rede local para uma rede virtual do Azure por meio de VPN.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![Conectividade Lógica da Rede do Cliente com a Rede MSFT usando VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="6a5d5-117">Calcule a entrada/saída máxima esperada</span><span class="sxs-lookup"><span data-stu-id="6a5d5-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="6a5d5-118">Determine os requisitos da taxa de transferência de linha de base do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="6a5d5-119">Determine os limites de taxa de transferência de gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="6a5d5-120">Para obter ajuda, consulte a seção "Agregar taxa de transferência por tipo de VPN e SKU" do [Planejamento e design para Gateway de VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="6a5d5-121">Determine as [Diretrizes de taxa de transferência para a VM do Azure](../virtual-machines/virtual-machines-windows-sizes.md) para seu tamanho de VM.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="6a5d5-122">Determine a largura de banda do Provedor de Serviços de Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="6a5d5-123">Calcule sua taxa de transferência esperada - Menor largura de banda de (VM, Gateway, ISP) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="6a5d5-124">Se a taxa de transferência calculada não atender aos requisitos de taxa de transferência de linha de base do aplicativo, será necessário aumentar a largura de banda do recurso identificado como o afunilamento.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="6a5d5-125">Para redimensionar um Gateway de VPN do Azure, consulte [Alterar um SKU de gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="6a5d5-126">Para redimensionar uma máquina virtual, consulte [Redimensionar uma VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="6a5d5-127">Se não houver largura de banda de Internet esperada, também convém entrar em contato com seu ISP.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="6a5d5-128">Validar a taxa de transferência de rede usando as ferramentas de desempenho</span><span class="sxs-lookup"><span data-stu-id="6a5d5-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="6a5d5-129">Essa validação deve ser executada durante o horário de pico, já que a saturação de taxa de transferência de túnel VPN durante o teste não apresenta resultados precisos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="6a5d5-130">A ferramenta que usamos para esse teste é iPerf, que funciona tanto no Windows como no Linux e tem modos de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="6a5d5-131">Ela é limitada a 3 Gbps para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="6a5d5-132">Essa ferramenta não executa operações de leitura/gravação em disco.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="6a5d5-133">A ferramenta somente produz o tráfego TCP gerado automaticamente de uma extremidade à outra.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="6a5d5-134">As estatísticas são geradas com base em experimentos que medem a largura de banda disponível entre nós de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="6a5d5-135">Ao testar entre dois nós, um atua como o servidor e o outro como um cliente.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="6a5d5-136">Quando esse teste for concluído, é recomendável reverter as funções para testar tanto a taxa de transferência de upload como a de download em ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="6a5d5-137">Baixar iPerf</span><span class="sxs-lookup"><span data-stu-id="6a5d5-137">Download iPerf</span></span>
<span data-ttu-id="6a5d5-138">Baixar [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="6a5d5-139">Para obter detalhes, consulte a [Documentação iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="6a5d5-140">Os produtos de terceiros mencionados neste artigo são fabricados por empresas que são independentes da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="6a5d5-141">A Microsoft não oferece nenhuma garantia, implícita ou não, sobre o desempenho ou a confiabilidade desses produtos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="6a5d5-142">Executar iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="6a5d5-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="6a5d5-143">Habilite uma regra NSG/ACL permitindo o tráfego (para teste de endereço IP público em VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="6a5d5-144">Em ambos os nós, habilite uma exceção de firewall para a porta 5001.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="6a5d5-145">**Windows:** Execute o seguinte comando como um administrador:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="6a5d5-146">Para remover a regra após a conclusão do teste, execute esse comando:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="6a5d5-147">**Linux do Azure:** as imagens do Linux do Azure têm firewalls permissivos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="6a5d5-148">Se houver um aplicativo escutando em uma porta, o tráfego será permitido.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="6a5d5-149">Imagens personalizadas que são protegidas podem precisar de portas abertas explicitamente.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="6a5d5-150">Os firewalls da camada de OS do Linux comuns incluem `iptables`, `ufw`, ou `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="6a5d5-151">No nó de servidor, altere para o diretório onde o iperf3.exe é extraído.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="6a5d5-152">Em seguida, execute o iPerf no modo de servidor e configure-o para escutar na porta 5001, de acordo com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="6a5d5-153">No nó de cliente, altere para o diretório onde a ferramenta iperf é extraída e, em seguida, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="6a5d5-154">O cliente induz o tráfego na porta 5001 para o servidor por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="6a5d5-155">O sinalizador '-P ' indica que estamos usando 32 conexões simultâneas para o nó de servidor.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="6a5d5-156">A tela a seguir mostra a saída a partir desse exemplo:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-156">The following screen shows the output from this example:</span></span>

    ![Saída](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="6a5d5-158">(OPCIONAL) Para preservar os resultados dos testes, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="6a5d5-159">Após concluir as etapas anteriores, execute as mesmas etapas com as funções invertidas, de modo que o nó de servidor agora seja o cliente e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="6a5d5-160">Solucionar problemas com cópia de arquivo lenta</span><span class="sxs-lookup"><span data-stu-id="6a5d5-160">Address slow file copy issues</span></span>
<span data-ttu-id="6a5d5-161">É possível que você tenha experiência com cópia de arquivo lenta ao utilizar o Windows Explorer ou ao arrastar e soltar por meio de uma sessão RDP.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="6a5d5-162">Esse problema normalmente ocorre devido a um ou ambos os seguintes fatores:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="6a5d5-163">Os aplicativos de cópia de arquivo, como o Windows Explorer e o RDP não usam múltiplos threads ao copiar arquivos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="6a5d5-164">Para obter melhor desempenho, use um aplicativo de cópia de arquivo multi-threaded como o [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) para copiar arquivos usando 16 ou 32 threads.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="6a5d5-165">Para alterar o número de thread para cópia de arquivo no Richcopy, clique em **Ação** > **Opções de cópia** > **Cópia de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="6a5d5-166">
![Problemas com cópia de arquivo lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="6a5d5-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="6a5d5-167">Velocidade de leitura/gravação de disco de VM insuficiente.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="6a5d5-168">Para obter mais informações, consulte [Solução de Problemas de Armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6a5d5-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="6a5d5-169">Interface externa do dispositivo local</span><span class="sxs-lookup"><span data-stu-id="6a5d5-169">On-premises device external facing interface</span></span>
<span data-ttu-id="6a5d5-170">Se o endereço IP para a Internet do dispositivo VPN local estiver incluído na definição [rede local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) no Azure, você poderá enfrentar a impossibilidade de conectar o VPN, problemas de desempenho ou desconexões esporádicas.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="6a5d5-171">Verificação de latência</span><span class="sxs-lookup"><span data-stu-id="6a5d5-171">Checking latency</span></span>
<span data-ttu-id="6a5d5-172">Use o tracert para rastrear o dispositivo Microsoft Azure Edge e determinar se há atrasos superiores a 100 ms entre saltos.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="6a5d5-173">Na rede local, execute *tracert* para o VIP do Gateway Azure ou VM.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="6a5d5-174">Após visualizar somente o * retornado, você saberá que atingiu o limite do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="6a5d5-175">Quando nomes DNS que incluem "MSN" forem retornados, você saberá que atingiu o backbone da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6a5d5-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="6a5d5-176">
![Verificação de Latência](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="6a5d5-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a5d5-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a5d5-177">Next steps</span></span>
<span data-ttu-id="6a5d5-178">Para obter mais informações ou ajuda, confira os seguintes links:</span><span class="sxs-lookup"><span data-stu-id="6a5d5-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="6a5d5-179">Otimizar a taxa de transferência de rede para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="6a5d5-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="6a5d5-180">Suporte da Microsoft</span><span class="sxs-lookup"><span data-stu-id="6a5d5-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
