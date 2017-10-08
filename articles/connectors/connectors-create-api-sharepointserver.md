---
title: "Olá aaaUse do SharePoint Server Connector em seus aplicativos lógicos | Microsoft Docs"
description: "Começar a usar Olá Olá do SharePoint Server Connector em seus aplicativos lógicos"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Introdução ao conector do SharePoint Olá
Olá conector do SharePoint fornece um toowork de maneira com listas no SharePoint.

Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Criar uma conexão tooSharePoint
toouse Olá conector do SharePoint, você primeiro crie um **conexão** Forneça detalhes de saudação para essas propriedades: 

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| A criptografia do token |Sim |Fornecer credenciais do SharePoint |

tooconnect muito**SharePoint**, digite tooSharePoint sua identidade (nome de usuário e senha, as credenciais de cartão inteligente, etc.). Depois que você tenha sido autenticado, você poderá continuar conector do toouse saudação do SharePoint em seu aplicativo de lógica. 

Enquanto no designer de saudação do seu aplicativo lógico, siga toosign essas etapas na conexão de saudação do SharePoint toocreate **conexão** para uso em seu aplicativo lógico:

1. Insira do SharePoint na caixa de pesquisa hello e aguarde Olá pesquisa tooreturn todas as entradas com o SharePoint em nome de saudação:   
   ![Configurar o SharePoint][1]  
2. Selecione **SharePoint – Quando um arquivo é criado**   
3. Selecione **entrar tooSharePoint**:   
   ![Configurar o SharePoint][2]    
4. Forneça seu toosign de credenciais do SharePoint no tooauthenticate com o SharePoint   
   ![Configurar o SharePoint][3]     
5. Após a conclusão da autenticação Olá você será redirecionado tooyour lógica aplicativo toocomplete-lo por meio da configuração do SharePoint **quando um arquivo é criado** caixa de diálogo.          
   ![Configurar o SharePoint][4]  
6. Em seguida, você pode adicionar outros gatilhos e ações que você precisa toocomplete seu aplicativo lógico.   
7. Salve seu trabalho selecionando **salvar** na barra de menus do hello acima.  

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sharepoint/).

## <a name="more-connectors"></a>Mais conectores
Voltar toohello [lista APIs](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
