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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Solução de problemas Olá extensão do painel de acesso para o Internet Explorer
Este artigo o ajudará a solucionar problemas Olá os problemas a seguir:

* Você está tooaccess não é possível seus aplicativos por meio do portal meus aplicativos Olá ao usar o Internet Explorer.
* Você verá hello "Instalar o Software" mensagem mesmo que você já tiver instalado o software de saudação.

Se você for um administrador, consulte também: [como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Executar Olá, ferramenta de diagnóstico
Você pode diagnosticar problemas de instalação com a extensão do painel de acesso de saudação baixando e executando a ferramenta de diagnóstico saudação do painel de acesso:

1. [Clique aqui ferramenta de diagnóstico de saudação do toodownload.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Olá abrir arquivo e pressione **extrair tudo** botão.
   
    ![Pressione Extrair Tudo](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Em seguida, pressione Olá **extrair** toocontinue do botão.
   
    ![Pressione Extrair](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. ferramenta de saudação toorun, com o botão direito Olá txt **AccessPanelExtensionDiagnosticTool**, em seguida, selecione **abrir com > Host de Script com base do Microsoft Windows**.
   
    ![Abrir com > Microsoft Windows com base em Script Host](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Você verá Olá janela de diagnóstico, que descreve o que pode estar errado com a instalação a seguir.
   
    ![Um exemplo de janela de diagnóstico Olá](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Clique em "**Sim**" toolet Olá programa hello problemas que foram encontrados.
7. toosave essas alterações, feche todas as janelas do Internet Explorer e abra novamente o Internet Explorer.<br />Se você ainda não puder acessar seus aplicativos, tente Olá estas etapas.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Verifique que Olá que extensão do painel de acesso está habilitado
tooverify que Olá extensão do painel de acesso está habilitado no Internet Explorer:

1. No Internet Explorer, clique em Olá **ícone de engrenagem** no canto superior direito de saudação da janela de saudação. Em seguida, selecione **Opções da Internet**.<br />(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.
   
    ![Vá tooTools > Opções da Internet](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Clique em Olá **programas** guia, em seguida, clique em hello **gerenciar complementos** botão.
   
    ![Clique em Gerenciar complementos](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. Na caixa de diálogo, selecione **extensão do painel de acesso** e, em seguida, clique em Olá **habilitar** botão.
   
    ![Clique em Habilitar](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave essas alterações, feche todas as janelas do Internet Explorer e, em seguida, abra o Internet Explorer novamente.

## <a name="enable-extensions-for-inprivate-browsing"></a>Habilitar extensões para a navegação InPrivate
Se você estiver usando o modo de Navegação InPrivate hello:

1. No Internet Explorer, clique em Olá **ícone de engrenagem** no canto superior direito de saudação da janela de saudação. Em seguida, selecione **Opções da Internet**.<br />(Em versões mais antigas do Internet Explorer pode ser encontrada em **Ferramentas > Opções da Internet**.
   
    ![Um exemplo de janela de diagnóstico Olá](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Vá toohello **privacidade** guia, em seguida, **desmarque** Olá a caixa de seleção **desabilitar barras de ferramentas e extensões quando a navegação InPrivate é iniciado**</p>
   
    ![Desmarque a opção de desabilitar as barras de ferramentas e extensões quando começar a navegação InPrivate](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave essas alterações, feche todas as janelas do Internet Explorer e, em seguida, abra o Internet Explorer novamente.

## <a name="uninstall-hello-access-panel-extension"></a>Desinstalar Olá extensão do painel de acesso
Olá toouninstall extensão do painel de acesso do seu computador:

1. No teclado, pressione Olá **tecla Windows** tooopen menu de início de saudação. Quando o menu Olá estiver aberto, você pode digitar qualquer coisa toodo uma pesquisa. Digite "Painel de controle" e, em seguida, abra Olá **painel de controle** quando ele aparece nos resultados da pesquisa hello.
   
    ![Pesquise Painel de Controle](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. Olá canto superior direito da saudação painel de controle, alterar Olá **exibir** opção muito**ícones grandes**. Em seguida, localize e clique em Olá **programas e recursos** botão.
   
    ![Acompanhamento na Olá exibição tooshow ícones grandes](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Olá, selecione lista **extensão do painel de acesso**e clique em Olá de hello **desinstalação** botão.
   
    ![Clique em Desinstalar](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. Extensão de saudação tooinstall, em seguida, tente novamente toosee se Olá problema foi resolvido.

Se você encontrar problemas ao desinstalar a extensão hello, você também pode remover usando Olá [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) ferramenta.

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md)
* [Como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo](active-directory-saas-ie-group-policy.md)

