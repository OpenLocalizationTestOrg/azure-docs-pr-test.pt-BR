---
title: "Como migrar aplicativos lógicos para a versão de esquema 2015-08-01-preview | Microsoft Docs"
description: "Você pode facilmente migrar aplicativos lógicos para a última versão do esquema. Basta seguir estas etapas."
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
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="bb9d9-104">Como migrar aplicativos lógicos para a versão de esquema 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="bb9d9-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="bb9d9-105">Para mover aplicativos lógicos existentes para o novo esquema, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb9d9-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="bb9d9-106">Abra o aplicativo lógico no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bb9d9-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="bb9d9-107">Clique em Atualizar Esquema:</span><span class="sxs-lookup"><span data-stu-id="bb9d9-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="bb9d9-108">![Ícone de API][step1] </span><span class="sxs-lookup"><span data-stu-id="bb9d9-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="bb9d9-109">A página Atualizar Esquema exibe e fornece um link para um documento que fornece detalhes sobre os aperfeiçoamentos no novo esquema: ![Ícone de API][step2]</span><span class="sxs-lookup"><span data-stu-id="bb9d9-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="bb9d9-110">Quando você seleciona **Atualizar Esquema**, executamos automaticamente as etapas de migração e lhe fornecemos o código de saída.</span><span class="sxs-lookup"><span data-stu-id="bb9d9-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="bb9d9-111">Você pode usar isso para atualizar sua definição. No entanto, siga as práticas recomendadas de codificação, como as descritas na seção **Práticas recomendadas** abaixo.</span><span class="sxs-lookup"><span data-stu-id="bb9d9-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="bb9d9-112">Práticas recomendadas ao migrar aplicativos lógicos para a última versão do esquema:</span><span class="sxs-lookup"><span data-stu-id="bb9d9-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="bb9d9-113">Copie o script migrado para um novo aplicativo lógico - não substitua o antigo até concluir o teste e confirmar que o aplicativo migrado funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="bb9d9-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="bb9d9-114">Testar o aplicativo lógico **antes** de colocá-lo em produção</span><span class="sxs-lookup"><span data-stu-id="bb9d9-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="bb9d9-115">Após a conclusão da migração, comece a atualizar os Aplicativos Lógicos para usar as [APIs gerenciadas](apis-list.md) sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="bb9d9-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="bb9d9-116">Por exemplo, você pode começar a usar o Dropbox v2 em todos os casos em que usa o DropBox v1.</span><span class="sxs-lookup"><span data-stu-id="bb9d9-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="bb9d9-117">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="bb9d9-117">What's next</span></span>
* [<span data-ttu-id="bb9d9-118">Saiba como migrar manualmente os aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="bb9d9-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






