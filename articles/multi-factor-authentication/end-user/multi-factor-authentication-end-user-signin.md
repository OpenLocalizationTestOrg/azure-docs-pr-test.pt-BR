---
title: aaaAzure MFA entrar com a verificacao | Microsoft Docs
description: "Esta página fornece orientação sobre onde toogo toosee Olá vários métodos de entrada disponíveis com o Azure MFA."
keywords: "autenticação do usuário, experiência de conexão, conectar com telefone celular, conectar com telefone do escritório"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="4dcc8-104">Olá experiência de entrada com o Azure multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4dcc8-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="4dcc8-105">Olá finalidade deste artigo é toowalk por meio de uma experiência de conexão típica.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="4dcc8-106">Para obter ajuda com entrar ou tootroubleshoot problemas, consulte [tendo problemas com o Azure multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="4dcc8-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="4dcc8-107">Qual será sua experiência de conexão?</span><span class="sxs-lookup"><span data-stu-id="4dcc8-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="4dcc8-108">Sua experiência de entrada é diferente dependendo do que você escolhe toouse como o segundo fator: uma chamada telefônica, um aplicativo de autenticação ou textos.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="4dcc8-109">Escolha a opção de saudação que melhor descreve o que está fazendo:</span><span class="sxs-lookup"><span data-stu-id="4dcc8-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="4dcc8-110">Como entrar no Azure?</span><span class="sxs-lookup"><span data-stu-id="4dcc8-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="4dcc8-111">Com um telefone de chamada telefônica toomy móvel ou comercial</span><span class="sxs-lookup"><span data-stu-id="4dcc8-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="4dcc8-112">Com um celular toomy do texto</span><span class="sxs-lookup"><span data-stu-id="4dcc8-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="4dcc8-113">Com notificações do aplicativo do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="4dcc8-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="4dcc8-114">Com códigos de verificação de aplicativo do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="4dcc8-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="4dcc8-115">Com um método alternativo, porque não consigo usar meu método preferido agora</span><span class="sxs-lookup"><span data-stu-id="4dcc8-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="4dcc8-116">Conectando com uma chamada telefônica</span><span class="sxs-lookup"><span data-stu-id="4dcc8-116">Signing in with a phone call</span></span>
<span data-ttu-id="4dcc8-117">Olá informações a seguir descreve a experiência de verificação em duas etapas Olá com chamada tooyour móveis ou telefone comercial.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="4dcc8-118">Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="4dcc8-119">A Microsoft liga para você.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="4dcc8-120">Atenda phone hello e pressione a tecla # de saudação.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="4dcc8-121">Conectando com uma mensagem de texto</span><span class="sxs-lookup"><span data-stu-id="4dcc8-121">Signing in with a text message</span></span>
<span data-ttu-id="4dcc8-122">Olá informações a seguir descreve a experiência de verificação de duas etapas Olá com um telefone celular de tooyour de mensagem de texto:</span><span class="sxs-lookup"><span data-stu-id="4dcc8-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="4dcc8-123">Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="4dcc8-124">A Microsoft envia para você uma mensagem de texto com um código numérico.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="4dcc8-125">Insira código Olá Olá caixa fornecida na página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4dcc8-126">Entrar com o aplicativo do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="4dcc8-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="4dcc8-127">Olá informações a seguir descrevem a experiência de saudação do aplicativo do Microsoft Authenticator Olá para verificações de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="4dcc8-128">Há duas maneiras diferentes toouse Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="4dcc8-129">Você pode receber notificações por push em seu dispositivo ou você pode abrir Olá aplicativo tooget um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="4dcc8-130">toosign com uma notificação de aplicativo do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="4dcc8-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="4dcc8-131">Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4dcc8-132">A Microsoft envia um aplicativo de Microsoft Authenticator toohello notificação em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![A Microsoft envia notificação](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="4dcc8-134">Notificação de saudação aberta no seu telefone e selecione Olá **verificar** chave.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="4dcc8-135">Se sua empresa exigir um PIN, digite-o aqui.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="4dcc8-136">Agora você deve estar conectado.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="4dcc8-137">toosign usando um código de verificação com o aplicativo do Microsoft Authenticator Olá</span><span class="sxs-lookup"><span data-stu-id="4dcc8-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="4dcc8-138">Se você usar códigos de verificação Olá Microsoft Authenticator aplicativo tooget, em seguida, quando você abre o aplicativo hello você vir um número em seu nome de conta.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="4dcc8-139">Esse número é alterado a cada 30 segundos para que você não use Olá mesmo número duas vezes.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="4dcc8-140">Quando for solicitado um código de verificação, abra o aplicativo hello e usar qualquer número que está sendo exibido.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="4dcc8-141">Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4dcc8-142">A Microsoft solicita que você insira um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-142">Microsoft prompts you for a verification code.</span></span>

  ![Inserir código de verificação](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="4dcc8-144">Abra Olá Microsoft Authenticator aplicativo em seu telefone e insira o código de saudação na caixa Olá onde você está tentando entrar.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="4dcc8-145">Conectando-se com um método alternativo</span><span class="sxs-lookup"><span data-stu-id="4dcc8-145">Signing in with an alternate method</span></span>
<span data-ttu-id="4dcc8-146">Às vezes, você não tem o telefone hello ou dispositivo que você deseja configurar como seu método preferido de verificação.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="4dcc8-147">É por isso que recomendamos que faça o backup da conta.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="4dcc8-148">Olá seção a seguir mostra como toosign com um método alternativo para o método principal pode não estar disponível.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="4dcc8-149">Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="4dcc8-150">Selecione **Usar uma opção de verificação diferente**.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="4dcc8-151">Você verá opções de verificação diferentes, de acordo com a quantidade configurada.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="4dcc8-152">Escolha um método alternativo e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-152">Choose an alternate method and sign in.</span></span>

  ![Usar método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="4dcc8-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4dcc8-154">Next steps</span></span>

<span data-ttu-id="4dcc8-155">Se você tiver problemas para entrar usando a verificação em duas etapas, consulte [Problemas com a Autenticação Multifator do Microsoft Azure](multi-factor-authentication-end-user-troubleshoot.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="4dcc8-156">Saiba como muito[gerenciar as configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4dcc8-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="4dcc8-157">Descubra como muito[Introdução ao aplicativo do Microsoft Authenticator Olá](microsoft-authenticator-app-how-to.md) para que você possa usar notificações toosign, em vez de chamadas telefônicas e de textos.</span><span class="sxs-lookup"><span data-stu-id="4dcc8-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
