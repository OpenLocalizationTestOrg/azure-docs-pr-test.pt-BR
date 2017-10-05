---
title: "Introdução ao iOS no Azure AD v2 – Teste | Microsoft Docs"
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
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="8d8ac-103">Testar a consulta da API do Microsoft Graph de seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="8d8ac-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="8d8ac-104">Pressione `Command` + `R` para executar o código no simulador.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Captura de tela de exemplo](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="8d8ac-106">Quando estiver pronto para testar, toque em *“Chamar API do Microsoft Graph”* e você será solicitado a digitar seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="8d8ac-107">Consentimento</span><span class="sxs-lookup"><span data-stu-id="8d8ac-107">Consent</span></span>
<span data-ttu-id="8d8ac-108">Na primeira vez que você entrar no aplicativo, será apresentada uma tela de consentimento semelhante à tela abaixo, na qual você precisa aceitar explicitamente:</span><span class="sxs-lookup"><span data-stu-id="8d8ac-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Tela de consentimento](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="8d8ac-110">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="8d8ac-110">Expected results</span></span>
<span data-ttu-id="8d8ac-111">Você deverá ver as informações de perfil do usuário retornadas pela chamada à API do Microsoft Graph na seção *Registro em Log*.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="8d8ac-112">Mais informações sobre escopos e permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="8d8ac-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="8d8ac-113">A API do Microsoft Graph requer o escopo `user.read` para ler o perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="8d8ac-114">Esse escopo é adicionado automaticamente, por padrão, a cada aplicativo que é registrado em nosso portal de registro.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="8d8ac-115">Algumas outras APIs do Microsoft Graph, bem como APIs personalizadas do servidor de back-end, podem exigir escopos adicionais.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="8d8ac-116">Por exemplo, para o Microsoft Graph, o escopo `Calendars.Read` é necessário para listar os calendários do usuário.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="8d8ac-117">Para acessar o calendário do usuário no contexto de um aplicativo, é necessário adicionar a permissão delegada `Calendars.Read` às informações de registro do aplicativo e, em seguida, adicionar o escopo `Calendars.Read` à chamada `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="8d8ac-118">Talvez o usuário precise fornecer consentimentos adicionais à medida que o número de escopos aumentar.</span><span class="sxs-lookup"><span data-stu-id="8d8ac-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



