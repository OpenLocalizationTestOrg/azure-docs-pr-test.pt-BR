---
title: "aaaArticle índice para gerenciamento de aplicativos no Active Directory do Azure | Microsoft Azure"
description: "Saiba como data de validade de saudação toocustomize para seus certificados de Federação e como toorenew certificados que expirará em breve."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Índice de artigos sobre gerenciamento de aplicativos no Active Directory do Azure
Esta página fornece uma lista abrangente de cada documento escrito sobre Olá vários recursos relacionados ao aplicativo no Azure Active Directory (AD do Azure).

Há uma área de recurso principal tooeach breve introdução, bem como orientação sobre quais tooread artigos dependendo de quais informações você está procurando.

## <a name="overview-articles"></a>Artigos de visão geral
artigos de saudação abaixo são bons pontos de partida para aqueles que desejam simplesmente uma breve explicação de recursos de gerenciamento de aplicativo do AD do Azure.

| Guia de artigos |  |
|:---:| --- |
| Um problemas de gerenciamento de aplicativo toohello de Introdução que resolve do AD do Azure |[Gerenciando aplicativos com o AD do Azure (Active Directory do Azure)](active-directory-enable-sso-scenario.md) |
| Uma visão geral da saudação vários recursos no AD do Azure relacionados tooenabling logon único, definir quem tem acesso tooapps e como os usuários iniciam aplicativos |[Acesso aos aplicativos e logon único no Active Directory do Azure](active-directory-appssoaccess-whatis.md) |
| Examinar Olá diferentes etapas envolvidas ao integrar aplicativos no AD do Azure |[Integrando aplicativos com o Azure Active Directory](active-directory-integrating-applications-getting-started.md)<br /><br />[Habilitar logon único tooSaaS aplicativos](active-directory-sso-integrate-saas-apps.md)<br /><br />[Gerenciando acesso tooApps](active-directory-managing-access-to-apps.md) |
| Uma explicação técnica de como os aplicativos são representados no AD do Azure |[Como e por que os aplicativos são adicionados tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Artigos de solução de problemas
Esta seção fornece acesso rápido toorelevant guias de solução de problemas. Para obter mais informações sobre cada área de recurso podem ser encontradas em rest Olá desta página.

| Área de recurso |  |
|:---:| --- |
| Logon único federado |[Solução de problemas de logon único baseado em SAML](active-directory-saml-debugging.md) |
| Logon único baseado em senha |[Solução de problemas Olá extensão do painel de acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Proxy de Aplicativo |[Guia de solução de problemas de Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md) |
| Logon único entre o AD local e o AD do Azure |[Solução de problemas de sincronização de senha](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Solucionar problemas de write-back de senha](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Associações de grupo dinâmico |[Solucionar problemas de associações a grupos dinâmicos](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>SSO (Logon único)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Logon único federado: logon em muitos aplicativos usando uma identidade
Logon único permite que os usuários tooaccess uma variedade de aplicativos e serviços usando apenas um conjunto de credenciais. Federação é um método por meio do qual você pode habilitar o logon único. Quando os usuários tentam toosign em aplicativos federados, elas receberão oficial entrar página da organização tootheir redirecionado processada pelo Active Directory do Azure e são então aplicativo toohello back redirecionado após a autenticação bem-sucedida.

| Guia de artigos |  |
|:---:| --- |
| Uma introdução toofederation e outros tipos de logon |[Logon único com o AD do Azure](active-directory-appssoaccess-whatis.md) |
| Milhares de aplicativos SaaS pré-integrados com o AD do Azure com etapas de configuração de logon único simplificadas |[Introdução à Galeria de aplicativos do AD do Azure Olá](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Lista completa de aplicativos pré-integrados que dão suporte à federação](http://aka.ms/aadfederatedapps)<br /><br />[Como seu aplicativo de tooAdd toohello Galeria de aplicativo do Azure AD](active-directory-app-gallery-listing.md) |
| Mais de 150 tutoriais de aplicativo em como tooconfigure o logon único para aplicativos como [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md)e muito mais |[Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure](active-directory-saas-tutorial-list.md) |
| Como toomanually configurar e personalizar a configuração de logon único |[Como tooConfigure tooApps federado logon único que não estão em Olá Galeria de aplicativos do Azure Active Directory](active-directory-saas-custom-apps.md)<br /><br />[Como tooCustomize as declarações emitidas no hello Token SAML para aplicativos Pre-Integrated](active-directory-saml-claims-customization.md) |
| Guia para aplicativos federados que usam o protocolo do SAML Olá solução de problemas |[Solução de problemas de logon único baseado em SAML](active-directory-saml-debugging.md) |
| Como tooconfigure data de expiração do certificado do aplicativo e como toorenew seus certificados |[Gerenciamento de certificados para logon único federado no Active Directory do Azure](active-directory-sso-certs.md) |

Logon único federado está disponível para todas as edições do AD do Azure para backup tooten aplicativos por usuário. [AD do Azure Premium](https://azure.microsoft.com/pricing/details/active-directory/) oferece suporte a uma quantidade ilimitada de aplicativos. Se sua organização tiver [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), em seguida, você pode [use grupos de aplicativos do tooassign acesso toofederated](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Logon único com base em senha: compartilhamento de conta e SSO para aplicativos não federados
tooenable único logon tooapplications que não oferecem suporte a federação, o AD do Azure oferece senha recursos de gerenciamento que podem armazenar com segurança senhas tooSaaS aplicativos e entrar automaticamente os usuários esses aplicativos. Você pode distribuir facilmente as credenciais para contas recém-criadas e compartilhar contas de equipe com várias pessoas. Os usuários não precisam necessariamente tooknow Olá credenciais toohello contas de acesso para que eles recebem.

| Guia de artigos |  |
|:---:| --- |
| Funciona SSO baseada em senha uma introdução toohow e uma breve visão geral técnica |[Logon único com base em senha com o AD do Azure](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Um resumo dos cenários de saudação relacionadas tooaccount compartilhamento e como esses problemas serão resolvidos pelo AD do Azure |[Compartilhar contas com o AD do Azure](active-directory-sharing-accounts.md) |
| Alterar senha Olá para determinados aplicativos automaticamente em intervalos regulares |[Substituição de senha automática (visualização)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Implantação e solução de problemas guias para a versão do Internet Explorer de saudação do hello extensão de gerenciamento de senha do AD do Azure |[Como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo](active-directory-saas-ie-group-policy.md)<br /><br />[Solução de problemas Olá extensão do painel de acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Com base em senha de logon único está disponível para todas as edições do AD do Azure para backup tooten aplicativos por usuário. [AD do Azure Premium](https://azure.microsoft.com/pricing/details/active-directory/) oferece suporte a uma quantidade ilimitada de aplicativos. Se sua organização tiver [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), em seguida, você pode [use grupos tooassign acesso tooapplications](#managing-access-to-applications). A substituição de senha automática é um recurso do [AD do Azure Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Proxy de aplicativo: Aplicativos de locais de tooon de único logon e acesso remoto
Se você tiver aplicativos em sua rede privada que precisam toobe acessado por usuários e dispositivos fora da rede hello, você pode usar o Proxy de aplicativo do Azure AD tooenable acesso remoto seguro toothose aplicativos.

| Guia de artigos |  |
|:---:| --- |
| Visão geral do Proxy de Aplicativo do AD do Azure e como ele funciona |[Fornecer acesso remoto seguro a aplicativos locais tooon](active-directory-application-proxy-get-started.md) |
| Tutoriais sobre como tooconfigure Proxy de aplicativo e como toopublish seu primeiro aplicativo |[Como tooSet o Proxy de aplicativo do Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Como instalar tooSilently Olá conector de Proxy de aplicativo](active-directory-application-proxy-silent-installation.md)<br /><br />[Como tooPublish aplicativos usando o Proxy de aplicativo](active-directory-application-proxy-publish.md)<br /><br />[Como tooUse seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md) |
| Como tooenable único acesso condicional e logon para os aplicativos publicados com o Proxy de aplicativo |[Logon único com Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Acesso condicional e Proxy de Aplicativo](active-directory-application-proxy-conditional-access.md) |
| Orientação sobre como toouse Proxy de aplicativo para os seguintes cenários de saudação |[Como tooSupport aplicativos clientes nativos](active-directory-application-proxy-native-client.md)<br /><br />[Como tooSupport aplicativos com reconhecimento de declarações](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Como tooSupport aplicativos publicados em redes separadas e locais](active-directory-application-proxy-connectors.md) |
| Guia de solução de problemas de Proxy de Aplicativo |[Guia de solução de problemas de Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md) |

Proxy de aplicativo está disponível para todas as edições do AD do Azure para backup tooten aplicativos por usuário. [AD do Azure Premium](https://azure.microsoft.com/pricing/details/active-directory/) oferece suporte a uma quantidade ilimitada de aplicativos. Se sua organização tiver [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), em seguida, você pode [use grupos tooassign acesso tooapplications](#managing-access-to-applications).

Você também pode estar interessado em [serviços de domínio do AD do Azure](../active-directory-domain-services/active-directory-ds-overview.md), que permite a você toomigrate sua tooAzure de aplicativos local ao mesmo tempo, ainda que satisfazem a identidade de saudação precisa desses aplicativos.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Habilitação do logon único entre o AD do Azure e o AD local
Se sua organização mantém um Windows Server Active Directory no local junto com o Active Directory do Azure na nuvem hello, você provavelmente desejará tooenable logon único entre esses dois sistemas. O Azure AD Connect (ferramenta de saudação que integra-se esses dois sistemas juntos) fornece várias opções para configurar o logon único: estabelecer federação com o AD FS ou outro provedor de Federação ou habilitar a sincronização de senha.

| Guia de artigos |  |
|:---:| --- |
| Uma visão geral sobre as opções de logon único Olá oferecidos no Azure AD Connect, bem como informações sobre o gerenciamento de ambientes híbridos |[Opções de logon único do usuário no Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Diretrizes gerais para o gerenciamento de ambientes com o Active Directory local e o Active Directory do Azure |[Considerações de design da Identidade Híbrida Azure AD](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Integração de suas identidades locais com o Azure Active Directory](active-directory-aadconnect.md) |
| Orientação sobre como usar a sincronização de senha tooenable SSO |[Implementar a sincronização de senha com o Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Solucionar problemas de sincronização de senha](https://support.microsoft.com/en-us/kb/2855271) |
| Orientação sobre como usar o write-back de senha tooenable SSO |[Introdução ao Gerenciamento de Senhas no Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Solucionar problemas de write-back de senha](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Orientação sobre como usar tooenable de provedores de identidade de terceiros SSO |[Lista de tooEnable compatível de terceiros identidade provedores que podem ser usados Single Sign-On](https://aka.ms/ssoproviders) |
| Como os usuários do Windows 10 podem aproveitar os benefícios de saudação do logon único por meio de junção do Azure AD |[Estendendo os recursos de nuvem tooWindows 10 dispositivos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-overview.md) |

O Azure AD Connect está disponível para [todas as edições do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). O Autoatendimento de Redefinição de Senha do Azure AD está disponível para o [Azure AD Básico](https://azure.microsoft.com/pricing/details/active-directory/) e o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Write-back de senha tooon-local AD é um [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) recurso.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Acesso condicional: imponha requisitos adicionais de segurança a aplicativos de alto risco
Depois de configurar recursos e aplicativos de tooyour de logon único, em seguida, proteção adicional para aplicativos confidenciais através da aplicação de requisitos específicos de segurança em todos os aplicativos de entrada toothat. Por exemplo, você pode usar o AD do Azure toodemand que todo acesso tooa determinado aplicativo sempre exigem a autenticação multifator, independentemente de estarem ou não que o aplicativo intrinsecamente dá suporte a essa funcionalidade. Outro exemplo comum de acesso condicional é toorequire que os usuários sejam conectados toohello organização um particularmente confidenciais de aplicativos de rede na ordem tooaccess confiável.

| Guia de artigos |  |
|:---:| --- |
| Os recursos de acesso condicional uma introdução toohello oferecidos em AD do Azure, Office 365 e Intune |[Gerenciamento de riscos com acesso condicional](active-directory-conditional-access.md) |
| Como acessar o tooenable condicional para Olá seguintes tipos de recursos |[Acesso condicional para aplicativos SaaS](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Acesso condicional para serviços do Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Acesso condicional para aplicativos locais](active-directory-conditional-access.md)<br /><br />[Acesso condicional para aplicativos locais publicados por meio do Proxy de Aplicativo do Azure AD](active-directory-application-proxy-conditional-access.md) |

| Como dispositivos de tooregister com o Active Directory do Azure no pedido tooenable políticas de acesso condicional baseado em dispositivo | [Visão geral do registro de dispositivo do Active Directory do Azure](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Como tooEnable registro de dispositivo automático para dispositivos Windows que ingressaram no domínio](active-directory-conditional-access-automatic-device-registration.md)<br />— [Etapas para dispositivos com Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Etapas para dispositivos com Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Como toouse Olá aplicativo Authenticator da Microsoft para verificação em duas etapas | [Autenticador da Microsoft](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

O Acesso Condicional é um recurso do [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

## <a name="apps--azure-ad"></a>Aplicativos e AD do Azure
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: localize quais aplicativos SaaS estão sendo usados em sua organização
Cloud App Discovery ajuda os departamentos de TI Saiba quais aplicativos SaaS estão sendo usados em toda a organização de saudação. Ele pode medir o uso do aplicativo e popularidade, para que ele possa determinar quais aplicativos serão beneficiadas Olá mais do que está sendo colocado sob controle de TI e que está sendo integrado ao AD do Azure.

| Guia de artigos |  |
|:---:| --- |
| Uma visão geral de como isso funciona |[Encontrando aplicativos em nuvem não autorizados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Aprofundar em como ele funciona, com tooquestions respostas em privacidade |[Considerações de privacidade e segurança](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Perguntas frequentes |[Perguntas frequentes sobre o Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Tutoriais para implantação do Cloud App Discovery |[Guia de implantação de política de grupo](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Guia de implantação do System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Instalação em servidores proxy com portas personalizadas](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Olá alterar o log para o agente de atualizações de Cloud App Discovery toohello |[Log de alterações](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

O Cloud App Discovery é um recurso do [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Provisionar e desprovisionar automaticamente as contas de usuário em aplicativos SaaS
Automatize Olá criação, manutenção e remoção das identidades de usuário em aplicativos SaaS como o Dropbox, Salesforce, ServiceNow e muito mais. Corresponder e sincronização de identidades existentes entre o AD do Azure e seus aplicativos SaaS e controlar o acesso desabilitando contas automaticamente quando os usuários saírem Olá organização.

| Guia de artigos |  |
|:---:| --- |
| Saiba mais sobre como ele funciona e encontrar respostas a perguntas toocommon |[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos](active-directory-saas-app-provisioning.md) |
| Configurar como as informações são mapeadas entre o AD do Azure e seu aplicativo SaaS |[Personalizando mapeamentos de atributo](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Escrevendo expressões para mapeamentos de atributo](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Como tooenable automatizado provisionamento aplicativo tooany que oferece suporte ao protocolo SCIM Olá |[Configurar o provisionamento automatizado de usuários tooany SCIM-Enabled aplicativo](active-directory-scim-provisioning.md) |
| Como tooreport em e solucionar problemas de provisionamento do usuário |[Relatórios sobre o provisionamento automático de usuário](active-directory-saas-provisioning-reporting.md)<br><br>[Notificações de provisionamento](active-directory-saas-account-provisioning-notifications.md)<br><br>[Solução de problemas de provisionamento do usuário](active-directory-application-provisioning-content-map.md) |
| Limitar quem recebe aplicativo tooan provisionados com base em seus valores de atributo |[Filtro de escopo](active-directory-saas-scoping-filters.md) |

Provisionamento automatizado de usuários está disponível para todas as edições do AD do Azure para backup tooten aplicativos por usuário. [AD do Azure Premium](https://azure.microsoft.com/pricing/details/active-directory/) oferece suporte a uma quantidade ilimitada de aplicativos. Se sua organização tiver [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) ou [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), em seguida, você pode [usar grupos toomanage que os usuários sejam provisionados](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Compilação de aplicativos integrados ao AD do Azure
Se sua organização está desenvolvendo ou manutenção de linha de negócios (LoB) aplicativos, ou se você for um desenvolvedor de aplicativo com clientes que usam o Active Directory do Azure, Olá tutoriais a seguir irá ajudá-lo a integrar seus aplicativos com o AD do Azure.

| Guia de artigos |  |
|:---:| --- |
| Orientação para profissionais de TI e desenvolvedores de aplicativos sobre a integração de aplicativos ao AD do Azure |[Guia de saudação do profissional de TI para desenvolver aplicativos do AD do Azure](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Guia do desenvolvedor de saudação do Active Directory do Azure](active-directory-developers-guide.md) |
| Como fornecedores de tooapplication adicionar toohello seus aplicativos Galeria de aplicativo do Azure AD |[Listando seu aplicativo no hello Galeria de aplicativos do Azure Active Directory](active-directory-app-gallery-listing.md) |
| Como toomanage acessar toodeveloped aplicativos usando o Active Directory do Azure |[Como atribuição de usuário para aplicativos desenvolvidos de tooEnable](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Atribuir usuários tooyour aplicativo](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Atribuindo grupo tooyour aplicativo](active-directory-applications-guiding-developers-assigning-groups.md) |

Se você estiver desenvolvendo aplicativos voltados para o consumidor, você pode estar interessado em usar [do Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) para que você não tem sua própria toomanage de sistema de identidade toodevelop seus usuários. [Saiba mais](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Gerenciando acesso tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Usando grupos e toomanage autoatendimento que tenha acesso toowhich aplicativos
toohelp gerenciados que devem ter acesso toowhich recursos, Active Directory do Azure permite que você tooset atribuições e permissões em escala usando grupos. IT poderá tooenable recursos de autoatendimento para que os usuários podem simplesmente solicitar permissão quando necessário.

| Guia de artigos |  |
|:---:| --- |
| Uma visão geral dos recursos de gerenciamento de acesso do AD do Azure |[Introdução tooManaging tooApps de acesso](active-directory-managing-access-to-apps.md)<br /><br />[Como funciona o gerenciamento de acesso no Azure AD](active-directory-manage-groups.md)<br /><br />[Como tooUse grupos tooManage acesso tooSaaS aplicativos](active-directory-accessmanagement-group-saasapps.md) |
| Habilitar o gerenciamento por autoatendimento de aplicativos e grupos |[Gerenciamento de aplicativos de autoatendimento](active-directory-self-service-application-access.md)<br /><br />[Gerenciamento de grupo de autoatendimento](active-directory-accessmanagement-self-service-group-management.md) |
| Instruções para configuração de seus grupos no AD do Azure |[Como tooCreate grupos de segurança](active-directory-accessmanagement-manage-groups.md)<br /><br />[Como tooDesignate proprietários para um grupo](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Como tooUse hello "todos os usuários" do grupo](active-directory-accessmanagement-dedicated-groups.md) |
| Use grupos dinâmicos tooautomatically popular a associação de grupo usando regras de associação com base em atributo |[Associação de grupo dinâmico: regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Solucionar problemas de associações a grupos dinâmicos](active-directory-accessmanagement-troubleshooting.md) |

O gerenciamento de acesso de aplicativo baseado em grupo está disponível para o [Azure AD Básico](https://azure.microsoft.com/pricing/details/active-directory/) e o [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). O gerenciamento de grupo de autoatendimento, o gerenciamento de aplicativos de autoatendimento e os grupos dinâmicos são recursos do [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) .

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>Colaboração B2B: Habilitar tooapplications de acesso do parceiro
Se sua empresa tem uma parceria com outras empresas, é provável que você precisa de aplicativos corporativos do tooyour toomanage parceiro acesso. Colaboração do Azure de B2B do Active Directory fornece uma maneira fácil e seguro tooshare seus aplicativos com parceiros.

| Guia de artigos |  |
|:---:| --- |
| Uma visão geral de diferentes recursos do AD do Azure que podem ajudar você a gerenciar usuários externos, como parceiros, clientes etc. |[Comparando recursos de gerenciamento de identidades externas no AD do Azure](active-directory-b2b-compare-external-identities.md) |
| Uma introdução tooB2B como tooget iniciada e colaboração |[Integração de parceiros de nuvem simples e segura com o Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Colaboração B2B do Azure Active Directory](active-directory-b2b-collaboration-overview.md) |
| Aprofundar em colaboração B2B do Azure AD e como toouse-lo |[Colaboração B2B: como funciona](active-directory-b2b-how-it-works.md)<br /><br />[Limitações atuais da Colaboração B2B do Azure AD](active-directory-b2b-current-limitations.md)<br /><br />[Passo a passo detalhado do uso da Colaboração B2B do Azure AD](active-directory-b2b-detailed-walkthrough.md) |
| Artigos de referência com detalhes técnicos sobre o funcionamento da Colaboração B2B do AD do Azure |[Formato de arquivo CSV para adicionar usuários do parceiro](active-directory-b2b-references-csv-file-format.md)<br /><br />[Atributos de usuário afetados pela colaboração B2B do Azure AD](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Formato de token de usuário para usuários parceiros](active-directory-b2b-references-external-user-token-format.md) |

A Colaboração B2B está disponível atualmente para [todas as edições do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Painel de acesso: um portal para acessar aplicativos e recursos de autoatendimento
Olá painel de acesso do AD do Azure é onde os usuários finais podem iniciar seus aplicativos e acesso Olá recursos de autoatendimento que permitem a eles toomanage seus aplicativos e as associações de grupo. Além disso, toohello painel de acesso, outras opções para acessar aplicativos habilitados do SSO são incluídos na lista de saudação abaixo.

| Guia de artigos |  |
|:---:| --- |
| Uma comparação de saudação diferentes opções disponíveis para a implantação de aplicativos de logon único toousers |[Implantando aplicativos integrados do Azure AD tooUsers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Uma visão geral do hello painel de acesso e seu MyApps equivalente móvel |[Introdução tooAccess painel e MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Como os aplicativos tooaccess AD do Azure Olá site do Office 365 |[Usando Olá o iniciador do aplicativo do Office 365](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Como aplicativos tooaccess AD do Azure Olá aplicativo móvel do Intune Managed Browser |[Navegador gerenciado do Intune](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Como os aplicativos de tooaccess AD do Azure usando links profundos tooinitiate o logon único |[Obtendo Links diretos logon tooYour aplicativos](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

O Painel de Acesso está disponível para [todas as edições do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Relatórios: Facilmente as alterações de acesso do aplicativo de auditoria e monitorar tooapps entradas
Active Directory do Azure fornece vários relatórios e alertas toohelp monitorar tooapplications de acesso da sua organização. Você pode receber alertas para aplicativos de tooyour-conexões anormais, e você pode controlar quando e por que o aplicativo de tooan de acesso de um usuário foi alterado.

| Guia de artigos |  |
|:---:| --- |
| Uma visão geral da saudação reporting recursos no Active Directory do Azure |[Introdução aos relatórios do AD do Azure](active-directory-reporting-getting-started.md) |
| Como toomonitor Olá entradas e o uso de aplicativos de seus usuários |[Exibir relatórios de acesso e de uso](active-directory-view-access-usage-reports.md) |
| Controlar alterações feitas toowho podem acessar um aplicativo específico |[Eventos de relatório de auditoria do Active Directory do Azure](active-directory-reporting-audit-events.md) |
| Exportar dados de saudação dessas ferramentas tooyour preferido de relatórios usando Olá API Reporting |[Guia de Introdução com hello API Reporting do AD do Azure](active-directory-reporting-api-getting-started.md) |

toosee quais relatórios estão incluídos com diferentes edições do Active Directory do Azure, [clique aqui](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Consulte também
[O que é o Active Directory do Azure?](active-directory-whatis.md)

[Active Directory B2C do Azure](https://azure.microsoft.com/services/active-directory-b2c/)

[Serviços de Domínio do Active Directory do Azure](https://azure.microsoft.com/services/active-directory-ds/)

[Autenticação Multifator do Azure](https://azure.microsoft.com/services/multi-factor-authentication/)
