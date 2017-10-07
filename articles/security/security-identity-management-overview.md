---
title: "segurança aaaAzure recursos que ajudam com o gerenciamento de identidades | Microsoft Docs"
description: " Este artigo fornece uma visão geral dos recursos de segurança do Azure do núcleo Olá ajudar no gerenciamento de identidade. Microsoft identidade e acesso de gerenciamento ajudam a soluções TI proteger acesso tooapplications e recursos em datacenter corporativo hello e em nuvem Olá, habilitando níveis adicionais de validação, como autenticação multifator e condicional políticas de acesso. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Visão geral da segurança de gerenciamento de identidade do Azure
Microsoft identidade e acesso de gerenciamento ajudam a soluções TI proteger acesso tooapplications e recursos em datacenter corporativo hello e em nuvem Olá, habilitando níveis adicionais de validação, como autenticação multifator e condicional políticas de acesso. O monitoramento de atividade suspeita por meio de alertas, auditoria e relatórios de segurança avançados ajuda a reduzir potenciais problemas de segurança. [O Azure Active Directory Premium](../active-directory/active-directory-editions.md) fornece toothousands de logon único de aplicativos de nuvem (SaaS) e acesso tooweb aplicativos executados no local.

Benefícios de segurança do Azure AD (Active Directory) incluem a capacidade de saudação:

* Criar e gerenciar uma identidade única para cada usuário em sua empresa híbrida, mantendo os usuários, grupos e dispositivos em sincronia
* Fornecer acesso de logon único tooyour aplicativos incluindo milhares de aplicativos SaaS pré-integrados
* Habilitar segurança de acesso do aplicativo por meio da aplicação do Multi-Factor Authentication com base em regras para aplicativos locais e na nuvem
* Provisionar o acesso remoto seguro local tooon web de aplicativos por meio do Proxy de aplicativo do Azure AD

Olá objetivo deste artigo é tooprovide uma visão geral dos recursos de segurança do Azure do núcleo Olá ajudar no gerenciamento de identidade. Nós também fornecemos links tooarticles que forneça os detalhes de cada recurso para saber mais.  

artigo Olá enfoca Olá principais recursos de gerenciamento de identidade do Azure a seguir:

* Logon único
* Proxy reverso
* Autenticação multifator
* Relatórios baseados em aprendizado de máquina, alertas e monitoramento de segurança
* Gerenciamento de acesso e identidade do consumidor
* Registro de dispositivos
* Privileged Identity Management
* Identity Protection
* Gerenciamento de identidade híbrida

## <a name="single-sign-on"></a>Logon único
Logon único (SSO) significa que está sendo tooaccess capaz de todos os aplicativos de saudação e recursos que você precisa toodo business, inscrevendo-se apenas uma vez usando uma conta de usuário único. Depois de conectado, você pode acessar todos os aplicativos de saudação sem sendo tooauthenticate necessário (por exemplo, digite uma senha) uma segunda vez.

Muitas organizações contam com o software como um aplicativo de serviço (SaaS) como o Office 365, Box e Salesforce para produtividade do usuário final. Historicamente, IT precisou tooindividually criar e atualizar contas de usuário em cada aplicativo SaaS, e os usuários tinham tooremember uma senha para cada aplicativo SaaS.

AD do Azure estende ambientes do Active Directory local para nuvem hello, permitindo que os usuários toouse seu primário toonot somente logon da conta organizacional tootheir domínio dispositivos e recursos da empresa, mas também todos os Olá web e aplicativos SaaS necessário para seu trabalho.

Não apenas os usuários não têm toomanage vários conjuntos de nomes de usuário e senhas, acesso de aplicativo pode ser automaticamente provisionados ou desprovisionados grupos organizacionais com base em e seu status como um funcionário. Apresenta a segurança do Azure AD e controles de controle de acesso que permitem que você toocentrally gerenciam o acesso dos usuários nos aplicativos SaaS.

