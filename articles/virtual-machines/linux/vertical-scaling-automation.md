---
title: "escala de aaaVertically máquina virtual do Azure na automação do Azure | Microsoft Docs"
description: "Como toovertically dimensionar uma máquina Virtual Linux em alertas de toomonitoring de resposta na automação do Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="5607e-103">Dimensionar verticalmente uma máquina virtual Linux do Azure com a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="5607e-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="5607e-104">Dimensionamento vertical é o processo de saudação de aumentar ou diminuir os recursos de saudação de um computador na carga de trabalho de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="5607e-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="5607e-105">No Azure, isso pode ser feito alterando o tamanho de saudação do hello Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="5607e-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="5607e-106">Isso pode ajudar os seguintes cenários de saudação</span><span class="sxs-lookup"><span data-stu-id="5607e-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="5607e-107">Se Olá Máquina Virtual não está sendo usado com frequência, você pode redimensioná-la para baixo tooa menor tamanho tooreduce os custos mensais</span><span class="sxs-lookup"><span data-stu-id="5607e-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="5607e-108">Se Olá Máquina Virtual está vendo uma carga de pico, ele pode ser redimensionada tooa maior tamanho tooincrease sua capacidade</span><span class="sxs-lookup"><span data-stu-id="5607e-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="5607e-109">tópicos Olá Olá etapas tooaccomplish trata como abaixo</span><span class="sxs-lookup"><span data-stu-id="5607e-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="5607e-110">Instalação de automação do Azure tooaccess suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5607e-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="5607e-111">Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5607e-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="5607e-112">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="5607e-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="5607e-113">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="5607e-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="5607e-114">Devido ao tamanho de saudação do hello primeira Máquina Virtual, ele pode ser dimensionado, de tamanhos de saudação poderá ficar limitado devido a disponibilidade de toohello de saudação outros tamanhos de cluster Olá atual Máquina Virtual é implantada no.</span><span class="sxs-lookup"><span data-stu-id="5607e-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="5607e-115">Olá publicadas runbooks de automação usados neste artigo, podemos cuidar da ocorrência e dimensionar somente dentro de saudação abaixo pares de tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="5607e-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="5607e-116">Isso significa que uma máquina Virtual de Standard_D1v2 não repentinamente ser aumentadas tooStandard_G5 ou tooBasic_A0 foi reduzido.</span><span class="sxs-lookup"><span data-stu-id="5607e-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="5607e-117">Par de dimensionamento de tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="5607e-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="5607e-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="5607e-118">Basic_A0</span></span> |<span data-ttu-id="5607e-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="5607e-119">Basic_A4</span></span> |
> | <span data-ttu-id="5607e-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="5607e-120">Standard_A0</span></span> |<span data-ttu-id="5607e-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="5607e-121">Standard_A4</span></span> |
> | <span data-ttu-id="5607e-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="5607e-122">Standard_A5</span></span> |<span data-ttu-id="5607e-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="5607e-123">Standard_A7</span></span> |
> | <span data-ttu-id="5607e-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="5607e-124">Standard_A8</span></span> |<span data-ttu-id="5607e-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="5607e-125">Standard_A9</span></span> |
> | <span data-ttu-id="5607e-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="5607e-126">Standard_A10</span></span> |<span data-ttu-id="5607e-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="5607e-127">Standard_A11</span></span> |
> | <span data-ttu-id="5607e-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="5607e-128">Standard_D1</span></span> |<span data-ttu-id="5607e-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="5607e-129">Standard_D4</span></span> |
> | <span data-ttu-id="5607e-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="5607e-130">Standard_D11</span></span> |<span data-ttu-id="5607e-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="5607e-131">Standard_D14</span></span> |
> | <span data-ttu-id="5607e-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="5607e-132">Standard_DS1</span></span> |<span data-ttu-id="5607e-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="5607e-133">Standard_DS4</span></span> |
> | <span data-ttu-id="5607e-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="5607e-134">Standard_DS11</span></span> |<span data-ttu-id="5607e-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="5607e-135">Standard_DS14</span></span> |
> | <span data-ttu-id="5607e-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="5607e-136">Standard_D1v2</span></span> |<span data-ttu-id="5607e-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="5607e-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="5607e-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="5607e-138">Standard_D11v2</span></span> |<span data-ttu-id="5607e-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="5607e-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="5607e-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="5607e-140">Standard_G1</span></span> |<span data-ttu-id="5607e-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="5607e-141">Standard_G5</span></span> |
> | <span data-ttu-id="5607e-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="5607e-142">Standard_GS1</span></span> |<span data-ttu-id="5607e-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="5607e-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="5607e-144">Instalação de automação do Azure tooaccess suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5607e-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="5607e-145">Olá primeira coisa toodo é criar uma conta de automação do Azure que hospedará Olá runbooks usado tooscale Olá conjunto de escala de VM instâncias.</span><span class="sxs-lookup"><span data-stu-id="5607e-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="5607e-146">Serviço de automação Olá introduzidos recentemente recurso "Executar como conta" hello que torna Configurando Olá entidade de serviço para execução automática Olá runbooks em nome do usuário Olá muito fácil.</span><span class="sxs-lookup"><span data-stu-id="5607e-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="5607e-147">Você pode ler mais sobre isso em um artigo de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="5607e-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="5607e-148">Autenticar Runbooks com uma conta Executar como do Azure</span><span class="sxs-lookup"><span data-stu-id="5607e-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="5607e-149">Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5607e-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="5607e-150">Olá runbooks que são necessários para escalar verticalmente sua máquina Virtual já estão publicados em Olá Galeria de Runbook de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5607e-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="5607e-151">Você precisará tooimport-los em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="5607e-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="5607e-152">Você pode aprender como runbooks tooimport lendo Olá artigo a seguir.</span><span class="sxs-lookup"><span data-stu-id="5607e-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="5607e-153">Galerias de runbook e de módulos para a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="5607e-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="5607e-154">Olá runbooks que precisam toobe importado são mostrados na imagem de saudação abaixo</span><span class="sxs-lookup"><span data-stu-id="5607e-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importar Runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="5607e-156">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="5607e-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="5607e-157">Depois de importar runbooks Olá precisará tooadd um runbook de toohello webhook para que ele pode ser acionado por um alerta de uma máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="5607e-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="5607e-158">detalhes de saudação da criação de um webhook para seu Runbook podem ser lido aqui</span><span class="sxs-lookup"><span data-stu-id="5607e-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="5607e-159">Webhooks da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="5607e-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="5607e-160">Certifique-se de que copiar Olá webhook antes de fechar a caixa de diálogo de webhook hello como ele será necessário na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="5607e-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="5607e-161">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="5607e-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="5607e-162">Selecione Configurações da Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="5607e-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="5607e-163">Selecione “Regras de alerta”</span><span class="sxs-lookup"><span data-stu-id="5607e-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="5607e-164">Selecione “Adicionar alerta”</span><span class="sxs-lookup"><span data-stu-id="5607e-164">Select "Add alert"</span></span>
4. <span data-ttu-id="5607e-165">Selecione um alerta de saudação toofire métrica em</span><span class="sxs-lookup"><span data-stu-id="5607e-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="5607e-166">Selecione uma condição que, quando atendida será causar toofire alerta Olá</span><span class="sxs-lookup"><span data-stu-id="5607e-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="5607e-167">Selecione um limite para a condição de saudação na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="5607e-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="5607e-168">toobe atendida</span><span class="sxs-lookup"><span data-stu-id="5607e-168">toobe fulfilled</span></span>
7. <span data-ttu-id="5607e-169">Selecionar um período sobre quais Olá monitorando o serviço irá verificar para a condição de saudação e limite as etapas 5 e 6</span><span class="sxs-lookup"><span data-stu-id="5607e-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="5607e-170">Cole o webhook Olá copiada da seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="5607e-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Adicionar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

