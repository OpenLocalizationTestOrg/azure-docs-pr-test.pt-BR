---
title: "Portas e protocolos exigidos para Identidade Híbrida- Azure | Microsoft Docs"
description: "Essa página é uma página de referência técnica para as portas que são necessário toobe aberto para conexão do AD do Azure"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>Portas e Protocolos Requeridos para Identidade Híbrida
Olá documento a seguir é uma referência técnica em portas Olá necessárias e protocolos para implementar uma solução de identidade híbrida. Use Olá ilustração a seguir e consulte a tabela de toohello correspondente.

![O que é o Azure AD Connect](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Tabela 1 - AD do Azure Connect e AD Local
Esta tabela descreve Olá portas e protocolos são necessários para a comunicação entre o servidor do Azure AD Connect hello e AD local.

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |Pesquisas de DNS na floresta de destino hello. |
| Kerberos |88 (TCP/UDP) |Floresta de toohello AD de autenticação Kerberos. |
| MS-RPC |135 (TCP/UDP) |Usado durante a configuração inicial do Assistente de conexão do AD do Azure hello quando ele é ligado toohello AD floresta hello e também durante a sincronização de senha. |
| LDAP |389 (TCP/UDP) |Usado para importar dados do AD. Dados são criptografados com Sinal e Selo do Kerberos. |
| RPC | 445 (TCP/UDP) |Usado por toocreate de SSO contínuo uma conta de computador na floresta do AD de saudação. |
| LDAP/SSL |636 (TCP/UDP) |Usado para importar dados do AD. transferência de dados de saudação foi assinada e criptografada. Usado somente se você estiver usando SSL. |
| RPC |49152- 65535 (Porta RPC alta aleatória)(TCP/UDP) |Usado durante a configuração inicial do Azure AD Connect quando ele é ligado toohello AD florestas hello e durante a sincronização de senha. Confira os artigos [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017) e [KB224196](https://support.microsoft.com/kb/224196) para saber mais. |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Tabela 2 - AD do Azure Connect e Azure AD
Esta tabela descreve Olá portas e protocolos são necessários para a comunicação entre o servidor do Azure AD Connect hello e o Azure AD.

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Usado certificados SSL em tooverify toodownload CRLs (listas de certificados revogados). |
| HTTPS |443(TCP/UDP) |Toosynchronize usado com o Azure AD. |

Para obter uma lista de URLs e IP endereços necessário tooopen em seu firewall, consulte [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Tabela 3 – Azure AD Connect e Servidores de Federação AD FS/WAP
Esta tabela descreve Olá portas e protocolos são necessários para a comunicação entre o servidor do Azure AD Connect hello e servidores de Federação/WAP do AD FS.  

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Usado certificados SSL em tooverify toodownload CRLs (listas de certificados revogados). |
| HTTPS |443(TCP/UDP) |Toosynchronize usado com o Azure AD. |
| WinRM |5985 |Ouvinte do WinRM |

## <a name="table-4---wap-and-federation-servers"></a>Tabela 4 - Servidores de Federação e WAP
Esta tabela descreve Olá portas e protocolos são necessários para a comunicação entre servidores de Federação hello e WAP.

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Usado para autenticação. |

## <a name="table-5---wap-and-users"></a>Tabela 5 - WAP e Usuários
Esta tabela descreve Olá portas e protocolos são necessários para a comunicação entre usuários e servidores WAP hello.

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Usado para autenticação de dispositivo. |
| TCP |49443 (TCP) |Usado para autenticação de certificado. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Tabela 6a e 6b - Autenticação de passagem com SSO (logon único) e Sincronização de hash de senha com SSO (logon único)
Olá tabelas a seguir descreve Olá portas e protocolos são necessários para a comunicação entre hello Azure AD Connect e AD do Azure.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Tabela 6a - Autenticação de passagem com SSO
|Protocolo|Número da porta|Descrição
| --- | --- | ---
|HTTP|80|Habilite o tráfego HTTP de saída para a validação de segurança como o SSL. Também necessário para o conector de saudação atualização automática recurso toofunction corretamente.
|HTTPS|443| Habilite o tráfego HTTPS de saída para operações como a habilitação e desabilitação do recurso de saudação, registrando conectores, baixar atualizações do conector e tratamento de solicitações de entrada do usuário todos os.

Além disso, o Azure AD Connect precisa toobe toomake capaz direto IP conexões toohello [Datacenter do Azure intervalos IP](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Tabela 6b - Sincronização de hash de senha com SSO

|Protocolo|Número da porta|Descrição
| --- | --- | ---
|HTTPS|443| Habilite o registro SSO (necessário somente para o processo de registro SSO de saudação).

Além disso, o Azure AD Connect precisa toobe toomake capaz direto IP conexões toohello [Datacenter do Azure intervalos IP](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Novamente, isso só é necessário para o processo de registro SSO hello.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabela 7a e 7b – Agente do Azure AD Connect Health para (AD FS/Sync) e Azure AD
Olá tabelas a seguir descrevem os pontos de extremidade hello, portas e protocolos que são necessários para a comunicação entre agentes de integridade de conexão do AD do Azure e o Azure AD

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabela 7a – Portas e protocolos para o agente do Azure AD Connect Health para o (AD FS/Sync) e Azure AD
Esta tabela descreve Olá protocolos que são necessários para a comunicação entre agentes de integridade de conexão de saudação do AD do Azure e o Azure AD e portas de saída a seguir.  

| Protocolo | Portas | Descrição |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Saída |
| Barramento de Serviço do Azure |5671 (TCP/UDP) |Saída |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7b – Pontos de extremidade de agente do Azure AD Connect Health para (AD FS/Sync) e Azure AD
Para obter uma lista de pontos de extremidade, consulte [Olá seção de requisitos para o agente de integridade de conexão de saudação do AD do Azure](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

