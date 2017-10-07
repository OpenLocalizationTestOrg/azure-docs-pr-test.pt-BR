---
title: "Perguntas frequentes (FAQ) – Azure AD B2C | Microsoft Docs"
description: Perguntas frequentes sobre o Active Directory B2C do Azure.
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: Perguntas frequentes (FAQ) 
Esta página respostas a perguntas frequentes sobre Olá B2C do Azure Active Directory (AD do Azure). Continue verificando as atualizações.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>Posso usar recursos do AD B2C do Azure no locatário existente de AD do Azure, com base em funcionário?
O AD do Azure e Azure AD B2C são ofertas de produtos separada e não podem coexistir no hello mesmo locatário.  Um locatário do Azure AD representa uma organização.  Um locatário Azure AD B2C representa uma coleção de identidades toobe usado com aplicativos de terceira parte confiável.  Com as políticas personalizadas (em visualização pública), o Azure AD B2C pode federar tooAzure AD permitindo a autenticação de funcionários em uma organização.

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Pode usar o Azure AD B2C tooprovide logon social (Facebook e Google +) no Office 365?
B2C do Azure AD não pode ser usado tooauthenticate usuários para o Microsoft Office 365.  AD do Azure é a solução da Microsoft para o gerenciamento de aplicativos de tooSaaS de acesso de funcionários e tem recursos projetados para essa finalidade, como acesso condicional e licenciamento.  O Azure AD B2C fornece uma plataforma de gerenciamento de identidade e acesso para a criação de aplicativos Web e móveis.  Quando o Azure AD B2C é configurado toofederate tooan locatário do AD Azure, Olá locatário do AD Azure gerencia tooapplications de acesso de funcionários que se baseiam no Azure AD B2C.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>O que são contas locais no AD B2C do Azure? Como elas são diferentes de contas corporativas ou de estudante no AD do Azure?
Em um locatário do AD do Azure, os usuários que pertencem a toohello locatário entrar com um endereço de email do formulário Olá `<xyz>@<tenant domain>`.  Olá `<tenant domain>` uma saudação é verificada Olá inicias ou Locatário de domínios no hello `<...>.onmicrosoft.com` domínio. Esse tipo de conta é uma conta corporativa ou de estudante.

Em um locatário Azure AD B2C, a maioria dos aplicativos deseja Olá usuário toosign em qualquer endereço de email arbitrário (por exemplo, joe@comcast.net, bob@gmail.com, sarah@contoso.com, ou jim@live.com). Esse tipo de conta é uma conta local.  Também há suporte para nomes de usuário arbitrários como contas locais (por exemplo, joe, bob, sarah ou jim). Você pode escolher um destes dois tipos de conta local, configurando o Azure AD B2C na Olá portal do Azure.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>A quais provedores de identidade social você oferece suporte? Quais fazer você planejar toosupport em Olá futuras?
Atualmente, há suporte para Facebook, Google+, LinkedIn, Amazon, Twitter (versão prévia), WeChat (versão prévia), Weibo (versão prévia) e QQ (versão prévia). Vamos adicionar suporte para outros provedores de identidade social populares com base na demanda do cliente.

