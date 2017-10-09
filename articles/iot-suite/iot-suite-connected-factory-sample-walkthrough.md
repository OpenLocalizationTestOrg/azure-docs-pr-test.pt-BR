---
title: "passo a passo do aaaConnected fábrica Azure IoT Suite solução | Microsoft Docs"
description: "Uma descrição do hello Azure IoT pré-configurado solução conectados fábrica e sua arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="3d2bd-103">Passo a passo de solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="3d2bd-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="3d2bd-104">Olá IoT Suite conectado fábrica [pré-configurado solução] [ lnk-preconfigured-solutions] é uma implementação de uma solução de ponta a ponta industrial que:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="3d2bd-105">Conecta-se tooboth simulado industrial dispositivos que executam o OPC UA servidores em linhas de produção de fábrica simulada e dispositivos de servidor de OPC UA reais.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="3d2bd-106">Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3d2bd-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="3d2bd-107">Mostra KPIs operacionais e OEE desses dispositivos e de linhas de produção.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="3d2bd-108">Demonstra como um aplicativo baseado em nuvem pode ser usado toointeract com sistemas de servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="3d2bd-109">Permite que você tooconnect seus próprios dispositivos de servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="3d2bd-110">Permite que você toobrowse e modificar Olá dados do servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="3d2bd-111">Integra-se com hello Azure tempo série Insights (TSI) serviço tooprovide exibições personalizadas de dados de saudação de seus servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="3d2bd-112">Você pode usar a solução hello como ponto de partida para sua própria implementação e [personalizar] [ lnk-customize] -toomeet seus próprios requisitos comerciais específicos.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="3d2bd-113">Este artigo o orienta por meio de alguns dos elementos-chave Olá Olá conectado fábrica solução tooenable toounderstand como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="3d2bd-114">Esse conhecimento ajuda a:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="3d2bd-115">Solucione problemas na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="3d2bd-116">Planejar como toocustomize toohello solução toomeet necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="3d2bd-117">Criar sua própria solução IoT que usa os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="3d2bd-118">Para obter mais informações, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3d2bd-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="3d2bd-119">Arquitetura lógica</span><span class="sxs-lookup"><span data-stu-id="3d2bd-119">Logical architecture</span></span>

