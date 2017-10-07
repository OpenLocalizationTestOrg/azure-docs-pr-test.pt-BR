---
title: "aaaAzure gerenciamento de segurança e visão geral do monitoramento | Microsoft Docs"
description: " O Azure fornece tooaid de mecanismos de segurança no gerenciamento de saudação e monitoramento de serviços de nuvem do Azure e máquinas virtuais.  Este artigo fornece uma visão geral desses recursos e serviços de segurança básicos. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Visão geral de monitoramento e gerenciamento de segurança do Azure
O Azure fornece tooaid de mecanismos de segurança no gerenciamento de saudação e monitoramento de serviços de nuvem do Azure e máquinas virtuais. Este artigo fornece uma visão geral desses recursos e serviços de segurança básicos. Links são fornecidos tooarticles que forneça os detalhes de cada para saber mais.

segurança de saudação de seus serviços de nuvem da Microsoft é uma parceria e responsabilidade compartilhada entre você e a Microsoft. Responsabilidade compartilhada significa que Microsoft é responsável por hello Microsoft Azure e a segurança física dos seus centros de dados (usando proteções de segurança, como portas de entrada do selo bloqueado, limites e protege). Além disso, o Azure fornece alta seguras níveis de segurança de nuvem na camada de software Olá que atenda às necessidades de conformidade dos seus clientes exigentes, privacidade e segurança de saudação.

Você possui os dados e identidades, responsabilidade Olá para protegê-los, Olá segurança de seus recursos locais e Olá segurança de componentes de nuvem em que você tem controle. A Microsoft fornece com toohelp de controles e recursos de segurança, você protege seus dados e aplicativos. O grau de responsabilidade de segurança é baseado no tipo de saudação do serviço de nuvem.

Olá gráfico a seguir resume o saldo de saudação de responsabilidade pelo Atendimento Microsoft e hello.

![Responsabilidade compartilhada][1]

Para uma análise aprofundada do gerenciamento de segurança, veja [Gerenciamento de segurança no Azure](azure-security-management.md).

Aqui estão Olá principais recursos toobe abordada neste artigo:

* Controle de Acesso Baseado em Função
* Antimalware
* Multi-Factor Authentication
* ExpressRoute
* Gateways de rede virtual
* Privileged Identity Management
* Identity Protection
* Central de Segurança

## <a name="role-based-access-control"></a>Controle de Acesso Baseado em Função
O RBAC (Controle de Acesso Baseado em Função) fornece o gerenciamento de acesso refinado para os recursos do Azure. Usando o RBAC, você pode conceder pessoas somente a quantidade Olá de acesso que eles precisam tooperform seus trabalhos.  RBAC também pode ajudar a garantir que quando as pessoas saem organização Olá percam tooresources acesso na nuvem hello.

Saiba mais:

