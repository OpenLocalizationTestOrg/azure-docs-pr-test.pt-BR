---
title: "O provisionamento do usuário para um aplicativo da Galeria do Azure AD está levando horas ou mais | Microsoft Docs"
description: "Como descobrir por que o provisionamento para seu aplicativo está demorando mais do que o esperado"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="525a1-103">O provisionamento do usuário para um aplicativo da Galeria do Azure AD está levando horas ou mais</span><span class="sxs-lookup"><span data-stu-id="525a1-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="525a1-104">Ao habilitar pela primeira vez o provisionamento automático para um aplicativo, a sincronização inicial pode levar de 20 minutos até várias horas, dependendo do tamanho do diretório do Azure AD e do número de usuários no escopo para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="525a1-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="525a1-105">Sincronizações subsequentes após a sincronização inicial são mais rápidas, uma vez que o serviço de provisionamento armazena as marcas d'água que representam o estado dos dois sistemas após a sincronização inicial, melhorando o desempenho dessas sincronizações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="525a1-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="525a1-106">Como melhorar o desempenho do provisionamento</span><span class="sxs-lookup"><span data-stu-id="525a1-106">How to improve provisioning performance</span></span>

<span data-ttu-id="525a1-107">Se a sincronização inicial estiver demorando mais do que apenas algumas horas, há algo que você pode fazer para melhorar o desempenho:</span><span class="sxs-lookup"><span data-stu-id="525a1-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="525a1-108">**Filtros de escopo de usuário.**</span><span class="sxs-lookup"><span data-stu-id="525a1-108">**User scoping filters.**</span></span> <span data-ttu-id="525a1-109">Filtros de escopo permitem ajustar os dados que o serviço de provisionamento extrai do Azure AD filtrando usuários com base em valores de atributo específicos.</span><span class="sxs-lookup"><span data-stu-id="525a1-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="525a1-110">Para obter mais informações sobre filtros de escopo, consulte [Provisionamento de aplicativos com base em atributo com filtros de escopo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="525a1-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="525a1-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="525a1-111">Next steps</span></span>
[<span data-ttu-id="525a1-112">Automatizar o provisionamento e desprovisionamento de usuários para aplicativos SaaS com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="525a1-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

