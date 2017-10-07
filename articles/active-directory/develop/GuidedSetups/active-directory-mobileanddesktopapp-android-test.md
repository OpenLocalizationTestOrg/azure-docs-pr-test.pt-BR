---
title: "aaaAzure AD v2 Android Introdução - teste | Microsoft Docs"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="61062-103">Testar seu código</span><span class="sxs-lookup"><span data-stu-id="61062-103">Test your code</span></span>

1. <span data-ttu-id="61062-104">Implante seu código tooyour/emulador de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61062-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="61062-105">Quando você estiver pronto tootest, use um Microsoft Azure Active Directory (conta organizacional) ou um toosign de conta Account da Microsoft (live.com, outlook.com) no.</span><span class="sxs-lookup"><span data-stu-id="61062-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="61062-106">![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="61062-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="61062-107">
![Conexão](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="61062-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="61062-108">Consentimento</span><span class="sxs-lookup"><span data-stu-id="61062-108">Consent</span></span>
<span data-ttu-id="61062-109">Olá primeira vez que um usuário faz logon no aplicativo tooyour, será apresentada com uma tela consentimento com, semelhante toohello de abaixo, onde precisam aceitar tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="61062-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Consentimento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="61062-111">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="61062-111">Expected results</span></span>
<span data-ttu-id="61062-112">Você deve ver os resultados de saudação do tooMicrosoft chamada de API do Graph 'me' ponto de extremidade usado tootooobtain perfil de usuário Olá - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="61062-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="61062-113">Para obter uma lista de pontos de extremidade comuns do Microsoft Graph, consulte este [artigo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="61062-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="61062-114">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="61062-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="61062-115">Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo.</span><span class="sxs-lookup"><span data-stu-id="61062-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="61062-116">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="61062-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="61062-117">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="61062-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="61062-118">Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária.</span><span class="sxs-lookup"><span data-stu-id="61062-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="61062-119">Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilentAsync` chamar.</span><span class="sxs-lookup"><span data-stu-id="61062-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="61062-120">usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.</span><span class="sxs-lookup"><span data-stu-id="61062-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
