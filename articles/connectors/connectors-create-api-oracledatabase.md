---
title: "conector de banco de dados Oracle aaaAdd Olá em seus aplicativos do Azure lógica | Microsoft Docs"
description: "Usar o conector do banco de dados Oracle de saudação em um aplicativo de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="d4929-103">Introdução ao conector do banco de dados Oracle Olá</span><span class="sxs-lookup"><span data-stu-id="d4929-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="d4929-104">Usando o conector do banco de dados Oracle hello, crie o organizacionais fluxos de trabalho que usam dados no banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="d4929-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="d4929-105">Esse conector pode se conectar a tooan banco de dados do Oracle no local ou uma máquina virtual do Azure com o banco de dados Oracle instalado.</span><span class="sxs-lookup"><span data-stu-id="d4929-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="d4929-106">Com esse conector, você pode:</span><span class="sxs-lookup"><span data-stu-id="d4929-106">With this connector, you can:</span></span>

* <span data-ttu-id="d4929-107">Crie o fluxo de trabalho adicionando um novo cliente tooa clientes banco de dados, ou atualizando um pedido em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="d4929-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="d4929-108">Use ações tooget uma linha de dados, inserir uma nova linha e até mesmo excluir.</span><span class="sxs-lookup"><span data-stu-id="d4929-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="d4929-109">Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados Oracle (uma ação).</span><span class="sxs-lookup"><span data-stu-id="d4929-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="d4929-110">Este tópico mostra como toouse Olá conector de banco de dados Oracle em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="d4929-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4929-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4929-111">Prerequisites</span></span>

