---
title: "Introdução ao Android no Azure AD v2 – Testar | Microsoft Docs"
description: Como um aplicativo do Android pode obter um token de acesso e chamar a API do Microsoft Graph ou APIs que exigem tokens de acesso por meio do ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="7a56f-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="7a56f-103">Test your code</span></span>

1. <span data-ttu-id="7a56f-104">Implante o código no dispositivo/emulador.</span><span class="sxs-lookup"><span data-stu-id="7a56f-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="7a56f-105">Quando você estiver pronto para testar, use uma conta do Microsoft Azure Active Directory (conta organizacional) ou uma Conta da Microsoft (live.com, outlook.com) para se conectar.</span><span class="sxs-lookup"><span data-stu-id="7a56f-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="7a56f-106">![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="7a56f-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="7a56f-107">
![Conexão](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="7a56f-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="7a56f-108">Consentimento</span><span class="sxs-lookup"><span data-stu-id="7a56f-108">Consent</span></span>
<span data-ttu-id="7a56f-109">Na primeira vez que um usuário entrar no aplicativo, será apresentada uma tela de consentimento semelhante à tela abaixo, na qual ele precisa aceitar explicitamente:</span><span class="sxs-lookup"><span data-stu-id="7a56f-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Consentimento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="7a56f-111">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="7a56f-111">Expected results</span></span>
<span data-ttu-id="7a56f-112">Você deverá ver os resultados de uma chamada ao ponto de extremidade “me” da API do Microsoft Graph usado para obter o perfil do usuário – https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="7a56f-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="7a56f-113">Para obter uma lista de pontos de extremidade comuns do Microsoft Graph, consulte este [artigo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="7a56f-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="7a56f-114">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="7a56f-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="7a56f-115">A API do Microsoft Graph requer o escopo `user.read` para ler o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="7a56f-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="7a56f-116">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="7a56f-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="7a56f-117">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="7a56f-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="7a56f-118">Por exemplo, para o Microsoft Graph, o escopo `Calendars.Read` é necessário para listar os calendários do usuário.</span><span class="sxs-lookup"><span data-stu-id="7a56f-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="7a56f-119">Para acessar o calendário do usuário no contexto de um aplicativo, é necessário adicionar a permissão delegada `Calendars.Read` às informações de registro do aplicativo e, em seguida, adicionar o escopo `Calendars.Read` à chamada `acquireTokenSilentAsync`.</span><span class="sxs-lookup"><span data-stu-id="7a56f-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="7a56f-120">Talvez o usuário precise fornecer consentimentos adicionais à medida que o número de escopos aumentar.</span><span class="sxs-lookup"><span data-stu-id="7a56f-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
