---
title: "cenários de aaaAdvanced com o Azure MFA e VPNs de terceiros"
description: "Guias de configuração passo a passo para o Azure MFA toointegrate com a Cisco, Citrix e Juniper."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Cenários avançados com soluções da Autenticação Multifator do Azure e VPNs de terceiros
Autenticação multifator do Azure pode ser usada tooseamlessly conectar-se com várias soluções VPN de terceiros. Este artigo se concentra no dispositivo Cisco® ASA VPN, dispositivo Citrix NetScaler SSL VPN e Olá Juniper redes proteger acesso/Pulse Secure conectar seguro SSL dispositivo VPN. Criamos tooaddress de guias de configuração esses três dispositivos comuns, mas o servidor multi-Factor Authentication pode integrar com a maioria dos sistemas que usam o RADIUS, LDAP, IIS ou autenticação baseada em declarações tooAD FS. Você pode encontrar mais detalhes em [Configurações do servidor MFA](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Dispositivo de VPN Cisco ASA e Azure Multi-Factor Authentication
Autenticação multifator do Azure se integra com a Cisco® ASA VPN appliance tooprovide mais segurança para logons Cisco AnyConnect® VPN e acesso ao portal.  Isso pode ser feito usando o protocolo LDAP ou RADIUS hello.  Selecione uma das Olá toodownload Olá detalhadas passo a passo de configuração a seguir guias.

| Guia de configuração | Descrição |
| --- | --- |
| [Cisco ASA com VPN Anyconnect e configuração do Azure MFA para LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Integrar o dispositivo VPN Cisco ASA ao Azure MFA usando LDAP |
| [Configuração do Cisco ASA com VPN Anyconnect e do Azure MFA para RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Integrar o dispositivo VPN Cisco ASA ao Azure MFA usando RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>VPN do Citrix NetScaler SSL e Azure Multi-Factor Authentication
Autenticação multifator do Azure se integra com a Citrix NetScaler SSL VPN dispositivo tooprovide mais segurança para logons do Citrix NetScaler SSL VPN e acesso ao portal.  Isso pode ser feito usando o protocolo LDAP ou RADIUS hello.  Selecione uma das Olá toodownload Olá detalhadas passo a passo de configuração a seguir guias.

| Guia de configuração | Descrição |
| --- | --- |
| [Configuração da VPN do Citrix NetScaler SSL e do Azure MFA para LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Integrar a VPN Citrix NetScaler SSL ao dispositivo Azure MFA usando LDAP |
| [Configuração da VPN Citrix NetScaler SSL e do Azure MFA para RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Integrar o dispositivo VPN Citrix NetScaler SSL ao Azure MFA usando RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Dispositivo de VPN Juniper/Pulse Secure SSL e Azure Multi-Factor Authentication
Autenticação multifator do Azure se integra ao seu Juniper/Pulse Secure SSL VPN dispositivo tooprovide adicionais de segurança para logons Juniper/Pulse Secure SSL VPN e acesso ao portal.  Isso pode ser feito usando o protocolo LDAP ou RADIUS hello.  Selecione uma das Olá toodownload Olá detalhadas passo a passo de configuração a seguir guias.

| Guia de configuração | Descrição |
| --- | --- |
| [Configuração da VPN do Juniper/Pulse Secure SSL e do Azure MFA para LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Integrar o dispositivo VPN Juniper/Pulse Secure SSL ao Azure MFA usando LDAP |
| [Configuração da VPN do Juniper/Pulse Secure SSL e do Azure MFA para RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Integrar o dispositivo VPN Juniper/Pulse Secure SSL ao Azure MFA usando RADIUS |

## <a name="next-steps"></a>Próximas etapas

- [Aumentar sua infraestrutura de autenticação existente com hello extensão NPS para o Azure multi-Factor Authentication](multi-factor-authentication-nps-extension.md)

- [Definir as configurações da Autenticação Multifator do Azure](multi-factor-authentication-whats-next.md)