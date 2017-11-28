---
title: "Visão geral de tempo de execução de funções de aaaAzure | Microsoft Docs"
description: "Visão geral da saudação visualização de tempo de execução de funções do Azure"
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
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="66940-103">Visão geral do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="66940-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="66940-104">saudação de tempo de execução de funções do Azure fornece uma nova maneira você tootake vantagem de manter a simplicidade hello e flexibilidade de funções do Azure Olá local do modelo de programação.</span><span class="sxs-lookup"><span data-stu-id="66940-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="66940-105">Mesmo baseia Olá abra raízes de origem como funções do Azure, o tempo de execução de funções do Azure é implantado no local tooprovide um desenvolvimento quase idêntico experiência como serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="66940-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Portal de visualização do Azure Functions Runtime][1]

<span data-ttu-id="66940-107">saudação de tempo de execução de funções do Azure fornece uma maneira para você tooexperience Azure funções antes de confirmar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="66940-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="66940-108">Dessa forma, ativos de código Olá que compilar podem, em seguida, ser executados com você toohello nuvem quando você migrar.</span><span class="sxs-lookup"><span data-stu-id="66940-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="66940-109">saudação de tempo de execução também abre novas opções para você, como o uso de capacidade de computação de reposição de saudação dos processos de lote local computadores toorun durante a noite.</span><span class="sxs-lookup"><span data-stu-id="66940-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="66940-110">Você também pode usar dispositivos em sua organização tooconditionally enviar tooother sistemas de dados locais e na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="66940-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="66940-111">saudação de tempo de execução de funções do Azure consiste em duas partes:</span><span class="sxs-lookup"><span data-stu-id="66940-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="66940-112">Função de Gerenciamento do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="66940-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="66940-113">Função de Trabalho do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="66940-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="66940-114">Função de Gerenciamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="66940-114">Azure Functions Management Role</span></span>

<span data-ttu-id="66940-115">Olá função de gerenciamento de funções do Azure fornece um host para o gerenciamento de saudação de sua funções no local.</span><span class="sxs-lookup"><span data-stu-id="66940-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="66940-116">Esta função executa Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="66940-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="66940-117">Hospedagem de saudação funções Portal de gerenciamento, que é Olá Olá mesmo que você vê no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66940-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="66940-118">Isso permite que você desenvolver suas funções no mesmo Olá maneira como você faria no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="66940-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="66940-119">Distribuição de funções por vários trabalhadores do Functions.</span><span class="sxs-lookup"><span data-stu-id="66940-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="66940-120">Fornecimento de um ponto de extremidade de publicação, para que você possa publicar suas funções diretamente do Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66940-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="66940-121">Função de Trabalho do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="66940-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="66940-122">Funções de trabalho Hello Azure funções são implantadas nos contêineres do Windows e é onde o código de função é executado.</span><span class="sxs-lookup"><span data-stu-id="66940-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="66940-123">Você pode implantar várias Funções de Trabalho em toda sua organização, e essa é uma maneira importante com a qual os clientes podem usar o poder da computação sobressalente.</span><span class="sxs-lookup"><span data-stu-id="66940-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="66940-124">Requisitos mínimos</span><span class="sxs-lookup"><span data-stu-id="66940-124">Minimum Requirements</span></span>

<span data-ttu-id="66940-125">tooget iniciado com hello tempo de execução de funções do Azure deve ter um computador com **Windows Server 2016 ou Windows 10 criadores Update** com acesso tooa **do SQL Server** instância.</span><span class="sxs-lookup"><span data-stu-id="66940-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66940-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66940-126">Next Steps</span></span>

<span data-ttu-id="66940-127">Instalar Olá [visualização de tempo de execução de funções do Azure](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="66940-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
