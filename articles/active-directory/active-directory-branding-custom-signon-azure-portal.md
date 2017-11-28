---
title: "aaaCustomize sua entrada no página Olá Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooadd uma página toohello sign-in do Azure da identidade visual da empresa"
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
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="a24d3-103">Adicionar identidade visual tooyour página de entrada de saudação do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a24d3-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="a24d3-104">tooavoid confusão, muitas empresas deseja tooapply uma aparência consistente em todos os sites de saudação e serviços que gerenciam.</span><span class="sxs-lookup"><span data-stu-id="a24d3-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="a24d3-105">O Azure Active Directory fornece esse recurso, permitindo-lhe toocustomize Olá aparência Olá entrar página com o logotipo da empresa e esquemas de cores personalizadas.</span><span class="sxs-lookup"><span data-stu-id="a24d3-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="a24d3-106">Olá entrar é Olá página que aparece quando você entrar no tooOffice 365 ou outros aplicativos baseados na web que estão usando o AD do Azure como seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="a24d3-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="a24d3-107">Você interage com essa página tooenter suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="a24d3-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="a24d3-108">Se você quiser tooshow a marca da empresa, cores e outros elementos personalizáveis nesta página, consulte Olá diferença de saudação toounderstand imagens entre duas experiências de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="a24d3-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="a24d3-109">Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **antes de** uma personalização:</span><span class="sxs-lookup"><span data-stu-id="a24d3-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Página de entrada do Office 365 antes da personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="a24d3-111">Olá seguinte captura de tela mostra e exemplo de hello Office 365 na página de entrada em um computador desktop **depois** uma personalização:</span><span class="sxs-lookup"><span data-stu-id="a24d3-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Página de entrada do Office 365 após a personalização](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="a24d3-113">Personalizando a página de entrada hello</span><span class="sxs-lookup"><span data-stu-id="a24d3-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="a24d3-114">Normalmente, se você precisar de acesso baseado em navegador tooyour nuvem aplicativos e serviços que sua empresa assina, você usa página de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="a24d3-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="a24d3-115">Se você aplicou alterações tooyour na página de entrada, pode levar a hora de tooan para Olá alterações tooappear.</span><span class="sxs-lookup"><span data-stu-id="a24d3-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="a24d3-116">Uma página de entrada com marca só aparece quando você visita um serviço com uma URL específica do locatário, como https://outlook.com/**contoso**.com ou https://mail.**contoso**.com.</span><span class="sxs-lookup"><span data-stu-id="a24d3-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="a24d3-117">Quando você visita um serviço com URLs específicas sem locatário (por exemplo, https://mail.office365.com), uma página de entrada sem marca é exibida.</span><span class="sxs-lookup"><span data-stu-id="a24d3-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="a24d3-118">Nesse caso, sua identidade visual aparecerá assim que você inserir sua ID de usuário ou que tiver selecionado um bloco de usuário.</span><span class="sxs-lookup"><span data-stu-id="a24d3-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="a24d3-119">O nome do domínio deve aparecer como "Ativo" no hello **domínios** Olá a parte do portal do Azure no qual você configurou a identidade visual.</span><span class="sxs-lookup"><span data-stu-id="a24d3-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="a24d3-120">Para obter mais informações, confira [Adicionar nomes de domínio personalizados](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a24d3-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="a24d3-121">Identidade visual da página de entrada não reporta o sinal do consumidor toohello na página do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a24d3-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="a24d3-122">Se você entrar com uma conta da Microsoft, você pode ver a lista marcada de blocos do usuário renderizados pelo AD do Azure, mas Olá identidade visual da sua organização não se aplica toohello página de logon da conta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a24d3-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="a24d3-123">Na página entrar, Olá **Mantenha-me conectado** caixa de seleção permite que um tooremain do usuário conectado ao fechar e reabrir o navegador.</span><span class="sxs-lookup"><span data-stu-id="a24d3-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="a24d3-125">Ela não afeta o tempo de vida da sessão.</span><span class="sxs-lookup"><span data-stu-id="a24d3-125">It does not effect session lifetime.</span></span> <span data-ttu-id="a24d3-126">Você pode ocultar Olá a caixa de seleção na página de entrada do Active Directory do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="a24d3-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="a24d3-127">Se a caixa de seleção de saudação é exibida depende de configuração de saudação do **Mantenha-me conectado desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="a24d3-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Mantenha-me conectado](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="a24d3-129">toohide Olá caixa de seleção, defina essa configuração muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="a24d3-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="a24d3-130">Alguns recursos do SharePoint Online e o Office 2010 dependem usuários sendo capaz de toocheck nesta caixa.</span><span class="sxs-lookup"><span data-stu-id="a24d3-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="a24d3-131">Se você configurar toohidden essa configuração, os usuários podem ver prompts adicionais e inesperados em toosign.</span><span class="sxs-lookup"><span data-stu-id="a24d3-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="a24d3-132">**diretório de tooyour identidade visual da empresa de tooadd:**</span><span class="sxs-lookup"><span data-stu-id="a24d3-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="a24d3-133">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a24d3-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a24d3-134">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a24d3-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="a24d3-136">Em Olá **usuários e grupos** folha, selecione **identidade visual da empresa**.</span><span class="sxs-lookup"><span data-stu-id="a24d3-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="a24d3-137">Em Olá **usuários e grupos - identidade visual da empresa** folha, selecione Olá **editar** comando.</span><span class="sxs-lookup"><span data-stu-id="a24d3-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Editar identidade visual personalizada](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="a24d3-139">Modificar Olá elementos você deseja toocustomize.</span><span class="sxs-lookup"><span data-stu-id="a24d3-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="a24d3-140">Todos os elementos são opcionais.</span><span class="sxs-lookup"><span data-stu-id="a24d3-140">All elements are optional.</span></span>
6. <span data-ttu-id="a24d3-141">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a24d3-141">Click **Save**.</span></span>

<span data-ttu-id="a24d3-142">Pode demorar até tooan horas para que as alterações feitas toohello entrar tooappear identidade visual da página.</span><span class="sxs-lookup"><span data-stu-id="a24d3-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a24d3-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a24d3-143">Next steps</span></span>
[<span data-ttu-id="a24d3-144">Adicionar identidade visual da empresa específica a um idioma</span><span class="sxs-lookup"><span data-stu-id="a24d3-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
