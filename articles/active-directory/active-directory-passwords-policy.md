---
title: "Política: SSPR do Azure AD | Microsoft Docs"
description: "Opções de política de autoatendimento de redefinição de senha do Azure AD"
services: active-directory
keywords: "Gerenciamento de senha do Active Directory, gerenciamento de senha, autoatendimento de redefinição de senha do Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Políticas e restrições de senha do Active Directory do Azure

Este artigo descreve as políticas de senha hello e requisitos de complexidade associados a contas de usuário armazenadas em seu locatário do AD do Azure.

## <a name="administrator-password-policy-differences"></a>Diferenças de política de senha do administrador

A Microsoft impõe uma política padrão rígida de redefinição de senha de **duas entradas** para qualquer função de administrador do Azure (exemplo: Administrador Global, Administrador de Assistência Técnica, Administrador de Senha etc.)

Isso desativa os administradores usem as perguntas de segurança e impõe a seguir hello.

Dois portão política, que exige duas partes de dados de autenticação (endereço de email **e** número de telefone), Olá circunstâncias a seguir se aplica

* Todas as funções de administrador do Azure
  * Administrador de assistência técnica
  * Administrador de suporte a serviço
  * Administrador de cobrança
  * Suporte de camada 1 do parceiro
  * Suporte de camada 2 do parceiro
  * Administrador de serviços do Exchange
  * Administrador de serviços do Lync
  * Administrador da conta de usuário
  * Gravadores de diretório
  * Administrador de empresa/administrador global
  * Administrador de serviços do SharePoint
  * Administrador de conformidade
  * Administrador de aplicativos
  * Administrador de segurança
  * Administrador de função com privilégios
  * Administrador de serviços do Intune
  * Administrador de serviços de Proxy de Aplicativo
  * Administrador de serviços do CRM
  * Administrador de serviços do Power BI
  
* Trinta dias decorridos de uma avaliação **OU**
* O domínio personalizado está presente (contoso.com) **OU**
* O Azure AD Connect está sincronizando identidades do seu diretório local

### <a name="exceptions"></a>Exceções
Política de uma porta que exigem uma parte dos dados de autenticação (endereço de email **ou** número de telefone), Olá circunstâncias a seguir se aplica

* Primeiros 30 dias de uma avaliação **OU**
* O domínio personalizado não está presente (*.onmicrosoft.com) **E** o Azure AD Connect não está sincronizando identidades


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Políticas UserPrincipalName que se aplicam a contas de usuário tooall

Cada conta de usuário que precisa toosign em tooAzure AD deve ter um valor de atributo de nome principal (UPN) do usuário exclusiva associado à sua conta. tabela de saudação abaixo descreve Olá políticas que se aplicam a tooboth local contas de usuário do Active Directory sincronizado toohello nuvem e contas de usuário somente toocloud.

| Propriedade | Requisitos de UserPrincipalName |
| --- | --- |
| Caracteres permitidos |<ul> <li>A – Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Caracteres não permitidos |<ul> <li>Qualquer ' @' caractere que não é separando o nome de usuário de saudação do domínio hello.</li> <li>Não pode conter um caractere ponto '.' hello imediatamente anterior ' @' símbolo</li></ul> |
| Restrições de comprimento |<ul> <li>O comprimento total não deve exceder 113 caracteres</li><li>64 caracteres antes de saudação ' @' símbolo</li><li>48 caracteres depois de saudação ' @' símbolo</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Políticas de senha que se aplicam somente a contas de usuário toocloud

Olá, a tabela a seguir descreve configurações de política de senha disponíveis Olá que podem ser aplicadas toouser contas são criadas e gerenciadas no AD do Azure.

