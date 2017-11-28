---
title: "aaaTroubleshooting a associação dinâmica de grupos | Microsoft Docs"
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
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a><span data-ttu-id="a317f-103">Solucionando problemas de associações dinâmicas a grupos</span><span class="sxs-lookup"><span data-stu-id="a317f-103">Troubleshooting dynamic memberships for groups</span></span>
<span data-ttu-id="a317f-104">**Configurei uma regra em um grupo, mas nenhuma associação foi atualizada no grupo de saudação**</span><span class="sxs-lookup"><span data-stu-id="a317f-104">**I configured a rule on a group but no memberships get updated in hello group**</span></span><br/><span data-ttu-id="a317f-105">Verifique se esse Olá **Habilitar gerenciamento de grupo de delegado** configuração está definida muito**Sim** em Olá **configurar** guia. Você verá essa configuração somente se você estiver conectado como um toowhom usuário uma licença Azure Active Directory Premium é atribuído.</span><span class="sxs-lookup"><span data-stu-id="a317f-105">Verify that hello **Enable delegated group management** setting is set too**Yes** in hello **Configure** tab. You will see this setting only if you are signed in as a user toowhom an Azure Active Directory Premium license is assigned.</span></span> <span data-ttu-id="a317f-106">Verifique Olá valores para atributos de usuário na regra Olá: há usuários que atendem Olá regra?</span><span class="sxs-lookup"><span data-stu-id="a317f-106">Verify hello values for user attributes on hello rule: are there users that satisfy hello rule?</span></span>

<span data-ttu-id="a317f-107">**Configurei uma regra, mas agora os membros existentes de saudação da regra de saudação são removidos**</span><span class="sxs-lookup"><span data-stu-id="a317f-107">**I configured a rule, but now hello existing members of hello rule are removed**</span></span><br/><span data-ttu-id="a317f-108">Este comportamento é esperado.</span><span class="sxs-lookup"><span data-stu-id="a317f-108">This is expected behavior.</span></span> <span data-ttu-id="a317f-109">Membros existentes do grupo de saudação são removidos quando uma regra é habilitada ou alterada.</span><span class="sxs-lookup"><span data-stu-id="a317f-109">Existing members of hello group are removed when a rule is enabled or changed.</span></span> <span data-ttu-id="a317f-110">os usuários de saudação retornados da avaliação de regra de saudação são adicionados como grupo de toohello de membros.</span><span class="sxs-lookup"><span data-stu-id="a317f-110">hello users returned from evaluation of hello rule are added as members toohello group.</span></span>     

<span data-ttu-id="a317f-111">**Não vejo as alterações da associação instantaneamente quando adiciono ou altero uma regra, por que não?**</span><span class="sxs-lookup"><span data-stu-id="a317f-111">**I don’t see membership changes instantly when I add or change a rule, why not?**</span></span><br/><span data-ttu-id="a317f-112">A avaliação de associação dedicada é feita periodicamente em um processo assíncrono em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a317f-112">Dedicated membership evaluation is done periodically in an asynchronous background process.</span></span> <span data-ttu-id="a317f-113">Quanto tempo Olá processo usa é determinado pelo número de saudação de usuários em seu diretório e Olá o tamanho de grupo Olá criado como resultado de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="a317f-113">How long hello process takes is determined by hello number of users in your directory and hello size of hello group created as a result of hello rule.</span></span> <span data-ttu-id="a317f-114">Normalmente, os diretórios com um número pequeno de usuários verá alterações de associação de grupo de saudação em menos de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a317f-114">Typically, directories with small numbers of users will see hello group membership changes in less than a few minutes.</span></span> <span data-ttu-id="a317f-115">Diretórios com um grande número de usuários podem levar 30 minutos ou mais toopopulate.</span><span class="sxs-lookup"><span data-stu-id="a317f-115">Directories with a large number of users can take 30 minutes or longer toopopulate.</span></span>

### <a name="next-steps"></a><span data-ttu-id="a317f-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a317f-116">Next steps</span></span>
<span data-ttu-id="a317f-117">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a317f-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a317f-118">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a317f-118">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a317f-119">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a317f-119">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a317f-120">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="a317f-120">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a317f-121">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a317f-121">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
