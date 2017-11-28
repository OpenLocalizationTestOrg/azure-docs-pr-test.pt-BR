---
title: "marca tooyour página de entrada no hello Azure Active Directory da empresa de idioma específico de aaaAdd | Microsoft Docs"
description: "Saiba como tooadd um idioma específico da empresa a identidade visual de imagens e a página de texto tooan sign-in do Azure"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="84d00-103">Adicionar marca tooyour página de entrada no hello Azure Active Directory da empresa de idioma específico</span><span class="sxs-lookup"><span data-stu-id="84d00-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="84d00-104">tooavoid confusão, muitas empresas deseja tooapply uma aparência consistente em todos os sites de saudação e serviços que gerenciam.</span><span class="sxs-lookup"><span data-stu-id="84d00-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="84d00-105">O Azure Active Directory fornece esse recurso, permitindo-lhe toocustomize Olá aparência Olá entrar página com o logotipo da empresa e esquemas de cores personalizadas.</span><span class="sxs-lookup"><span data-stu-id="84d00-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="84d00-106">Olá entrar é Olá página que aparece quando você entrar no tooOffice 365 ou outros aplicativos baseados na web que estão usando o AD do Azure como seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="84d00-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="84d00-107">Você interage com essa página tooenter suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="84d00-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="84d00-108">Personalizando Olá página de entrada para outro idioma</span><span class="sxs-lookup"><span data-stu-id="84d00-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="84d00-109">Você pode adicionar elementos específicos de idioma tooyour personalizado na página de entrada somente se você já tiver criado uma página de logon personalizada conforme descrito em [adicionar identidade visual a página de entrada tooyour](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84d00-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="84d00-110">Você pode configurar uma página de entrada por diretório com um conjunto padrão de elementos personalizáveis.</span><span class="sxs-lookup"><span data-stu-id="84d00-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="84d00-111">Depois de configurar o conjunto de elementos da página padrão de saudação, você pode configurar versões mais para localidades diferentes.</span><span class="sxs-lookup"><span data-stu-id="84d00-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="84d00-112">Você também pode misturar e combinar vários elementos.</span><span class="sxs-lookup"><span data-stu-id="84d00-112">You can also mix and match various elements.</span></span> <span data-ttu-id="84d00-113">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="84d00-113">For example, you could:</span></span>

* <span data-ttu-id="84d00-114">Criar uma **Imagem de página de entrada** padrão que funcione para todas as culturas e depois criar versões específicas para o inglês e o francês.</span><span class="sxs-lookup"><span data-stu-id="84d00-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="84d00-115">Quando você define sua tooone navegadores desses dois idiomas, Olá específico do idioma imagem aparece, enquanto a ilustração do padrão de saudação aparece para todos os outros idiomas.</span><span class="sxs-lookup"><span data-stu-id="84d00-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="84d00-116">Configure logotipos diferentes para sua organização (por exemplo, versões em japonês ou hebraico).</span><span class="sxs-lookup"><span data-stu-id="84d00-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="84d00-117">É recomendável que você mantenha diversas Olá variações de idioma baixas, por motivos de desempenho e manutenção.</span><span class="sxs-lookup"><span data-stu-id="84d00-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="84d00-118">**diretório de tooyour identidade visual da empresa de tooadd:**</span><span class="sxs-lookup"><span data-stu-id="84d00-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="84d00-119">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="84d00-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="84d00-120">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="84d00-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Abrir o gerenciamento de usuários](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="84d00-122">Em Olá **usuários e grupos** folha, selecione **identidade visual da empresa**.</span><span class="sxs-lookup"><span data-stu-id="84d00-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="84d00-123">Em Olá **usuários e grupos - identidade visual da empresa** folha, selecione Olá **Adicionar idioma** comando.</span><span class="sxs-lookup"><span data-stu-id="84d00-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Adicionar elementos de identidade visual específicos do idioma](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="84d00-125">Modificar Olá elementos você deseja toocustomize.</span><span class="sxs-lookup"><span data-stu-id="84d00-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="84d00-126">Todos os elementos são opcionais.</span><span class="sxs-lookup"><span data-stu-id="84d00-126">All elements are optional.</span></span>
6. <span data-ttu-id="84d00-127">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="84d00-127">Click **Save**.</span></span>

<span data-ttu-id="84d00-128">Pode demorar até tooan horas para que as alterações feitas toohello entrar tooappear identidade visual da página.</span><span class="sxs-lookup"><span data-stu-id="84d00-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84d00-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="84d00-129">Next steps</span></span>
[<span data-ttu-id="84d00-130">Adicionar identidade visual tooyour na página de entrada</span><span class="sxs-lookup"><span data-stu-id="84d00-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
