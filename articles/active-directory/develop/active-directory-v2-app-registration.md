---
title: "um aplicativo com o ponto de extremidade de v 2.0 de saudação do AD do Azure usando o portal de saudação do aaaRegister | Microsoft Docs"
description: Como tooregister um aplicativo com a Microsoft para habilitar entrar e acessar o Microsoft services usando o ponto de extremidade do hello v 2.0
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="e5221-103">Como tooregister um aplicativo com o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="e5221-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="e5221-104">toobuild um aplicativo que aceita MSA & AD do Azure entrar, primeiro será necessário tooregister um aplicativo com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5221-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="e5221-105">Neste momento, você não ser capaz de toouse quaisquer aplicativos existentes que você possa ter com o AD do Azure ou MSA - você precisará toocreate uma nova marca.</span><span class="sxs-lookup"><span data-stu-id="e5221-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="e5221-106">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="e5221-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="e5221-107">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="e5221-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="e5221-108">Visite o portal de registro de aplicativo hello Microsoft</span><span class="sxs-lookup"><span data-stu-id="e5221-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="e5221-109">Coisas mais importantes primeiro - navegue muito[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="e5221-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="e5221-110">Este é o novo portal de registro de aplicativos em que você pode gerenciar todos os seus aplicativos Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5221-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="e5221-111">Entrar com uma conta da Microsoft pessoal, profissional ou escolar.</span><span class="sxs-lookup"><span data-stu-id="e5221-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="e5221-112">Se você não tiver uma, inscreva-se para uma nova conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="e5221-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="e5221-113">Vá em frente, não vai demorar muito. Vamos aguardar aqui.</span><span class="sxs-lookup"><span data-stu-id="e5221-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="e5221-114">Pronto?</span><span class="sxs-lookup"><span data-stu-id="e5221-114">Done?</span></span> <span data-ttu-id="e5221-115">Você deve agora estar olhando a lista de aplicativos da Microsoft, que provavelmente está vazia.</span><span class="sxs-lookup"><span data-stu-id="e5221-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="e5221-116">Vamos mudar isso.</span><span class="sxs-lookup"><span data-stu-id="e5221-116">Let's change that.</span></span>

<span data-ttu-id="e5221-117">Clique em **Adicionar um aplicativo**e dê um nome a ele.</span><span class="sxs-lookup"><span data-stu-id="e5221-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="e5221-118">portal de saudação atribuirá seu aplicativo uma Id globalmente exclusiva do aplicativo que você usará posteriormente no seu código.</span><span class="sxs-lookup"><span data-stu-id="e5221-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="e5221-119">Se seu aplicativo inclui um componente do lado do servidor que precisam de tokens de acesso para chamadas APIs (pense: Office, Azure ou sua própria API da web), você desejará toocreate um **segredo do aplicativo** aqui também.</span><span class="sxs-lookup"><span data-stu-id="e5221-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="e5221-120">Em seguida, adicione Olá plataformas que seu aplicativo usará.</span><span class="sxs-lookup"><span data-stu-id="e5221-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="e5221-121">Para aplicativos baseados na Web, forneça um **URI de Redirecionamento** em que é possível enviar mensagens de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5221-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="e5221-122">Para aplicativos móveis, cópia inativo padrão Olá redirecione o uri criado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="e5221-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="e5221-123">Opcionalmente, você pode personalizar Olá aparência de sua página de entrada hello perfil.</span><span class="sxs-lookup"><span data-stu-id="e5221-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="e5221-124">Certifique-se de que tooclick **salvar** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e5221-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="e5221-125">Quando você cria um aplicativo usando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), aplicativo hello será registrado no locatário de saudação inicial da conta de saudação que você use toosign no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5221-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="e5221-126">Isso significa que não é possível registrar um aplicativo no seu locatário do Azure AD usando uma conta pessoal da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e5221-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="e5221-127">Se você explicitamente tooregister um aplicativo em um locatário específico, entre com uma conta que criou originalmente no locatário.</span><span class="sxs-lookup"><span data-stu-id="e5221-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="e5221-128">Compilar um aplicativo de início rápido</span><span class="sxs-lookup"><span data-stu-id="e5221-128">Build a quick start app</span></span>
<span data-ttu-id="e5221-129">Agora que você tem um aplicativo da Microsoft, poderá concluir um dos nossos tutoriais de início rápido da v2.0.</span><span class="sxs-lookup"><span data-stu-id="e5221-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="e5221-130">Aqui estão algumas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e5221-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

