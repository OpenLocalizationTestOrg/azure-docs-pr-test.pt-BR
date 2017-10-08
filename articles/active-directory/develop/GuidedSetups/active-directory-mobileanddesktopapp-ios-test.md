---
title: "aaaAzure AD v2 iOS guia de Introdução - teste | Microsoft Docs"
description: Como aplicativos iOS (Swift) podem chamar uma API que exige tokens de acesso pelo ponto de extremidade do Azure Active Directory v2
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="6b591-103">Testar consulta Olá Microsoft Graph API do seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="6b591-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="6b591-104">Pressione `Command`  +  `R` toorun código de saudação no simulador hello.</span><span class="sxs-lookup"><span data-stu-id="6b591-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="6b591-106">Quando você estiver pronto tootest, toque em *'Chamar Microsoft Graph API'* e você será solicitado tootype seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6b591-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="6b591-107">Consentimento</span><span class="sxs-lookup"><span data-stu-id="6b591-107">Consent</span></span>
<span data-ttu-id="6b591-108">Olá primeira vez que você entrar no aplicativo tooyour, você verá uma tela consentimento com, semelhante toohello de abaixo, onde você precisa aceitar tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="6b591-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Tela de consentimento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="6b591-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="6b591-110">Expected results</span></span>
<span data-ttu-id="6b591-111">Você deve ver as informações de perfil do usuário retornadas pela chamada de API do Graph Microsoft hello em hello *log* seção.</span><span class="sxs-lookup"><span data-stu-id="6b591-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="6b591-112">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="6b591-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="6b591-113">Olá Microsoft Graph API requer Olá `user.read` tooread Olá perfil de usuário do escopo.</span><span class="sxs-lookup"><span data-stu-id="6b591-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="6b591-114">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="6b591-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="6b591-115">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="6b591-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="6b591-116">Por exemplo, para o Microsoft Graph, Olá escopo `Calendars.Read` é calendários do usuário de saudação toolist necessária.</span><span class="sxs-lookup"><span data-stu-id="6b591-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="6b591-117">Em ordem tooaccess Olá calendário do usuário em um contexto de um aplicativo, você precisa Olá tooadd `Calendars.Read` delegado informações do registro do aplicativo permissão toohello e adicione Olá `Calendars.Read` toohello escopo `acquireTokenSilent` chamar.</span><span class="sxs-lookup"><span data-stu-id="6b591-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="6b591-118">usuário Olá pode ser solicitado para consente adicionais que você aumenta o número de saudação de escopos.</span><span class="sxs-lookup"><span data-stu-id="6b591-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



