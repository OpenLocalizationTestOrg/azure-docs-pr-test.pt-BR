---
title: "aaaManage seus contêineres de volume StorSimple | Microsoft Docs"
description: "Explica como você pode usar o hello StorSimple Manager página tooadd contêineres de volume de serviço, modificar ou excluir um contêiner de volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="74e1a-103">Use contêineres de volume Olá Gerenciador StorSimple service toomanage StorSimple</span><span class="sxs-lookup"><span data-stu-id="74e1a-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="74e1a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="74e1a-104">Overview</span></span>
<span data-ttu-id="74e1a-105">Este tutorial explica como toouse Olá toocreate do serviço StorSimple Manager e gerenciar contêineres de volume StorSimple.</span><span class="sxs-lookup"><span data-stu-id="74e1a-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="74e1a-106">Um contêiner de volume em um dispositivo Microsoft Azure StorSimple contém um ou mais volumes que compartilham as configurações da conta de armazenamento, da criptografia e do consumo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="74e1a-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="74e1a-107">Um dispositivo pode ter vários contêineres de volume para todos os seus volumes.</span><span class="sxs-lookup"><span data-stu-id="74e1a-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="74e1a-108">Um contêiner de volume possui Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="74e1a-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="74e1a-109">**Volumes** – Olá em camadas ou localmente afixado volumes do StorSimple contidos no contêiner de volume hello.</span><span class="sxs-lookup"><span data-stu-id="74e1a-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="74e1a-110">Um contêiner de volume pode conter volumes do StorSimple too256.</span><span class="sxs-lookup"><span data-stu-id="74e1a-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="74e1a-111">**Criptografia** – uma chave de criptografia que pode ser definida para cada contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="74e1a-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="74e1a-112">Essa chave é usada para criptografar dados Olá que são enviados de sua nuvem de toohello do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="74e1a-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="74e1a-113">Uma chave de grau militar AES de 256 bits é usada com a chave de usuário inserido hello.</span><span class="sxs-lookup"><span data-stu-id="74e1a-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="74e1a-114">toosecure seus dados, é recomendável que você sempre habilite a criptografia de armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="74e1a-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="74e1a-115">**Conta de armazenamento** – Olá conta de armazenamento que é o provedor de serviço de armazenamento de nuvem tooyour vinculado.</span><span class="sxs-lookup"><span data-stu-id="74e1a-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="74e1a-116">Todos os volumes de saudação que reside em um contêiner de volume compartilham essa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="74e1a-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="74e1a-117">Você pode escolher uma conta de armazenamento de uma lista existente ou criar uma nova conta ao criar o contêiner de volume hello e, em seguida, especifique as credenciais de acesso de saudação para essa conta.</span><span class="sxs-lookup"><span data-stu-id="74e1a-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="74e1a-118">**Largura de banda em nuvem** – Olá largura de banda consumida pelo dispositivo hello quando dados de saudação do dispositivo hello está sendo enviados toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="74e1a-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="74e1a-119">Você pode impor um controle de largura de banda, especificando um valor entre 1 e 1000 Mbps ao definir esse contêiner.</span><span class="sxs-lookup"><span data-stu-id="74e1a-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="74e1a-120">Se você quiser Olá dispositivo tooconsume largura de banda disponível, defina tooUnlimited neste campo.</span><span class="sxs-lookup"><span data-stu-id="74e1a-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="74e1a-121">Você também pode criar e aplicar uma largura de banda modelo tooallocate largura de banda com base em agendamento.</span><span class="sxs-lookup"><span data-stu-id="74e1a-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Página de contêineres de volume](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="74e1a-123">Este procedimentos a seguir explicam como toouse Olá StorSimple **contêineres de Volume** Olá toocomplete de página operações comuns a seguir:</span><span class="sxs-lookup"><span data-stu-id="74e1a-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="74e1a-124">Adicionar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-124">Add a volume container</span></span> 
* <span data-ttu-id="74e1a-125">Modificar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-125">Modify a volume container</span></span> 
* <span data-ttu-id="74e1a-126">Excluir um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="74e1a-127">Adicionar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-127">Add a volume container</span></span>
<span data-ttu-id="74e1a-128">Execute Olá seguindo as etapas tooadd um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="74e1a-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="74e1a-129">Modificar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-129">Modify a volume container</span></span>
<span data-ttu-id="74e1a-130">Execute Olá seguindo as etapas toomodify um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="74e1a-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="74e1a-131">Excluir um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="74e1a-131">Delete a volume container</span></span>
<span data-ttu-id="74e1a-132">Um contêiner de volume possui volumes dentro dele.</span><span class="sxs-lookup"><span data-stu-id="74e1a-132">A volume container has volumes within it.</span></span> <span data-ttu-id="74e1a-133">Ele pode ser excluído somente se todos os volumes de saudação contidos nele são excluídos primeiro.</span><span class="sxs-lookup"><span data-stu-id="74e1a-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="74e1a-134">Execute Olá seguindo as etapas toodelete um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="74e1a-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="74e1a-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74e1a-135">Next steps</span></span>
* <span data-ttu-id="74e1a-136">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="74e1a-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="74e1a-137">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="74e1a-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

