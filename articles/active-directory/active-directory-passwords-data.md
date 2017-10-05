---
title: Requisitos de dados SSPR do Azure AD | Microsoft Docs
description: "Requisitos de dados para autoatendimento de redefinição de senha do Azure AD e como atendê-los"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="a9498-103">Implantar redefinição de senha sem exigir registro do usuário final</span><span class="sxs-lookup"><span data-stu-id="a9498-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="a9498-104">A implantação do SSPR (Autoatendimento de Redefinição de Senha) exige que os dados de autenticação estejam presentes.</span><span class="sxs-lookup"><span data-stu-id="a9498-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="a9498-105">Algumas organizações precisam que seus próprios usuários insiram os respectivos dados de autenticação, mas muitas organizações preferem sincronizar com dados existentes no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9498-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="a9498-106">Se você tiver formatado corretamente os dados no diretório local e configurar [Azure AD Connect usando as configurações expressas](./connect/active-directory-aadconnect-get-started-express.md), esses dados serão disponibilizados para o Azure AD e o SSPR sem exigir qualquer interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a9498-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="a9498-107">Todos os números de telefone devem estar no formato +CountryCode PhoneNumber (por exemplo: +1 4255551234) para que funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="a9498-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="a9498-108">A redefinição de senha não dá suporte a ramais telefônicos.</span><span class="sxs-lookup"><span data-stu-id="a9498-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="a9498-109">Mesmo no formato +1 4255551234X12345, as extensões são removidas antes que a chamada seja completada.</span><span class="sxs-lookup"><span data-stu-id="a9498-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="a9498-110">Campos populados</span><span class="sxs-lookup"><span data-stu-id="a9498-110">Fields populated</span></span>

<span data-ttu-id="a9498-111">Se você usar as configurações padrão no Azure AD Connect, serão realizados os seguintes mapeamentos.</span><span class="sxs-lookup"><span data-stu-id="a9498-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="a9498-112">AD local</span><span class="sxs-lookup"><span data-stu-id="a9498-112">On-premises AD</span></span> | <span data-ttu-id="a9498-113">AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a9498-113">Azure AD</span></span> | <span data-ttu-id="a9498-114">Informações de contato para Autenticação do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9498-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9498-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="a9498-115">telephoneNumber</span></span> | <span data-ttu-id="a9498-116">Telefone comercial</span><span class="sxs-lookup"><span data-stu-id="a9498-116">Office phone</span></span> | <span data-ttu-id="a9498-117">Telefone alternativo</span><span class="sxs-lookup"><span data-stu-id="a9498-117">Alternate phone</span></span> |
| <span data-ttu-id="a9498-118">Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="a9498-118">mobile</span></span> | <span data-ttu-id="a9498-119">Telefone celular</span><span class="sxs-lookup"><span data-stu-id="a9498-119">Mobile phone</span></span> | <span data-ttu-id="a9498-120">Telefone</span><span class="sxs-lookup"><span data-stu-id="a9498-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="a9498-121">Perguntas e respostas de segurança</span><span class="sxs-lookup"><span data-stu-id="a9498-121">Security questions and answers</span></span>

