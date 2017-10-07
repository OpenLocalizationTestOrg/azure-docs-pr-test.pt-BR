---
title: Perguntas frequentes sobre o Active Directory de aaaAzure | Microsoft Docs
description: Azure Active Directory perguntas frequentes sobre responde perguntas sobre como acessam a tooaccess do Azure e Active Directory do Azure, o gerenciamento de senhas e aplicativo.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Perguntas frequentes sobre o Azure Active Directory
O Azure AD (Azure Active Directory) é uma solução abrangente de IDaaS (identidade como um serviço) que inclui todos os aspectos de identidade, gerenciamento de acesso e segurança.

Para obter mais informações, confira [O que é Azure Active Directory?](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Acessar o Azure e o Azure Active Directory
**P: por que recebo "nenhuma assinatura encontrada" quando tento tooaccess AD do Azure no portal clássico do Azure de Olá?**

**R:** tooaccess Olá portal clássico do Azure, cada usuário precisa de permissões com uma assinatura do Azure. Se você tiver uma assinatura paga do Office 365 ou do AD do Azure, vá muito[http://aka.ms/accessAAD](http://aka.ms/accessAAD) para uma etapa única de ativação. Caso contrário, será necessário tooactivate livremente [conta do Azure](https://azure.microsoft.com/pricing/free-trial/) ou uma assinatura paga.

Para obter mais informações, consulte:

* [Como as assinaturas do Azure são associadas ao Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gerenciar o diretório de saudação para sua assinatura do Office 365 no Azure](active-directory-manage-o365-subscription.md)

- - -
**P: qual é a relação de saudação entre o AD do Azure, Office 365 e o Azure?**

**R:** AD do Azure fornece recursos comuns de identidade e acesso tooall os serviços da web. Se você estiver usando o Office 365, Microsoft Azure, Intune, ou outras pessoas, você está já usando o AD do Azure toohelp ativar o gerenciamento de logon e acesso para todos esses serviços.

Todos os usuários que estão configurados toouse os serviços da web são definidos como contas de usuário em uma ou mais instâncias do AD do Azure. Você pode configurar essas contas de recursos do Azure AD gratuitamente, como acesso a aplicativos de nuvem.

Serviços pagos do Azure AD, como Enterprise Mobility + Security, complementam outros serviços Web, como Office 365 e Microsoft Azure, com soluções abrangentes de segurança e gerenciamento de escala empresarial.
- - -
**P: por que entrar no portal do Azure de toohello mas não Olá portal clássico do Azure?**

**R:** hello portal do Azure não requer uma assinatura válida e o portal clássico Olá exigem uma assinatura válida.  Se você não tiver uma assinatura, você não pode entrar no portal clássico do toohello.
- - -
**P: quais são Olá diferenças entre o administrador de assinatura e administrador de diretório?**

**R:** por padrão, você recebe função de administrador de assinatura de saudação quando você se inscrever para o Azure. Um administrador de assinatura pode usar uma conta da Microsoft ou um trabalho ou escola conta do diretório Olá Olá assinatura do Azure está associada.  Essa função é serviços autorizados toomanage em Olá portal do Azure.

Se outras pessoas necessário toosign no e acessar serviços usando Olá a mesma assinatura, você pode adicioná-los como coadministradores. Essa função tem Olá mesmo privilégios de acesso Olá administrador de serviço, mas não é possível alterar a associação de saudação dos diretórios de tooAzure de assinaturas.  Para obter informações adicionais sobre administradores de assinatura, consulte [como tooadd ou alterar funções de administrador do Azure](../billing-add-change-azure-subscription-administrator.md) e [assinaturas do Azure como estão associadas com o Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


O AD do Azure tem um conjunto diferente de diretório do administrador funções toomanage hello e recursos relacionados à identidade.  Esses administradores terão acesso toovarious recursos no portal do Azure de saudação ou Olá portal clássico do Azure. Olá a função de admin determina o que podem fazer, como criar ou editar usuários, atribuir funções administrativas tooothers, redefinir senhas de usuário, gerenciar licenças de usuário ou gerenciar domínios.  Para obter informações adicionais sobre administradores de diretório do Azure AD e suas funções, confira [Atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md).

Além disso, os serviços pagos do Azure AD, como Enterprise Mobility + Security, complementam outros serviços Web, como Office 365 e Microsoft Azure, com soluções abrangentes de segurança e gerenciamento de escala empresarial.

- - -
**P: existe um relatório que mostra quando meu licenças de usuário do AD do Azure irá expirar?**

**R:** Não.  Isso não está disponível atualmente.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Introdução ao Azure AD Híbrido


**P: como sair de um locatário quando eu for adicionado como colaborador?**

**R:** ao locatário da organização tooanother são ser adicionado como um parceiro, você pode usar o hello "locatário alternador" em tooswitch direita superior do hello entre locatários.  Atualmente, não há nenhum Olá tooleave de maneira convidar organização e Microsoft está trabalhando para fornecer essa funcionalidade.  Até que esse recurso está disponível, você pode pedir Olá convidar tooremove da organização do seu locatário.
- - -
**P: como posso conectar meu tooAzure de diretório local AD?**

**R:** seu tooAzure de diretório local AD pode se conectar usando o Azure AD Connect.

Para saber mais, veja [Integrando identidades locais ao Azure Active Directory](active-directory-aadconnect.md).

- - -
**P: como configurar o SSO entre meu diretório local e meus aplicativos de nuvem?**

**R:** você só precisa tooset backup logon único (SSO) entre seu diretório local e o AD do Azure. Como acessar seus aplicativos na nuvem por meio do AD do Azure, serviço Olá unidades automaticamente os usuários toocorrectly autenticam com suas credenciais locais.

A implementação do SSO do local pode ser facilmente realizada com soluções de federação, como AD FS (Serviços de Federação Active Directory) ou configurando a sincronização de hash de senha. Você pode implantar facilmente as duas opções usando o Assistente de configuração do hello Azure AD Connect.

Para saber mais, veja [Integrando identidades locais ao Azure Active Directory](active-directory-aadconnect.md).

- - -
**P: o Azure AD oferece um portal de autoatendimento para usuários em minha organização?**

**R:** Sim, o AD do Azure fornece Olá [painel de acesso do AD do Azure](http://myapps.microsoft.com) de usuário de autoatendimento e acesso ao aplicativo. Se você for um cliente do Office 365, você pode encontrar muitos Olá mesmos recursos no portal de saudação Office 365.

Para obter mais informações, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

- - -
**P: o Azure AD me ajuda a gerenciar a infraestrutura local?**

**R:** Sim. edição do Azure AD Premium Olá fornece integridade de conexão do AD do Azure. O Azure AD Connect Health ajuda a monitorar e obter informações sobre sua identidade local hello e infraestrutura de serviços de sincronização.  

Para obter mais informações, consulte [monitorar seus serviços locais de infraestrutura e sincronização de identidade na nuvem Olá](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Gerenciamento de senhas
**P: posso usar o write-back de senha do Azure AD sem sincronização de senhas? (Neste cenário, é possível toouse AD do Azure redefinição de senha de autoatendimento (SSPR) com senha senhas write-back e não o armazenamento em nuvem Olá?)**

**R:** não é necessário toosynchronize seu Active Directory senhas tooAzure AD tooenable regravação. Em um ambiente federado, o AD do Azure-logon único (SSO) depende do usuário de Olá Olá local diretório tooauthenticate. Esse cenário não requer Olá local senha toobe controlada no AD do Azure.

- - -
**P: quanto tempo leva para um toobe senha gravado tooActive diretório local?**

**R:** o write-back de senha opera em tempo real.

Para saber mais, confira [Introdução ao gerenciamento de senhas](active-directory-passwords-getting-started.md).

- - -
**P: posso usar o write-back de senha com senhas que são gerenciadas por um administrador?**

**R:** Sim, se você tiver o write-back de senha habilitado, operações de saudação de senha executadas por um administrador são gravadas tooyour ambiente de local.  

Para obter respostas mais perguntas toopassword relacionados, consulte [perguntas frequentes sobre o gerenciamento de senha](active-directory-passwords-faq.md).
- - -
**P: o que fazer se eu não consiga se lembrar minha senha existente do Office 365/Azure AD durante a tentativa de toochange minha senha?**

**R:** para esse tipo de situação, há algumas opções.  Use SSPR (redefinição de senha de autoatendimento), se estiver disponível.  O funcionamento de SSPR dependerá de como está configurado.  Para obter mais informações, consulte [como senha Olá redefinir trabalho portal](active-directory-passwords-best-practices.md).

Para usuários do Office 365, o administrador pode redefinir senha hello usando Olá etapas descritas em [redefinir senhas de usuário](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Para contas do AD do Azure, os administradores podem redefinir senhas usando um dos seguintes hello:

- [Redefinir contas Olá portal do Azure](active-directory-users-reset-password-azure-portal.md)
- [Redefinir contas no portal clássico Olá](active-directory-create-users-reset-password.md)
- [Usando o PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Segurança
**P: As contas são bloqueadas após uma quantidade específica de tentativas com falha, ou uma estratégia mais sofisticada é usada?**</br>
Podemos usar contas de toolock estratégia mais sofisticadas.  Isso se baseia em Olá IP da solicitação de saudação e senhas Olá inseridas. duração de saudação de bloqueio de saudação também aumenta com base na probabilidade de saudação que se trata de um ataque.  

**P: determinados senhas (comuns) recusadas por hello mensagens 'essa senha tiver sido usado toomany vezes', isso faz referência toopasswords usado no active directory de saudação atual?**</br>
Isso se refere a toopasswords globalmente comuns, como qualquer variantes de "Senha" e "123456".

**P: Uma solicitação de entrada de fontes questionáveis (botnets, ponto de extremidade tor) será bloqueada em um locatário B2C, ou isso exige um locatário de edição Basic ou Premium?**</br>
Temos um gateway que filtra solicitações e fornece alguma proteção contra botnets, e ele é aplicado a todos os locatários B2C.

## <a name="application-access"></a>Acesso a aplicativos
**P: onde obter uma lista de aplicativos que estão pré-integrados ao Azure AD e seus recursos?**

**R:** o Azure AD tem mais de 2.600 aplicativos pré-integrados da Microsoft, provedores de serviços de aplicativos e parceiros. Todos os aplicativos pré-integrados dão suporte ao SSO (logon único). SSO permite usar suas credenciais organizacionais tooaccess seus aplicativos. Alguns aplicativos Olá também oferecem suporte a provisionamento e cancelamento de provisionamento automatizado.

Para obter uma lista completa de aplicativos pré-integrados hello, consulte Olá [Marketplace do Active Directory](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**P: se hello aplicativo que necessário não está no marketplace do AD do Azure Olá?**

**R:** com o Azure AD Premium, você pode adicionar e configurar qualquer aplicativo que desejar. Dependendo dos recursos do aplicativo e de suas preferências, você pode configurar o SSO e o provisionamento automatizado.  

Para obter mais informações, consulte:

* [Configurando um único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure Olá](active-directory-saas-custom-apps.md)
* [Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications](active-directory-scim-provisioning.md)

- - -
**P: como os usuários entrar em tooapplications usando o AD do Azure?**

**R:** AD do Azure fornece várias maneiras para os usuários tooview e acessar seus aplicativos, tais como:

* Painel de acesso de saudação do AD do Azure
* iniciador do aplicativo Hello Office 365
* Aplicativos de toofederated de entrada direta
* Links profundos toofederated, com base em senha, ou aplicativos existentes

Para obter mais informações, consulte [Implantando o AD do Azure integrado a aplicativos toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**P: quais são maneiras diferentes de saudação do AD do Azure permite a autenticação e tooapplications de logon único?**

**R:** o Azure AD dá suporte a vários protocolos padronizados para autenticação e autorização, como SAML 2.0, OpenID Connect, OAuth 2.0 e WS-Federation. O Azure AD também dá suporte a cofres de senhas e recursos de entrada automatizada para aplicativos que dão suporte apenas à autenticação baseada em formulários.  

Para obter mais informações, consulte:

* [Cenários de autenticação do Azure AD](active-directory-authentication-scenarios.md)
* [Protocolos de autenticação do Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Como funciona o logon único com o Active Directory do Azure?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**P: posso adicionar aplicativos que estou executando no local?**

**R:** Proxy de aplicativo do Azure AD oferece acesso fácil e seguro aplicativos web tooon local que você escolher. Você pode acessar esses aplicativos em Olá mesma maneira que você acessar o software como um serviço (SaaS) de aplicativos no AD do Azure. Não é necessário para uma VPN ou toochange sua infraestrutura de rede.  

Para obter mais informações, consulte [como tooprovide proteger o acesso remoto aplicativos locais tooon](active-directory-application-proxy-get-started.md).

- - -
**P: como exigir a autenticação multifator para usuários que acessam determinado aplicativo?**

**R:** com o acesso condicional do Azure AD, você pode atribuir uma política de acesso exclusiva para cada aplicativo. Em sua política, você pode exigir a autenticação multifator sempre ou quando os usuários não são rede local toohello conectado.  

Para obter mais informações, consulte [tooOffice 365 e outros aplicativos de proteção de acesso conectado tooAzure do Active Directory](active-directory-conditional-access.md).

- - -
**P: o que é o provisionamento automatizado de usuário para aplicativos SaaS?**

**R:** criação de saudação tooautomate usar o AD do Azure, manutenção e remoção das identidades de usuário no número de aplicativos SaaS populares de nuvem.

Para obter mais informações, consulte [automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](active-directory-saas-app-provisioning.md).

- - -
**P: posso configurar uma conexão LDAP segura com o Azure AD?**

**R:**  Não. O AD do Azure não oferece suporte a protocolo LDAP de saudação.