<span data-ttu-id="3d2bd-120">Olá diagrama a seguir descreve os componentes lógicos de saudação da solução Olá pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Arquitetura lógica de fábrica conectada][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="3d2bd-122">Padrões de comunicação</span><span class="sxs-lookup"><span data-stu-id="3d2bd-122">Communication patterns</span></span>

<span data-ttu-id="3d2bd-123">solução de saudação usa Olá [especificação OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT de dados de telemetria OPC UA Hub no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="3d2bd-124">solução de saudação usa Olá [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT borda para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="3d2bd-125">solução de saudação também tem um cliente de OPC UA integrado a um aplicativo web que pode estabelecer conexões com servidores OPC UA locais.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="3d2bd-126">Olá cliente usa um [proxy reverso](https://wikipedia.org/wiki/Reverse_proxy) e receber ajuda de conexão do IoT Hub toomake Olá sem a necessidade de abrir portas no firewall de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="3d2bd-127">Esse padrão de comunicação é chamado de [comunicação auxiliada por serviço](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="3d2bd-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="3d2bd-128">solução de saudação usa Olá [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT borda para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="3d2bd-129">Simulação</span><span class="sxs-lookup"><span data-stu-id="3d2bd-129">Simulation</span></span>

<span data-ttu-id="3d2bd-130">Olá simulados estações e execução de produção de hello simulado sistemas (MES) formam uma linha de produção de fábrica.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="3d2bd-131">Hello dispositivos simulados e hello OPC publicador módulo baseiam Olá [OPC UA .NET padrão] [ lnk-OPC-UA-NET-Standard] publicado por Olá OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="3d2bd-132">Olá OPC Proxy e o publicador de OPC são implementados como módulos com base em [Azure IoT borda][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="3d2bd-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="3d2bd-133">Cada linha de produção simulada tem um gateway designado anexado.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="3d2bd-134">Todos os componentes de simulação executados em contêineres Docker hospedados em uma VM do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="3d2bd-135">simulação de saudação é configurado toorun oito simulada linhas de produção por padrão.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="3d2bd-136">Linha de produção simulada</span><span class="sxs-lookup"><span data-stu-id="3d2bd-136">Simulated production line</span></span>

<span data-ttu-id="3d2bd-137">Uma linha de produção fabrica peças.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-137">A production line manufactures parts.</span></span> <span data-ttu-id="3d2bd-138">É composto de estações diferentes: uma estação de assembly, uma de teste e uma de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="3d2bd-139">simulação de saudação é executado e atualiza os dados de saudação que são expostos por meio de nós OPC UA hello.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="3d2bd-140">Todas as estações de linha de produção simulada são gerenciadas pelo Olá MES por meio de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="3d2bd-141">Sistema de execução de fabricação simulado</span><span class="sxs-lookup"><span data-stu-id="3d2bd-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="3d2bd-142">Olá MES monitora cada estação na linha de produção de hello por meio de alterações de status do OPC UA toodetect estação.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="3d2bd-143">Ele chama OPC UA estações do métodos toocontrol hello e passa um produto de uma estação toohello lado até que ela seja concluída.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="3d2bd-144">Módulo de editor de gateway OPC</span><span class="sxs-lookup"><span data-stu-id="3d2bd-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="3d2bd-145">Módulo de publicador OPC conecta toohello estação OPC UA servidores e assina toohello OPC nós toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="3d2bd-146">módulo de saudação converte dados de nó de saudação em formato JSON, criptografa e envia tooIoT Hub como mensagens de OPC UA Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="3d2bd-147">módulo de OPC publicador Olá apenas exige uma porta de saída https (443) e pode trabalhar com a infraestrutura existente do enterprise.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="3d2bd-148">Módulo de proxy de gateway OPC</span><span class="sxs-lookup"><span data-stu-id="3d2bd-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="3d2bd-149">Olá Gateway OPC UA Proxy módulo túneis de mensagens de comando e controle de OPC UA binárias e requer apenas uma porta de saída https (443).</span><span class="sxs-lookup"><span data-stu-id="3d2bd-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="3d2bd-150">Pode funcionar com a infraestrutura existente da empresa, inclusive Proxies da Web.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="3d2bd-151">Ele usa dados do dispositivo do Hub IoT métodos tootransfer colocadas em pacotes TCP/IP na camada de aplicativo hello e, portanto, garante a relação de confiança de ponto de extremidade, criptografia de dados e integridade usando SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="3d2bd-152">Olá protocolo binário de OPC UA retransmitido por meio do proxy de saudação em si usa criptografia e autenticação de assistência ao usuário.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="3d2bd-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="3d2bd-153">Azure Time Series Insights</span></span>

<span data-ttu-id="3d2bd-154">Olá Gateway OPC publicador módulo assina tooOPC UA servidor nós toodetect de alterações em valores de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="3d2bd-155">Se for detectada uma alteração de dados em um de nós hello, esse módulo envia mensagens tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="3d2bd-156">IoT Hub fornece uma fonte de evento tooAzure TSI.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="3d2bd-157">Armazena dados de TSI por 30 dias, com base em carimbos de hora anexado toohello mensagens.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="3d2bd-158">Os dados incluem:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-158">This data includes:</span></span>

* <span data-ttu-id="3d2bd-159">ApplicationUri UA OPC</span><span class="sxs-lookup"><span data-stu-id="3d2bd-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="3d2bd-160">NodeId UA OPC</span><span class="sxs-lookup"><span data-stu-id="3d2bd-160">OPC UA NodeId</span></span>
* <span data-ttu-id="3d2bd-161">Valor do nó de saudação</span><span class="sxs-lookup"><span data-stu-id="3d2bd-161">Value of hello node</span></span>
* <span data-ttu-id="3d2bd-162">Carimbo de data/hora de origem</span><span class="sxs-lookup"><span data-stu-id="3d2bd-162">Source timestamp</span></span>
* <span data-ttu-id="3d2bd-163">DisplayName UA OPC</span><span class="sxs-lookup"><span data-stu-id="3d2bd-163">OPC UA DisplayName</span></span>

<span data-ttu-id="3d2bd-164">Atualmente, TSI não permitem que os clientes desejarem dados Olá tookeep toocustomize quanto tempo.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="3d2bd-165">O TSI executa consultas em relação a dados de nó usando um SearchSpan (Time.From, Time.To) e agrega por OPC UA ApplicationUri, OPC UA NodeId ou OPC UA DisplayName.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="3d2bd-166">dados de saudação tooretrieve Olá OEE e um KPI, gráficos e medidores gráficos de série de tempo de saudação, dados são agregados por contagem de eventos, Sum, Avg, Min e Max.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="3d2bd-167">série de tempo de saudação é criado usando um processo diferente.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-167">hello time series are built using a different process.</span></span> <span data-ttu-id="3d2bd-168">OEE KPIs calculados do banco de dados de estação e são transferidos para a topologia de saudação (linhas de produção, fábricas, enterprise) no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="3d2bd-169">Além disso, a série temporal para a topologia OEE e um KPI é calculado no aplicativo hello, sempre que um período de tempo exibido está pronto.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="3d2bd-170">Por exemplo, modo de exibição de dia de saudação é atualizado a cada hora cheia.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="3d2bd-171">exibição de série de tempo de saudação de dados do nó vêm diretamente de TSI usando uma agregação para o período de tempo.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="3d2bd-172">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="3d2bd-172">IoT Hub</span></span>
<span data-ttu-id="3d2bd-173">Olá [hub IoT] [ lnk-IoT Hub] recebe os dados enviados do hello OPC publicador módulo em nuvem hello e facilita o serviço do Azure TSI toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="3d2bd-174">Olá IoT Hub na solução Olá também:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="3d2bd-175">Mantém um registro de identidade que armazena IDs Olá para todos os módulo de publicador OPC e todos os módulos de Proxy de OPC.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="3d2bd-176">É usado como o canal de transporte para a comunicação bidirecional de saudação OPC Proxy módulo.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="3d2bd-177">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3d2bd-177">Azure Storage</span></span>
<span data-ttu-id="3d2bd-178">solução de Olá usa o armazenamento de BLOBs do Azure como o armazenamento em disco para dados de implantação de VM e toostore hello.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="3d2bd-179">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3d2bd-179">Web app</span></span>
<span data-ttu-id="3d2bd-180">aplicativo web do Hello implantado como parte da solução Olá pré-configurado consiste de um cliente integrado de OPC UA, processamento de alertas e visualização de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3d2bd-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d2bd-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d2bd-181">Next steps</span></span>

<span data-ttu-id="3d2bd-182">Você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d2bd-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="3d2bd-183">[Permissões no site de azureiotsuite.com Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="3d2bd-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="3d2bd-184">Implantar um gateway no Windows ou Linux para solução de fábrica pré-configurado Olá conectado</span><span class="sxs-lookup"><span data-stu-id="3d2bd-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
