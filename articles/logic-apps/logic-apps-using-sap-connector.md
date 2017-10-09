---
title: "aaaConnect tooan sistema SAP no Azure lógica de aplicativos local | Microsoft Docs"
description: "Conecte-se tooan no sistema local da SAP de seu fluxo de trabalho de aplicativo lógica por meio do gateway de dados local Olá"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="eb63d-103">Conecte-se tooan no sistema local da SAP de lógica de aplicativos com o conector do SAP Olá</span><span class="sxs-lookup"><span data-stu-id="eb63d-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="eb63d-104">gateway de dados local Olá permite toomanage dados e acessar com segurança os recursos que estão no local.</span><span class="sxs-lookup"><span data-stu-id="eb63d-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="eb63d-105">Este tópico mostra como você pode se conectar a lógica aplicativos tooan no sistema local da SAP.</span><span class="sxs-lookup"><span data-stu-id="eb63d-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="eb63d-106">Neste exemplo, seu aplicativo lógico solicita um IDOC via HTTP e envia a resposta de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="eb63d-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="eb63d-107">Limitações atuais:</span><span class="sxs-lookup"><span data-stu-id="eb63d-107">Current limitations:</span></span> 
> - <span data-ttu-id="eb63d-108">Seu aplicativo lógico expira se não concluir todas as etapas necessárias para a resposta de saudação dentro Olá [limite de solicitação](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="eb63d-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="eb63d-109">Nesse cenário, as solicitações podem ser bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="eb63d-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="eb63d-110">seletor de arquivo Hello não exibe todos os campos disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb63d-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="eb63d-111">Nesse cenário, você pode adicionar os caminhos manualmente.</span><span class="sxs-lookup"><span data-stu-id="eb63d-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb63d-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb63d-112">Prerequisites</span></span>

- <span data-ttu-id="eb63d-113">Instalar e configurar hello mais recente [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127) versão 1.15.6150.1 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="eb63d-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="eb63d-114">[Como tooconnect toohello no gateway de dados local em um aplicativo de lógica](http://aka.ms/logicapps-gateway) listas Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="eb63d-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="eb63d-115">gateway de saudação deve ser instalado em um computador local antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="eb63d-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="eb63d-116">Download e instalação hello mais recente SAP biblioteca de cliente em hello mesmo computador onde você instalou o gateway de dados hello.</span><span class="sxs-lookup"><span data-stu-id="eb63d-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="eb63d-117">Use qualquer Olá versões da SAP a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb63d-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="eb63d-118">Servidor SAP</span><span class="sxs-lookup"><span data-stu-id="eb63d-118">SAP Server</span></span>
        - <span data-ttu-id="eb63d-119">Qualquer servidor SAP que Olá suporte .NET conector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="eb63d-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="eb63d-120">Cliente SAP</span><span class="sxs-lookup"><span data-stu-id="eb63d-120">SAP Client</span></span>
        - <span data-ttu-id="eb63d-121">Conector SAP do .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="eb63d-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="eb63d-122">Adicionar gatilhos e ações para conectar-se o sistema do SAP tooyour</span><span class="sxs-lookup"><span data-stu-id="eb63d-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="eb63d-123">conector do SAP Olá tem ações, mas não a gatilhos.</span><span class="sxs-lookup"><span data-stu-id="eb63d-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="eb63d-124">Assim, temos toouse outro gatilho no início de saudação do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb63d-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="eb63d-125">Adicionar Olá gatilho de solicitação/resposta e, em seguida, selecione **nova etapa**.</span><span class="sxs-lookup"><span data-stu-id="eb63d-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="eb63d-126">Selecione **adicionar uma ação**e, em seguida, selecione o conector do SAP Olá digitando `SAP` no campo de pesquisa de saudação:</span><span class="sxs-lookup"><span data-stu-id="eb63d-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Selecionar Servidor de Aplicativos SAP ou Servidor de Mensagens SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="eb63d-128">Selecione [**Servidor de Aplicativos SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) ou [**Servidor de Mensagens SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), de acordo com a configuração do SAP.</span><span class="sxs-lookup"><span data-stu-id="eb63d-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="eb63d-129">Se você não tiver uma conexão existente, você é solicitado toocreate um.</span><span class="sxs-lookup"><span data-stu-id="eb63d-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="eb63d-130">Selecione **conectar por meio do gateway de dados local**e insira os detalhes de saudação para seu sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="eb63d-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Adicionar tooSAP de cadeia de caracteres de conexão](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="eb63d-132">Em **Gateway**, selecione um gateway existente ou tooinstall um novo gateway, selecione **instalar o Gateway**.</span><span class="sxs-lookup"><span data-stu-id="eb63d-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Instalar um novo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="eb63d-134">Depois de inserir todos os detalhes de saudação, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="eb63d-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="eb63d-135">Lógica de aplicativos configura e testa a conexão hello, certificando-se de que a conexão Olá funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="eb63d-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="eb63d-136">Insira um nome para a conexão SAP.</span><span class="sxs-lookup"><span data-stu-id="eb63d-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="eb63d-137">opções diferentes de SAP Olá agora estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="eb63d-137">hello different SAP options are now available.</span></span> <span data-ttu-id="eb63d-138">toofind categoria IDOC, selecione na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb63d-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="eb63d-139">Ou digite manualmente no caminho hello e resposta Olá selecione HTTP no hello **corpo** campo:</span><span class="sxs-lookup"><span data-stu-id="eb63d-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Ação do SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="eb63d-141">Adicionar ação de saudação para criar um **resposta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="eb63d-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="eb63d-142">mensagem de resposta de saudação deve ser de saída do SAP hello.</span><span class="sxs-lookup"><span data-stu-id="eb63d-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="eb63d-143">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="eb63d-143">Save your logic app.</span></span> <span data-ttu-id="eb63d-144">Testá-lo, enviando um IDOC por meio da URL do gatilho Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="eb63d-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="eb63d-145">Após Olá que IDOC é enviada, aguarde resposta de saudação do aplicativo lógico de saudação:</span><span class="sxs-lookup"><span data-stu-id="eb63d-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="eb63d-146">Check-out como muito[monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="eb63d-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="eb63d-147">Agora que o conector do SAP Olá é adicionado tooyour lógica aplicativo, comece a explorar outras funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="eb63d-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="eb63d-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="eb63d-148">BAPI</span></span>
- <span data-ttu-id="eb63d-149">RFC</span><span class="sxs-lookup"><span data-stu-id="eb63d-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="eb63d-150">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="eb63d-150">Get help</span></span>

<span data-ttu-id="eb63d-151">tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="eb63d-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="eb63d-152">toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="eb63d-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb63d-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb63d-153">Next steps</span></span>

- <span data-ttu-id="eb63d-154">Saiba como toovalidate, transformar e outras funções BizTalk no hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb63d-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="eb63d-155">[Conecte-se a dados locais tooon](../logic-apps/logic-apps-gateway-connection.md) de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="eb63d-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