* <span data-ttu-id="d4929-112">Versões do Oracle com suporte:</span><span class="sxs-lookup"><span data-stu-id="d4929-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="d4929-113">Oracle 9 e versões posteriores</span><span class="sxs-lookup"><span data-stu-id="d4929-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="d4929-114">Software cliente do Oracle 8.1.7 e posteriores</span><span class="sxs-lookup"><span data-stu-id="d4929-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="d4929-115">Saudação de instalar o gateway de dados no local.</span><span class="sxs-lookup"><span data-stu-id="d4929-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="d4929-116">[Conecte-se a dados locais tooon de aplicativos lógicos](../logic-apps/logic-apps-gateway-connection.md) listas Olá etapas.</span><span class="sxs-lookup"><span data-stu-id="d4929-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="d4929-117">gateway de saudação é necessário tooconnect tooan banco de dados do Oracle no local ou uma VM do Azure com o banco de dados Oracle instalado.</span><span class="sxs-lookup"><span data-stu-id="d4929-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="d4929-118">gateway de dados local Olá atua como uma ponte e fornece uma transferência de dados segura entre os dados de local (dados que não está na nuvem Olá) e seus aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="d4929-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="d4929-119">Olá mesmo gateway pode ser usado com vários serviços e várias fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="d4929-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="d4929-120">Portanto, talvez seja necessário apenas gateway de saudação tooinstall uma vez.</span><span class="sxs-lookup"><span data-stu-id="d4929-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="d4929-121">Instale Olá cliente Oracle na máquina de saudação onde você instalou o gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="d4929-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="d4929-122">Certifique-se de que tooinstall hello provedor de dados Oracle de 64 bits para .NET do Oracle:</span><span class="sxs-lookup"><span data-stu-id="d4929-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="d4929-123">ODAC 12c Release 4 (12.1.0.2.4) de 64 bits para Windows x64</span><span class="sxs-lookup"><span data-stu-id="d4929-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="d4929-124">Se o cliente do Oracle Olá não estiver instalado, ocorrerá um erro quando você tentar toocreate ou usa conexão hello.</span><span class="sxs-lookup"><span data-stu-id="d4929-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="d4929-125">Consulte os erros comuns Olá neste tópico.</span><span class="sxs-lookup"><span data-stu-id="d4929-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="d4929-126">Adicionar Olá conector</span><span class="sxs-lookup"><span data-stu-id="d4929-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4929-127">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="d4929-127">This connector does not have any triggers.</span></span> <span data-ttu-id="d4929-128">Ele tem somente ações.</span><span class="sxs-lookup"><span data-stu-id="d4929-128">It has only actions.</span></span> <span data-ttu-id="d4929-129">Para quando você criar seu aplicativo lógico, adicionar outro toostart de gatilho sua lógica de aplicativo, como **agenda - recorrência**, ou **de solicitação / resposta - resposta**.</span><span class="sxs-lookup"><span data-stu-id="d4929-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="d4929-130">Em Olá [portal do Azure](https://portal.azure.com), criar um aplicativo em branco lógica.</span><span class="sxs-lookup"><span data-stu-id="d4929-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="d4929-131">No início de saudação do seu aplicativo lógico, selecione Olá **de solicitação / resposta - solicitação** gatilho:</span><span class="sxs-lookup"><span data-stu-id="d4929-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="d4929-132">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d4929-132">Select **Save**.</span></span> <span data-ttu-id="d4929-133">Quando você salva, a URL de uma solicitação é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d4929-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="d4929-134">Selecione **Nova etapa** e selecione **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="d4929-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="d4929-135">Digite `oracle` toosee Olá ações disponíveis:</span><span class="sxs-lookup"><span data-stu-id="d4929-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="d4929-136">Isso também é toosee de maneira mais rápida de Olá Olá gatilhos e ações disponíveis para qualquer conector.</span><span class="sxs-lookup"><span data-stu-id="d4929-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="d4929-137">Digite parte do nome do conector hello, como `oracle`.</span><span class="sxs-lookup"><span data-stu-id="d4929-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="d4929-138">designer de saudação lista todos os gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="d4929-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="d4929-139">Selecione uma das ações de saudação, como **banco de dados Oracle - Get linha**.</span><span class="sxs-lookup"><span data-stu-id="d4929-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="d4929-140">Selecione **Conectar por meio do gateway de dados local**.</span><span class="sxs-lookup"><span data-stu-id="d4929-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="d4929-141">Insira o nome do servidor Oracle hello, método de autenticação, nome de usuário, senha e selecione Olá gateway:</span><span class="sxs-lookup"><span data-stu-id="d4929-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="d4929-142">Uma vez conectado, selecione uma tabela da lista de saudação e inserir a tabela de tooyour de identificação de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4929-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="d4929-143">Você precisa de tabela de toohello tooknow Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="d4929-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="d4929-144">Se você não souber, contate o administrador de banco de dados Oracle e obter a saída Olá `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="d4929-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="d4929-145">Isso proporciona Olá necessário tooproceed de informações de identificação.</span><span class="sxs-lookup"><span data-stu-id="d4929-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="d4929-146">Em Olá exemplo a seguir, os dados do trabalho está sendo retornados de um banco de dados de recursos humanos:</span><span class="sxs-lookup"><span data-stu-id="d4929-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="d4929-147">Nesta próxima etapa, você pode usar qualquer Olá toobuild outros conectores seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d4929-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="d4929-148">Se você quiser tootest Obtendo dados do Oracle, envie por conta própria um email com os dados de Oracle hello usando uma saudação envie email conectores, Office 365 ou Gmail.</span><span class="sxs-lookup"><span data-stu-id="d4929-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="d4929-149">Usar os tokens dinâmico Olá de saudação do hello Oracle tabela toobuild `Subject` e `Body` do email:</span><span class="sxs-lookup"><span data-stu-id="d4929-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="d4929-150">**Salve** seu aplicativo lógico e selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="d4929-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="d4929-151">Fechar o designer de saudação e examine Olá executa histórico de status de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4929-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="d4929-152">Se ele falhar, selecione a linha de mensagem com falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4929-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="d4929-153">Olá designer é aberto e mostra qual etapa falha e também mostra Olá informações de erro.</span><span class="sxs-lookup"><span data-stu-id="d4929-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="d4929-154">Se tiver êxito, você receberá um email com informações de saudação que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="d4929-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="d4929-155">Ideias de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="d4929-155">Workflow ideas</span></span>

