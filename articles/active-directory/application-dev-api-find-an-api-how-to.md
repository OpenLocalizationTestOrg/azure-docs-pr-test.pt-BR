---
title: "Como localizar uma API específica necessária para um aplicativo personalizado | Microsoft Docs"
description: "Como configurar as permissões que você precisa para acessar uma API em particular em seu aplicativo personalizado do Azure AD"
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="fe11c-103">Como localizar uma API específica necessária para um aplicativo personalizado</span><span class="sxs-lookup"><span data-stu-id="fe11c-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="fe11c-104">O acesso às APIs exigem configuração de escopos de acesso e funções.</span><span class="sxs-lookup"><span data-stu-id="fe11c-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="fe11c-105">Se você quiser expor suas APIs web do aplicativo de recursos para aplicativos cliente, precisará configurar escopos de acesso e funções da API.</span><span class="sxs-lookup"><span data-stu-id="fe11c-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="fe11c-106">Se desejar que um aplicativo cliente acesse uma API web, você precisará configurar permissões para acessar a API no registro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe11c-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="fe11c-107">Configurando um aplicativo de recurso para expor APIs Web</span><span class="sxs-lookup"><span data-stu-id="fe11c-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="fe11c-108">Quando você expõe sua API web, a API é exibida na lista **Selecionar uma API** ao adicionar permissões a um registro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe11c-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="fe11c-109">Para adicionar escopos de acesso, siga as etapas descritas em [Adicionando escopos de acesso ao seu aplicativo de recurso](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="fe11c-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="fe11c-110">Configurando um aplicativo cliente para acessar APIs Web</span><span class="sxs-lookup"><span data-stu-id="fe11c-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="fe11c-111">Quando você adiciona permissões em seu registro de aplicativo, você pode **Adicionar acesso à API** para APIs web expostas.</span><span class="sxs-lookup"><span data-stu-id="fe11c-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="fe11c-112">Para acessar APIs web, siga as etapas descritas em [Adicionar credenciais ou permissões para acessar APIs web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="fe11c-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe11c-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe11c-113">Next steps</span></span>

-   [<span data-ttu-id="fe11c-114">Integrando aplicativos com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fe11c-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="fe11c-115">Noções básicas sobre o manifesto de aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe11c-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


