---
title: "aaaCreate um aplicativo do Android em aplicativos de celular do serviço de aplicativo do Azure | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de back-ends dos aplicativos móveis do Azure para desenvolvimento do Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="ca9c8-103">Criar um aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="ca9c8-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ca9c8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ca9c8-104">Overview</span></span>
<span data-ttu-id="ca9c8-105">Este tutorial mostra como tooadd um back-end baseado em nuvem serviço aplicativo móvel do Android tooan usando um back-end do aplicativo móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9c8-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="ca9c8-106">Você criará um novo back-end do aplicativo móvel e um aplicativo Android simples com *Lista de tarefas pendentes* que armazena dados de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9c8-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="ca9c8-107">Concluir este tutorial é um pré-requisito para todos os outros tutoriais do Android sobre como usar o recurso de aplicativos móveis Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9c8-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca9c8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ca9c8-108">Prerequisites</span></span>
<span data-ttu-id="ca9c8-109">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca9c8-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ca9c8-110">[Ferramentas de desenvolvedor Android](https://developer.android.com/sdk/index.html), que inclui o ambiente de desenvolvimento integrado do Android Studio hello e plataforma Android mais recentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca9c8-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="ca9c8-111">SDK do Azure Mobile Android, que é referenciado automaticamente como parte do projeto de início rápido de saudação que você baixar.</span><span class="sxs-lookup"><span data-stu-id="ca9c8-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="ca9c8-112">Uma [conta ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca9c8-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="ca9c8-113">Criar um novo back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="ca9c8-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="ca9c8-114">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="ca9c8-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="ca9c8-115">Baixe e execute o aplicativo do Android Olá</span><span class="sxs-lookup"><span data-stu-id="ca9c8-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
