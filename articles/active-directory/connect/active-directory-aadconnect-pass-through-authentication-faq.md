---
title: "Azure AD Connect: Autenticação de Passagem – Perguntas frequentes | Microsoft Docs"
description: "Toofrequently respostas perguntas frequentes sobre a autenticação de passagem do Azure Active Directory."
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Autenticação de passagem do Azure Active Directory: perguntas frequentes

Neste artigo, respondemos perguntas frequentes sobre a Autenticação de Passagem do Azure AD (Azure Active Directory). Continue verificando para ver novo conteúdo.

>[!IMPORTANT]
>recurso de autenticação de passagem de saudação está atualmente em visualização.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Qual Olá AD do Azure métodos de entrada - autenticação de passagem, sincronização de Hash de senha e os serviços de Federação do Active Directory (AD FS) - devo escolher?

Depende de seu ambiente local e dos requisitos organizacionais. Revise este artigo para uma [Olá de comparação de métodos de entrada do AD do Azure vários](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>A Autenticação de Passagem é um recurso gratuito?

Autenticação de passagem é um recurso gratuito e não é necessário qualquer edições pagas do AD do Azure toouse-lo. Ele permanece livre quando Olá recurso alcança disponibilidade geral.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>A Autenticação de Passagem está disponível na [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) e na [Nuvem do Microsoft Azure Governamental](https://azure.microsoft.com/features/gov/)?

Não, autenticação de passagem está disponível apenas na instância do hello world-wide do AD do Azure.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>O [Acesso Condicional](../active-directory-conditional-access.md) funciona com a Autenticação de Passagem?

Sim, todos os recursos de Acesso Condicional, incluindo a Autenticação Multifator do Azure, funcionam com a Autenticação de Passagem.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Autenticação de passagem dá suporte a "ID alternativa" como nome de usuário hello, em vez de "userPrincipalName"?

Sim. Dá suporte à autenticação de passagem `Alternate ID` como Olá username quando configurado no Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-get-started-custom.md). Nem todos os aplicativos do Office 365 dão suporte ao `Alternate ID`. Consulte a documentação do toohello do aplicativo específico de declaração de suporte de saudação.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Sincronização de Hash de senha agir como uma autenticação de fallback por meio do tooPass?

Não, a sincronização de Hash de senha não é genérica autenticação de fallback por meio do tooPass. Ela funciona como fallback apenas para [cenários a que a Autenticação de Passagem não dá suporte atualmente](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid usuário falhas de entrada, você deve configurar a autenticação de passagem para [alta disponibilidade](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>Posso instalar um [Proxy de aplicativo do Azure AD](../active-directory-application-proxy-get-started.md) conector Olá mesmo servidor como um agente de autenticação de passagem?

Sim, essa configuração é compatível com hello rebatizado versões do agente de autenticação de passagem da saudação (versões 1.5.193.0 ou posterior).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>De quais versões do Azure AD Connect e do Agente de Autenticação de Passagem você precisa?

Você precisa de versão 1.1.486.0 ou posterior para o Azure AD Connect e 1.5.58.0 ou posterior para hello agente de autenticação de passagem para toowork esse recurso. Todo o software deve ser instalado em servidores com Windows Server 2012 R2 ou posterior.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>O que acontece se a minha senha de usuário expirou e tente toosign usando a autenticação de passagem?

Se você tiver configurado [write-back de senha](../active-directory-passwords-update-your-own-password.md) para um usuário específico, e se o usuário Olá fizer logon usando a autenticação de passagem, alterar ou redefinir suas senhas. senhas de saudação são gravadas do Active Directory local tooon conforme o esperado.

No entanto, se o write-back de senha não está configurado para um usuário específico ou se hello o usuário não tem um AD do Azure válidas licença atribuída, usuário de saudação não pode atualizar sua senha na nuvem hello. Ele não poderá atualizar a senha mesmo que ela tenha expirado. Olá usuário vê esta mensagem: "sua organização não permite que você tooupdate sua senha neste site. Atualize-lo de acordo com o método toohello recomendado pela sua organização ou peça ao seu administrador se precisar de Ajuda." usuário Hello ou administrador Olá tem tooreset sua senha no Active Directory local.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>Como a Autenticação de Passagem protege você contra ataques de senha de força bruta?

Leia [este artigo](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) para obter mais informações.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>O que os Agentes de Autenticação de Passagem comunicam pelas portas 80 e 443?

- Olá autenticação agentes fazem solicitações HTTPS pela porta 443 para todas as operações de recurso.
- Olá autenticação agentes fazer solicitações HTTP pela porta 80 toodownload SSL listas de certificados revogados.

     >[!NOTE]
     >Atualizações recentes reduzimos número Olá das portas exigidas pelo recurso de saudação. Se você tiver versões mais antigas do Azure AD Connect ou hello agente de autenticação, mantenha essas portas abertas também: 5671, 8080, 9090, 9091, 9350, 9352 e 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Agentes de autenticação de passagem Olá pode se comunicar através de um servidor de proxy da web de saída?

Sim. Se WPAD (Web Proxy de descoberta automática) estiver habilitado no seu ambiente local, os agentes de autenticação tentativa toolocate automaticamente e usar um servidor de proxy da web na rede de saudação.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>Posso instalar dois ou mais agentes de autenticação de passagem em Olá mesmo servidor?

Não, você só pode instalar um Agente de Autenticação de Passagem em um único servidor. Se você quiser tooconfigure autenticação de passagem para alta disponibilidade, siga as instruções de Olá neste [artigo](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) em vez disso.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Eu já uso os Serviços de Federação do Active Directory (AD FS) para entrar no Azure AD. Como alternar-tooPass-por meio de autenticação?

Se você tiver configurado o AD FS como seu método de entrada usando o Assistente do hello Azure AD Connect, altere o método de entrada do usuário de saudação tooPass através da autenticação. Essa alteração permite que a autenticação de passagem no locatário hello e converte _todos os_ seus domínios federados em domínios gerenciados. Todas as solicitações de entrada posteriores em seu locatário serão tratadas pela Autenticação de Passagem. Atualmente, não há nenhuma maneira com suporte no Azure AD Connect toouse uma combinação do AD FS e autenticação de passagem em domínios diferentes.

Se o AD FS foi configurado como método de entrada hello _fora_ do Assistente para conectar-se de saudação do AD do Azure, altere o método de entrada do usuário de saudação autenticação por meio do tooPass (da opção "Não configurar" hello). Essa alteração permite que a autenticação de passagem no locatário hello. No entanto, todos os seus domínios federados continuam toouse do AD FS para entrar. Use PowerShell toomanually converter algumas ou todas as essas federados domínios tooManaged domínios. Depois disso, todas as solicitações de entrada em domínios gerenciados serão tradadas (_somente_) pela autenticação de passagem.

>[!IMPORTANT]
>A Autenticação de Passagem não trata da entrada para usuários do Azure AD somente na nuvem.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>Eu posso usar a Autenticação de Passagem em um ambiente de várias floresta do AD?

Sim. Ambientes de várias florestas têm suporte se houver relações de confiança entre suas florestas do AD e se o encaminhamento de sufixo de nome estiver configurado corretamente.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Os Agentes de Autenticação de Passagem fornecem a capacidade de balanceamento de carga?

Não, a instalação de vários Agentes de Autenticação de Passagem garante a [alta disponibilidade](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), mas não o balanceamento de carga. Um ou dois Olá agentes de autenticação podem terminar o tratamento de solicitações de entrada hello em massa de saudação.

As solicitações de validação de senha que Olá toohandle da necessidade de agentes de autenticação são simplificadas. Portanto, as cargas máxima e média da maioria dos clientes é facilmente manipulada pelos dois ou três Agentes de Autenticação no total.

É recomendável que você instale agentes de autenticação tooyour fechar controladores de domínio tooimprove entrar latência.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Posso instalar Olá primeiro agente de autenticação de passagem em um servidor diferente Olá que executa o Azure AD Connect?

Não, esse cenário _não_ tem suporte.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Quantos Agentes de Autenticação de Passagem devo instalar?

Recomendamos que:

- Você instale dois ou três Agentes de Autenticação no total. Essa configuração é suficiente para a maioria dos clientes.
- Instalar tooimprove entrar latência de agentes de autenticação nos controladores de domínio (ou fechar toothem possível).
- Você garantir que o servidores (onde os agentes de autenticação são instalados) sejam adicionados toohello AD mesma floresta como usuários Olá cujas senhas necessário toobe validado.

>[!NOTE]
>Há um limite do sistema de 12 Agentes de Autenticação por locatário.

## <a name="how-can-i-disable-pass-through-authentication"></a>Como posso desabilitar a Autenticação de Passagem?

Execute novamente o Assistente de conexão do AD do Azure hello e alterar o método de entrada do usuário de saudação do método de autenticação de passagem de tooanother. Esta alteração desabilita a autenticação de passagem em locatário hello e desinstala o hello agente de autenticação do servidor de saudação. Você tem toomanually desinstalação Olá agentes de autenticação de outros servidores.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>O que acontece quando eu desinstalo um Agente de Autenticação de Passagem?

Desinstalar um agente de autenticação de passagem de um servidor faz com que ele toostop aceitando solicitações de entrada. Verifique se você tem outro agente de autenticação em execução antes de realizar essa operação, tooavoid interrupção usuário entrar em seu locatário.

## <a name="next-steps"></a>Próximas etapas
- [**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento. Saiba quais cenários têm suporte e quais não têm.
- [**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.
- [**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
