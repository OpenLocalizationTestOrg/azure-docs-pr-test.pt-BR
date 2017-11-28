---
title: "aaaWebJobs no serviço de aplicativo do Azure"
description: "Saiba como toobuild o plano de fundo do WebJobs toorun testes, interagir com os serviços como o armazenamento e o barramento de serviço e criar tarefas agendadas."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="d6eac-103">Usando WebJobs no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="d6eac-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="d6eac-104">Este artigo contém links toodocumentation recursos sobre como toouse WebJobs do Azure e Olá SDK do Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="d6eac-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="d6eac-105">WebJobs do Azure fornecem um scripts toorun de maneira fácil ou processos em segundo plano programas como em [aplicativos de Web do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d6eac-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="d6eac-106">Você pode carregar e executar um arquivo executável, como cmd, bat, exe (.NET), ps1, sh, php, py, js e jar.</span><span class="sxs-lookup"><span data-stu-id="d6eac-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="d6eac-107">Esses programas são executados como WebJobs em uma agenda (cron) ou continuamente.</span><span class="sxs-lookup"><span data-stu-id="d6eac-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="d6eac-108">Olá SDK do WebJobs torna mais fácil toouse o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6eac-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="d6eac-109">Olá SDK do WebJobs tem uma associação e o sistema de gatilho que funciona com o armazenamento de Blobs do Microsoft Azure, filas e tabelas e filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="d6eac-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="d6eac-110">Criar, implantar e gerenciar WebJobs é fácil com ferramentas integradas no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6eac-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="d6eac-111">Você pode criar WebJobs de modelos, publicar e gerenciá-los (executar/parar/monitor/depurar).</span><span class="sxs-lookup"><span data-stu-id="d6eac-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="d6eac-112">painel do WebJobs Olá no hello portal do Azure fornece recursos de gerenciamento avançado que lhe dá controle total sobre a execução de saudação do WebJobs, incluindo Olá capacidade tooinvoke funções individuais em trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="d6eac-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="d6eac-113">painel Olá também exibe a saída de log e tempos de execução de função.</span><span class="sxs-lookup"><span data-stu-id="d6eac-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

