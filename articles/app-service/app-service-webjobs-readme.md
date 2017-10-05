---
title: "WebJobs no Serviço de Aplicativo do Azure"
description: "Saiba como criar trabalhos Web para executar testes em segundo plano, interagir com serviços como Armazenamento e Barramento de Serviço e criar tarefas agendadas."
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
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="f38e7-103">Usando WebJobs no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f38e7-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="f38e7-104">Este tópico fornece links para recursos de documentação sobre como usar o Azure WebJobs e o SDK do Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="f38e7-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="f38e7-105">Trabalhos Web do Azure fornece uma maneira fácil de executar scripts ou programas como processos em segundo plano em [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f38e7-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f38e7-106">Você pode carregar e executar um arquivo executável, como cmd, bat, exe (.NET), ps1, sh, php, py, js e jar.</span><span class="sxs-lookup"><span data-stu-id="f38e7-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="f38e7-107">Esses programas são executados como WebJobs em uma agenda (cron) ou continuamente.</span><span class="sxs-lookup"><span data-stu-id="f38e7-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="f38e7-108">O SDK de WebJobs torna mais fácil de usar o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f38e7-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="f38e7-109">O SDK de WebJobs tem uma um sistema de disparo e associação que funciona com o os blobs de armazenamento do Microsoft Azure, filas e tabelas, bem como filas do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="f38e7-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="f38e7-110">Criar, implantar e gerenciar WebJobs é fácil com ferramentas integradas no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f38e7-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="f38e7-111">Você pode criar WebJobs de modelos, publicar e gerenciá-los (executar/parar/monitor/depurar).</span><span class="sxs-lookup"><span data-stu-id="f38e7-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="f38e7-112">O painel de Trabalhos Web no portal de gerenciamento do Azure fornece recursos de gerenciamento poderosos que lhe dão controle total sobre a execução de Trabalhos Web, incluindo a capacidade de invocar funções individuais dentro de Trabalhos Web.</span><span class="sxs-lookup"><span data-stu-id="f38e7-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="f38e7-113">O painel também exibe a saída de log e tempos de execução de função.</span><span class="sxs-lookup"><span data-stu-id="f38e7-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

