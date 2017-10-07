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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="61fdf-103">Implantar redefinição de senha sem exigir registro do usuário final</span><span class="sxs-lookup"><span data-stu-id="61fdf-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="61fdf-104">A implantação de redefinição de senha de autoatendimento (SSPR) requer autenticação dados toobe presente.</span><span class="sxs-lookup"><span data-stu-id="61fdf-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="61fdf-105">Algumas organizações têm seus usuários inserir seus próprios dados de autenticação, mas muitas organizações preferem toosynchronize com os dados existentes no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61fdf-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="61fdf-106">Se você tiver formatado corretamente os dados em seu diretório local e configurar [do Azure AD Connect usando as configurações expressas](./connect/active-directory-aadconnect-get-started-express.md), que os dados ficam disponível tooAzure AD e SSPR com nenhuma interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="61fdf-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="61fdf-107">Os números de telefone devem estar no formato de saudação + CountryCode PhoneNumber exemplo: + 1 4255551234 toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="61fdf-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="61fdf-108">A redefinição de senha não dá suporte a ramais telefônicos.</span><span class="sxs-lookup"><span data-stu-id="61fdf-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="61fdf-109">Mesmo em formato 12345 do hello 4255551234 + 1 X, extensões são removidas antes de saudação é chamada.</span><span class="sxs-lookup"><span data-stu-id="61fdf-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="61fdf-110">Campos populados</span><span class="sxs-lookup"><span data-stu-id="61fdf-110">Fields populated</span></span>

<span data-ttu-id="61fdf-111">Se você usar as configurações padrão de Olá Olá do Azure AD Connect a seguir são feitos mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="61fdf-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="61fdf-112">AD local</span><span class="sxs-lookup"><span data-stu-id="61fdf-112">On-premises AD</span></span> | <span data-ttu-id="61fdf-113">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61fdf-113">Azure AD</span></span> | <span data-ttu-id="61fdf-114">Informações de contato para Autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61fdf-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61fdf-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="61fdf-115">telephoneNumber</span></span> | <span data-ttu-id="61fdf-116">Telefone comercial</span><span class="sxs-lookup"><span data-stu-id="61fdf-116">Office phone</span></span> | <span data-ttu-id="61fdf-117">Telefone alternativo</span><span class="sxs-lookup"><span data-stu-id="61fdf-117">Alternate phone</span></span> |
| <span data-ttu-id="61fdf-118">Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="61fdf-118">mobile</span></span> | <span data-ttu-id="61fdf-119">Telefone celular</span><span class="sxs-lookup"><span data-stu-id="61fdf-119">Mobile phone</span></span> | <span data-ttu-id="61fdf-120">Telefone</span><span class="sxs-lookup"><span data-stu-id="61fdf-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="61fdf-121">Perguntas e respostas de segurança</span><span class="sxs-lookup"><span data-stu-id="61fdf-121">Security questions and answers</span></span>

