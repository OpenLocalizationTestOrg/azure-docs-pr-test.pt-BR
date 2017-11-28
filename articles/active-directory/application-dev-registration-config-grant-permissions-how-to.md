---
title: "Como conceder permissões a um aplicativo personalizado | Microsoft Docs"
description: "Como conceder permissões a seu aplicativo personalizado usando o portal do Azure AD ou um parâmetro de URL"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="718c3-103">Como conceder permissões a um aplicativo personalizado</span><span class="sxs-lookup"><span data-stu-id="718c3-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="718c3-104">Para dar consentimento de forma preventiva em seu aplicativo ou se você estiver encontrado um erro afirmando que você não consentiu com um aplicativo, tente as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="718c3-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="718c3-105">Como executar consentimento de administrador em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="718c3-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="718c3-106">Isso tem o efeito de dar consentimento ao aplicativo para todos os usuários na organização.</span><span class="sxs-lookup"><span data-stu-id="718c3-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="718c3-107">Navegue até a folha **Registros do aplicativo** como um **administrador global** e selecione o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="718c3-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="718c3-108">Selecione **Permissões Necessárias** e toque no botão **Conceder Permissões** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="718c3-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="718c3-109">Como alternativa, você pode construir uma solicitação para *login.microsoftonline.com* com as configurações do seu aplicativo e anexar um consentimento *&prompt=admin\_*.</span><span class="sxs-lookup"><span data-stu-id="718c3-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="718c3-110">Após entrar com credenciais de administrador, o aplicativo recebe consentimento para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="718c3-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="718c3-111">Como forçar o consentimento de usuário em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="718c3-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="718c3-112">Anexe nas solicitações de autenticação *&prompt=consent*, que exige o consentimento dos usuários finais cada vez que eles se autenticam.</span><span class="sxs-lookup"><span data-stu-id="718c3-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="718c3-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="718c3-113">Next steps</span></span>

[<span data-ttu-id="718c3-114">Consentir e integrar aplicativos ao AzureAD</span><span class="sxs-lookup"><span data-stu-id="718c3-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="718c3-115">Consentimento e permissão para aplicativos convergidos do AzureAD v2.0</span><span class="sxs-lookup"><span data-stu-id="718c3-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="718c3-116">StackOverflow do AzureAD</span><span class="sxs-lookup"><span data-stu-id="718c3-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
