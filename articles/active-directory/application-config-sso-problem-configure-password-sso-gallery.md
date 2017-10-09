---
title: aaaProblem configurando senha single sign-on para um aplicativo da Galeria do AD do Azure | Microsoft Docs
description: "Entender a face de pessoas problemas comuns Olá ao configurar logon único de senha para aplicativos que já estão listados no hello Galeria de aplicativos do Azure AD"
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problema ao configurar o logon único com senha para um aplicativo na Galeria do Azure AD

Este artigo ajuda face de pessoas de problemas comuns do toounderstand Olá ao configurar **senha Single Sign-on** com um aplicativo da Galeria do AD do Azure.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>As credenciais são preenchidas, mas a extensão Olá não enviá-los

Isso geralmente acontece se o fornecedor do aplicativo hello mudou sua entrada recentemente página tooadd um campo, alterar um identificador subjacente que usamos campos de nome de usuário e senha Olá toodetect ou modificar como entrada hello experiência funciona para seus aplicativos. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicativos fornecedores toorapidly resolver esses problemas.

Enquanto a Microsoft tem tecnologias tooautomatically detectar quando essas integrações quebrar, mas, às vezes, não é capaz de toofind esses problemas direito ausente, ou se eles contêm algum tempo toofix. No caso de Olá quando uma dessas integrações não funciona corretamente, agradeceríamos se você abrir um caso de suporte para que possamos corrigi-lo assim que possível.

