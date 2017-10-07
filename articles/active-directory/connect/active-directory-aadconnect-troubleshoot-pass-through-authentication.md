---
title: "Azure AD Connect: solução de problemas de autenticação de passagem | Microsoft Docs"
description: "Este artigo descreve como tootroubleshoot autenticação de passagem do Azure Active Directory (AD do Azure)."
services: active-directory
keywords: "Solução de problemas de Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
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
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Solucionar problemas de Autenticação de Passagem do Azure Active Directory

Este artigo ajuda você a localizar informações de solução de problemas comuns relacionados à autenticação de passagem do Azure AD.

>[!IMPORTANT]
>Se você está enfrentando usuário problemas para entrar com a autenticação de passagem, não desabilitar o recurso de saudação ou desinstalar os agentes de autenticação de passagem sem ter que toofall uma conta de Administrador Global somente em nuvem novamente. Saiba mais sobre [adicionar uma conta de Administrador Global somente de nuvem](../active-directory-users-create-azure-portal.md). A realização dessa etapa é fundamental e garante que você não ficará bloqueado do seu locatário.

## <a name="general-issues"></a>Problemas gerais

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Verificar o status do recurso de saudação e agentes de autenticação

Certifique-se de que esse recurso de autenticação de passagem Olá ainda é **habilitado** no status do locatário e hello dos agentes de autenticação mostra **Active**e não **inativo**. Você pode verificar o status, vai toohello **do Azure AD Connect** folha no hello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/).

