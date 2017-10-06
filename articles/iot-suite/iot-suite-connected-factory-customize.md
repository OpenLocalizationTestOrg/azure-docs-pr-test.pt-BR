---
title: "aaaCustomize Azure IoT Suite conectado fábrica | Microsoft Docs"
description: "Uma descrição de como o comportamento de saudação toocustomize de saudação conectadas fábrica pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="09e2e-103">Personalizar como Olá conectadas fábrica solução exibe dados de seus servidores de OPC UA</span><span class="sxs-lookup"><span data-stu-id="09e2e-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="09e2e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="09e2e-104">Introduction</span></span>

<span data-ttu-id="09e2e-105">Olá fábrica conectado solução agrega e exibe dados de saudação OPC UA servidores conectados toohello solução.</span><span class="sxs-lookup"><span data-stu-id="09e2e-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="09e2e-106">Você pode procurar e enviar comandos toohello OPC UA servidores em sua solução.</span><span class="sxs-lookup"><span data-stu-id="09e2e-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="09e2e-107">Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="09e2e-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="09e2e-108">Exemplos de dados agregados na solução Olá incluem hello eficiência geral de equipamentos (OEE) e indicadores chave de desempenho (KPIs) que você pode exibir no painel de saudação na fábrica de saudação, linha e níveis de estação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="09e2e-109">Olá, seguinte captura de tela mostra valores OEE e KPI Olá Olá **Assembly** estação, na **produção linha 1**, em Olá **Munique** fábrica:</span><span class="sxs-lookup"><span data-stu-id="09e2e-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Exemplo de valores OEE e um KPI na solução Olá][img-oee-kpi]

<span data-ttu-id="09e2e-111">ativa a solução Olá tooview você obter informações de itens de dados específicos do hello servidores OPC UA, chamados *estações*.</span><span class="sxs-lookup"><span data-stu-id="09e2e-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="09e2e-112">Olá seguinte captura de tela mostra gráficos do número de saudação de itens fabricados de uma estação específico:</span><span class="sxs-lookup"><span data-stu-id="09e2e-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Gráficos de número de itens fabricados][img-manufactured-items]

<span data-ttu-id="09e2e-114">Se você clicar em um dos gráficos Olá, você pode explorar dados Olá ainda mais usando Insights de série de tempo (TSI):</span><span class="sxs-lookup"><span data-stu-id="09e2e-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Explorar dados usando o Time Series Insights][img-tsi]

<span data-ttu-id="09e2e-116">Este artigo descreve:</span><span class="sxs-lookup"><span data-stu-id="09e2e-116">This article describes:</span></span>

- <span data-ttu-id="09e2e-117">Como dados saudação são feita a toohello disponível em vários modos de exibição na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="09e2e-118">Como você pode personalizar a solução de saudação de maneira Olá exibe dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="09e2e-119">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="09e2e-119">Data sources</span></span>

<span data-ttu-id="09e2e-120">Olá fábrica conectado solução exibe dados de saudação OPC UA servidores conectados toohello solução.</span><span class="sxs-lookup"><span data-stu-id="09e2e-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="09e2e-121">instalação de padrão de saudação inclui vários servidores de OPC UA executando uma simulação de fábrica.</span><span class="sxs-lookup"><span data-stu-id="09e2e-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="09e2e-122">Você pode adicionar seus próprios servidores OPC UA que [se conectar por meio de um gateway] [ lnk-connect-cf] tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="09e2e-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="09e2e-123">Você pode procurar itens de dados de saudação que um servidor conectado de OPC UA pode enviar tooyour solução no painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="09e2e-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="09e2e-124">Navegue toohello **selecionar um servidor de OPC UA** exibição:</span><span class="sxs-lookup"><span data-stu-id="09e2e-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Navegue toohello selecione um modo de exibição do servidor de OPC UA][img-select-server]

1. <span data-ttu-id="09e2e-126">Selecione um servidor e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="09e2e-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="09e2e-127">Clique em **continuar** quando o aviso de segurança de saudação aparece.</span><span class="sxs-lookup"><span data-stu-id="09e2e-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="09e2e-128">Este aviso só aparecerá uma vez para cada servidor e estabelece uma relação de confiança entre o painel de solução hello e servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="09e2e-129">Você pode agora itens de dados do hello procurar Olá servidor podem enviar toohello solução.</span><span class="sxs-lookup"><span data-stu-id="09e2e-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="09e2e-130">Os itens que estão sendo enviados toohello solução tem uma marca de seleção verde:</span><span class="sxs-lookup"><span data-stu-id="09e2e-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Itens publicados][img-published]

1. <span data-ttu-id="09e2e-132">Se você for um *administrador* solução hello, você pode escolher toopublish um toomake de item de dados disponível em Olá conectado a solução de fábrica.</span><span class="sxs-lookup"><span data-stu-id="09e2e-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="09e2e-133">Como administrador, também pode alterar o valor de saudação de itens de dados e chamar métodos em Olá servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="09e2e-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="09e2e-134">Dados de saudação do mapa</span><span class="sxs-lookup"><span data-stu-id="09e2e-134">Map hello data</span></span>

