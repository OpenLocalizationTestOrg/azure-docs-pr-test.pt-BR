---
title: "Azure AD Connect: Autenticação de passagem – atualização de agentes de autenticação de versão prévia | Microsoft Docs"
description: "Este artigo descreve como tooupgrade sua configuração de autenticação de passagem do Azure Active Directory (AD do Azure)."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Autenticação de passagem do Azure Active Directory: atualização de agentes de autenticação de versão prévia

## <a name="overview"></a>Visão geral

Este artigo é para clientes que usam a Autenticação de passagem do Azure AD por meio da versão prévia. Podemos Olá recentemente atualizado (e copiada) software de agente de autenticação. Você precisa de visualização de atualização too_manually_ autenticação agentes instalados nos servidores locais. Esta atualização manual é uma ação que deve ser realizada uma única vez. Todas as atualizações futuras tooAuthentication agentes são automáticos. Olá motivos tooupgrade são da seguinte maneira:

- versões de visualização de saudação de agentes de autenticação não receberão qualquer ainda mais a segurança ou correções de bugs.
-   versões de visualização de saudação de agentes de autenticação não podem ser instaladas em servidores adicionais, para alta disponibilidade.

## <a name="check-versions-of-your-authentication-agents"></a>Verificar as versões dos seus Agentes de autenticação

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>Etapa 1: verificar o local em que os Agentes de autenticação estão instalados

Siga estas etapas toocheck onde os agentes de autenticação estão instalados:

1. Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global de saudação para seu locatário.
2. Selecione **Active Directory do Azure** na navegação esquerda hello.
3. Selecione **Azure AD Connect**. 
4. Selecione **Autenticação de passagem**. Esta folha lista servidores de saudação onde os agentes de autenticação estão instalados.

![Centro de administração do Azure Active Directory - folha Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>Etapa 2: Verificar as versões de saudação do seus agentes de autenticação

versões de saudação toocheck de seus agentes de autenticação, em cada servidor identificado na saudação anterior da etapa, siga estas instruções:

1. Vá muito**painel de controle -> Programas -> Programas e recursos** no servidor de local de saudação.
2. Se houver uma entrada para "**agente do Microsoft Azure AD Connect autenticação**", você não precisa tootake qualquer ação nesse servidor.
3. Se houver uma entrada para "**conector de Proxy de aplicativo do Microsoft Azure AD**", versões 1.5.132.0 ou anterior, você precisa toomanually atualização neste servidor.

![Versão prévia do Agente de autenticação](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>Práticas recomendadas toofollow antes de iniciar a atualização de saudação

Antes de atualizar, certifique-se de que você tenha Olá itens no local a seguir:

1. **Criar conta de Administrador Global somente em nuvem**: não atualizar sem a necessidade de toouse uma conta de Administrador Global somente em nuvem em situações de emergência onde os agentes de autenticação de passagem não estão funcionando adequadamente. Saiba mais sobre [adicionar uma conta de Administrador Global somente de nuvem](../active-directory-users-create-azure-portal.md). A realização dessa etapa é fundamental e garante que você não ficará bloqueado do seu locatário.
2.  **Garantir a alta disponibilidade**: se não concluído anteriormente, instale um segundo autônomo agente de autenticação tooprovide alta disponibilidade para solicitações de entrada, usando esses [instruções](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Atualizando Olá agente de autenticação no servidor do Azure AD Connect

Você precisa atualizar do Azure AD Connect antes de atualizar Olá agente de autenticação em Olá mesmo servidor. Siga estas etapas em seus servidores primários e de preparo do Azure AD Connect:

1. **Atualização do Azure AD Connect**: siga essa [artigo](./active-directory-aadconnect-upgrade-previous-version.md) e toohello mais recente do Azure AD Connect versão de atualização.
2. **Desinstalar a versão de visualização de saudação do hello agente de autenticação**: baixar [este script do PowerShell](https://aka.ms/rmpreviewagent) e executá-lo como um administrador no servidor de saudação.
3. **Baixar a versão mais recente Olá de saudação agente de autenticação (versões 1.5.193.0 ou posterior)**: entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global do locatário. Selecione **Azure Active Directory -> Azure AD Connect -> Autenticação de passagem -> Baixar agente**. Aceite os termos de saudação do serviço e baixar a versão mais recente Olá de saudação agente de autenticação.
4. **Instale a versão mais recente Olá de saudação agente de autenticação**: executar Olá executável baixado na etapa 3. Forneça as suas credenciais de Administrador Global do locatário quando solicitado.
5. **Verificar a versão mais recente Olá foi instalado**: conforme mostrado antes, vá muito**painel de controle -> Programas -> Programas e recursos** e verifique se há uma entrada para "**Microsoft Azure AD Connect Agente de autenticação**".

>[!NOTE]
>Se você marcar a folha de autenticação de passagem de saudação no hello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) depois de concluir Olá etapas anteriores, você verá duas entradas de agente de autenticação por servidor - uma entrada mostrando Olá Agente de autenticação como **Active** e Olá outros como **inativo**. Isso é _esperado_. Olá **inativo** entrada é descartada automaticamente depois de alguns dias.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>Atualizando Olá agente de autenticação em outros servidores

Siga essas etapas tooupgrade agentes de autenticação em outros servidores (onde o Azure AD Connect não está instalado):

1. **Desinstalar a versão de visualização de saudação do hello agente de autenticação**: baixar [este script do PowerShell](https://aka.ms/rmpreviewagent) e executá-lo como um administrador no servidor de saudação.
2. **Baixar a versão mais recente Olá de saudação agente de autenticação (versões 1.5.193.0 ou posterior)**: entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global do locatário. Selecione **Azure Active Directory -> Azure AD Connect -> Autenticação de passagem -> Baixar agente**. Aceite os termos de saudação do serviço e baixar a versão mais recente do hello.
3. **Instale a versão mais recente Olá de saudação agente de autenticação**: executar Olá executável baixado na etapa 2. Forneça as suas credenciais de Administrador Global do locatário quando solicitado.
4. **Verificar a versão mais recente Olá foi instalado**: conforme mostrado antes, vá muito**painel de controle -> Programas -> Programas e recursos** e verifique se há uma entrada chamada **Microsoft Azure AD Connect Agente de autenticação**.

>[!NOTE]
>Se você marcar a folha de autenticação de passagem de saudação no hello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) depois de concluir Olá etapas anteriores, você verá duas entradas de agente de autenticação por servidor - uma entrada mostrando Olá Agente de autenticação como **Active** e Olá outros como **inativo**. Isso é _esperado_. Olá **inativo** entrada é descartada automaticamente depois de alguns dias.

## <a name="next-steps"></a>Próximas etapas
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
