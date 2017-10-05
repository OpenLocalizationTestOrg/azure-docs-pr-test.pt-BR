---
title: Registrar um aplicativo com o ponto de extremidade do Azure AD v2.0 usando o portal | Microsoft Docs
description: "Como registrar um aplicativo na Microsoft para habilitar a entrada e acessar os serviços da Microsoft usando o ponto de extremidade v2.0"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="d214a-103">Como registrar um aplicativo com o ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="d214a-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="d214a-104">Para criar um aplicativo que aceite entrada do AD do Azure e do MSA, você primeiro precisará registrar um aplicativo com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d214a-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="d214a-105">Você não poderá usar nenhum dos seus aplicativos existentes com o Azure AD ou MSA, será necessário criar um novo.</span><span class="sxs-lookup"><span data-stu-id="d214a-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="d214a-106">Nem todos os recursos e cenários do Azure Active Directory têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="d214a-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d214a-107">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d214a-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="d214a-108">Visite o Portal de Registro de Aplicativos da Microsoft</span><span class="sxs-lookup"><span data-stu-id="d214a-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="d214a-109">Primeiro as prioridades, navegue até [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="d214a-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="d214a-110">Este é o novo portal de registro de aplicativos em que você pode gerenciar todos os seus aplicativos Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d214a-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="d214a-111">Entrar com uma conta da Microsoft pessoal, profissional ou escolar.</span><span class="sxs-lookup"><span data-stu-id="d214a-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="d214a-112">Se você não tiver uma, inscreva-se para uma nova conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="d214a-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="d214a-113">Vá em frente, não vai demorar muito. Vamos aguardar aqui.</span><span class="sxs-lookup"><span data-stu-id="d214a-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="d214a-114">Pronto?</span><span class="sxs-lookup"><span data-stu-id="d214a-114">Done?</span></span> <span data-ttu-id="d214a-115">Você deve agora estar olhando a lista de aplicativos da Microsoft, que provavelmente está vazia.</span><span class="sxs-lookup"><span data-stu-id="d214a-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="d214a-116">Vamos mudar isso.</span><span class="sxs-lookup"><span data-stu-id="d214a-116">Let's change that.</span></span>

<span data-ttu-id="d214a-117">Clique em **Adicionar um aplicativo**e dê um nome a ele.</span><span class="sxs-lookup"><span data-stu-id="d214a-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="d214a-118">O portal atribuirá ao seu aplicativo uma Id de aplicativo globalmente exclusiva que você usará posteriormente em seu código.</span><span class="sxs-lookup"><span data-stu-id="d214a-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="d214a-119">Caso seu aplicativo inclua um componente do servidor que precisa de tokens de acesso para chamar APIs (tais como: Office, Azure ou sua própria API Web), também convém criar um **Segredo de Aplicativo** aqui.</span><span class="sxs-lookup"><span data-stu-id="d214a-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="d214a-120">Em seguida, adicione as Plataformas que seu aplicativo usará.</span><span class="sxs-lookup"><span data-stu-id="d214a-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="d214a-121">Para aplicativos baseados na Web, forneça um **URI de Redirecionamento** em que é possível enviar mensagens de entrada.</span><span class="sxs-lookup"><span data-stu-id="d214a-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="d214a-122">Para aplicativos móveis, copie o URI de redirecionamento criado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="d214a-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="d214a-123">Opcionalmente, você pode personalizar a aparência de sua página de entrada na Seção do perfil.</span><span class="sxs-lookup"><span data-stu-id="d214a-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="d214a-124">Certifique-se de clicar em **Salvar** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="d214a-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="d214a-125">Quando você cria um aplicativo usando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ele será registrado no locatário inicial da conta que você usa para entrar no portal.</span><span class="sxs-lookup"><span data-stu-id="d214a-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="d214a-126">Isso significa que não é possível registrar um aplicativo no seu locatário do Azure AD usando uma conta pessoal da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d214a-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="d214a-127">Se você quiser registrar um aplicativo em um determinado locatário explicitamente, entre com uma conta criada originalmente no locatário em questão.</span><span class="sxs-lookup"><span data-stu-id="d214a-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="d214a-128">Compilar um aplicativo de início rápido</span><span class="sxs-lookup"><span data-stu-id="d214a-128">Build a quick start app</span></span>
<span data-ttu-id="d214a-129">Agora que você tem um aplicativo da Microsoft, poderá concluir um dos nossos tutoriais de início rápido da v2.0.</span><span class="sxs-lookup"><span data-stu-id="d214a-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="d214a-130">Aqui estão algumas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d214a-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

