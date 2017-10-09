---
title: "aaaUser Provisionando o aplicativo de galeria tooan AD do Azure está levando horas ou mais | Microsoft Docs"
description: Como toofind out por que o provisionamento de aplicativo tooyour pode estar demorando mais tempo do que esperado
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="2fb90-103">Provisionamento de aplicativo da Galeria de tooan AD do Azure do usuário está levando horas ou mais</span><span class="sxs-lookup"><span data-stu-id="2fb90-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="2fb90-104">Quando é preciso habilitar o provisionamento automático para um aplicativo, a sincronização inicial Olá pode levar de horas de tooseveral de 20 minutos, dependendo do tamanho de Olá Olá diretório AD do Azure e o número de saudação de usuários em escopo para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="2fb90-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="2fb90-105">As sincronizações subsequentes após a sincronização inicial Olá ser mais rápido, Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial hello, melhorando o desempenho de sincronizações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="2fb90-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="2fb90-106">Como tooimprove provisionamento de desempenho</span><span class="sxs-lookup"><span data-stu-id="2fb90-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="2fb90-107">Se a sincronização inicial hello está demorando mais do que algumas horas, há algo que você pode fazer tooimprove desempenho:</span><span class="sxs-lookup"><span data-stu-id="2fb90-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="2fb90-108">**Filtros de escopo de usuário.**</span><span class="sxs-lookup"><span data-stu-id="2fb90-108">**User scoping filters.**</span></span> <span data-ttu-id="2fb90-109">Filtros de escopo permitem toofine ajustar dados de Olá Olá extrai provisionamento de serviço do AD do Azure, filtrando usuários com base em valores de atributo específicos.</span><span class="sxs-lookup"><span data-stu-id="2fb90-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="2fb90-110">Para obter mais informações sobre filtros de escopo, consulte [provisionamento de aplicativos com base em atributo com filtros de escopo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="2fb90-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fb90-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fb90-111">Next steps</span></span>
[<span data-ttu-id="2fb90-112">Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="2fb90-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