<span data-ttu-id="09e2e-135">Olá conectado mapas de solução de fábrica e Olá agregações itens de dados publicados de saudação OPC UA server toohello várias exibições em solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="09e2e-136">Olá fábrica conectado solução implanta tooyour conta do Azure quando você provisiona solução hello.</span><span class="sxs-lookup"><span data-stu-id="09e2e-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="09e2e-137">Um arquivo JSON em Olá solução do Visual Studio conectado fábrica armazena essas informações de mapeamento.</span><span class="sxs-lookup"><span data-stu-id="09e2e-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="09e2e-138">Você pode exibir e modificar esse arquivo de configuração JSON Olá conectado fábrica solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09e2e-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="09e2e-139">Você pode reutilizar a solução Olá depois que você fizer uma alteração.</span><span class="sxs-lookup"><span data-stu-id="09e2e-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="09e2e-140">Você pode usar o arquivo de configuração de saudação para:</span><span class="sxs-lookup"><span data-stu-id="09e2e-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="09e2e-141">Edite saudação fábricas de simulada existente, as linhas de produção e estações.</span><span class="sxs-lookup"><span data-stu-id="09e2e-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="09e2e-142">Mapear dados de servidores de OPC UA reais que você se conectar a solução toohello.</span><span class="sxs-lookup"><span data-stu-id="09e2e-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="09e2e-143">tooclone uma cópia da saudação conectado a solução do Visual Studio de fábrica, use Olá git comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="09e2e-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="09e2e-144">arquivo Hello **ContosoTopologyDescription.json** define Olá mapeamento da saudação dados do servidor de OPC UA itens toohello exibições no painel de solução de fábrica conectado hello.</span><span class="sxs-lookup"><span data-stu-id="09e2e-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="09e2e-145">Você pode encontrar esse arquivo de configuração no hello **Contoso\Topology** pasta Olá **WebApp** projeto no hello solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09e2e-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="09e2e-146">conteúdo de saudação do arquivo JSON de saudação é organizado como uma hierarquia de fábrica, linha de produção e os nós de estação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="09e2e-147">Essa hierarquia define a hierarquia de navegação de saudação no painel de fábrica conectado hello.</span><span class="sxs-lookup"><span data-stu-id="09e2e-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="09e2e-148">Os valores em cada nó de hierarquia Olá determinam informações de Olá exibidas no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="09e2e-149">Por exemplo, o arquivo JSON de saudação contém Olá Olá fábrica Munique valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="09e2e-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="09e2e-150">local, a descrição e o nome da saudação aparecem nesta exibição no painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="09e2e-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Dados de Munique no painel de saudação][img-munich]

<span data-ttu-id="09e2e-152">Cada fábrica, linha de produção e estação tem uma propriedade de imagem.</span><span class="sxs-lookup"><span data-stu-id="09e2e-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="09e2e-153">Você pode encontrar esses arquivos JPEG em Olá **Content\img** pasta Olá **WebApp** projeto.</span><span class="sxs-lookup"><span data-stu-id="09e2e-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="09e2e-154">Esses arquivos de imagem exibem no painel de fábrica conectado de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="09e2e-155">Cada estação inclui várias propriedades detalhadas que definem Olá mapeamento da saudação OPC UA itens de dados.</span><span class="sxs-lookup"><span data-stu-id="09e2e-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="09e2e-156">Essas propriedades são descritas Olá seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="09e2e-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="09e2e-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="09e2e-157">OpcUri</span></span>

<span data-ttu-id="09e2e-158">Olá **OpcUri** valor é hello OPC UA aplicativo URI que identifica exclusivamente a saudação servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="09e2e-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="09e2e-159">Por exemplo, Olá **OpcUri** valor de estação de assembly hello na linha de produção 1 em Munique semelhante ao seguinte Olá: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="09e2e-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="09e2e-160">Você pode exibir hello URIs de saudação conectada OPC UA servidores no painel de solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="09e2e-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Exibir URIs do servidor OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="09e2e-162">Simulação</span><span class="sxs-lookup"><span data-stu-id="09e2e-162">Simulation</span></span>