* <span data-ttu-id="d4929-156">Você deseja toomonitor Olá #oracle hashtag e colocar Olá tweets em um banco de dados para que possam ser consultados e usados em outros aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d4929-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="d4929-157">Em um aplicativo de lógica, adicionar Olá `Twitter - When a new tweet is posted` disparar e digite Olá **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="d4929-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="d4929-158">Em seguida, adicione Olá `Oracle Database - Insert row` ação e selecione a tabela:</span><span class="sxs-lookup"><span data-stu-id="d4929-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="d4929-159">As mensagens são enviadas tooa fila de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="d4929-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="d4929-160">Você deseja que essas mensagens tooget e colocá-los em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d4929-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="d4929-161">Em um aplicativo de lógica, adicionar Olá `Service Bus - when a message is received in a queue` gatilho e selecione Olá fila.</span><span class="sxs-lookup"><span data-stu-id="d4929-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="d4929-162">Em seguida, adicione Olá `Oracle Database - Insert row` ação e selecione a tabela:</span><span class="sxs-lookup"><span data-stu-id="d4929-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="d4929-163">Erros comuns</span><span class="sxs-lookup"><span data-stu-id="d4929-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="d4929-164">**Erro**: não é possível alcançar o hello Gateway</span><span class="sxs-lookup"><span data-stu-id="d4929-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="d4929-165">**Causa**: gateway de dados local Olá não é capaz de tooconnect toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="d4929-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="d4929-166">**Mitigação**: Verifique se o gateway está em execução na máquina local de saudação onde você instalou e que ele pode se conectar a toohello internet.</span><span class="sxs-lookup"><span data-stu-id="d4929-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="d4929-167">É recomendável não instalar o gateway de saudação em um computador que pode ser desativado ou suspensão.</span><span class="sxs-lookup"><span data-stu-id="d4929-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="d4929-168">Também é possível reiniciar o serviço de gateway de dados de local de saudação (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="d4929-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="d4929-169">**Erro**: Olá provedor que está sendo usado foi preterido: ' OracleClient exige software cliente Oracle versão 8.1.7 ou posterior.'.</span><span class="sxs-lookup"><span data-stu-id="d4929-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="d4929-170">Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) provedor oficial do tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="d4929-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="d4929-171">**Causa**: Olá Oracle cliente SDK não está instalado na máquina de saudação onde hello gateway de dados está em execução ao local.</span><span class="sxs-lookup"><span data-stu-id="d4929-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="d4929-172">**Resolução**: baixar e instalar o SDK de cliente Oracle Olá Olá mesmo computador que o gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="d4929-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="d4929-173">**Erro**: a tabela '[Nome_da_tabela]' não define colunas de chave</span><span class="sxs-lookup"><span data-stu-id="d4929-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="d4929-174">**Causa**: Olá tabela não tem nenhuma chave primária.</span><span class="sxs-lookup"><span data-stu-id="d4929-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="d4929-175">**Resolução**: conector do banco de dados Oracle Olá requer uma tabela com uma coluna de chave primária.</span><span class="sxs-lookup"><span data-stu-id="d4929-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="d4929-176">Não há suporte no momento</span><span class="sxs-lookup"><span data-stu-id="d4929-176">Currently not supported</span></span>

* <span data-ttu-id="d4929-177">Exibições e procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="d4929-177">Views and stored procedures</span></span> 
* <span data-ttu-id="d4929-178">Qualquer tabela com chaves compostas</span><span class="sxs-lookup"><span data-stu-id="d4929-178">Any table with composite keys</span></span>
* <span data-ttu-id="d4929-179">Tipos de objeto aninhados em tabelas</span><span class="sxs-lookup"><span data-stu-id="d4929-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="d4929-180">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="d4929-180">Connector-specific details</span></span>

<span data-ttu-id="d4929-181">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="d4929-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="d4929-182">Obtenha ajuda</span><span class="sxs-lookup"><span data-stu-id="d4929-182">Get some help</span></span>

<span data-ttu-id="d4929-183">Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) é um ótimo colocar tooask perguntas, responder a perguntas e veja o que outros usuários de aplicativos lógicos estão fazendo.</span><span class="sxs-lookup"><span data-stu-id="d4929-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="d4929-184">Você pode ajudar a melhorar os Aplicativos Lógicos e os conectores vitando e enviando suas ideias em [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d4929-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d4929-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4929-185">Next steps</span></span>
<span data-ttu-id="d4929-186">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)e explorar os conectores disponíveis Olá na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d4929-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
