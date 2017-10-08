---
title: 'Azure AD Connect: solucionar problemas de conectividade | Microsoft Docs'
description: Explica como os problemas de conectividade da tootroubleshoot ao Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Solucionar problemas de conectividade com o Azure AD Connect
Este artigo explica como funciona a conectividade entre o Azure AD Connect e AD do Azure e como os problemas de conectividade da tootroubleshoot. Esses problemas são provavelmente toobe visto em um ambiente com um servidor proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Solucionar problemas de conectividade no Assistente de instalação de saudação
Conexão do AD do Azure está usando autenticação moderna (usando a biblioteca ADAL Olá) para autenticação. Assistente de instalação Hello e mecanismo de sincronização de saudação adequado exigem toobe Machine. config configurado corretamente uma vez que esses dois são aplicativos .NET.

Neste artigo, mostramos como a Fabrikam se conecta tooAzure AD por meio de seu proxy. servidor de proxy Olá chamado fabrikamproxy e está usando a porta 8080.

Primeiro é preciso toomake se [ **Machine. config** ](active-directory-aadconnect-prerequisites.md#connectivity) está configurado corretamente.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> Em alguns blogs não Microsoft, ele está documentado que as alterações devem ser feitas toomiiserver.exe.config em vez disso. No entanto, esse arquivo será substituído em cada atualização até mesmo se ele funciona durante a instalação inicial, sistema Olá deixará de funcionar na primeira atualização. Por esse motivo, a recomendação de saudação é tooupdate Machine. config em vez disso.
>
>

servidor de proxy Olá também deve ter URLs Olá necessário abertos. lista oficial Hello está documentada em [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

As URLs, Olá a tabela a seguir é Olá absoluto toobe mínimo bare capaz de tooconnect tooAzure AD. Essa lista não inclui quaisquer recursos opcionais, como write-back de senha ou Azure AD Connect Health. É documentado toohelp aqui na solução de problemas de configuração inicial de saudação.

| URL | Port | Descrição |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Lista de usados toodownload CRL. |
| \*.verisign.com |HTTP/80 |Lista de usados toodownload CRL. |
| \*.entrust.com |HTTP/80 |Lista de CRL toodownload usado para MFA. |
| \*.windows.net |HTTPS/443 |Toosign usado em tooAzure AD. |
| Secure.aadcdn.microsoftonline p.com |HTTPS/443 |Usado para MFA. |
| \*.microsoftonline.com |HTTPS/443 |Usado tooconfigure seus dados de diretório e de importação/exportação do AD do Azure. |

## <a name="errors-in-hello-wizard"></a>Erros no Assistente de saudação
Assistente de instalação Hello está usando dois contextos de segurança diferente. Na página de saudação **conectar tooAzure AD**, utiliza Olá usuário conectado no momento. Na página de saudação **configurar**, ele está sendo alterado toohello [conta que está executando o serviço Olá para o mecanismo de sincronização Olá](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Se houver um problema, ele aparece provavelmente já no hello **conectar tooAzure AD** página no Assistente de saudação desde que a configuração de proxy de saudação é global.

Olá problemas a seguir é erros mais comuns de Olá encontrados no Assistente de instalação de saudação.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>Assistente de instalação de saudação não foi configurado corretamente
Este erro aparece quando o Assistente de saudação em si não pode acessar o proxy de saudação.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Se você vir esse erro, verifique se Olá [Machine. config](active-directory-aadconnect-prerequisites.md#connectivity) foi configurado corretamente.
* Se que parece correto, execute as etapas de saudação em [verificar a conectividade de proxy](#verify-proxy-connectivity) toosee se houver problema Olá fora Olá assistente também.

### <a name="a-microsoft-account-is-used"></a>Uma conta da Microsoft é usada
Se você usar uma **conta da Microsoft** em vez de uma conta **corporativa ou de estudante**, você verá um erro genérico.  
![Uma conta da Microsoft é usada](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>não é possível alcançar o ponto de extremidade MFA de saudação
Este erro ocorrerá se hello ponto de extremidade **https://secure.aadcdn.microsoftonline-p.com** não pode ser alcançado e o administrador global tem MFA habilitado.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Se você vir esse erro, verifique se esse ponto de extremidade Olá **secure.aadcdn.microsoftonline p.com** toohello proxy foi adicionado.

### <a name="hello-password-cannot-be-verified"></a>Olá senha não pode ser verificada
Não é possível verificar se o Assistente de instalação Olá for bem-sucedida na conexão tooAzure AD, mas a própria senha Olá que você vir esse erro:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* É a senha de saudação uma senha temporária e deve ser alterada? É-Olá, na verdade, a senha correta? Tente toosign em toohttps://login.microsoftonline.com (em outro computador servidor do Azure AD Connect Olá) e verifique a conta Olá é utilizável.

### <a name="verify-proxy-connectivity"></a>Verificar a conectividade do proxy
tooverify se hello, servidor do Azure AD Connect tem conectividade real com hello Proxy e a Internet, use algumas toosee PowerShell se proxy hello está permitindo solicitações da web ou não. Em um prompt do PowerShell, execute `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Tecnicamente hello primeira chamada é toohttps://login.microsoftonline.com e esse URI também funciona, mas outros URI hello é toorespond mais rápido.)

PowerShell usa configuração Olá no proxy de saudação toocontact Machine. config. configurações de saudação no netsh/winhttp não devem afetar esses cmdlets.

Se o proxy hello está configurado corretamente, você deve obter um status de êxito: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Se você receber **servidor remoto do não é possível tooconnect toohello**, PowerShell está tentando toomake uma chamada direta sem usar proxy hello ou DNS não está configurado corretamente. Verifique se Olá **Machine. config** arquivo está configurado corretamente.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Se o proxy de saudação não está configurado corretamente, você obterá um erro: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Erro | Texto do erro | Comentário |
| --- | --- | --- |
| 403 |Proibido |proxy de saudação não foi aberto para Olá solicitado URL. Verificar configuração de proxy de saudação e verifique se Olá [URLs](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) foram abertos. |
| 407 |Autenticação de proxy necessária |servidor de proxy Olá necessária uma entrada e nenhum foi fornecido. Se o servidor proxy requer autenticação, verifique se toohave essa configuração definida em Machine. config de saudação. Verifique também se que você estiver usando contas de domínio para o usuário Olá executando o Assistente de saudação e Olá conta de serviço. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>padrão de comunicação de saudação entre o Azure AD Connect e AD do Azure
Se você executou todas essas etapas anteriores e ainda não conseguiu se conectar, comece a examinar os logs de rede. Esta seção está documentando um padrão de conectividade normal e bem-sucedido. Ele também é listando herrings vermelho comuns que podem ser ignorados durante a leitura de logs de saudação de rede.

* Há chamadas toohttps://dc.services.visualstudio.com. Não é necessário toohave que essa URL aberto no proxy Olá Olá instalação toosucceed e essas chamadas pode ser ignorado.
* Consulte a resolução de dns lista toobe de hosts real Olá Olá nsatc.net de espaço de nome DNS e outros namespaces não em microsoftonline.com. No entanto, não há quaisquer solicitações de serviço da web em nomes de servidor real hello e você não tem tooadd proxy de toohello essas URLs.
* provisioningapi e adminwebservice de pontos de extremidade de saudação são pontos de extremidade de descoberta e usadas toofind Olá real do ponto de extremidade toouse. Esses pontos de extremidade são diferentes dependendo de sua região.

### <a name="reference-proxy-logs"></a>Logs de proxy de referência
Aqui está um despejo de um proxy real log e hello página Assistente de instalação de onde ele foi feito (toohello entradas duplicadas foram removidas mesmo ponto de extremidade). Esta seção pode ser usada como referência para seus próprios logs de proxy e de rede. pontos de extremidade de saudação real podem ser diferentes em seu ambiente (em particular as URLs em *itálico*).

**Conecte-se tooAzure AD**

| Hora | URL |
| --- | --- |
| 11/01/2016 08:31 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:31 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 08:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 08:32 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:33 |connect://provisioningapi.microsoftonline.com:443 |
| 11/01/2016 08:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Configurar**

| Hora | URL |
| --- | --- |
| 11/01/2016 08:43 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 08:43 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 08:44 |connect://login.microsoftonline.com:443 |
| 11/01/2016 08:46 |connect://provisioningapi.microsoftonline.com:443 |
| 11/01/2016 08:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Sincronização inicial**

| Hora | URL |
| --- | --- |
| 11/01/2016 08:48 |connect://login.windows.net:443 |
| 11/01/2016 08:49 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 08:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/01/2016 08:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Erros de autenticação
Esta seção aborda os erros que podem ser retornados do ADAL (biblioteca de autenticação Olá usada pelo Azure AD Connect) e do PowerShell. Erro de saudação explicado deve ajudá-lo na entender as próximas etapas.

### <a name="invalid-grant"></a>Concessão Inválida
Senha ou nome de usuário inválido. Para obter mais informações, consulte [Olá senha não pode ser verificada](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Tipo de usuário desconhecido
O seu diretório do Azure AD não pode ser encontrado ou resolvido. Talvez você tentar toologin com um nome de usuário em um domínio não verificado?

### <a name="user-realm-discovery-failed"></a>Falha na descoberta do realm de usuário
Problemas de configuração de rede ou proxy. rede de saudação não pode ser alcançado. Consulte [solucionar problemas de conectividade no Assistente de instalação Olá](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>A senha do usuário expirou
Suas credenciais expiraram. Altere a sua senha.

### <a name="authorizationfailure"></a>AuthorizationFailure
Problema desconhecido.

### <a name="authentication-cancelled"></a>Autenticação cancelada
desafio de autenticação multifator (MFA) Olá foi cancelado.

### <a name="connecttomsonline"></a>ConnectToMSOnline
A autenticação foi bem-sucedida, mas o PowerShell do Azure AD tem um problema de autenticação.

### <a name="azurerolemissing"></a>AzureRoleMissing
A autenticação foi bem-sucedida. Você não é um administrador global.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
A autenticação foi bem-sucedida. O gerenciamento de identidades com privilégios foi habilitado e atualmente você não é um administrador global. Para saber mais, confira [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
A autenticação foi bem-sucedida. Não foi possível recuperar as informações da empresa do Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
A autenticação foi bem-sucedida. Não foi possível recuperar informações de domínio do Azure AD.

### <a name="unexpected-exception"></a>Exceção inesperada
Mostrado como um erro inesperado no Assistente de instalação de saudação. Pode ocorrer se você tentar toouse um **Microsoft Account** em vez de **conta de escola ou organização**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Etapas para solucionar problemas de versões anteriores.
Com versões começando pelo número de compilação 1.1.105.0 (lançado em fevereiro de 2016), o Assistente de entrada hello foi desativado. Essa configuração de seção e hello deixam de ser necessária, mas é mantida como referência.

Para Olá logon único no assistente toowork, winhttp deve ser configurado. Essa configuração pode ser feita com [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Assistente de entrada Hello não foi configurado corretamente
Esse erro aparece quando o Assistente de entrada hello não pode acessar o proxy de saudação ou proxy Olá não está permitindo que a solicitação de saudação.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Se você vir esse erro, examine a configuração de proxy de saudação em [netsh](active-directory-aadconnect-prerequisites.md#connectivity) e verifique se ela está correta.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Se que parece correto, execute as etapas de saudação em [verificar a conectividade de proxy](#verify-proxy-connectivity) toosee se houver problema Olá fora Olá assistente também.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
