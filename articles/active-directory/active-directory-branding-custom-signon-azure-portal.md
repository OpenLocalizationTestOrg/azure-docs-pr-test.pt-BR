---
title: "Personalizar a página de entrada do Azure Active Directory | Microsoft Docs"
description: "Saiba como adicionar uma identidade visual à página de entrada do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="48508-103">Adicionar identidade visual à sua página de entrada no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48508-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="48508-104">Para evitar confusão, muitas empresas desejam aplicar uma aparência consistente em todos os sites e serviços que elas gerenciam.</span><span class="sxs-lookup"><span data-stu-id="48508-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="48508-105">O Azure Active Directory fornece esse recurso, permitindo que você personalize a aparência da página de entrada com esquemas de cores e o logotipo da empresa.</span><span class="sxs-lookup"><span data-stu-id="48508-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="48508-106">A página de entrada é a página que aparece quando você entra no Office 365 ou em outros aplicativos baseados na Web que estejam usando o Azure AD como provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="48508-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="48508-107">Você interage com essa página para inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="48508-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="48508-108">Se você quiser mostrar a marca da empresa, cores e outros elementos personalizáveis nessa página, consulte as imagens a seguir para compreender a diferença entre as duas experiências.</span><span class="sxs-lookup"><span data-stu-id="48508-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="48508-109">A captura de tela a seguir mostra um exemplo de página de entrada do Office 365 em um computador desktop **antes** de uma personalização:</span><span class="sxs-lookup"><span data-stu-id="48508-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Página de entrada do Office 365 antes da personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="48508-111">A captura de tela a seguir mostra um exemplo de página de entrada do Office 365 em um computador desktop **depois** de uma personalização:</span><span class="sxs-lookup"><span data-stu-id="48508-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Página de entrada do Office 365 após a personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="48508-113">Personalização da página de entrada</span><span class="sxs-lookup"><span data-stu-id="48508-113">Customizing the sign-in page</span></span>
<span data-ttu-id="48508-114">Normalmente, se você precisar de acesso baseado em navegador para seus aplicativos e serviços de nuvem que sua organização assina, use a página de entrada.</span><span class="sxs-lookup"><span data-stu-id="48508-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="48508-115">Se você tiver as alterações aplicadas à sua página de entrada, poderá demorar até uma hora para que as alterações sejam exibidas.</span><span class="sxs-lookup"><span data-stu-id="48508-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="48508-116">Uma página de entrada com marca só aparece quando você visita um serviço com uma URL específica do locatário, como https://outlook.com/**contoso**.com ou https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="48508-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="48508-117">Quando você visita um serviço com URLs específicas sem locatário (por exemplo, https://mail.office365.com), uma página de entrada sem marca é exibida.</span><span class="sxs-lookup"><span data-stu-id="48508-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="48508-118">Nesse caso, sua identidade visual aparecerá assim que você inserir sua ID de usuário ou que tiver selecionado um bloco de usuário.</span><span class="sxs-lookup"><span data-stu-id="48508-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="48508-119">O nome do domínio deve aparecer como "Ativo" na parte **Domínios** do portal do Azure no qual você configurou a identidade visual.</span><span class="sxs-lookup"><span data-stu-id="48508-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="48508-120">Para obter mais informações, confira [Adicionar nomes de domínio personalizados](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="48508-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="48508-121">A identidade visual da página de entrada não se transfere para a página de entrada do consumidor da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48508-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="48508-122">Se você entrar com uma conta da Microsoft, talvez veja uma lista com identidade visual de blocos de usuários renderizados pelo Azure AD, mas a identidade visual da sua organização não se aplicará à página de entrada da conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48508-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="48508-123">Na sua página de entrada, a caixa de seleção **Mantenha-me conectado** permite que o usuário permaneça conectado ao fechar e reabrir o navegador.</span><span class="sxs-lookup"><span data-stu-id="48508-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="48508-125">Ela não afeta o tempo de vida da sessão.</span><span class="sxs-lookup"><span data-stu-id="48508-125">It does not effect session lifetime.</span></span> <span data-ttu-id="48508-126">Você pode ocultar a caixa de seleção na página de entrada do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48508-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="48508-127">A exibição da caixa de seleção depende da configuração de **Manter a minha sessão iniciada desativada**.</span><span class="sxs-lookup"><span data-stu-id="48508-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="48508-129">Para ocultar a caixa de seleção, defina essa configuração para **Sim**.</span><span class="sxs-lookup"><span data-stu-id="48508-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="48508-130">Alguns recursos do SharePoint Online e do Office 2010 dependem da capacidade dos usuários marcarem essa caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="48508-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="48508-131">Se você definir essa configuração como oculta, os usuários poderão ver avisos adicionais e inesperados para entrar.</span><span class="sxs-lookup"><span data-stu-id="48508-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="48508-132">**Para adicionar identidade visual da empresa ao diretório:**</span><span class="sxs-lookup"><span data-stu-id="48508-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="48508-133">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="48508-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="48508-134">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="48508-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="48508-136">Na folha **Usuários e grupos**, selecione **Identidade visual da empresa**.</span><span class="sxs-lookup"><span data-stu-id="48508-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="48508-137">Na folha **Usuários e grupos - Identidade visual da empresa**, selecione o comando **Editar**.</span><span class="sxs-lookup"><span data-stu-id="48508-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![Editar identidade visual personalizada](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="48508-139">Modifique os elementos que você deseja personalizar.</span><span class="sxs-lookup"><span data-stu-id="48508-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="48508-140">Todos os elementos são opcionais.</span><span class="sxs-lookup"><span data-stu-id="48508-140">All elements are optional.</span></span>
6. <span data-ttu-id="48508-141">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48508-141">Click **Save**.</span></span>

<span data-ttu-id="48508-142">Pode demorar até uma hora para que apareçam todas as alterações feitas à identidade visual da página de entrada.</span><span class="sxs-lookup"><span data-stu-id="48508-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48508-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48508-143">Next steps</span></span>
[<span data-ttu-id="48508-144">Adicionar identidade visual da empresa específica a um idioma</span><span class="sxs-lookup"><span data-stu-id="48508-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