![Centro de administração do Azure Active Directory - folha Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centro de administração do Azure Active Directory - folha Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Mensagens de erro de entrada voltadas ao usuário

Se usuário Olá toosign não é possível em usando a autenticação de passagem, eles poderão ver uma saudação voltado ao usuário os erros a seguir na tela de entrada hello AD do Azure: 

|Erro|Descrição|Resolução
| --- | --- | ---
|AADSTS80001|Não é possível tooconnect tooActive diretório|Verifique se o agente de servidores é membros da floresta Olá mesmo AD como usuários Olá cujas senhas necessário toobe validado e são tooActive tooconnect capaz de diretório.  
|AADSTS8002|Tempo limite esgotado tooActive conexão diretório|Verifique tooensure que o Active Directory está disponível e está respondendo toorequests dos agentes de saudação.
|AADSTS80004|saudação de nome de usuário passado toohello agente não era válido|Certifique-se de usuário hello está tentando toosign com direito Olá de nome de usuário.
|AADSTS80005|Validação encontrou WebException imprevisível|Um erro transitório. Repita a solicitação de saudação. Se ele persistir toofail, contate o suporte da Microsoft.
|AADSTS80007|Erro na comunicação com o Active Directory|Verifique os logs de agente Olá para obter mais informações e verificar se o Active Directory está funcionando conforme o esperado.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Motivos de falha no logon no Centro de administração do Active Directory do Azure Olá

Iniciar a solução de problemas de logon do usuário, observando Olá [relatório de atividade de entrada](../active-directory-reporting-activity-sign-ins.md) em Olá [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/).

![Centro de administração do Azure Active Directory - relatório Entradas](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Navegue muito**Active Directory do Azure** -> **entradas** em Olá [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com/) e clique em atividade de entrada de um usuário específico. Procure Olá **código de erro de entrada** campo. Mapear o valor de saudação do motivo da falha do campo tooa e resolução usando Olá a tabela a seguir:

|Código de erro de logon|Motivo da falha no logon|Resolução
| --- | --- | ---
| 50144 | A senha do Active Directory do usuário expirou. | Redefina a senha do usuário Olá no Active Directory local.
| 80001 | Nenhum Agente de Autenticação disponível. | Instale e registre um Agente de Autenticação.
| 80002 | A solicitação de validação de senha do Agente de Autenticação atingiu o tempo limite. | Verifique se o seu Active Directory está acessível a partir do hello agente de autenticação.
| 80003 | Resposta inválida recebida pelo Agente de Autenticação. | Se o problema de saudação consistentemente reproduzível por vários usuários, verifique a configuração do Active Directory.
| 80004 | Nome UPN incorreto usado na solicitação de entrada. | Peça Olá toosign de usuário com nome de usuário correto hello.
| 80005 | Agente de Autenticação: ocorreu um erro. | Erro transitório. Tente novamente mais tarde.
| 80007 | Autenticação agente tooconnect não é possível tooActive Directory. | Verifique se o seu Active Directory está acessível a partir do hello agente de autenticação.
| 80010 | Senha de toodecrypt não é possível do agente de autenticação. | Se o problema de saudação consistentemente reproduzível, instalar e registrar um novo agente de autenticação. E desinstale Olá atual. 
| 80011 | Chave de descriptografia não é possível tooretrieve do agente de autenticação. | Se o problema de saudação consistentemente reproduzível, instalar e registrar um novo agente de autenticação. E desinstale Olá atual.

## <a name="authentication-agent-installation-issues"></a>Problemas de instalação do Agente de Autenticação

### <a name="an-unexpected-error-occurred"></a>Erro inesperado

[Coletar logs de agente](#collecting-pass-through-authentication-agent-logs) do servidor de saudação e entre em contato com Microsoft Support com seu problema.

## <a name="authentication-agent-registration-issues"></a>Problemas de registro do Agente de Autenticação

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Falha do registro de saudação agente de autenticação tooblocked portas de conclusão

Certifique-se de que esse servidor de saudação no qual Olá agente de autenticação tenha sido instalado pode se comunicar com nosso serviço URLs e portas listadas [aqui](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Falha do registro de saudação agente de autenticação devido a erros de autorização tootoken ou conta

Use uma conta Administrador Global somente de nuvem para todas as operações de registro e instalação de Agente de Autenticação do Azure AD Connect ou autônomo. Há um problema conhecido com contas de Administrador Global habilitado MFA; Desative temporariamente MFA (somente operações de saudação toocomplete) como uma solução alternativa.

### <a name="an-unexpected-error-occurred"></a>Erro inesperado

[Coletar logs de agente](#collecting-pass-through-authentication-agent-logs) do servidor de saudação e entre em contato com Microsoft Support com seu problema.

## <a name="authentication-agent-uninstallation-issues"></a>Problemas de desinstalação do Agente de Autenticação

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Mensagem de aviso ao desinstalar o Azure AD Connect

Se você tiver habilitado em seu locatário de autenticação de passagem e tente toouninstall do Azure AD Connect, ele mostra Olá a seguinte mensagem de aviso: "os usuários não será capaz de AD toosign em tooAzure a menos que você tenha outros agentes de autenticação de passagem instalado em outros servidores."

Certifique-se de que a configuração está [alta disponível](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) antes de desinstalar o Azure AD Connect tooavoid quebra a entrada do usuário.

## <a name="issues-with-enabling-hello-feature"></a>Problemas com a habilitação do recurso de saudação

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Falha ao habilitar o recurso de saudação porque não havia nenhum agente de autenticação

Você precisa toohave tooenable de agente de autenticação active pelo menos uma autenticação de passagem em seu locatário. Você pode instalar um Agente de Autenticação através da instalação do Azure AD Connect ou de um Agente de Autenticação autônomo.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Falha ao habilitar o recurso de saudação tooblocked portas de conclusão

Certifique-se de que esse servidor de saudação em que o Azure AD Connect está instalado pode se comunicar com nosso serviço URLs e portas listadas [aqui](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Falha ao habilitar o recurso de saudação devido a erros de autorização tootoken ou conta

Certifique-se de que você use uma conta de Administrador Global somente em nuvem ao habilitar o recurso de saudação. Há um problema conhecido com a autenticação multifator (MFA)-habilitado contas de Administrador Global; Desative temporariamente MFA (somente operação de saudação toocomplete) como uma solução alternativa.

## <a name="exchange-activesync-configuration-issues"></a>Problemas de configuração do Exchange ActiveSync

Esses são os problemas comuns do hello quando você configurar o suporte do Exchange ActiveSync para autenticação de passagem.

### <a name="exchange-powershell-issue"></a>Problema do Exchange PowerShell

Se você vir hello "**um parâmetro não pode ser encontrado que coincida com o nome de parâmetro 'PerTenantSwitchToESTSEnabled'\.**" Erro ao executar Olá `Set-OrganizationConfig` PowerShell do Exchange command, entre em contato com o Microsoft Support.

### <a name="exchange-activesync-not-working"></a>O Exchange ActiveSync não está funcionando

configuração de saudação em vigor algum tempo tootake - Olá período de tempo depende do ambiente. Se a situação Olá persistir por um longo tempo, entre em contato com o Microsoft Support.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Coletar logs do Agente de Autenticação de Passagem

Dependendo do tipo de saudação do problema, que talvez seja necessário, você precisa toolook em locais diferentes para logs de agente de autenticação de passagem.

### <a name="authentication-agent-event-logs"></a>Logs de eventos do Agente de Autenticação

Para erros relacionados a toohello agente de autenticação, abra a saudação aplicativo de Visualizador de eventos no servidor de saudação e verifique em **aplicativo e serviço Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Para análises detalhadas, habilite o log de "Sessão" hello. Não execute Olá agente de autenticação com esse log habilitado durante operações normais; Use somente para solução de problemas. conteúdo do log Olá é visível apenas depois que o log de saudação é desabilitado novamente.

### <a name="detailed-trace-logs"></a>Logs de rastreamento detalhados

tootroubleshoot usuário falhas de entrada, procure logs de rastreamento em **%programdata%\Microsoft\Azure AD conectar-se a autenticação Agent\Trace\\**. Os logs incluem motivos por que um usuário específico falha ao entrar usando o recurso de autenticação de passagem de saudação. Esses erros também são motivos de falha no logon mapeado toohello mostrados a saudação anterior [tabela](#sign-in-failure-reasons-on-the-Azure-portal). A seguir está um exemplo de entrada de log:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Você pode obter descritivos detalhes do erro de saudação ('1328' hello anterior exemplo), abra o prompt de comando hello e Olá executando comandos a seguir (Observação: substitua '1328' número de erro real Olá que você vê em seus logs):

`Net helpmsg 1328`

![Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Logs do controlador de domínio

Se o log de auditoria estiver habilitado, informações adicionais podem ser encontradas nos logs de segurança Olá controladores de domínio. Uma maneira simples tooquery solicitações de entrada enviadas pelos agentes de autenticação de passagem é o seguinte:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Contadores do Monitor de Desempenho

Outra maneira toomonitor agentes de autenticação é tootrack contadores de desempenho específicos em cada servidor onde Olá Authentication Agent está instalado. Olá Use contadores globais a seguir (**autenticações # PTA**, **#PTA falha autenticações** e **autenticações bem-sucedidas #PTA**) e contadores de erros (**Erros de autenticação # PTA**):

![Contadores do Monitor de Desempenho de Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>A Autenticação de Passagem fornece alta disponibilidade usando vários Agentes de Autenticação e _não_ o balanceamento de carga. Dependendo da configuração, _nem_ todos os seus Agentes de Autenticação receberão um número de solicitações aproximadamente _igual_. É possível que um Agente de Autenticação específico não receba nenhum tráfego.
