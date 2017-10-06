---
title: "aaaCreate um aplicativo Cordova em aplicativos de celular do serviço de aplicativo do Azure | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de back-ends dos aplicativos móveis do Azure para o desenvolvimento do Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova,javascript,móvel,cliente"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Criar um aplicativo Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como tooadd um back-end baseado em nuvem serviço aplicativo móvel do Apache Cordova tooan usando um back-end do aplicativo móvel do Azure.  Você criará um novo back-end do aplicativo móvel e um aplicativo Apache Cordova simples com *Lista de tarefas pendentes* que armazena dados de aplicativo no Azure.

Concluir este tutorial é um pré-requisito para todos os outros tutoriais do Apache Cordova sobre como usar o recurso de aplicativos móveis Olá no serviço de aplicativo do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* Um computador com o [Visual Studio Community 2017] ou mais recente.
* [Ferramentas do Visual Studio para Apache Cordova].
* Uma [conta ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).

Você também pode ignorar o Visual Studio e usar a linha de comando do Apache Cordova Olá diretamente.  Usando a linha de comando Olá é útil quando concluir Olá tutorial em um computador Mac.  Compilar aplicativos de cliente do Apache Cordova usando a linha de comando Olá não é coberto por este tutorial.

## <a name="create-an-azure-mobile-app-backend"></a>Criar um back-end de aplicativo móvel do Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Assista a um vídeo que mostra etapas semelhantes](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Configurar o projeto do servidor de saudação
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Baixe e execute o aplicativo do Apache Cordova Olá
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Próximas etapas
Agora que você concluiu este tutorial de início rápido, passar tooone de saudação tutoriais a seguir:

* [Adicionar dados Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.
* [Adicionar autenticação](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.
* [Adicionar notificações por Push](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.

Saiba mais sobre os principais conceitos com o Serviço de Aplicativo do Azure.

* [Dados Off-line]
* [Autenticação]
* [Notificações por Push]

Saiba como toouse Olá SDKs.

* [SDK do Apache Cordova]
* [SDK do Servidor ASP.NET]
* [SDK do Servidor Node.js]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Ferramentas do Visual Studio para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Dados Off-line]: app-service-mobile-offline-data-sync.md
[Autenticação]: app-service-mobile-auth.md
[Notificações por Push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
