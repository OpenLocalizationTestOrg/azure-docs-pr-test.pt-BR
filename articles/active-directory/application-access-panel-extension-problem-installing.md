---
title: "aaaProblem instalar a extensão de navegador painel do acesso de aplicativo hello | Microsoft Docs"
description: "Como os erros comuns toofix encontrado ao instalar a extensão de navegador do painel de acesso de saudação"
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
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Problema ao instalar a extensão de navegador de painel de acesso do hello aplicativo

Olá painel de acesso é um portal baseado na web que permite que um usuário que tem um trabalho ou escola conta em aplicativos tooview e inicie baseado em nuvem do Azure Active Directory (AD do Azure) administrador Olá AD do Azure-los concedeu acesso ao. Um usuário com as edições do AD do Azure também pode usar grupos de autoatendimento e recursos de gerenciamento de aplicativo por meio do painel de acesso de saudação. Olá painel de acesso é separado do hello portal do Azure e não exige que os usuários toohave uma assinatura do Azure.

toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Atende aos requisitos de navegador de saudação painel de acesso

Olá painel de acesso requer um navegador que ofereça suporte ao JavaScript e CSS habilitou. toouse baseado em senha-logon único (SSO) no hello painel de acesso, Olá extensão do painel de acesso deve ser instalado no navegador do usuário hello. Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.

Para SSO baseado em senha, navegadores de saudação do usuário podem ser:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Edge no Windows 10 Anniversary Edition ou posterior 

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de navegador do painel de acesso

Olá tooinstall extensão de navegador do painel de acesso, execute as etapas de saudação abaixo:

1.  Olá abrir [painel de acesso](https://myapps.microsoft.com) em um dos navegadores Olá com suporte e entre como um **usuário** no AD do Azure.

2.  Clique em uma **aplicativo SSO de senha** no painel de acesso de saudação.

3.  Olá prompt perguntando tooinstall Olá software, selecione **instalar agora**.

4.  Com base em seu navegador é direcionado toohello link para download. **Adicionar** navegador de tooyour Olá extensão.

5.  Se seu navegador solicita, selecione tooeither **habilitar** ou **permitir** Olá extensão.

6.  Quando estiver instalado, **reinicie** a sessão do navegador.

7.  Entrar painel de acesso de saudação e veja se é possível **iniciar** seus aplicativos de SSO de senha

Você também pode baixar a extensão Olá para Chrome e borda de links diretos da saudação abaixo:

-   [Extensão do Painel de Acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão do Painel de Acesso do Edge](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configurar uma política de grupo para o Internet Explorer

Você pode configurar uma política de grupo que permitem que você extensão do painel de acesso de saudação do tooremotely instalar para o Internet Explorer em computadores de seus usuários.

os pré-requisitos de saudação incluem:

-   Você configurou o [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e você tiver ingressado domínio de tooyour máquinas dos usuários.

-   Você deve ter hello "Editar configurações de" permissão tooedit Olá objeto de política de grupo (GPO). Por padrão, membros da saudação grupos de segurança a seguir têm essa permissão: os administradores de domínio, administradores de empresa e proprietários de criadores de diretiva de grupo. [Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga o tutorial Olá [como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a política de grupo](active-directory-saas-ie-group-policy.md) para obter instruções passo a passo sobre como tooconfigure Olá a política de grupo e implantá-lo toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Solucionar problemas de saudação painel de acesso no Internet Explorer

Siga Olá [solucionar Olá extensão do painel de acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md) guia para acessar uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de saudação do IE.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se essas etapas de solução de problemas não resolver o problema de saudação

Abra um tíquete de suporte com hello informações a seguir se disponíveis:

-   ID de erro de correlação

-   UPN (endereço de email de usuário)

-   TenantID

-   Tipo de navegador

-   Fuso horário e hora/cronograma durante o erro

-   Rastreamentos do Fiddler

## <a name="next-steps"></a>Próximas etapas
[O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
