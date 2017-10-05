---
title: "Problema ao instalar a extensão do navegador do painel de acesso do aplicativo | Microsoft Docs"
description: "Como corrigir erros comuns encontrados ao instalar a extensão do navegador do painel de acesso"
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
ms.reviewer: japere
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="65ca9-103">Problema ao instalar a extensão do navegador do painel de acesso do aplicativo</span><span class="sxs-lookup"><span data-stu-id="65ca9-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="65ca9-104">O Painel de Acesso é um portal baseado na Web que permite a um usuário que tenha uma conta corporativa ou de estudante no Azure Active Directory (Azure AD) exibir e iniciar aplicativos baseados em nuvem para os quais o administrador do Azure AD concedeu acesso.</span><span class="sxs-lookup"><span data-stu-id="65ca9-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="65ca9-105">Um usuário com as edições do Azure AD também pode usar os recursos de gerenciamento de grupo de autoatendimento e aplicativo por meio do Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="65ca9-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="65ca9-106">O Painel de Acesso é separado do Portal do Azure e não exige que os usuários tenham uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="65ca9-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="65ca9-107">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="65ca9-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="65ca9-108">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="65ca9-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="65ca9-109">Atender aos requisitos de navegador para o Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="65ca9-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="65ca9-110">O Painel de Acesso exige um navegador com suporte para JavaScript e CSS habilitado.</span><span class="sxs-lookup"><span data-stu-id="65ca9-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="65ca9-111">Para usar o SSO (logon único) baseado em senha no Painel de Acesso, a extensão do Painel de Acesso deve estar instalada no navegador do usuário.</span><span class="sxs-lookup"><span data-stu-id="65ca9-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="65ca9-112">Essa extensão é baixada automaticamente quando um usuário seleciona um aplicativo configurado para SSO baseado em senha.</span><span class="sxs-lookup"><span data-stu-id="65ca9-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="65ca9-113">Para SSO baseado em senha, os navegadores do usuário final podem ser:</span><span class="sxs-lookup"><span data-stu-id="65ca9-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="65ca9-114">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="65ca9-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="65ca9-115">Edge no Windows 10 Anniversary Edition ou posterior</span><span class="sxs-lookup"><span data-stu-id="65ca9-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="65ca9-116">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="65ca9-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="65ca9-117">Firefox 26.0 ou posterior, no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="65ca9-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="65ca9-118">Como instalar a extensão do Navegador do Painel de Acesso</span><span class="sxs-lookup"><span data-stu-id="65ca9-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="65ca9-119">Para instalar a extensão do Navegador do Painel de Acesso, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="65ca9-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="65ca9-120">Abra o [Painel de Acesso](https://myapps.microsoft.com) em um dos navegadores compatíveis e entre como um **usuário** no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65ca9-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="65ca9-121">Clique em um **aplicativo de SSO com senha** no Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="65ca9-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="65ca9-122">No prompt solicitando a instalação do software, selecione **Instalar Agora**.</span><span class="sxs-lookup"><span data-stu-id="65ca9-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="65ca9-123">Com base no seu navegador, você será direcionado para o link de download.</span><span class="sxs-lookup"><span data-stu-id="65ca9-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="65ca9-124">**Adicione** a extensão ao seu navegador.</span><span class="sxs-lookup"><span data-stu-id="65ca9-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="65ca9-125">Se o navegador solicitar, selecione como **Habilitar** ou **Permitir** a extensão.</span><span class="sxs-lookup"><span data-stu-id="65ca9-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="65ca9-126">Quando estiver instalado, **reinicie** a sessão do navegador.</span><span class="sxs-lookup"><span data-stu-id="65ca9-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="65ca9-127">Entrar no Painel de Acesso e verificar se é possível **iniciar** os aplicativos de SSO de senha</span><span class="sxs-lookup"><span data-stu-id="65ca9-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="65ca9-128">Também é possível baixar a extensão para Chrome e Edge diretamente pelos links abaixo:</span><span class="sxs-lookup"><span data-stu-id="65ca9-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="65ca9-129">Extensão do Painel de Acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="65ca9-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="65ca9-130">Extensão do Painel de Acesso do Edge</span><span class="sxs-lookup"><span data-stu-id="65ca9-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="65ca9-131">Configurar uma política de grupo para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="65ca9-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="65ca9-132">É possível configurar uma política de grupo que permita instalar remotamente a extensão do Painel de Acesso para o Internet Explorer nos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="65ca9-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="65ca9-133">Os pré-requisitos incluem:</span><span class="sxs-lookup"><span data-stu-id="65ca9-133">The prerequisites include:</span></span>

-   <span data-ttu-id="65ca9-134">Você configurou os [Serviços de Domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)e os computadores dos usuários ingressaram no domínio.</span><span class="sxs-lookup"><span data-stu-id="65ca9-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="65ca9-135">Você deve ter a permissão "Editar configurações" para editar o GPO (Objeto de Política de Grupo).</span><span class="sxs-lookup"><span data-stu-id="65ca9-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="65ca9-136">Por padrão, os membros dos grupos de segurança a seguir têm esta permissão: Administradores de Domínio, Administradores de Empresa e Proprietários Criadores de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="65ca9-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="65ca9-137">[Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="65ca9-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="65ca9-138">Siga o tutorial [Como Implantar a Extensão do Painel de Acesso para o Internet Explorer usando Política de Grupo](active-directory-saas-ie-group-policy.md) para obter instruções passo a passo sobre como configurar política de grupo e implantá-la nos usuários.</span><span class="sxs-lookup"><span data-stu-id="65ca9-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="65ca9-139">Solucionar problemas do Painel de Acesso no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="65ca9-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="65ca9-140">Siga o guia [Solucionar problemas da Extensão do Painel de Acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md) para acessar uma ferramenta de diagnóstico e as instruções passo a passo sobre como configurar a extensão para o IE.</span><span class="sxs-lookup"><span data-stu-id="65ca9-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="65ca9-141">Se essas etapas de solução de problemas não resolverem o problema</span><span class="sxs-lookup"><span data-stu-id="65ca9-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="65ca9-142">Abra um tíquete de suporte com as informações a seguir, se estiverem disponíveis:</span><span class="sxs-lookup"><span data-stu-id="65ca9-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="65ca9-143">ID de erro de correlação</span><span class="sxs-lookup"><span data-stu-id="65ca9-143">Correlation error ID</span></span>

-   <span data-ttu-id="65ca9-144">UPN (endereço de email de usuário)</span><span class="sxs-lookup"><span data-stu-id="65ca9-144">UPN (user email address)</span></span>

-   <span data-ttu-id="65ca9-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="65ca9-145">TenantID</span></span>

-   <span data-ttu-id="65ca9-146">Tipo de navegador</span><span class="sxs-lookup"><span data-stu-id="65ca9-146">Browser type</span></span>

-   <span data-ttu-id="65ca9-147">Fuso horário e hora/cronograma durante o erro</span><span class="sxs-lookup"><span data-stu-id="65ca9-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="65ca9-148">Rastreamentos do Fiddler</span><span class="sxs-lookup"><span data-stu-id="65ca9-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="65ca9-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65ca9-149">Next steps</span></span>
[<span data-ttu-id="65ca9-150">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65ca9-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
