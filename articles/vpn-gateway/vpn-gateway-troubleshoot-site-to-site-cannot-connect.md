---
title: "aaaTroubleshoot uma conexão de VPN site a site do Azure que não é possível conectar | Microsoft Docs"
description: "Saiba como tootroubleshoot uma conexão de VPN site a site que repentinamente para de funcionar e não pode ser reconectada."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Solução de problemas: uma conexão VPN site a site do Azure não consegue se conectar e deixa de funcionar

Depois de configurar uma conexão de VPN site a site entre uma rede local e uma rede virtual do Azure, Olá conexão VPN, de repente, para de funcionar e não pode ser reconectada. Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

problema de saudação tooresolve, primeiro tente muito[gateway de VPN do Azure Olá redefinição](vpn-gateway-resetgw-classic.md) e redefinir o túnel de saudação do dispositivo VPN de local de saudação. Se Olá problema persistir, siga estas causa etapas tooidentify Olá problema de saudação.

### <a name="prerequisite-step"></a>Etapa de pré-requisito

Verifique o tipo de saudação do gateway de VPN do Azure hello.

1. Vá toohello [portal do Azure](https://portal.azure.com).

2. Verificar Olá **visão geral** página do gateway de VPN Olá para obter informações de tipo hello.
    
    ![Visão geral do gateway de saudação](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Etapa 1. Verifique se o dispositivo VPN de local de saudação é validado

1. Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable). Se o dispositivo de saudação não for um dispositivo VPN validado, você terá toocontact Olá dispositivo fabricante toosee se houver um problema de compatibilidade.

2. Verifique se o que dispositivo VPN hello está configurado corretamente. Para obter mais informações, consulte [Editar exemplos de configuração de dispositivo](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>Etapa 2. Verifique se a chave compartilhada Olá

Compare a chave compartilhada Olá Olá local VPN dispositivo toohello VPN de rede Virtual do Azure toomake se chaves Olá correspondem. 

chave compartilhada do tooview Olá para Olá conexão VPN do Azure, use um dos métodos a seguir de saudação:

**Portal do Azure**

1. Vá conexão site a site de gateway VPN de toohello que você criou.

2. Em Olá **configurações** seção, clique em **chave compartilhada**.
    
    ![Chave compartilhada](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**PowerShell do Azure**

Para o modelo de implantação do Azure Resource Manager hello:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Para o modelo de implantação clássico hello:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>Etapa 3. Verifique se o par VPN Olá IPs

-   Olá definição de IP no hello **Gateway de rede Local** objeto no Azure deve corresponder o IP do dispositivo local hello.
-   Olá definição de IP do gateway do Azure que é definida em hello local dispositivo deve corresponder a saudação IP de gateway do Azure.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>Etapa 4. Verifique UDR e NSGs na sub-rede de gateway Olá

Verificar e remover roteamento definido pelo usuário (UDR) ou grupos de segurança de rede (NSGs) na sub-rede de gateway de saudação e, em seguida, o resultado de saudação de teste. Se Olá problema for resolvido, valide configurações Olá UDR ou NSG aplicada.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>Etapa 5. Saudação de verificação de endereço de interface externa do dispositivo VPN local

- Se Olá endereço IP da Internet do dispositivo VPN hello está incluído no hello **rede Local** definição no Azure, você pode experimentar desconexões esporádicas.
- Olá interface externa do dispositivo deve ser diretamente no hello da Internet. Não deve haver nenhuma conversão de endereços de rede ou um firewall entre hello da Internet e o dispositivo hello.
- tooconfigure firewall toohave clustering um IP virtual, interrompa o cluster hello e expor o dispositivo de VPN Olá diretamente a interface pública tooa gateway Olá pode fazer a interface com.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>Etapa 6. Verifique se as sub-redes de saudação correspondem exatamente (gateways com base na política do Azure)

-   Verifique se as sub-redes de saudação correspondem exatamente entre hello rede virtual do Azure e definições de local para Olá rede virtual do Azure.
-   Verifique se as sub-redes de saudação correspondem exatamente entre hello **Gateway de rede Local** e definições de rede do local de saudação local.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>Etapa 7. Verifique se a investigação de integridade de gateway do Azure Olá

1. Vá toohello [investigação de integridade](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Clique em aviso de saudação do certificado.
3. Se você receber uma resposta, o gateway VPN Olá será considerada íntegra. Se você não receber uma resposta, gateway Olá pode não ser Íntegro ou um NSG na sub-rede de gateway hello está causando o problema de saudação. Olá texto a seguir é um exemplo de resposta:

    &lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Instância primária: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>Etapa 8. Verifique se Olá local dispositivo VPN tem Olá sigilo habilitado

recurso de sigilo Olá pode causar problemas de desconexão. Se o dispositivo de VPN Olá sigilo total, desabilite o recurso de hello. Atualize política de IPsec de gateway VPN hello.

## <a name="next-steps"></a>Próximas etapas

-   [Configurar uma rede virtual de tooa conexão site a site](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Configurar uma política IPsec/IKE para conexões VPN site a site](vpn-gateway-ipsecikepolicy-rm-powershell.md)
