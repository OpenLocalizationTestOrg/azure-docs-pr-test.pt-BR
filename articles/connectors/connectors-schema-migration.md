---
title: "aaaHow toomigrate lógica aplicativos tooschema versão 2015-08-01-preview | Microsoft Docs"
description: "Você pode facilmente migrar sua versão de esquema mais recente do lógica aplicativos toohello. Basta seguir estas etapas."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>Como toomigrate lógica aplicativos tooschema versão 2015-08-01-preview
toomove sua lógica aplicativos toohello novo esquema existente, Olá a seguir:  

1. Abra o aplicativo lógica no hello portal do Azure  
2. Clique em Atualizar Esquema:
   
   ![Ícone de API][step1]   
   página de atualização de esquema Olá exibe e fornece um link tooa documento que fornecem detalhes sobre as melhorias de saudação no novo esquema de saudação: ![ícone da API][step2]

> [!NOTE]
> Quando você seleciona **atualizar esquema**, automaticamente executar etapas de migração hello e fornecer saída de saudação de código para você. Você pode usar este tooupdate sua definição, no entanto, certifique-se de seguir boas práticas de codificação, como aqueles indicados no hello **práticas recomendadas** seção abaixo.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Práticas recomendadas ao migrar sua versão de esquema mais recente do lógica aplicativos toohello:
* Saudação de cópia migrados script tooa nova lógica de aplicativo - não substituir Olá antigo um até ter concluído seu aplicativo migrado de teste e confirmado hello funciona conforme o esperado.
* Testar o aplicativo lógico **antes** de colocá-lo em produção
* Após a conclusão da migração, iniciar a saudação de toouse aplicativos lógica [APIs gerenciadas](apis-list.md) sempre que possível. Por exemplo, você pode começar a usar o Dropbox v2 em todos os casos em que usa o DropBox v1.

## <a name="whats-next"></a>O que vem a seguir
* [Saiba como toomanually migrar seus aplicativos lógicos](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






