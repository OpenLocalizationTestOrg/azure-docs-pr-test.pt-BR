---
title: Personalizar mapeamentos de atributo do Azure AD | Microsoft Docs
description: "Saiba quais são os mapeamentos de atributo para aplicativos SaaS no Active Directory do Azure e como você pode modificá-los para atender às necessidades de negócios."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6ca2fdc9c68ea0030d938eeaebd57aafa0e2790f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="6a8fa-103">Personalizar os mapeamentos de atributos de provisionamento de usuário para aplicativos SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a8fa-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="6a8fa-104">O AD do Microsoft Azure dá suporte para provisionamento de usuário para aplicativos SaaS de terceiros, como Salesforce, Google Apps e outros.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-104">Microsoft Azure AD provides support for user provisioning to third-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="6a8fa-105">Se você tiver provisionamento de usuário para um aplicativo SaaS de terceiro habilitado, o Portal de Gerenciamento controlará seus valores de atributo na forma de uma configuração chamada "mapeamento de atributo".</span><span class="sxs-lookup"><span data-stu-id="6a8fa-105">If you have user provisioning for a third-party SaaS application enabled, the Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="6a8fa-106">Há um conjunto predefinido de mapeamentos de atributo entre objetos de usuário do AD do Azure e objetos de usuário de cada aplicativo SaaS.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="6a8fa-107">Alguns aplicativos gerenciam outros tipos de objetos, como grupos ou contatos.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="6a8fa-108">Você pode personalizar mapeamentos de atributo padrão de acordo com suas necessidades comerciais.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-108">You can customize the default attribute mappings according to your business needs.</span></span> <span data-ttu-id="6a8fa-109">Isso significa que você pode alterar ou excluir mapeamentos de atributo existentes ou criar novos mapeamentos de atributo.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="6a8fa-110">No portal do Azure AD, você pode acessar esse recurso clicando em uma configuração de **Mapeamentos** em **Provisionamento** na seção **Gerenciar** de um **Aplicativo Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-110">In the Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in the **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="6a8fa-112">Clicar em uma configuração de **Mapeamentos** abre a folha **Mapeamento de Atributo** relacionada.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-112">Clicking a **Mappings** configuration, opens the related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="6a8fa-113">Há mapeamentos de atributo que são exigidos por um aplicativo SaaS para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-113">There are attribute mappings that are required by a SaaS application to function correctly.</span></span> <span data-ttu-id="6a8fa-114">Para os atributos necessários, o recurso **Excluir** não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-114">For required attributes, the **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="6a8fa-116">No exemplo acima, você pode ver que o atributo **Username** de um objeto gerenciado no Salesforce é preenchido com o valor **userPrincipalName** do Objeto do Azure Active Directory vinculado.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-116">In the example above, you can see that the **Username** attribute of a managed object in Salesforce is populated with the **userPrincipalName** value of the linked Azure Active Directory Object.</span></span>

