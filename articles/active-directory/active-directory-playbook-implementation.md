---
title: "aaaAzure guia estratégico de implementação do Active Directory PoC | Microsoft Docs"
description: "Explorar e implementar rapidamente os cenários de Identidade e Gerenciamento de Acesso"
services: active-directory
keywords: azure active directory, cartilha, Prova de Conceito, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Guia estratégico de prova de conceito do Azure Active Directory: Implementação

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation - sincronizando AD tooAzure AD 

Uma identidade híbrida é foundation Olá para a maioria das empresas Olá que já tem um diretório local. Olá, a meta aqui é toointentionally como reduzir o tempo gasto aqui como valor Olá tooshow possíveis cenários reais de identidade e acesso hello. 

| Cenário | Blocos de construção| 
| --- | --- |  
| [Estender seus locais de nuvem de toohello de identidade](#extending-your-on-premises-identity-to-the-cloud) | [Sincronização de Diretórios - PHS (sincronização de hash de senha)](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Observação**: se você já tiver o DirSync/ADSync ou versões anteriores do Azure AD Connect, esta etapa será opcional. Alguns cenários neste guia podem exigir uma versão mais recente do Azure AD Connect.  <br/>[Identidade visual](active-directory-playbook-building-blocks.md#branding) | 
| [Atribuindo licenças do Azure AD usando grupos](#assigning-azure-ad-licenses-using-groups) | [Licenciamento baseado em grupo](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Estender seus locais de nuvem de toohello de identidade 

1. Bob é administrador do Active Directory de saudação da Contoso. Ele obtém a identidade do hello requisito tooenable como um serviço para um conjunto de usuários. Após a execução do Assistente de conexão do AD do Azure, Olá identidade de saudação de usuários de destino disponíveis na nuvem hello. 
2. Bob pergunta Susie, um dos usuários de destino hello, tooaccess Olá painel de acesso do Active Directory do Azure e confirmar que ela pode autenticar. Susana vê uma página de logon com marca e um painel de acesso vazio, que está pronto para habilitar o acesso futuro a aplicativos.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Atribuição de licenças do Azure AD usando Grupos 

1. Bob é Olá Administrador Global do Azure AD e quer tooallocate AD do Azure licenças tooa conjunto específico de usuários como parte da implantação inicial de saudação do AD do Azure.
2. Bob cria um grupo de saudação usuários piloto. 
3. Bob atribui o grupo de toohello licenças Olá
4. Susie, um dos operadores de informações Olá, é adicionada toohello grupo de segurança como parte de suas funções de trabalho
5. Depois de algum tempo, Susie tem licença de acesso para toohello do Azure AD premium. Isso permitirá que mais cenários POC hello mais tarde.

## <a name="theme---lots-of-apps-one-identity"></a>Tema - muitos aplicativos, uma identidade

| Cenário | Blocos de construção| 
| --- | --- |  
| [Integrar aplicativos SaaS - SSO federado](#integrate-saas-applications---federated-sso) | [Configuração de SSO federado SaaS](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Grupos - propriedade delegada](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Integrar aplicativos SaaS - SSO de senha](#integrate-saas-applications---password-sso) | [Configuração do SSO de senha de SaaS](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [SSO e eventos de ciclo de vida de identidade](#sso-and-identity-lifecycle-events) | [Ciclo de vida de identidade e SaaS](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Contas de tooShared acesso seguras](#secure-access-to-shared-accounts) | [Configuração de Contas Compartilhadas SaaS](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Proteger aplicativos de locais de tooOn de acesso remoto](#secure-remote-access-to-on-premises-applications) | [Configuração de proxy de aplicativo](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [Sincronizar LDAP identidades tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [Configuração do Conector LDAP Genérico](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Integrar aplicativos SaaS - SSO federado 

1. Bob é Olá Administrador Global do Azure AD e recebe uma solicitação de saudação Marketing departamento tooenable acesso tootheir instância ServiceNow. Bob localiza um tutorial passo a passo de saudação na documentação do AD do Azure e segue e delegados Olá atribuição de tooKevin de aplicativo toohello usuários, head Olá da equipe de Marketing. 
2. Kevin fizer logon como proprietário de saudação do ServiceNow direitos e atribui Susie toohello aplicativo. Kevin também observa que o perfil de Susana foi criado automaticamente no ServiceNow
3. Susie é um operador de informações do departamento de Marketing hello. Ela registra no tooazure AD e localiza todos os aplicativos SaaS recebe tooin myapps portal. A partir daí, ele obtém perfeitamente tooServiceNow de acesso.
4. o departamento de Marketing Olá deseja tooaudit quem acessou o ServiceNow. Carlos baixa um relatório de atividades e o compartilha com Kevin por email.  

### <a name="sso-and-identity-lifecycle-events"></a>SSO e eventos de ciclo de vida de identidade

1. Susie usa uma licença e pela política corporativa Olá local conta do AD foi desabilitado temporário. Susie agora não é possível fazer logon no tooAzure AD e, portanto, não é possível acessar o ServiceNow. 
2. Susie faz um movimento lateral de tooSales de Marketing. Kevin remove o acesso dela do ServiceNow. Susie conecta Olá myapps de ad do azure e ela não vê Olá ServiceNow lado a lado. Após 10 minutos, Kevin confirma que a conta de Susana foi desabilitada no Console de gerenciamento do ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Integrar aplicativos SaaS - SSO de senha

1. Bob configura acesso tooAtlassian HipChat. HipChat tem tooSusie de SSO de senha integração e conceder acesso
2. Susie efetua logon no portal de myapps toohello e vê uma saudação do link toodownload extensão de navegador IE do AD do Azure, que ela baixa
3. Ao clicar, ela recebe a solicitação para fornecer suas credenciais de usuário e senha do HipChat. Essa é uma operação única e, depois de concluí-la, ela tem acesso tooHipChat
4. Alguns dias mais tarde, Susana abre o portal myapps e clica no HipChat novamente. Desta vez, ele obtém o acesso
5. Kevin, o proprietário do aplicativo HipChat hello, quer tooaudit quem acessou o aplicativo hello. Carlos baixa um relatório de auditoria e o compartilha com Kevin por email. 

### <a name="secure-access-tooshared-accounts"></a>Contas de tooShared acesso seguras 

1. Bob é encarregado toosecure Olá compartilhado Twitter identificador membros da equipe de vendas de saudação. Ele adiciona o Twitter como um aplicativo do SSO e atribui toohello o grupo de segurança de Olá, equipe de vendas. Ele recebeu Olá credenciais toohello compartilhado conta e ele fornece a ele no sistema de saudação. 
2. As credenciais de Twitter de compartilhamento não é mais confiável devido pessoas toomultiple conhecimento. Bob permite a substituição automática de senha do Twitter hello.
3. Susie, um membro da equipe de vendas hello, efetua logon no portal de myapps toohello e vê uma saudação do link toodownload extensão de navegador IE do AD do Azure. Ela instala a extensão.
4. Após clicar em ela obtenha acesso direto a tooTwitter. Não sabe a senha de saudação.
5. Arnold também faz parte da equipe de vendas de saudação. Ele tem Olá mesma experiência como Susie nas etapas 3 e 4
6. o departamento de vendas Olá deseja tooaudit quem acessou o Twitter. Carlos baixa um relatório de atividades e o compartilha com Kevin por email. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Proteger aplicativos de locais de tooOn de acesso remoto

1. Bob, hello Azure AD de Administrador Global, ficou diversas solicitações tooenable funcionários tooaccess útil vários recursos locais, como o aplicativo de despesas hello, enquanto estiver trabalhando remotamente. Ele segue Olá [documentação do Proxy de aplicativo](active-directory-application-proxy-enable.md) tooinstall um conector e publicar as despesas como um aplicativo de Proxy de aplicativo. 
2. Bob compartilha URL de aplicativo hello externa despesas com Susie, um dos funcionários de saudação que precisa de acesso remoto. Ela acessa o link Olá, e depois de autenticar no AAD, ela é capaz de tooaccess Olá despesas aplicativo e continuar toobe produtivo enquanto remoto. 
3. Bob, em seguida, continua a aplicativos de locais adicionais toopublish usando Olá mesmo processo e fornecendo acesso toousers conforme necessário. Ele adiciona acesso condicional e autenticação multifator para Olá aplicativos mais confidenciais que publica, tooensure adicionais de segurança.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>Sincronizar LDAP identidades tooAzure AD

1. A empresa de Carlos tem uma infraestrutura complexa de identidade. A maioria dos usuários de saudação é mantida dentro do Windows Server Active Directory domínio ADDS (serviços). Alguns deles são gerenciadas pelo sistema de RH dentro do ADLDS (Active Directory Lightweight Directory Services).
2. Bob é designado para habilitar aplicativos de tooSaaS de acesso para todos os usuários (também esses não presentes no ADDS).
3. Bob configura dados toopull conector de LDAP genérico ADLDS no Azure AD Connect.
4. Bob cria regras de sincronização para que usuários LDAP sejam preenchidos no metaverso e tooAzure AD
5. Susana, como usuário do LDAP, acessa seu aplicativo SaaS usando a identidade sincronizada



> [!IMPORTANT] 
> Esta é uma configuração avançada que exige alguma familiaridade com o FIM/MIM. Se usada em produção, aconselhamos consulgar as perguntas sobre essa configuração através do [Suporte Premier](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Tema - aumentar sua segurança 

| Cenário | Blocos de construção| 
| --- | --- |  
| [Acesso à conta de administrador protegida](#secure-administrator-account-access) | [Azure MFA com chamadas telefônicas](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Acesso seguro para aplicativos](#secure-access-to-applications) | [Acesso condicional para aplicativos SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Habilitar administração Just in Time](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Proteger identidades com base em riscos](#protect-identities-based-on-risk) | [Descoberta de eventos de risco](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Implantação de políticas de risco de logon](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Autenticar sem senhas usando autenticação baseada em certificado](#authenticate-without-passwords-using-certificate-based-authentication) | [Configurando autenticação baseada em certificado](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Acesso à conta de administrador protegida

1. Bob é Olá Administrador Global do AD do Azure. Ele identificou Stuart como um coadministrador do serviço de saudação. 
2. Bob configura conta de Stuart tooalways exigem postura de segurança do MFA tooimprove Olá
3. Stuart logs em toohello portal do Azure e os avisos que ele precisa tooregister seu logon do telefone número toocontinue Olá
4. Logons subsequentes de Stuart agora são protegidos com autenticação multifator e agora ele recebe um telefonema tooverify sua identidade.

### <a name="secure-access-tooapplications"></a>Acesso seguro tooapplications

1. Kevin é proprietário de negócios de saudação do ServiceNow. empresa de saudação agora deseja toologin esses usuários com MFA ao acessar a rede corporativa de saudação externa.
2. Bob, nosso Administrador Global do AD do Azure, adiciona um acesso condicional política toohello ServiceNow aplicativo tooenable MFA para acesso externo
3. Susie, nosso profissional da informação, faz logon no portal meus aplicativos e clica em bloco de ServiceNow hello. Agora ela recebe o desafio da MFA.

### <a name="enable-just-in-time-jit-administration"></a>Habilitar administração JIT (Just in Time)

1. Carlos e Stuart são Administradores Globais do Azure AD. Eles querem funções de gerenciamento de toohello tooenable JIT acesso e também registros tookeep sobre o uso Olá Olá privilegiado funções.
2. Bob permite PIM no locatário do AD do Azure hello e torna-se Olá administrador de segurança. Ele altera a mesmo e associação de função de administrador global de Stuart de tooeligible permanente.
3. Bob e Stuart agora precisam ativar suas funções por meio do portal do Azure de saudação antes de fazer quaisquer alterações tooAzure AD configuração. 

### <a name="protect-identities-based-on-risk"></a>Proteger identidades com base em riscos 

1. Susana, uma operadora de informações, tenta fazer logon de um navegador Tor. 
2. Bob verifica o painel de proteção de identidade Olá AD do Azure e vê o logon de Susie de um endereço IP anônimo. equipe de segurança Olá quer toochallenge tal acessa os usuários com MFA
3. Bob permite que a política do Azure AD Identity Protection toochallenge MFA para eventos de risco médio ou superior
4. O tempo passa e Susana faz logon pelo navegador Tor novamente. Neste momento, ela será exibida Olá desafio MFA

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Autenticar sem senhas usando autenticação baseada em certificado

1. Carlos é o Administrador Global da instituição financeira, que proíbe o uso de senhas como um fator de autenticação para seus aplicativos.
2. Carlos habilita e impõe a autenticação de certificado no ADFS e no Azure AD
3. Susie enquanto estiver acessar o aplicativo solicitado tooauthenticate usando o certificado

## <a name="theme---scale-with-self-service"></a>Tema - escala com serviço de autoatendimento

| Cenário | Blocos de construção| 
| --- | --- |  
| [Redefinição de senha por autoatendimento](#self-service-password-reset) | [Redefinição de senha por autoatendimento](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Self tooApplications acesso ao serviço](#self-service-access-to-applications) | [Self tooApplications acesso ao serviço](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Redefinição de senha por autoatendimento 

1. Bob é Olá AD do Azure Global admin e permite gerenciamento de senha do serviço de autoatendimento tooa subconjunto de usuários, incluindo Susie. 
2. Susie registra no portal de toomyapps e veja uma mensagem tooregister suas informações de segurança para eventos de redefinição de senha futuras.
3. Após alguns dias, Susana esquece sua senha e a redefine por meio do Portal do Azure AD

### <a name="self-service-access-tooapplications"></a>Self tooApplications acesso ao serviço 

1. Kevin é proprietário de negócios de saudação do ServiceNow. Ele quer que os usuários muito "Registrar" sob demanda, em vez de adicioná-los todos de uma vez
2. Bob, nosso Administrador Global do AD do Azure, modifica Olá ServiceNow aplicativo tooenable solicitações de autoatendimento
3. Susie, nosso profissional da informação, faz logon no portal meus aplicativos e cliques Olá botão "Adicionar mais aplicativos" e consulte ServiceNow como uma saudação recomendada de aplicativos. Em seguida, ela navega toomy back portal dos aplicativos e ver o aplicativo do ServiceNow hello.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]