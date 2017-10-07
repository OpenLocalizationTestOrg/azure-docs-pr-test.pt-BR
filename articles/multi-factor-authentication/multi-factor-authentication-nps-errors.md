---
title: "códigos de erro de aaaTroubleshoot de saudação extensão do Azure MFA NPS | Microsoft Docs"
description: "Obter ajuda para resolver problemas com hello extensão NPS para o Azure multi-Factor Authentication com resoluções específicas para mensagens de erro comuns"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Resolver mensagens de erro de saudação extensão NPS para o Azure multi-Factor Authentication

Se você encontrar erros com hello extensão NPS para o Azure multi-Factor Authentication, use tooreach este artigo uma resolução mais rápida. 

## <a name="troubleshooting-steps-for-common-errors"></a>Etapas de solução de problemas para erros comuns

| Código do erro | Etapas para solucionar problemas |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Entre em contato com o suporte](#contact-microsoft-support)e mencione a lista de saudação de etapas para coletar logs. Forneça as informações sobre o que aconteceu antes do erro hello, incluindo a id de locatário e o nome de usuário principal (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Pode haver um problema com como certificado de saudação do cliente foi instalado ou associado ao seu locatário. Siga as instruções de saudação em [Olá de solução de problemas extensão MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate problemas de certificado de cliente. |
| **ESTS_TOKEN_ERROR** | Siga as instruções de saudação em [Olá de solução de problemas extensão MFA NPS](multi-factor-authentication-nps-extension.md#troubleshooting) problemas de token de certificado de cliente tooinvestigate e ADAL. |
| **HTTPS_COMMUNICATION_ERROR** | servidor NPS Olá é tooreceive não é possível respostas do Azure MFA. Verifique se os firewalls estão aberta bidirecionalmente para tráfego tooand de https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | No servidor de saudação que executa a extensão NPS hello, verifique se que você possa acessar https://adnotifications.windowsazure.com e https://login.microsoftonline.com/. Se os sites não forem carregados, resolva os problemas de conectividade no servidor. |
| **REGISTRY_CONFIG_ERROR** | Uma chave está ausente no registro Olá para o aplicativo hello, que pode ser porque Olá [script do PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) não foi executado após a instalação. mensagem de saudação do erro deve incluir a chave ausente hello. Certifique-se de que ter chave Olá HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa. |
| **REQUEST_FORMAT_ERROR** <br> Solicitação do RADIUS ausente. Atributo userName\Identifier obrigatório do RADIUS. Verifique se o NPS está recebendo as solicitações RADIUS | Esse erro geralmente reflete um problema de instalação. Olá extensão NPS deve ser instalado em servidores NPS que podem receber solicitações RADIUS. Servidores NPS que são instalados como dependências para serviços como RDG e RRAS não recebem solicitações RADIUS. Extensão de NPS não funciona quando instalados por tais instalações e os erros de saída desde que ele não é possível ler detalhes de saudação da solicitação de autenticação de saudação. |
| **REQUEST_MISSING_CODE** | Certifique-se de que o protocolo de criptografia de senha de saudação entre hello NPS e servidores NAS dá suporte ao método de autenticação secundário Olá que você está usando. **PAP** oferece suporte a todos os métodos de autenticação de saudação do Azure MFA na nuvem Olá: chamada telefônica, mensagem de texto unidirecional, notificação de aplicativo móvel e código de verificação de aplicativo móvel. **CHAPV2** e **EAP** dão suporte a chamada telefônica e notificação de aplicativo móvel. |
| **USERNAME_CANONICALIZATION_ERROR** | Verificar se o usuário hello está presente na instância do Active Directory local e esse serviço de NPS Olá tem o diretório de saudação do tooaccess de permissões. Se estiver usando relações de confiança entre florestas, [contate o suporte](#contact-microsoft-support) para obter mais ajuda. |


   

### <a name="alternate-login-id-errors"></a>Erros de ID de logon alternativo

| Código do erro | Mensagem de erro | Etapas para solucionar problemas |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Erro: falha na pesquisa do userObjectSid | Verifique se que esse usuário Olá existe na instância do Active Directory local. Se estiver usando relações de confiança entre florestas, [contate o suporte](#contact-microsoft-support) para obter mais ajuda. |
| **ALTERNATE_LOGIN_ID_ERROR** | Erro: falha de pesquisa de LoginId alternativo | Verifique se LDAP_ALTERNATE_LOGINID_ATTRIBUTE está definida tooa [atributo válido do active directory](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Se LDAP_FORCE_GLOBAL_CATALOG for definido tooTrue ou LDAP_LOOKUP_FORESTS é configurado com um valor não vazio, verifique se você tiver configurado um Catálogo Global e atributo AlternateLoginId Olá é adicionado tooit. <br><br> Se LDAP_LOOKUP_FORESTS estiver configurado com um valor não vazio, verifique se que Olá valor está correto. Se houver mais de um nome de floresta, os nomes de saudação devem ser separados por ponto e vírgula, não espaços. <br><br> Se essas etapas não corrigir o problema de hello, [entre em contato com o suporte](#contact-microsoft-support) para obter mais ajuda. |
| **ALTERNATE_LOGIN_ID_ERROR** | Erro: o valor de LoginId alternativo está vazio | Verifique se o que atributo AlternateLoginId hello está configurado para o usuário hello. |


## <a name="errors-your-users-may-encounter"></a>Erros que os usuários podem ver

| Código do erro | Mensagem de erro | Etapas para solucionar problemas |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Locatário do chamador não tem a autenticação de toodo de permissões de acesso de usuário de Olá | Verifique se hello domínio de locatário e domínio Olá Olá nome de usuário principal (UPN) são Olá mesmo. Por exemplo, certifique-se de que user@contoso.com está tentando tooauthenticate toohello Contoso locatário. Olá UPN representa um usuário válido para o locatário Olá no Azure. |
| **AuthenticationMethodNotConfigured** | Olá especificado o método de autenticação não foi configurado para o usuário Olá | Tem usuário Olá adicionar ou verificar seus métodos de verificação de acordo com as instruções de toohello em [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Não há suporte para o método de autenticação especificado. | Colete todos os logs que incluem esse erro e [contate o suporte](#contact-microsoft-support). Quando você contatar o suporte, forneça o nome de saudação de método de verificação secundária hello que disparou o erro de saudação. |
| **BecAccessDenied** | MSODS Bec chamada retornou um acesso negado, provavelmente Olá username não está definida no locatário Olá | usuário Hello está presente no local do Active Directory, mas não está sincronizado no Azure AD pelo AD Connect. Ou então, usuário hello está ausente para o locatário hello. Adicionar Olá usuário tooAzure AD e tê-los a adicionar seus métodos de verificação de acordo com instruções toohello [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** ou **StrongAuthenticationServiceInvalidParameter** | número de telefone Hello está em um formato irreconhecível | Tem usuário Olá corrigir os números de telefone de verificação. |
| **InvalidSession** | Olá especificado sessão é inválida ou ter expirado | sessão Olá demorou mais do que três minutos toocomplete. Verifique se esse usuário Olá é inserir o código de verificação de saudação ou responder a notificação do aplicativo toohello, dentro de três minutos de iniciar a solicitação de autenticação de saudação. Se isso não resolver o problema de saudação, verifique se não há nenhum latências de rede entre o cliente, o servidor NAS, o servidor NPS e o ponto de extremidade do hello Azure MFA.  |
| **NoDefaultAuthenticationMethodIsConfigured** | Nenhum método de autenticação padrão foi configurado para o usuário Olá | Tem usuário Olá adicionar ou verificar seus métodos de verificação de acordo com as instruções de toohello em [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md). Verifique se esse usuário Olá tem escolher um método de autenticação padrão e configurado esse método para sua conta. |
| **OathCodePinIncorrect** | Código e PIN incorretos inseridos. | Esse erro não é esperado no hello extensão do NPS. Se o usuário ver esse erro, [contate o suporte](#contact-microsoft-support) para obter ajuda na solução de problemas. |
| **ProofDataNotFound** | Dados de prova não foi configurados para Olá especificado método de autenticação. | Tem usuário Olá tente um método de verificação diferente ou adicione um novos métodos de verificação de acordo com as instruções de toohello em [gerenciar as configurações de verificação em duas etapas](./end-user/multi-factor-authentication-end-user-manage-settings.md). Se o usuário Olá continua toosee esse erro depois de confirmar que o seu método de verificação está configurado corretamente, [entre em contato com o suporte](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Código e PIN incorretos inseridos. (OneWaySMS) | Esse erro não é esperado no hello extensão do NPS. Se o usuário ver esse erro, [contate o suporte](#contact-microsoft-support) para obter ajuda na solução de problemas. |
| **TenantIsBlocked** | O locatário está bloqueado | [Entre em contato com o suporte](#contact-microsoft-support) com a ID de diretório na página de propriedades de saudação do AD do Azure no portal do Azure de saudação. |
| **UserNotFound** | usuário de saudação especificado não foi encontrado | locatário Olá não está mais visível como ativo no AD do Azure. Verifique se a sua assinatura está ativa e você tem Olá necessário primeiro aplicativos de terceiros. Verifique também se locatário Olá na entidade do certificado de saudação é conforme o esperado e cert Olá ainda está válido e registrado em entidade de serviço hello. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Mensagens que os usuários podem ver que não são erros

Às vezes, os usuários podem receber mensagens da Autenticação Multifator, pois sua solicitação de autenticação falhou. Eles não são erros no produto Olá da configuração, mas são avisos intencionais explicando por que uma solicitação de autenticação foi negada.

| Código do erro | Mensagem de erro | Etapas recomendadas | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Código incorreto inserido\Código OATH incorreto | Não é um erro; o usuário inseriu o código incorreto. | usuário de Olá inseriu o código errado Olá. Solicite a ele para que repita a solicitação de um novo código ou entre novamente. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Repetição de código máxima permitida atingida | usuário Olá falha no desafio de verificação de saudação muitas vezes. Dependendo de suas configurações, talvez seja necessário toobe desbloqueado por um administrador agora.  |
| **SMSAuthFailedWrongCodeEntered** | Código incorreto inserido/OTP da mensagem de texto incorreto | usuário de Olá inseriu o código errado Olá. Solicite a ele para que repita a solicitação de um novo código ou entre novamente. |

## <a name="errors-that-require-support"></a>Erros que exigem suporte

Se você encontrar um desses erros, recomendamos que [contate o suporte](#contact-microsoft-support) para obter ajuda de diagnóstico. Não há nenhum conjunto padrão de etapas que pode corrigir esses erros. Quando você contatar o suporte, tooinclude-se como a quantidade de informações possível sobre etapas de saudação que levaram tooan erro e suas informações de locatário.

| Código do erro | Mensagem de erro |
| ---------- | ------------- |
| **InvalidParameter** | A solicitação não pode ser nula |
| **InvalidParameter** | A ObjectId não deve ser nula nem vazia para ReplicationScope:{0} |
| **InvalidParameter** | Olá comprimento de CompanyName \{0} \ é maior do que o comprimento máximo permitido de saudação \\{1 \\} |
| **InvalidParameter** | O UserPrincipalName não deve ser nulo nem vazio |
| **InvalidParameter** | Olá fornecido que tenantid não está no formato correto |
| **InvalidParameter** | A SessionId não deve ser nula nem vazia |
| **InvalidParameter** | Não foi possível resolver nenhum ProofData da solicitação ou do Msods. Olá ProofData é desconhecido |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Próximas etapas

### <a name="troubleshoot-user-accounts"></a>Solução de problemas de contas de usuário

Se os usuários estiverem [tendo problemas com a verificação em duas etapas](./end-user/multi-factor-authentication-end-user-troubleshoot.md), ajude-os a diagnosticar os problemas por conta própria. 

### <a name="contact-microsoft-support"></a>Contatar Suporte da Microsoft

Caso você precise de mais ajuda, contate um profissional de suporte por meio do [suporte do Servidor de Autenticação Multifator do Azure](https://support.microsoft.com/oas/default.aspx?prid=14947). Ao entrar em contato conosco, é útil incluir o máximo possível de informações sobre o problema. Informações que você pode fornecer incluem página Olá onde você viu o erro de saudação, Olá erro específico código, ID de sessão específica hello, Olá ID de usuário de saudação que viu o erro hello e logs de depuração.

toocollect logs de depuração para o diagnóstico de suporte, use Olá etapas a seguir: 

1. Abra um prompt de comando do Administrador e execute estes comandos:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Reproduza o problema de saudação

3. Pare rastreamento Olá com estes comandos:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Compacte o conteúdo de saudação da pasta C:\NPS hello e anexe o caso de suporte de toohello de arquivo hello compactado.