<span data-ttu-id="a9498-122">As perguntas e respostas de segurança são armazenadas em seu locatário do Azure AD e podem ser acessadas somente por usuários pelo [Portal de registro do SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="a9498-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="a9498-123">Os administradores não podem ver nem modificar o conteúdo das perguntas e respostas dos outros usuários.</span><span class="sxs-lookup"><span data-stu-id="a9498-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="a9498-124">O que acontece quando um usuário se registra</span><span class="sxs-lookup"><span data-stu-id="a9498-124">What happens when a user registers</span></span>

<span data-ttu-id="a9498-125">Quando um usuário se registra, a página de registro define os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="a9498-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="a9498-126">Telefone de autenticação</span><span class="sxs-lookup"><span data-stu-id="a9498-126">Authentication Phone</span></span>
* <span data-ttu-id="a9498-127">E-mail de autenticação</span><span class="sxs-lookup"><span data-stu-id="a9498-127">Authentication Email</span></span>
* <span data-ttu-id="a9498-128">Perguntas de segurança e respostas</span><span class="sxs-lookup"><span data-stu-id="a9498-128">Security Questions and Answers</span></span>

<span data-ttu-id="a9498-129">Se você forneceu um valor para **Celular** ou **Email Alternativo**, os usuários poderão usar esses valores imediatamente para redefinir as senhas, mesmo que não tenham se registrado no serviço.</span><span class="sxs-lookup"><span data-stu-id="a9498-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="a9498-130">Além disso, os usuários visualizam esses valores ao se registrarem pela primeira vez, e os modificam, se for desejado.</span><span class="sxs-lookup"><span data-stu-id="a9498-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="a9498-131">Após registro bem-sucedido, esses valores serão persistidos nos campos **Telefone de Autenticação** e **Email de Autenticação**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="a9498-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="a9498-132">Definir e ler os dados de autenticação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9498-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="a9498-133">Os campos a seguir podem ser definidos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9498-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="a9498-134">Email alternativo</span><span class="sxs-lookup"><span data-stu-id="a9498-134">Alternate Email</span></span>
* <span data-ttu-id="a9498-135">Telefone celular</span><span class="sxs-lookup"><span data-stu-id="a9498-135">Mobile Phone</span></span>
* <span data-ttu-id="a9498-136">Telefone comercial – só poderá ser definido se não for sincronizar com um diretório local</span><span class="sxs-lookup"><span data-stu-id="a9498-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="a9498-137">Usando o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a9498-137">Using PowerShell V1</span></span>

<span data-ttu-id="a9498-138">Para começar, primeiramente é preciso [baixar e instalar o módulo PowerShell do Azure AD](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="a9498-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="a9498-139">Depois de instalá-lo, você poderá seguir as etapas abaixo para configurar cada campo.</span><span class="sxs-lookup"><span data-stu-id="a9498-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="a9498-140">Definir dados de autenticação com o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a9498-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="a9498-141">Ler dados de autenticação com o PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="a9498-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="a9498-142">O Telefone de Autenticação e o Email de Autenticação só podem ser lidos usando o PowerShell V1 com os comandos abaixo</span><span class="sxs-lookup"><span data-stu-id="a9498-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="a9498-143">Usando o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a9498-143">Using PowerShell V2</span></span>

<span data-ttu-id="a9498-144">Para começar, primeiramente é preciso [baixar e instalar o módulo PowerShell V2 do Azure AD](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="a9498-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="a9498-145">Depois de instalá-lo, você poderá seguir as etapas abaixo para configurar cada campo.</span><span class="sxs-lookup"><span data-stu-id="a9498-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="a9498-146">Para instalar rapidamente de versões recentes do PowerShell que suportam Install-Module, execute estes comandos (a primeira linha apenas verifica se ele já está instalado):</span><span class="sxs-lookup"><span data-stu-id="a9498-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="a9498-147">Definir Dados de Autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a9498-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="a9498-148">Ler Dados de Autenticação com o PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="a9498-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="a9498-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a9498-149">Next steps</span></span>

<span data-ttu-id="a9498-150">Os links a seguir fornecem informações adicionais sobre a redefinição de senha usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9498-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="a9498-151">[**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9498-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="a9498-152">[**Licenciamento**](active-directory-passwords-licensing.md): configure o licenciamento do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9498-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="a9498-153">[**Distribuição**](active-directory-passwords-best-practices.md): planeje e implante o SSPR para seus usuários usando as diretrizes descritas aqui</span><span class="sxs-lookup"><span data-stu-id="a9498-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="a9498-154">[**Personalizar**](active-directory-passwords-customize.md): personalize a aparência da experiência do SSPR em sua empresa.</span><span class="sxs-lookup"><span data-stu-id="a9498-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="a9498-155">[**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9498-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="a9498-156">[**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR</span><span class="sxs-lookup"><span data-stu-id="a9498-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="a9498-157">[**Detalhamento Técnico**](active-directory-passwords-how-it-works.md): veja os bastidores para entender como o recurso funciona</span><span class="sxs-lookup"><span data-stu-id="a9498-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="a9498-158">[**Perguntas frequentes**](active-directory-passwords-faq.md): como?</span><span class="sxs-lookup"><span data-stu-id="a9498-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="a9498-159">Por quê?</span><span class="sxs-lookup"><span data-stu-id="a9498-159">Why?</span></span> <span data-ttu-id="a9498-160">O quê?</span><span class="sxs-lookup"><span data-stu-id="a9498-160">What?</span></span> <span data-ttu-id="a9498-161">Onde?</span><span class="sxs-lookup"><span data-stu-id="a9498-161">Where?</span></span> <span data-ttu-id="a9498-162">Quem?</span><span class="sxs-lookup"><span data-stu-id="a9498-162">Who?</span></span> <span data-ttu-id="a9498-163">Quando?</span><span class="sxs-lookup"><span data-stu-id="a9498-163">When?</span></span> <span data-ttu-id="a9498-164">– respostas para perguntas que você sempre quis fazer</span><span class="sxs-lookup"><span data-stu-id="a9498-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="a9498-165">[**Solução de problemas**](active-directory-passwords-troubleshoot.md) - Saiba como resolver problemas comuns que vemos com a SSPR</span><span class="sxs-lookup"><span data-stu-id="a9498-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
