---
title: "O que é a colaboração B2B do Azure Active Directory? | Microsoft Docs"
description: "A colaboração B2B do Azure Active Directory dá suporte a relações entre empresas, permitindo que os parceiros de negócios acessem de maneira seletiva seus aplicativos corporativos."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="5c960-104">O que é a colaboração B2B do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="5c960-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="5c960-105">Os recursos de colaboração B2B (entre empresas) do Azure AD permitem que qualquer organização que use o Azure AD trabalhe com segurança com usuários de qualquer outra organização, seja ela grande ou pequena.</span><span class="sxs-lookup"><span data-stu-id="5c960-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="5c960-106">Essas organizações podem usar o Azure AD ou não ou até mesmo ter uma organização de TI ou não.</span><span class="sxs-lookup"><span data-stu-id="5c960-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="5c960-107">As organizações que usam o Azure AD podem fornecer acesso a documentos, recursos e aplicativos a seus parceiros, mantendo o controle completo sobre seus próprios dados corporativos.</span><span class="sxs-lookup"><span data-stu-id="5c960-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="5c960-108">Os desenvolvedores podem usar as APIs entre empresas do Azure AD para programar aplicativos que reúnem duas organizações de forma mais segura.</span><span class="sxs-lookup"><span data-stu-id="5c960-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="5c960-109">Além disso, a navegação é muito fácil para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="5c960-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="5c960-110">97% de nossos clientes nos disseram que a colaboração B2B do Azure AD é muito importante para eles.</span><span class="sxs-lookup"><span data-stu-id="5c960-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![gráfico de pizza](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="5c960-112">Desde o início de abril de 2017, já tínhamos cerca de 3 milhões de usuários usando recursos de colaboração B2B do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c960-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="5c960-113">E mais de 23% das organizações do Azure AD que têm mais de 10 usuários já estão se beneficiando desses recursos.</span><span class="sxs-lookup"><span data-stu-id="5c960-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="5c960-114">Os principais benefícios da colaboração B2B do Azure AD para sua organização</span><span class="sxs-lookup"><span data-stu-id="5c960-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="5c960-115">Trabalhar com qualquer usuário de qualquer parceiro</span><span class="sxs-lookup"><span data-stu-id="5c960-115">Work with any user from any partner</span></span>

* <span data-ttu-id="5c960-116">Os parceiros usam suas próprias credenciais</span><span class="sxs-lookup"><span data-stu-id="5c960-116">Partners use their own credentials</span></span>

* <span data-ttu-id="5c960-117">Não há requisito para que os parceiros usem o Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c960-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="5c960-118">Diretórios externos nem configuração complexa são necessários</span><span class="sxs-lookup"><span data-stu-id="5c960-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="5c960-119">Colaboração simples e segura</span><span class="sxs-lookup"><span data-stu-id="5c960-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="5c960-120">Fornece acesso a quaisquer dados ou aplicativos corporativos, aplicando sofisticadas políticas de autorização com base no AD Azure</span><span class="sxs-lookup"><span data-stu-id="5c960-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="5c960-121">Fácil para os usuários</span><span class="sxs-lookup"><span data-stu-id="5c960-121">Easy for users</span></span>

* <span data-ttu-id="5c960-122">Segurança de altíssimo nível para aplicativos e dados</span><span class="sxs-lookup"><span data-stu-id="5c960-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="5c960-123">Sem sobrecarga de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5c960-123">No management overhead</span></span>

* <span data-ttu-id="5c960-124">Sem conta externa ou gerenciamento de senhas</span><span class="sxs-lookup"><span data-stu-id="5c960-124">No external account or password management</span></span>

