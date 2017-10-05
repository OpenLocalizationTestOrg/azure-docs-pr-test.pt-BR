---
title: "Descubra quando um usuário específico será capaz de acessar um aplicativo | Microsoft Docs"
description: "Como saber quando um usuário extremamente importante é capaz de acessar um aplicativo que você configurou para o provisionamento do usuário com o Azure AD"
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
ms.openlocfilehash: fcefb31904cfb77022db0358e9feee6a0479db81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a><span data-ttu-id="03333-103">Descubra quando um usuário específico será capaz de acessar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="03333-103">Find out when a specific user will be able to access an application</span></span>
<span data-ttu-id="03333-104">Ao usar o provisionamento automático de usuário com um aplicativo, o Azure AD automaticamente provisionar e atualizar contas de usuário em um aplicativo com base em coisas como [atribuição de usuário e grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) em um intervalo de tempo agendado regularmente, normalmente a cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="03333-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="03333-105">Quanto tempo demora?</span><span class="sxs-lookup"><span data-stu-id="03333-105">How long does it take?</span></span>

<span data-ttu-id="03333-106">O tempo necessário para que um determinado usuário seja provisionado depende principalmente se uma sincronização "completa" inicial já ocorreu.</span><span class="sxs-lookup"><span data-stu-id="03333-106">The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="03333-107">A primeira sincronização entre o Azure AD e um aplicativo pode levar de 20 minutos até várias horas, dependendo do tamanho do diretório do Azure AD e o número de usuários no escopo para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="03333-107">The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="03333-108">Sincronizações subsequentes após a sincronização inicial ser mais rápido (por exemplo, em 10 minutos), como o serviço de provisionamento armazena as marcas d'água que representam o estado dos dois sistemas após a sincronização inicial, melhorando o desempenho de sincronizações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="03333-108">Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-check-the-status-of-a-user"></a><span data-ttu-id="03333-109">Como verificar o status de um usuário</span><span class="sxs-lookup"><span data-stu-id="03333-109">How to check the status of a user</span></span>

<span data-ttu-id="03333-110">Para ver o status de provisionamento para um usuário selecionado, consulte os logs de auditoria no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03333-110">To see the provisioning status for a selected user, consult the Audit logs in Azure AD.</span></span>

<span data-ttu-id="03333-111">Os logs de auditoria de provisionamento podem ser acessados no portal do Azure, na guia **Azure Active Directory &gt; Aplicativos Empresariais &gt; \[Nome do Aplicativo\] &gt; Logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="03333-111">The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab.</span></span> <span data-ttu-id="03333-112">Filtre os logs na categoria de **provisionamento de conta**, para ver apenas os eventos de provisionamento para aquele aplicativo.</span><span class="sxs-lookup"><span data-stu-id="03333-112">Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app.</span></span> <span data-ttu-id="03333-113">Você pode procurar por usuários com base na "ID correspondente" que foi configurado para eles nos mapeamentos de atributo.</span><span class="sxs-lookup"><span data-stu-id="03333-113">You can search for users based on the “matching ID” that was configured for them in the attribute mappings.</span></span> 

<span data-ttu-id="03333-114">Por exemplo, se você configurou o "nome UPN" ou "endereço de email" como o atributo correspondente no lado do Azure AD e o usuário não sendo provisionado tem um valor de "audrey@contoso.com", em seguida, pesquise os logs de auditoria para "audrey@contoso.com" e reveja as entradas retornadas.</span><span class="sxs-lookup"><span data-stu-id="03333-114">For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="03333-115">Os logs de auditoria de provisionamento registram todas as operações executadas pelo serviço de provisionamento, incluindo:</span><span class="sxs-lookup"><span data-stu-id="03333-115">The provisioning audit logs record all the operations performed by the provisioning service, including:</span></span>

* <span data-ttu-id="03333-116">Consultando o Azure AD para usuários atribuídos que estão no escopo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="03333-116">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="03333-117">Consultando o aplicativo de destino para a existência desses usuários</span><span class="sxs-lookup"><span data-stu-id="03333-117">Querying the target app for the existence of those users</span></span>
* <span data-ttu-id="03333-118">Comparando objetos de usuário entre o sistema</span><span class="sxs-lookup"><span data-stu-id="03333-118">Comparing the user objects between the system</span></span>
* <span data-ttu-id="03333-119">Adicionar, atualizar ou desabilitar a conta de usuário no sistema de destino com base na comparação</span><span class="sxs-lookup"><span data-stu-id="03333-119">Adding, updating, or disabling the user account in the target system based on the comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="03333-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03333-120">Next steps</span></span>
<span data-ttu-id="03333-121">[Automatizar o provisionamento e desprovisionamento de usuários para aplicativos SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="03333-121">[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
