---
title: "Saiba como usar o conector de FTP em aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se ao servidor FTP para gerenciar seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no servidor FTP."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="ca8e7-105">Introdução ao conector de FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-105">Get started with the FTP connector</span></span>
<span data-ttu-id="ca8e7-106">Use o conector de FTP para monitorar, gerenciar e criar arquivos em um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="ca8e7-107">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="ca8e7-108">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="ca8e7-109">Conectar-se ao FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-109">Connect to FTP</span></span>
<span data-ttu-id="ca8e7-110">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="ca8e7-111">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="ca8e7-112">Criar uma conexão com o FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="ca8e7-113">Usar o gatilho de FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-113">Use a FTP trigger</span></span>
<span data-ttu-id="ca8e7-114">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="ca8e7-115">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ca8e7-116">O conector de FTP exige um servidor FTP que possa ser acessado pela Internet e esteja configurado para operar com o modo PASSIVO.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="ca8e7-117">Além disso, o conector de FTP **não é compatível com FTPS implícito (FTP por SSL)**.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="ca8e7-118">O conector de FTP permite apenas FTPS explícito (FTP por SSL).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="ca8e7-119">Neste exemplo, mostrarei como usar o gatilho **FTP – Quando um arquivo é adicionado ou modificado** para iniciar um fluxo de trabalho do aplicativo lógico quando um arquivo é adicionado, ou modificado, em um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="ca8e7-120">Em um exemplo corporativo, você pode usar esse gatilho para monitorar uma pasta FTP em busca de novos arquivos que representam pedidos de clientes.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="ca8e7-121">Você pode usar uma ação de conector FTP, como **Obter conteúdo do arquivo** para obter o conteúdo do pedido para processamento posterior e armazenamento em seu banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="ca8e7-122">Digite *ftp* na caixa de pesquisa no designer de aplicativos lógicos e selecione o gatilho **FTP - Quando um arquivo é criado ou modificado**</span><span class="sxs-lookup"><span data-stu-id="ca8e7-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="ca8e7-123">![Imagem 1 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="ca8e7-124">O controle **Quando um arquivo é adicionado ou modificado** é aberto</span><span class="sxs-lookup"><span data-stu-id="ca8e7-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="ca8e7-125">![Imagem 2 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="ca8e7-126">Escolha **...** , localizado no lado direito do controle.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="ca8e7-127">Isso abre o controle de seletor de pasta </span><span class="sxs-lookup"><span data-stu-id="ca8e7-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="ca8e7-128">![Imagem 3 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="ca8e7-129">Escolha **>** (seta para a direita) e procure a pasta que deseja monitorar em busca de arquivos novos ou modificados.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="ca8e7-130">Selecione a pasta e observe que a pasta agora é exibida no controle **Pasta**.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="ca8e7-131">![Imagem 4 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="ca8e7-132">Neste ponto, seu aplicativo lógico foi configurado com um gatilho que iniciará uma execução de outros gatilhos e as ações no fluxo de trabalho quando um arquivo é, ou modificado, ou criado, na pasta FTP específica.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca8e7-133">Para que um aplicativo lógico funcione, ele deve conter pelo menos um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="ca8e7-134">Siga as etapas na próxima seção para adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="ca8e7-135">Usar uma ação de FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-135">Use a FTP action</span></span>
<span data-ttu-id="ca8e7-136">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ca8e7-137">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="ca8e7-138">Agora que você adicionou um gatilho, siga estas etapas para adicionar uma ação que obterá o conteúdo do arquivo novo ou modificado encontrado pelo gatilho.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="ca8e7-139">Escolha **+ Nova etapa** a fim de adicionar a ação para obter o conteúdo do arquivo no servidor FTP</span><span class="sxs-lookup"><span data-stu-id="ca8e7-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="ca8e7-140">Selecione o link **Adicionar uma ação** .</span><span class="sxs-lookup"><span data-stu-id="ca8e7-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="ca8e7-141">![Imagem 1 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="ca8e7-142">Insira *FTP* para pesquisar todas as ações relacionadas ao FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="ca8e7-143">Escolha **FTP - Obter conteúdo do arquivo** como a ação a ser tomada quando um arquivo novo ou modificado é encontrado na pasta FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="ca8e7-144">![Imagem 2 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="ca8e7-145">O controle **Obter conteúdo do arquivo** é aberto.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-145">The **Get file content** control opens.</span></span> <span data-ttu-id="ca8e7-146">**Observação**: será solicitado que você autorize o aplicativo lógico a acessar sua conta no servidor FTP, caso não tenha feito isso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="ca8e7-147">![Imagem 3 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="ca8e7-148">Escolha o controle **Arquivo** (o espaço em branco localizado abaixo de **ARQUIVO***).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="ca8e7-149">Aqui, você pode usar qualquer uma das várias propriedades do arquivo novo ou modificado encontrado no servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="ca8e7-150">Escolha a opção **Conteúdo do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="ca8e7-151">![Imagem 4 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="ca8e7-152">O controle é atualizado, indicando que a ação **FTP – Obter conteúdo do arquivo** obterá o *conteúdo do arquivo* novo ou modificado no servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="ca8e7-153">![Imagem 5 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="ca8e7-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="ca8e7-154">Salve seu trabalho e adicione um arquivo à pasta FTP para testar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="ca8e7-155">Neste ponto, o aplicativo lógico foi configurado com um gatilho para monitorar uma pasta em um servidor FTP e iniciar o fluxo de trabalho quando encontrar um arquivo novo ou modificado no servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="ca8e7-156">O aplicativo lógico também foi configurado com uma ação para obter o conteúdo do arquivo novo ou modificado.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="ca8e7-157">Agora você pode adicionar outra ação, como a ação [SQL Server – inserir linha](connectors-create-api-sqlazure.md), para inserir o conteúdo do arquivo novo ou modificado em uma tabela de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ca8e7-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="ca8e7-158">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="ca8e7-158">Connector-specific details</span></span>

<span data-ttu-id="ca8e7-159">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="ca8e7-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca8e7-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca8e7-160">Next Steps</span></span>
[<span data-ttu-id="ca8e7-161">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="ca8e7-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

