---
title: aaaCustomizing mapeamentos de atributos do AD do Azure | Microsoft Docs
description: "Saiba quais mapeamentos de atributo para aplicativos SaaS no Azure Active Directory são como você pode modificá-las tooaddress sua empresa precisa."
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
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="82b6b-103">Personalizar os mapeamentos de atributos de provisionamento de usuário para aplicativos SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82b6b-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="82b6b-104">AD do Microsoft Azure oferece suporte para aplicativos SaaS de terceiros toothird, como Salesforce, Google Apps e outros usuários de provisionamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="82b6b-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="82b6b-105">Se você tiver o provisionamento de um aplicativo SaaS de terceiros habilitado do usuário, Olá Portal de gerenciamento do Azure controla seus valores de atributo na forma de uma configuração chamada "mapeamento de atributo".</span><span class="sxs-lookup"><span data-stu-id="82b6b-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="82b6b-106">Há um conjunto predefinido de mapeamentos de atributo entre objetos de usuário do AD do Azure e objetos de usuário de cada aplicativo SaaS.</span><span class="sxs-lookup"><span data-stu-id="82b6b-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="82b6b-107">Alguns aplicativos gerenciam outros tipos de objetos, como grupos ou contatos.</span><span class="sxs-lookup"><span data-stu-id="82b6b-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="82b6b-108">Você pode personalizar mapeamentos de atributos padrão de saudação de acordo com as necessidades de negócios de tooyour.</span><span class="sxs-lookup"><span data-stu-id="82b6b-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="82b6b-109">Isso significa que você pode alterar ou excluir mapeamentos de atributo existentes ou criar novos mapeamentos de atributo.</span><span class="sxs-lookup"><span data-stu-id="82b6b-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="82b6b-110">No portal de saudação do AD do Azure, você pode acessar esse recurso clicando em um **mapeamentos** configuração em **provisionamento** em Olá **gerenciar** seção de um  **Aplicativo corporativo**.</span><span class="sxs-lookup"><span data-stu-id="82b6b-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="82b6b-112">Clicar em um **mapeamentos** configuração, abre Olá relacionada **mapeamento de atributo** folha.</span><span class="sxs-lookup"><span data-stu-id="82b6b-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="82b6b-113">Não há mapeamentos de atributos que são exigidos por um toofunction de aplicativos SaaS corretamente.</span><span class="sxs-lookup"><span data-stu-id="82b6b-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="82b6b-114">Para atributos obrigatórios, Olá **excluir** recurso não está disponível.</span><span class="sxs-lookup"><span data-stu-id="82b6b-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="82b6b-116">O exemplo hello acima, você pode ver que Olá **Username** atributo de um objeto gerenciado no Salesforce é preenchido com hello **userPrincipalName** valor da saudação vinculado objeto do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="82b6b-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="82b6b-117">Você pode personalizar os **Mapeamentos de Atributo** existentes clicando em um mapeamento.</span><span class="sxs-lookup"><span data-stu-id="82b6b-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="82b6b-118">Isso abre o hello **Editar atributo** folha.</span><span class="sxs-lookup"><span data-stu-id="82b6b-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="82b6b-120">Noções básicas sobre tipos de mapeamento de atributo</span><span class="sxs-lookup"><span data-stu-id="82b6b-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="82b6b-121">Com mapeamentos de atributo, você controla como os atributos são preenchidos em um aplicativo SaaS de terceiro.</span><span class="sxs-lookup"><span data-stu-id="82b6b-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="82b6b-122">Há quatro tipos diferentes de mapeamento com suporte:</span><span class="sxs-lookup"><span data-stu-id="82b6b-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="82b6b-123">**Direto** – o atributo de destino Olá é populado com valor de saudação de um atributo do objeto vinculado Olá no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="82b6b-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="82b6b-124">**Constante** – o atributo de destino Olá é preenchido com uma cadeia de caracteres específica que você especificou.</span><span class="sxs-lookup"><span data-stu-id="82b6b-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="82b6b-125">**Expressão** -atributo de destino de saudação é preenchido com base no resultado de saudação de uma expressão como script.</span><span class="sxs-lookup"><span data-stu-id="82b6b-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="82b6b-126">Para saber mais, consulte [Escrever expressões para mapeamentos de atributo no Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="82b6b-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="82b6b-127">**Nenhum** -Olá atributo de destino é deixado sem modificações.</span><span class="sxs-lookup"><span data-stu-id="82b6b-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="82b6b-128">No entanto, se o atributo de destino Olá estiver vazio, ele é preenchido com o valor de padrão de saudação que você especificar.</span><span class="sxs-lookup"><span data-stu-id="82b6b-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="82b6b-129">Em tipos de mapeamento de atributo básico de toothese quatro adição, mapeamentos de atributos personalizados suportam o conceito de saudação do opcional **padrão** atribuição de valor.</span><span class="sxs-lookup"><span data-stu-id="82b6b-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="82b6b-130">atribuição de valor saudação padrão garante que um atributo de destino é preenchido com um valor se não houver nenhum valor no AD do Azure nem no objeto de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="82b6b-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="82b6b-131">Olá a configuração mais comum é tooleave em branco.</span><span class="sxs-lookup"><span data-stu-id="82b6b-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="82b6b-132">Noções básicas de propriedades de mapeamento de atributo</span><span class="sxs-lookup"><span data-stu-id="82b6b-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="82b6b-133">Na seção anterior do hello, você já foram introduzidas toohello propriedade de tipo de mapeamento de atributo.</span><span class="sxs-lookup"><span data-stu-id="82b6b-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="82b6b-134">Na propriedade de toothis adição, mapeamentos de atributo também dão suporte a saudação seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="82b6b-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="82b6b-135">**Atributo de origem** -atributo de usuário de saudação do sistema de origem da saudação (por exemplo: Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="82b6b-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="82b6b-136">**Atributo de destino** – atributo de usuário Olá no sistema de destino da saudação (por exemplo: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="82b6b-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="82b6b-137">**Correspondem a objetos que usam esse atributo** – se este mapeamento deve ser usado ou não toouniquely identificar usuários entre sistemas de origem e destino hello.</span><span class="sxs-lookup"><span data-stu-id="82b6b-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="82b6b-138">Isso normalmente é definido em Olá userPrincipalName ou atributo de email no AD do Azure, que geralmente é mapeada tooa campo de nome de usuário em um aplicativo de destino.</span><span class="sxs-lookup"><span data-stu-id="82b6b-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="82b6b-139">**Precedência de correspondência** – vários atributos de correspondência podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="82b6b-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="82b6b-140">Quando houver vários, elas são avaliadas na ordem Olá definido por este campo.</span><span class="sxs-lookup"><span data-stu-id="82b6b-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="82b6b-141">Assim que uma correspondência for encontrada, mais nenhum atributo correspondente será avaliado.</span><span class="sxs-lookup"><span data-stu-id="82b6b-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="82b6b-142">**Aplicar esse mapeamento**</span><span class="sxs-lookup"><span data-stu-id="82b6b-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="82b6b-143">**Sempre** – aplicar esse mapeamento nas ações de criação e atualização do usuário</span><span class="sxs-lookup"><span data-stu-id="82b6b-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="82b6b-144">**Somente durante a criação** – aplicar esse mapeamento somente nas ações de criação de usuário</span><span class="sxs-lookup"><span data-stu-id="82b6b-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="82b6b-145">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="82b6b-145">What you should know</span></span>

<span data-ttu-id="82b6b-146">O Microsoft Azure AD fornece uma implementação muito eficiente de um processo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="82b6b-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="82b6b-147">Em um ambiente inicializado, apenas os objetos que precisam de atualização são processados durante um ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="82b6b-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="82b6b-148">Atualizar mapeamentos de atributo tem um impacto no desempenho de saudação de um ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="82b6b-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="82b6b-149">Uma configuração de mapeamento de atributo de toohello de atualização requer que todos os toobe de objetos gerenciados reavaliadas.</span><span class="sxs-lookup"><span data-stu-id="82b6b-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="82b6b-150">É um melhor prática tookeep Olá número recomendado de mapeamentos de atributo tooyour alterações consecutivas no mínimo.</span><span class="sxs-lookup"><span data-stu-id="82b6b-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b6b-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82b6b-151">Next steps</span></span>

* [<span data-ttu-id="82b6b-152">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="82b6b-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="82b6b-153">Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos</span><span class="sxs-lookup"><span data-stu-id="82b6b-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="82b6b-154">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="82b6b-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="82b6b-155">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="82b6b-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="82b6b-156">Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications</span><span class="sxs-lookup"><span data-stu-id="82b6b-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="82b6b-157">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="82b6b-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="82b6b-158">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="82b6b-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

