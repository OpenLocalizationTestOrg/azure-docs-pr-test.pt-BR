---
title: "Adicionar o conector do Banco de Dados Oracle em seus Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Usar o conector do Banco de Dados Oracle em um aplicativo lógico"
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
ms.openlocfilehash: cc64441617eb5e7d5e70c1cf5c491a672428bc51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="8af34-103">Introdução ao conector do Banco de Dados Oracle</span><span class="sxs-lookup"><span data-stu-id="8af34-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="8af34-104">Com o conector do Banco de Dados Oracle, você cria fluxos de trabalho organizacionais que usam os dados em seu banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="8af34-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="8af34-105">Esse conector pode se conectar ao Banco de Dados Oracle local, ou a uma máquina virtual do Azure com o Banco de Dados Oracle instalado.</span><span class="sxs-lookup"><span data-stu-id="8af34-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="8af34-106">Com esse conector, você pode:</span><span class="sxs-lookup"><span data-stu-id="8af34-106">With this connector, you can:</span></span>

* <span data-ttu-id="8af34-107">Compile o fluxo de trabalho adicionando um novo cliente a um banco de dados de clientes ou atualizando um pedido em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="8af34-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="8af34-108">Use as ações para obter uma linha de dados, inserir uma nova linha e até mesmo excluir.</span><span class="sxs-lookup"><span data-stu-id="8af34-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="8af34-109">Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados Oracle (uma ação).</span><span class="sxs-lookup"><span data-stu-id="8af34-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="8af34-110">Este tópico mostra como usar o conector do Banco de Dados Oracle um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8af34-110">This topic shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8af34-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8af34-111">Prerequisites</span></span>