<span data-ttu-id="6a8fa-117">Você pode personalizar os **Mapeamentos de Atributo** existentes clicando em um mapeamento.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="6a8fa-118">Isso abre a folha **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-118">This opens the **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="6a8fa-120">Noções básicas sobre tipos de mapeamento de atributo</span><span class="sxs-lookup"><span data-stu-id="6a8fa-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="6a8fa-121">Com mapeamentos de atributo, você controla como os atributos são preenchidos em um aplicativo SaaS de terceiro.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="6a8fa-122">Há quatro tipos diferentes de mapeamento com suporte:</span><span class="sxs-lookup"><span data-stu-id="6a8fa-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="6a8fa-123">**Direto** – o atributo de destino é preenchido com o valor de um atributo do objeto vinculado no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-123">**Direct** – the target attribute is populated with the value of an attribute of the linked object in Azure AD.</span></span>
* <span data-ttu-id="6a8fa-124">**Constante** – o atributo de destino é preenchido com uma cadeia de caracteres especificada por você.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-124">**Constant** – the target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="6a8fa-125">**Expressão** – o atributo de destino é preenchido com base no resultado de uma expressão de script.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-125">**Expression** - the target attribute is populated based on the result of a script-like expression.</span></span> 
  <span data-ttu-id="6a8fa-126">Para saber mais, consulte [Escrever expressões para mapeamentos de atributo no Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="6a8fa-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="6a8fa-127">**Nenhum** – o atributo de destino é deixado inalterado.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-127">**None** - the target attribute is left unmodified.</span></span> <span data-ttu-id="6a8fa-128">No entanto, se o atributo de destino estiver vazio, ele será preenchido com o valor padrão que você especificar.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-128">However, if the target attribute is ever empty, it is populated with the Default value that you specify.</span></span>

<span data-ttu-id="6a8fa-129">Além desses quatro tipos de mapeamentos de atributo básicos, os mapeamentos de atributo personalizados dão suporte ao conceito de uma atribuição de valor **padrão** opcional.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-129">In addition to these four basic attribute mapping types, custom attribute mappings support the concept of an optional **default** value assignment.</span></span> <span data-ttu-id="6a8fa-130">A atribuição do valor padrão assegura que um atributo de destino seja preenchido com um valor, se não houver um valor no AD do Azure nem no objeto de destino.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-130">The default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on the target object.</span></span> <span data-ttu-id="6a8fa-131">A configuração mais comum é deixar isso em branco.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-131">The most common configuration is to leave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="6a8fa-132">Noções básicas de propriedades de mapeamento de atributo</span><span class="sxs-lookup"><span data-stu-id="6a8fa-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="6a8fa-133">Na seção anterior, você já foi apresentado à propriedade de tipo de mapeamento de atributo.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-133">In the previous section, you have already been introduced to the attribute mapping type property.</span></span>
<span data-ttu-id="6a8fa-134">Além dessa propriedade, mapeamentos de atributo também dão suporte aos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="6a8fa-134">In addition to this property, attribute mappings do also support the following attributes:</span></span>

- <span data-ttu-id="6a8fa-135">**Atributo de origem** – o atributo de usuário do sistema de origem (por exemplo, Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6a8fa-135">**Source attribute** - The user attribute from the source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="6a8fa-136">**Atributo de destino** – o atributo do usuário no sistema de destino (por exemplo: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="6a8fa-136">**Target attribute** – The user attribute in the target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="6a8fa-137">**Combinar objetos utilizando esse atributo** – se esse mapeamento deve ou não ser utilizado para identificar com exclusividade usuários entre os sistemas de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-137">**Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between the source and target systems.</span></span> <span data-ttu-id="6a8fa-138">Normalmente, isso é definido no atributo userPrincipalName ou email no Azure AD, que costuma ser mapeado para um campo de nome de usuário em um aplicativo de destino.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-138">This is typically set on the userPrincipalName or mail attribute in Azure AD, which is typically mapped to a username field in a target application.</span></span>
- <span data-ttu-id="6a8fa-139">**Precedência de correspondência** – vários atributos de correspondência podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="6a8fa-140">Quando houver múltiplos, os atributos serão avaliados na ordem definida por esse campo.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-140">When there are multiple, they are evaluated in the order defined by this field.</span></span> <span data-ttu-id="6a8fa-141">Assim que uma correspondência for encontrada, mais nenhum atributo correspondente será avaliado.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="6a8fa-142">**Aplicar esse mapeamento**</span><span class="sxs-lookup"><span data-stu-id="6a8fa-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="6a8fa-143">**Sempre** – aplicar esse mapeamento nas ações de criação e atualização do usuário</span><span class="sxs-lookup"><span data-stu-id="6a8fa-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="6a8fa-144">**Somente durante a criação** – aplicar esse mapeamento somente nas ações de criação de usuário</span><span class="sxs-lookup"><span data-stu-id="6a8fa-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="6a8fa-145">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="6a8fa-145">What you should know</span></span>

<span data-ttu-id="6a8fa-146">O Microsoft Azure AD fornece uma implementação muito eficiente de um processo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="6a8fa-147">Em um ambiente inicializado, apenas os objetos que precisam de atualização são processados durante um ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="6a8fa-148">A atualização de mapeamentos de atributo tem impacto no desempenho de um ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-148">Updating attribute mappings has an impact on the performance of a synchronization cycle.</span></span> <span data-ttu-id="6a8fa-149">Uma atualização a uma configuração de mapeamento de atributo exige que todos os objetos gerenciados sejam reavaliados.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-149">An update to the attribute mapping configuration requires all managed objects to be reevaluated.</span></span> <span data-ttu-id="6a8fa-150">É uma prática recomendada manter o número de alterações consecutivas aos seus mapeamentos de atributos no mínimo.</span><span class="sxs-lookup"><span data-stu-id="6a8fa-150">It is a recommended best practice to keep the number of consecutive changes to your attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a8fa-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a8fa-151">Next steps</span></span>

* [<span data-ttu-id="6a8fa-152">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6a8fa-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6a8fa-153">Automatizar o provisionamento/desprovisionamento de usuários para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="6a8fa-153">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="6a8fa-154">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="6a8fa-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="6a8fa-155">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="6a8fa-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="6a8fa-156">Usando o SCIM para habilitar o provisionamento automático de usuários e grupos do Active Directory do Azure para aplicativos</span><span class="sxs-lookup"><span data-stu-id="6a8fa-156">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="6a8fa-157">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="6a8fa-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="6a8fa-158">Lista de tutoriais sobre como integrar aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="6a8fa-158">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

