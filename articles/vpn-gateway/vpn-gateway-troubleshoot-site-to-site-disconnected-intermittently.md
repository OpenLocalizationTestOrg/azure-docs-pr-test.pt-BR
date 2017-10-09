---
title: aaaTroubleshoot VPN Site a Site do Azure desconecta intermitentemente | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema no qual conexão de VPN Site a Site Olá desconectado regularmente."
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
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Solução de problemas: desconexão intermitente da VPN Site a Site do Azure

Você pode experimentar o problema de saudação que uma conexão de VPN do Microsoft Azure ponto a Site novo ou existente não é estável ou desconecta regularmente. Este artigo fornece etapas toohelp identificar e resolver Olá causa do problema de saudação de solução de problemas. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

### <a name="prerequisite-step"></a>Etapa de pré-requisito

Verifique o tipo de saudação do gateway de rede virtual do Azure:

1. Vá muito[portal do Azure](https://portal.azure.com).
2. Verificar Olá **visão geral** página Olá virtual do gateway de rede para obter informações de tipo hello.
    
    ![Visão geral de saudação do gateway Olá](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Etapa 1 Verifique se Olá dispositivo VPN é validado ao local

1. Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable). Se o dispositivo VPN Olá não for validado, você pode ter toocontact Olá dispositivo fabricante toosee se houver qualquer problema de compatibilidade.
2. Verifique se o que dispositivo VPN hello está configurado corretamente. Para obter mais informações, consulte [Editando amostras de configuração de dispositivo](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>Configurações de associação de segurança de saudação de verificação de etapa 2 (para gateways de rede virtual do Azure baseado em políticas)

1. Certifique-se de qual Olá a rede virtual, sub-redes e intervalos de saudação **gateway de rede Local** definição no Microsoft Azure são os mesmos configuração Olá no dispositivo VPN de local de saudação.
2. Verifique se que coincidirem com as configurações de associação de segurança hello.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Etapa 3 Verificar as Rotas Definidas pelo Usuário ou os Grupos de Segurança de Rede na Sub-rede do Gateway

Uma rota definida pelo usuário na sub-rede de gateway Olá pode ser restringir o tráfego e permitindo que o outro tráfego. Isso torna aparecem que conexão de VPN Olá é confiável para o tráfego e boa para outras pessoas. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Etapa 4 seleção hello "um túnel VPN por par de sub-rede" configuração (para gateways de rede virtual baseado em políticas)

Certifique-se de que Olá dispositivo de VPN está definido toohave ao local **um túnel VPN por par de sub-rede** para gateways de rede virtual baseado em políticas.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Etapa 5 Verificar a Limitação de Associação de Segurança (para gateways de rede virtual baseados em políticas)

gateway de rede virtual com base na política Olá tem limite de 200 pares de associação de segurança de sub-rede. Se vezes o número de saudação de sub-redes de rede virtual do Azure multiplicado por Olá número de sub-redes locais é maior que 200, consulte sub-redes esporádicas desconectando.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Etapa 6 Verificar o endereço da interface externa do dispositivo VPN local

- Se hello Internet voltada para o endereço IP do dispositivo VPN hello está incluída no hello **gateway de rede Local** definição no Azure, você pode enfrentar desconexões esporádicas.
- Olá interface externa do dispositivo deve ser diretamente no hello da Internet. Não deve haver nenhuma conversão de endereço de rede (NAT) ou um firewall entre hello da Internet e o dispositivo hello.
-  Se você configurar o Firewall Clustering toohave um IP virtual, interrompa o cluster hello e expor o dispositivo de VPN Olá diretamente tooa interface pública que Olá gateway pode fazer a interface com.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Etapa 7 de seleção se Olá dispositivo VPN tem sigilo habilitado ao local

Olá **sigilo** recurso pode causar problemas de desconexão de saudação. Se o dispositivo de VPN Olá tem **sigilo** habilitado, desabilite o recurso de saudação. Em seguida, [atualizar a política de IPsec de gateway de rede virtual Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Próximas etapas

- [Configurar uma rede virtual de tooa de conexão Site a Site](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Configure a política IPsec/IKE para conexões VPN Site a Site](vpn-gateway-ipsecikepolicy-rm-powershell.md)

