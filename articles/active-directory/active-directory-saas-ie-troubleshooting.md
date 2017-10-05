---
title: "Resolução de problemas da extensão do Painel de Acesso do Azure para IE | Microsoft Docs"
description: "Como usar a política de grupo para implantar o complemento do Internet Explorer para o portal de meus aplicativos."
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
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="b19ac-103">Resolução de problemas da extensão do painel de acesso do Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b19ac-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="b19ac-104">Este artigo ajuda você a solucionar os problemas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b19ac-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="b19ac-105">Você não consegue acessar seus aplicativos por meio do portal de meus aplicativos ao usar o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b19ac-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="b19ac-106">Consulte a mensagem "Instalação de Software", mesmo que você já tenha instalado o software.</span><span class="sxs-lookup"><span data-stu-id="b19ac-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="b19ac-107">Se você for um administrador, consulte também: [como implantar a extensão do painel de acesso para o Internet Explorer usando a política de grupo](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="b19ac-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="b19ac-108">Execute a ferramenta de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b19ac-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="b19ac-109">Você pode diagnosticar problemas de instalação com a extensão do painel de acesso fazendo download e executando a ferramenta de diagnóstico do painel de acesso:</span><span class="sxs-lookup"><span data-stu-id="b19ac-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="b19ac-110">Clique aqui para baixar a ferramenta de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b19ac-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="b19ac-111">Abra o arquivo e pressione o botão **Extrair todos** .</span><span class="sxs-lookup"><span data-stu-id="b19ac-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Pressione Extrair Tudo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="b19ac-113">Em seguida, pressione o botão **Extrair** para continuar.</span><span class="sxs-lookup"><span data-stu-id="b19ac-113">Then press the **Extract** button to continue.</span></span>
   
    ![Pressione Extrair](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="b19ac-115">Para executar a ferramenta, clique com o botão direito do mouse no arquivo denominado **AccessPanelExtensionDiagnosticTool**, em seguida, selecione **Abrir com > Microsoft Windows com base em Script Host**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Abrir com > Microsoft Windows com base em Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="b19ac-117">Você verá a janela diagnóstico a seguir, que descreve o que pode estar errado com a sua instalação.</span><span class="sxs-lookup"><span data-stu-id="b19ac-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Um exemplo da janela de diagnóstico](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="b19ac-119">Clique em "**Sim**" para permitir que o programa corrija os problemas encontrados.</span><span class="sxs-lookup"><span data-stu-id="b19ac-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="b19ac-120">Para salvar essas alterações, feche todas as janelas do Internet Explorer e abra novamente o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b19ac-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="b19ac-121">Se você não puder acessar seus aplicativos, tente as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="b19ac-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="b19ac-122">Verifique se a extensão do painel de acesso está habilitada</span><span class="sxs-lookup"><span data-stu-id="b19ac-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="b19ac-123">Para verificar se a extensão do painel de acesso está habilitada no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="b19ac-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="b19ac-124">No Internet Explorer, clique no **ícone de engrenagem** no canto superior direito da janela.</span><span class="sxs-lookup"><span data-stu-id="b19ac-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="b19ac-125">Em seguida, selecione **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="b19ac-126">(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Vá para Ferramentas > Opções da Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="b19ac-128">Clique na guia **Programas** e clique no botão **Gerenciar Complementos**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Clique em Gerenciar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="b19ac-130">Nesta caixa de diálogo, selecione **extensão do painel de acesso** e, em seguida, clique no botão **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Clique em Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="b19ac-132">Para salvar essas alterações, feche todas as janelas do Internet Explorer e abra novamente o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b19ac-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="b19ac-133">Habilitar extensões para a navegação InPrivate</span><span class="sxs-lookup"><span data-stu-id="b19ac-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="b19ac-134">Se você estiver usando o modo de Navegação InPrivate:</span><span class="sxs-lookup"><span data-stu-id="b19ac-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="b19ac-135">No Internet Explorer, clique no **ícone de engrenagem** no canto superior direito da janela.</span><span class="sxs-lookup"><span data-stu-id="b19ac-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="b19ac-136">Em seguida, selecione **Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="b19ac-137">(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Um exemplo da janela de diagnóstico](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="b19ac-139">Vá para a guia **Privacidade**, em seguida, **desmarque** a caixa de seleção **Desabilitar barras de ferramentas e extensões quando a Navegação InPrivate se iniciar**</span><span class="sxs-lookup"><span data-stu-id="b19ac-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Desmarque a opção de desabilitar as barras de ferramentas e extensões quando começar a navegação InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="b19ac-141">Para salvar essas alterações, feche todas as janelas do Internet Explorer e abra novamente o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b19ac-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="b19ac-142">Desinstalar a extensão do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="b19ac-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="b19ac-143">Para desinstalar a extensão do painel de acesso do computador:</span><span class="sxs-lookup"><span data-stu-id="b19ac-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="b19ac-144">No teclado, pressione a **tecla Windows** para abrir o menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="b19ac-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="b19ac-145">Quando o menu estiver aberto, você pode digitar qualquer coisa para fazer uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b19ac-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="b19ac-146">Digite "Control Panel" e, em seguida, abra o **Painel de controle** quando ele aparecer nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b19ac-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Pesquise Painel de Controle](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="b19ac-148">No canto superior direito do painel de controle, altere a opção **Exibir para** **ícones grandes**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="b19ac-149">Em seguida, localize e clique no botão **Programas e Recursos**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Altere a exibição para mostrar ícones grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="b19ac-151">Na lista, selecione **Extensão do Painel de Acesso** e clique no botão **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="b19ac-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Clique em Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="b19ac-153">Você pode tentar instalar a extensão novamente para ver se o problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="b19ac-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="b19ac-154">Se você encontrar problemas ao desinstalar a extensão, também pode removê-lo usando a ferramenta [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) .</span><span class="sxs-lookup"><span data-stu-id="b19ac-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="b19ac-155">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="b19ac-155">Related Articles</span></span>
* [<span data-ttu-id="b19ac-156">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b19ac-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b19ac-157">Acesso a aplicativos e logon único com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b19ac-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b19ac-158">Como implantar a extensão do painel de acesso para o Internet Explorer usando a Política de Grupo</span><span class="sxs-lookup"><span data-stu-id="b19ac-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