* <span data-ttu-id="5c960-125">Sem gerenciamento de ciclo de vida de conta manual ou sincronizada</span><span class="sxs-lookup"><span data-stu-id="5c960-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="5c960-126">Sem sobrecarga administrativa externa</span><span class="sxs-lookup"><span data-stu-id="5c960-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="5c960-127">É possível adicionar usuários de colaboração B2B facilmente à sua organização</span><span class="sxs-lookup"><span data-stu-id="5c960-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="5c960-128">Administradores podem adicionar usuários de colaboração B2B (convidado) no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c960-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![adicionar usuários convidados](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="5c960-130">Habilita que seus colaboradores tragam sua própria identidade</span><span class="sxs-lookup"><span data-stu-id="5c960-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="5c960-131">Os colaboradores B2B podem entrar com uma identidade de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="5c960-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="5c960-132">Se o usuário não tiver uma conta da Microsoft ou uma conta do Azure AD, uma dela será criada facilmente para o usuário no momento do resgate da oferta.</span><span class="sxs-lookup"><span data-stu-id="5c960-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![Escolha de identidade de logon](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="5c960-134">Delegar aos proprietários de aplicativos e grupos</span><span class="sxs-lookup"><span data-stu-id="5c960-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="5c960-135">Os proprietários de aplicativos e grupos podem adicionar usuários B2B diretamente em qualquer aplicativo de sua importância, seja ele um aplicativo da Microsoft ou não.</span><span class="sxs-lookup"><span data-stu-id="5c960-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="5c960-136">Os administradores podem delegar permissão para adicionar usuários B2B a não-administradores.</span><span class="sxs-lookup"><span data-stu-id="5c960-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="5c960-137">Não-administradores podem usar o [Painel de acesso do aplicativo do Azure AD](https://myapps.microsoft.com) para adicionar usuários de colaboração B2B a aplicativos ou grupos.</span><span class="sxs-lookup"><span data-stu-id="5c960-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![painel de acesso](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![adicionar membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="5c960-140">As políticas de autorização protegem o conteúdo corporativo</span><span class="sxs-lookup"><span data-stu-id="5c960-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="5c960-141">Políticas de acesso condicional, como autenticação multifator, podem ser aplicadas:</span><span class="sxs-lookup"><span data-stu-id="5c960-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="5c960-142">No nível do locatário</span><span class="sxs-lookup"><span data-stu-id="5c960-142">At the tenant level</span></span>
- <span data-ttu-id="5c960-143">No nível do aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c960-143">At the application level</span></span>
- <span data-ttu-id="5c960-144">Para que usuários específicos protejam dados e aplicativos corporativos</span><span class="sxs-lookup"><span data-stu-id="5c960-144">For specific users to protect corporate apps and data</span></span>

![adicionar membro](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="5c960-146">Use nossas APIs e código de exemplo para facilmente criar aplicativos para integração</span><span class="sxs-lookup"><span data-stu-id="5c960-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="5c960-147">Integre seus parceiros externos de modo personalizado às necessidades de sua organização.</span><span class="sxs-lookup"><span data-stu-id="5c960-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="5c960-148">Usando as [APIs de convite de colaboração B2B](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), você pode personalizar suas experiências de integração, incluindo a criação de portais de inscrição de autoatendimento.</span><span class="sxs-lookup"><span data-stu-id="5c960-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="5c960-149">Nós fornecemos o código de exemplo para o portal de autoatendimento [no Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="5c960-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![portal de inscrição](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="5c960-151">Com a colaboração B2B do Azure AD é possível obter toda a capacidade do Azure AD para proteger seus relacionamentos com parceiros e para que os usuários finais localizem de maneira fácil e intuitiva.</span><span class="sxs-lookup"><span data-stu-id="5c960-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="5c960-152">Então siga em frente, una-se às milhares de organizações que já estão usando B2B do Azure AD para sua colaboração externa!</span><span class="sxs-lookup"><span data-stu-id="5c960-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c960-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c960-153">Next steps</span></span>

* <span data-ttu-id="5c960-154">Experiências de administrador são encontradas no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5c960-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="5c960-155">Experiências de operadores de informações estão disponíveis no [Painel de Acesso](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5c960-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="5c960-156">E, como sempre, conecte-se com a equipe do produto para enviar comentários, sugestões e participar de discussões por meio da [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b) (Comunidade Técnica da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="5c960-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="5c960-157">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="5c960-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="5c960-158">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="5c960-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="5c960-159">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="5c960-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* <span data-ttu-id="5c960-160">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md) (Os elementos do email de convite para colaboração B2B)</span><span class="sxs-lookup"><span data-stu-id="5c960-160">[The elements of the B2B collaboration invitation email](active-directory-b2b-invitation-email.md)</span></span>
* [<span data-ttu-id="5c960-161">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="5c960-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="5c960-162">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c960-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="5c960-163">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c960-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="5c960-164">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c960-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="5c960-165">API e personalização da colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c960-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="5c960-166">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="5c960-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="5c960-167">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="5c960-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="5c960-168">Auditoria e relatórios de um usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="5c960-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="5c960-169">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5c960-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
