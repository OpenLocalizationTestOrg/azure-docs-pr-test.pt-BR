---
title: "comportamento de aaaOverride HTTP usando o mecanismo de regras do Azure CDN Olá | Microsoft Docs"
description: "mecanismo de regras de saudação permite toocustomize como solicitações HTTP são manipuladas pelo CDN do Azure, como bloqueio de entrega de saudação de certos tipos de conteúdo, defina uma política de cache e modificar os cabeçalhos HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Substituir o comportamento HTTP usando o mecanismo de regras do hello CDN do Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Visão geral
mecanismo de regras de saudação permite toocustomize como solicitações HTTP são tratadas como bloqueio de entrega de saudação de certos tipos de conteúdo, definindo uma política de cache e modificar os cabeçalhos HTTP.  Este tutorial demonstrará a criação de uma regra que irá alterar Olá comportamento de ativos CDN do cache.  Também há conteúdo de vídeo disponíveis no hello "[Consulte também](#see-also)" seção.

   > [!TIP] 
   > Para obter a sintaxe de toohello uma referência em detalhes, consulte [referência do mecanismo de regras](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Tutorial
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Clique em Olá **HTTP grande** guia, seguida por **mecanismo de regras**.
   
    São exibidas opções para uma nova regra.
   
    ![Novas opções de regra CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > ordem de saudação na qual várias regras são listadas afeta como elas são manipuladas. Uma regra subsequente pode substituir ações Olá especificadas por uma regra anterior.
   > 
   > 
3. Insira um nome no hello **nome / descrição** caixa de texto.
4. Identificar o tipo de saudação de solicitações Olá regra será aplicada.  Por padrão, Olá **sempre** condição de correspondência está selecionada.  Você usará **Sempre** para este tutorial; portanto, deixe essa opção marcada.
   
   ![Condição de correspondência CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Há muitos tipos de correspondência de condições disponíveis no menu suspenso de saudação.  Clicando em toohello de ícone informativo azul de saudação à esquerda da condição de correspondência Olá explicará condição Olá atualmente selecionado em detalhes.
   > 
   >  Para a lista completa de saudação de expressões condicionais em detalhes, consulte [expressões condicionais do mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Para Olá a lista completa das condições de correspondência em detalhes, consulte [corresponder a condições de mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Clique em Olá  **+**  botão Avançar muito**recursos** tooadd um novo recurso.  No menu suspenso de Olá Olá esquerda, selecione **Force interno Max-Age**.  Na saudação de texto que aparece, digite **300**.  Deixe Olá restantes valores padrão.
   
   ![Recurso CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Como com condições de correspondência, clicando em toohello de ícone informativo Olá azul à esquerda do hello novo recurso exibirá detalhes sobre esse recurso.  No caso de saudação de **Force interno Max-Age**, substituindo o ativo de saudação **Cache-Control** e **Expires** cabeçalhos toocontrol ao nó de extremidade CDN Olá atualizará Olá ativo de origem hello.  Nosso exemplo de 300 segundos significa que o nó de borda do hello CDN armazenará em cache ativo Olá para 5 minutos antes de atualizar um ativo de saudação de sua origem.
   > 
   > Para Olá a lista completa de recursos em detalhes, consulte [detalhes do recurso de mecanismo de regras](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Clique em Olá **adicionar** nova regra de botão toosave hello.  nova regra de saudação agora está aguardando aprovação. Depois que ele tiver sido aprovado, o status de saudação será alterado de **XML pendente** muito**XML Active**.
   
   > [!IMPORTANT]
   > Alterações de regras podem levar too90 minutos toopropagate por meio de saudação CDN.
   > 
   > 

## <a name="see-also"></a>Consulte também
* [Visão geral da CDN do Azure](cdn-overview.md)
* [Referência do Mecanismo de Regras](cdn-rules-engine-reference.md)
* [Condições de correspondência do Mecanismo de regras](cdn-rules-engine-reference-match-conditions.md)
* [Expressões condicionais do Mecanismo de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Recursos do Mecanismo de regras](cdn-rules-engine-reference-features.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
* [Azure Fridays: novos recursos Premium poderosos do Azure CDN](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vídeo)