Em adição toothis, **se você em contato com o fornecedor do aplicativo,** **enviá-los em nossa maneira** para que possamos trabalhar com eles toonatively integrar seus aplicativos com o Active Directory do Azure. Você pode enviar Olá fornecedor toohello [listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los iniciados.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>As credenciais estão preenchidas e enviadas, mas página Olá indica Olá credenciais estão incorretas

tooresolve esse problema, primeiro seguinte Olá de verificação:

-   Faça com que o usuário Olá primeiro tentar muito**entrar no site de aplicativo toohello diretamente** com hello credenciais armazenadas para eles.

  * Se isso funcionar, em seguida, ter Olá usuário clique Olá **atualizar credenciais** botão Olá **bloco de aplicativo** em Olá **aplicativos** seção Olá [aplicativo Acessar o painel](https://myapps.microsoft.com/) tooupdate-los toohello mais recente conhecido trabalhando nome de usuário e senha.

   * Se você ou outro credenciais de Olá administrador atribuído para este usuário, localizar usuário hello ou atribuição de aplicativo do grupo navegando toohello **usuários e grupos** guia do aplicativo hello, selecionando a atribuição de saudação e clicando em Olá **credenciais de atualização** botão.

-   Se o usuário Olá atribuído suas próprias credenciais, ter usuário Olá **verificar toobe-se de que sua senha não expirou no aplicativo hello** e nesse caso, **atualizar sua senha expirada** entrando no toohello aplicativo diretamente.

   * Após Olá senha foi atualizada no aplicativo hello, solicitar Olá Olá de tooclick usuário **atualizar credenciais** botão Olá **bloco de aplicativo** em Olá **aplicativos** seção de saudação [painel de acesso do aplicativo](https://myapps.microsoft.com/) tooupdate-los toohello mais recente conhecido trabalhando nome de usuário e senha.

   * Se você ou outro credenciais de Olá administrador atribuído para este usuário, localizar usuário hello ou atribuição de aplicativo do grupo navegando toohello **usuários e grupos** guia do aplicativo hello, selecionando a atribuição de saudação e clicando em Olá **credenciais de atualização** botão.

-   Têm extensão de navegador Olá usuário atualização Olá acesso painel seguindo as etapas Olá na Olá [como tooinstall Olá extensão de navegador do painel de acesso](#how-to-install-the-access-panel-browser-extension) seção.

-   Verifique se a extensão de navegador do painel de acesso hello está em execução e habilitados no navegador do usuário.

-   Certifique-se de que os usuários não estão tentando toosign no aplicativo toohello do painel de acesso Olá ao mesmo tempo em **modo privado, inPrivate ou incognito**. Não há suporte para a extensão do painel de acesso Olá nesses modos.

Caso isso não funciona, ele pode ser o caso de Olá que ocorreu uma alteração no lado do aplicativo hello que violou temporariamente a integração do aplicativo hello com o Azure AD. Por exemplo, isso pode ocorrer quando o fornecedor do aplicativo hello apresenta um script em sua página que se comporta de forma diferente para vs manuais automatizada de entrada, que faz com que automatizada de integração, como nosso próprio, toobreak. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicativos fornecedores toorapidly resolver esses problemas.

Enquanto a Microsoft tem tecnologias tooautomatically detectar quando essas integrações quebrar, mas, às vezes, não é capaz de toofind esses problemas direito ausente, ou se eles contêm algum tempo toofix. No caso de Olá quando uma dessas integrações não funciona corretamente, agradeceríamos se você abrir um caso de suporte para que possamos corrigi-lo assim que possível.

Em adição toothis, **se você em contato com o fornecedor do aplicativo,** **enviá-los em nossa maneira** para que possamos trabalhar com eles toonatively integrar seus aplicativos com o Active Directory do Azure. Você pode enviar Olá fornecedor toohello [listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los iniciados.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>extensão de saudação funciona no Chrome e Firefox, mas não no Internet Explorer

Há duas causas principais toothis problema:

-   Dependendo das configurações de segurança de saudação habilitadas no Internet Explorer, se o site de saudação não for parte de um **zona confiáveis**, às vezes, nosso script impedidos de execução para o aplicativo hello.

  *  tooresolve isso, instrua o usuário de saudação muito**adicionar sites da Web do aplicativo hello** toohello **Sites confiáveis** lista dentro de seus **as configurações de segurança do Internet Explorer**. Você pode enviar seu usuários toohello [como tooadd toomy um site confiável sites lista](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artigo para obter instruções detalhadas.

-   Em circunstâncias raras, validação de segurança do Internet Explorer pode às vezes causar tooload de página hello mais lentamente do que a execução de saudação do nosso script.

   * Infelizmente, essa situação pode variar dependendo da versão do navegador hello, velocidade do computador ou site visitado. Nesse caso, é recomendável que você contate o suporte para que possamos corrigir integração Olá para esse aplicativo específico.

Em adição toothis, **se você em contato com o fornecedor do aplicativo,** **enviá-los em nossa maneira** para que possamos trabalhar com eles toonatively integrar seus aplicativos com o Active Directory do Azure. Você pode enviar Olá fornecedor toohello [listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los iniciados.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Verifique se hello página de logon do aplicativo foi alterado recentemente ou requer um campo adicional

Se a página de logon do aplicativo hello mudou drasticamente, às vezes, isso faz com que o nosso toobreak integrações. Um exemplo disso é quando um fornecedor do aplicativo adiciona uma entrada no campo, um captcha, ou passa por tootheir de autenticação multifator. Felizmente, em muitos casos, Microsoft pode trabalhar com aplicativos fornecedores toorapidly resolver esses problemas.

A Microsoft tem tecnologias tooautomatically detectar quando essas integrações quebrar, mas, às vezes, não é possível toofind esses emite imediatamente. Caso contrário, eles têm toofix algum tempo. No caso de Olá quando uma dessas integrações não funciona corretamente, agradeceríamos abrir um caso de suporte para que possamos corrigi-lo assim que possível.

Em adição toothis, **se você em contato com o fornecedor do aplicativo,** **enviá-los em nossa maneira** para que possamos trabalhar com eles toonatively integrar seus aplicativos com o Active Directory do Azure. Você pode enviar Olá fornecedor toohello [listando seu aplicativo na Galeria de aplicativo do Active Directory do Azure Olá](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget-los iniciados.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de navegador do painel de acesso

Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:

1.  Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.

2.  Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.

3.  Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.

4.  Com base em seu navegador é direcionado toohello link para download. **Adicionar** navegador de tooyour Olá extensão.

5.  Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.

6.  Quando estiver instalado, **reinicie** a sessão do navegador.

7.  Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha

Você também pode baixar a extensão Olá para Chrome e Firefox de links diretos da saudação abaixo:

-   [Extensão do Painel de Acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão do Painel de Acesso do Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)

