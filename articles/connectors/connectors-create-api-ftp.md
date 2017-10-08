---
title: "aaaLearn como toouse Olá conector FTP em aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte tooFTP server toomanage seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no servidor FTP."
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
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="a10a5-105">Introdução ao conector FTP Olá</span><span class="sxs-lookup"><span data-stu-id="a10a5-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="a10a5-106">Use Olá FTP conector toomonitor, gerenciar e criar arquivos em um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="a10a5-107">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a10a5-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a10a5-108">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a10a5-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="a10a5-109">Conecte-se tooFTP</span><span class="sxs-lookup"><span data-stu-id="a10a5-109">Connect tooFTP</span></span>
<span data-ttu-id="a10a5-110">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="a10a5-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a10a5-111">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="a10a5-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="a10a5-112">Criar uma conexão tooFTP</span><span class="sxs-lookup"><span data-stu-id="a10a5-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="a10a5-113">Usar o gatilho de FTP</span><span class="sxs-lookup"><span data-stu-id="a10a5-113">Use a FTP trigger</span></span>
<span data-ttu-id="a10a5-114">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a10a5-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a10a5-115">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a10a5-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a10a5-116">conector FTP Olá requer um servidor FTP que é acessível de saudação à Internet e é configurado toooperate com modo passivo.</span><span class="sxs-lookup"><span data-stu-id="a10a5-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="a10a5-117">Além disso, o conector Olá FTP é **não é compatível com implícita FTPS (FTP sobre SSL)**.</span><span class="sxs-lookup"><span data-stu-id="a10a5-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="a10a5-118">conector FTP Olá suporta apenas explícita FTPS (FTP sobre SSL).</span><span class="sxs-lookup"><span data-stu-id="a10a5-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="a10a5-119">Neste exemplo, mostrarei como Olá toouse **FTP - quando um arquivo é adicionado ou modificado** disparar um fluxo de trabalho do aplicativo de lógica de tooinitiate quando um arquivo é adicionado ao ou modificado em um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="a10a5-120">Um exemplo de empresa, você pode usar toomonitor esse gatilho uma pasta FTP para novos arquivos que representam os pedidos de clientes.</span><span class="sxs-lookup"><span data-stu-id="a10a5-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="a10a5-121">Você pode usar uma ação de conector FTP como **obter conteúdo do arquivo** tooget conteúdo de saudação de ordem de saudação para processamento e armazenamento no banco de dados Pedidos.</span><span class="sxs-lookup"><span data-stu-id="a10a5-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="a10a5-122">Digite *ftp* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **FTP - quando um arquivo é adicionado ou modificado** gatilho</span><span class="sxs-lookup"><span data-stu-id="a10a5-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="a10a5-123">![Imagem 1 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="a10a5-124">Olá **quando um arquivo é adicionado ou modificado** controle abre</span><span class="sxs-lookup"><span data-stu-id="a10a5-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="a10a5-125">![Imagem 2 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="a10a5-126">Selecione Olá **...**  localizado no lado direito de saudação do controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="a10a5-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="a10a5-127">Isso abre o controle de seletor de pasta Olá</span><span class="sxs-lookup"><span data-stu-id="a10a5-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="a10a5-128">![Imagem 3 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="a10a5-129">Selecione Olá  **>**  (seta para a direita) e procure a pasta de saudação toofind que você deseja toomonitor para arquivos novos ou modificados.</span><span class="sxs-lookup"><span data-stu-id="a10a5-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="a10a5-130">Selecionar pasta hello e observe a pasta Olá agora é exibida no hello **pasta** controle.</span><span class="sxs-lookup"><span data-stu-id="a10a5-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="a10a5-131">![Imagem 4 do gatilho de FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="a10a5-132">Neste ponto, seu aplicativo lógica foi configurado com um gatilho que começará uma execução de saudação outros gatilhos e ações no fluxo de trabalho hello quando um arquivo é modificado ou criado na pasta FTP específica hello.</span><span class="sxs-lookup"><span data-stu-id="a10a5-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="a10a5-133">Para uma lógica aplicativo toobe funcional, ele deve conter pelo menos um gatilho e uma ação.</span><span class="sxs-lookup"><span data-stu-id="a10a5-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="a10a5-134">Siga as etapas de Olá Olá tooadd próximo da seção uma ação.</span><span class="sxs-lookup"><span data-stu-id="a10a5-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="a10a5-135">Usar uma ação de FTP</span><span class="sxs-lookup"><span data-stu-id="a10a5-135">Use a FTP action</span></span>
<span data-ttu-id="a10a5-136">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="a10a5-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a10a5-137">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a10a5-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="a10a5-138">Agora que você adicionou um gatilho, siga essas etapas tooadd uma ação que obterão o conteúdo de saudação do arquivo de novos ou modificados de Olá encontrado pelo gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="a10a5-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="a10a5-139">Selecione **+ nova etapa** tooadd Olá Olá ação tooget Olá conteúdo de Olá arquivo no servidor de saudação FTP</span><span class="sxs-lookup"><span data-stu-id="a10a5-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="a10a5-140">Selecione Olá **adicionar uma ação** link.</span><span class="sxs-lookup"><span data-stu-id="a10a5-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="a10a5-141">![Imagem 1 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="a10a5-142">Digite *FTP* toosearch para todas as ações relacionadas tooFTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="a10a5-143">Selecione **FTP - obter o conteúdo do arquivo** como Olá tootake ação quando um arquivo novo ou modificado for encontrado na pasta de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="a10a5-144">![Imagem 2 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="a10a5-145">Olá **obter conteúdo do arquivo** controlar é aberta.</span><span class="sxs-lookup"><span data-stu-id="a10a5-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="a10a5-146">**Observação**: você será solicitado tooauthorize tooaccess de aplicativo sua lógica de conta, seu servidor FTP se você não tiver feito isso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a10a5-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="a10a5-147">![Imagem 3 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="a10a5-148">Selecione Olá **arquivo** controle (espaço em branco Olá localizada abaixo **arquivo***).</span><span class="sxs-lookup"><span data-stu-id="a10a5-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="a10a5-149">Aqui, você pode usar qualquer Olá em várias propriedades de arquivo novo ou modificado Olá encontrado no servidor FTP hello.</span><span class="sxs-lookup"><span data-stu-id="a10a5-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="a10a5-150">Selecione Olá **o conteúdo do arquivo** opção.</span><span class="sxs-lookup"><span data-stu-id="a10a5-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="a10a5-151">![Imagem 4 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="a10a5-152">controle de saudação é atualizado, indicando que Olá **FTP - obter o conteúdo do arquivo** ação obterá Olá *o conteúdo do arquivo* do arquivo de saudação novos ou modificados no servidor de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="a10a5-153">![Imagem 5 da ação de FTP](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="a10a5-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="a10a5-154">Salve seu trabalho e adicione um tootest de pasta do arquivo toohello FTP seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a10a5-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="a10a5-155">Neste ponto, Olá lógica aplicativo tiver sido configurado com toomonitor um gatilho uma pasta em um servidor FTP e o fluxo de trabalho Iniciar hello quando encontra um novo arquivo ou um arquivo modificado no servidor de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="a10a5-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="a10a5-156">Olá lógica aplicativo também foi configurado com um conteúdo de saudação tooget ação de arquivo novo ou modificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="a10a5-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="a10a5-157">Agora você pode adicionar outra ação como Olá [SQL Server - Inserir linha](connectors-create-api-sqlazure.md) ação tooinsert Olá conteúdo Olá novos ou modificados arquivo em uma tabela de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a10a5-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="a10a5-158">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="a10a5-158">Connector-specific details</span></span>

<span data-ttu-id="a10a5-159">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="a10a5-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a10a5-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a10a5-160">Next Steps</span></span>
[<span data-ttu-id="a10a5-161">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a10a5-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

