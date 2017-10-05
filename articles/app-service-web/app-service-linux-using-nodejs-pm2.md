---
title: "Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux | Microsoft Docs"
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
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="f351f-104">Usar a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="f351f-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="f351f-105">Se definir a pilha de aplicativos como o Node.js para o Aplicativo Web do Azure no Linux, você terá a opção de definir um arquivo de inicialização do Node.js, como mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="f351f-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Definir um arquivo de inicialização do Node.js][1]

<span data-ttu-id="f351f-107">Use esta opção para fazer uma das seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="f351f-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="f351f-108">Especificar o script de inicialização para seu aplicativo Node.js (por exemplo: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="f351f-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="f351f-109">Especificar o arquivo de configuração PM2 a ser usado para seu aplicativo Node.js (por exemplo: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="f351f-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f351f-110">Se você quiser que seus processos do Node.js sejam reiniciados automaticamente quando determinados arquivos forem modificados, use a configuração PM2.</span><span class="sxs-lookup"><span data-stu-id="f351f-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="f351f-111">Caso contrário, seu aplicativo não será reiniciado quando receber as notificações de alteração (por exemplo, quando o código do aplicativo for alterado).</span><span class="sxs-lookup"><span data-stu-id="f351f-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="f351f-112">Você pode verificar a [documentação do arquivo de processos](http://pm2.keymetrics.io/docs/usage/application-declaration/) do Node.js para todas as opções, mas veja a seguir um exemplo do que você pode usar como seu arquivo process.json:</span><span class="sxs-lookup"><span data-stu-id="f351f-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="f351f-113">Os aspectos importantes a observar nessa configuração são:</span><span class="sxs-lookup"><span data-stu-id="f351f-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="f351f-114">A propriedade "script" especifica o script de inicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f351f-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="f351f-115">A propriedade "instances" especifica quantas instâncias do processo de nó serão iniciadas.</span><span class="sxs-lookup"><span data-stu-id="f351f-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="f351f-116">Se você estiver executando seu aplicativo em VMs maiores com vários núcleos, é uma boa ideia para maximizar seus recursos definir um valor mais alto aqui.</span><span class="sxs-lookup"><span data-stu-id="f351f-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="f351f-117">A matriz "watch" especifica todos os arquivos para os quais você deseja reiniciar o processo de nó quando eles forem alterados.</span><span class="sxs-lookup"><span data-stu-id="f351f-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="f351f-118">No momento, para "watch_options", é necessário especificar "usePolling" como true devido ao modo como o conteúdo do aplicativo é montado.</span><span class="sxs-lookup"><span data-stu-id="f351f-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f351f-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f351f-119">Next steps</span></span>
* [<span data-ttu-id="f351f-120">O que é um Aplicativo Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="f351f-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="f351f-121">Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="f351f-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
