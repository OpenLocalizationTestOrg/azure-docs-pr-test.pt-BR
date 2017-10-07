---
title: "aaaSingle logon no gerenciamento de aplicativos de empresa no Active Directory do Azure de saudação | Microsoft Docs"
description: "Saiba como toomanage de logon único para aplicativos da empresa usando Olá Active Directory do Azure"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Gerenciar o logon único para aplicativos empresariais
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-enterprise-apps-manage-sso.md)
> * [Portal clássico do Azure](active-directory-sso-integrate-saas-apps.md)
> 

Este artigo descreve como Olá toouse [portal do Azure](https://portal.azure.com) toomanage configurações de logon único para aplicativos corporativos. Aplicativos empresariais são aplicativos que são implantados e usados dentro da sua organização. Este artigo se aplica especialmente tooapps que foram adicionados do hello [Galeria de aplicativos do Active Directory do Azure](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Localizando seus aplicativos no portal de saudação
Todos os aplicativos que são configurados para logon único podem ser exibidos e gerenciados no hello portal do Azure. aplicativos Olá podem ser encontrados no hello **mais serviços** &gt; **aplicativos empresariais** seção do portal de saudação. 

![Folha de Aplicativos Empresariais][1]

Selecione **todos os aplicativos** tooview uma lista de todos os aplicativos que foram configuradas. Selecionar um aplicativo carrega a folha de recursos Olá para esse aplicativo, onde os relatórios podem ser exibidos para esse aplicativo e uma variedade de configurações que pode ser gerenciada.

toomanage único-configurações de logon, selecione **o logon único**.

![Folha de recursos do aplicativo][2]

## <a name="single-sign-on-modes"></a>Modos de logon único
Olá **o logon único** folha começa com um **modo** menu, o que permite Olá toobe de modo de logon único configurado. Olá as opções disponíveis incluem:

* **Baseado no SAML logon** -esta opção estará disponível se o aplicativo hello oferece suporte completo federado logon único com o Azure Active Directory usando o protocolo de saudação SAML 2.0.
* **Logon baseado em senha em** -essa opção está disponível se o Azure AD dá suporte ao preenchimento de formulário de senha para este aplicativo.
* **Vinculado sinal em** -anteriormente conhecido como "Existente single sign-on", essa opção permite que os administradores tooplace um aplicativo de toothis link no iniciador do aplicativo de painel de acesso do AD do Azure ou Office 365 do seu usuário.

Para obter mais informações sobre esses modos, confira [Como o logon único funciona com o Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Logon único baseado em SAML
Olá **baseado no SAML logon** opção exibe um blade que é dividido em quatro seções:

### <a name="domains-and-urls"></a>Domínios e URLs
Isso é onde todos os detalhes sobre o domínio do aplicativo hello e as URLs são adicionados tooyour diretório AD do Azure. Todas as entradas necessárias toomake aplicativo de trabalho de logon único são exibidas diretamente na tela hello, enquanto todas as entradas opcionais podem ser exibidas selecionando Olá **Mostrar configurações de URL avançadas** caixa de seleção. lista completa de saudação de entradas com suporte incluem:

* **URL de logon** – onde o usuário Olá vai toothis toosign no aplicativo. Se aplicativo hello for configurado tooperform serviço único iniciado pelo provedor de logon, e em seguida, quando um usuário navega toothis URL, o provedor de serviços Olá Olá necessário sinal e redirecionamento tooAzure AD tooauthenticate Olá usuário. Se esse campo é populado, o AD do Azure usará este aplicativo de saudação do URL toolaunch do Office 365 e hello painel de acesso do AD do Azure. Se esse campo for omitido, o AD do Azure executa em vez disso, o provedor de identidade-iniciado com logon quando Olá aplicativo é iniciado do Office 365, Olá painel de acesso do AD do Azure, ou de saudação do AD do Azure única URL de logon.
* **Identificador** -esse URI deve identificar exclusivamente aplicativo hello para qual SSO está sendo configurado. Isso é o valor de saudação que AD do Azure envia tooapplication back como Olá parâmetro de público-alvo do token SAML hello e aplicativo hello é esperado toovalidate-lo. Esse valor também aparece como Olá ID de entidade em todos os metadados SAML fornecido pelo aplicativo hello.
* **URL de resposta** -Olá URL de resposta é onde o aplicativo hello espera o token SAML tooreceive hello. Isso também é chamado tooas Olá asserção consumidor Service (ACS) URL. Depois que eles tiverem sido inseridos, clique em Avançar tooproceed toohello próxima tela. Esta tela fornece informações sobre quais toobe necessidades configurada no hello aplicativo lado tooenable-tooaccept um token SAML do AD do Azure.
* **Estado de retransmissão** -estado de retransmissão Olá é um parâmetro opcional que pode ajudar a informar o aplicativo hello onde tooredirect Olá usuário após a autenticação é concluída. Normalmente o valor de saudação é uma URL válida no aplicativo hello, no entanto, alguns aplicativos usam este campo diferente (consulte o logon único do aplicativo hello documentação para obter detalhes). estado de retransmissão Olá capacidade tooset Olá é um novo recurso que é exclusivo toohello novo portal do Azure.

### <a name="user-attributes"></a>Atributos de usuário
Isso é onde administradores podem exibir e editar atributos de saudação que são enviados no token SAML Olá que o AD do Azure emite toohello aplicativo cada vez que os usuários entrar.

Olá, somente o atributo editável com suporte é hello **identificador de usuário** atributo. valor Olá desse atributo é o campo de saudação no AD do Azure que identifica exclusivamente cada usuário em um aplicativo hello. Por exemplo, se Olá aplicativo foi implantado usando hello "endereço de Email" como nome de usuário hello e identificador exclusivo, em seguida, Olá valor deve ser definido toohello "user.mail" campo no AD do Azure.

### <a name="saml-signing-certificate"></a>Certificado de assinatura de SAML
Esta seção mostra detalhes de saudação do certificado de saudação do AD do Azure usa tokens SAML de saudação toosign emitidos toohello aplicativo que autentica cada usuário de saudação do tempo. Ele permite que propriedades Olá Olá atual certificado toobe inspecionado, incluindo a data de expiração de saudação.

### <a name="application-configuration"></a>Configuração de aplicativo
seção final Olá fornece documentação hello e/ou controles necessários tooconfigure Olá próprio aplicativo toouse Active Directory do Azure como um provedor de identidade.

Olá **configurar o aplicativo** menu suspenso fornece novas instruções concisas, incorporadas para configurar o aplicativo hello. Este é outro novo recurso exclusivo toohello novo portal do Azure.

> [!NOTE]
> Para obter um exemplo completo de documentação do embedded, consulte aplicativo do Salesforce.com hello. A documentação de aplicativos adicionais está sendo adicionada continuamente.
> 
> 

![Documentos internos][3]

## <a name="password-based-sign-on"></a>Logon baseado em senha em
Se houver suporte para o aplicativo hello, selecionando Olá modo SSO baseado em senha e selecionando **salvar** instantaneamente configura toodo SSO baseado em senha. Para obter mais informações sobre a implantação de SSO baseada em senha, confira [Como o logon único funciona com o Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Logon baseado em senha em][4]

## <a name="linked-sign-on"></a>Logon vinculado
Se houver suporte para o aplicativo hello, selecionar modo de SSO Olá vinculado permite tooenter Olá URL que você deseja Olá painel de acesso do AD do Azure ou Office 365 tooredirect toowhen os usuários clicam neste aplicativo. Para obter mais informações sobre o SSO vinculado (anteriormente conhecido como "SSO existente"), confira [Como o logon único funciona com o Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Logon vinculado][5]

##<a name="feedback"></a>Comentários

Esperamos que você deseja usar Olá melhor experiência de AD do Azure. Mantenha comentários Olá vindo! Poste seus comentários e ideias para a melhoria nos Olá **Portal de administração** seção do nosso [Fórum de comentários](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Nos estiver contentes sobre a criação de novo e interessante diariamente e usar tooshape sua orientação e definir o que devemos construir a seguir.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
