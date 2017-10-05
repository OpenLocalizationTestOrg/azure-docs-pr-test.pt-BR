---
title: "Criar um aplicativo de funções no Portal do Azure | Microsoft Docs"
description: "Crie um novo aplicativo de funções no Serviço de Aplicativo do Azure por meio do portal."
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
ms.openlocfilehash: 85a88c537415cd6f2b6bc005cc18e3baaa29e9a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-app-from-the-azure-portal"></a><span data-ttu-id="4e7d5-103">Criar um aplicativo de funções no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e7d5-103">Create a function app from the Azure portal</span></span>

<span data-ttu-id="4e7d5-104">Os Aplicativos do Azure Functions usam a infraestrutura do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-104">Azure Function Apps uses the Azure App Service infrastructure.</span></span> <span data-ttu-id="4e7d5-105">Este tópico mostra como criar um aplicativo de funções no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-105">This topic shows you how to create a function app in the Azure portal.</span></span> <span data-ttu-id="4e7d5-106">Um aplicativo de funções é o contêiner que hospeda a execução de funções individuais.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-106">A function app is the container that hosts the execution of individual functions.</span></span> <span data-ttu-id="4e7d5-107">Quando você cria um aplicativo de funções no plano de hospedagem do Serviço de Aplicativo, o aplicativo de funções pode usar todos os recursos do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-107">When you create a function app in the App Service hosting plan, your function app can use all the features of App Service.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="4e7d5-108">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="4e7d5-108">Create a function app</span></span>

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="4e7d5-109">Ao criar um aplicativo de funções, forneça um **Nome de aplicativo** válido, que pode conter apenas letras, números e hifens.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-109">When you create a function app, supply a valid **App name**, which can contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="4e7d5-110">Sublinhado (**_**) não é um caractere permitido.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-110">Underscore (**_**) is not an allowed character.</span></span>

<span data-ttu-id="4e7d5-111">Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-111">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="4e7d5-112">O nome da sua conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-112">Your storage account name must be unique within Azure.</span></span> 

<span data-ttu-id="4e7d5-113">Depois de criar o aplicativo de funções, é possível criar funções individuais em uma ou mais linguagens diferentes.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-113">After the function app is created, you can create individual functions in one or more different languages.</span></span> <span data-ttu-id="4e7d5-114">Crie funções [usando o portal](functions-create-first-azure-function.md#create-function), [a implantação contínua](functions-continuous-deployment.md) ou [carregando com FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span><span class="sxs-lookup"><span data-stu-id="4e7d5-114">Create functions [by using the portal](functions-create-first-azure-function.md#create-function), [continuous deployment](functions-continuous-deployment.md), or by [uploading with FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).</span></span>

## <a name="service-plans"></a><span data-ttu-id="4e7d5-115">Planos de serviço</span><span class="sxs-lookup"><span data-stu-id="4e7d5-115">Service plans</span></span>

<span data-ttu-id="4e7d5-116">O Azure Functions tem dois planos de serviço diferentes: o plano de Consumo e o plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-116">Azure Functions has two different service plans: Consumption plan and App Service plan.</span></span> <span data-ttu-id="4e7d5-117">O plano de Consumo automaticamente aloca potência de computação quando seu código está em execução, escala horizontalmente conforme a necessidade para tratar da carga e reduz horizontalmente quando o código não está em execução.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-117">The Consumption plan automatically allocates compute power when your code is running, scales-out as necessary to handle load, and then scales-in when code is not running.</span></span> <span data-ttu-id="4e7d5-118">O plano do Serviço de Aplicativo fornece ao aplicativo de funções o acesso a todos os recursos do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-118">The App Service plan gives your function app access to all the facilities of App Service.</span></span> <span data-ttu-id="4e7d5-119">É necessário escolher o plano de serviço quando o aplicativo de funções é criado, e ele não pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-119">You must choose your service plan when your function app is created, and it cannot currently be changed.</span></span> <span data-ttu-id="4e7d5-120">Para obter mais informações, consulte [Escolher um plano de hospedagem do Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4e7d5-120">For more information, see [Choose an Azure Functions hosting plan](functions-scale.md).</span></span>

<span data-ttu-id="4e7d5-121">Se você estiver planejando executar funções do JavaScript em um plano do Serviço de Aplicativo, deverá escolher um plano com menos núcleos.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-121">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan with fewer cores.</span></span> <span data-ttu-id="4e7d5-122">Para obter mais informações, consulte a [Referência do JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="4e7d5-122">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a><span data-ttu-id="4e7d5-123">Requisitos da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="4e7d5-123">Storage account requirements</span></span>

<span data-ttu-id="4e7d5-124">Ao criar um aplicativo de funções no Serviço de Aplicativo, é necessário criar ou se vincular a uma conta do Armazenamento do Azure de uso geral que dá suporte ao armazenamento de Blobs, Filas e Tabelas.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-124">When creating a function app in App Service, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage.</span></span> <span data-ttu-id="4e7d5-125">Internamente, o Functions usa o Armazenamento para operações como gerenciamento de gatilhos e log de execuções de função.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-125">Internally, Functions uses Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="4e7d5-126">Algumas contas de armazenamento não dão suporte a filas e tabelas, como contas de armazenamento somente blob, Armazenamento Premium do Azure e contas de armazenamento de uso geral com replicação ZRS.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-126">Some storage accounts do not support queues and tables, such as blob-only storage accounts, Azure Premium Storage, and general-purpose storage accounts with ZRS replication.</span></span> <span data-ttu-id="4e7d5-127">Essas contas são filtradas na folha Conta de Armazenamento durante a criação de um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-127">These accounts are filtered out of from the Storage Account blade when creating a function app.</span></span>

>[!NOTE]
><span data-ttu-id="4e7d5-128">Ao usar o plano de hospedagem de Consumo, o código da função e os arquivos de configuração da associação são armazenados no armazenamento de Arquivos do Azure na conta de armazenamento principal.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-128">When using the Consumption hosting plan, your function code and binding configuration files are stored in Azure File storage in the main storage account.</span></span> <span data-ttu-id="4e7d5-129">Ao excluir a conta de armazenamento principal, esse conteúdo será excluído e não poderá ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="4e7d5-129">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

<span data-ttu-id="4e7d5-130">Para saber mais sobre tipos de conta de armazenamento, confira [Introdução aos serviços de Armazenamento do Microsoft Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="4e7d5-130">To learn more about storage account types, see [Introducing the Azure Storage Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4e7d5-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e7d5-131">Next steps</span></span>

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



