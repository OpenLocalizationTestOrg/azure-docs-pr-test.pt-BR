---
title: "Instalação do Kit de Ferramentas do Azure para IntelliJ | Microsoft Docs"
description: Saiba como instalar o Kit de Ferramentas do Azure para o IDEA do IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bf11a8580500f78c4a96a02953f221501eeffe6c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="3352d-103">Instalação do Kit de Ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="3352d-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="3352d-104">O Kit de Ferramentas do Azure para IntelliJ fornece modelos e funcionalidade que permitem criar, desenvolver, testar e implantar com facilidade aplicativos Azure usando o ambiente de desenvolvimento IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3352d-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="3352d-105">O Kit de Ferramentas do Azure para IntelliJ é um projeto de código-fonte aberto, cujo código-fonte está disponível de acordo com a Licença do MIT no site do projeto no GitHub na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="3352d-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="3352d-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="3352d-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="3352d-107">Há dois métodos de instalação do Kit de Ferramentas do Azure para IntelliJ, na caixa de diálogo de Configurações e no menu Configurar na tela inicial; ambos os métodos de instalação serão demonstrados nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3352d-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="3352d-108">Para instalar o Kit de Ferramentas do Azure para IntelliJ na caixa de diálogo de configurações</span><span class="sxs-lookup"><span data-stu-id="3352d-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>
1. <span data-ttu-id="3352d-109">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3352d-109">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="3352d-110">Quando o IDEA do IntelliJ é aberto, clique em **Arquivo**, em seguida, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="3352d-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
    ![Abra a caixa de diálogo Configurações do IDEA do IntelliJ][01a]
3. <span data-ttu-id="3352d-112">Na caixa de diálogo Configurações, clique em **Plug-ins** e, em seguida, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="3352d-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
    ![Caixa de diálogo Configurações do IDEA do IntelliJ][02a]
4. <span data-ttu-id="3352d-114">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3352d-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="3352d-115">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="3352d-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
    <span data-ttu-id="3352d-117">O IDEA do IntelliJ exibirá o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3352d-117">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Progresso da instalação][04]
5. <span data-ttu-id="3352d-119">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="3352d-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Reiniciar IDEA do IntelliJ][05]
6. <span data-ttu-id="3352d-121">Clique em **OK** para fechar a caixa de diálogo Configurações.</span><span class="sxs-lookup"><span data-stu-id="3352d-121">Click **OK** to close the Settings dialog box.</span></span>
   
    ![Feche a caixa de diálogo Configurações do IDEA do IntelliJ][06]
7. <span data-ttu-id="3352d-123">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="3352d-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Reiniciar IDEA do IntelliJ][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="3352d-125">Para instalar o Kit de Ferramentas do Azure para IntelliJ a partir da tela inicial</span><span class="sxs-lookup"><span data-stu-id="3352d-125">To install the Azure Toolkit for IntelliJ from the start screen</span></span>
1. <span data-ttu-id="3352d-126">Inicie o IDEA do IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="3352d-126">Start IntelliJ IDEA.</span></span>
2. <span data-ttu-id="3352d-127">Quando for exibida a tela inicial do IDEA do IntelliJ, clique em **Configurar**, em seguida, clique em **Plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="3352d-127">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
    ![Instale os plug-ins do IDEA do IntelliJ][01b]
3. <span data-ttu-id="3352d-129">Na caixa de diálogo **Plug-ins**, clique em **Procurar repositórios**.</span><span class="sxs-lookup"><span data-stu-id="3352d-129">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
    ![Procure os repositórios de plug-in do IDEA do IntelliJ][02b]
4. <span data-ttu-id="3352d-131">Na caixa de diálogo **Procurar repositórios** , digite "Azure" na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3352d-131">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="3352d-132">Realce **Kit de Ferramentas do Azure para IntelliJ** e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="3352d-132">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
    ![Procure o Kit de Ferramentas do Azure para IntelliJ][03]
   
    <span data-ttu-id="3352d-134">O IDEA do IntelliJ exibirá o progresso da instalação em uma caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3352d-134">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
    ![Progresso da instalação][04]
5. <span data-ttu-id="3352d-136">Quando a instalação for concluída, clique em **Reiniciar IDEA do IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="3352d-136">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
    ![Reiniciar IDEA do IntelliJ][05]
6. <span data-ttu-id="3352d-138">Quando for solicitado a reiniciar o IDEA do IntelliJ ou adiar, clique em **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="3352d-138">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
    ![Reiniciar IDEA do IntelliJ][07]

## <a name="see-also"></a><span data-ttu-id="3352d-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3352d-140">See Also</span></span>
<span data-ttu-id="3352d-141">Para obter mais informações sobre os kits de ferramentas do Azure para Java IDEs, confira os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="3352d-141">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="3352d-142">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3352d-142">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3352d-143">[Novidades no Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3352d-143">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3352d-144">[Instalação do Kit de Ferramentas do Azure para o Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3352d-144">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3352d-145">[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3352d-145">[Sign In Instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3352d-146">[Criar um aplicativo Web Hello World para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3352d-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="3352d-147">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3352d-147">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3352d-148">[Novidades no Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3352d-148">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3352d-149">*Instalação do Kit de Ferramentas do Azure para IntelliJ (Este artigo)*</span><span class="sxs-lookup"><span data-stu-id="3352d-149">*Installing the Azure Toolkit for IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="3352d-150">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3352d-150">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3352d-151">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3352d-151">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="3352d-152">Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="3352d-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="3352d-153">[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="3352d-153">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="3352d-154">[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="3352d-154">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="3352d-155">[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3352d-155">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3352d-156">[Criar um aplicativo Web Hello World para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="3352d-156">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="3352d-157">[Instalação do Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="3352d-157">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
<span data-ttu-id="3352d-158">[Instruções de entrada para o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3352d-158">[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="3352d-159">[Instruções de entrada para o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="3352d-159">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="3352d-160">[Novidades no Kit de Ferramentas do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3352d-160">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="3352d-161">[Novidades no Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="3352d-161">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="3352d-162">[Central de desenvolvimento Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="3352d-162">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>

<!-- IMG List -->

[01a]: ./media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: ./media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: ./media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: ./media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: ./media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: ./media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: ./media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: ./media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: ./media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