<span data-ttu-id="61fdf-122">Perguntas de segurança e as respostas são armazenadas com segurança em seu locatário do AD do Azure e são apenas toousers acessível por meio de saudação [portal de registro SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="61fdf-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="61fdf-123">Os administradores não podem ver ou modificar o conteúdo de Olá de usuários perguntas e respostas de outro.</span><span class="sxs-lookup"><span data-stu-id="61fdf-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="61fdf-124">O que acontece quando um usuário se registra</span><span class="sxs-lookup"><span data-stu-id="61fdf-124">What happens when a user registers</span></span>

<span data-ttu-id="61fdf-125">Quando um usuário se registra, os conjuntos de páginas de registro Olá Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="61fdf-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="61fdf-126">Telefone de autenticação</span><span class="sxs-lookup"><span data-stu-id="61fdf-126">Authentication Phone</span></span>
* <span data-ttu-id="61fdf-127">E-mail de autenticação</span><span class="sxs-lookup"><span data-stu-id="61fdf-127">Authentication Email</span></span>
* <span data-ttu-id="61fdf-128">Perguntas de segurança e respostas</span><span class="sxs-lookup"><span data-stu-id="61fdf-128">Security Questions and Answers</span></span>

<span data-ttu-id="61fdf-129">Se você tiver fornecido um valor para **celular** ou **Email alternativo**, os usuários podem usar imediatamente tooreset esses valores suas senhas, mesmo se eles ainda não registrado para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="61fdf-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="61fdf-130">Além disso, os usuários consulte esses valores de durante o registro do hello primeira vez e modificá-las, se desejarem.</span><span class="sxs-lookup"><span data-stu-id="61fdf-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="61fdf-131">Depois que eles registrar com êxito, esses valores serão mantidos no hello **telefone de autenticação** e **Email de autenticação** campos, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="61fdf-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="61fdf-132">Definir e ler os dados de autenticação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="61fdf-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="61fdf-133">Olá campos a seguir pode ser definida usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="61fdf-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="61fdf-134">Email alternativo</span><span class="sxs-lookup"><span data-stu-id="61fdf-134">Alternate Email</span></span>
* <span data-ttu-id="61fdf-135">Telefone celular</span><span class="sxs-lookup"><span data-stu-id="61fdf-135">Mobile Phone</span></span>
* <span data-ttu-id="61fdf-136">Telefone comercial – só poderá ser definido se não for sincronizar com um diretório local</span><span class="sxs-lookup"><span data-stu-id="61fdf-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="61fdf-137">Usando o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="61fdf-137">Using PowerShell V1</span></span>

<span data-ttu-id="61fdf-138">tooget iniciado, é necessário muito[baixar e instalar o módulo do PowerShell do Azure AD Olá](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="61fdf-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="61fdf-139">Depois de instalado, você pode seguir as etapas de saudação que seguem tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="61fdf-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="61fdf-140">Definir dados de autenticação com o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="61fdf-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="61fdf-141">Ler dados de autenticação com o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="61fdf-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="61fdf-142">Telefone de autenticação e o Email de autenticação só podem ser lidos usando o Powershell V1 usar Olá comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="61fdf-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="61fdf-143">Usando o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="61fdf-143">Using PowerShell V2</span></span>

<span data-ttu-id="61fdf-144">tooget iniciado, é necessário muito[baixar e instalar o módulo do PowerShell hello Azure AD V2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="61fdf-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="61fdf-145">Depois de instalado, você pode seguir as etapas de saudação que seguem tooconfigure cada campo.</span><span class="sxs-lookup"><span data-stu-id="61fdf-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="61fdf-146">tooinstall rapidamente a partir de versões recentes do PowerShell que dão suporte a Install-Module, execute estes comandos (primeira linha de saudação simplesmente verifica toosee se ele já está instalado):</span><span class="sxs-lookup"><span data-stu-id="61fdf-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="61fdf-147">Definir Dados de Autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="61fdf-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="61fdf-148">Ler Dados de Autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="61fdf-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="61fdf-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61fdf-149">Next steps</span></span>

<span data-ttu-id="61fdf-150">Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="61fdf-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="61fdf-151">[**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61fdf-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="61fdf-152">[**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61fdf-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="61fdf-153">[**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui</span><span class="sxs-lookup"><span data-stu-id="61fdf-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="61fdf-154">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.</span><span class="sxs-lookup"><span data-stu-id="61fdf-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="61fdf-155">[**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="61fdf-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="61fdf-156">[**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR</span><span class="sxs-lookup"><span data-stu-id="61fdf-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="61fdf-157">[**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona</span><span class="sxs-lookup"><span data-stu-id="61fdf-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="61fdf-158">[**Perguntas frequentes**](active-directory-passwords-faq.md): como?</span><span class="sxs-lookup"><span data-stu-id="61fdf-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="61fdf-159">Por quê?</span><span class="sxs-lookup"><span data-stu-id="61fdf-159">Why?</span></span> <span data-ttu-id="61fdf-160">O quê?</span><span class="sxs-lookup"><span data-stu-id="61fdf-160">What?</span></span> <span data-ttu-id="61fdf-161">Onde?</span><span class="sxs-lookup"><span data-stu-id="61fdf-161">Where?</span></span> <span data-ttu-id="61fdf-162">Quem?</span><span class="sxs-lookup"><span data-stu-id="61fdf-162">Who?</span></span> <span data-ttu-id="61fdf-163">Quando?</span><span class="sxs-lookup"><span data-stu-id="61fdf-163">When?</span></span> <span data-ttu-id="61fdf-164">-Respostas tooquestions você sempre quis tooask</span><span class="sxs-lookup"><span data-stu-id="61fdf-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="61fdf-165">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR</span><span class="sxs-lookup"><span data-stu-id="61fdf-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