| Propriedade | Requisitos |
| --- | --- |
| Caracteres permitidos |<ul><li>A – Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Caracteres não permitidos |<ul><li>Caracteres Unicode</li><li>Espaços</li><li> **Senhas fortes apenas**: não pode conter um caractere de ponto '.' hello imediatamente anterior ' @' símbolo</li></ul> |
| Restrições de senha |<ul><li>Mínimo de 8 caracteres e no máximo 16 caracteres</li><li>**Senhas fortes apenas**: requer 3 de 4 dos seguintes hello:<ul><li>Caracteres minúsculos</li><li>Caracteres maiúsculos</li><li>Números (0-9)</li><li>Símbolos (veja as restrições de senha acima)</li></ul></li></ul> |
| Tempo de expiração da senha |<ul><li>Valor padrão: **90** dias </li><li>Valor é configurável usando o cmdlet Set-MsolPasswordPolicy de saudação do hello Azure módulo Active Directory para Windows PowerShell.</li></ul> |
| Notificação de expiração de senha |<ul><li>Valor padrão: **14** dias (antes do vencimento de senha)</li><li>Valor é configurável usando o cmdlet Set-MsolPasswordPolicy do hello.</li></ul> |
| Expiração de senha |<ul><li>Valor padrão: **false** dias (indica que a expiração de senha está habilitada) </li><li>Valor pode ser configurado para contas de usuário individuais usando o cmdlet Set-MsolUser de saudação. </li></ul> |
| Histórico de **alteração** de senha |A última senha **não pode** ser usada novamente ao **alterar** uma senha. |
| Histórico de **redefinição** de senha | A última senha **pode** ser usada novamente ao **redefinir** uma senha esquecida. |
| Bloqueio de conta |Após 10 tentativas malsucedidas de entrada (senha incorreta), usuário Olá será bloqueado por um minuto. Tentativas adicionais de entrada incorreta bloqueio usuário Olá para aumentar a duração. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Definir políticas de expiração de senha no Active Directory do Azure

Um administrador global para um serviço de nuvem da Microsoft pode usar tooset de módulo do Microsoft Azure Active Directory para Windows PowerShell Olá as senhas de usuário não tooexpire. Você também pode usar o Windows PowerShell cmdlets tooremove Olá nunca expira configuração ou toosee quais senhas de usuário são configuradas não tooexpire. Este guia se aplica a provedores de tooother, como o Microsoft Intune e Office 365, que também dependem do Active Directory do Microsoft Azure para serviços de identidade e diretório.

> [!NOTE]
> Senhas apenas para contas de usuário que não estão sincronizadas por meio da sincronização de diretório podem ser configuradas toonot expirar. Para saber mais sobre a sincronização de diretório, confira [Conectar AD ao Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Definir ou verificar políticas de senha usando o PowerShell

tooget iniciado, é necessário muito[baixar e instalar o módulo do PowerShell do Azure AD Olá](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Depois de instalado, você pode seguir etapas Olá abaixo tooconfigure cada campo.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Como toocheck a política de expiração de senha
1. Conecte-se tooWindows PowerShell usando suas credenciais de administrador da empresa.
2. Execute uma saudação comandos a seguir:

   * toosee se a senha de um único usuário está configurada toonever expirar, execute Olá cmdlet a seguir usando o nome principal de usuário de saudação (UPN) (por exemplo, aprilr@contoso.onmicrosoft.com) ou Olá ID de usuário do usuário Olá deseja toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee hello "Senha nunca expira" configuração para todos os usuários, execute Olá cmdlet a seguir:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Defina uma senha tooexpire

1. Conecte-se tooWindows PowerShell usando suas credenciais de administrador da empresa.
2. Execute uma saudação comandos a seguir:

   * senha de saudação tooset de um usuário para hello senha expirar, execute Olá cmdlet a seguir usando o nome principal de usuário de saudação (UPN) ou Olá ID do usuário hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * senhas de saudação tooset de todos os usuários na organização Olá para que elas expirem, usam Olá cmdlet a seguir:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Conjunto de toonever uma senha expirar

1. Conecte-se tooWindows PowerShell usando suas credenciais de administrador da empresa.
2. Execute uma saudação comandos a seguir:

   * senha Olá tooset toonever de um usuário expirar, execute Olá cmdlet a seguir usando o nome principal de usuário de saudação (UPN) ou Olá ID do usuário hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * senhas de saudação tooset de todos os usuários de saudação em uma organização toonever expirar, execute Olá cmdlet a seguir:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR
