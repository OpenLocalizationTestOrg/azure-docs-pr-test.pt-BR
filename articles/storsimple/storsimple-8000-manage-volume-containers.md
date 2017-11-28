---
title: "aaaManage seus contêineres de volume StorSimple no dispositivo da série StorSimple 8000 do hello | Microsoft Docs"
description: "Explica como você pode usar o hello Gerenciador de dispositivos do StorSimple contêineres de volume do serviço página tooadd, modificar ou excluir um contêiner de volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="4c463-103">Use contêineres de volume Olá Gerenciador de dispositivos do StorSimple service toomanage StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c463-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="4c463-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4c463-104">Overview</span></span>
<span data-ttu-id="4c463-105">Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar contêineres de volume StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c463-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="4c463-106">Um contêiner de volume em um dispositivo Microsoft Azure StorSimple contém um ou mais volumes que compartilham as configurações da conta de armazenamento, da criptografia e do consumo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="4c463-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="4c463-107">Um dispositivo pode ter vários contêineres de volume para todos os seus volumes.</span><span class="sxs-lookup"><span data-stu-id="4c463-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="4c463-108">Um contêiner de volume possui Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="4c463-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="4c463-109">**Volumes** – Olá em camadas ou localmente afixado volumes do StorSimple contidos no contêiner de volume hello.</span><span class="sxs-lookup"><span data-stu-id="4c463-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="4c463-110">**Criptografia** – uma chave de criptografia que pode ser definida para cada contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="4c463-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="4c463-111">Essa chave é usada para criptografar dados Olá que são enviados de sua nuvem de toohello do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c463-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="4c463-112">Uma chave de grau militar AES de 256 bits é usada com a chave de usuário inserido hello.</span><span class="sxs-lookup"><span data-stu-id="4c463-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="4c463-113">toosecure seus dados, é recomendável que você sempre habilite a criptografia de armazenamento em nuvem.</span><span class="sxs-lookup"><span data-stu-id="4c463-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="4c463-114">**Conta de armazenamento** – Olá conta de armazenamento do Azure que é usado toostore Olá dados.</span><span class="sxs-lookup"><span data-stu-id="4c463-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="4c463-115">Todos os volumes de saudação que reside em um contêiner de volume compartilham essa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4c463-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="4c463-116">Você pode escolher uma conta de armazenamento de uma lista existente ou criar uma nova conta ao criar o contêiner de volume hello e, em seguida, especifique as credenciais de acesso de saudação para essa conta.</span><span class="sxs-lookup"><span data-stu-id="4c463-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="4c463-117">**Largura de banda em nuvem** – Olá largura de banda consumida pelo dispositivo hello quando dados de saudação do dispositivo hello está sendo enviados toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="4c463-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="4c463-118">Imponha um controle de largura de banda especificando um valor entre 1 e 1.000 Mbps ao criar esse contêiner.</span><span class="sxs-lookup"><span data-stu-id="4c463-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="4c463-119">Se você quiser Olá dispositivo tooconsume largura de banda disponível, defina este campo muito**Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="4c463-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="4c463-120">Você também pode criar e aplicar uma largura de banda modelo tooallocate largura de banda com base em agendamento.</span><span class="sxs-lookup"><span data-stu-id="4c463-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="4c463-121">Olá procedimentos a seguir explicam como toouse Olá StorSimple **contêineres de Volume** Olá toocomplete de folha operações comuns a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c463-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="4c463-122">Adicionar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-122">Add a volume container</span></span>
* <span data-ttu-id="4c463-123">Modificar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-123">Modify a volume container</span></span>
* <span data-ttu-id="4c463-124">Excluir um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="4c463-125">Adicionar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-125">Add a volume container</span></span>
<span data-ttu-id="4c463-126">Execute Olá seguindo as etapas tooadd um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="4c463-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="4c463-127">Modificar um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-127">Modify a volume container</span></span>
<span data-ttu-id="4c463-128">Execute Olá seguindo as etapas toomodify um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="4c463-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="4c463-129">Excluir um contêiner de volume</span><span class="sxs-lookup"><span data-stu-id="4c463-129">Delete a volume container</span></span>
<span data-ttu-id="4c463-130">Um contêiner de volume possui volumes dentro dele.</span><span class="sxs-lookup"><span data-stu-id="4c463-130">A volume container has volumes within it.</span></span> <span data-ttu-id="4c463-131">Ele pode ser excluído somente se todos os volumes de saudação contidos nele são excluídos primeiro.</span><span class="sxs-lookup"><span data-stu-id="4c463-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="4c463-132">Execute Olá seguindo as etapas toodelete um contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="4c463-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="4c463-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c463-133">Next steps</span></span>
* <span data-ttu-id="4c463-134">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="4c463-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="4c463-135">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4c463-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

