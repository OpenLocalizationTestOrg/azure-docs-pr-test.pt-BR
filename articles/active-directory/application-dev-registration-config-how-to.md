---
title: "Como selecionar permissões para uma API | Microsoft Docs"
description: "Como localizar os pontos de extremidade de autenticação para um aplicativo personalizado que você está desenvolvendo ou registrando com o Azure AD."
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="127a3-103">Como selecionar permissões para uma API</span><span class="sxs-lookup"><span data-stu-id="127a3-103">How to select permissions for a given API</span></span>

<span data-ttu-id="127a3-104">Você pode encontrar os pontos de extremidade de autenticação para seu aplicativo no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="127a3-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="127a3-105">Navegue até o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="127a3-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="127a3-106">No painel de navegação esquerdo, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="127a3-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="127a3-107">Clique em **Registros do Aplicativo** e escolha **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="127a3-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="127a3-108">Isso abre a página **Pontos de Extremidade**, que lista todos os pontos de extremidade de autenticação de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="127a3-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="127a3-109">Use o ponto de extremidade específico ao protocolo de autenticação que você está usando, em conjunto com a ID do aplicativo, para criar a solicitação de autenticação específica ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="127a3-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="127a3-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="127a3-110">Next steps</span></span>
[<span data-ttu-id="127a3-111">Guia do desenvolvedor do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="127a3-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
