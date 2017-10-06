---
title: "logon único aaaProblems entrar no aplicativo de galeria tooa configurado para federado | Microsoft Docs"
description: "Diretrizes para erros específicos de saudação ao entrar em um aplicativo que você configurou para baseado no SAML federado logon único com o Azure AD"
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
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a>Problemas para entrar no aplicativo de galeria tooa configurado para logon único federado

tootroubleshoot seu problema, você precisa de configuração de aplicativo hello tooverify no AD do Azure como segue:

-   Você tiver seguido todas as etapas de configuração de saudação para Olá aplicativo da Galeria de AD do Azure.

-   Olá identificador e URL de resposta configurado no AAD correspondem a elas valores esperados no aplicativo hello

-   Você atribuiu usuários toohello aplicativo

## <a name="application-not-found-in-directory"></a>Aplicativo não encontrado no diretório

*Erro AADSTS70001: O aplicativo com identificador 'https://contoso.com' não foi encontrado no diretório Olá*.

**Possível causa**

atributo de emissor Olá envia de saudação aplicativo tooAzure que AD na solicitação SAML Olá não corresponde o valor de identificador de saudação configurado no aplicativo de saudação do AD do Azure.

**Resolução**

Verifique se esse atributo de emissor Olá na solicitação SAML Olá correspondentes Olá valor de identificador configurado no AD do Azure:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Vá muito**domínio e URLs** seção. Verifique se o valor no hello identificador de caixa de texto é compatível com o valor Olá Olá identificador valor exibido no erro Olá Olá.

Depois que você atualizou o valor do identificador Olá no AD do Azure e sua correspondência Olá valor envia por aplicativo hello na solicitação SAML hello, você deve ser capaz de toosign no aplicativo toohello.

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a>endereço de resposta de saudação não coincide com os endereços de resposta de saudação configurados para o aplicativo hello.

*Erro AADSTS50011: o endereço de resposta de saudação 'https://contoso.com' não coincide com os endereços de resposta de saudação configurados para o aplicativo hello*

**Possível causa**

Olá AssertionConsumerServiceURL valor na solicitação SAML Olá não coincide com o padrão configurado no AD do Azure ou valor de URL de resposta de saudação. Olá AssertionConsumerServiceURL valor na solicitação SAML Olá é a URL de saudação consulte erro hello.

**Resolução**

Verifique se esse valor de AssertionConsumerServiceURL Olá na solicitação SAML Olá sua correspondência Olá valor de URL de resposta configurado no AD do Azure.

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Vá muito**domínio e URLs** seção. Verifique ou atualize o valor de saudação na caixa de texto toomatch Olá AssertionConsumerServiceURL valor na solicitação SAML de saudação do hello URL de resposta.  
    * Se você não vir o texto da URL de resposta de saudação, selecione Olá **Mostrar configurações de URL avançadas** caixa de seleção.

Depois que você atualizou o valor de URL de resposta Olá no AD do Azure e tem correspondência do valor de saudação envia por aplicativo hello em Olá solicitação SAML, você deve ser capaz de toosign no aplicativo toohello.

## <a name="user-not-assigned-a-role"></a>Usuário não atribuído a uma função

*Erro AADSTS50105: Olá usuário conectado 'brian@contoso.com' não está atribuído a função tooa para o aplicativo hello*.

**Possível causa**

saudação de usuário não recebeu acesso toohello aplicativo no AD do Azure.

**Resolução**

tooassign um ou mais aplicativos de tooan usuários diretamente, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja tooassign uma lista de saudação do usuário toofrom.

7.  Depois que o aplicativo hello carrega, clique em **usuários e grupos** no menu de navegação à esquerda do aplicativo hello.

8.  Clique Olá **adicionar** botão na parte superior Olá **usuários e grupos** Olá de tooopen lista **Adicionar atribuição** folha.

9.  Clique em Olá **usuários e grupos** seletor de saudação **Adicionar atribuição** folha.

10. Tipo de saudação **nome completo** ou **endereço de email** do usuário Olá que lhe interessam atribuindo em Olá **pesquisar por nome ou endereço de email** caixa de pesquisa.

11. Passe o mouse sobre Olá **usuário** em Olá lista tooreveal um **caixa de seleção**. Clique em tooadd de foto ou logotipo de perfil do Olá caixa de seleção próxima toohello usuário seu usuário toohello **selecionados** lista.

