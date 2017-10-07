---
title: Requisitos de dados SSPR do Azure AD | Microsoft Docs
description: "Redefinição de senha de autoatendimento do AD do Azure requisitos de dados e como toosatisfy-los"
services: active-directory
keywords: 
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Implantar redefinição de senha sem exigir registro do usuário final

A implantação de redefinição de senha de autoatendimento (SSPR) requer autenticação dados toobe presente. Algumas organizações têm seus usuários inserir seus próprios dados de autenticação, mas muitas organizações preferem toosynchronize com os dados existentes no Active Directory. Se você tiver formatado corretamente os dados em seu diretório local e configurar [do Azure AD Connect usando as configurações expressas](./connect/active-directory-aadconnect-get-started-express.md), que os dados ficam disponível tooAzure AD e SSPR com nenhuma interação do usuário.

Os números de telefone devem estar no formato de saudação + CountryCode PhoneNumber exemplo: + 1 4255551234 toowork corretamente.

> [!NOTE]
> A redefinição de senha não dá suporte a ramais telefônicos. Mesmo em formato 12345 do hello 4255551234 + 1 X, extensões são removidas antes de saudação é chamada.

## <a name="fields-populated"></a>Campos populados

Se você usar as configurações padrão de Olá Olá do Azure AD Connect a seguir são feitos mapeamentos.

| AD local | AD do Azure | Informações de contato para Autenticação do Azure AD |
| --- | --- | --- |
| telephoneNumber | Telefone comercial | Telefone alternativo |
| Serviço Móvel | Telefone celular | Telefone |


## <a name="security-questions-and-answers"></a>Perguntas e respostas de segurança

Perguntas de segurança e as respostas são armazenadas com segurança em seu locatário do AD do Azure e são apenas toousers acessível por meio de saudação [portal de registro SSPR](https://aka.ms/ssprsetup). Os administradores não podem ver ou modificar o conteúdo de Olá de usuários perguntas e respostas de outro.

### <a name="what-happens-when-a-user-registers"></a>O que acontece quando um usuário se registra

Quando um usuário se registra, os conjuntos de páginas de registro Olá Olá campos a seguir:

* Telefone de autenticação
* E-mail de autenticação
* Perguntas de segurança e respostas

Se você tiver fornecido um valor para **celular** ou **Email alternativo**, os usuários podem usar imediatamente tooreset esses valores suas senhas, mesmo se eles ainda não registrado para o serviço de saudação. Além disso, os usuários consulte esses valores de durante o registro do hello primeira vez e modificá-las, se desejarem. Depois que eles registrar com êxito, esses valores serão mantidos no hello **telefone de autenticação** e **Email de autenticação** campos, respectivamente.

## <a name="set-and-read-authentication-data-using-powershell"></a>Definir e ler os dados de autenticação usando o PowerShell

Olá campos a seguir pode ser definida usando o PowerShell

* Email alternativo
* Telefone celular
* Telefone comercial – só poderá ser definido se não for sincronizar com um diretório local

### <a name="using-powershell-v1"></a>Usando o PowerShell V1

tooget iniciado, é necessário muito[baixar e instalar o módulo do PowerShell do Azure AD Olá](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Depois de instalado, você pode seguir as etapas de saudação que seguem tooconfigure cada campo.

#### <a name="set-authentication-data-with-powershell-v1"></a>Definir dados de autenticação com o PowerShell V1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Ler dados de autenticação com o PowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Telefone de autenticação e o Email de autenticação só podem ser lidos usando o Powershell V1 usar Olá comandos a seguir

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Usando o PowerShell V2

tooget iniciado, é necessário muito[baixar e instalar o módulo do PowerShell hello Azure AD V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Depois de instalado, você pode seguir as etapas de saudação que seguem tooconfigure cada campo.

tooinstall rapidamente a partir de versões recentes do PowerShell que dão suporte a Install-Module, execute estes comandos (primeira linha de saudação simplesmente verifica toosee se ele já está instalado):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Definir Dados de Autenticação com o PowerShell V2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Ler Dados de Autenticação com o PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR
