---
title: aplicativos aaaProvisioning com filtros de escopo | Microsoft Docs
description: "Saiba como os filtros de escopo toouse tooprevent objetos em aplicativos que dão suporte ao provisionamento automatizado de usuários, na verdade, está sendo provisionado se um objeto não atender às suas necessidades de negócios."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="ca9fb-103">Provisionamento de aplicativo com base em atributo com filtros de escopo</span><span class="sxs-lookup"><span data-stu-id="ca9fb-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="ca9fb-104">Olá objetivo desta seção é tooexplain como toouse escopo filtra toodefine com base em atributo regras que determinam quais usuários são provisionados toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-104">hello objective of this section is tooexplain how toouse scoping filters toodefine attribute-based rules that determine which users are provisioned toohello application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="ca9fb-105">Cláusulas e grupos de escopo</span><span class="sxs-lookup"><span data-stu-id="ca9fb-105">Clauses and Scope Groups</span></span>
![Filtro de Escopo][1] 

<span data-ttu-id="ca9fb-107">Filtros de escopo são definidos por um ou mais **grupos de escopo** e cada um deles contém uma ou mais **cláusulas**.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="ca9fb-108">cláusulas de saudação toosee para um grupo de escopo específico, expandi-lo clicando em Olá seta à esquerda da toohello saudação do nome do grupo.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-108">toosee hello clauses for a particular scope group, expand it by clicking hello arrow toohello left of hello group name.</span></span>

<span data-ttu-id="ca9fb-109">Um **cláusula** determina quais usuários podem toopass por meio de saudação filtro de escopo, avaliando os atributos de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-109">A **clause** determines which users are allowed toopass through hello scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="ca9fb-110">Por exemplo, você pode ter uma cláusula que requer que 'estado' atributo igual Nova York um usuário, para que somente os usuários de Nova York serão provisionados no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into hello application.</span></span>

![Nome do grupo de escopo][2] 

<span data-ttu-id="ca9fb-112">Cada **grupo de escopo** inicia com um obrigatório **cláusula**, conforme mostrado na captura de tela de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-112">Each **scope group** starts with one mandatory **clause**, as shown in hello screenshot above.</span></span> <span data-ttu-id="ca9fb-113">Essa cláusula declara que o usuário Olá deve ser atribuído primeiro aplicativo toohello antes de ser avaliado pelos filtros de escopo.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-113">This clause simply states that hello user must first be assigned toohello application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="ca9fb-114">Essa cláusula não pode ser excluída nem modificada.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="ca9fb-115">Você pode adicionar novas cláusulas ou novos grupos de escopo, pressionando o botão adequado hello.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-115">You can add new clauses or new scope groups by pressing hello appropriate button.</span></span> <span data-ttu-id="ca9fb-116">Você pode dar um nome a cada grupo de escopo editando sua propriedade **Nome do Grupo de Escopo** .</span><span class="sxs-lookup"><span data-stu-id="ca9fb-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="ca9fb-117">Como os filtros de escopo são avaliados</span><span class="sxs-lookup"><span data-stu-id="ca9fb-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="ca9fb-118">Durante o provisionamento, podemos testar cada usuário atribuído em relação a seu escopo toodetermine de filtros, se esse usuário merece acesso toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-118">During provisioning, we test every assigned user against your scoping filters toodetermine if that user deserves access toohello application.</span></span> <span data-ttu-id="ca9fb-119">Você pode pensar em cada cláusula como sendo um teste que deve ser passado para Olá usuário tooavoid ser filtrado.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-119">You can think of each clause as being a test that must be passed in order for hello user tooavoid getting filtered out.</span></span> 

<span data-ttu-id="ca9fb-120">Se você tiver vários grupos de escopo definidos, cada usuário deve passar pelo menos um deles tooaccess aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-120">If you have multiple scope groups defined, each user must pass at least one of them tooaccess hello application.</span></span> <span data-ttu-id="ca9fb-121">Em cada grupo de escopo, no entanto, Olá usuário deve passar cada cláusula toopass desse grupo de escopo específico.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-121">Within each scope group, however, hello user must pass every clause toopass that specific scope group.</span></span> 

<span data-ttu-id="ca9fb-122">Em outras palavras, você pode pensar como os grupos sendo OR juntos, e você pode pensar em cláusulas de saudação dentro deles como sendo AND juntos.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-122">In other words, you can think of scope groups as being OR’d together, and you can think of hello clauses within them as being AND’d together.</span></span> <span data-ttu-id="ca9fb-123">Por exemplo, considere Olá abaixo do filtro de escopo:</span><span class="sxs-lookup"><span data-stu-id="ca9fb-123">For example, consider hello scoping filter below:</span></span>

![Nome do grupo de escopo][3]  

<span data-ttu-id="ca9fb-125">De acordo com toothis filtro de escopo, os usuários devem atender a seguir Olá critérios, toobe provisionado:</span><span class="sxs-lookup"><span data-stu-id="ca9fb-125">According toothis scoping filter, users must satisfy hello following criteria, toobe provisioned:</span></span>

1. <span data-ttu-id="ca9fb-126">Eles devem ser atribuídos toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-126">They must be assigned toohello application.</span></span>
2. <span data-ttu-id="ca9fb-127">Eles devem trabalhar no departamento de engenharia Olá</span><span class="sxs-lookup"><span data-stu-id="ca9fb-127">They must work in hello Engineering department</span></span>
3. <span data-ttu-id="ca9fb-128">Eles devem trabalhar em São Francisco ou no Canadá.</span><span class="sxs-lookup"><span data-stu-id="ca9fb-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ca9fb-129">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="ca9fb-129">Related Articles</span></span>
* [<span data-ttu-id="ca9fb-130">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ca9fb-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ca9fb-131">Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos</span><span class="sxs-lookup"><span data-stu-id="ca9fb-131">Automate User Provisioning and Deprovisioning tooSaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="ca9fb-132">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="ca9fb-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="ca9fb-133">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="ca9fb-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="ca9fb-134">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="ca9fb-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="ca9fb-135">Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications</span><span class="sxs-lookup"><span data-stu-id="ca9fb-135">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="ca9fb-136">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="ca9fb-136">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
