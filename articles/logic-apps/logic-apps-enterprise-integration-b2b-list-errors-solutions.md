---
title: "Lista de erros e soluções de Aplicativos Lógicos B2B: Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Lista de erros e soluções de Aplicativos Lógicos B2B"
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
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Lista de erros e soluções de Aplicativos Lógicos B2B  
Este artigo ajuda você a solucionar problemas de erros que podem ocorrer em cenários de Aplicativos Lógicos B2B e sugere ações adequadas para corrigir esses erros.


## <a name="agreement-resolution"></a>Resolução do contrato

### <a name="no-agreement-found"></a>*Nenhum contrato encontrado 

|   |   |  
|---|---|
| Descrição do erro | Não foi encontrado nenhum contrato com os Parâmetros de Resolução de Contrato|    
| Ação do usuário | contrato Olá deve ser adicionado a conta de integração toohello com identidades comercial acordada.</br> identidades de negócios Olá devem corresponder toohello ids de mensagem de entrada|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* Não foi encontrado nenhum contrato com identidades

|   |   | 
|---|---|
| Descrição do erro | Não foi encontrado nenhum contrato com as identidades: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'| 
| Ação do usuário | AS2 inválido-de ou AS2-tooconfigured de acordo. </br> Mensagem de AS2 correta AS2-de ou cabeçalhos com configurações de contrato de mensagem AS2 tooheaders ou contrato de ids de toomatch AS2 no AS2 |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* Cabeçalhos de mensagem AS2 ausentes  

|   |   |  
|---|---|
| Descrição do erro| Cabeçalhos de AS2 inválidos. Um dos cabeçalhos “AS2-To” ou “AS2-From” está vazio| 
| Ação do usuário | Foi recebida uma mensagem AS2 que não continha Olá AS2-de ou AS2 tooor ambos os cabeçalhos. </br> Verifique a mensagem AS2 AS2-de e AS2-tooheaders e corrija-as com base na configuração do contrato |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* Cabeçalhos e corpo da mensagem AS2 ausentes    

|   |   |  
|---|---|
| Descrição do erro| conteúdo da solicitação Olá é nulo ou vazio | 
| Ação do usuário | Foi recebida uma mensagem AS2 que não contém o corpo da mensagem de saudação |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* Falha na descriptografia mensagem AS2

|   |   | 
|---|---|
| Descrição do erro |  [processado/Erro: falha na descriptografia] | 
| Ação do usuário | Adicionar @base64ToBinary tooAS2Message antes de enviar toopartner 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* Falha na descriptografia do MDN

|   |   | 
|---|---|
| Descrição do erro |  [processado/Erro: falha na descriptografia] | 
| Ação do usuário | Adicionar @base64ToBinary tooMDN antes de enviar toopartner 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* Certificado de assinatura ausente

|   |   |  
|---|---|
| Descrição do erro| Olá certificado de assinatura não foi configurado para parte do AS2. </br> AS2-From: partner1 AS2-To: partner2 | 
| Ação do usuário | Definir as configurações do contrato AS2 com o certificado correto para assinatura |
|  |  | 

## <a name="x12-and-edifact"></a>X12 e EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* Espaço à esquerda ou à direita encontrado    
    
|   |   | 
|---|---|
| Descrição do erro | Erro encontrado durante a análise. Olá Edifact transação com id ' 123456 'contida no intercâmbio (sem grupo) com a id ' 987654', com a id do remetente 'Parceiro1', id do destinatário 'Parceiro2' está sendo suspenso com os seguintes erros: separador levam à direita encontrado |
| Ação do usuário | Olá contrato configurações toobe configurado tooallow à esquerda e à direita de espaço. </br> Editar o contrato configurações tooallow à esquerda e à direita de espaço |
|   |   |

![permitir espaço](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Seleção duplicada habilitou no contrato de saudação

|   |   | 
|---|---| 
| Descrição do erro | Duplicar Número de Controle |
| Ação do usuário | Esse erro indica uma mensagem de saudação recebida tem números de controle duplicados. </br> Corrija o número de controle hello e reenviar a mensagem de saudação |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Esquema ausente no contrato de saudação

|   |   | 
|---|---| 
| Descrição do erro | Erro encontrado durante a análise. conjunto de transação Olá X12 com a id '564220001' contidos no grupo funcional com a id '56422', no intercâmbio com id '000056422' com a id de remetente 12345678 '', id do destinatário ' 87654321' está sendo suspenso com os seguintes erros "mensagem de saudação tem um tipo de documento desconhecido PE e não resolveu tooany de esquemas existentes de Olá configurados no contrato de hello " |
| Ação do usuário | Configurar o esquema nas configurações do contrato Olá  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Esquema incorreto no contrato de saudação

|   |   | 
|---|---| 
| Descrição do erro | mensagem de saudação tem um tipo de documento desconhecido e não resolveu tooany de esquemas existentes de Olá configurados no contrato de saudação. |
| Ação do usuário | Configurar o esquema correto nas configurações do contrato Olá  |
|   |   |

## <a name="flat-file"></a>Arquivo simples

### <a name="-input-message-with-no-body"></a>* Mensagem de entrada sem corpo

|   |   | 
|---|---|
| Descrição do erro | InvalidTemplate. Expressões de linguagem de modelo não é possível tooprocess em entradas de 'Flat_File_Decoding' ação na linha '1' e '1902' da coluna: ' necessária a propriedade 'content' espera um valor mas obteve nulo. Caminho “”.”. |
| Ação do usuário | Esse erro indica a mensagem de entrada hello não contém um corpo |
|   |   | 

## <a name="learn-more"></a>Saiba mais
[Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)