* <span data-ttu-id="8af34-112">Versões do Oracle com suporte:</span><span class="sxs-lookup"><span data-stu-id="8af34-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="8af34-113">Oracle 9 e versões posteriores</span><span class="sxs-lookup"><span data-stu-id="8af34-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="8af34-114">Software cliente do Oracle 8.1.7 e posteriores</span><span class="sxs-lookup"><span data-stu-id="8af34-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="8af34-115">Instalar o gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="8af34-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="8af34-116">[Conectar-se a dados locais de aplicativos lógicos](../logic-apps/logic-apps-gateway-connection.md) lista as etapas.</span><span class="sxs-lookup"><span data-stu-id="8af34-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="8af34-117">O gateway é necessário para se conectar ao Banco de Dados Oracle local, ou uma VM do Azure com o Banco de Dados Oracle instalado.</span><span class="sxs-lookup"><span data-stu-id="8af34-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8af34-118">O gateway de dados local atua como uma ponte e fornece transferência de dados segura entre dados locais (dados que não estão na nuvem) e seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8af34-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="8af34-119">O mesmo gateway pode ser usado com vários serviços e várias fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="8af34-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="8af34-120">Assim, você só precisará instalar o gateway uma vez.</span><span class="sxs-lookup"><span data-stu-id="8af34-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="8af34-121">Instale o Cliente Oracle no computador onde você instalou o gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="8af34-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="8af34-122">Instale o Provedor de Dados do Oracle de 64 bits para .NET a partir do Oracle:</span><span class="sxs-lookup"><span data-stu-id="8af34-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="8af34-123">ODAC 12c Release 4 (12.1.0.2.4) de 64 bits para Windows x64</span><span class="sxs-lookup"><span data-stu-id="8af34-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="8af34-124">Se o cliente Oracle não estiver instalado, ocorrerá um erro ao tentar criar ou usar a conexão.</span><span class="sxs-lookup"><span data-stu-id="8af34-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="8af34-125">Consulte os erros comuns neste tópico.</span><span class="sxs-lookup"><span data-stu-id="8af34-125">See the common errors in this topic.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="8af34-126">Adicione o conector</span><span class="sxs-lookup"><span data-stu-id="8af34-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8af34-127">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="8af34-127">This connector does not have any triggers.</span></span> <span data-ttu-id="8af34-128">Ele tem somente ações.</span><span class="sxs-lookup"><span data-stu-id="8af34-128">It has only actions.</span></span> <span data-ttu-id="8af34-129">Então, quando você criar seu aplicativo lógico, adicione outro gatilho para iniciar seu aplicativo lógico, como **Agenda - Recorrência** ou **Solicitação / Resposta - Resposta**.</span><span class="sxs-lookup"><span data-stu-id="8af34-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="8af34-130">No [portal do Azure](https://portal.azure.com), crie um aplicativo lógico em branco.</span><span class="sxs-lookup"><span data-stu-id="8af34-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="8af34-131">No início de seu aplicativo lógico, selecione o gatilho **Solicitação / Resposta - Solicitação**:</span><span class="sxs-lookup"><span data-stu-id="8af34-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="8af34-132">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8af34-132">Select **Save**.</span></span> <span data-ttu-id="8af34-133">Quando você salva, a URL de uma solicitação é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8af34-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="8af34-134">Selecione **Nova etapa** e selecione **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="8af34-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="8af34-135">Digite `oracle` para ver as ações disponíveis:</span><span class="sxs-lookup"><span data-stu-id="8af34-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="8af34-136">Essa também é a maneira mais rápida de ver os gatilhos e ações disponíveis para qualquer conector.</span><span class="sxs-lookup"><span data-stu-id="8af34-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="8af34-137">Digite parte do nome do conector, como `oracle`.</span><span class="sxs-lookup"><span data-stu-id="8af34-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="8af34-138">O designer lista todos os gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="8af34-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="8af34-139">Selecione uma das ações, como **Banco de Dados Oracle - Obter linhas**.</span><span class="sxs-lookup"><span data-stu-id="8af34-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="8af34-140">Selecione **Conectar por meio do gateway de dados local**.</span><span class="sxs-lookup"><span data-stu-id="8af34-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="8af34-141">Insira o nome do servidor Oracle, o método de autenticação, o nome de usuário, a senha e selecione o gateway:</span><span class="sxs-lookup"><span data-stu-id="8af34-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="8af34-142">Após a conexão, selecione uma tabela na lista e insira a ID da linha à tabela.</span><span class="sxs-lookup"><span data-stu-id="8af34-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="8af34-143">Você precisa saber o identificador da tabela.</span><span class="sxs-lookup"><span data-stu-id="8af34-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="8af34-144">Se você não souber, contate o administrador do banco de dados Oracle e obtenha a saída de `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="8af34-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="8af34-145">Isso lhe dará as informações de identificação necessárias para continuar.</span><span class="sxs-lookup"><span data-stu-id="8af34-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="8af34-146">No exemplo a seguir, os dados do trabalho retornam de um banco de dados de Recursos Humanos:</span><span class="sxs-lookup"><span data-stu-id="8af34-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="8af34-147">Nesta próxima etapa, use qualquer um dos outros conectores para compilar seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8af34-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="8af34-148">Se você quiser testar a obtenção de dados do Oracle, envie um email com os dados do Oracle usando um dos conectores de envio de email, como o Office 365 ou o Gmail.</span><span class="sxs-lookup"><span data-stu-id="8af34-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="8af34-149">Use os tokens dinâmicos da tabela do Oracle para criar o `Subject` e o `Body` de seu email:</span><span class="sxs-lookup"><span data-stu-id="8af34-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="8af34-150">**Salve** seu aplicativo lógico e selecione **Executar**.</span><span class="sxs-lookup"><span data-stu-id="8af34-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="8af34-151">Feche o designer e examine o histórico de execuções do status.</span><span class="sxs-lookup"><span data-stu-id="8af34-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="8af34-152">Se ele falhar, selecione a linha da mensagem com falha.</span><span class="sxs-lookup"><span data-stu-id="8af34-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="8af34-153">O designer abre e mostra qual etapa falhou, e também mostra as informações do erro.</span><span class="sxs-lookup"><span data-stu-id="8af34-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="8af34-154">Se for bem-sucedido, você receberá um e-mail com as informações que adicionou.</span><span class="sxs-lookup"><span data-stu-id="8af34-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="8af34-155">Ideias de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="8af34-155">Workflow ideas</span></span>

* <span data-ttu-id="8af34-156">Você deseja monitorar a hashtag #oracle e colocar os tweets em um banco de dados para que possam ser consultados e usados em outros aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8af34-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="8af34-157">Em um aplicativo lógico, adicione o gatilho `Twitter - When a new tweet is posted` e insira a hashtag **#oracle**.</span><span class="sxs-lookup"><span data-stu-id="8af34-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="8af34-158">Em seguida, adicione a ação `Oracle Database - Insert row` e selecione sua tabela:</span><span class="sxs-lookup"><span data-stu-id="8af34-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="8af34-159">As mensagens são enviadas a uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="8af34-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="8af34-160">Obtenha essas mensagens e coloque-as em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8af34-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="8af34-161">Em um aplicativo lógico, adicione o gatilho `Service Bus - when a message is received in a queue` e selecione a fila.</span><span class="sxs-lookup"><span data-stu-id="8af34-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="8af34-162">Em seguida, adicione a ação `Oracle Database - Insert row` e selecione sua tabela:</span><span class="sxs-lookup"><span data-stu-id="8af34-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="8af34-163">Erros comuns</span><span class="sxs-lookup"><span data-stu-id="8af34-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="8af34-164">**Erro**: não é possível acessar o Gateway</span><span class="sxs-lookup"><span data-stu-id="8af34-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="8af34-165">**Causa**: o gateway de dados local não é capaz de se conectar à nuvem.</span><span class="sxs-lookup"><span data-stu-id="8af34-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="8af34-166">**Atenuação**: verifique se o gateway está em execução no computador local onde ele foi instalado e se ele pode se conectar à internet.</span><span class="sxs-lookup"><span data-stu-id="8af34-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="8af34-167">Recomendamos a não instalação do gateway em um computador que pode ser desativado ou suspenso.</span><span class="sxs-lookup"><span data-stu-id="8af34-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="8af34-168">Você também pode reiniciar o serviço de gateway de dados local (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="8af34-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="8af34-169">**Erro**: o provedor que está sendo usado é preterido: 'O System.Data.OracleClient exige o software cliente da Oracle versão 8.1.7 ou posterior.'.</span><span class="sxs-lookup"><span data-stu-id="8af34-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="8af34-170">Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) para instalar o provedor oficial.</span><span class="sxs-lookup"><span data-stu-id="8af34-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="8af34-171">**Causa**: o SDK do cliente da Oracle não está instalado no computador onde o gateway de dados local está em execução.</span><span class="sxs-lookup"><span data-stu-id="8af34-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="8af34-172">**Resolução**: baixe e instale o SDK do cliente da Oracle no mesmo computador que o gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="8af34-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="8af34-173">**Erro**: a tabela '[Nome_da_tabela]' não define colunas de chave</span><span class="sxs-lookup"><span data-stu-id="8af34-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="8af34-174">**Causa**: a tabela não tem uma chave primária.</span><span class="sxs-lookup"><span data-stu-id="8af34-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="8af34-175">**Resolução**: o conector do Banco de Dados Oracle exige o uso de uma tabela com uma coluna de chave primária.</span><span class="sxs-lookup"><span data-stu-id="8af34-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="8af34-176">Não há suporte no momento</span><span class="sxs-lookup"><span data-stu-id="8af34-176">Currently not supported</span></span>

* <span data-ttu-id="8af34-177">Exibições e procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="8af34-177">Views and stored procedures</span></span> 
* <span data-ttu-id="8af34-178">Qualquer tabela com chaves compostas</span><span class="sxs-lookup"><span data-stu-id="8af34-178">Any table with composite keys</span></span>
* <span data-ttu-id="8af34-179">Tipos de objeto aninhados em tabelas</span><span class="sxs-lookup"><span data-stu-id="8af34-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="8af34-180">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="8af34-180">Connector-specific details</span></span>

<span data-ttu-id="8af34-181">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="8af34-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="8af34-182">Obtenha ajuda</span><span class="sxs-lookup"><span data-stu-id="8af34-182">Get some help</span></span>

<span data-ttu-id="8af34-183">O [fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) é um ótimo lugar para fazer perguntas, responder a perguntas e saber o que os outros usuários dos Aplicativos Lógicos estão fazendo.</span><span class="sxs-lookup"><span data-stu-id="8af34-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="8af34-184">Você pode ajudar a melhorar os Aplicativos Lógicos e os conectores vitando e enviando suas ideias em [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="8af34-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8af34-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8af34-185">Next steps</span></span>
<span data-ttu-id="8af34-186">[Crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) e explore os conectores disponíveis nos Aplicativos Lógicos em nossa [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8af34-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore the available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
