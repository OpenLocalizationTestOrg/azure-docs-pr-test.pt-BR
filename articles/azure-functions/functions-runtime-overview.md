---
title: "Visão geral do Azure Functions Runtime | Microsoft Docs"
description: "Visão geral da visualização do Azure Functions Runtime"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="0a410-103">Visão geral do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="0a410-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="0a410-104">O Azure Functions Runtime fornece a você uma nova maneira para aproveitar a simplicidade e a flexibilidade do modelo de programação do Azure Functions local.</span><span class="sxs-lookup"><span data-stu-id="0a410-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="0a410-105">Compilado sobre as mesmas raízes de código-fonte aberto que o Azure Functions, o Azure Functions Runtime é implantado localmente a fim de fornecer uma experiência de desenvolvimento quase idêntica ao serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0a410-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Portal de visualização do Azure Functions Runtime][1]

<span data-ttu-id="0a410-107">O Azure Functions Runtime permite que você experimente o Azure Functions antes de se comprometer com a nuvem.</span><span class="sxs-lookup"><span data-stu-id="0a410-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="0a410-108">Dessa forma, você levar seus ativos de código compilados para a nuvem quando decidir migrar.</span><span class="sxs-lookup"><span data-stu-id="0a410-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="0a410-109">O runtime também disponibiliza novas opções, como o uso do poder de computação sobressalente de seus computadores locais para executar processos em lote durante a noite.</span><span class="sxs-lookup"><span data-stu-id="0a410-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="0a410-110">Você também pode usar os dispositivos de sua organização para enviar condicionalmente dados a outros sistemas, locais e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="0a410-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="0a410-111">O Azure Functions Runtime é formado por duas partes:</span><span class="sxs-lookup"><span data-stu-id="0a410-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="0a410-112">Função de Gerenciamento do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="0a410-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="0a410-113">Função de Trabalho do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="0a410-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="0a410-114">Função de Gerenciamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0a410-114">Azure Functions Management Role</span></span>

<span data-ttu-id="0a410-115">A função de gerenciamento do Azure Functions fornece um host para gerenciar o Functions localmente.</span><span class="sxs-lookup"><span data-stu-id="0a410-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="0a410-116">Essa função executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="0a410-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="0a410-117">Hospedagem do Portal de Gerenciamento do Azure Functions, que é o mesmo do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a410-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0a410-118">Isso permite que você desenvolva suas funções da mesma maneira que faria no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a410-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="0a410-119">Distribuição de funções por vários trabalhadores do Functions.</span><span class="sxs-lookup"><span data-stu-id="0a410-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="0a410-120">Fornecimento de um ponto de extremidade de publicação, para que você possa publicar suas funções diretamente do Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a410-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="0a410-121">Função de Trabalho do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0a410-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="0a410-122">As Funções de Trabalho do Azure Functions são implantadas em Contêineres do Windows, e é nesse local que o código da função é executado.</span><span class="sxs-lookup"><span data-stu-id="0a410-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="0a410-123">Você pode implantar várias Funções de Trabalho em toda sua organização, e essa é uma maneira importante com a qual os clientes podem usar o poder da computação sobressalente.</span><span class="sxs-lookup"><span data-stu-id="0a410-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="0a410-124">Requisitos mínimos</span><span class="sxs-lookup"><span data-stu-id="0a410-124">Minimum Requirements</span></span>

<span data-ttu-id="0a410-125">Para começar com o Azure Functions Runtime, você deve ter um computador com **Windows Server 2016 ou com a Atualização do Windows 10 para Criadores** com acesso a uma instância do **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0a410-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a410-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a410-126">Next Steps</span></span>

<span data-ttu-id="0a410-127">Instalar a [visualização do Azure Functions Runtime](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="0a410-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
