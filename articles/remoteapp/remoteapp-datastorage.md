---
title: Nunca armazenar dados confidenciais em imagens personalizadas do Azure RemoteApp | Microsoft Docs
description: Saiba mais sobre as diretrizes para armazenar dados em imagens personalizadas no Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="c5f38-103">Nunca armazene dados confidenciais em imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="c5f38-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c5f38-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="c5f38-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c5f38-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c5f38-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c5f38-106">Ao hospedar seu aplicativo no Azure RemoteApp, a primeira etapa é criar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="c5f38-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="c5f38-107">Usamos essa imagem personalizada para criar instâncias de VM que fornecem seus aplicativos para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="c5f38-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="c5f38-108">A imagem personalizada deve conter APENAS aplicativos e nunca dados confidenciais que podem ser perdidos, como Bancos de Dados SQL, arquivos de pessoal ou arquivos de dados especiais, como arquivos da empresa do QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="c5f38-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="c5f38-109">Todos os dados confidenciais devem residir externamente ao Azure RemoteApp em um servidor de arquivos, outra VM do Azure ou no SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f38-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="c5f38-110">A imagem deve hospedar apenas o aplicativo que se conecta à fonte de dados e apresenta os dados.</span><span class="sxs-lookup"><span data-stu-id="c5f38-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="c5f38-111">Releia os [Requisitos para as imagens do Azure RemoteApp](remoteapp-imagereqs.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c5f38-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="c5f38-112">Para entender por que você não deve armazenar dados confidenciais, você precisa entender como o Azure RemoteApp funciona.</span><span class="sxs-lookup"><span data-stu-id="c5f38-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="c5f38-113">Quando uma coleção é criada ou atualizada, nos bastidores, são criados vários clones ou cópias da imagem.</span><span class="sxs-lookup"><span data-stu-id="c5f38-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="c5f38-114">Todas essas instâncias de VM são réplicas exatas da imagem personalizada. Quando os usuários iniciam os aplicativos eles são conectados a uma dessas instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="c5f38-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="c5f38-115">Mas a mesma instância não é garantida e não deve importar porque não é persistente.</span><span class="sxs-lookup"><span data-stu-id="c5f38-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="c5f38-116">As instâncias de VM hospedando os aplicativos são não persistentes e podem ser destruídas ou excluídas, por exemplo, durante a atualização da coleção.</span><span class="sxs-lookup"><span data-stu-id="c5f38-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="c5f38-117">Depois que a coleção é provisionada e os usuários começam a se conectar às VMs, os dados de usuário são persistentes e protegidos, pois eles são salvos no armazenamento separado dentro de um VHD que chamamos de um [UPD (disco de perfil de usuário)](remoteapp-upd.md), que é o perfil do usuário em c:\users\<userprofile>.</span><span class="sxs-lookup"><span data-stu-id="c5f38-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="c5f38-118">Quando um aplicativo é iniciado, o UPD é montado e tratado como um perfil do usuário local pelo sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="c5f38-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="c5f38-119">Leia mais sobre como o [Azure RemoteApp salva configurações e dados de usuário](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="c5f38-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="c5f38-120">Dados de exemplo que não devem residir na imagem:</span><span class="sxs-lookup"><span data-stu-id="c5f38-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="c5f38-121">Dados compartilhados para os usuários acessarem</span><span class="sxs-lookup"><span data-stu-id="c5f38-121">Shared data for users to access</span></span>
* <span data-ttu-id="c5f38-122">Banco de dados SQL ou banco de dados do QuickBooks</span><span class="sxs-lookup"><span data-stu-id="c5f38-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="c5f38-123">Quaisquer dados em D:\\</span><span class="sxs-lookup"><span data-stu-id="c5f38-123">Any data in D:\\</span></span>

<span data-ttu-id="c5f38-124">Dados de exemplo que podem residir no perfil padrão a ser copiado para o UPD de todos os usuários:</span><span class="sxs-lookup"><span data-stu-id="c5f38-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="c5f38-125">Arquivos de configuração por usuário</span><span class="sxs-lookup"><span data-stu-id="c5f38-125">Configuration files per user</span></span>
* <span data-ttu-id="c5f38-126">Scripts que os usuários precisariam que fossem preservados no seu UPD</span><span class="sxs-lookup"><span data-stu-id="c5f38-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="c5f38-127">Pontos principais:</span><span class="sxs-lookup"><span data-stu-id="c5f38-127">Key points:</span></span>

* <span data-ttu-id="c5f38-128">Nunca armazene dados confidenciais que possam ser perdidos na imagem ao criar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="c5f38-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="c5f38-129">Dados confidenciais sempre devem residir em um servidor de arquivos separado, VM do Azure separada, na nuvem e sempre externos às instâncias de VM que hospedam seus aplicativos no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c5f38-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="c5f38-130">Os dados de usuário são salvos e persistem no UPD (disco de perfil do usuário)</span><span class="sxs-lookup"><span data-stu-id="c5f38-130">User data is saved and persists in the user profile disk (UPD)</span></span>

