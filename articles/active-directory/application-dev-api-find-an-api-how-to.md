---
title: "aaaHow toofind uma API específica necessária para um aplicativo personalizado | Microsoft Docs"
description: "Como permissões de saudação tooconfigure necessário tooaccess uma API em particular em personalizados desenvolvidos aplicativo AD do Azure"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="6c80b-103">Como toofind uma API específica necessária para um aplicativo personalizado</span><span class="sxs-lookup"><span data-stu-id="6c80b-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="6c80b-104">Acesso tooAPIs exigem configuração de funções e escopos de acesso.</span><span class="sxs-lookup"><span data-stu-id="6c80b-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="6c80b-105">Se você quiser tooexpose seus aplicativos de tooclient APIs do recurso aplicativo da web, você precisa tooconfigure acesso escopos e funções para Olá API.</span><span class="sxs-lookup"><span data-stu-id="6c80b-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="6c80b-106">Se você quiser que um aplicativo de cliente tooaccess uma API da web, você precisa tooconfigure permissões tooaccess Olá API no registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="6c80b-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="6c80b-107">Configurando um recurso aplicativo tooexpose APIs da web</span><span class="sxs-lookup"><span data-stu-id="6c80b-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="6c80b-108">Quando você expõe a API da web, exibido no Olá Olá API **selecionar uma API** ao adicionar um registro de aplicativo tooan permissões de lista.</span><span class="sxs-lookup"><span data-stu-id="6c80b-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="6c80b-109">tooadd escopos de acesso, execute as etapas de saudação descritas em [adicionar acesso escopos do aplicativo de recurso tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="6c80b-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="6c80b-110">Configurando um cliente aplicativo tooaccess APIs da web</span><span class="sxs-lookup"><span data-stu-id="6c80b-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="6c80b-111">Quando você adiciona um registro de aplicativo tooyour permissões, você pode **adicionar acesso à API** tooexposed APIs da web.</span><span class="sxs-lookup"><span data-stu-id="6c80b-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="6c80b-112">tooaccess APIs da web, siga etapas Olá descritas em [adicionar tooaccess credenciais ou permissões de APIs da web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="6c80b-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c80b-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c80b-113">Next steps</span></span>

-   [<span data-ttu-id="6c80b-114">Integrando aplicativos com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6c80b-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="6c80b-115">Noções básicas sobre o manifesto de aplicativo do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="6c80b-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


