---
title: "aaaCustomizing declarações emitidas no token SAML Olá para aplicativos pré-integrados no Active Directory do Azure | Microsoft Docs"
description: "Saiba como toocustomize Olá declarações emitidas no hello token SAML para aplicativos pré-integrados no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Personalizando declarações emitidas em Olá token SAML para aplicativos pré-integrados no Active Directory do Azure
Atualmente o Active Directory do Azure dá suporte a milhares de aplicativos pré-integrados em Olá Galeria de aplicativos do Azure AD, incluindo mais 360 que dão suporte a logon único usando o protocolo de saudação SAML 2.0. Quando um usuário se autentica tooan aplicativo por meio do AD do Azure usando SAML, o AD do Azure envia um aplicativo de token toohello (por meio de um HTTP POST). E, em seguida, o aplicativo hello valida e usa Olá toolog token Olá usuário em vez de solicitar um nome de usuário e senha. Esses tokens SAML contêm informações sobre o usuário Olá conhecido como "declarações".

Em linguagem de identificação, uma declaração de"" informações que declara um provedor de identidade sobre um usuário dentro do token Olá que emitem para esse usuário. Em [token SAML](http://en.wikipedia.org/wiki/SAML_2.0), esses dados geralmente contidos em Olá SAML atributo de instrução. Olá ID exclusiva do usuário é representado geralmente em hello, que também chamado de assunto SAML como identificador de nome.

Por padrão, o Active Directory do Azure emite um aplicativo de tooyour token SAML que contém uma declaração NameIdentifier, com um valor de saudação do usuário (conhecidos como UPN) no AD do Azure. Esse valor pode identificar exclusivamente o usuário hello. token SAML Olá também contém declarações adicionais que contém o endereço de email do usuário Olá, nome e sobrenome.

tooview ou editar Olá as declarações emitidas no hello aplicativo toohello token de SAML, aplicativo hello abrir no portal do Azure. Selecione Olá **exibir e editar todos os outros atributos de usuário** caixa de seleção no hello **atributos de usuário** seção de aplicativo hello.

![Seção Atributos de usuário][1]

Há dois motivos possíveis quais declarações de saudação tooedit emitidas no token SAML Olá pode ser necessário:
* aplicativo Hello gravou toorequire outro conjunto de declaração URIs ou valores de declaração.
* aplicativo Hello foi implantado em uma forma que requer toobe de declaração NameIdentifier Olá algo diferente de nome de usuário da saudação (conhecidos como UPN) armazenados no Active Directory do Azure.

Você pode editar qualquer um dos valores de declaração saudação padrão. Selecione a linha de declaração de saudação na tabela de atributos de token de SAML hello. Isso abre o hello **Editar atributo** seção e, em seguida, você pode editar a declaração de nome, valor e namespace associado Olá declaração.

![Editar Atributo de Usuário][2]

Você também pode remover declarações (que não sejam NameIdentifier) usando o menu de contexto hello, que abre clicando em Olá **...**  ícone.  Você também pode adicionar novas declarações usando Olá **Adicionar atributo** botão.

![Editar Atributo de Usuário][3]

## <a name="editing-hello-nameidentifier-claim"></a>Edição Olá declaração NameIdentifier
problema de saudação toosolve onde o aplicativo hello foi implantado usando um nome de usuário diferente, clique em Olá **identificador de usuário** suspensa no hello **atributos de usuário** seção. Essa ação apresenta uma caixa de diálogo com várias opções diferentes:

![Editar Atributo de Usuário][4]

No hello lista suspensa, selecione **user.mail** tooset Olá NameIdentifier declaração endereço de email do usuário de saudação toobe no diretório de saudação. Ou, selecione **user.onpremisessamaccountname** nome de conta do SAM do tooset toohello usuário sincronizado a partir do Azure AD local.

Você também pode usar o hello especial **ExtractMailPrefix()** sufixo do domínio Olá função tooremove de endereço de email Olá, nome de conta SAM ou Olá UPN. Isso extrai somente a primeira parte de saudação do usuário Olá nome que está sendo passado (por exemplo, "joe_smith" em vez de joe_smith@contoso.com).

![Editar Atributo de Usuário][5]

Agora também adicionamos Olá **JOIN ()** saudação do função toojoin verificar o domínio com valor de identificador de usuário hello. Quando você seleciona a função do hello JOIN () em Olá **identificador de usuário** primeiro selecione Olá identificador de usuário, como o nome da entidade usuário ou endereço de email e na Olá segunda lista suspensa, selecione o domínio verificado. Se você selecionar o endereço de email de saudação com domínio verificado hello, o AD do Azure extrai Olá username de saudação primeiro valor joe_smith de joe_smith@contoso.com e acrescenta com contoso.onmicrosoft.com. Consulte Olá exemplo a seguir:

![Editar Atributo de Usuário][6]

## <a name="adding-claims"></a>Adicionando declarações
Ao adicionar uma declaração, você pode especificar o nome do atributo hello (que não precisará toofollow um padrão URI de acordo com a especificação SAML Olá). Definir Olá valor tooany atributo de usuário que é armazenado no diretório de saudação.

![Adicionar Atributo de Usuário][7]

Por exemplo, você precisa toosend departamento Olá Olá usuário pertence tooin sua organização como uma declaração (por exemplo, vendas). Insira o nome da declaração Olá conforme o esperado pelo aplicativo hello e, em seguida, selecione **User. Department** como valor de saudação.

> [!NOTE]
> Se para um determinado usuário, não há nenhum valor armazenado para um atributo selecionado, essa declaração não está sendo emitida no token de saudação.

> [!TIP]
> Olá **user.onpremisesecurityidentifier** e **user.onpremisesamaccountname** somente têm suporte quando a sincronização de dados de usuário do local do Active Directory usando Olá [Azure Ferramenta de conexão do AD](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Declarações restritas

Há algumas declarações restritas no SAML. Se você adicionar essas declarações, então o Azure AD não as enviará. A seguir é Olá SAML restrito conjunto de declarações:

    | Tipo de declaração (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>Próximas etapas
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](../active-directory-apps-index.md)
* [Configurando um único logon tooapplications que não estão na Galeria de aplicativos do Active Directory do Azure Olá](../active-directory-saas-custom-apps.md)
* [Solução de problemas de logon único baseado em SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png