* [Blog da equipe do Active Directory sobre o RBAC](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Controle de Acesso Baseado em Função do Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Antimalware
Com o Azure, você pode usar o software antimalware de fornecedores de segurança, como Microsoft, Symantec, Trend Micro, McAfee e Kaspersky toohelp proteger suas máquinas virtuais de arquivos mal-intencionados, adware e outras ameaças.

O Antimalware da Microsoft oferece que Olá capacidade tooinstall um agente de antimalware para funções de PaaS e máquinas virtuais. Com base no System Center Endpoint Protection, esse recurso oferece local comprovado nuvem de toohello de tecnologia de segurança.

Também oferecemos integração profunda da tendência [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ e [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ produtos em Olá plataforma Windows Azure. DeepSecurity é uma solução antivírus e SecureCloud é uma solução de criptografia. O DeepSecurity é implantado nas VMs com um modelo de extensão. Usando o portal de saudação da interface do usuário e o PowerShell, você pode escolher toouse DeepSecurity dentro de novas VMs estão sendo girados para cima ou VMs existentes que já foram implantados.

Também há suporte para o SEP (Symantec End Point Protection) no Azure. Por meio da integração de portal, os clientes podem especificar que pretendem toouse Set em uma VM. SET pode ser instalado em uma nova VM por meio do hello portal do Azure ou pode ser instalado em uma VM existente usando o PowerShell.

Saiba mais:

* [Implantando soluções antimalware em máquinas virtuais do Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Microsoft Antimalware para Serviços de Nuvem do Azure e máquinas virtuais](azure-security-antimalware.md)
* [Como tooinstall e configurar o Trend Micro Deep Security como um serviço em uma VM do Windows](../virtual-machines/windows/classic/install-trend.md)
* [Como tooinstall e configurar o Symantec Endpoint Protection em uma VM do Windows](../virtual-machines/windows/classic/install-symantec.md)
* [New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection (Novas opções de antimalware para proteção das Máquinas Virtuais do Azure – McAfee Endpoint Protection)](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Autenticação Multifator
Azure multi-factor authentication (MFA) é um método de autenticação que requer o uso de saudação de mais de um método de verificação e adiciona uma segunda camada crítica de segurança toouser entradas e transações. MFA ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de opções de verificação – chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou código de verificação e tokens OATH de terceiros.

Saiba mais:

* [Autenticação multifator](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [Como funciona o Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
O Microsoft Azure ExpressRoute permite estender suas redes locais no hello nuvem da Microsoft em uma conexão privada dedicada facilitada por um provedor de conectividade. Com o ExpressRoute, você pode estabelecer serviços de nuvem de tooMicrosoft de conexões, como o Microsoft Azure, Office 365 e CRM Online. A conectividade pode ocorrer de uma rede “qualquer para qualquer” (VPN IP), uma rede Ethernet ponto a ponto ou uma conexão cruzada virtual por meio de um provedor de conectividade em uma colocalização. Conexões de rota expressa não passam pela Olá Internet pública. Isso permite toooffer de conexões de rota expressa mais confiabilidade, velocidades mais rápidas, latências menores e maior segurança que as conexões típicas pela Internet da saudação.

Saiba mais:

* [Visão Geral Técnica do ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Gateways de rede virtual
Gateways de VPN, também chamado de Gateways de rede Virtual do Azure, são usados toosend o tráfego de rede entre redes virtuais e locais de local. Eles também são usadas toosend tráfego entre várias redes virtuais no Azure (VNet para VNet).  Os gateways de VPN fornecem conectividade segura entre instalações entre o Azure e sua infraestrutura.

Saiba mais:

* [Sobre gateways de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Azure Network Security Overview](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Às vezes, os usuários precisam toocarry operações privilegiadas em recursos do Azure ou outros aplicativos SaaS. Isso geralmente significa que as organizações têm toogive acesso privilegiado permanente-los no Azure Active Directory (AD do Azure). Esse é um risco de segurança cada vez maior para os recursos hospedados na nuvem, devido ao fato de as organizações não conseguirem monitorar de maneira adequada o que esses usuários estão fazendo com seu acesso com privilégios.
Além disso, se uma conta de usuário com acesso com privilégios for comprometida, essa violação poderá afetar a segurança geral da nuvem. O Azure AD Privileged Identity Management ajuda tooresolve esse risco, reduzindo o tempo de exposição de saudação de privilégios e aumenta a visibilidade em uso.  

Privileged Identity Management apresenta o conceito de saudação de um administrador temporário para uma função ou um "just in time" acesso de administrador, que é um usuário que precisa toocomplete um processo de ativação para essa função. alterações de processo de ativação Olá Olá atribuição Olá tooa da função de usuário no AD do Azure de tooactive inativa, por um período de tempo especificado como oito horas.

Saiba mais:

* [Gerenciamento de identidades com privilégios do AD do Azure](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Introdução ao Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Identity Protection
Proteção de identidade do Active Directory (AD) do Azure fornece uma exibição consolidada de atividades suspeitas entrar e proteger a sua empresa toohelp de vulnerabilidades potenciais. O Identity Protection detecta atividades suspeitas de usuários e identidades (administrador) com privilégios baseadas em sinais, tais como ataques de força bruta, perda de credenciais e entradas por meio de locais desconhecidos e dispositivos infectados.

Ao fornecer notificações e correção recomendada, Identity Protection ajuda a riscos toomitigate em tempo real. Ela calcula a gravidade de risco do usuário, e você pode configurar o acesso do aplicativo políticas com base em risco tooautomatically ajuda proteção contra ameaças futuras.

Saiba mais:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Canal 9: Azure AD e Identity Show: visualização do Identity Protection](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Central de Segurança
Central de segurança do Azure ajuda a evitar, detectar e responder toothreats e fornece que maior visibilidade e controle, segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Central de segurança ajuda a otimizar e monitorar a segurança de seus recursos do Azure por hello:

* Permitindo que você toodefine políticas para seus recursos de assinatura do Azure tooyour de acordo com a segurança da empresa precisa e Olá tipo de aplicativos ou confidencialidade dos dados de saudação em cada assinatura.
* Monitoramento de estado de saudação de suas máquinas virtuais do Azure, redes e aplicativos.
* Fornece uma lista de prioridade de alertas de segurança, incluindo alertas de parceiros integrados soluções, juntamente com informações de saudação necessário tooquickly investigar e recomendações sobre como tooremediate um ataque.

Saiba mais:

* [Introdução tooAzure Central de segurança](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
