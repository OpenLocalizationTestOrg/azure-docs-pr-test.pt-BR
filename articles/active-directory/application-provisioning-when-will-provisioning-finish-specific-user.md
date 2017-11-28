---
title: "aaaFind-out quando um usuário específico será capaz de tooaccess um aplicativo | Microsoft Docs"
description: "Como toofind-out quando um usuário criticamente importante ser capaz de tooaccess um aplicativo que você tiver configurado para provisionamento do usuário com o Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="a8b65-103">Descobrir quando um usuário específico será capaz de tooaccess um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8b65-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="a8b65-104">Ao usar o provisionamento automático de usuário com um aplicativo, o Azure AD automaticamente provisionar e atualizar contas de usuário em um aplicativo com base em coisas como [atribuição de usuário e grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) em um intervalo de tempo agendado regularmente, normalmente a cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="a8b65-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="a8b65-105">Quanto tempo demora?</span><span class="sxs-lookup"><span data-stu-id="a8b65-105">How long does it take?</span></span>

<span data-ttu-id="a8b65-106">tempo de saudação que leva para um toobe de determinado usuário provisionado depende principalmente se já tiver ocorrido uma sincronização inicial de "full".</span><span class="sxs-lookup"><span data-stu-id="a8b65-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="a8b65-107">Olá primeira sincronização entre o AD do Azure e um aplicativo pode demorar horas tooseveral de 20 minutos, dependendo do tamanho de saudação do diretório de saudação do AD do Azure e número de saudação de usuários em escopo para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="a8b65-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="a8b65-108">As sincronizações subsequentes após a sincronização inicial de saudação ser mais rápido (por exemplo, em 10 minutos), como Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial hello, melhorando o desempenho de sincronizações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="a8b65-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="a8b65-109">Como toocheck Olá status de um usuário</span><span class="sxs-lookup"><span data-stu-id="a8b65-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="a8b65-110">status de provisionamento toosee Olá para um usuário selecionado, consulte Olá os logs de auditoria no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8b65-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="a8b65-111">Olá provisionamento logs de auditoria pode ser acessada no hello portal do Azure, na Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[nome do aplicativo\] &gt; Logs de auditoria**guia. Saudação de filtro logon Olá **provisionamento de conta** tooonly categoria consulte Olá provisionamento eventos para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8b65-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="a8b65-112">Você pode procurar usuários com base em hello "correspondência ID" que foi configurado para eles nos mapeamentos de atributo hello.</span><span class="sxs-lookup"><span data-stu-id="a8b65-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="a8b65-113">Por exemplo, se você configurou hello "user principal name" ou "endereço de email" como Olá correspondência de atributo no lado de saudação do AD do Azure e não sendo provisionamento de usuário de saudação tem um valor de "audrey@contoso.com", em seguida, os logs de auditoria de saudação de pesquisa para"audrey@contoso.com" e, em seguida, examine as entradas são retornadas.</span><span class="sxs-lookup"><span data-stu-id="a8b65-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="a8b65-114">Olá provisionamento auditoria registra registro todas Olá operações executadas pelo Olá provisionamento de serviço, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a8b65-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="a8b65-115">Consultando o Azure AD para usuários atribuídos que estão no escopo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="a8b65-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="a8b65-116">Consultando o aplicativo de destino Olá existência Olá desses usuários</span><span class="sxs-lookup"><span data-stu-id="a8b65-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="a8b65-117">Comparando objetos de usuário Olá entre sistema Olá</span><span class="sxs-lookup"><span data-stu-id="a8b65-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="a8b65-118">Adicionar, atualizar ou desabilitar a conta de usuário de saudação no sistema de destino de saudação com base em comparação de saudação</span><span class="sxs-lookup"><span data-stu-id="a8b65-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b65-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8b65-119">Next steps</span></span>
<span data-ttu-id="a8b65-120">[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'</span><span class="sxs-lookup"><span data-stu-id="a8b65-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
