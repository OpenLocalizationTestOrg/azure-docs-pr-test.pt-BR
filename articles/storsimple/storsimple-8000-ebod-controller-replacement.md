---
title: aaaReplace um controlador StorSimple 8600 EBOD | Microsoft Docs
description: Explica como tooremove e substituir um ou ambos os controladores EBOD em um dispositivo 8600 StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="41a4d-103">Substituir um controlador EBOD em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="41a4d-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="41a4d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="41a4d-104">Overview</span></span>
<span data-ttu-id="41a4d-105">Este tutorial explica como tooreplace um módulo do controlador EBOD com falha em seu dispositivo StorSimple do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="41a4d-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="41a4d-106">tooreplace um módulo do controlador EBOD, você precisa:</span><span class="sxs-lookup"><span data-stu-id="41a4d-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="41a4d-107">Remover o controlador EBOD com falha de saudação</span><span class="sxs-lookup"><span data-stu-id="41a4d-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="41a4d-108">Instalar um novo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-108">Install a new EBOD controller</span></span>

<span data-ttu-id="41a4d-109">Considere Olá informações a seguir antes de começar:</span><span class="sxs-lookup"><span data-stu-id="41a4d-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="41a4d-110">Módulos EBOD em branco precisam ser inseridos em todos os slots não utilizados.</span><span class="sxs-lookup"><span data-stu-id="41a4d-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="41a4d-111">compartimento de saudação não será resfriado corretamente se um slot for deixado aberto.</span><span class="sxs-lookup"><span data-stu-id="41a4d-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="41a4d-112">controlador do EBOD Olá é intercambiável e pode ser removido ou substituído.</span><span class="sxs-lookup"><span data-stu-id="41a4d-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="41a4d-113">Não remova um módulo com falha até que você tenha uma peça de reposição.</span><span class="sxs-lookup"><span data-stu-id="41a4d-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="41a4d-114">Quando você iniciar o processo de substituição hello, você deve finalizá-lo dentro de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="41a4d-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41a4d-115">Antes de tentar tooremove ou substituir qualquer componente do StorSimple, certifique-se de que você examine Olá [convenções de ícone de segurança](storsimple-safety.md#safety-icon-conventions) e outros [precauções de segurança](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="41a4d-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="41a4d-116">Remover um controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-116">Remove an EBOD controller</span></span>
<span data-ttu-id="41a4d-117">Antes de falha ao substituir Olá módulo controlador EBOD em seu dispositivo StorSimple, verifique se esse Olá outro módulo controlador EBOD está ativo e em execução.</span><span class="sxs-lookup"><span data-stu-id="41a4d-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="41a4d-118">Olá procedimento e a tabela a seguir explicam como tooremove Olá módulo do controlador EBOD.</span><span class="sxs-lookup"><span data-stu-id="41a4d-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="41a4d-119">tooremove um módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="41a4d-120">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="41a4d-120">Open hello Azure portal.</span></span>
2. <span data-ttu-id="41a4d-121">Acesse o dispositivo tooyour e navegue muito**configurações** > **a integridade do Hardware**e verifique se esse status de saudação do hello LED de módulo do controlador EBOD ativo Olá é verde e hello LED para Olá falhado Módulo do controlador EBOD é vermelho.</span><span class="sxs-lookup"><span data-stu-id="41a4d-121">Go tooyour device and navigate too**Settings** > **Hardware health**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="41a4d-122">Localize o módulo do controlador EBOD Olá falhado no hello parte posterior do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="41a4d-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="41a4d-123">Remova os cabos de saudação que se conectam a saudação EBOD módulo toohello controlador antes de retirar o módulo EBOD de saudação do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="41a4d-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="41a4d-124">Tome nota da porta SAS exata de saudação do módulo do controlador EBOD Olá que estava conectado toohello controlador.</span><span class="sxs-lookup"><span data-stu-id="41a4d-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="41a4d-125">Configuração de toothis toorestore necessário Olá sistema será depois de substituir o módulo EBOD de saudação.</span><span class="sxs-lookup"><span data-stu-id="41a4d-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="41a4d-126">Normalmente, isso será a porta A, que é rotulada como **hospedar em** em Olá diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="41a4d-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   
    ![Backplane do controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="41a4d-128">**Figura 1** Parte posterior do módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="41a4d-129">Rótulo</span><span class="sxs-lookup"><span data-stu-id="41a4d-129">Label</span></span> | <span data-ttu-id="41a4d-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="41a4d-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="41a4d-131">1</span><span class="sxs-lookup"><span data-stu-id="41a4d-131">1</span></span> |<span data-ttu-id="41a4d-132">LED de falha</span><span class="sxs-lookup"><span data-stu-id="41a4d-132">Fault LED</span></span> |
   | <span data-ttu-id="41a4d-133">2</span><span class="sxs-lookup"><span data-stu-id="41a4d-133">2</span></span> |<span data-ttu-id="41a4d-134">LED de energia</span><span class="sxs-lookup"><span data-stu-id="41a4d-134">Power LED</span></span> |
   | <span data-ttu-id="41a4d-135">3</span><span class="sxs-lookup"><span data-stu-id="41a4d-135">3</span></span> |<span data-ttu-id="41a4d-136">Conectores SAS</span><span class="sxs-lookup"><span data-stu-id="41a4d-136">SAS connectors</span></span> |
   | <span data-ttu-id="41a4d-137">4</span><span class="sxs-lookup"><span data-stu-id="41a4d-137">4</span></span> |<span data-ttu-id="41a4d-138">LEDs de SAS</span><span class="sxs-lookup"><span data-stu-id="41a4d-138">SAS LEDs</span></span> |
   | <span data-ttu-id="41a4d-139">5</span><span class="sxs-lookup"><span data-stu-id="41a4d-139">5</span></span> |<span data-ttu-id="41a4d-140">Portas seriais apenas para uso em fábrica</span><span class="sxs-lookup"><span data-stu-id="41a4d-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="41a4d-141">6</span><span class="sxs-lookup"><span data-stu-id="41a4d-141">6</span></span> |<span data-ttu-id="41a4d-142">Porta A (Host in)</span><span class="sxs-lookup"><span data-stu-id="41a4d-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="41a4d-143">7</span><span class="sxs-lookup"><span data-stu-id="41a4d-143">7</span></span> |<span data-ttu-id="41a4d-144">Porta B (Host out)</span><span class="sxs-lookup"><span data-stu-id="41a4d-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="41a4d-145">8</span><span class="sxs-lookup"><span data-stu-id="41a4d-145">8</span></span> |<span data-ttu-id="41a4d-146">Porta C (Apenas para uso em fábrica)</span><span class="sxs-lookup"><span data-stu-id="41a4d-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="41a4d-147">Instalar um novo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-147">Install a new EBOD controller</span></span>
<span data-ttu-id="41a4d-148">Olá procedimento e a tabela a seguir explicam como tooinstall um módulo do controlador EBOD no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41a4d-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="41a4d-149">tooinstall um controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="41a4d-150">Verifique o dispositivo EBOD de saudação danos, especialmente toohello conector da interface.</span><span class="sxs-lookup"><span data-stu-id="41a4d-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="41a4d-151">Não instale o novo controlador de EBOD Olá se algum pino estiver torto.</span><span class="sxs-lookup"><span data-stu-id="41a4d-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="41a4d-152">Com travas Olá Olá abra posição, módulo de saudação do slide para compartimento Olá até Olá travas.</span><span class="sxs-lookup"><span data-stu-id="41a4d-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Instalando o controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="41a4d-154">**Figura 2** módulo do controlador do EBOD instalando Olá</span><span class="sxs-lookup"><span data-stu-id="41a4d-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="41a4d-155">Trava Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="41a4d-155">Close hello latch.</span></span> <span data-ttu-id="41a4d-156">Você ouvirá um clique quando Olá trava estiver no lugar.</span><span class="sxs-lookup"><span data-stu-id="41a4d-156">You should hear a click as hello latch engages.</span></span>
   
    ![Liberando a trava do EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="41a4d-158">**Figura 3** fechando a trava do módulo EBOD Olá</span><span class="sxs-lookup"><span data-stu-id="41a4d-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="41a4d-159">Reconecte os cabos de saudação.</span><span class="sxs-lookup"><span data-stu-id="41a4d-159">Reconnect hello cables.</span></span> <span data-ttu-id="41a4d-160">Use Olá configuração exata que foi apresentada antes da substituição de saudação.</span><span class="sxs-lookup"><span data-stu-id="41a4d-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="41a4d-161">Consulte o diagrama a seguir de saudação e de tabela para obter detalhes sobre como os cabos de saudação do tooconnect.</span><span class="sxs-lookup"><span data-stu-id="41a4d-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Cabeamento do dispositivo 4U para alimentação](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="41a4d-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="41a4d-163">**Figure 4**.</span></span> <span data-ttu-id="41a4d-164">Reconectando os cabos</span><span class="sxs-lookup"><span data-stu-id="41a4d-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="41a4d-165">Rótulo</span><span class="sxs-lookup"><span data-stu-id="41a4d-165">Label</span></span> | <span data-ttu-id="41a4d-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="41a4d-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="41a4d-167">1</span><span class="sxs-lookup"><span data-stu-id="41a4d-167">1</span></span> |<span data-ttu-id="41a4d-168">Compartimento principal</span><span class="sxs-lookup"><span data-stu-id="41a4d-168">Primary enclosure</span></span> |
   | <span data-ttu-id="41a4d-169">2</span><span class="sxs-lookup"><span data-stu-id="41a4d-169">2</span></span> |<span data-ttu-id="41a4d-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="41a4d-170">PCM 0</span></span> |
   | <span data-ttu-id="41a4d-171">3</span><span class="sxs-lookup"><span data-stu-id="41a4d-171">3</span></span> |<span data-ttu-id="41a4d-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="41a4d-172">PCM 1</span></span> |
   | <span data-ttu-id="41a4d-173">4</span><span class="sxs-lookup"><span data-stu-id="41a4d-173">4</span></span> |<span data-ttu-id="41a4d-174">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="41a4d-174">Controller 0</span></span> |
   | <span data-ttu-id="41a4d-175">5</span><span class="sxs-lookup"><span data-stu-id="41a4d-175">5</span></span> |<span data-ttu-id="41a4d-176">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="41a4d-176">Controller 1</span></span> |
   | <span data-ttu-id="41a4d-177">6</span><span class="sxs-lookup"><span data-stu-id="41a4d-177">6</span></span> |<span data-ttu-id="41a4d-178">Controlador 0 do EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="41a4d-179">7</span><span class="sxs-lookup"><span data-stu-id="41a4d-179">7</span></span> |<span data-ttu-id="41a4d-180">Controlador 1 do EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="41a4d-181">8</span><span class="sxs-lookup"><span data-stu-id="41a4d-181">8</span></span> |<span data-ttu-id="41a4d-182">Compartimento EBOD</span><span class="sxs-lookup"><span data-stu-id="41a4d-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="41a4d-183">9</span><span class="sxs-lookup"><span data-stu-id="41a4d-183">9</span></span> |<span data-ttu-id="41a4d-184">Unidades de distribuição de energia</span><span class="sxs-lookup"><span data-stu-id="41a4d-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41a4d-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41a4d-185">Next steps</span></span>
<span data-ttu-id="41a4d-186">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="41a4d-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

