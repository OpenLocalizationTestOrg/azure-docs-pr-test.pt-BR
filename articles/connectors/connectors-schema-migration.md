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
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="99532-104">Como toomigrate lógica aplicativos tooschema versão 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="99532-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="99532-105">toomove sua lógica aplicativos toohello novo esquema existente, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="99532-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="99532-106">Abra o aplicativo lógica no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="99532-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="99532-107">Clique em Atualizar Esquema:</span><span class="sxs-lookup"><span data-stu-id="99532-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="99532-108">![Ícone de API][step1] </span><span class="sxs-lookup"><span data-stu-id="99532-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="99532-109">página de atualização de esquema Olá exibe e fornece um link tooa documento que fornecem detalhes sobre as melhorias de saudação no novo esquema de saudação: ![ícone da API][step2]</span><span class="sxs-lookup"><span data-stu-id="99532-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="99532-110">Quando você seleciona **atualizar esquema**, automaticamente executar etapas de migração hello e fornecer saída de saudação de código para você.</span><span class="sxs-lookup"><span data-stu-id="99532-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="99532-111">Você pode usar este tooupdate sua definição, no entanto, certifique-se de seguir boas práticas de codificação, como aqueles indicados no hello **práticas recomendadas** seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="99532-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="99532-112">Práticas recomendadas ao migrar sua versão de esquema mais recente do lógica aplicativos toohello:</span><span class="sxs-lookup"><span data-stu-id="99532-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="99532-113">Saudação de cópia migrados script tooa nova lógica de aplicativo - não substituir Olá antigo um até ter concluído seu aplicativo migrado de teste e confirmado hello funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="99532-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="99532-114">Testar o aplicativo lógico **antes** de colocá-lo em produção</span><span class="sxs-lookup"><span data-stu-id="99532-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="99532-115">Após a conclusão da migração, iniciar a saudação de toouse aplicativos lógica [APIs gerenciadas](apis-list.md) sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="99532-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="99532-116">Por exemplo, você pode começar a usar o Dropbox v2 em todos os casos em que usa o DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="99532-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="99532-117">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="99532-117">What's next</span></span>
* [<span data-ttu-id="99532-118">Saiba como toomanually migrar seus aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="99532-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






