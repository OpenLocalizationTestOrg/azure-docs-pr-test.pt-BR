---
title: Provisionar aplicativos com filtros de escopo | Microsoft Docs
description: "Saiba como usar filtros de escopo para impedir que objetos em aplicativos, que dão suporte a provisionamento automatizado de usuários, sejam provisionados, caso um objeto não satisfaça suas necessidades de negócios."
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="b5850-103">Provisionamento de aplicativo com base em atributo com filtros de escopo</span><span class="sxs-lookup"><span data-stu-id="b5850-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="b5850-104">O objetivo desta seção é explicar como usar filtros de escopo para definir regras baseadas em atributo que determinam quais usuários serão provisionados ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5850-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="b5850-105">Cláusulas e grupos de escopo</span><span class="sxs-lookup"><span data-stu-id="b5850-105">Clauses and Scope Groups</span></span>
![Filtro de Escopo][1] 

<span data-ttu-id="b5850-107">Filtros de escopo são definidos por um ou mais **grupos de escopo** e cada um deles contém uma ou mais **cláusulas**.</span><span class="sxs-lookup"><span data-stu-id="b5850-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="b5850-108">Para ver as cláusulas de determinado grupo de escopo, expanda-o clicando na seta à esquerda do nome do grupo.</span><span class="sxs-lookup"><span data-stu-id="b5850-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="b5850-109">Uma **cláusula** determina quais usuários têm permissão para passar pelo filtro de escopo, avaliando os atributos de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="b5850-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="b5850-110">Por exemplo, pode haver uma cláusula que requer que o atributo de “estado” de um usuário seja igual a Nova York, somente os usuários de Nova York serão provisionados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5850-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Nome do grupo de escopo][2] 

<span data-ttu-id="b5850-112">Cada **grupo de escopo** começa com uma **cláusula** obrigatória, conforme mostrado na captura de tela acima.</span><span class="sxs-lookup"><span data-stu-id="b5850-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="b5850-113">Essa cláusula simplesmente informa que o usuário deve primeiro ser atribuído ao aplicativo antes de ser avaliado por seus filtros de escopo.</span><span class="sxs-lookup"><span data-stu-id="b5850-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="b5850-114">Essa cláusula não pode ser excluída nem modificada.</span><span class="sxs-lookup"><span data-stu-id="b5850-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="b5850-115">Você pode adicionar novas cláusulas ou novos grupos de escopo, pressionando o botão adequado.</span><span class="sxs-lookup"><span data-stu-id="b5850-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="b5850-116">Você pode dar um nome a cada grupo de escopo editando sua propriedade **Nome do Grupo de Escopo** .</span><span class="sxs-lookup"><span data-stu-id="b5850-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="b5850-117">Como os filtros de escopo são avaliados</span><span class="sxs-lookup"><span data-stu-id="b5850-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="b5850-118">Durante o provisionamento, testamos cada usuário atribuído em relação a seus filtros de escopo para determinar se esse usuário merece acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5850-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="b5850-119">Você pode pensar em cada cláusula como sendo um teste que o usuário deve passar para evitar ser filtrado.</span><span class="sxs-lookup"><span data-stu-id="b5850-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="b5850-120">Se houver vários grupos de escopo definidos, cada usuário deverá passar em pelo menos um deles para acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5850-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="b5850-121">Em cada grupo de escopo, no entanto, o usuário deve passar por cada cláusula a fim de passar naquele grupo de escopo específico.</span><span class="sxs-lookup"><span data-stu-id="b5850-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="b5850-122">Em outras palavras, você pode pensar nos grupos de escopo como sendo agrupados por OR e pode considerar as cláusulas dentro deles como sendo agrupadas por AND.</span><span class="sxs-lookup"><span data-stu-id="b5850-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="b5850-123">Por exemplo, considere o filtro de escopo abaixo:</span><span class="sxs-lookup"><span data-stu-id="b5850-123">For example, consider the scoping filter below:</span></span>

![Nome do grupo de escopo][3]  

<span data-ttu-id="b5850-125">De acordo com esse filtro de escopo, os usuários devem atender aos seguintes critérios para serem provisionados:</span><span class="sxs-lookup"><span data-stu-id="b5850-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="b5850-126">Eles devem ser atribuídos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b5850-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="b5850-127">Eles devem trabalhar no departamento de engenharia</span><span class="sxs-lookup"><span data-stu-id="b5850-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="b5850-128">Eles devem trabalhar em São Francisco ou no Canadá.</span><span class="sxs-lookup"><span data-stu-id="b5850-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b5850-129">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="b5850-129">Related Articles</span></span>
* [<span data-ttu-id="b5850-130">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b5850-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b5850-131">Automatizar o provisionamento e desprovisionamento de usuários para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="b5850-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="b5850-132">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="b5850-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="b5850-133">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="b5850-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="b5850-134">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="b5850-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="b5850-135">Usando o SCIM para habilitar o provisionamento automático de usuários e grupos do Active Directory do Azure para aplicativos</span><span class="sxs-lookup"><span data-stu-id="b5850-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="b5850-136">Lista de tutoriais sobre como integrar aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="b5850-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