12. **Opcional:** se você gostaria que muito**adicionar mais de um usuário**, tipo em outro **nome completo** ou **endereço de email** em Olá **pesquisar por nome endereço de email ou** caixa de pesquisa e, em seguida, clique em tooadd de caixa de seleção Olá esse usuário toohello **selecionados** lista.

13. Quando você terminar de selecionar usuários, clique em Olá **selecione** botão tooadd-los toohello lista de usuários e grupos toobe atribuído toohello aplicativo.

14. **Opcional:** clique Olá **Selecionar função** seletor de saudação **Adicionar atribuição** folha tooselect uma função tooassign toohello usuários selecionados.

15. Clique em Olá **atribuir** botão tooassign Olá aplicativo toohello selecionado de usuários.

Após um curto período de tempo, usuários de saudação selecionado ser capaz de toolaunch esses aplicativos usando Olá métodos descritos na seção de descrição de solução de saudação.

## <a name="not-a-valid-saml-request"></a>Não é uma solicitação SAML válida

*Erro AADSTS75005: solicitação de Olá não é uma mensagem de protocolo Saml2 válida.*

**Possível causa**

AD do Azure não oferece suporte a saudação SAML solicitação enviada pelo aplicativo hello para logon único. Alguns problemas comuns são:

-   Faltando campos obrigatórios na solicitação SAML Olá

-   Método codificado de solicitação SAML

**Resolução**

1.  Capturar solicitação SAML. Siga o tutorial Olá [como toodebug baseado no SAML único logon tooapplications no AD do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn como solicitar toocapture Olá SAML.

2.  Entre em contato com o fornecedor do aplicativo hello e compartilhamento:

   -   Solicitação SAML

   -   [Requisitos de protocolo SAML de logon único do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

Eles devem validar suporte a implementação do Azure AD SAML Olá para logon único.

## <a name="no-resource-in-requiredresourceaccess-list"></a>Nenhum recurso na lista requiredResourceAccess

*Erro ao aplicativo de cliente AADSTS65005:hello solicitou acesso tooresource ' 00000002-0000-0000-c000-000000000000'. A solicitação falhou porque o cliente Olá não especificou esse recurso em sua lista de requiredResourceAccess*.

**Possível causa**

objeto de aplicativo Hello está corrompido.

**Resolução: opção 1**

problema de saudação toosolve, adicione o valor de identificador exclusivo da saudação na configuração de saudação do AD do Azure. tooadd um valor de identificador, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello

8.  Em Olá **domínio e a URL** seção, verifique no hello **Mostrar configurações de URL avançadas**.

9.  em Olá **identificador** um identificador exclusivo para o aplicativo hello de tipo de caixa de texto.

10. **Salvar** configuração hello.


**Resolução: opção 2**

Se a opção 1 acima não funcionou, tente remover o aplicativo hello de diretório hello. Em seguida, adicione e reconfigurar o aplicativo hello, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Clique em **excluir** na parte superior esquerda Olá da aplicativo hello **visão geral** folha.

8.  Atualizar o AD do Azure e adicionar o aplicativo hello da Galeria do AD do Azure hello. Em seguida, Configure o aplicativo hello

<span id="_Hlk477190176" class="anchor"></span>Depois de reconfigurar o aplicativo hello, você deve ser capaz de toosign no aplicativo toohello.

## <a name="certificate-or-key-not-configured"></a>Chave ou certificado não configurado

*Erro AADSTS50003: nenhuma chave de assinatura configurada.*

**Possível causa**

objeto de aplicativo Hello está corrompido e o AD do Azure não reconhece o certificado de saudação configurado para o aplicativo hello.

**Resolução**

toodelete e criar um novo certificado, execute as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

 * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Clique em **criar novo certificado** em Olá **SAML certificado de assinatura** seção.

9.  Selecione a data de validade. Em seguida, clique em **Salvar.**

10. Verificar **ativar o novo certificado** certificado do active toooverride hello. Em seguida, clique em **salvar** na parte superior de saudação da folha de saudação e aceitar o certificado de substituição tooactivate hello.

11. Em Olá **o certificado de autenticação SAML** seção, clique em **remover** tooremove Olá **não utilizado** certificado.

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a>Problema ao personalizar Olá SAML declarações enviadas tooan aplicativo

toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
[Como toodebug baseado no SAML único logon tooapplications no AD do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
