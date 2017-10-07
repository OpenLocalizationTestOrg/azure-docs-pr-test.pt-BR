---
title: aaaConfigure SSO do AD do Azure para aplicativos | Microsoft Docs
description: "Saiba como o serviço de tooself se conectar a aplicativos tooAzure do Active Directory usando SAML e SSO baseado em senha"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Configurando um único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure Olá
Este artigo é sobre um recurso que permite que os administradores tooconfigure único logon tooapplications não está presente na Galeria de aplicativo do Active Directory do Azure Olá *sem escrever código*. Este recurso foi lançado na visualização técnica de 18 de novembro de 2015 e foi incluído no [Azure Active Directory Premium](active-directory-editions.md). Se você está procurando em vez disso, diretrizes para desenvolvedores sobre como toointegrate a aplicativos personalizados com o Azure AD por meio de código, consulte [cenários de autenticação do AD do Azure](active-directory-authentication-scenarios.md).

Olá Galeria de aplicativos do Active Directory do Azure fornece uma lista de aplicativos que são conhecidos toosupport um formulário de logon único com o Active Directory do Azure, conforme descrito em [neste artigo](active-directory-appssoaccess-whatis.md). (Como IT especialista ou sistema integrador em sua organização) localizados aplicativo hello deseja tooconnect, você pode começar por instruções passo a passo do hello siga apresentadas em Olá logon único do portal tooenable gerenciamento do Azure.

Os clientes com licenças do [Active Directory Premium do Azure](active-directory-editions.md) também obtêm estes recursos adicionais:

