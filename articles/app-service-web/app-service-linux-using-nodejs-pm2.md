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
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>Usar a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Se você definir Olá tooNode.js de pilha de aplicativo para o aplicativo Web do Azure no Linux, você obtém Olá opção tooset um arquivo de inicialização do Node. js conforme mostrado no Olá a imagem a seguir:

![Definir um arquivo de inicialização do Node.js][1]

Você pode usar este toodo opção um de saudação tarefas a seguir:

* Especifique o script de inicialização de saudação para seu aplicativo Node. js (por exemplo: /bin/server.js).
* Especifique a saudação PM2 toouse de arquivo de configuração para seu aplicativo Node. js (por exemplo: /foo/process.json).
  
  > [!NOTE]
  > Se você quiser automaticamente seu toorestart de processos do Node. js quando determinados arquivos são modificados, use a configuração de PM2 de hello. Caso contrário, seu aplicativo não será reiniciado quando receber as notificações de alteração (por exemplo, quando o código do aplicativo for alterado).
  > 
  > 

Você pode verificar Olá Node. js [processar documentação arquivo](http://pm2.keymetrics.io/docs/usage/application-declaration/) para todas as opções de hello, mas a seguir está um exemplo de como o que você pode usar como o arquivo process.json:

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

Toonote coisas importantes nesta configuração são:

* propriedade de "script" Hello Especifica o script de início do aplicativo.
* propriedade de "ocorrências" Hello Especifica quantas instâncias de saudação toolaunch de processo de nó. Se você estiver executando o aplicativo em máquinas virtuais maiores que têm vários núcleos, é uma boa ideia toomaximize seus recursos, definindo um valor mais alto aqui.
* Olá "observar" matriz especifica todos os arquivos que você deseja toorestart processo de nó Olá para quando elas forem alteradas.
* Para hello "watch_options", você precisa no momento toospecify "usePolling" como true devido à forma como o hello seu conteúdo de aplicativos está montado.

## <a name="next-steps"></a>Próximas etapas
* [O que é um Aplicativo Web do Azure no Linux?](app-service-linux-intro.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
