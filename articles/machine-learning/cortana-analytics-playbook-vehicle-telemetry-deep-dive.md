---
title: "Aprofunde-se nos aaaDeep prever a integridade de veículo e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="1f739-103">Guia estratégico de solução de análise de telemetria veículo: mergulho profundo na solução Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="1f739-104">Isso **menu** toohello seções neste guia estratégico de links:</span><span class="sxs-lookup"><span data-stu-id="1f739-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="1f739-105">Esta seção faz uma busca detalhada em cada um dos estágios Olá descritos nos Olá arquitetura da solução com instruções e ponteiros para personalização.</span><span class="sxs-lookup"><span data-stu-id="1f739-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="1f739-106">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="1f739-106">Data Sources</span></span>
<span data-ttu-id="1f739-107">solução de saudação usa duas fontes de dados diferentes:</span><span class="sxs-lookup"><span data-stu-id="1f739-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="1f739-108">**sinais de veículo simulados, conjunto de dados de diagnóstico** e</span><span class="sxs-lookup"><span data-stu-id="1f739-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="1f739-109">**catálogo do veículo**</span><span class="sxs-lookup"><span data-stu-id="1f739-109">**vehicle catalog**</span></span>

<span data-ttu-id="1f739-110">Um simulador de telemática do veículo é incluído como parte desta solução.</span><span class="sxs-lookup"><span data-stu-id="1f739-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="1f739-111">Ele emite informações de diagnóstico e sinaliza o estado toohello correspondente de veículo hello e toohello direcionando padrão em um determinado ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="1f739-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="1f739-112">Clique em [veículo Telemáticas da simulador](http://go.microsoft.com/fwlink/?LinkId=717075) Olá toodownload **veículo Telemáticas da simulador solução do Visual Studio** personalizações com base nos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="1f739-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="1f739-113">Catálogo de veículo Olá contém um conjunto de dados de referência com um mapeamento de toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="1f739-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Simulador de telemática do veículo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="1f739-115">*Figura 1 – Simulador de Telemática do Veículo*</span><span class="sxs-lookup"><span data-stu-id="1f739-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="1f739-116">Este é um conjunto de dados formatados em JSON que contém Olá esquema a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f739-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="1f739-117">Coluna</span><span class="sxs-lookup"><span data-stu-id="1f739-117">Column</span></span> | <span data-ttu-id="1f739-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="1f739-118">Description</span></span> | <span data-ttu-id="1f739-119">Valores</span><span class="sxs-lookup"><span data-stu-id="1f739-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f739-120">VIN</span><span class="sxs-lookup"><span data-stu-id="1f739-120">VIN</span></span> |<span data-ttu-id="1f739-121">Número de Identificação do Veículo gerado aleatoriamente</span><span class="sxs-lookup"><span data-stu-id="1f739-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="1f739-122">É obtido em uma lista principal de 10.000 números de identificação do veículo gerados aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="1f739-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="1f739-123">Temperatura externa</span><span class="sxs-lookup"><span data-stu-id="1f739-123">Outside temperature</span></span> |<span data-ttu-id="1f739-124">Olá fora temperatura onde o veículo hello está aumentando</span><span class="sxs-lookup"><span data-stu-id="1f739-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="1f739-125">Número gerado aleatoriamente de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="1f739-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="1f739-126">Temperatura do motor</span><span class="sxs-lookup"><span data-stu-id="1f739-126">Engine temperature</span></span> |<span data-ttu-id="1f739-127">temperatura de mecanismo de saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="1f739-128">Número gerado aleatoriamente de 0 a 500</span><span class="sxs-lookup"><span data-stu-id="1f739-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="1f739-129">Velocidade</span><span class="sxs-lookup"><span data-stu-id="1f739-129">Speed</span></span> |<span data-ttu-id="1f739-130">velocidade do mecanismo Olá no qual Olá veículo está aumentando</span><span class="sxs-lookup"><span data-stu-id="1f739-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="1f739-131">Número gerado aleatoriamente de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="1f739-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="1f739-132">Combustível</span><span class="sxs-lookup"><span data-stu-id="1f739-132">Fuel</span></span> |<span data-ttu-id="1f739-133">nível de combustível de saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="1f739-134">Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível de combustível)</span><span class="sxs-lookup"><span data-stu-id="1f739-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="1f739-135">Óleo do Motor</span><span class="sxs-lookup"><span data-stu-id="1f739-135">EngineOil</span></span> |<span data-ttu-id="1f739-136">nível de petróleo mecanismo saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="1f739-137">Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível de óleo do motor)</span><span class="sxs-lookup"><span data-stu-id="1f739-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="1f739-138">Pressão do pneu</span><span class="sxs-lookup"><span data-stu-id="1f739-138">Tire pressure</span></span> |<span data-ttu-id="1f739-139">pressão de pneu de saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="1f739-140">Número gerado aleatoriamente de 0 a 50 (indica a porcentagem do nível de pressão do pneu)</span><span class="sxs-lookup"><span data-stu-id="1f739-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="1f739-141">Hodômetro</span><span class="sxs-lookup"><span data-stu-id="1f739-141">Odometer</span></span> |<span data-ttu-id="1f739-142">leitura do odômetro saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="1f739-143">Número gerado aleatoriamente de 0 a 200.000</span><span class="sxs-lookup"><span data-stu-id="1f739-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="1f739-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="1f739-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="1f739-145">posição de pedais Olá acelerador de veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="1f739-146">Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível do acelerador)</span><span class="sxs-lookup"><span data-stu-id="1f739-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="1f739-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="1f739-147">Parking_brake_status</span></span> |<span data-ttu-id="1f739-148">Indica se o veículo hello está estacionado ou não</span><span class="sxs-lookup"><span data-stu-id="1f739-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="1f739-149">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-149">True or False</span></span> |
| <span data-ttu-id="1f739-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="1f739-150">Headlamp_status</span></span> |<span data-ttu-id="1f739-151">Indica onde lâmpada frontal de saudação está ativa ou não</span><span class="sxs-lookup"><span data-stu-id="1f739-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="1f739-152">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-152">True or False</span></span> |
| <span data-ttu-id="1f739-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="1f739-153">Brake_pedal_status</span></span> |<span data-ttu-id="1f739-154">Indica se o pedal de freio Olá é pressionado ou não</span><span class="sxs-lookup"><span data-stu-id="1f739-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="1f739-155">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-155">True or False</span></span> |
| <span data-ttu-id="1f739-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="1f739-156">Transmission_gear_position</span></span> |<span data-ttu-id="1f739-157">posição de engrenagem Olá transmissão de veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="1f739-158">Estados: primeira, segunda, terceira, quarta, quinta, sexta, sétima, oitava</span><span class="sxs-lookup"><span data-stu-id="1f739-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="1f739-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="1f739-159">Ignition_status</span></span> |<span data-ttu-id="1f739-160">Indica se o veículo hello está em execução ou parado</span><span class="sxs-lookup"><span data-stu-id="1f739-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="1f739-161">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-161">True or False</span></span> |
| <span data-ttu-id="1f739-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="1f739-162">Windshield_wiper_status</span></span> |<span data-ttu-id="1f739-163">Indica se a wiper de para-brisa hello está ativada ou não</span><span class="sxs-lookup"><span data-stu-id="1f739-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="1f739-164">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-164">True or False</span></span> |
| <span data-ttu-id="1f739-165">ABS</span><span class="sxs-lookup"><span data-stu-id="1f739-165">ABS</span></span> |<span data-ttu-id="1f739-166">Indica se o ABS está engatado ou não</span><span class="sxs-lookup"><span data-stu-id="1f739-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="1f739-167">Verdadeiro ou Falso</span><span class="sxs-lookup"><span data-stu-id="1f739-167">True or False</span></span> |
| <span data-ttu-id="1f739-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="1f739-168">Timestamp</span></span> |<span data-ttu-id="1f739-169">Olá carimbo de hora do ponto de dados de saudação é criado</span><span class="sxs-lookup"><span data-stu-id="1f739-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="1f739-170">Data</span><span class="sxs-lookup"><span data-stu-id="1f739-170">Date</span></span> |
| <span data-ttu-id="1f739-171">City</span><span class="sxs-lookup"><span data-stu-id="1f739-171">City</span></span> |<span data-ttu-id="1f739-172">local de saudação do veículo Olá</span><span class="sxs-lookup"><span data-stu-id="1f739-172">hello location of hello vehicle</span></span> |<span data-ttu-id="1f739-173">Há quatro cidades nesta solução: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="1f739-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="1f739-174">conjunto de dados de referência do Hello veículo modelo contém o mapeamento do modelo toohello VIN.</span><span class="sxs-lookup"><span data-stu-id="1f739-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="1f739-175">VIN</span><span class="sxs-lookup"><span data-stu-id="1f739-175">VIN</span></span> | <span data-ttu-id="1f739-176">Modelo</span><span class="sxs-lookup"><span data-stu-id="1f739-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="1f739-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="1f739-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="1f739-178">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-178">Sedan</span></span> |
| <span data-ttu-id="1f739-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="1f739-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="1f739-180">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-180">Hybrid</span></span> |
| <span data-ttu-id="1f739-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="1f739-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="1f739-182">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-182">Family Saloon</span></span> |
| <span data-ttu-id="1f739-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="1f739-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="1f739-184">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-184">Sedan</span></span> |
| <span data-ttu-id="1f739-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="1f739-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="1f739-186">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-186">Hybrid</span></span> |
| <span data-ttu-id="1f739-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="1f739-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="1f739-188">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-188">Family Saloon</span></span> |
| <span data-ttu-id="1f739-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="1f739-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="1f739-190">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-190">Sedan</span></span> |
| <span data-ttu-id="1f739-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="1f739-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="1f739-192">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-192">Hybrid</span></span> |
| <span data-ttu-id="1f739-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="1f739-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="1f739-194">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-194">Family Saloon</span></span> |
| <span data-ttu-id="1f739-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="1f739-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="1f739-196">Conversível</span><span class="sxs-lookup"><span data-stu-id="1f739-196">Convertible</span></span> |
| <span data-ttu-id="1f739-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="1f739-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="1f739-198">Van</span><span class="sxs-lookup"><span data-stu-id="1f739-198">Station Wagon</span></span> |
| <span data-ttu-id="1f739-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="1f739-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="1f739-200">Carro compacto</span><span class="sxs-lookup"><span data-stu-id="1f739-200">Compact Car</span></span> |
| <span data-ttu-id="1f739-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="1f739-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="1f739-202">SUV pequeno</span><span class="sxs-lookup"><span data-stu-id="1f739-202">Small SUV</span></span> |
| <span data-ttu-id="1f739-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="1f739-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="1f739-204">Carro esportivo</span><span class="sxs-lookup"><span data-stu-id="1f739-204">Sports Car</span></span> |
| <span data-ttu-id="1f739-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="1f739-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="1f739-206">SUV médio</span><span class="sxs-lookup"><span data-stu-id="1f739-206">Medium SUV</span></span> |
| <span data-ttu-id="1f739-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="1f739-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="1f739-208">Van</span><span class="sxs-lookup"><span data-stu-id="1f739-208">Station Wagon</span></span> |
| <span data-ttu-id="1f739-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="1f739-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="1f739-210">SUV grande</span><span class="sxs-lookup"><span data-stu-id="1f739-210">Large SUV</span></span> |
| <span data-ttu-id="1f739-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="1f739-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="1f739-212">SUV grande</span><span class="sxs-lookup"><span data-stu-id="1f739-212">Large SUV</span></span> |
| <span data-ttu-id="1f739-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="1f739-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="1f739-214">Cupê</span><span class="sxs-lookup"><span data-stu-id="1f739-214">Coupe</span></span> |
| <span data-ttu-id="1f739-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="1f739-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="1f739-216">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-216">Sedan</span></span> |
| <span data-ttu-id="1f739-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="1f739-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="1f739-218">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-218">Hybrid</span></span> |
| <span data-ttu-id="1f739-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="1f739-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="1f739-220">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-220">Family Saloon</span></span> |
| <span data-ttu-id="1f739-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="1f739-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="1f739-222">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-222">Sedan</span></span> |
| <span data-ttu-id="1f739-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="1f739-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="1f739-224">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-224">Hybrid</span></span> |
| <span data-ttu-id="1f739-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="1f739-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="1f739-226">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-226">Family Saloon</span></span> |
| <span data-ttu-id="1f739-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="1f739-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="1f739-228">Automóvel Sedan</span><span class="sxs-lookup"><span data-stu-id="1f739-228">Sedan</span></span> |
| <span data-ttu-id="1f739-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="1f739-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="1f739-230">Híbrido</span><span class="sxs-lookup"><span data-stu-id="1f739-230">Hybrid</span></span> |
| <span data-ttu-id="1f739-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="1f739-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="1f739-232">Automóvel de três volumes</span><span class="sxs-lookup"><span data-stu-id="1f739-232">Family Saloon</span></span> |
| <span data-ttu-id="1f739-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="1f739-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="1f739-234">Conversível</span><span class="sxs-lookup"><span data-stu-id="1f739-234">Convertible</span></span> |
| <span data-ttu-id="1f739-235">…….</span><span class="sxs-lookup"><span data-stu-id="1f739-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="1f739-236">Referências</span><span class="sxs-lookup"><span data-stu-id="1f739-236">References</span></span>
[<span data-ttu-id="1f739-237">Solução Vehicle Telematics Simulator do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f739-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="1f739-238">Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="1f739-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="1f739-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f739-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="1f739-240">Ingestão</span><span class="sxs-lookup"><span data-stu-id="1f739-240">Ingestion</span></span>
<span data-ttu-id="1f739-241">Combinações de fábrica de dados, análise de fluxo e Hubs de eventos do Azure são sinais de veículo tooingest utilizou hello, eventos de diagnóstico Olá e em tempo real e análise em lote.</span><span class="sxs-lookup"><span data-stu-id="1f739-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="1f739-242">Todos esses componentes são criados e configurados como parte da implantação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="1f739-243">Análise em tempo real</span><span class="sxs-lookup"><span data-stu-id="1f739-243">Real-time analysis</span></span>
<span data-ttu-id="1f739-244">Olá eventos gerados pelo Olá veículo Telemáticas da simulador são publicados usando o Hub de eventos toohello Olá SDK do Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f739-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="1f739-245">trabalho de análise de fluxo de saudação consome esses eventos de saudação Hub de eventos e processos Olá dados a integridade de veículo de saudação tooanalyze em tempo real.</span><span class="sxs-lookup"><span data-stu-id="1f739-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Painel do Hub de Eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="1f739-247">*Figura 4 – Painel do Hub de Eventos*</span><span class="sxs-lookup"><span data-stu-id="1f739-247">*Figure 4 - Event Hub dashboard*</span></span>

![Dados de processamento do trabalho do Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="1f739-249">*Figura 5 – Dados de processamento do trabalho do Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="1f739-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="1f739-250">trabalho de análise de fluxo de saudação;</span><span class="sxs-lookup"><span data-stu-id="1f739-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="1f739-251">consome dados de saudação Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1f739-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="1f739-252">executa uma junção com hello referência toomap Olá veículo VIN toohello correspondente modelo de dados</span><span class="sxs-lookup"><span data-stu-id="1f739-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="1f739-253">persisti-los no armazenamento de blobs do Azure para análise avançada em lote.</span><span class="sxs-lookup"><span data-stu-id="1f739-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="1f739-254">Olá consulta de análise de fluxo a seguir é usado toopersist Olá dados no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f739-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Consulta do trabalho do Stream Analytics para a ingestão de dados](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="1f739-256">*Figura 6 – Consulta do trabalho do Stream Analytics para a ingestão de dados*</span><span class="sxs-lookup"><span data-stu-id="1f739-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="1f739-257">Análise do lote</span><span class="sxs-lookup"><span data-stu-id="1f739-257">Batch analysis</span></span>
<span data-ttu-id="1f739-258">Também podemos gerar um volume adicional de sinais simulados do veículo e um conjunto de dados de diagnóstico para fazer uma análise de lote mais avançada.</span><span class="sxs-lookup"><span data-stu-id="1f739-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="1f739-259">Isso é necessário tooensure um volume de dados representativo para processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="1f739-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="1f739-260">Para essa finalidade, estamos usando um pipeline denominado "PrepareSampleDataPipeline" em toogenerate de fluxo de trabalho do Azure Data Factory Olá registros um ano de veículo simulada sinais e o conjunto de dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1f739-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="1f739-261">Clique em [atividade personalizada de fábrica de dados](http://go.microsoft.com/fwlink/?LinkId=717077) Olá toodownload atividade de DotNet fábrica de dados personalizada solução do Visual Studio para personalizações de acordo com suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="1f739-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Preparar os dados de exemplo para o fluxo de trabalho do processamento em lote](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="1f739-263">*Figura 7 – Preparar os dados de exemplo para o fluxo de trabalho do processamento em lote*</span><span class="sxs-lookup"><span data-stu-id="1f739-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="1f739-264">Olá pipeline consiste em um .net ADF personalizado atividade, mostrados aqui:</span><span class="sxs-lookup"><span data-stu-id="1f739-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="1f739-266">*Figura 8 – PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="1f739-267">Depois que o pipeline Olá for executado com êxito e "RawCarEventsTable" conjunto de dados está marcado como "Pronto", um ano vale a pena de veículo simulada sinais e diagnóstico dados são produzidos.</span><span class="sxs-lookup"><span data-stu-id="1f739-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="1f739-268">Veja a seguir Olá pastas e arquivos criados na sua conta de armazenamento no contêiner do "connectedcar" hello:</span><span class="sxs-lookup"><span data-stu-id="1f739-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Saída de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="1f739-270">*Figura 9 – Saída de PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="1f739-271">Referências</span><span class="sxs-lookup"><span data-stu-id="1f739-271">References</span></span>
[<span data-ttu-id="1f739-272">SDK do Hub de Eventos do Azure para ingestão de fluxo</span><span class="sxs-lookup"><span data-stu-id="1f739-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="1f739-273">[Recursos de movimentação de dados do Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Atividade DotNet do Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="1f739-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="1f739-274">Solução do Visual Studio de atividade DotNet do Azure Data Factory para preparação de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1f739-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="1f739-275">Conjunto de dados de saudação de partição</span><span class="sxs-lookup"><span data-stu-id="1f739-275">Partition hello dataset</span></span>
<span data-ttu-id="1f739-276">Olá bruto veículo semi-estruturados sinais e o conjunto de dados de diagnóstico são particionadas na etapa de preparação de dados Olá em um formato de ano/mês.</span><span class="sxs-lookup"><span data-stu-id="1f739-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="1f739-277">Esse particionamento promove a consulta mais eficiente e escalonável armazenamento de longo prazo, permitindo sobre falhas de um blob conta toohello próximo como conta primeiro Olá preenchido.</span><span class="sxs-lookup"><span data-stu-id="1f739-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="1f739-278">Esta etapa na solução de saudação é processamento toobatch somente aplicável.</span><span class="sxs-lookup"><span data-stu-id="1f739-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="1f739-279">Entrada e saída de gerenciamento de dados:</span><span class="sxs-lookup"><span data-stu-id="1f739-279">Input and output data data management:</span></span>

* <span data-ttu-id="1f739-280">Olá **dados de saída** (rotulado *PartitionedCarEventsTable*) é toobe mantida por um longo período de tempo como o formulário básico / "rawest" hello de dados "Data Lake" do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="1f739-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="1f739-281">Olá **dados de entrada** toothis pipeline normalmente seria descartada como dados de saída de saudação tem toohello fidelidade completa de entrada - apenas é armazenado (particionado) melhor para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="1f739-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Fluxo de trabalho de eventos de partição de carros](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="1f739-283">*Figura 10 – Fluxo de trabalho de eventos de partição de carros*</span><span class="sxs-lookup"><span data-stu-id="1f739-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="1f739-284">dados brutos de saudação são particionados usando uma atividade de HDInsight Hive em "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="1f739-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="1f739-285">dados de exemplo Hello gerados na etapa 1 para um ano são particionados por mês/ano.</span><span class="sxs-lookup"><span data-stu-id="1f739-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="1f739-286">as partições de Hello são usadas toogenerate veículo sinais e dados de diagnóstico para cada mês (total de 12 partições) de um ano.</span><span class="sxs-lookup"><span data-stu-id="1f739-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Atividade de PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="1f739-288">*Figura 11 – PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="1f739-289">***Script do Hive de PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="1f739-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="1f739-290">Hello seguinte script de Hive, chamado "partitioncarevents.hql", é usado para particionamento e está localizado na pasta de "\demo\src\connectedcar\scripts" hello do zip Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="1f739-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="1f739-291">Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f739-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Saída particionada](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="1f739-293">*Figura 12 – Saída Particionada*</span><span class="sxs-lookup"><span data-stu-id="1f739-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="1f739-294">dados de saudação agora é otimizado, é mais gerenciáveis e pronto para processamento adicional de informações de lote rich toogain.</span><span class="sxs-lookup"><span data-stu-id="1f739-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="1f739-295">Análise de Dados</span><span class="sxs-lookup"><span data-stu-id="1f739-295">Data Analysis</span></span>
<span data-ttu-id="1f739-296">Nesta seção, consulte como toocombine Stream Analytics do Azure, aprendizado de máquina do Azure, Azure Data Factory e do Azure HDInsight para rich avançado hábitos de análise de integridade de veículo e referências.</span><span class="sxs-lookup"><span data-stu-id="1f739-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="1f739-297">Há três subseções aqui:</span><span class="sxs-lookup"><span data-stu-id="1f739-297">There are three subsections here:</span></span>

1. <span data-ttu-id="1f739-298">**Aprendizado de máquina**: Esta subseção contém informações sobre a experiência de detecção de anomalias de saudação que foram usados em veículos de toopredict essa solução exigir a manutenção e veículos exigir recuperações devido a problemas de toosafety de manutenção.</span><span class="sxs-lookup"><span data-stu-id="1f739-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="1f739-299">**Análise em tempo real**: Esta subseção contém informações sobre análise de em tempo real hello usando Olá a linguagem de consulta do Stream Analytics e operacionalização de aprendizado de máquina Olá experiências em tempo real usando um aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="1f739-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="1f739-300">**Análise de lote**: Esta subseção contém informações relativas a saudação transformar e processamento de dados de lote hello usando HDInsight do Azure e aprendizado de máquina do Azure operacionalizada pela fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f739-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="1f739-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1f739-301">Machine Learning</span></span>
<span data-ttu-id="1f739-302">Nossa meta é veículos de saudação toopredict que exigem manutenção ou a recuperação baseada em determinadas estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="1f739-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="1f739-303">Fazemos Olá suposições a seguir</span><span class="sxs-lookup"><span data-stu-id="1f739-303">We make hello following assumptions</span></span>

* <span data-ttu-id="1f739-304">Se uma saudação três condições a seguir forem verdadeira, veículos Olá exigem **manutenção manutenção**:</span><span class="sxs-lookup"><span data-stu-id="1f739-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="1f739-305">A pressão do pneu está baixa</span><span class="sxs-lookup"><span data-stu-id="1f739-305">Tire pressure is low</span></span>
  * <span data-ttu-id="1f739-306">O nível de óleo do motor está baixo</span><span class="sxs-lookup"><span data-stu-id="1f739-306">Engine oil level is low</span></span>
  * <span data-ttu-id="1f739-307">A temperatura do motor está alta</span><span class="sxs-lookup"><span data-stu-id="1f739-307">Engine temperature is high</span></span>
* <span data-ttu-id="1f739-308">Se uma saudação seguintes condições forem verdadeira, veículos Olá podem ter um **problema de segurança** e exigem **recuperação**:</span><span class="sxs-lookup"><span data-stu-id="1f739-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="1f739-309">A temperatura do motor é alta, mas a temperatura externa é baixa</span><span class="sxs-lookup"><span data-stu-id="1f739-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="1f739-310">A temperatura do motor é baixa, mas a temperatura externa é alta</span><span class="sxs-lookup"><span data-stu-id="1f739-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="1f739-311">Com base nos requisitos de saudação anterior, nós criamos anomalias de toodetect dois modelos separados, um para detecção de manutenção de veículo e outra para detecção de recuperação do veículo.</span><span class="sxs-lookup"><span data-stu-id="1f739-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="1f739-312">Em ambos os esses modelos, algoritmo de análise de componente Principal (PCA) interno Olá é usado para detecção de anomalias.</span><span class="sxs-lookup"><span data-stu-id="1f739-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="1f739-313">**Modelo de detecção de manutenção**</span><span class="sxs-lookup"><span data-stu-id="1f739-313">**Maintenance detection model**</span></span>

<span data-ttu-id="1f739-314">Se um dos três indicadores pneu pressão, petróleo mecanismo ou temperatura mecanismo - satisfizer sua condição do respectiva, o modelo de detecção de manutenção de saudação relata uma anomalia.</span><span class="sxs-lookup"><span data-stu-id="1f739-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="1f739-315">Como resultado, precisamos apenas tooconsider essas três variáveis na criação de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="1f739-316">Em nossa experiência no aprendizado de máquina do Azure, primeiro usamos uma **selecionar colunas no conjunto de dados** tooextract módulo esses três variáveis.</span><span class="sxs-lookup"><span data-stu-id="1f739-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="1f739-317">Em seguida, usamos Olá anomalias com base em PCA detecção módulo toobuild Olá anomalias modelo de detecção.</span><span class="sxs-lookup"><span data-stu-id="1f739-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="1f739-318">Análise de componente principal (PCA) é uma técnica estabelecida no aprendizado de máquina que pode ser aplicadas toofeature detecção de anomalias, classificação e seleção.</span><span class="sxs-lookup"><span data-stu-id="1f739-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="1f739-319">O PCA converte um conjunto de casos contendo variáveis possivelmente correlacionadas em um conjunto de valores chamado de componentes principais.</span><span class="sxs-lookup"><span data-stu-id="1f739-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="1f739-320">a ideia chave Olá de modelagem com base em PCA é tooproject dados em um espaço menor dimensional para anomalias e recursos podem ser identificadas com mais facilidade.</span><span class="sxs-lookup"><span data-stu-id="1f739-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="1f739-321">Para cada nova entrada hello muito o modelo de detecção, detector de anomalias Olá primeiro calcula sua projeção de eigenvectors hello e, em seguida, calcula Olá normalizado erro reconstrução.</span><span class="sxs-lookup"><span data-stu-id="1f739-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="1f739-322">Esse erro normalizado é Olá anomalias.</span><span class="sxs-lookup"><span data-stu-id="1f739-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="1f739-323">Erro de saudação superior Olá, hello mais anormal Olá instância é.</span><span class="sxs-lookup"><span data-stu-id="1f739-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="1f739-324">Problema de detecção de manutenção hello, cada registro pode ser considerado como um ponto em um espaço de 3-dimensional definido pela pressão pneu, petróleo mecanismo e temperatura de mecanismo coordenadas.</span><span class="sxs-lookup"><span data-stu-id="1f739-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="1f739-325">toocapture essas anomalias, podemos pode dados de projeto Olá original no espaço de 3-dimensional de saudação para um espaço 2-dimensional usando PCA.</span><span class="sxs-lookup"><span data-stu-id="1f739-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="1f739-326">Assim, definimos o parâmetro hello número de componentes toouse em PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="1f739-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="1f739-327">Esse parâmetro desempenha um papel importante na aplicação da detecção de anomalias com base no PCA.</span><span class="sxs-lookup"><span data-stu-id="1f739-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="1f739-328">Depois de projetar os dados usando o PCA, podemos identificar essas anomalias mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="1f739-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="1f739-329">**Modelo de detecção de anomalias de recuperação** no modelo de detecção de anomalias de recuperação hello, usamos Olá selecionar colunas no conjunto de dados e de anomalias com base em PCA módulos de detecção de maneira semelhante.</span><span class="sxs-lookup"><span data-stu-id="1f739-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="1f739-330">Especificamente, podemos primeiro extrair a três variáveis - temperatura de mecanismo, temperatura externa e velocidade - usando Olá **selecionar colunas no conjunto de dados** módulo.</span><span class="sxs-lookup"><span data-stu-id="1f739-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="1f739-331">Também incluímos velocidade Olá variável desde que a temperatura do mecanismo de saudação normalmente está correlacionada toohello velocidade.</span><span class="sxs-lookup"><span data-stu-id="1f739-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="1f739-332">Em seguida, usamos a dados de saudação tooproject do módulo de detecção de anomalias com base em PCA de espaço de 3-dimensional Olá para um 2-dimensional.</span><span class="sxs-lookup"><span data-stu-id="1f739-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="1f739-333">Olá recuperação critérios são atendidos e então veículo Olá requer o Lembre-se quando a temperatura do mecanismo e temperatura fora altamente negativamente são correlacionadas.</span><span class="sxs-lookup"><span data-stu-id="1f739-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="1f739-334">Usando o algoritmo de detecção de anomalias com base em PCA, podemos capturar anomalias Olá depois de executar o PCA.</span><span class="sxs-lookup"><span data-stu-id="1f739-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="1f739-335">Quando o modelo de treinamento, precisamos de dados normal toouse, que não exigem manutenção ou lembre-se de que o modelo de detecção de anomalias com base em PCA Olá dados de entrada tootrain hello.</span><span class="sxs-lookup"><span data-stu-id="1f739-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="1f739-336">Olá experimento de pontuação, usamos toodetect de modelo de detecção de anomalias Olá treinado se veículo Olá exige manutenção ou lembre-se ou não.</span><span class="sxs-lookup"><span data-stu-id="1f739-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="1f739-337">Análise em tempo real</span><span class="sxs-lookup"><span data-stu-id="1f739-337">Real-time analysis</span></span>
<span data-ttu-id="1f739-338">saudação de consulta do Stream Analytics SQL a seguir é usada tooget média de saudação de todas as Olá parâmetros de veículo importantes, como velocidade de veículo, nível de combustível, temperatura de mecanismo, leitura do odômetro, pneu pressão, nível de petróleo mecanismo e outros.</span><span class="sxs-lookup"><span data-stu-id="1f739-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="1f739-339">médias Hello são usadas toodetect anomalias, emitir alertas e determinar Olá condições de integridade geral dos veículos operados na região específica e correlacioná-lo toodemographics.</span><span class="sxs-lookup"><span data-stu-id="1f739-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Consulta do Stream Analytics para o processamento em tempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="1f739-341">*Figura 13 – Consulta do Stream Analytics para o processamento em tempo real*</span><span class="sxs-lookup"><span data-stu-id="1f739-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="1f739-342">Todas as médias de saudação são calculadas em um TumblingWindow de 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="1f739-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="1f739-343">Estamos usando uma TubmlingWindow neste caso, pois exigimos intervalos de tempo que não se sobrepõem e são contínuos.</span><span class="sxs-lookup"><span data-stu-id="1f739-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="1f739-344">toolearn mais informações sobre todos os recursos de "Janelas" hello no Azure Stream Analytics, clique em [janelas (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f739-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="1f739-345">**Previsão em tempo real**</span><span class="sxs-lookup"><span data-stu-id="1f739-345">**Real-time prediction**</span></span>

<span data-ttu-id="1f739-346">Um aplicativo é incluído como parte do modelo de aprendizado de máquina solução toooperationalize Olá Olá em tempo real.</span><span class="sxs-lookup"><span data-stu-id="1f739-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="1f739-347">Este aplicativo chamado "RealTimeDashboardApp" é criado e configurado como parte da implantação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="1f739-348">aplicativo Hello executa seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1f739-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="1f739-349">Escuta tooan instância de Hub de eventos onde Stream Analytics é publicar Olá eventos em um padrão de continuamente.</span><span class="sxs-lookup"><span data-stu-id="1f739-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="1f739-350">![Consulta de análise de fluxo para publicar dados Olá](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figura 14 – a consulta do Stream Analytics para publicar Olá dados tooan instância de Hub de eventos de saída*</span><span class="sxs-lookup"><span data-stu-id="1f739-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="1f739-351">Para cada evento que esse aplicativo recebe:</span><span class="sxs-lookup"><span data-stu-id="1f739-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="1f739-352">Processos Olá dados usando o ponto de extremidade de pontuação de solicitação-resposta de aprendizado máquina (RR).</span><span class="sxs-lookup"><span data-stu-id="1f739-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="1f739-353">o ponto de extremidade do Hello RRS é automaticamente publicado como parte da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="1f739-354">a saída RRS Olá é o conjunto de dados do Power BI tooa publicado usando APIs de envio por push hello.</span><span class="sxs-lookup"><span data-stu-id="1f739-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="1f739-355">Esse padrão também é aplicável tooscenarios no qual você deseja toointegrate um aplicativo de linha de negócios (LoB) com o fluxo de análise em tempo real de hello, para cenários como alertas, notificações e mensagens.</span><span class="sxs-lookup"><span data-stu-id="1f739-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="1f739-356">Clique em [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) Olá toodownload solução RealtimeDashboardApp Visual Studio para personalizações.</span><span class="sxs-lookup"><span data-stu-id="1f739-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="1f739-357">**Olá tooexecute aplicativo de painel em tempo real**</span><span class="sxs-lookup"><span data-stu-id="1f739-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="1f739-358">Extrair e salvar localmente a ![Pasta RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figura 16 – Pasta RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="1f739-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="1f739-359">Execute o aplicativo hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="1f739-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="1f739-360">Forneça credenciais válidas do Power BI, entre e clique em Aceitar</span><span class="sxs-lookup"><span data-stu-id="1f739-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Aplicativo de painel em tempo real entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Aplicativo de painel em tempo real concluir entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="1f739-363">*Figura 17 – RealtimeDashboardApp: Entrar tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="1f739-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="1f739-364">Se desejar que o conjunto de dados tooflush Olá Power BI, execute Olá RealtimeDashboardApp com o parâmetro "flushdata" hello:</span><span class="sxs-lookup"><span data-stu-id="1f739-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="1f739-365">Análise do lote</span><span class="sxs-lookup"><span data-stu-id="1f739-365">Batch analysis</span></span>
<span data-ttu-id="1f739-366">Olá meta é tooshow como Contoso motores utiliza Olá computação do Azure recursos tooharness grandes dados toogain informações valiosas definir padrão, o comportamento de uso e integridade de veículo.</span><span class="sxs-lookup"><span data-stu-id="1f739-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="1f739-367">Isso possibilita:</span><span class="sxs-lookup"><span data-stu-id="1f739-367">This makes it possible to:</span></span>

* <span data-ttu-id="1f739-368">Melhorar a experiência do cliente hello e torná-lo mais barato, fornecendo informações sobre orientando hábitos e comportamentos de um eficiente de combustível</span><span class="sxs-lookup"><span data-stu-id="1f739-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="1f739-369">Saiba proativamente sobre clientes e suas decisões de negócios toogovern padrões de carro e fornecer Olá melhor na classe produtos e serviços</span><span class="sxs-lookup"><span data-stu-id="1f739-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="1f739-370">Nesta solução, pretendemos Olá métricas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f739-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="1f739-371">**Agressivo orientando comportamento**: identifica a tendência de saudação do hello modelos, locais, condições de referências e tempo de informações de toogain ano Olá nos padrões de um agressivas.</span><span class="sxs-lookup"><span data-stu-id="1f739-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="1f739-372">A Contoso Motors pode usar essas informações para campanhas de marketing, orientando novos recursos personalizados e seguro baseado em uso.</span><span class="sxs-lookup"><span data-stu-id="1f739-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="1f739-373">**Comportamento de um eficiente de combustível**: identifica a tendência de saudação do hello modelos, locais, condições de carro e tempo de saudação ano toogain visões e padrões de um eficiente de combustível.</span><span class="sxs-lookup"><span data-stu-id="1f739-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="1f739-374">Motores Contoso pode usar essas informações para campanhas de marketing orienta a novos recursos e pró-ativo drivers toohello reporting para custam efetivo e ambiente hábitos de carro amigáveis.</span><span class="sxs-lookup"><span data-stu-id="1f739-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="1f739-375">**Lembre-se de modelos**: identifica os modelos que exigem recuperações por operacionalização experiência de aprendizado de máquina de detecção de anomalias de saudação</span><span class="sxs-lookup"><span data-stu-id="1f739-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="1f739-376">Vamos dar uma olhada nos detalhes de saudação de cada uma dessas métricas</span><span class="sxs-lookup"><span data-stu-id="1f739-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="1f739-377">**Padrão de condução agressiva**</span><span class="sxs-lookup"><span data-stu-id="1f739-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="1f739-378">Olá particionado veículo sinais e dados de diagnóstico são processados no pipeline de saudação denominado "AggresiveDrivingPatternPipeline" usando modelos de saudação do Hive toodetermine, local, vehicle, gerando condições e outros parâmetros que exibe agressivo um padrão.</span><span class="sxs-lookup"><span data-stu-id="1f739-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="1f739-379">![Fluxo de trabalho de padrão de condução agressiva](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figura 18 – Fluxo de trabalho de padrão de condução agressiva*</span><span class="sxs-lookup"><span data-stu-id="1f739-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="1f739-380">***Consulta do Hive do padrão de condução agressiva***</span><span class="sxs-lookup"><span data-stu-id="1f739-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="1f739-381">Olá script de Hive chamado "aggresivedriving.hql" usado para analisar agressiva um padrão de condição está localizado na pasta "\demo\src\connectedcar\scripts" do zip Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="1f739-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="1f739-382">Ela usa a combinação de saudação da veículo posição de engrenagem de transmissão, freio pedais status e velocidade toodetect precipitado/agressiva orientando comportamento com base no modelo padrão em alta velocidade.</span><span class="sxs-lookup"><span data-stu-id="1f739-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="1f739-383">Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f739-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Saída do AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="1f739-385">*Figura 19 – Saída do AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="1f739-386">**Padrão de condução para a eficiência do combustível**</span><span class="sxs-lookup"><span data-stu-id="1f739-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="1f739-387">Olá particionado veículo sinais e dados de diagnóstico são processados no pipeline de saudação denominado "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="1f739-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="1f739-388">Hive é usado toodetermine Olá modelos, local, veículo, condições uma e outras propriedades que apresentam o padrão de um eficiente combustível.</span><span class="sxs-lookup"><span data-stu-id="1f739-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Padrão de condução para a eficiência do combustível](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="1f739-390">*Figura 20 – Fluxo de trabalho do padrão de condução para a eficiência do combustível*</span><span class="sxs-lookup"><span data-stu-id="1f739-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="1f739-391">***Consulta do Hive do padrão de condução para a eficiência do combustível***</span><span class="sxs-lookup"><span data-stu-id="1f739-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="1f739-392">Olá script de Hive chamado "fuelefficientdriving.hql" usado para analisar agressiva um padrão de condição está localizado na pasta "\demo\src\connectedcar\scripts" do zip Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="1f739-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="1f739-393">Ele usa a combinação de saudação de posição de engrenagem de transmissão do veículo, status pedais freio, velocidade e combustível de toodetect posição pedais de acelerador comportamento um eficiente com base em aceleração, modelo, e acelerar padrões.</span><span class="sxs-lookup"><span data-stu-id="1f739-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="1f739-394">Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f739-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Saída do FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="1f739-396">*Figura 21 – Saída do FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="1f739-397">**Previsões do Recall**</span><span class="sxs-lookup"><span data-stu-id="1f739-397">**Recall Predictions**</span></span>

<span data-ttu-id="1f739-398">experiência de aprendizado de máquina de saudação é provisionada e publicada como um serviço web como parte da implantação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="1f739-399">ponto de extremidade de pontuação de lote de saudação é utilizado nesse fluxo de trabalho, registrado como um serviço vinculado de fábrica de dados e operacionalizada usando a atividade de pontuação de lote de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="1f739-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Ponto de extremidade de Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="1f739-401">*Figura 22 – Ponto de extremidade do Machine Learning registrado como um serviço vinculado no data factory*</span><span class="sxs-lookup"><span data-stu-id="1f739-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="1f739-402">Olá serviço vinculado registrado é usado nos Olá DetectAnomalyPipeline tooscore Olá dados usando o modelo de detecção de anomalias de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Atividade de pontuação em lote do Machine Learning no data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="1f739-404">*Figura 23 – Atividade de pontuação em lote do Azure Machine Learning no data factory*</span><span class="sxs-lookup"><span data-stu-id="1f739-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="1f739-405">Há algumas etapas executadas nesse pipeline para preparação de dados para que ele pode ser operacionalizado com o serviço web de pontuação de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline para prever os veículos que exigem recalls](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="1f739-407">*Figura 24 – DetectAnomalyPipeline para prever os veículos que exigem recalls*</span><span class="sxs-lookup"><span data-stu-id="1f739-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="1f739-408">***Consulta do Hive para detecção de anomalias***</span><span class="sxs-lookup"><span data-stu-id="1f739-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="1f739-409">Depois de saudação de pontuação é concluída, uma atividade de HDInsight é tooprocess usados e os dados de agregação Olá categorizadas como anomalias pelo modelo de saudação com uma pontuação de probabilidade de 0,60 ou superior.</span><span class="sxs-lookup"><span data-stu-id="1f739-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="1f739-410">Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f739-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Saída de DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="1f739-412">*Figura 25 – Saída do DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="1f739-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="1f739-413">Publicar</span><span class="sxs-lookup"><span data-stu-id="1f739-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="1f739-414">Análise em tempo real</span><span class="sxs-lookup"><span data-stu-id="1f739-414">Real-time analysis</span></span>
<span data-ttu-id="1f739-415">Uma das consultas Olá no trabalho do Stream Analytics Olá publica saída de tooan eventos hello instância do Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f739-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Trabalho do Stream Analytics publica saída tooan instância de Hub de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="1f739-417">*Figura 26 – trabalho do Stream Analytics publica saída tooan instância de Hub de eventos*</span><span class="sxs-lookup"><span data-stu-id="1f739-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Instância do Hub de eventos de saída do Stream Analytics consulta toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="1f739-419">*Figura 27 – toohello de toopublish de consulta do Stream Analytics instância do Hub de eventos de saída*</span><span class="sxs-lookup"><span data-stu-id="1f739-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="1f739-420">Este fluxo de eventos é consumido pelos Olá que realtimedashboardapp incluído na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="1f739-421">Este aplicativo utiliza o serviço de web de aprendizado de máquina solicitação-resposta Olá para pontuação em tempo real e publica Olá dados resultantes tooa Power BI dataset para consumo.</span><span class="sxs-lookup"><span data-stu-id="1f739-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="1f739-422">Análise do lote</span><span class="sxs-lookup"><span data-stu-id="1f739-422">Batch analysis</span></span>
<span data-ttu-id="1f739-423">Olá resultados lote hello e processamento em tempo real são tabelas de banco de dados do Azure SQL toohello publicados para consumo.</span><span class="sxs-lookup"><span data-stu-id="1f739-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="1f739-424">Hello Azure SQL Server, o banco de dados e tabelas de saudação são criadas automaticamente como parte do script de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Fluxo de trabalho toodata mart de copiar resultados de processamento em lote](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="1f739-426">*Figura 28 – resultados copiar toodata mart fluxo de trabalho de processamento em lotes*</span><span class="sxs-lookup"><span data-stu-id="1f739-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Trabalho do Stream Analytics publica mart toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="1f739-428">*Figura 29 – trabalho do Stream Analytics publica mart toodata*</span><span class="sxs-lookup"><span data-stu-id="1f739-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Configuração do data mart no trabalho do Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="1f739-430">*Figura 30 – Configuração do data mart no trabalho do Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="1f739-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="1f739-431">Consumir</span><span class="sxs-lookup"><span data-stu-id="1f739-431">Consume</span></span>
<span data-ttu-id="1f739-432">O PowerBI fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="1f739-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="1f739-433">Clique aqui para obter instruções detalhadas sobre como configurar relatórios do Power BI hello e painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f739-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="1f739-434">painel final Olá tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="1f739-434">hello final dashboard looks like this:</span></span>

![Painel do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="1f739-436">*Figura 31 – Painel do Power BI*</span><span class="sxs-lookup"><span data-stu-id="1f739-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="1f739-437">Resumo</span><span class="sxs-lookup"><span data-stu-id="1f739-437">Summary</span></span>
<span data-ttu-id="1f739-438">Este documento contém um detalhamento de saudação veículo solução de análise de telemetria.</span><span class="sxs-lookup"><span data-stu-id="1f739-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="1f739-439">Isto apresenta um padrão de arquitetura lambda para a análise em tempo real e em lote com previsões e ações.</span><span class="sxs-lookup"><span data-stu-id="1f739-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="1f739-440">Esse padrão se aplica a tooa ampla variedade de casos de uso que exigem o afunilamento (em tempo real) e análise de caminho frio (em lotes).</span><span class="sxs-lookup"><span data-stu-id="1f739-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

