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
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Como rede virtual do tooa toovalidate VPN taxa de transferência

Uma conexão de gateway VPN permite a conectividade entre locais seguras, tooestablish entre sua rede Virtual no Azure e seu local infraestrutura de TI.

Este artigo mostra como toovalidate taxa de transferência de rede de saudação local recursos tooan máquina virtual do Azure. Ele também fornece diretrizes de solução de problemas.

>[!NOTE]
>Este artigo destina-se toohelp diagnosticar e corrigir problemas comuns. Se você estiver toosolve não é possível problema de saudação usando Olá seguintes informações, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Visão geral

Olá conexão de gateway VPN envolve Olá componentes a seguir:

- Dispositivo VPN local (exibir uma lista de [dispositivos VPN validados)](vpn-gateway-about-vpn-devices.md#devicetable).
- Internet pública
- Gateway de VPN do Azure
- Máquina virtual do Azure

Olá diagrama a seguir mostra a conectividade lógica saudação de uma rede de local tooan rede virtual do Azure por meio de VPN.

![TooMSFT lógica de conectividade de rede do cliente de rede usando VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Calcular Olá máximo esperado de entrada/saída

1.  Determine os requisitos da taxa de transferência de linha de base do aplicativo.
2.  Determine os limites de taxa de transferência de gateway de VPN do Azure. Para obter ajuda, consulte a seção hello "taxa de transferência agregada por tipo SKU e VPN" [de planejamento e design para o Gateway de VPN](vpn-gateway-plan-design.md).
3.  Determinar Olá [orientação de taxa de transferência de VM do Azure](../virtual-machines/virtual-machines-windows-sizes.md) para o tamanho da VM.
4.  Determine a largura de banda do Provedor de Serviços de Internet (ISP).
5.  Calcule sua taxa de transferência esperada - Menor largura de banda de (VM, Gateway, ISP) * 0,8.

Se a taxa de transferência calculada não atende aos requisitos de taxa de transferência de linha de base do seu aplicativo, você precisará tooincrease largura de banda de saudação do recurso de saudação que você identificou como gargalo hello. tooresize um Gateway de VPN do Azure, consulte [alterando um SKU de gateway](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). tooresize uma máquina virtual, consulte [redimensionar uma VM](../virtual-machines/virtual-machines-windows-resize-vm.md). Se não houver largura de banda de Internet esperada, talvez também seja toocontact seu ISP.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Validar a taxa de transferência de rede usando as ferramentas de desempenho

Essa validação deve ser executada durante o horário de pico, já que a saturação de taxa de transferência de túnel VPN durante o teste não apresenta resultados precisos.

ferramenta de saudação que usamos para este teste é iPerf, que funciona no Windows e Linux e tem modos de cliente e servidor. Ele é limitado too3 Gbps para máquinas virtuais do Windows.

Essa ferramenta não executa qualquer toodisk de operações de leitura/gravação. Somente será gerado automaticamente o tráfego de TCP de uma toohello final outros. Ela gerada estatísticas com base em experimentação que mede a largura de banda de saudação disponível entre os nós de cliente e servidor. Ao testar entre dois nós, um atua como servidor de saudação e hello como um cliente. Depois que esse teste é concluído, é recomendável que você reverter Olá funções tootest ambos upload e download de taxa de transferência em ambos os nós.

### <a name="download-iperf"></a>Baixar iPerf
Baixar [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Para obter detalhes, consulte a [Documentação iPerf](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >produtos de terceiros Olá neste artigo são fabricados por empresas que são independentes da Microsoft. Microsoft não dá nenhuma garantia, implícita ou não, sobre o desempenho de saudação ou confiabilidade desses produtos.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Executar iPerf (iperf3.exe)
1. Habilite uma regra ACL/NSG permitindo o tráfego de saudação (para o endereço IP público de teste na VM do Azure).

2. Em ambos os nós, habilite uma exceção de firewall para a porta 5001.

    **Windows:** comando a seguir de saudação executar como administrador:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    regra de saudação tooremove durante o teste estiver concluída, execute este comando:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Linux do Azure:** as imagens do Linux do Azure têm firewalls permissivos. Se houver um aplicativo de escuta em uma porta, o tráfego de saudação é permitido pelo. Imagens personalizadas que são protegidas podem precisar de portas abertas explicitamente. Os firewalls da camada de OS do Linux comuns incluem `iptables`, `ufw`, ou `firewalld`.

3. No nó do servidor de saudação, altere o diretório de toohello onde iperf3.exe são extraídos. Em seguida, execute iPerf no modo de servidor e defina-toolisten na porta 5001 como Olá comandos a seguir:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. No nó do cliente hello, altere o diretório de toohello onde ferramenta iperf é extraída e, em seguida, executar Olá comando a seguir:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    cliente de saudação é induzindo tráfego no servidor de toohello 5001 porta para 30 segundos. Olá sinalizador '-P ' que indica que estamos usando o nó do servidor de toohello de conexões simultâneas 32.

    Olá, tela a seguir mostra a saída de hello neste exemplo:

    ![Saída](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. Saudação (opcional) toopreserve teste resultados, executados este comando:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Depois de concluir as etapas anteriores hello, execute Olá mesmas etapas com as funções hello revertidas, para que hello nó do servidor agora será cliente hello e vice-versa.

## <a name="address-slow-file-copy-issues"></a>Solucionar problemas com cópia de arquivo lenta
É possível que você tenha experiência com cópia de arquivo lenta ao utilizar o Windows Explorer ou ao arrastar e soltar por meio de uma sessão RDP. Esse problema é normalmente devido tooone ou ambos Olá fatores a seguir:

- Os aplicativos de cópia de arquivo, como o Windows Explorer e o RDP não usam múltiplos threads ao copiar arquivos. Para obter melhor desempenho, use um aplicativo de cópia de arquivo multithread como [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy arquivos usando threads de 16 ou 32. número de threads toochange Olá para cópia de arquivo em Richcopy, clique em **ação** > **opções de cópia** > **cópia do arquivo**.<br><br>
![Problemas com cópia de arquivo lenta](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Velocidade de leitura/gravação de disco de VM insuficiente. Para obter mais informações, consulte [Solução de Problemas de Armazenamento do Azure](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Interface externa do dispositivo local
Se Olá endereço IP da Internet de dispositivo VPN está incluído no hello ao local [rede local](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definição no Azure, você pode enfrentar dificuldades toobring Olá desconecta de VPN, esporádica ou problemas de desempenho.

## <a name="checking-latency"></a>Verificação de latência
Use o tracert tootrace tooMicrosoft Azure borda dispositivo toodetermine se houver atrasos exceder 100 ms entre saltos.

Na rede do local de hello, execute *tracert* toohello VIP de hello Azure Gateway ou a VM. Depois que você veja apenas * retornado, você sabe Olá borda do Azure foi atingido. Quando você vir nomes DNS que incluem "MSN" retornada, você sabe que você tenha atingido o backbone de Microsoft hello.<br><br>
![Verificação de Latência](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações ou Ajuda, consulte Olá links a seguir:

- [Otimizar a taxa de transferência de rede para máquinas virtuais do Azure](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Suporte da Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