Saiba mais:

* [Visão geral do logon único](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Integrar o logon único do Azure AD com aplicativos de SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Proxy reverso
Proxy de aplicativo do Azure AD permite que você publique aplicativos locais, tais como [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) sites, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), e [IIS](http://www.iis.net/)-com base em aplicativos na sua rede privada e fornece acesso seguro toousers fora da sua rede. Proxy de aplicativo fornece acesso remoto e -logon único (SSO) para vários tipos de web de aplicativos no local com hello milhares de aplicativos SaaS que dá suporte ao AD do Azure. Os funcionários podem fazer logon no tooyour aplicativos de casa em seus próprios dispositivos e autenticar através desse proxy baseado em nuvem.

Saiba mais:

* [Habilitando o Proxy de Aplicativo do AD do Azure.](../active-directory/active-directory-application-proxy-enable.md)
* [Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure](../active-directory/active-directory-application-proxy-publish.md)
* [Logon único com Proxy de Aplicativo](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Trabalhando com acesso condicional](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Autenticação multifator
Azure multi-factor authentication (MFA) é um método de autenticação que requer o uso de saudação de mais de um método de verificação e adiciona uma segunda camada crítica de segurança toouser entradas e transações. MFA ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de opções de verificação – chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou código de verificação e tokens OAuth de terceiros.

Saiba mais:

* [Autenticação multifator](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [Como funciona o Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Relatórios baseados em aprendizado de máquina, alertas e monitoramento de segurança
Monitoramento e alertas de segurança e relatórios baseados no aprendizado de máquina que identificam padrões de acesso inconsistentes podem ajudá-lo a proteger seus negócios. Você pode usar o acesso do Azure Active Directory e uso relatórios toogain visibilidade Olá integridade e segurança do diretório da sua organização. Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.

No hello portal clássico do Azure, os relatórios são categorizados em Olá maneiras a seguir:

* Relatórios de anomalias – contêm eventos que encontramos toobe anormais de conexão. Nosso objetivo é toomake você ciente de tais atividades e permitem que você toobe capaz de toomake uma decisão sobre se um evento é suspeito.
* Relatórios de aplicativos integrados: fornecem um panorama de como os aplicativos em nuvem estão sendo usados na sua organização. O Active Directory do Azure oferece integração com milhares de aplicativos em nuvem.
* Relatórios de erros – indica os erros que podem ocorrer ao provisionar contas tooexternal aplicativos.
* Relatórios específicos do usuário: exibem dados de atividade de entrada/dispositivo de um usuário específico.
* Logs de atividade – contém um registro de todos os eventos auditados em Olá últimas 24 horas, últimos 7 dias ou últimos 30 dias e alterações do grupo de atividade e atividade de registro e redefinição de senha.

Saiba mais:

* [Exibir relatórios de acesso e de uso](../active-directory/active-directory-view-access-usage-reports.md)
* [Introdução aos Relatórios do Active Directory do Azure](../active-directory/active-directory-reporting-getting-started.md)
* [Guia de Relatórios do Active Directory do Azure](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Gerenciamento de acesso e identidade do consumidor
B2C de diretório ativo do Azure é um serviço de gerenciamento de identidades global, altamente disponível para aplicativos voltados para o consumidor que pode ser dimensionado toohundreds de milhões de identidades. Ele pode ser integrado a plataformas móveis e da Web. Seus consumidores podem fazer logon tooall seus aplicativos por meio de experiências personalizáveis com suas contas sociais existentes ou criando novas credenciais.

Olá anterior, os desenvolvedores de aplicativos que desejavam toosign backup e os consumidores de entrar em seus aplicativos poderiam ter gravado seu próprio código. E teria que usar local bancos de dados ou sistemas toostore nomes de usuário e senhas. B2C de diretório ativo do Azure oferece um melhor forma toointegrate consumidor gerenciamento de identidades em aplicativos com a Ajuda de saudação de uma plataforma segura, baseado em padrões e um grande conjunto de políticas extensíveis de sua organização.

Quando você usa o Azure Active Directory B2C, os consumidores poderão se inscrever nos seus aplicativos usando suas contas sociais existentes (Facebook, Google, Amazon, LinkedIn) ou criando novas credenciais (endereço de email e senha ou o nome de usuário e a senha).

Saiba mais:

* [O que é o Azure Active Directory B2C?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Visualização do Active Directory B2C do Azure: inscrever e conectar consumidores em seus aplicativos](../active-directory-b2c/active-directory-b2c-overview.md)
* [Visualização do Azure Active Directory B2C: tipos de aplicativos](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Registro de dispositivos
O registro de dispositivo do AD do Azure é a base de saudação para baseado em dispositivo [acesso condicional](../active-directory/active-directory-conditional-access-device-registration-overview.md) cenários. Quando um dispositivo é registrado, o registro de dispositivo do Azure Active Directory fornece dispositivo Olá com uma identidade que é usado tooauthenticate hello quando Olá usuário entra em. dispositivo Olá autenticado e atributos de saudação do dispositivo hello, podem ser usado tooenforce políticas de acesso condicional para aplicativos hospedados na nuvem hello e local.

Quando combinado com uma solução MDM (gerenciamento) de dispositivos móveis como Intune, os atributos de dispositivo Olá no Active Directory do Azure são atualizados com informações adicionais sobre o dispositivo de saudação. Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade.

Saiba mais:

* [Introdução ao registro de dispositivos do Azure Active Directory](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Configurar o registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Active Directory (AD) Privileged Identity Management do Azure lhe permite gerenciar, controlar e monitorar suas identidades com privilégios e tooresources de acesso no AD do Azure, bem como outros serviços online da Microsoft como o Office 365 ou Microsoft Intune.

Às vezes, os usuários precisam toocarry operações privilegiadas em recursos do Azure ou Office 365 ou outros aplicativos SaaS. Isso geralmente significa que as organizações têm toogive acesso privilegiado permanente-las no AD do Azure. Esse é um risco de segurança cada vez maior para recursos hospedados em nuvem porque as organizações não podem monitorar de maneira suficiente o que esses usuários estão fazendo com seus privilégios de administrador. Além disso, se uma conta de usuário com acesso privilegiado for comprometida, essa falha poderá afetar a segurança geral da nuvem. O Azure AD Privileged Identity Management ajuda tooresolve esse risco.

O Gerenciamento de identidades com privilégios do AD do Azure:

* Ver quais usuários são administradores do Azure AD
* Habilitar sob demanda "just in time" tooMicrosoft acesso administrativo a serviços Online como o Office 365 e Intune
* Obter relatórios sobre o histórico de acesso de administrador e as alterações nas atribuições de administrador
* Receber alertas sobre a função de tooa de acesso privilegiado

Saiba mais:

* [Gerenciamento de identidades com privilégios do AD do Azure](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Funções no Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Como tooadd ou remover uma função de usuário](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Identity Protection
O Azure AD Identity Protection é um serviço de segurança que fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades da sua organização. O Identity Protection aproveita as funcionalidades de detecção de anomalias existentes do Azure Active Directory (disponíveis por meio dos Relatórios de Atividade Anômala do Azure AD) e apresenta novos tipos de evento de risco que podem detectar anomalias em tempo real.

Saiba mais:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Canal 9: Azure AD e Identity Show: visualização do Identity Protection](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Gerenciamento de identidade híbrida
Abordagem tooidentity abrange locais da Microsoft e nuvem hello, criando uma identidade de usuário único para autenticação e autorização tooall recursos, independentemente do local.

Saiba mais:

* [Hybrid identity white paper](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Active Directory do Azure](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog da equipe do Active Directory](https://blogs.technet.microsoft.com/ad/)
