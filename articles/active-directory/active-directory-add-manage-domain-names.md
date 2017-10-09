---
title: "nomes de domínio personalizados aaaManaging no Active Directory do Azure | Microsoft Docs"
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
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="80b9a-103">Gerenciando nomes de domínio personalizados no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80b9a-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="80b9a-104">Um nome de domínio pode ser um identificador importante para muitos recursos de diretório, como parte de:</span><span class="sxs-lookup"><span data-stu-id="80b9a-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="80b9a-105">Um nome de usuário ou endereço de email de um usuário</span><span class="sxs-lookup"><span data-stu-id="80b9a-105">A user name or email address for a user</span></span>
* <span data-ttu-id="80b9a-106">Olá endereço de um grupo</span><span class="sxs-lookup"><span data-stu-id="80b9a-106">hello address for a group</span></span>
* <span data-ttu-id="80b9a-107">URI da ID do aplicativo Hello para um aplicativo</span><span class="sxs-lookup"><span data-stu-id="80b9a-107">hello app ID URI for an application</span></span>

<span data-ttu-id="80b9a-108">Um recurso no Azure Active Directory (AD do Azure) pode incluir um nome de domínio que já é verificado toobe pertencentes a directory Olá que contém o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="80b9a-109">Somente um administrador global pode executar tarefas de gerenciamento de domínio no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80b9a-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80b9a-110">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="80b9a-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="80b9a-111">Para como toomanage seu nomes de domínio no Centro de administração de saudação do AD do Azure, consulte [gerenciar nomes de domínio personalizado no Active Directory do Azure](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80b9a-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="80b9a-112">Definir nome de domínio primário de saudação do seu diretório do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80b9a-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="80b9a-113">Quando o diretório é criado, o nome de domínio inicial hello, como 'contoso.onmicrosoft.com', também é o nome de domínio primário de Olá para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="80b9a-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="80b9a-114">domínio primário Olá é o nome de domínio de padrão de saudação para um novo usuário quando você cria um novo usuário no hello [portal clássico do Azure](https://manage.windowsazure.com/), ou outros portais, como o portal de administração do Office 365 de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="80b9a-115">Isso simplifica o processo de saudação para um administrador toocreate novos usuários no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="80b9a-116">nome de domínio primário toochange Olá para seu diretório:</span><span class="sxs-lookup"><span data-stu-id="80b9a-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="80b9a-117">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com uma conta de usuário que seja um administrador global do seu diretório do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80b9a-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="80b9a-118">Selecione **do Active Directory** na barra de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="80b9a-119">Abra seu diretório.</span><span class="sxs-lookup"><span data-stu-id="80b9a-119">Open your directory.</span></span>
4. <span data-ttu-id="80b9a-120">Selecione Olá **domínios** guia.</span><span class="sxs-lookup"><span data-stu-id="80b9a-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="80b9a-121">Selecione Olá **alteração principal** botão na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="80b9a-122">Selecione o domínio de saudação que você deseje Olá toobe novo domínio primário para seu diretório.</span><span class="sxs-lookup"><span data-stu-id="80b9a-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="80b9a-123">Você pode alterar o nome de domínio primário Olá para o diretório toobe qualquer domínio personalizado verificado que não está federado.</span><span class="sxs-lookup"><span data-stu-id="80b9a-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="80b9a-124">Alterar domínio primário de saudação do seu diretório não alterará os nomes de usuário Olá para todos os usuários existentes.</span><span class="sxs-lookup"><span data-stu-id="80b9a-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="80b9a-125">Adicionar nomes de domínio personalizado tooyour AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80b9a-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="80b9a-126">Você pode adicionar o diretório do AD do Azure do too900 domínio personalizado nomes tooeach.</span><span class="sxs-lookup"><span data-stu-id="80b9a-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="80b9a-127">Olá processo muito[adicionar um nome de domínio personalizados adicionais](active-directory-add-domain.md) Olá mesmo para o primeiro nome de domínio personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="80b9a-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="80b9a-128">Adicionar subdomínios de um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="80b9a-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="80b9a-129">Se você quiser tooadd um nome de domínio de terceiro nível, como 'europe.contoso.com' tooyour directory, você deve primeiro adicionar e verificar o domínio de segundo nível hello, como contoso.com. subdomínio Hello serão automaticamente verificado pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80b9a-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="80b9a-130">foi verificado toosee que Olá subdomínio que você acabou de adicionar, atualizar Olá página no navegador de saudação que lista os domínios de saudação em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="80b9a-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="80b9a-131">Quais toodo se você alterar o registrador de DNS Olá para seu nome de domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="80b9a-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="80b9a-132">Se você alterar o registrador de DNS Olá para seu nome de domínio personalizado, você pode continuar toouse seu nome de domínio personalizado com o Azure AD em si sem interrupção e sem outras tarefas de configuração.</span><span class="sxs-lookup"><span data-stu-id="80b9a-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="80b9a-133">Se você usar seu nome de domínio personalizado com o Office 365, Intune, ou outros serviços que dependem de nomes de domínio personalizado no AD do Azure, consulte a documentação de toohello para esses serviços.</span><span class="sxs-lookup"><span data-stu-id="80b9a-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="80b9a-134">Excluir um nome de domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="80b9a-134">Delete a custom domain name</span></span>
<span data-ttu-id="80b9a-135">Você pode excluir um nome de domínio do AD do Azure se sua organização não usa esse nome de domínio, ou se você precisar toouse nome de domínio com outro AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="80b9a-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="80b9a-136">toodelete um nome de domínio personalizado, primeiro você deve assegurar que não há recursos no seu diretório se baseia no nome de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="80b9a-137">Você não poderá excluir um nome de domínio do diretório se:</span><span class="sxs-lookup"><span data-stu-id="80b9a-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="80b9a-138">Qualquer usuário tem um nome de usuário, o endereço de email ou o endereço de proxy que incluem o nome de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="80b9a-139">Qualquer grupo tem um endereço de email ou o endereço de proxy que inclui o nome de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="80b9a-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="80b9a-140">Qualquer aplicativo no AD do Azure tem um URI de identificação que inclui o nome de domínio de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80b9a-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="80b9a-141">Você deve alterar ou excluir qualquer esse recurso em seu diretório do AD do Azure antes de excluir o nome de domínio personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="80b9a-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="80b9a-142">Usar nomes de domínio toomanage PowerShell ou API do Graph</span><span class="sxs-lookup"><span data-stu-id="80b9a-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="80b9a-143">A maioria das tarefas de gerenciamento para nomes de domínio no Azure Active Directory também pode ser concluída usando o Microsoft PowerShell ou de forma programática, usando a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80b9a-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="80b9a-144">Usando nomes de domínio do PowerShell toomanage no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80b9a-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="80b9a-145">Usando nomes de domínio do API do Graph toomanage no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="80b9a-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="80b9a-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80b9a-146">Next steps</span></span>
* [<span data-ttu-id="80b9a-147">Saiba mais sobre nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b9a-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="80b9a-148">Gerenciar nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="80b9a-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

