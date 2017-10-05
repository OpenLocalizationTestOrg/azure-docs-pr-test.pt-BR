---
title: "Solução de problemas de associação dinâmica para grupos| Microsoft Docs"
description: "Solução de problemas para a associação dinâmica para grupos no Azure AD."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 32947e8cc69c9a48d9a285bf0a37ab3398571f86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="091c2-103">Solucionando problemas de associações dinâmicas a grupos</span><span class="sxs-lookup"><span data-stu-id="091c2-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="091c2-104">**Configurei uma regra em um grupo, mas nenhuma associação foi atualizada no grupo**</span><span class="sxs-lookup"><span data-stu-id="091c2-104">**I configured a rule on a group but no memberships get updated in the group**</span></span><br/><span data-ttu-id="091c2-105">Verifique se a configuração **Habilitar gerenciamento do grupo delegado** está definida para **Sim** na guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="091c2-105">Verify that the **Enable delegated group management** setting is set to **Yes** in the **Configure** tab.</span></span> <span data-ttu-id="091c2-106">Você verá essa configuração somente se estiver conectado como um usuário que recebe uma licença do Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="091c2-106">You will see this setting only if you are signed in as a user to whom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="091c2-107">Verifique os valores dos atributos de usuário na regra: há usuários que atendem à regra?</span><span class="sxs-lookup"><span data-stu-id="091c2-107">Verify the values for user attributes on the rule: are there users that satisfy the rule?</span></span>

<span data-ttu-id="091c2-108">**Configurei uma regra, mas agora os membros da regra existentes foram removidos**</span><span class="sxs-lookup"><span data-stu-id="091c2-108">**I configured a rule, but now the existing members of the rule are removed**</span></span><br/><span data-ttu-id="091c2-109">Este comportamento é esperado.</span><span class="sxs-lookup"><span data-stu-id="091c2-109">This is expected behavior.</span></span> <span data-ttu-id="091c2-110">Membros existentes do grupo são removidos quando uma regra é habilitada ou alterada.</span><span class="sxs-lookup"><span data-stu-id="091c2-110">Existing members of the group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="091c2-111">Os usuários retornados da avaliação da regra são adicionados como membros ao grupo.</span><span class="sxs-lookup"><span data-stu-id="091c2-111">The users returned from evaluation of the rule are added as members to the group.</span></span>     

<span data-ttu-id="091c2-112">**Não vejo as alterações da associação instantaneamente quando adiciono ou altero uma regra, por que não?**</span><span class="sxs-lookup"><span data-stu-id="091c2-112">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="091c2-113">A avaliação de associação dedicada é feita periodicamente em um processo assíncrono em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="091c2-113">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="091c2-114">O tempo que o processo leva é determinado pelo número de usuários no diretório e pelo tamanho do grupo criado como resultado da regra.</span><span class="sxs-lookup"><span data-stu-id="091c2-114">How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule.</span></span> <span data-ttu-id="091c2-115">Normalmente, os diretórios com um pequeno número de usuários verão as alterações de associação de grupo em poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="091c2-115">Typically, directories with small numbers of users will see the group membership changes in less than a few minutes.</span></span> <span data-ttu-id="091c2-116">Os diretórios com um grande número de usuários podem levar até 30 minutos ou mais para serem populados.</span><span class="sxs-lookup"><span data-stu-id="091c2-116">Directories with a large number of users can take 30 minutes or longer to populate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="091c2-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="091c2-117">Next steps</span></span>
<span data-ttu-id="091c2-118">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="091c2-118">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="091c2-119">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="091c2-119">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="091c2-120">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="091c2-120">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="091c2-121">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="091c2-121">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="091c2-122">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="091c2-122">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
