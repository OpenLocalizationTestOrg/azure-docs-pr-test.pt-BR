---
title: "aaaLicensing Microsoft® Smooth Streaming Client Porting Kit"
description: "Saiba mais sobre como toolicensing Olá Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="4dbb6-103">Licenciamento do kit de portabilidade de cliente do Microsoft® Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="4dbb6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4dbb6-104">Overview</span></span>
<span data-ttu-id="4dbb6-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** abreviada) é uma implementação de cliente de Smooth Streaming otimizada toohelp inserido os fabricantes de dispositivo, cabo e operadoras móveis, provedores de serviço de conteúdo, fone fabricantes, fornecedores de software independentes (ISVs) e produtos de toocreate de provedores de soluções e serviços para streaming de conteúdo adaptável em formato Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="4dbb6-106">SSPK é uma implementação independente dispositivo e plataforma de cliente de Smooth Streaming que pode ser movido por plataforma e o dispositivo de tooany licenciado hello.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="4dbb6-107">Incluída abaixo é uma arquitetura de alto nível e caixa IIS Smooth Streaming Porting Kit é Olá Smooth Streaming Client implementação fornecida pela Microsoft e inclui toda a lógica de núcleo Olá para reprodução de conteúdo de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="4dbb6-108">Em seguida, isso será portado por parceiros para um dispositivo ou plataforma específicos, implementando interfaces apropriadas.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="4dbb6-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="4dbb6-110">Description</span></span>
<span data-ttu-id="4dbb6-111">O SSPK é licenciado em termos que oferecem excelente valor comercial.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="4dbb6-112">Licença SSPK fornece setor Olá com:</span><span class="sxs-lookup"><span data-stu-id="4dbb6-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="4dbb6-113">a fonte do Kit de Portabilidade de Smooth Streaming em C++</span><span class="sxs-lookup"><span data-stu-id="4dbb6-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="4dbb6-114">implementa a funcionalidade de Cliente do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="4dbb6-115">adiciona a análise de formato, heurística, lógica de buffer etc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="4dbb6-116">APIs do aplicativo Player</span><span class="sxs-lookup"><span data-stu-id="4dbb6-116">Player application APIs</span></span> 
  * <span data-ttu-id="4dbb6-117">interfaces de programação para interação com um aplicativo de player de mídia</span><span class="sxs-lookup"><span data-stu-id="4dbb6-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="4dbb6-118">Interface da Camada de Abstração de Plataforma (PAL)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="4dbb6-119">interfaces de programação para interação com o sistema operacional de saudação (threads, soquetes)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="4dbb6-120">Interface da Camada de Abstração de Hardware (HAL)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="4dbb6-121">interfaces de programação para interação com decodificadores A/V de hardware (decodificação, renderização)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="4dbb6-122">Interface de Gerenciamento de Direitos Digitais (DRM)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="4dbb6-123">interfaces de programação para lidar com DRM por meio de saudação DRM abstração DAL (camada)</span><span class="sxs-lookup"><span data-stu-id="4dbb6-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="4dbb6-124">O Kit de Portabilidade do Microsoft PlayReady é fornecido separadamente, mas se integra por meio dessa interface.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="4dbb6-125">Para saber mais sobre o licenciamento do Dispositivo Microsoft PlayReady, clique [aqui](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="4dbb6-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="4dbb6-126">Amostras de implementação</span><span class="sxs-lookup"><span data-stu-id="4dbb6-126">Implementation samples</span></span> 
  * <span data-ttu-id="4dbb6-127">implementação de amostra de PAL para Linux</span><span class="sxs-lookup"><span data-stu-id="4dbb6-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="4dbb6-128">implementação de amostra de HAL para GStreamer</span><span class="sxs-lookup"><span data-stu-id="4dbb6-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="4dbb6-129">Opções de Licenciamento</span><span class="sxs-lookup"><span data-stu-id="4dbb6-129">Licensing Options</span></span>
<span data-ttu-id="4dbb6-130">Microsoft Smooth Streaming Client Porting Kit é feita toolicensees disponível em dois contratos de licença distintas: uma para o desenvolvimento de Smooth Streaming Client provisória produtos e outro para a distribuição de usuários de tooend Smooth Streaming Final produtos de cliente.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="4dbb6-131">Kit de toodevelop provisória produtos, um Microsoft Smooth Streaming Client Porting Kit para fabricantes de chipset, integradores de sistema ou software independente ISVs (fornecedores) que exigem uma movimentação de código fonte **licença do produto provisória** deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="4dbb6-132">Para os fabricantes de dispositivo ou ISVs que precisam de direitos de distribuição para os usuários tooend de Smooth Streaming Final produtos de cliente, Olá Microsoft Smooth Streaming Client Porting Kit **Final de licenças de produto** devem ser executados.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="4dbb6-133">Licença de Produto Provisório do Kit de Portabilidade de Cliente do Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="4dbb6-134">Sob esta licença Microsoft oferece um Smooth Streaming Client Porting Kit Olá toodevelop de direitos de propriedade intelectual necessários e distribuir licenciados de dispositivo do Smooth Streaming Client provisória produtos tooother Smooth Streaming Client Porting Kit que Distribua Smooth Streaming Final produtos de cliente.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="4dbb6-135">Estrutura de taxa</span><span class="sxs-lookup"><span data-stu-id="4dbb6-135">Fee structure</span></span>
<span data-ttu-id="4dbb6-136">Uma taxa de licença única de US $50.000 fornece acesso toohello Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="4dbb6-137">Licença de Produto Final do Kit de Portabilidade de Cliente do Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="4dbb6-138">Sob esta licença, a Microsoft oferece todos os tooreceive de direitos de propriedade intelectual Smooth Streaming Client provisória produtos de outras licenças de Smooth Streaming Client Porting Kit e toodistribute da empresa com a marca Final de cliente Smooth Streaming Usuários tooend de produtos.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="4dbb6-139">Estrutura de taxa</span><span class="sxs-lookup"><span data-stu-id="4dbb6-139">Fee structure</span></span>
<span data-ttu-id="4dbb6-140">Olá Smooth Streaming Client Final do produto é oferecido em um modelo de direitos autorais, como em:</span><span class="sxs-lookup"><span data-stu-id="4dbb6-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="4dbb6-141">US$ 0,10 por implementação de dispositivo fornecida</span><span class="sxs-lookup"><span data-stu-id="4dbb6-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="4dbb6-142">royalty Hello está limitado a r $50.000 por ano</span><span class="sxs-lookup"><span data-stu-id="4dbb6-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="4dbb6-143">Nenhum royalty para as primeiras 10.000 implementações de dispositivo por ano</span><span class="sxs-lookup"><span data-stu-id="4dbb6-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="4dbb6-144">Procedimento de licenciamento e acesso do SSPK</span><span class="sxs-lookup"><span data-stu-id="4dbb6-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="4dbb6-145">Caso tenha alguma dúvida sobre licenciamento, envie um email para [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="4dbb6-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="4dbb6-146">Olá [portal SSPK distribuição](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) é acessível tooregistered licenciados provisória.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="4dbb6-147">Licenciados provisória e SSPK Final podem enviar perguntas técnicas muito[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4dbb6-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="4dbb6-148">Licenciados do Contrato do Produto provisório do cliente do Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="4dbb6-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="4dbb6-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="4dbb6-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="4dbb6-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="4dbb6-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="4dbb6-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="4dbb6-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-153">Alticast Corporation</span></span>
* <span data-ttu-id="4dbb6-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="4dbb6-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="4dbb6-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-157">Cavium, Inc.</span></span>
* <span data-ttu-id="4dbb6-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="4dbb6-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-159">Enseo, Inc.</span></span>
* <span data-ttu-id="4dbb6-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-160">Fluendo S.A.</span></span>
* <span data-ttu-id="4dbb6-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="4dbb6-162">Infomir GMBH</span></span>
* <span data-ttu-id="4dbb6-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="4dbb6-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="4dbb6-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="4dbb6-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="4dbb6-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-166">MediaTek Inc.</span></span>
* <span data-ttu-id="4dbb6-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="4dbb6-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="4dbb6-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="4dbb6-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="4dbb6-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="4dbb6-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="4dbb6-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="4dbb6-172">SoftAtHome</span></span>
* <span data-ttu-id="4dbb6-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-173">Sony Corporation</span></span>
* <span data-ttu-id="4dbb6-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="4dbb6-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="4dbb6-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="4dbb6-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="4dbb6-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="4dbb6-180">Licenciados do Contrato do Produto final do cliente do Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="4dbb6-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="4dbb6-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="4dbb6-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="4dbb6-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="4dbb6-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="4dbb6-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="4dbb6-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="4dbb6-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="4dbb6-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="4dbb6-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-189">VE TİC.</span></span> <span data-ttu-id="4dbb6-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="4dbb6-190">A.Ş</span></span>
* <span data-ttu-id="4dbb6-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="4dbb6-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="4dbb6-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="4dbb6-193">Compal eletrônicos, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="4dbb6-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="4dbb6-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="4dbb6-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-196">Enseo, Inc.</span></span>
* <span data-ttu-id="4dbb6-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="4dbb6-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-198">Fluendo S.A.</span></span>
* <span data-ttu-id="4dbb6-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="4dbb6-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="4dbb6-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="4dbb6-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="4dbb6-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="4dbb6-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="4dbb6-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="4dbb6-205">Infomir GMBH</span></span>
* <span data-ttu-id="4dbb6-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-207">KDDI Corporation</span></span>
* <span data-ttu-id="4dbb6-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="4dbb6-209">Orange SA</span></span>
* <span data-ttu-id="4dbb6-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="4dbb6-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="4dbb6-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="4dbb6-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="4dbb6-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="4dbb6-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="4dbb6-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="4dbb6-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="4dbb6-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="4dbb6-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="4dbb6-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="4dbb6-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="4dbb6-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="4dbb6-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="4dbb6-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="4dbb6-219">SoftAtHome</span></span>
* <span data-ttu-id="4dbb6-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-220">Sony Corporation</span></span>
* <span data-ttu-id="4dbb6-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="4dbb6-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="4dbb6-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="4dbb6-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="4dbb6-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="4dbb6-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="4dbb6-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="4dbb6-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="4dbb6-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="4dbb6-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="4dbb6-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-228">Wistron Corporation</span></span>
* <span data-ttu-id="4dbb6-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="4dbb6-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="4dbb6-230">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="4dbb6-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4dbb6-231">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="4dbb6-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

