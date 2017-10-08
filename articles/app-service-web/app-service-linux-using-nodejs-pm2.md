---
title: "configuração de aaaUsing PM2 para Node.js no aplicativo Web do Azure no Linux | Microsoft Docs"
description: "Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux"
keywords: "serviço de aplicativo do Azure, aplicativo web, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="28ea5-104">Usar a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="28ea5-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="28ea5-105">Se você definir Olá tooNode.js de pilha de aplicativo para o aplicativo Web do Azure no Linux, você obtém Olá opção tooset um arquivo de inicialização do Node. js conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="28ea5-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Definir um arquivo de inicialização do Node.js][1]

<span data-ttu-id="28ea5-107">Você pode usar este toodo opção um de saudação tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28ea5-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="28ea5-108">Especifique o script de inicialização de saudação para seu aplicativo Node. js (por exemplo: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="28ea5-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="28ea5-109">Especifique a saudação PM2 toouse de arquivo de configuração para seu aplicativo Node. js (por exemplo: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="28ea5-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="28ea5-110">Se você quiser automaticamente seu toorestart de processos do Node. js quando determinados arquivos são modificados, use a configuração de PM2 de hello.</span><span class="sxs-lookup"><span data-stu-id="28ea5-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="28ea5-111">Caso contrário, seu aplicativo não será reiniciado quando receber as notificações de alteração (por exemplo, quando o código do aplicativo for alterado).</span><span class="sxs-lookup"><span data-stu-id="28ea5-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="28ea5-112">Você pode verificar Olá Node. js [processar documentação arquivo](http://pm2.keymetrics.io/docs/usage/application-declaration/) para todas as opções de hello, mas a seguir está um exemplo de como o que você pode usar como o arquivo process.json:</span><span class="sxs-lookup"><span data-stu-id="28ea5-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="28ea5-113">Toonote coisas importantes nesta configuração são:</span><span class="sxs-lookup"><span data-stu-id="28ea5-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="28ea5-114">propriedade de "script" Hello Especifica o script de início do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28ea5-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="28ea5-115">propriedade de "ocorrências" Hello Especifica quantas instâncias de saudação toolaunch de processo de nó.</span><span class="sxs-lookup"><span data-stu-id="28ea5-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="28ea5-116">Se você estiver executando o aplicativo em máquinas virtuais maiores que têm vários núcleos, é uma boa ideia toomaximize seus recursos, definindo um valor mais alto aqui.</span><span class="sxs-lookup"><span data-stu-id="28ea5-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="28ea5-117">Olá "observar" matriz especifica todos os arquivos que você deseja toorestart processo de nó Olá para quando elas forem alteradas.</span><span class="sxs-lookup"><span data-stu-id="28ea5-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="28ea5-118">Para hello "watch_options", você precisa no momento toospecify "usePolling" como true devido à forma como o hello seu conteúdo de aplicativos está montado.</span><span class="sxs-lookup"><span data-stu-id="28ea5-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28ea5-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28ea5-119">Next steps</span></span>
* [<span data-ttu-id="28ea5-120">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="28ea5-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="28ea5-121">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="28ea5-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