* Integração de autoatendimento de qualquer aplicativo com suporte a provedores de identidade SAML 2.0 (iniciado por SP ou IdP)
* Integração de autoatendimento de qualquer aplicativo Web que tenha uma página de entrada baseada em HTML usando o [SSO baseado em senha](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Conexão de autoatendimento de aplicativos que usam o protocolo SCIM Olá para provisionamento do usuário ([descrito aqui](active-directory-scim-provisioning.md))
* Capacidade tooadd links tooany aplicativo hello [iniciador do aplicativo do Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou hello [painel de acesso do AD do Azure](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Isso pode incluir não apenas a aplicativos SaaS que você usa, mas ainda não foram toohello onboard Galeria de aplicativos do AD do Azure, mas aplicativos web de terceiros que sua organização tiver implantado tooservers que controlar, na nuvem de saudação ou local.

Esses recursos, também conhecidos como *modelos de integração de aplicativos*, fornecem pontos de conexão baseados em padrões para aplicativos que dão suporte à autenticação baseada em formulários, a SCIM ou a SAML e que incluem opções e configurações flexíveis para compatibilidade com um grande número de aplicativos. 

## <a name="adding-an-unlisted-application"></a>Adicionando um aplicativo não listado
tooconnect um aplicativo usando um modelo de integração do aplicativo, entre no portal de gerenciamento do Azure hello usando sua conta de administrador do Active Directory do Azure e procurar toohello **do Active Directory > [Directory] > aplicativos**seção, selecione **adicionar**e, em seguida, **adicionar um aplicativo da Galeria Olá**. 

![][1]

Na Galeria de aplicativo hello, você pode adicionar um aplicativo não listado usando Olá **personalizado** categoria esquerda hello, ou selecionando Olá **adicionar um aplicativo não listado** link que é mostrada na pesquisa de saudação resultados se seu aplicativo desejado não foi encontrado. Depois de inserir um nome para seu aplicativo, você pode configurar o comportamento e as opções de logon único hello. 

**Dica rápida**: como uma prática recomendada, use Olá pesquisa função toocheck toosee se o aplicativo hello já existe na Galeria de aplicativo hello. Se o aplicativo hello for encontrado e sua descrição menciona "logon único", em seguida, aplicativo hello já tem suporte para logon único federado. 

![][2]

Adicionar um aplicativo dessa maneira fornece um toohello experiência muito semelhante disponível para aplicativos pré-integrados. toostart, selecione **configurar logon único**. exibição da próxima tela Hello apresenta Olá após três opções para configurar o logon único, que são descritas nas seções a seguir de saudação.

![][3]

## <a name="azure-ad-single-sign-on"></a>Logon Único do AD do Azure
Selecione esta opção tooconfigure SAML autenticação para aplicativo hello. Isso requer que Olá suporte a aplicativos SAML 2.0 e você deve coletar informações sobre como toouse Olá recursos SAML do aplicativo hello antes de continuar. Depois de selecionar **próximo**, você será solicitado tooenter três URLs diferentes correspondente toohello pontos de extremidade SAML para o aplicativo hello. 

![][4]

Estes são:

* **URL de logon (iniciado por SP somente)** – onde o usuário Olá vai toothis toosign no aplicativo. Se o aplicativo hello estiver configurado tooperform serviço iniciado pelo provedor SSO, em seguida, quando um usuário navega toothis URL, provedor de serviços de saudação será Olá redirecionamento necessário tooAzure AD tooauthenticate e logon de usuário Olá no. Se esse campo é populado, o AD do Azure usará este aplicativo de saudação do URL toolaunch do Office 365 e hello painel de acesso do AD do Azure. Se esse campo é omitido, o AD do Azure executará em vez disso, o provedor de identidade-iniciado com logon quando Olá aplicativo é iniciado do Office 365, Olá painel de acesso do AD do Azure, ou de saudação do AD do Azure única URL de logon (copiable do guia do painel de saudação).
* **URL do emissor** -Olá URL do emissor deve identificar exclusivamente aplicativo hello para qual SSO está sendo configurado. Esse é o valor de saudação que o AD do Azure envia tooapplication back como Olá **público** parâmetro de token SAML hello e aplicativo hello é esperado toovalidate-lo. Esse valor também aparece como Olá **ID da entidade** em todos os metadados SAML fornecido pelo aplicativo hello. Verifique a documentação do aplicativo hello SAML para obter detalhes sobre o que é a ID da entidade ou valor de público é. Abaixo está um exemplo de como Olá URL público é exibido no aplicativo de toohello retornado de token de SAML hello:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **URL de resposta** -Olá URL de resposta é onde o aplicativo hello espera o token SAML tooreceive hello. Isso também é chamado tooas Olá **URL do serviço de consumidor de declaração (ACS)**. Consulte a documentação de SAML do aplicativo hello para obter detalhes sobre o que é sua URL de resposta de token de SAML ou URL do ACS.
  Depois que eles tiverem sido inseridos, clique em **próximo** tooproceed toohello próxima tela. Esta tela fornece informações sobre quais toobe necessidades configurada no hello aplicativo lado tooenable-tooaccept um token SAML do AD do Azure. 

![][5]

Os valores que são necessários variam de acordo com o aplicativo hello, por isso verifique a documentação de SAML do aplicativo hello para obter detalhes. Olá **logon** e **logout** service URL resolver toohello mesmo ponto de extremidade, que é o ponto de extremidade de tratamento de solicitação SAML Olá para sua instância do AD do Azure. Olá URL do emissor é o valor de saudação que aparece como hello "Emissor" dentro de saudação aplicativo de toohello emitidos token SAML. 

Depois que seu aplicativo tiver sido configurado, clique em **próximo** botão e, em seguida, Olá **concluir** caixa de diálogo tooclose hello. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Atribuir usuários e aplicativos de SAML tooyour grupos
Depois que seu aplicativo tiver sido configurado toouse AD do Azure como um provedor de identidade baseado no SAML, é tootest quase pronto. Como um controle de segurança do AD do Azure não emitirá um token que permite que eles toosign em aplicativo hello, a menos que receberam acesso usando o Azure AD. Os usuários podem ter acesso diretamente ou através de um grupo do qual sejam membros. 

tooassign um aplicativo de tooyour usuário ou grupo, clique em Olá **atribuir usuários** botão. Selecione o usuário hello ou grupo que você deseja tooassign e, em seguida, selecione Olá **atribuir** botão. 

![][6]

Atribuir um usuário permitirá tooissue do AD do Azure um token de usuário hello, bem como fazendo com que um bloco para este aplicativo tooappear no painel de acesso do usuário hello. Um bloco de aplicativo também será exibida no iniciador do aplicativo hello Office 365 se Olá usuário está usando o Office 365. 

Você pode carregar um logotipo em bloco para o aplicativo hello usando Olá **carregar logotipo** botão Olá **configurar** guia para o aplicativo hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Personalizando Olá declarações emitidas no token SAML Olá
Quando um usuário se autentica toohello aplicativo, o AD do Azure emitirá um aplicativo de toohello token SAML que contém informações (ou declarações) sobre o usuário Olá que identifica exclusivamente. Por padrão, isso inclui nome de usuário, endereço de email, nome e sobrenome do usuário hello. 

Você pode exibir ou editar declarações Olá enviadas em Olá aplicativo toohello token SAML Olá **atributos** guia. 

![][7]

Há duas razões possíveis por que talvez seja necessário tooedit declarações de saudação emitidas no token SAML Olá: •hello aplicativo foi escrito toorequire outro conjunto de declaração URIs ou valores •Your ter sido implantado em uma forma que requer a saudação de declaração Declaração NameIdentifier toobe algo diferente de nome de usuário da saudação (conhecidos como UPN) armazenados no Active Directory do Azure. 

Para obter informações sobre como tooadd e editar solicitações para esses cenários, confira este [artigo sobre a personalização de declarações](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Teste o aplicativo de SAML hello
Depois que as URLs de SAML hello e certificado foram configuradas no AD do Azure e no aplicativo hello, usuários ou grupos foram atribuídos toohello aplicativo no Azure, Olá declarações foram examinadas e editadas se necessário e usuário Olá é toosign pronto em Olá aplicativo. 

tootest, simplesmente entram no hello painel de acesso do AD do Azure em https://myapps.microsoft.com usando uma conta de usuário atribuída toohello aplicativo e, em seguida, clique no bloco de saudação para Olá aplicativo tookick fora do processo de logon único hello. Como alternativa, você pode navegar diretamente toohello URL de logon para o aplicativo hello e entrar a partir daí. 

Para obter dicas de depuração, consulte este [artigo sobre como toodebug baseado no SAML único logon tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Logon único com senha
Selecione esta opção tooconfigure [com base em senha de logon único](active-directory-appssoaccess-whatis.md) para um aplicativo web que possui uma página de entrada HTML. SSO baseado em senha, também senha chamado tooas compartimentalização, permite que você toomanage acesso e senhas tooweb aplicativos de usuário que não oferecem suporte à Federação de identidade. Também é útil para cenários onde vários usuários necessário tooshare uma única conta, como contas de aplicativo de mídia social tooyour da organização. 

Depois de selecionar **próximo**, será tooenter solicitadas Olá URL baseado na web entrar página do aplicativo hello. Observe que isso deve ser página Olá que inclua campos de entrada de usuário e senha hello. Uma vez inserida, o Azure AD inicia uma processo tooparse Olá página de entrada para uma entrada de nome de usuário e uma senha. Se o processo de saudação não for bem-sucedida, ela orientará você durante um processo alternativo de instalar uma extensão de navegador (requer o Internet Explorer, o Chrome ou Firefox) que permitirá que você toomanually campos de saudação de captura.

Depois que a página de entrada hello for capturada, os usuários e grupos podem ser atribuídos e políticas de credencial podem ser definidas como regular [aplicativos SSO de senha](active-directory-appssoaccess-whatis.md).

Observação: Você pode carregar um logotipo em bloco para o aplicativo hello usando Olá **carregar logotipo** botão Olá **configurar** guia para o aplicativo hello. 

## <a name="existing-single-sign-on"></a>Logon único existente
Selecione esta opção tooadd portal do painel de acesso do AD do Azure ou Office 365 da organização um link tooan aplicativo tooyour. Você pode usar este tooadd links toocustom os aplicativos web que atualmente usam o Azure Active Directory Federation Services (ou outro serviço de federação) em vez do AD do Azure para autenticação. Ou, você pode adicionar páginas, links profundos toospecific do SharePoint ou outras páginas da web que você deseja que apenas tooappear em painéis de acesso do usuário. 

Depois de selecionar **próximo**, serão solicitadas tooenter URL Olá Olá toolink de aplicativo para. Depois de concluído, os usuários e grupos podem ser atribuídos toohello aplicativo, que faz com que o hello aplicativo tooappear em Olá [iniciador do aplicativo do Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou hello [painel de acesso do AD do Azure](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) para os usuários.

Observação: Você pode carregar um logotipo em bloco para o aplicativo hello usando Olá **carregar logotipo** botão Olá **configurar** guia para o aplicativo hello.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Como tooCustomize as declarações emitidas no hello Token SAML para aplicativos Pre-Integrated](active-directory-saml-claims-customization.md)
* [Solução de problemas de logon único baseado em SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
