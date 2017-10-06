---
title: "aaaError na página do aplicativo depois de entrar no | Microsoft Docs"
description: "Como tooresolve problemas com o Azure AD de conexão ao próprio aplicativo hello emite um erro"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Erro em uma página de aplicativo após a entrada

Nesse cenário, AD do Azure tem assinado usuário hello, mas aplicativo hello está exibindo um erro não permitindo Olá usuário toosuccessfully término hello entrada no fluxo. Nesse cenário, o aplicativo hello não está aceitando problema de resposta de saudação pelo AD do Azure.

Há alguns possíveis motivos por que o aplicativo hello não aceitou resposta de saudação do AD do Azure. Se Olá erro no aplicativo hello tooknow limpar suficiente o que está faltando na resposta Olá, então:

-   Se aplicativo hello Galeria de saudação do AD do Azure, verifique se você tiver seguido todas as etapas de saudação artigo Olá [como toodebug baseado no SAML único logon tooapplications no Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Usar uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) toocapture SAML de solicitação, resposta SAML e o token SAML.

-   Compartilhe resposta SAML Olá com tooknow de fornecedor do aplicativo hello, o que está faltando.

## <a name="missing-attributes-in-hello-saml-response"></a>Atributos ausentes em Olá resposta SAML

tooadd um atributo em toobe de configuração do AD do Azure Olá enviado em resposta a saudação do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Clique em **exibir e editar os atributos de todos os outros usuários sob** Olá **atributos de usuário** Olá de tooedit seção atributos toobe enviado toohello aplicativo no token SAML hello quando o usuário entrar.

   um atributo de tooadd:

   * clique em **Adicionar atributo**. Digite hello **nome** e Olá Olá selecione **valor** na lista suspensa de saudação.

   * Clique em **Salvar.** Você verá um novo atributo Olá na tabela de saudação.

9.  Salve a configuração de saudação.

Próxima vez que usuário Olá entra no aplicativo toohello, o AD do Azure enviar novo atributo de saudação em Olá resposta SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>aplicativo Hello espera um valor de identificador de usuário diferente ou um formato

aplicativo de entrada toohello Hello está falhando porque Olá resposta SAML tem atributos como funções ou porque o aplicativo hello está esperando um formato diferente para o atributo EntityID de saudação.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Adicione um atributo na configuração de aplicativo do AD do Azure hello:

Olá toochange valor de identificador de usuário, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Em Olá **atributos de usuário**, selecione Olá identificador exclusivo para os usuários no hello **identificador de usuário** lista suspensa.

## <a name="change-entityid-user-identifier-format"></a>Alterar o formato EntityID (Identificador de Usuário)

Se o aplicativo hello espera outro formato para o atributo EntityID de saudação. Em seguida, você não será tooselect capaz de formato de ID (identificador de usuário) de saudação AD do Azure envia toohello aplicativo em resposta Olá após a autenticação do usuário.

Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) em Olá seção NameIDPolicy.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>aplicativo Hello espera um método de assinatura diferente para Olá resposta SAML

toochange quais partes do token SAML Olá são assinados digitalmente pelo Active Directory do Azure. Siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Clique em **Mostrar configurações de assinatura de certificado avançadas** em Olá **o certificado de autenticação SAML** seção.

9.  Selecione Olá apropriado **opção assinatura** esperado pelo aplicativo hello:

  * Assinar resposta SAML

  * Assinar resposta SAML e declaração

  * Assinar declaração SAML

Próxima vez que usuário Olá entra no aplicativo toohello, logon do AD do Azure Olá parte da resposta SAML Olá selecionada.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>aplicativo Hello espera Olá assinatura toobe algoritmo SHA-1

Por padrão, o AD do Azure assina token SAML hello usando Olá algoritmo de segurança mais. Não é recomendável alterar o algoritmo de entrada hello tooSHA-1, a menos que exigido pelo aplicativo hello.

toochange Olá algoritmo de assinatura, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Clique em **Mostrar configurações de assinatura de certificado avançadas** em Olá **o certificado de autenticação SAML** seção.

9.  Selecione SHA-1, em Olá **algoritmo de assinatura**.

Próxima vez Olá usuário se autentica no aplicativo toohello, logon do AD do Azure Olá token SAML usando o algoritmo SHA-1.

## <a name="next-steps"></a>Próximas etapas
[Como toodebug baseado no SAML único logon tooapplications no Active Directory do Azure](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
