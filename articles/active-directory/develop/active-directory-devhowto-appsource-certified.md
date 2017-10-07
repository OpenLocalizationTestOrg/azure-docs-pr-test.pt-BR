---
title: aaaHow tooget AppSource certificado para o Active Directory do Azure | Microsoft Docs
description: Obter detalhes sobre como tooget seu aplicativo AppSource certificados para o Active Directory do Azure.
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Como tooget AppSource certificados para o Active Directory do Azure
[Microsoft AppSource](https://appsource.microsoft.com/) é um destino para toodiscover de usuários de negócios, tente e gerenciar aplicativos SaaS de linha de negócios (autônomo SaaS e o complemento tooexisting Microsoft SaaS produtos).

toolist um aplicativo SaaS em AppSource autônomo, seu aplicativo deve aceitar logon único de contas de trabalho de qualquer empresa ou organização que possui o Active Directory do Azure. processo de entrada Hello deve usar Olá [OpenID Connect](./active-directory-protocols-openid-connect-code.md) ou [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolos. A integração SAML não é aceita para certificação AppSource.

## <a name="guides-and-code-samples"></a>Guias e exemplos de código
Se você quiser toolearn sobre como toointegrate o aplicativo com o Azure Active Directory usando Open ID se conectar, siga nosso guias e Olá amostras de código [guia do desenvolvedor do Active Directory do Azure](./active-directory-developers-guide.md#get-started "começar com O AD do Azure para desenvolvedores").

## <a name="multi-tenant-applications"></a>Aplicativos multilocatários

Um aplicativo que aceita entradas de usuários de qualquer empresa ou organização que tenha o Azure Active Directory sem a necessidade de uma instância, configuração ou implantação separada é conhecido como *aplicativo multilocatário*. AppSource recomenda a aplicativos implementar Olá multilocação tooenable *único clique* livre experiência de avaliação.

Em ordem tooenable multilocação em seu aplicativo:
- Definir `Multi-Tenanted` propriedade muito`Yes` nas informações do registro do aplicativo hello [Portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (por padrão, os aplicativos criados no hello Portal do Azure são configurados como *únicolocatário*)
- Atualizar seu toohello de solicitações do código toosend '`common`' ponto de extremidade (atualizar o ponto de extremidade de saudação do *https://login.microsoftonline.com/ {yourtenant}* muito*https://login.microsoftonline.com/common*)
- Para algumas plataformas, como o ASP.NET, você precisa também tooupdate tooaccept seu código vários emissores

Para obter mais informações sobre multilocação, consulte: [como toosign em qualquer usuário do Azure AD (Active Directory) usando Olá padrão de aplicativo multilocatário](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Aplicativos de locatário único
Aplicativos que só aceitam entradas de usuários de uma instância definida do Azure Active Directory são conhecidos como *aplicativo de locatário único*. Os usuários externos (incluindo as contas de trabalho ou escola de outras organizações ou conta pessoal) podem entrar no aplicativo de único locatário tooa depois de adicionar cada usuário como *conta convidado* instância toohello Active Directory do Azure aplicativo Hello está registrado. Você pode adicionar usuários como tooan de contas de convidado do Azure Active Directory por meio de saudação [ *colaboração B2B do Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - e isso pode ser feito [programaticamente](../active-directory-b2b-code-samples.md). Quando você adiciona um usuário como conta de convidado tooan Active Directory do Azure, um email de convite é enviado toohello usuário, que tem o convite de saudação tooaccept clicando no link Olá no email de convite de saudação. Convites enviados tooan adicional do usuário em uma organização convidar que também seja um membro da organização do parceiro de saudação são tooaccept necessária não toosign um convite no.

Aplicativos de locatário único podem habilitar Olá *contato Me* experiência, mas se você quiser tooenable Olá clique simples / livre experiência de avaliação que recomenda AppSource, habilitar a multilocação em seu aplicativo em vez disso.


## <a name="appsource-trial-experiences"></a>Experiências de avaliação do AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Avaliação gratuita (experiência de avaliação orientada pelo cliente) 
Olá *avaliação orientada pelo cliente* é experiência Olá AppSource recomenda que oferece um aplicativo de tooyour acesso único clique. Abaixo, uma ilustração de como essa experiência se parece:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>O usuário localiza o aplicativo no Site do AppSource</li><li>Seleciona a opção “Avaliação gratuita”</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource redireciona o usuário tooa URL no seu site da web</li><li>O site inicia Olá <i>single-sign-on</i> processar automaticamente (no carregamento da página)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Usuário é redirecionado tooMicrosoft entrar página</li><li>O usuário fornece credenciais toosign em</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>O usuário dá consentimento ao seu aplicativo</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Entrar for concluída e o usuário é redirecionado tooyour back web site</li><li>Usuário começa a avaliação gratuita Olá</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Entre em Contato Comigo (experiência de avaliação orientada pelo parceiro)
Olá *experiência de avaliação do parceiro* pode ser usado quando um manual ou uma operação de longo prazo precisa de usuário de saudação do toohappen tooprovision / da empresa: por exemplo, seu aplicativo precisa de máquinas virtuais de tooprovision, instâncias de banco de dados, ou operações que levam muito tempo toocomplete. Nesse caso, após o usuário selecionará Olá *'Solicitação avaliação'* botão e preenche um formulário, AppSource envia Olá informações de contato do usuário. Ao receber essas informações, em seguida, provisionar ambiente hello e enviar Olá instruções toohello usuário como tooaccess Olá experiência de avaliação:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>O usuário localiza o aplicativo no Site do AppSource</li><li>Seleciona a opção “Entrar em contato comigo”</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Preenche um formulário com as informações de contato</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Você recebe as informações do usuário</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Configure o ambiente</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Entre em contato com usuário com as informações da avaliação</td>
        </tr>
        </table><br/><br/>
        <ul><li>Você recebe informações do usuário e configura a instância de avaliação</li><li>Enviar Olá hiperlink tooaccess sua toohello de usuário do aplicativo</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Usuário acessar seu aplicativo e o processo de logon único do hello concluída</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>O usuário dá consentimento ao seu aplicativo</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Entrar for concluída e o usuário é redirecionado tooyour back web site</li><li>Usuário começa a avaliação gratuita Olá</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Mais informações
Para obter mais informações sobre a experiência de avaliação do hello AppSource, consulte [este vídeo](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Próximas etapas

- Para saber mais sobre como criar aplicativos que dão suporte a logons do Azure Active Directory, confira [Cenários de autenticação do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 

- Para obter informações sobre como toolist seu aplicativo SaaS no AppSource, vá consulte [AppSource informações do parceiro](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Obtenha suporte
Integração do Active Directory do Azure, usamos [estouro de pilha](http://stackoverflow.com/questions/tagged/azure-active-directory) com suporte de tooprovide Olá da comunidade. 

É altamente recomendável fazer suas perguntas sobre estouro de pilha primeiro e procurar existente toosee de problemas, se alguém fez sua pergunta antes. Marque suas perguntas ou comentários com `[azure-active-directory]`.

Use Olá comentários de tooprovide seção comentários a seguir e ajudar a refinar e formatar o nosso conteúdo.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->