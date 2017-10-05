---
title: "Conectar a um sistema SAP local no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Conectar ao sistema SAP local no fluxo de trabalho do aplicativo lógico por meio do gateway de dados local"
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
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="d99d1-103">Conectar a um sistema SAP local por meio de aplicativos lógicos com o conector do SAP</span><span class="sxs-lookup"><span data-stu-id="d99d1-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="d99d1-104">O gateway de dados local permite gerenciar dados e acessar com segurança recursos locais.</span><span class="sxs-lookup"><span data-stu-id="d99d1-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="d99d1-105">Este tópico mostra como é possível conectar aplicativos lógicos a um sistema SAP local.</span><span class="sxs-lookup"><span data-stu-id="d99d1-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="d99d1-106">Neste exemplo, o aplicativo lógico solicita um IDOC por HTTP e envia a resposta de volta.</span><span class="sxs-lookup"><span data-stu-id="d99d1-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="d99d1-107">Limitações atuais:</span><span class="sxs-lookup"><span data-stu-id="d99d1-107">Current limitations:</span></span> 
> - <span data-ttu-id="d99d1-108">O aplicativo lógico atingirá o tempo limite se todas as etapas necessárias para a resposta não forem concluídas dentro do [tempo limite de solicitação](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="d99d1-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="d99d1-109">Nesse cenário, as solicitações podem ser bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="d99d1-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="d99d1-110">O seletor de arquivos não exibe todos os campos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d99d1-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="d99d1-111">Nesse cenário, você pode adicionar os caminhos manualmente.</span><span class="sxs-lookup"><span data-stu-id="d99d1-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d99d1-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d99d1-112">Prerequisites</span></span>

- <span data-ttu-id="d99d1-113">Instale e configure a versão mais recente do [gateway de dados local](https://www.microsoft.com/download/details.aspx?id=53127), versão 1.15.6150.1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="d99d1-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="d99d1-114">[Como conectar-se ao gateway de dados local em um aplicativo lógico](http://aka.ms/logicapps-gateway) lista as etapas.</span><span class="sxs-lookup"><span data-stu-id="d99d1-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="d99d1-115">O gateway deve ser instalado em um computador local antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="d99d1-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="d99d1-116">Baixe e instale a biblioteca de cliente SAP mais recente no mesmo computador em que você instalou o gateway de dados.</span><span class="sxs-lookup"><span data-stu-id="d99d1-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="d99d1-117">Use qualquer uma das versões de SAP a seguir:</span><span class="sxs-lookup"><span data-stu-id="d99d1-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="d99d1-118">Servidor SAP</span><span class="sxs-lookup"><span data-stu-id="d99d1-118">SAP Server</span></span>
        - <span data-ttu-id="d99d1-119">Qualquer Servidor SAP compatível com o .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="d99d1-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="d99d1-120">Cliente SAP</span><span class="sxs-lookup"><span data-stu-id="d99d1-120">SAP Client</span></span>
        - <span data-ttu-id="d99d1-121">Conector SAP do .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="d99d1-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="d99d1-122">Adicionar gatilhos e ações para conectar ao sistema SAP</span><span class="sxs-lookup"><span data-stu-id="d99d1-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="d99d1-123">O conector do SAP tem ações, mas não gatilhos.</span><span class="sxs-lookup"><span data-stu-id="d99d1-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="d99d1-124">Portanto, precisamos usar outro gatilho no início do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d99d1-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="d99d1-125">Adicione o gatilho Solicitação/Resposta e, em seguida, selecione **Nova etapa**.</span><span class="sxs-lookup"><span data-stu-id="d99d1-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="d99d1-126">Selecione **Adicionar uma ação** e, em seguida, escolha o conector SAP digitando `SAP` no campo de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="d99d1-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Selecionar Servidor de Aplicativos SAP ou Servidor de Mensagens SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="d99d1-128">Selecione [**Servidor de Aplicativos SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) ou [**Servidor de Mensagens SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), de acordo com a configuração do SAP.</span><span class="sxs-lookup"><span data-stu-id="d99d1-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="d99d1-129">Caso não tenha uma conexão existente, é solicitado que você crie uma.</span><span class="sxs-lookup"><span data-stu-id="d99d1-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="d99d1-130">Selecione **Conectar-se por meio do gateway de dados local** e insira os detalhes do sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="d99d1-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Adicionar cadeia de conexão ao SAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="d99d1-132">Em **Gateway**, selecione um gateway existente ou, para instalar um novo gateway, selecione **Instalar Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d99d1-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Instalar um novo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="d99d1-134">Após inserir todos os detalhes, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d99d1-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="d99d1-135">Os Aplicativos Lógicos configuram e testam a conexão, garantindo seu funcionamento correto.</span><span class="sxs-lookup"><span data-stu-id="d99d1-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="d99d1-136">Insira um nome para a conexão SAP.</span><span class="sxs-lookup"><span data-stu-id="d99d1-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="d99d1-137">Agora, as diferentes opções de SAP estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d99d1-137">The different SAP options are now available.</span></span> <span data-ttu-id="d99d1-138">Para localizar a categoria do IDOC, selecione uma na lista.</span><span class="sxs-lookup"><span data-stu-id="d99d1-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="d99d1-139">Ou digite manualmente o caminho e selecione a resposta HTTP no campo **corpo**:</span><span class="sxs-lookup"><span data-stu-id="d99d1-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![Ação do SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="d99d1-141">Adicione a ação para criar uma **resposta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d99d1-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="d99d1-142">A mensagem de resposta deve se originar da saída do SAP.</span><span class="sxs-lookup"><span data-stu-id="d99d1-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="d99d1-143">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d99d1-143">Save your logic app.</span></span> <span data-ttu-id="d99d1-144">Teste-o enviando um IDOC por meio da URL de gatilho HTTP.</span><span class="sxs-lookup"><span data-stu-id="d99d1-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="d99d1-145">Após o envio do IDOC, aguarde a resposta do aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="d99d1-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="d99d1-146">Confira como [monitorar seus Aplicativos Lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d99d1-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="d99d1-147">Com o conector SAP adicionado ao aplicativo lógico, comece a explorar outras funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="d99d1-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="d99d1-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="d99d1-148">BAPI</span></span>
- <span data-ttu-id="d99d1-149">RFC</span><span class="sxs-lookup"><span data-stu-id="d99d1-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="d99d1-150">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="d99d1-150">Get help</span></span>

<span data-ttu-id="d99d1-151">Para fazer perguntas, responder a perguntas e saber o que os outros usuários dos Aplicativos Lógicos do Azure estão fazendo, visite o [fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d99d1-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d99d1-152">Para ajudar a melhorar os Aplicativos Lógicos do Azure e conectores, vote ou envie ideias no [site de comentários do usuário dos Aplicativos Lógicos do Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d99d1-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d99d1-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d99d1-153">Next steps</span></span>

- <span data-ttu-id="d99d1-154">Saiba como validar, transformar e outras funções semelhantes ao BizTalk no [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d99d1-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="d99d1-155">[Conectar-se a dados locais](../logic-apps/logic-apps-gateway-connection.md) por meio de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="d99d1-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
