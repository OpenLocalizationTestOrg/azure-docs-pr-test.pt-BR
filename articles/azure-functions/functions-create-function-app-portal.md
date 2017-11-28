---
title: "aaaCreate um aplicativo de função da saudação Portal do Azure | Microsoft Docs"
description: "Crie um novo aplicativo de função no serviço de aplicativo do Azure do portal de saudação."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a><span data-ttu-id="eaaec-103">Criar um aplicativo de função do hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eaaec-103">Create a function app from hello Azure portal</span></span>

<span data-ttu-id="eaaec-104">Aplicativos de função do Azure usa a infra-estrutura de serviço de aplicativo do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eaaec-104">Azure Function Apps uses hello Azure App Service infrastructure.</span></span> <span data-ttu-id="eaaec-105">Este tópico mostra como um aplicativo de função no portal do Azure de saudação do toocreate.</span><span class="sxs-lookup"><span data-stu-id="eaaec-105">This topic shows you how toocreate a function app in hello Azure portal.</span></span> <span data-ttu-id="eaaec-106">Um função de aplicativo é o contêiner de saudação que hospeda a execução de saudação de funções individuais.</span><span class="sxs-lookup"><span data-stu-id="eaaec-106">A function app is hello container that hosts hello execution of individual functions.</span></span> <span data-ttu-id="eaaec-107">Quando você cria um aplicativo de função no hello plano de hospedagem de serviço de aplicativo, seu aplicativo de função pode usar todos os recursos de saudação do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaaec-107">When you create a function app in hello App Service hosting plan, your function app can use all hello features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="eaaec-108">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="eaaec-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="eaaec-109">Ao criar um aplicativo de funções, forneça um **Nome de aplicativo** válido, que pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="eaaec-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="eaaec-110">Sublinhado (**_**) não é um caractere permitido.</span><span class="sxs-lookup"><span data-stu-id="eaaec-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="eaaec-111">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="eaaec-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="eaaec-112">O nome da sua conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="eaaec-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="eaaec-113">Depois de aplicativo de função hello for criado, você pode criar funções individuais em um ou mais idiomas diferentes.</span><span class="sxs-lookup"><span data-stu-id="eaaec-113">After hello function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="eaaec-114">Criar funções [usando o portal de saudação](functions-create-first-azure-function.md#create-function), [implantação contínua](functions-continuous-deployment.md), ou [Carregando com FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="eaaec-114">Create functions [by using hello portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="eaaec-115">Planos de serviço</span><span class="sxs-lookup"><span data-stu-id="eaaec-115">Service plans</span></span>

<span data-ttu-id="eaaec-116">O Azure Functions tem dois planos de serviço diferentes: o plano de Consumo e o plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaaec-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="eaaec-117">plano de consumo Olá aloca automaticamente a capacidade de computação quando seu código é executado, escalas-out como carga de toohandle necessário e escalas-in quando o código não está em execução.</span><span class="sxs-lookup"><span data-stu-id="eaaec-117">hello Consumption plan automatically allocates compute power when your code is running, scales-out as necessary toohandle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="eaaec-118">Olá plano de serviço de aplicativo fornece sua função de instalações de saudação de tooall de acesso de aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaaec-118">hello App Service plan gives your function app access tooall hello facilities of App Service.</span></span> <span data-ttu-id="eaaec-119">É necessário escolher o plano de serviço quando o aplicativo de funções é criado, e ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="eaaec-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="eaaec-120">Para obter mais informações, consulte [Escolher um plano de hospedagem do Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="eaaec-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="eaaec-121">Se você estiver planejando toorun funções de JavaScript em um plano de serviço de aplicativo, você deve escolher um plano com menos núcleos.</span><span class="sxs-lookup"><span data-stu-id="eaaec-121">If you are planning toorun JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="eaaec-122">Para obter mais informações, consulte Olá [referência de JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="eaaec-122">For more information, see hello [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="eaaec-123">Requisitos da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="eaaec-123">Storage account requirements</span></span>

<span data-ttu-id="eaaec-124">Ao criar um aplicativo de função no serviço de aplicativo, você deve criar ou vincular tooa uso geral do Azure conta de armazenamento que dá suporte ao armazenamento de Blob, fila e tabela.</span><span class="sxs-lookup"><span data-stu-id="eaaec-124">When creating a function app in App Service, you must create or link tooa general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="eaaec-125">Internamente, o Functions usa o Armazenamento para operações como gerenciamento de gatilhos e log de execuções de função.</span><span class="sxs-lookup"><span data-stu-id="eaaec-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="eaaec-126">Algumas contas de armazenamento não dão suporte a filas e tabelas, como contas de armazenamento somente blob, Armazenamento Premium do Azure e contas de armazenamento de uso geral com replicação ZRS.</span><span class="sxs-lookup"><span data-stu-id="eaaec-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="eaaec-127">Essas contas são filtradas fora da folha de conta de armazenamento Olá durante a criação de um aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="eaaec-127">These accounts are filtered out of from hello Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="eaaec-128">Ao usar o plano de hospedagem de consumo hello, seus arquivos de configuração de código e associação de função são armazenados no armazenamento de arquivo do Azure na conta de armazenamento principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="eaaec-128">When using hello Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in hello main storage account.</span></span> <span data-ttu-id="eaaec-129">Quando você exclui a conta de armazenamento principal hello, esse conteúdo será excluído e não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="eaaec-129">When you delete hello main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="eaaec-130">toolearn mais sobre os tipos de conta de armazenamento, consulte [apresentando os serviços de armazenamento do Azure Olá](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="eaaec-130">toolearn more about storage account types, see [Introducing hello Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eaaec-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eaaec-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



