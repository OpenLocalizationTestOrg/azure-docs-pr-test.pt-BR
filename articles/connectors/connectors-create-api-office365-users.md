---
title: "Adicionar o conector Usuários do Office 365 aos Aplicativos Lógicos | Microsoft Docs"
description: "Visão geral do conector dos Usuários do Office 365 com os parâmetros da API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="3fe06-103">Introdução ao conector dos Usuários do Office 365</span><span class="sxs-lookup"><span data-stu-id="3fe06-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="3fe06-104">Conecte-se aos Usuários do Office 365 para obter perfis, pesquisar usuários e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3fe06-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="3fe06-105">Com os Usuários do Office 365, você pode:</span><span class="sxs-lookup"><span data-stu-id="3fe06-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="3fe06-106">Criar seu fluxo de negócios baseado nos dados obtidos dos Usuários do Office 365.</span><span class="sxs-lookup"><span data-stu-id="3fe06-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="3fe06-107">Usar ações que obtêm relatórios diretos, o perfil de usuário de um gerenciador e muito mais.</span><span class="sxs-lookup"><span data-stu-id="3fe06-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="3fe06-108">Essas ações obtêm uma resposta e disponibilizam a saída para outras ações.</span><span class="sxs-lookup"><span data-stu-id="3fe06-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="3fe06-109">Por exemplo, obtenha relatórios diretos de uma pessoa e, em seguida, utilize essas informações e atualize um banco de dados SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3fe06-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="3fe06-110">É possível começar criando um aplicativo lógico agora. Consulte [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3fe06-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="3fe06-111">Criar uma conexão com os Usuários do Office 365</span><span class="sxs-lookup"><span data-stu-id="3fe06-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="3fe06-112">Ao adicionar esse conector aos seus aplicativos lógicos, é necessário entrar em sua conta dos Usuários do Office 365 e permitir que os aplicativos lógicos se conectem à sua conta.</span><span class="sxs-lookup"><span data-stu-id="3fe06-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="3fe06-113">Depois de criar a conexão, insira as propriedades dos Usuários do Office 365, como a ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="3fe06-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="3fe06-114">A **Referência da API REST** neste tópico descreve essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="3fe06-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3fe06-115">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="3fe06-115">Connector-specific details</span></span>

<span data-ttu-id="3fe06-116">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="3fe06-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3fe06-117">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="3fe06-117">More connectors</span></span>
<span data-ttu-id="3fe06-118">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3fe06-118">Go back to the [APIs list](apis-list.md).</span></span>