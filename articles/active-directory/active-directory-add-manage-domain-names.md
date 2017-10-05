---
title: "Gerenciando nomes de domínio personalizados no Azure Active Directory | Microsoft Docs"
description: "Conceitos de gerenciamento e instruções para gerenciar um domínio personalizado no Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="4e23a-103">Gerenciando nomes de domínio personalizados no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e23a-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="4e23a-104">Um nome de domínio pode ser um identificador importante para muitos recursos de diretório, como parte de:</span><span class="sxs-lookup"><span data-stu-id="4e23a-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="4e23a-105">Um nome de usuário ou endereço de email de um usuário</span><span class="sxs-lookup"><span data-stu-id="4e23a-105">A user name or email address for a user</span></span>
* <span data-ttu-id="4e23a-106">O endereço de um grupo</span><span class="sxs-lookup"><span data-stu-id="4e23a-106">The address for a group</span></span>
* <span data-ttu-id="4e23a-107">A URI da ID do aplicativo de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4e23a-107">The app ID URI for an application</span></span>

<span data-ttu-id="4e23a-108">Um recurso no Azure AD (Azure Active Directory) pode incluir um nome de domínio já verificado como pertencente ao diretório que contém o recurso.</span><span class="sxs-lookup"><span data-stu-id="4e23a-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="4e23a-109">Somente um administrador global pode executar tarefas de gerenciamento de domínio no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e23a-110">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4e23a-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="4e23a-111">Para saber como gerenciar seus nomes de domínio no centro de administração do Azure AD, consulte [Gerenciando nomes de domínio personalizados no Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4e23a-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="4e23a-112">Definir o nome de domínio primário para o diretório do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e23a-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="4e23a-113">Quando o diretório é criado, o nome de domínio inicial, como 'contoso.onmicrosoft.com', também é o nome de domínio primário para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4e23a-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="4e23a-114">O domínio primário é o nome de domínio padrão para um novo usuário ao criar um novo usuário no [portal clássico do Azure](https://manage.windowsazure.com/), ou outros portais, como o portal de administração do Office 365.</span><span class="sxs-lookup"><span data-stu-id="4e23a-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="4e23a-115">Isso simplifica o processo de criação de novos usuários no portal por um administrador.</span><span class="sxs-lookup"><span data-stu-id="4e23a-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="4e23a-116">Para alterar o nome de domínio primário para seu diretório:</span><span class="sxs-lookup"><span data-stu-id="4e23a-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="4e23a-117">Entre no [portal clássico do Azure](https://manage.windowsazure.com/) com uma conta de usuário que seja um administrador global do diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="4e23a-118">Selecione **Active Directory** na barra de navegação esquerda.</span><span class="sxs-lookup"><span data-stu-id="4e23a-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="4e23a-119">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4e23a-119">Open your directory.</span></span>
4. <span data-ttu-id="4e23a-120">Selecione a guia **Domínios** .</span><span class="sxs-lookup"><span data-stu-id="4e23a-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="4e23a-121">Selecione o botão **Alterar primário** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="4e23a-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="4e23a-122">Selecione o domínio que você deseja que seja o novo domínio primário para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4e23a-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="4e23a-123">Você pode alterar o nome de domínio primário para o seu diretório para qualquer domínio personalizado verificado não federado.</span><span class="sxs-lookup"><span data-stu-id="4e23a-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="4e23a-124">Alterar o domínio primário para o seu diretório não alterará os nomes de usuário para usuários existentes.</span><span class="sxs-lookup"><span data-stu-id="4e23a-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="4e23a-125">Adicionar nomes de domínio personalizados ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e23a-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="4e23a-126">Você pode adicionar até 900 nomes de domínio personalizados para cada diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="4e23a-127">O processo para [adicionar um nome de domínio personalizado adicional](active-directory-add-domain.md) é o mesmo para o primeiro nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4e23a-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="4e23a-128">Adicionar subdomínios de um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="4e23a-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="4e23a-129">Se você quiser adicionar um nome de domínio de terceiro nível como 'europe.contoso.com' ao seu diretório, deverá primeiro adicionar e verificar o domínio de segundo nível, como contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4e23a-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="4e23a-130">O subdomínio será verificado automaticamente pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="4e23a-131">Para conferir que o subdomínio que você acabou de adicionar foi verificado, atualize no navegador a página que lista os domínios em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="4e23a-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="4e23a-132">O que fazer se você alterar o registrador DNS para o nome de domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="4e23a-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="4e23a-133">Se você alterar o registrador DNS para seu nome de domínio personalizado, poderá continuar usando seu nome de domínio personalizado com o Azure AD sem interrupção e sem outras tarefas de configuração adicionais.</span><span class="sxs-lookup"><span data-stu-id="4e23a-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="4e23a-134">Se você usa o nome de domínio personalizado com o Office 365, o Intune ou outros serviços que dependem de nomes de domínio personalizado no Azure AD, consulte a documentação desses serviços.</span><span class="sxs-lookup"><span data-stu-id="4e23a-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="4e23a-135">Excluir um nome de domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="4e23a-135">Delete a custom domain name</span></span>
<span data-ttu-id="4e23a-136">Você poderá excluir um nome de domínio do Azure AD se sua organização não usar esse nome de domínio ou se for preciso usar o nome de domínio com outro Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="4e23a-137">Para excluir um nome de domínio personalizado, primeiro você deve assegurar que nenhum recurso em seu diretório dependa do nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="4e23a-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="4e23a-138">Você não poderá excluir um nome de domínio do diretório se:</span><span class="sxs-lookup"><span data-stu-id="4e23a-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="4e23a-139">Qualquer usuário tiver um nome de usuário, endereço de email ou endereço de proxy que inclua o nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="4e23a-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="4e23a-140">Qualquer grupo tiver um endereço de email ou endereço de proxy que inclua o nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="4e23a-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="4e23a-141">Qualquer aplicativo no Azure AD tiver um URI da ID do aplicativo que inclua o nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="4e23a-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="4e23a-142">Você deve alterar ou excluir qualquer recurso desse tipo em seu diretório do Azure AD antes que possa excluir o nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4e23a-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="4e23a-143">Usar o PowerShell ou o Graph API para gerenciar nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="4e23a-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="4e23a-144">A maioria das tarefas de gerenciamento para nomes de domínio no Azure Active Directory também pode ser concluída usando o Microsoft PowerShell ou de forma programática, usando a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e23a-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="4e23a-145">Como usar o PowerShell para gerenciar nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e23a-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="4e23a-146">Como usar a API do Graph para gerenciar nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e23a-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="4e23a-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e23a-147">Next steps</span></span>
* [<span data-ttu-id="4e23a-148">Saiba mais sobre nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e23a-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="4e23a-149">Gerenciar nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="4e23a-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