O Azure AD B2C também adicionou suporte para [políticas personalizadas](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Essas [políticas personalizadas](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) permitem que um desenvolvedor toocreate sua própria política que com qualquer provedor de identidade que oferece suporte a [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) ou SAML. 

Comece a usar políticas personalizadas verificando nosso [pacote de políticas personalizadas para iniciantes](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Posso configurar escopos toogather obter mais informações sobre os consumidores de vários provedores de identidade de redes sociais?
Não, mas esse recurso está em nosso roteiro. escopos de padrão de saudação usados para nosso conjunto com suporte dos provedores de identidade de redes sociais são:

* Facebook: email
* Google +: email
* Conta da Microsoft: perfil de email openid
* Amazon: perfil
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Meu aplicativo tem toobe executado no Azure para que ele funciona com o Azure AD B2C?
Não, você pode hospedar seu aplicativo em qualquer lugar (na nuvem hello ou local). Tudo o que precisa toointeract com o Azure AD B2C é Olá toosend de capacidade e receber solicitações HTTP em pontos de extremidade publicamente acessíveis.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Tenho vários locatários do Azure AD B2C. Como posso gerenciá-los em Olá portal do Azure?
Antes de abrir 'Do Azure AD B2C' no menu do lado esquerdo Olá Olá portal do Azure, você deve alternar no diretório Olá deseja toomanage.  Alternar pastas clicando em sua identidade no superior de saudação à direita da saudação portal do Azure e escolha um diretório na Olá suspensa que aparece.  Para um passo a passo com imagens, consulte [navegue tooAzure AD B2C configurações](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Como personalizar a emails de verificação (Olá conteúdo e hello "de:" campo) enviadas pelo Azure AD B2C?
Você pode usar o hello [marca do recurso da empresa](../active-directory/active-directory-add-company-branding.md) toocustomize conteúdo de saudação de emails de verificação. Especificamente, esses dois elementos de email Olá podem ser personalizados:

* **Logotipo de faixa**: mostrado no hello inferior direito.
* **Cor do plano de fundo**: mostrado na parte superior da saudação.

    ![Captura de tela de um email de verificação personalizado](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

assinatura de email Olá contém nome de saudação B2C locatário que você forneceu ao criar locatário Olá B2C. Você pode alterar o nome de saudação usando estas instruções:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) como Olá administrador da assinatura.
1. Navegue tooyour B2C locatário.
1. Clique em Olá **configurar** guia.
1. Saudação de alteração **nome** campo em Olá **propriedades do diretório** seção.
1. Clique em **salvar** final Olá Olá página.

Atualmente não há nenhum Olá toochange de maneira "de:" campo email hello. Vote em [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) você estiver interessado em Personalizar o corpo de saudação do email de verificação de saudação.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Como migrar Meus nomes de usuário existentes, senhas e perfis de tooAzure meu banco de dados AD B2C?
Você pode usar o hello Azure AD Graph API toowrite sua ferramenta de migração. Consulte Olá [exemplo de API do Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) para obter detalhes.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Qual é a política de senha usada para contas locais no AD B2C do Azure?
Olá política de senha do Azure AD B2C para contas locais baseia-se na política de saudação do AD do Azure. Azure AD B2C da inscrição, inscreva-se ou entrar e senha redefinir políticas usa hello "forte" senha forte e não expirarem senhas. Saudação de leitura [política de senha do AD do Azure](https://msdn.microsoft.com/library/azure/jj943764.aspx) para obter mais detalhes.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>É possível usar o Azure AD Connect toomigrate identidades que são armazenadas em minha tooAzure do Active Directory local AD B2C?
Não, o AD do Azure Connect não é projetado toowork com o Azure AD B2C. Considere o uso de saudação [API do Graph](active-directory-b2c-devquickstarts-graph-dotnet.md) para migração do usuário.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Meu aplicativo pode abrir as páginas do Azure AD B2C em um iFrame?
Não, por motivos de segurança, as páginas do Azure AD B2C não podem ser abertas em um iFrame.  Nosso serviço se comunica com hello navegador tooprohibit iFrames.  Olá comunidade de segurança em geral e Olá especificação OAUTH2, recomendamos usar iFrames para experiências de identidade devido toohello risco de jacking clique em.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>O AD B2C do Azure funciona com sistemas CRM, como o Microsoft Dynamics?
A integração com o Portal do Microsoft Dynamics 365 está disponível.  Consulte [toouse de configurar o Dynamics 365 Portal do Azure AD B2C para autenticação](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>O AD B2C do Azure funciona com o SharePoint local 2016 ou anterior?
B2C do AD do Azure não se destina a cenário Olá do SharePoint externo de compartilhamento do parceiro. consulte [do Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) em vez disso.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Devo usar Azure AD B2C ou identidades externas do B2B toomanage?
Leia este artigo sobre [identidades externas](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn mais sobre como aplicar Olá apropriado recursos tooyour cenários de identidade externa.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Quais recursos de relatórios e de auditoria são oferecidos pelo AD B2C do Azure? São que eles Olá mesmo como o Azure AD Premium?
Não, o Azure AD B2C suporte Olá mesmo conjunto de relatórios como o Azure AD Premium. No entanto, há muitos aspectos em comum:

* Olá entrar relatórios fornecem um registro de cada entrada com detalhes reduzidas.
* Relatórios de auditoria estão disponíveis no hello portal do Azure, no Active Directory do Azure > logs de auditoria da atividade > escolha B2C e aplicar filtros conforme desejado. A atividade de administração e a atividade do aplicativo são abordadas. 
* Um relatório de uso, abrangendo o número de usuários, o número de logons e o volume de MFA está disponível em [API de relatório de uso](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Posso localizar Olá da interface do usuário de páginas servidas por B2C do Azure AD? Quais são os idiomas com suporte?
Sim!  Leia sobre a [personalização de linguagem](active-directory-b2c-reference-language-customization.md), que está em visualização pública.  Podemos fornecer traduções para 36 idiomas, e você pode substituir qualquer cadeia de caracteres toosuit suas necessidades.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Posso usar minhas próprias URLs em minhas páginas de inscrição e de entrada atendidas pelo AD B2C do Azure? Por exemplo, pode alterar URL de saudação do login.microsoftonline.com toologin.contoso.com?
Não atualmente. Esse recurso está em nosso roteiro. Verificar seu domínio no hello **domínios** guia Olá portal clássico do Azure não atingir essa meta.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Como excluir o meu locatário do Azure AD B2C?
Siga estas etapas toodelete seu locatário do Azure AD B2C:

1. Siga estas etapas muito[navegue tooAzure AD B2C configurações](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.
1. Navegue toohello **aplicativos**, **provedores de identidade**, e **todas as políticas** e exclua todas as entradas de saudação em cada um deles.
1. Entrar agora toohello [portal clássico do Azure](https://manage.windowsazure.com/) como Olá administrador da assinatura. (Use Olá mesmo trabalho ou conta escolar ou Olá a mesma conta da Microsoft que você usou toosign para Azure).
1. Navegue de extensão do Active Directory toohello Olá esquerda e clique em seu locatário B2C.
1. Clique em Olá **usuários** guia.
1. Selecione cada usuário em vez (exclusão Olá administrador da assinatura do usuário atualmente está conectado como). Clique em **excluir** na parte inferior da saudação da página hello e clique em **Sim** quando solicitado.
1. Clique em Olá **aplicativos** guia.
1. Selecione **aplicativos que minha empresa possui** em Olá **Mostrar** campo da lista suspensa e clique em Olá marca de seleção.
1. Um aplicativo chamado **b2c-extensions-app**. Clique em **excluir** na parte inferior da saudação da página hello e clique em **Sim** quando solicitado.
1. Navegue extensão do Active Directory toohello novamente e selecione seu locatário B2C.
1. Clique em **excluir** final Olá Olá página. processo de saudação toocomplete, siga as instruções de saudação na tela hello.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Posso obter o AD B2C do Azure como parte do Enterprise Mobility Suite?
Não, o AD B2C do Azure é um serviço pré-pago do Azure e não faz parte do Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Como faço para relatar problemas com o AD B2C do Azure?
Veja [Solicitações de suporte a arquivos para o Azure Active Directory B2C](active-directory-b2c-support.md).
