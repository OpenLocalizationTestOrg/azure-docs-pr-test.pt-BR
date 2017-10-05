---
title: Erro inesperado ao executar o consentimento para um aplicativo | Microsoft Docs
description: "Discute os erros que podem ocorrer durante o processo de consentimento para um aplicativo e o que é possível fazer"
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
ms.openlocfilehash: fd500fdd4c8642bad96dcf71eebcf1fad461a35f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="37ebf-103">Erro inesperado ao executar o consentimento para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="37ebf-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="37ebf-104">Este artigo discute os erros que podem ocorrer durante o processo de consentimento para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37ebf-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="37ebf-105">Se você estiver procurando Solucionar Problemas de solicitações de consentimentos inesperados que não contêm mensagens de erro, consulte [Cenários de Autenticação do Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="37ebf-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="37ebf-106">Muitos aplicativos que se integram com o Azure Active Directory exigem permissões para acessar outros recursos para serem executados.</span><span class="sxs-lookup"><span data-stu-id="37ebf-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="37ebf-107">Quando esses recursos também são integrados com o Azure Active Directory, as permissões para acessá-los são solicitadas usando a estrutura de consentimento comum.</span><span class="sxs-lookup"><span data-stu-id="37ebf-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="37ebf-108">Isso resulta em uma solicitação de consentimento exibida que geralmente ocorre na primeira vez que um aplicativo é usado, mas também, pode ocorrer em um subsequente uso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37ebf-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="37ebf-109">Determinadas condições devem ser verdadeiras para que um usuário conceda as permissões exigidas por um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37ebf-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="37ebf-110">Se essas condições não forem atendidas, vários erros podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="37ebf-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="37ebf-111">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="37ebf-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="37ebf-112">Solicitação de erro de permissão não autorizada</span><span class="sxs-lookup"><span data-stu-id="37ebf-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="37ebf-113">O **AADSTS90093:** &lt;clientAppDisplayName&gt; está solicitando uma ou mais permissões que você não está autorizado a conceder.</span><span class="sxs-lookup"><span data-stu-id="37ebf-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="37ebf-114">Contate um administrador que pode consentir pedido em seu nome.</span><span class="sxs-lookup"><span data-stu-id="37ebf-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="37ebf-115">Esse erro ocorre quando um usuário que não é um administrador de empresa tenta usar um aplicativo que está solicitando permissões, as quais somente um administrador pode conceder.</span><span class="sxs-lookup"><span data-stu-id="37ebf-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="37ebf-116">Esse erro pode ser resolvido por um administrador concedendo acesso ao aplicativo em nome de sua organização.</span><span class="sxs-lookup"><span data-stu-id="37ebf-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="37ebf-117">Política impede concessão de permissões de erro</span><span class="sxs-lookup"><span data-stu-id="37ebf-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="37ebf-118">**AADSTS90093:** Um administrador do &lt;NomeExibiçãoLocatário&gt; definiu uma política que impede que você conceda ao &lt;nome do aplicativo&gt; as permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="37ebf-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="37ebf-119">Contate um administrador de &lt;Nome Exibiçãolocatário&gt; que pode conceder permissões para esse aplicativo em seu nome.</span><span class="sxs-lookup"><span data-stu-id="37ebf-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="37ebf-120">Esse erro ocorre quando um administrador da empresa desativa a capacidade de consentimento dos usuários para aplicativos e, em seguida, um usuário não administrador tenta usar um aplicativo que exige consentimento.</span><span class="sxs-lookup"><span data-stu-id="37ebf-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="37ebf-121">Esse erro pode ser resolvido por um administrador concedendo acesso ao aplicativo em nome de sua organização.</span><span class="sxs-lookup"><span data-stu-id="37ebf-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="37ebf-122">Erro de problema intermitente</span><span class="sxs-lookup"><span data-stu-id="37ebf-122">Intermittent problem error</span></span>
* <span data-ttu-id="37ebf-123">**AADSTS90090:** Parece que encontramos um problema intermitente ao registrar as permissões que você tentou conceder a &lt;NomeExibiçãoAplicativoCliente&gt;.</span><span class="sxs-lookup"><span data-stu-id="37ebf-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="37ebf-124">tente novamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="37ebf-124">try again later.</span></span>

