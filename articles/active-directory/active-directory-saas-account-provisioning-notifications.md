---
title: "as notificações de provisionamento de aaaAccount | Microsoft Docs"
description: "Saiba como tooensure que você será notificado sobre problemas relacionados a toouser de provisionamento que exigem atenção, permitindo que as notificações de provisionamento de conta."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="289c4-103">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="289c4-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="289c4-104">Com o provisionamento de usuário, você pode automatizar o processo de saudação do gerenciamento de usuários em aplicativos SaaS de terceiros.</span><span class="sxs-lookup"><span data-stu-id="289c4-104">With user provisioning, you can automate hello process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="289c4-105">Embora esse seja um processo automatizado, sua interação com esse processo é de tootime de tempo necessária.</span><span class="sxs-lookup"><span data-stu-id="289c4-105">While this is an automated process, your interaction with this process is from time tootime required.</span></span> <br>
<span data-ttu-id="289c4-106">Isso acontece, por exemplo hello, quando a senha de saudação da conta Olá configurou tooexchange dados com um terço de SaaS aplicativo expirou.</span><span class="sxs-lookup"><span data-stu-id="289c4-106">This is, for example hello case, when hello password of hello account you have configured tooexchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="289c4-107">Ao habilitar as notificações de provisionamento de conta, você pode garantir que você será notificado sobre problemas relacionado toouser provisionamento que exigem sua atenção.</span><span class="sxs-lookup"><span data-stu-id="289c4-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related toouser provisioning that require your attention.</span></span>

<span data-ttu-id="289c4-108">Você ativa ou desativa notificações de provisionamento de conta como parte de sua configuração de provisionamento de usuário de um aplicativo SaaS de terceiro.</span><span class="sxs-lookup"><span data-stu-id="289c4-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Provisionamento do usuário][1] 

<span data-ttu-id="289c4-110">tooactivate as notificações de provisionamento de conta, selecione Olá a caixa de seleção em Olá **confirmação** página da caixa de diálogo e alias de email do tipo saudação do destinatário hello.</span><span class="sxs-lookup"><span data-stu-id="289c4-110">tooactivate account provisioning notifications, select hello related checkbox on hello **Confirmation** dialog page, and then type hello email alias of hello recipient.</span></span>

![Notificações de provisionamento de conta][2]

<span data-ttu-id="289c4-112">Você pode inserir uma lista de distribuição como destinatário; No entanto, é importante toonote email de notificação de saudação contém tooreports links que são acessíveis apenas pelos administradores de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="289c4-112">You can enter a distribution list as recipient; however, it is important toonote that hello notification email contains links tooreports that are only accessible by hello Azure AD administrators.</span></span>

<span data-ttu-id="289c4-113">Se você tiver habilitadas de notificações de provisionamento de conta, você receberá emails sobre questões críticas que estão relacionada toouser provisionamento.</span><span class="sxs-lookup"><span data-stu-id="289c4-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related toouser provisioning.</span></span> <span data-ttu-id="289c4-114">No entanto, tooavoid uma sobrecarga de emails, você receberá apenas uma notificação de email por dia para cada SaaS email de notificação do aplicativo hello está habilitado.</span><span class="sxs-lookup"><span data-stu-id="289c4-114">However, tooavoid an email overload, you will only receive one notification email per day for each SaaS application hello notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="289c4-115">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="289c4-115">Related Articles</span></span>
* [<span data-ttu-id="289c4-116">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="289c4-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="289c4-117">Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos</span><span class="sxs-lookup"><span data-stu-id="289c4-117">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="289c4-118">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="289c4-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="289c4-119">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="289c4-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="289c4-120">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="289c4-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="289c4-121">Usando SCIM o provisionamento automático tooenable de usuários e grupos do Active Directory do Azure tooapplications</span><span class="sxs-lookup"><span data-stu-id="289c4-121">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="289c4-122">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="289c4-122">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
