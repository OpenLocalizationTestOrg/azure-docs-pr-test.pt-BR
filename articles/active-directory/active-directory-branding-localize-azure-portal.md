---
title: "Adicionar a identidade visual da empresa específica a um idioma à sua página de conexão no Azure Active Directory | Microsoft Docs"
description: "Saiba como adicionar imagens e texto de identidade visual da empresa específicos do idioma a uma página de entrada do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="86a34-103">Adicionar identidade visual específica a um idioma à sua página de conexão no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86a34-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="86a34-104">Para evitar confusão, muitas empresas desejam aplicar uma aparência consistente em todos os sites e serviços que elas gerenciam.</span><span class="sxs-lookup"><span data-stu-id="86a34-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="86a34-105">O Azure Active Directory fornece esse recurso, permitindo que você personalize a aparência da página de entrada com esquemas de cores e o logotipo da empresa.</span><span class="sxs-lookup"><span data-stu-id="86a34-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="86a34-106">A página de entrada é a página que aparece quando você entra no Office 365 ou em outros aplicativos baseados na Web que estejam usando o Azure AD como provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="86a34-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="86a34-107">Você interage com essa página para inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="86a34-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="86a34-108">Personalizando a página de entrada para outro idioma</span><span class="sxs-lookup"><span data-stu-id="86a34-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="86a34-109">Você pode adicionar elementos específicos do idioma à sua página de entrada somente se já tiver criado uma página de entrada personalizada, conforme descrito em [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md)(Adicionar a identidade visual da empresa à página de entrada).</span><span class="sxs-lookup"><span data-stu-id="86a34-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="86a34-110">Você pode configurar uma página de entrada por diretório com um conjunto padrão de elementos personalizáveis.</span><span class="sxs-lookup"><span data-stu-id="86a34-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="86a34-111">Depois de ter configurado o conjunto padrão de elementos de página, é possível configurar mais versões para diferentes localidades.</span><span class="sxs-lookup"><span data-stu-id="86a34-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="86a34-112">Você também pode misturar e combinar vários elementos.</span><span class="sxs-lookup"><span data-stu-id="86a34-112">You can also mix and match various elements.</span></span> <span data-ttu-id="86a34-113">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="86a34-113">For example, you could:</span></span>

* <span data-ttu-id="86a34-114">Criar uma **Imagem de página de entrada** padrão que funcione para todas as culturas e depois criar versões específicas para o inglês e o francês.</span><span class="sxs-lookup"><span data-stu-id="86a34-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="86a34-115">Quando você define seus navegadores para um desses dois idiomas, é exibida a imagem específica do idioma, enquanto a ilustração padrão é exibida para todos os outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="86a34-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="86a34-116">Configure logotipos diferentes para sua organização (por exemplo, versões em japonês ou hebraico).</span><span class="sxs-lookup"><span data-stu-id="86a34-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="86a34-117">É recomendável manter o número de variações de linguagem baixo, por motivos de desempenho e manutenção.</span><span class="sxs-lookup"><span data-stu-id="86a34-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="86a34-118">**Para adicionar identidade visual da empresa ao diretório:**</span><span class="sxs-lookup"><span data-stu-id="86a34-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="86a34-119">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="86a34-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="86a34-120">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="86a34-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="86a34-122">Na folha **Usuários e grupos**, selecione **Identidade visual da empresa**.</span><span class="sxs-lookup"><span data-stu-id="86a34-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="86a34-123">Na folha **Usuários e grupos - identidade visual da empresa**, selecione o comando **Adicionar idioma**.</span><span class="sxs-lookup"><span data-stu-id="86a34-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Adicionar elementos de identidade visual específicos do idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="86a34-125">Modifique os elementos que você deseja personalizar.</span><span class="sxs-lookup"><span data-stu-id="86a34-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="86a34-126">Todos os elementos são opcionais.</span><span class="sxs-lookup"><span data-stu-id="86a34-126">All elements are optional.</span></span>
6. <span data-ttu-id="86a34-127">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="86a34-127">Click **Save**.</span></span>

<span data-ttu-id="86a34-128">Pode demorar até uma hora para que apareçam todas as alterações feitas à identidade visual da página de entrada.</span><span class="sxs-lookup"><span data-stu-id="86a34-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a34-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86a34-129">Next steps</span></span>
[<span data-ttu-id="86a34-130">Adicionar identidade visual da empresa à página de entrada</span><span class="sxs-lookup"><span data-stu-id="86a34-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
