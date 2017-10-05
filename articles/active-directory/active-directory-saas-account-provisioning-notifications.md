---
title: "Notificações de provisionamento de conta | Microsoft Docs"
description: "Saiba como garantir que você será notificado sobre problemas relacionados ao provisionamento de usuário que exigem sua atenção habilitando notificações de provisionamento de conta."
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
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="ea0e9-103">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="ea0e9-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="ea0e9-104">Com o provisionamento de usuário, você pode automatizar o processo de gerenciar usuários em aplicativos SaaS de terceiros.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="ea0e9-105">Embora esse seja um processo automatizado, sua interação com esse processo às vezes é necessária.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="ea0e9-106">É, por exemplo, o caso, quando a senha da conta que você configurou para trocar dados com um aplicativo SaaS de terceiros expirou.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="ea0e9-107">Ao habilitar notificações de provisionamento de conta você pode garantir que será notificado sobre problemas relacionados ao provisionamento de usuário, que exigem sua atenção.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="ea0e9-108">Você ativa ou desativa notificações de provisionamento de conta como parte de sua configuração de provisionamento de usuário de um aplicativo SaaS de terceiro.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Provisionamento do usuário][1] 

<span data-ttu-id="ea0e9-110">Para ativar notificações de provisionamento de conta, marque a caixa de seleção relacionada na página de diálogo **Confirmação** e digite o alias de email do destinatário.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Notificações de provisionamento de conta][2]

<span data-ttu-id="ea0e9-112">Você pode inserir uma lista de distribuição como destinatário; no entanto, é importante observar que o email de notificação contém links para relatórios que só são acessíveis pelos administradores do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="ea0e9-113">Se você tiver notificações de provisionamento de conta habilitadas, receberá emails sobre problemas críticos relacionados ao provisionamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="ea0e9-114">No entanto, para evitar uma sobrecarga de emails, você só receberá um email de notificação por dia para cada aplicativo SaaS para o qual o email de notificação está habilitado.</span><span class="sxs-lookup"><span data-stu-id="ea0e9-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ea0e9-115">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="ea0e9-115">Related Articles</span></span>
* [<span data-ttu-id="ea0e9-116">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ea0e9-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ea0e9-117">Automatizar o provisionamento/desprovisionamento de usuários para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="ea0e9-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="ea0e9-118">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="ea0e9-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="ea0e9-119">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="ea0e9-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="ea0e9-120">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="ea0e9-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="ea0e9-121">Usando o SCIM para habilitar o provisionamento automático de usuários e grupos do Active Directory do Azure para aplicativos</span><span class="sxs-lookup"><span data-stu-id="ea0e9-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="ea0e9-122">Lista de tutoriais sobre como integrar aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="ea0e9-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
