---
title: "Autenticação de passagem do Azure AD – início rápido | Microsoft Docs"
description: "Este artigo descreve como tooget iniciado com a autenticação de passagem do Azure Active Directory (AD do Azure)."
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Autenticação de passagem do Azure Active Directory: início rápido

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Como toodeploy autenticação de passagem do AD do Azure

Autenticação de passagem do Azure Active Directory (AD do Azure) permite que seus usuários toosign tooboth locais e aplicativos baseados em nuvem usando Olá mesmas senhas. Ela permite a entrada de usuários validando suas senhas diretamente no Active Directory local.

>[!IMPORTANT]
>A autenticação de passagem do Azure AD está atualmente na versão prévia. Se você tiver sido usar esse recurso por meio da visualização, você deve garantir atualizar versões de visualização do hello autenticação agentes com instruções Olá [aqui](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

É necessário toofollow toodeploy essas instruções autenticação de passagem:

## <a name="step-1-check-prerequisites"></a>Etapa 1: verificar pré-requisitos

Certifique-se de que Olá pré-requisitos a seguir foram atendidos:

### <a name="on-hello-azure-active-directory-admin-center"></a>No Centro de administração do Active Directory do Azure Olá

1. Crie uma conta Administrador Global somente em nuvem no seu locatário do Azure AD. Dessa forma, você pode gerenciar configuração de saudação do seu locatário seus serviços locais falhar ou se tornar indisponíveis. Saiba mais sobre [adicionar uma conta de Administrador Global somente de nuvem](../active-directory-users-create-azure-portal.md). Executar essa etapa é tooensure crítica que você não seja bloqueada do seu locatário.
2. Adicione um ou mais [nomes de domínio personalizado](../active-directory-add-domain.md) locatário tooyour AD do Azure. Os usuários entram usando um desses nomes de domínio.

### <a name="in-your-on-premises-environment"></a>Em seu ambiente local

1. Identifique um servidor que executa o Windows Server 2012 R2 ou posterior no qual toorun do Azure AD Connect. Adicione floresta do servidor de saudação toohello mesmo AD como usuários de Olá cujas senhas necessário toobe validado.
2. Instalar Olá [versão mais recente do Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) no servidor de saudação identificado na etapa anterior. Se você já tiver a execução do Azure AD Connect, certifique-se de que a versão Olá é 1.1.557.0 ou posterior.
3. Identificar um servidor adicional executando o Windows Server 2012 R2 ou posterior no qual toorun um autônomo agente de autenticação. versão do agente de autenticação Olá precisa toobe 1.5.193.0 ou posterior. Este servidor é necessário tooensure alta disponibilidade das solicitações de entrada. Adicione floresta do servidor de saudação toohello mesmo AD como usuários de Olá cujas senhas necessário toobe validado.
4. Se houver um firewall entre os servidores e o AD do Azure, você precisa tooconfigure Olá itens a seguir:
   - Certifique-se de que os agentes de autenticação podem fazer **saída** solicitações tooAzure AD pela Olá portas a seguir:
   
   | Número da porta | Como ele é usado |
   | --- | --- |
   | **80** | Baixando a revogação de certificado CRLs (listas) ao validar o certificado SSL Olá |
   | **443** | Toda a comunicação de saída com o nosso serviço |
   
   Se o firewall reforça toooriginating usuários de acordo com as regras, abra essas portas para o tráfego dos serviços do Windows que são executados como serviço de rede.
   - Se seu firewall ou proxy permite lista branca de DNS, conexões de lista branca muito**\*. msappproxy.net** e  **\*. n e t**. Se não, permitir o acesso muito[intervalos de IP de DataCenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653), que é atualizado semanalmente.
   - Os agentes de autenticação precisam de acesso muito**login.windows.net** e **login.microsoftonline.com** para o registro inicial, isso abra o firewall para as URLs também.
   - Para validação de certificado, desbloquear Olá seguintes URLs: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** e  **www.microsoft.com:80**. Essas URLs são usadas para a validação de certificado com outros produtos da Microsoft, então você talvez já tenha essas URLs desbloqueadas.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Etapa 2: Habilitar o suporte do Exchange ActiveSync (opcional)

Siga essas instruções tooenable suporte do Exchange ActiveSync:

1. Use [PowerShell do Exchange](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) Olá toorun comando a seguir:
```
Get-OrganizationConfig | fl per*
```

2. Verifique o valor Olá Olá `PerTenantSwitchToESTSEnabled` configuração. Se o valor de saudação é **true**, seu locatário está configurado corretamente - isso é geralmente o caso de Olá para a maioria dos clientes. Se o valor de saudação é **false**, execute hello seguinte comando:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Verifique se o valor de Olá Olá `PerTenantSwitchToESTSEnabled` configuração agora está definida muito**true**. Aguarde uma hora antes da movimentação toohello a próxima etapa.

Se você enfrentar problemas durante esta etapa, verifique nosso [guia de solução de problemas](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) para obter mais informações.

## <a name="step-3-enable-hello-feature"></a>Etapa 3: Habilitar o recurso de saudação

A autenticação de passagem pode ser habilitada usando o [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Autenticação de passagem pode ser habilitada no servidor de principal ou de preparação de conectar Olá AD do Azure. É altamente recomendável habilitá-lo do servidor primário hello.

Se você estiver instalando o Azure AD Connect para Olá primeira vez, escolha Olá [caminho de instalação personalizado](active-directory-aadconnect-get-started-custom.md). Em Olá **usuário entrar** escolha **autenticação de passagem** como Olá entrada no método. Após a conclusão bem-sucedida, um agente de autenticação de passagem é instalado em Olá mesmo servidor do Azure AD Connect. Além disso, o recurso de autenticação de passagem de saudação está habilitado no seu locatário.

![Azure AD Connect – conexão do usuário](./media/active-directory-aadconnect-sso/sso3.png)

Se você já tiver instalado o Azure AD Connect (usando Olá [instalação expressa](active-directory-aadconnect-get-started-express.md) ou hello [instalação personalizada](active-directory-aadconnect-get-started-custom.md) caminho), selecione **página de entrada do usuário de alteração** no AD do Azure Conecte-se e, em seguida, clique em **próximo**. Em seguida, selecione **autenticação de passagem** como Olá entrada no método. Após a conclusão bem-sucedida, um agente de autenticação de passagem é instalado em Olá mesmo servidor como recurso Connect e saudação do AD do Azure está habilitado no seu locatário.

![Azure AD Connect – Alterar entrada do usuário](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>A Autenticação de Passagem é um recurso no nível do locatário. Ativá-lo afeta entrar para usuários em _todos os_ Olá gerenciados domínios em seu locatário. Se estiver alternando de tooPass-por meio de autenticação do AD FS, recomendamos que você aguarde pelo menos 12 horas antes de desligar a infraestrutura do AD FS - esse tempo de espera é tooensure que os usuários podem manter entrando tooExchange ActiveSync durante a transição.

## <a name="step-4-test-hello-feature"></a>Etapa 4: Testar o recurso de saudação

Siga essas tooverify instruções que você habilitou a autenticação de passagem corretamente:

1. Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global de saudação para seu locatário.
2. Selecione **Active Directory do Azure** na navegação esquerda hello.
3. Selecione **Azure AD Connect**.
4. Verifique se esse Olá **autenticação de passagem** recurso mostra como **habilitado**.
5. Selecione **Autenticação de passagem**. Esta folha lista servidores de saudação onde os agentes de autenticação estão instalados.

![Centro de administração do Azure Active Directory - folha Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centro de administração do Azure Active Directory - folha Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

Nesse momento, os usuários de todos os domínios gerenciados no seu locatário podem entrar usando a Autenticação de passagem. No entanto, os usuários de domínios federados continuam toosign usando os serviços de Federação do Active Directory (AD FS) ou outro provedor de federação que você configurou anteriormente. Se você converter um domínio de toomanaged federado, todos os usuários desse domínio iniciar automaticamente a assinatura usando a autenticação de passagem. Os usuários somente em nuvem não são afetados pelo recurso de autenticação de passagem de saudação.

## <a name="step-5-ensure-high-availability"></a>Etapa 5: Verificar a alta disponibilidade

Se você planejar toodeploy autenticação de passagem em um ambiente de produção, você deve instalar um agente de autenticação autônomo. Instalar este agente de autenticação de segundo em um servidor _outros_ de Olá uma execução do Azure AD Connect e Olá primeiro o agente de autenticação. Esta instalação fornece alta disponibilidade para solicitações de entrada. Siga essas instruções toodeploy um agente de autenticação autônomo:

1. **Baixar a versão mais recente Olá de saudação agente de autenticação (versões 1.5.193.0 ou posterior)**: entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global do locatário.
2. Selecione **Active Directory do Azure** na navegação esquerda hello.
3. Selecione **Azure AD Connect** e, em seguida, **Autenticação de passagem**. E selecione **Baixar agente**.
4. Clique em Olá **aceitar termos & baixar** botão.
5. **Instale a versão mais recente Olá de saudação agente de autenticação**: executar Olá executável baixado na saudação anterior da etapa. Forneça as suas credenciais de Administrador Global do locatário quando solicitado.

![Centro de administração do Azure Active Directory - botão de Baixar Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Centro de administração do Azure Active Directory - folha para Baixar Agente](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>Você também pode baixar Olá agente de autenticação de [aqui](https://aka.ms/getauthagent). Certifique-se de que você leia e aceite o agente de autenticação a saudação [termos de serviço](https://aka.ms/authagenteula) _antes de_ instalá-lo.

## <a name="next-steps"></a>Próximas etapas
- [**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento. Saiba quais cenários têm suporte e quais não têm.
- [**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-pass-through-authentication-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
