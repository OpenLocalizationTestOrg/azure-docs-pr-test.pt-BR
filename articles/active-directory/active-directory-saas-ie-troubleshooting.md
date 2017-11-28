---
title: "Olá aaaTroubleshooting extensão do painel de acesso do Azure para o IE | Microsoft Docs"
description: "Como toouse agrupar complemento do política toodeploy saudação do Internet Explorer para o portal de meus aplicativos hello."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="0cf96-103">Solução de problemas Olá extensão do painel de acesso para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="0cf96-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="0cf96-104">Este artigo o ajudará a solucionar problemas Olá os problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cf96-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="0cf96-105">Você está tooaccess não é possível seus aplicativos por meio do portal meus aplicativos Olá ao usar o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0cf96-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="0cf96-106">Você verá hello "Instalar o Software" mensagem mesmo que você já tiver instalado o software de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cf96-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="0cf96-107">Se você for um administrador, consulte também: [como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="0cf96-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="0cf96-108">Executar Olá, ferramenta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0cf96-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="0cf96-109">Você pode diagnosticar problemas de instalação com a extensão do painel de acesso de saudação baixando e executando a ferramenta de diagnóstico saudação do painel de acesso:</span><span class="sxs-lookup"><span data-stu-id="0cf96-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="0cf96-110">Clique aqui ferramenta de diagnóstico de saudação do toodownload.</span><span class="sxs-lookup"><span data-stu-id="0cf96-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="0cf96-111">Olá abrir arquivo e pressione **extrair tudo** botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Pressione Extrair Tudo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="0cf96-113">Em seguida, pressione Olá **extrair** toocontinue do botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Pressione Extrair](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="0cf96-115">ferramenta de saudação toorun, com o botão direito Olá txt **AccessPanelExtensionDiagnosticTool**, em seguida, selecione **abrir com > Host de Script com base do Microsoft Windows**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Abrir com > Microsoft Windows com base em Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="0cf96-117">Você verá Olá janela de diagnóstico, que descreve o que pode estar errado com a instalação a seguir.</span><span class="sxs-lookup"><span data-stu-id="0cf96-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Um exemplo de janela de diagnóstico Olá](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="0cf96-119">Clique em "**Sim**" toolet Olá programa hello problemas que foram encontrados.</span><span class="sxs-lookup"><span data-stu-id="0cf96-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="0cf96-120">toosave essas alterações, feche todas as janelas do Internet Explorer e abra novamente o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0cf96-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="0cf96-121">Se você ainda não puder acessar seus aplicativos, tente Olá estas etapas.</span><span class="sxs-lookup"><span data-stu-id="0cf96-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="0cf96-122">Verifique que Olá que extensão do painel de acesso está habilitado</span><span class="sxs-lookup"><span data-stu-id="0cf96-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="0cf96-123">tooverify que Olá extensão do painel de acesso está habilitado no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="0cf96-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="0cf96-124">No Internet Explorer, clique em Olá **ícone de engrenagem** no canto superior direito de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cf96-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="0cf96-125">Em seguida, selecione **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="0cf96-126">(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Vá tooTools > Opções da Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="0cf96-128">Clique em Olá **programas** guia, em seguida, clique em hello **gerenciar complementos** botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Clique em Gerenciar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="0cf96-130">Na caixa de diálogo, selecione **extensão do painel de acesso** e, em seguida, clique em Olá **habilitar** botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Clique em Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="0cf96-132">toosave essas alterações, feche todas as janelas do Internet Explorer e, em seguida, abra o Internet Explorer novamente.</span><span class="sxs-lookup"><span data-stu-id="0cf96-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="0cf96-133">Habilitar extensões para a navegação InPrivate</span><span class="sxs-lookup"><span data-stu-id="0cf96-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="0cf96-134">Se você estiver usando o modo de Navegação InPrivate hello:</span><span class="sxs-lookup"><span data-stu-id="0cf96-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="0cf96-135">No Internet Explorer, clique em Olá **ícone de engrenagem** no canto superior direito de saudação da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cf96-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="0cf96-136">Em seguida, selecione **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="0cf96-137">(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Um exemplo de janela de diagnóstico Olá](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="0cf96-139">Vá toohello **privacidade** guia, em seguida, **desmarque** Olá a caixa de seleção **desabilitar barras de ferramentas e extensões quando a navegação InPrivate é iniciado**</span><span class="sxs-lookup"><span data-stu-id="0cf96-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Desmarque a opção de desabilitar as barras de ferramentas e extensões quando começar a navegação InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="0cf96-141">toosave essas alterações, feche todas as janelas do Internet Explorer e, em seguida, abra o Internet Explorer novamente.</span><span class="sxs-lookup"><span data-stu-id="0cf96-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="0cf96-142">Desinstalar Olá extensão do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="0cf96-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="0cf96-143">Olá toouninstall extensão do painel de acesso do seu computador:</span><span class="sxs-lookup"><span data-stu-id="0cf96-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="0cf96-144">No teclado, pressione Olá **tecla Windows** tooopen menu de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cf96-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="0cf96-145">Quando o menu Olá estiver aberto, você pode digitar qualquer coisa toodo uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0cf96-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="0cf96-146">Digite "Painel de controle" e, em seguida, abra Olá **painel de controle** quando ele aparece nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="0cf96-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Pesquise Painel de Controle](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="0cf96-148">Olá canto superior direito da saudação painel de controle, alterar Olá **exibir** opção muito**ícones grandes**.</span><span class="sxs-lookup"><span data-stu-id="0cf96-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="0cf96-149">Em seguida, localize e clique em Olá **programas e recursos** botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Acompanhamento na Olá exibição tooshow ícones grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="0cf96-151">Olá, selecione lista **extensão do painel de acesso**e clique em Olá de hello **desinstalação** botão.</span><span class="sxs-lookup"><span data-stu-id="0cf96-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Clique em Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="0cf96-153">Extensão de saudação tooinstall, em seguida, tente novamente toosee se Olá problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="0cf96-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="0cf96-154">Se você encontrar problemas ao desinstalar a extensão hello, você também pode remover usando Olá [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) ferramenta.</span><span class="sxs-lookup"><span data-stu-id="0cf96-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="0cf96-155">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="0cf96-155">Related Articles</span></span>
* [<span data-ttu-id="0cf96-156">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0cf96-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0cf96-157">Acesso a aplicativos e logon único com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="0cf96-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0cf96-158">Como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo</span><span class="sxs-lookup"><span data-stu-id="0cf96-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

