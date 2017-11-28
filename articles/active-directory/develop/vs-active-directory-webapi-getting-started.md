---
title: "Introdução ao Azure AD em projetos WebApi do Visual Studio | Microsoft Docs"
description: "Como começar a usar o Active Directory do Azure em projetos da API Web após a conexão ou criação de um AD do Azure usando os serviços conectados do Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="8fc0c-103">Introdução ao Active Directory do Azure e aos serviços conectados do Visual Studio (projetos da API Web)</span><span class="sxs-lookup"><span data-stu-id="8fc0c-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fc0c-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="8fc0c-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="8fc0c-105">O que aconteceu</span><span class="sxs-lookup"><span data-stu-id="8fc0c-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="8fc0c-106">Exigir autenticação para acessar os controladores</span><span class="sxs-lookup"><span data-stu-id="8fc0c-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="8fc0c-107">Todos os controladores em seu projeto foram marcados com o atributo **Autorizar** .</span><span class="sxs-lookup"><span data-stu-id="8fc0c-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="8fc0c-108">Este atributo exige que o usuário seja autenticado antes de acessar as APIs definidas por esses controladores.</span><span class="sxs-lookup"><span data-stu-id="8fc0c-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="8fc0c-109">Para permitir que o controlador seja acessado anonimamente, remova este atributo do controlador.</span><span class="sxs-lookup"><span data-stu-id="8fc0c-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="8fc0c-110">Se desejar definir as permissões em um nível mais granular, aplique o atributo a cada método que necessita de autorização em vez de aplicá-lo à classe do controlador.</span><span class="sxs-lookup"><span data-stu-id="8fc0c-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc0c-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fc0c-111">Next steps</span></span>
[<span data-ttu-id="8fc0c-112">Saiba mais sobre o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8fc0c-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

