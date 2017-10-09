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
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Conecte-se tooan no sistema local da SAP de lógica de aplicativos com o conector do SAP Olá 

gateway de dados local Olá permite toomanage dados e acessar com segurança os recursos que estão no local. Este tópico mostra como você pode se conectar a lógica aplicativos tooan no sistema local da SAP. Neste exemplo, seu aplicativo lógico solicita um IDOC via HTTP e envia a resposta de saudação novamente.    

> [!NOTE]
> Limitações atuais: 
> - Seu aplicativo lógico expira se não concluir todas as etapas necessárias para a resposta de saudação dentro Olá [limite de solicitação](./logic-apps-limits-and-config.md). Nesse cenário, as solicitações podem ser bloqueadas. 
> - seletor de arquivo Hello não exibe todos os campos disponíveis de saudação. Nesse cenário, você pode adicionar os caminhos manualmente.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar e configurar hello mais recente [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127) versão 1.15.6150.1 ou mais recente. [Como tooconnect toohello no gateway de dados local em um aplicativo de lógica](http://aka.ms/logicapps-gateway) listas Olá etapas. gateway de saudação deve ser instalado em um computador local antes de prosseguir.

- Download e instalação hello mais recente SAP biblioteca de cliente em hello mesmo computador onde você instalou o gateway de dados hello. Use qualquer Olá versões da SAP a seguir: 
    - Servidor SAP
        - Qualquer servidor SAP que Olá suporte .NET conector (NCo) 3.0
 
    - Cliente SAP
        - Conector SAP do .NET (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Adicionar gatilhos e ações para conectar-se o sistema do SAP tooyour

conector do SAP Olá tem ações, mas não a gatilhos. Assim, temos toouse outro gatilho no início de saudação do fluxo de trabalho de saudação. 

1. Adicionar Olá gatilho de solicitação/resposta e, em seguida, selecione **nova etapa**.

2. Selecione **adicionar uma ação**e, em seguida, selecione o conector do SAP Olá digitando `SAP` no campo de pesquisa de saudação:    

     ![Selecionar Servidor de Aplicativos SAP ou Servidor de Mensagens SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. Selecione [**Servidor de Aplicativos SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) ou [**Servidor de Mensagens SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), de acordo com a configuração do SAP. Se você não tiver uma conexão existente, você é solicitado toocreate um.

   1. Selecione **conectar por meio do gateway de dados local**e insira os detalhes de saudação para seu sistema SAP:   

       ![Adicionar tooSAP de cadeia de caracteres de conexão](media/logic-apps-using-sap-connector/picture2.png)  

   2. Em **Gateway**, selecione um gateway existente ou tooinstall um novo gateway, selecione **instalar o Gateway**.

        ![Instalar um novo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Depois de inserir todos os detalhes de saudação, selecione **criar**. 
   Lógica de aplicativos configura e testa a conexão hello, certificando-se de que a conexão Olá funcione corretamente.

4. Insira um nome para a conexão SAP.

5. opções diferentes de SAP Olá agora estão disponíveis. toofind categoria IDOC, selecione na lista de saudação. Ou digite manualmente no caminho hello e resposta Olá selecione HTTP no hello **corpo** campo:

     ![Ação do SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Adicionar ação de saudação para criar um **resposta HTTP**. mensagem de resposta de saudação deve ser de saída do SAP hello.

7. Salve seu aplicativo lógico. Testá-lo, enviando um IDOC por meio da URL do gatilho Olá HTTP. Após Olá que IDOC é enviada, aguarde resposta de saudação do aplicativo lógico de saudação:   

     > [!TIP]
     > Check-out como muito[monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Agora que o conector do SAP Olá é adicionado tooyour lógica aplicativo, comece a explorar outras funcionalidades:

- BAPI
- RFC

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

- Saiba como toovalidate, transformar e outras funções BizTalk no hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Conecte-se a dados locais tooon](../logic-apps/logic-apps-gateway-connection.md) de aplicativos lógicos
