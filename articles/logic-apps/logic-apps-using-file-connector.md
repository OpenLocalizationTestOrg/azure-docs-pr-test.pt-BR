---
title: "sistemas de aplicativos do Azure lógica de arquivo local aaaConnect tooon | Microsoft Docs"
description: "Conectar sistemas de arquivo de tooon local de seu fluxo de trabalho de aplicativo lógica por meio do gateway de dados local hello e conector de sistema de arquivos"
keywords: sistemas de arquivos
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="1cfcb-104">Conectar sistemas de arquivos local tooon de lógica de aplicativos com o conector de saudação do sistema de arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="1cfcb-105">Conectividade de nuvem híbrida é toologic central aplicativos, dados de caso toomanage e com segurança acesso em recursos locais, seus aplicativos lógicos podem usar o gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="1cfcb-106">Neste artigo, mostramos como tooconnect tooan local sistema de arquivos com um cenário básico: copiar um arquivo que tooa de tooDropbox carregado compartilhamento de arquivos, em seguida, envie um email.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cfcb-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1cfcb-107">Prerequisites</span></span>

- <span data-ttu-id="1cfcb-108">Instalar e configurar hello mais recente [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="1cfcb-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="1cfcb-109">Instalar o gateway de dados mais recente no local hello, a versão 1.15.6150.1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="1cfcb-110">[Conecte-se o gateway de dados local toohello](http://aka.ms/logicapps-gateway) listas Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="1cfcb-111">gateway de saudação deve ser instalado em um computador local antes de continuar com o restante de saudação das etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="1cfcb-112">Adicionar o gatilho e ações para conectar-se o sistema de arquivos tooyour</span><span class="sxs-lookup"><span data-stu-id="1cfcb-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="1cfcb-113">Crie um aplicativo lógico e adicione este gatilho do Dropbox: **Quando um arquivo é criado**</span><span class="sxs-lookup"><span data-stu-id="1cfcb-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="1cfcb-114">Em um gatilho de saudação, escolha **próxima etapa** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="1cfcb-115">Na caixa de pesquisa hello, digite `file system` para que você possa exibir ações todos com suporte para o conector do sistema de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Procurar conector de arquivo](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="1cfcb-117">Escolha Olá **criar arquivo** ação e criar um sistema de arquivos de tooyour de conexão.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="1cfcb-118">Se você não tiver uma conexão existente, você é solicitado toocreate um.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="1cfcb-119">Escolha **Conectar por meio do gateway de dados local**.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="1cfcb-120">Outras propriedades serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-120">More properties appear.</span></span>
   2. <span data-ttu-id="1cfcb-121">Selecione a pasta raiz do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="1cfcb-122">Olá raiz pasta é Olá pai principal, que é usado para caminhos relativos para todas as ações relacionadas ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="1cfcb-123">Você pode especificar uma pasta local no computador de saudação onde o gateway de dados local hello está instalado ou pasta Olá pode ser um compartilhamento de rede que Olá máquina pode acessar.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="1cfcb-124">Digite hello username e password para gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="1cfcb-125">Selecione o gateway Olá instalada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-125">Select hello gateway that you previously installed.</span></span>

       ![Configurar conexão](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="1cfcb-127">Depois de fornecer todos os detalhes de saudação, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="1cfcb-128">Lógica de aplicativos configura e testa a conexão, certificando-se de que a conexão Olá funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="1cfcb-129">Se a conexão hello está configurado corretamente, você verá opções para a ação de saudação que você selecionou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="1cfcb-130">conector de sistema de arquivo Hello agora está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="1cfcb-131">Especifique que você deseja toocopy arquivos da pasta do Dropbox toohello raiz para o compartilhamento de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Ação Criar arquivo](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="1cfcb-133">Depois de seu arquivo de saudação de cópias de aplicativo lógica, adicione uma ação do Outlook que envia um email para que usuários relevantes saber sobre o novo arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="1cfcb-134">Insira os destinatários hello, o título e o corpo do email hello.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="1cfcb-135">No seletor de conteúdo dinâmico Olá, você pode escolher saídas de dados do conector de arquivo hello, assim você pode adicionar o email de toohello mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Ação Enviar email](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="1cfcb-137">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-137">Save your logic app.</span></span> <span data-ttu-id="1cfcb-138">Teste seu aplicativo carregando um arquivo tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="1cfcb-139">arquivo Hello deve conseguir um compartilhamento de arquivos copiados toohello local e você receberá um email sobre a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="1cfcb-140">Saiba como muito[monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1cfcb-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="1cfcb-141">Parabéns, você agora tem um aplicativo de lógica de trabalho que pode conectar-se o sistema de arquivos local tooyour.</span><span class="sxs-lookup"><span data-stu-id="1cfcb-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="1cfcb-142">Tente explorar outras funcionalidades que Olá ofertas de conector, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1cfcb-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="1cfcb-143">Criar arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-143">Create file</span></span>
- <span data-ttu-id="1cfcb-144">Lista de arquivos na pasta</span><span class="sxs-lookup"><span data-stu-id="1cfcb-144">List files in folder</span></span>
- <span data-ttu-id="1cfcb-145">Acrescentar arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-145">Append file</span></span>
- <span data-ttu-id="1cfcb-146">Excluir arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-146">Delete file</span></span>
- <span data-ttu-id="1cfcb-147">Obter conteúdo do arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-147">Get file content</span></span>
- <span data-ttu-id="1cfcb-148">Obter o conteúdo do arquivo usando o caminho</span><span class="sxs-lookup"><span data-stu-id="1cfcb-148">Get file content using path</span></span>
- <span data-ttu-id="1cfcb-149">Obter Metadados do Arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-149">Get file metadata</span></span>
- <span data-ttu-id="1cfcb-150">Obter Metadados do Arquivo usando o caminho</span><span class="sxs-lookup"><span data-stu-id="1cfcb-150">Get file metadata using path</span></span>
- <span data-ttu-id="1cfcb-151">Lista de arquivos na pasta-raiz</span><span class="sxs-lookup"><span data-stu-id="1cfcb-151">List files in root folder</span></span>
- <span data-ttu-id="1cfcb-152">Atualizar arquivo</span><span class="sxs-lookup"><span data-stu-id="1cfcb-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="1cfcb-153">Swagger de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="1cfcb-153">View hello swagger</span></span>
<span data-ttu-id="1cfcb-154">Consulte Olá [swagger detalhes](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="1cfcb-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="1cfcb-155">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="1cfcb-155">Get help</span></span>

<span data-ttu-id="1cfcb-156">tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1cfcb-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1cfcb-157">toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1cfcb-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cfcb-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1cfcb-158">Next steps</span></span>

- <span data-ttu-id="1cfcb-159">[Conecte-se a dados locais tooon](../logic-apps/logic-apps-gateway-connection.md) de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="1cfcb-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="1cfcb-160">Saiba mais sobre a [integração de empresas](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1cfcb-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