<span data-ttu-id="09e2e-163">Olá informações Olá **simulação** nó é específico toohello simulação OPC UA que é executado no hello servidores OPC UA provisionados por padrão.</span><span class="sxs-lookup"><span data-stu-id="09e2e-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="09e2e-164">Ele não é usado para um servidor OPC UA real.</span><span class="sxs-lookup"><span data-stu-id="09e2e-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="09e2e-165">Kpi1 e Kpi2</span><span class="sxs-lookup"><span data-stu-id="09e2e-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="09e2e-166">Esses nós descrevem como dados de estação Olá contribuem toohello dois valores KPI no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="09e2e-167">Em uma implantação padrão, esses valores de KPI são unidades por hora e kWh por hora.</span><span class="sxs-lookup"><span data-stu-id="09e2e-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="09e2e-168">solução de saudação calcula os valores KPI no nível de saudação de uma estação e agrega-los na linha de produção de hello e níveis de fábrica.</span><span class="sxs-lookup"><span data-stu-id="09e2e-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="09e2e-169">Cada KPI tem um valor mínimo, máximo e de destino.</span><span class="sxs-lookup"><span data-stu-id="09e2e-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="09e2e-170">Cada valor KPI também pode definir ações de alerta para tooperform de solução de fábrica Olá conectado.</span><span class="sxs-lookup"><span data-stu-id="09e2e-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="09e2e-171">Olá trecho a seguir mostra definições de KPI Olá para a estação de assembly hello na linha de produção 1 em Munique:</span><span class="sxs-lookup"><span data-stu-id="09e2e-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="09e2e-172">Olá seguinte captura de tela mostra dados KPI de saudação no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Informações de KPI no painel de saudação][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="09e2e-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="09e2e-174">OpcNodes</span></span>

<span data-ttu-id="09e2e-175">Olá **OpcNodes** identificam nós Olá itens de dados publicados de saudação servidor OPC UA e especificar como tooprocess esses dados.</span><span class="sxs-lookup"><span data-stu-id="09e2e-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="09e2e-176">Olá **NodeId** valor identifica Olá NodeID de UA OPC específico de saudação servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="09e2e-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="09e2e-177">primeiro nó Olá na estação de assembly Olá para a linha de produção 1 em Munique tem um valor **ns = 2; i = 385**.</span><span class="sxs-lookup"><span data-stu-id="09e2e-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="09e2e-178">Um **NodeId** valor especifica Olá tooread de item de dados de saudação servidor OPC UA e hello **SymbolicName** fornece toouse um nome amigável de usuário no painel de saudação para os dados.</span><span class="sxs-lookup"><span data-stu-id="09e2e-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="09e2e-179">Outros valores associados a cada nó são resumidos na Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="09e2e-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="09e2e-180">Valor</span><span class="sxs-lookup"><span data-stu-id="09e2e-180">Value</span></span> | <span data-ttu-id="09e2e-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="09e2e-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="09e2e-182">Relevância</span><span class="sxs-lookup"><span data-stu-id="09e2e-182">Relevance</span></span>  | <span data-ttu-id="09e2e-183">os valores KPI e OEE Olá esses dados contribuem para.</span><span class="sxs-lookup"><span data-stu-id="09e2e-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="09e2e-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="09e2e-184">OpCode</span></span>     | <span data-ttu-id="09e2e-185">Como os dados de saudação são agregados.</span><span class="sxs-lookup"><span data-stu-id="09e2e-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="09e2e-186">Unidades</span><span class="sxs-lookup"><span data-stu-id="09e2e-186">Units</span></span>      | <span data-ttu-id="09e2e-187">Olá unidades toouse, no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="09e2e-188">Visible</span><span class="sxs-lookup"><span data-stu-id="09e2e-188">Visible</span></span>    | <span data-ttu-id="09e2e-189">Se toodisplay este valor no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="09e2e-190">Alguns valores são usados em cálculos, mas não são exibidos.</span><span class="sxs-lookup"><span data-stu-id="09e2e-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="09e2e-191">Máximo</span><span class="sxs-lookup"><span data-stu-id="09e2e-191">Maximum</span></span>    | <span data-ttu-id="09e2e-192">valor máximo Olá que dispara um alerta no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="09e2e-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="09e2e-193">MaximumAlertActions</span></span> | <span data-ttu-id="09e2e-194">Tootake uma ação no alerta de tooan de resposta.</span><span class="sxs-lookup"><span data-stu-id="09e2e-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="09e2e-195">Por exemplo, envie uma estação de tooa do comando.</span><span class="sxs-lookup"><span data-stu-id="09e2e-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="09e2e-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="09e2e-196">ConstValue</span></span> | <span data-ttu-id="09e2e-197">Um valor constante usado em um cálculo.</span><span class="sxs-lookup"><span data-stu-id="09e2e-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="09e2e-198">Implantar alterações Olá</span><span class="sxs-lookup"><span data-stu-id="09e2e-198">Deploy hello changes</span></span>

<span data-ttu-id="09e2e-199">Quando terminar de fazer alterações toohello **ContosoTopologyDescription.json** arquivo, você deve reimplantar Olá conectado fábrica solução tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="09e2e-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="09e2e-200">Olá **azure iot-conectado-fábrica** repositório inclui um **build.ps1** script do PowerShell, você pode usar toorebuild e implantar a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e2e-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e2e-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09e2e-201">Next Steps</span></span>

<span data-ttu-id="09e2e-202">Saiba mais sobre solução de fábrica pré-configurado de saudação conectada por Olá ler artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="09e2e-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="09e2e-203">[Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="09e2e-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="09e2e-204">[Implantar um gateway para a fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="09e2e-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="09e2e-205">[Permissões no site de azureiotsuite.com Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="09e2e-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="09e2e-206">Perguntas frequentes do factory conectado</span><span class="sxs-lookup"><span data-stu-id="09e2e-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="09e2e-207">[Perguntas frequentes][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="09e2e-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md