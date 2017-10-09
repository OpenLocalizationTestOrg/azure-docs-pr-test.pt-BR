---
title: "aplicativo personalizado aaaHow toogrant permissões tooa | Microsoft Docs"
description: "Como toogrant permissões tooyour personalizado usando o aplicativo hello portal do AD do Azure ou um parâmetro de URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="57c51-103">Como toogrant permissões tooa personalizado aplicativo</span><span class="sxs-lookup"><span data-stu-id="57c51-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="57c51-104">Se quiser toogrant consentimento preventivamente no seu aplicativo ou em execução em um erro se você não tiver consentido tooan aplicativo, tente essas etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="57c51-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="57c51-105">Como tooperform consentimento do administrador para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="57c51-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="57c51-106">Isso tem o efeito de saudação de concessão de autorização toohello aplicativo para todos os usuários em sua organização.</span><span class="sxs-lookup"><span data-stu-id="57c51-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="57c51-107">Navegue toohello **registros do aplicativo** folha como uma **administrador global**, em seguida, selecione aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="57c51-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="57c51-108">Selecione **permissões necessárias**e finalmente chegar Olá **conceder permissões** botão na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="57c51-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="57c51-109">Como alternativa, você pode construir uma solicitação muito*login.microsoftonline.com* com suas configurações de aplicativo e acrescente em *& prompt = admin\_consentimento*.</span><span class="sxs-lookup"><span data-stu-id="57c51-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="57c51-110">Depois de entrar com credenciais de administrador, Olá aplicativo recebeu consentimento para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="57c51-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="57c51-111">Como tooforce consentimento do usuário para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="57c51-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="57c51-112">Acrescentar para solicitações de autenticação *& prompt = consentimento* que exigir que os usuários finais tooconsent cada vez que eles se autenticam.</span><span class="sxs-lookup"><span data-stu-id="57c51-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57c51-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57c51-113">Next steps</span></span>

[<span data-ttu-id="57c51-114">TooAzureAD consentimento e integração de aplicativos</span><span class="sxs-lookup"><span data-stu-id="57c51-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="57c51-115">Consentimento e permissão para aplicativos convergidos do AzureAD v2.0</span><span class="sxs-lookup"><span data-stu-id="57c51-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="57c51-116">StackOverflow do AzureAD</span><span class="sxs-lookup"><span data-stu-id="57c51-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