<span data-ttu-id="37ebf-125">Esse erro indica que ocorreu um erro de serviço intermitente.</span><span class="sxs-lookup"><span data-stu-id="37ebf-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="37ebf-126">Ele pode ser resolvido tentando consentir ao aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="37ebf-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="37ebf-127">Erro de recurso não disponível</span><span class="sxs-lookup"><span data-stu-id="37ebf-127">Resource not available error</span></span>
* <span data-ttu-id="37ebf-128">**AADSTS65005:** O aplicativo &lt;NomeExibiçãoAplicativoCliente&gt; solicitou permissões para acessar um recurso&lt;NomeExibiçãoAplicativoRecurso&gt; que não está disponível.</span><span class="sxs-lookup"><span data-stu-id="37ebf-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="37ebf-129">Contate o desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37ebf-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="37ebf-130">Recurso não disponível no erro do locatário</span><span class="sxs-lookup"><span data-stu-id="37ebf-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="37ebf-131">**AADSTS65005:** &lt;NomeExibiçãoAplicativoCliente&gt; está solicitando acesso a um recurso &lt;NomeExibiçãoAplicativoRecurso&gt; que não está disponível em sua organização &lt;NomeExibiçãoLocatário&gt;.</span><span class="sxs-lookup"><span data-stu-id="37ebf-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="37ebf-132">Certifique-se de que esse recurso está disponível ou contate o administrador de &lt;NomeExibiçãoLocatário&gt;.</span><span class="sxs-lookup"><span data-stu-id="37ebf-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="37ebf-133">Erro de incompatibilidade de permissões</span><span class="sxs-lookup"><span data-stu-id="37ebf-133">Permissions mismatch error</span></span>
* <span data-ttu-id="37ebf-134">**AADSTS65005:** O aplicativo solicitou consentimento para acessar o recurso &lt;NomeExibiçãoAplicativoRecurso&gt;.</span><span class="sxs-lookup"><span data-stu-id="37ebf-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="37ebf-135">A solicitação falhou porque não corresponde como o aplicativo configurado previamente durante o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37ebf-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="37ebf-136">Contate o fornecedor do aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="37ebf-136">Contact the app vendor.**</span></span>

<span data-ttu-id="37ebf-137">Esses erros ocorrem quando o aplicativo que um usuário está tentando consentir está solicitando permissões para acessar um aplicativo de recurso que não pode ser localizado no diretório da organização (locatário).</span><span class="sxs-lookup"><span data-stu-id="37ebf-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="37ebf-138">Isso pode ocorrer por vários motivos:</span><span class="sxs-lookup"><span data-stu-id="37ebf-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="37ebf-139">O desenvolvedor do aplicativo cliente configurou seu aplicativo incorretamente, fazendo com que solicite acesso a um recurso inválido.</span><span class="sxs-lookup"><span data-stu-id="37ebf-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="37ebf-140">Nesse caso, o desenvolvedor do aplicativo deve atualizar a configuração do aplicativo cliente para resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="37ebf-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="37ebf-141">Uma Entidade de Serviço que representa o aplicativo de recurso de destino não existe na organização ou existiu no passado mas foi removido.</span><span class="sxs-lookup"><span data-stu-id="37ebf-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="37ebf-142">Para resolver esse problema, uma Entidade de Serviço para o aplicativo de recurso deve ser provisionada na organização para que o aplicativo cliente possa solicitar-lhe permissões.</span><span class="sxs-lookup"><span data-stu-id="37ebf-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="37ebf-143">Isso pode acontecer de várias maneiras, dependendo do tipo de aplicativo, incluindo:</span><span class="sxs-lookup"><span data-stu-id="37ebf-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="37ebf-144">Adquirir uma assinatura para o aplicativo de recursos (aplicativos publicados pela Microsoft)</span><span class="sxs-lookup"><span data-stu-id="37ebf-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="37ebf-145">Consentimento para a aplicação de recursos</span><span class="sxs-lookup"><span data-stu-id="37ebf-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="37ebf-146">Conceder as permissões de aplicação através do Azure Portal</span><span class="sxs-lookup"><span data-stu-id="37ebf-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="37ebf-147">Adicionar o aplicativo a partir da Galeria do Aplicativo Azure AD</span><span class="sxs-lookup"><span data-stu-id="37ebf-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="37ebf-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37ebf-148">Next steps</span></span> 

[<span data-ttu-id="37ebf-149">Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1)</span><span class="sxs-lookup"><span data-stu-id="37ebf-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="37ebf-150">Escopos, permissões e consentimento no Azure Active Directory (ponto de extremidade v2.0)</span><span class="sxs-lookup"><span data-stu-id="37ebf-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


