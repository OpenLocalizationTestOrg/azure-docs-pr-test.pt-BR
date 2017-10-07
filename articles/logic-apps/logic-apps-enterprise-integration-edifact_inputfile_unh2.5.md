---
title: "aaaLogic aplicativos B2B edifact decodificar resolver UNH2.5 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Decodificação de edifact B2B dos Aplicativos Lógicos resolve UNH2.5"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a>Como toohandle EDIFACT documentos com UNH2.5 segmento
Quando UNH2.5 estiver presente no documento EDIFACT hello, ele está sendo usado para pesquisa de esquema. 

Exemplo: campo UNH Olá é **EAN008** na mensagem de saudação do EDIFACT  
UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'  

Mensagem de saudação do etapas toofollow toohandle 
1. Atualizar esquema da saudação
2. Verifique as configurações do contrato Olá  

## <a name="update-hello-schema"></a>Atualizar esquema da saudação
mensagem de saudação tooprocess, você precisa toodeploy um esquema com o nome do nó de raiz Olá UNH2.5.  Para um exemplo, o nome de raiz do esquema Olá seria **EFACT_D03B_ORDERS_EAN008**  

Para cada D03B_ORDERS com um segmento UNH2.5 diferente, você teria toodeploy um esquema individual.  

## <a name="add-schema-toohello-edifact-agreement"></a>Adicionar esquema toohello EDIFACT contrato
### <a name="edifact-decode"></a>Decodificação de EDIFACT
tooDecode Olá mensagem de entrada, configure o esquema de saudação em Olá EDIFACT configurações de recebimento do contrato
1. Adicionar conta de integração do hello esquema toohello    
2. Configurar o esquema de saudação em Olá EDIFACT configurações de recebimento do contrato. 
3. Selecione o contrato de EDIFACT e clique em **Editar como JSON**.  Adicione o valor UNH2.5 no contrato de recebimento de saudação **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)

### <a name="edifact-encode"></a>Codificação de EDIFACT
tooEncode Olá mensagem de entrada, configure o esquema de saudação em configurações de envio do acordo de EDIFACT Olá
1. Adicionar conta de integração do hello esquema toohello    
2. Configure o esquema de saudação em configurações de envio do acordo de EDIFACT hello. 
3. Selecione o contrato de EDIFACT e clique em **Editar como JSON**.  Adicione o valor UNH2.5 em Olá enviar contrato **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre os contratos da conta de integração](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  