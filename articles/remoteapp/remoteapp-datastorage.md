---
title: aaaNever armazenar dados confidenciais em imagens personalizadas para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as diretrizes de saudação para armazenar dados em imagens personalizadas no Azure RemoteApp"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="84019-103">Nunca armazene dados confidenciais em imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="84019-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="84019-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="84019-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="84019-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="84019-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="84019-106">Ao hospedar seu próprio aplicativo no Azure RemoteApp, Olá primeira etapa é toocreate uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="84019-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="84019-107">Usamos que instâncias VM toocreate imagem personalizada que servem tooyour usuários de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="84019-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="84019-108">imagem personalizada Olá deve conter apenas aplicativos e dados nunca confidenciais que podem ser perdidos, como bancos de dados SQL, arquivos de pessoal ou arquivos de dados especiais como QuickBooks da empresa.</span><span class="sxs-lookup"><span data-stu-id="84019-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="84019-109">Todos os dados confidenciais devem residir tooAzure externo RemoteApp em um servidor de arquivos, outra VM do Azure, ou no SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84019-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="84019-110">imagem de saudação deve apenas aplicativo de saudação host que conecta-se a fonte de dados toohello e apresenta os dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="84019-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="84019-111">Releia os [Requisitos para as imagens do Azure RemoteApp](remoteapp-imagereqs.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="84019-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="84019-112">toounderstand por que você não deve armazenar dados confidenciais, você precisa toounderstand como funciona o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="84019-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="84019-113">Quando uma coleção é criada ou atualizada, em segundo plano do hello vários clones ou cópias de imagem de saudação são criadas.</span><span class="sxs-lookup"><span data-stu-id="84019-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="84019-114">Todas essas instâncias VM são réplicas exatas de imagem personalizada do hello; Quando os usuários iniciar aplicativos estiverem conectado tooone dessas instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="84019-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="84019-115">Mas hello mesma instância não é garantida e não deve importar porque eles são não persistente.</span><span class="sxs-lookup"><span data-stu-id="84019-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="84019-116">Olá instâncias VM aplicativos de hospedagem Olá não são persistentes e podem ser destruído ou excluído com base, por exemplo, durante a atualização da coleção.</span><span class="sxs-lookup"><span data-stu-id="84019-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="84019-117">Depois de coleção Olá é provisionada e os usuários iniciam o toohello conectar máquinas virtuais, dados de usuário são persistentes e protegido porque ele é salvo em um armazenamento separado dentro de um VHD que chamamos um [disco de perfil de usuário (UDP)](remoteapp-upd.md), que é o perfil de usuário Olá c:\Users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="84019-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="84019-118">Quando um aplicativo é iniciado, Olá UPD é montado e tratada como um perfil de usuário local pelo sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="84019-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="84019-119">Leia mais sobre como o [Azure RemoteApp salva configurações e dados de usuário](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="84019-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="84019-120">Dados de exemplo não devem residir na imagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="84019-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="84019-121">Dados compartilhados para usuários tooaccess</span><span class="sxs-lookup"><span data-stu-id="84019-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="84019-122">Banco de dados SQL ou banco de dados do QuickBooks</span><span class="sxs-lookup"><span data-stu-id="84019-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="84019-123">Quaisquer dados em D:\\</span><span class="sxs-lookup"><span data-stu-id="84019-123">Any data in D:\\</span></span>

<span data-ttu-id="84019-124">Dados de exemplo que podem residir em saudação padrão perfil toobe copiado para UPD cada usuários:</span><span class="sxs-lookup"><span data-stu-id="84019-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="84019-125">Arquivos de configuração por usuário</span><span class="sxs-lookup"><span data-stu-id="84019-125">Configuration files per user</span></span>
* <span data-ttu-id="84019-126">Scripts que os usuários precisariam que fossem preservados no seu UPD</span><span class="sxs-lookup"><span data-stu-id="84019-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="84019-127">Pontos principais:</span><span class="sxs-lookup"><span data-stu-id="84019-127">Key points:</span></span>

* <span data-ttu-id="84019-128">Nunca armazene dados confidenciais que podem ser perdidos na imagem de saudação ao criar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="84019-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="84019-129">Dados confidenciais sempre deve residir em um servidor de arquivos separado, separe a VM do Azure, na nuvem hello e instâncias de VM externo sempre toohello hospedar seus aplicativos no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="84019-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="84019-130">Dados de usuário é salvo e persistir no disco de perfil de usuário de saudação (UDP)</span><span class="sxs-lookup"><span data-stu-id="84019-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

