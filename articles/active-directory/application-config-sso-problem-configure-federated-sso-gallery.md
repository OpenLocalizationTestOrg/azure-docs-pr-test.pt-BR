---
title: aaaProblem Configurando federado SSO para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Resolver alguns dos problemas comuns hello, você pode encontrar ao configurar federado único logon usando SAML para aplicativos que estão listados no hello Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Problema ao configurar o logon único federado para um aplicativo na Galeria do Azure AD

Se você encontrar um problema ao configurar um aplicativo. Verifique se que você tiver seguido todas as etapas de saudação tutorial Olá para o aplicativo hello. Configuração do aplicativo hello, você tem embutido documentação sobre como tooconfigure Olá aplicativo. Além disso, você pode acessar Olá [lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para uma orientação passo a passo de detalhes.

## <a name="cant-add-another-instance-of-hello-application"></a>Não é possível adicionar outra instância do aplicativo hello

tooadd uma segunda instância de um aplicativo, você precisa toobe capaz de:

-   Configure um identificador exclusivo para a segunda instância de saudação. Você não será capaz de tooconfigure Olá mesmo identificador usado para a primeira instância de saudação.

-   Configure um certificado diferente que Olá usada para Olá primeira instância.

Se hello aplicativo não oferece suporte a qualquer Olá acima. Em seguida, não será capaz de tooconfigure uma segunda instância.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Não é possível adicionar Olá identificador ou Olá URL de resposta

Se você não for capaz de tooconfigure Olá identificador ou Olá URL de resposta, confirme Olá identificador e valores de URL de resposta correspondam de padrões de saudação pré-configurado para o aplicativo hello.

padrões de saudação tooknow pré-configurado para o aplicativo hello:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.** Vá toostep 7. Se você já estiver na folha de configuração de aplicativo hello no AD do Azure.

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Selecione **baseado no SAML logon** de saudação **modo** lista suspensa.

9.  Vá toohello **identificador** ou **URL de resposta** textbox em Olá **seção URLs e de domínio.**

10. Há três maneiras tooknow padrões de saudação com suporte para o aplicativo hello:

   * Na caixa de texto de saudação, verá Olá suporte para padrões como um espaço reservado *exemplo:* <https://contoso.com>.

   * Se não há suporte para o padrão de hello, você verá um ponto de exclamação vermelho quando você tentar o valor de saudação tooenter na caixa de texto de saudação. Se você posicionar o mouse sobre o ponto de exclamação vermelho do hello, você veja os padrões de saudação com suporte.

   * Tutorial de saudação para o aplicativo hello, você também pode obter informações sobre os padrões de saudação com suporte. Em Olá **logon único do AD do Azure de configurar** seção. Etapa toohello vá para os valores de saudação configurado em Olá **domínio e URLs** seção.

Se os valores de saudação não coincidem com os padrões de saudação configurados previamente no AD do Azure. Você pode:

-   Trabalhar com hello aplicativo fornecedor tooget valores que correspondem a saudação padrão configurado previamente no AD do Azure

-   Ou, você pode contatar a equipe do AD do Azure em < aadapprequest@microsoft.com > ou deixar um comentário na atualização de Olá Olá tutorial toorequest dos padrões de saudação com suporte para o aplicativo hello

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>Onde definir o formato de ID (identificador de usuário) Olá

Não é o formato de ID (identificador de usuário) do hello tooselect capaz de AD do Azure envia toohello aplicativo em resposta Olá após a autenticação do usuário.

Azure AD Olá selecione formato Olá NameID atributo (identificador de usuário) com base no valor de saudação selecionado ou Olá formato solicitado pelo aplicativo hello em Olá AuthRequest SAML. Para obter mais informações, visite o artigo de saudação [protocolo SAML de logon único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) na seção Olá NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Não é possível localizar a configuração de Olá Olá AD do Azure metadados toocomplete com o aplicativo hello

os metadados do aplicativo hello toodownload ou o certificado do AD do Azure, siga as etapas de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

   * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello você configurou o logon único.

7.  Depois que o aplicativo hello carrega, clique em Olá **o logon único** no menu de navegação à esquerda do aplicativo hello.

8.  Vá muito**o certificado de autenticação SAML** seção e, em seguida, clique em **baixar** valor da coluna. Dependendo de qual aplicativo hello requer a configuração de logon único, você ver qualquer toodownload de opção Olá Olá Metadata XML ou Olá certificado.

AD do Azure não fornece um URL de metadados de saudação de tooget. Olá metadados somente podem ser recuperados como um arquivo XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Não sei como declarações SAML toocustomize enviado tooan aplicativo

toolearn como declarações de atributo toocustomize Olá SAML enviado tooyour aplicativo, consulte [declarações mapeamento no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
