---
title: "Personalizar a fábrica conectada do Azure IoT Suite | Microsoft Docs"
description: "Uma descrição de como personalizar o comportamento da solução pré-configurada de fábrica conectada."
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
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="859d1-103">Personalizar como a solução de fábrica conectada exibe dados dos servidores OPC UA</span><span class="sxs-lookup"><span data-stu-id="859d1-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="859d1-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="859d1-104">Introduction</span></span>

<span data-ttu-id="859d1-105">A solução de fábrica conectada agrega e exibe dados dos servidores OPC UA conectados à solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="859d1-106">Você pode procurar e enviar comandos para os servidores OPC UA na solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="859d1-107">Para obter mais informações sobre o OPC UA, consulte as [Perguntas frequentes sobre fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="859d1-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="859d1-108">Exemplos de dados agregados na solução incluem a OEE (Eficiência Geral de Equipamentos) e os KPIs (Indicadores Chave de Desempenho) que podem ser exibidos no painel nos níveis da fábrica, da linha e da estação.</span><span class="sxs-lookup"><span data-stu-id="859d1-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="859d1-109">A captura de tela a seguir mostra os valores de OEE e KPI da estação **Assembly** na **Linha de produção 1**, na fábrica de **Munique**:</span><span class="sxs-lookup"><span data-stu-id="859d1-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Exemplo de valores de OEE e KPI na solução][img-oee-kpi]

<span data-ttu-id="859d1-111">A solução permite exibir informações detalhadas de itens de dados específicos dos servidores OPC UA, chamados *estações*.</span><span class="sxs-lookup"><span data-stu-id="859d1-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="859d1-112">A seguinte captura de tela mostra gráficos do número de itens fabricados de uma estação específica:</span><span class="sxs-lookup"><span data-stu-id="859d1-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Gráficos de número de itens fabricados][img-manufactured-items]

<span data-ttu-id="859d1-114">Se você clicar em um dos gráficos, poderá explorar os dados ainda mais usando o TSI (Time Series Insights):</span><span class="sxs-lookup"><span data-stu-id="859d1-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Explorar dados usando o Time Series Insights][img-tsi]

<span data-ttu-id="859d1-116">Este artigo descreve:</span><span class="sxs-lookup"><span data-stu-id="859d1-116">This article describes:</span></span>

- <span data-ttu-id="859d1-117">Como os dados são disponibilizados para as várias exibições da solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="859d1-118">Como você pode personalizar a maneira como a solução exibe os dados.</span><span class="sxs-lookup"><span data-stu-id="859d1-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="859d1-119">Fontes de dados</span><span class="sxs-lookup"><span data-stu-id="859d1-119">Data sources</span></span>

<span data-ttu-id="859d1-120">A solução de fábrica conectada exibe dados dos servidores OPC UA conectados à solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="859d1-121">A instalação padrão inclui vários servidores OPC UA que executam uma simulação de fábrica.</span><span class="sxs-lookup"><span data-stu-id="859d1-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="859d1-122">Você pode adicionar seus próprios servidores OPC UA que [se conectam por meio de um gateway][lnk-connect-cf] à solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="859d1-123">Você pode procurar itens de dados que um servidor OPC UA conectado pode enviar para a solução no painel:</span><span class="sxs-lookup"><span data-stu-id="859d1-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="859d1-124">Navegue para a exibição **Selecionar um servidor OPC UA**:</span><span class="sxs-lookup"><span data-stu-id="859d1-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Navegar para a exibição Selecionar um servidor OPC UA][img-select-server]

1. <span data-ttu-id="859d1-126">Selecione um servidor e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="859d1-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="859d1-127">Clique em **Continuar** quando o aviso de segurança for exibido.</span><span class="sxs-lookup"><span data-stu-id="859d1-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="859d1-128">Esse aviso só será exibido uma vez para cada servidor e estabelece uma relação de confiança entre o painel da solução e o servidor.</span><span class="sxs-lookup"><span data-stu-id="859d1-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="859d1-129">Agora você pode procurar itens de dados que o servidor pode enviar para a solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="859d1-130">Os itens que estão sendo enviados para a solução têm uma marca de seleção verde:</span><span class="sxs-lookup"><span data-stu-id="859d1-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Itens publicados][img-published]

1. <span data-ttu-id="859d1-132">Se você for um *Administrador* da solução, poderá optar por publicar um item de dados para disponibilizá-lo na solução de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="859d1-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="859d1-133">Como Administrador, você também pode alterar o valor de itens de dados e chamar métodos no servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="859d1-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="859d1-134">Mapear os dados</span><span class="sxs-lookup"><span data-stu-id="859d1-134">Map the data</span></span>

<span data-ttu-id="859d1-135">A solução de fábrica conectada mapeia e agrega os itens de dados publicados do servidor OPC UA nas várias exibições da solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="859d1-136">A solução de fábrica conectada é implantada em sua conta do Azure quando você provisiona a solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="859d1-137">Um arquivo JSON da solução de fábrica conectada do Visual Studio armazena essas informações de mapeamento.</span><span class="sxs-lookup"><span data-stu-id="859d1-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="859d1-138">Exiba e modifique esse arquivo de configuração JSON na solução de fábrica conectada do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="859d1-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="859d1-139">Você pode reimplantar a solução depois de fazer uma alteração.</span><span class="sxs-lookup"><span data-stu-id="859d1-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="859d1-140">Você pode usar o arquivo de configuração para:</span><span class="sxs-lookup"><span data-stu-id="859d1-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="859d1-141">Editar as fábricas simuladas, linhas de produção e estações existentes.</span><span class="sxs-lookup"><span data-stu-id="859d1-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="859d1-142">Mapear dados de servidores OPC UA reais que estão conectados à solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="859d1-143">Para clonar uma cópia da solução de fábrica conectada do Visual Studio, use o seguinte comando do Git:</span><span class="sxs-lookup"><span data-stu-id="859d1-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="859d1-144">O arquivo **ContosoTopologyDescription.json** define o mapeamento dos itens de dados do servidor OPC UA para as exibições no painel da solução de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="859d1-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="859d1-145">Encontre esse arquivo de configuração na pasta **Contoso\Topology** do projeto **WebApp** na solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="859d1-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="859d1-146">O conteúdo do arquivo JSON é organizado como uma hierarquia de nós de fábrica, linha de produção e estação.</span><span class="sxs-lookup"><span data-stu-id="859d1-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="859d1-147">Essa hierarquia define a hierarquia de navegação no painel da fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="859d1-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="859d1-148">Os valores em cada nó da hierarquia determinam as informações exibidas no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="859d1-149">Por exemplo, o arquivo JSON contém os seguintes valores para a fábrica de Munique:</span><span class="sxs-lookup"><span data-stu-id="859d1-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

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

<span data-ttu-id="859d1-150">O nome, a descrição e a localização aparecem nesta exibição no painel:</span><span class="sxs-lookup"><span data-stu-id="859d1-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Dados de Munique no painel][img-munich]

<span data-ttu-id="859d1-152">Cada fábrica, linha de produção e estação tem uma propriedade de imagem.</span><span class="sxs-lookup"><span data-stu-id="859d1-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="859d1-153">Encontre esses arquivos JPEG na pasta **Content\img** do projeto **WebApp**.</span><span class="sxs-lookup"><span data-stu-id="859d1-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="859d1-154">Esses arquivos de imagem são exibidos no painel da fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="859d1-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="859d1-155">Cada estação inclui várias propriedades detalhadas que definem o mapeamento dos itens de dados do OPC UA.</span><span class="sxs-lookup"><span data-stu-id="859d1-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="859d1-156">Essas propriedades são descritas nas seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="859d1-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="859d1-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="859d1-157">OpcUri</span></span>

<span data-ttu-id="859d1-158">O valor de **OpcUri** é o URI do Aplicativo do OPC UA que identifica exclusivamente o servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="859d1-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="859d1-159">Por exemplo, o valor de **OpcUri** da estação de assembly na linha de produção 1 em Munique tem esta aparência: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="859d1-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="859d1-160">Exiba os URIs dos servidores OPC UA conectados no painel da solução:</span><span class="sxs-lookup"><span data-stu-id="859d1-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Exibir URIs do servidor OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="859d1-162">Simulação</span><span class="sxs-lookup"><span data-stu-id="859d1-162">Simulation</span></span>

<span data-ttu-id="859d1-163">As informações do nó **Simulation** são específicas à simulação do OPC UA executada nos servidores do OPC UA provisionados por padrão.</span><span class="sxs-lookup"><span data-stu-id="859d1-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="859d1-164">Ele não é usado para um servidor OPC UA real.</span><span class="sxs-lookup"><span data-stu-id="859d1-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="859d1-165">Kpi1 e Kpi2</span><span class="sxs-lookup"><span data-stu-id="859d1-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="859d1-166">Esses nós descrevem como os dados da estação contribuem para os dois valores de KPI no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="859d1-167">Em uma implantação padrão, esses valores de KPI são unidades por hora e kWh por hora.</span><span class="sxs-lookup"><span data-stu-id="859d1-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="859d1-168">A solução calcula os valores de KPI no nível de uma estação e agrega-os nos níveis da fábrica e da linha de produção.</span><span class="sxs-lookup"><span data-stu-id="859d1-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="859d1-169">Cada KPI tem um valor mínimo, máximo e de destino.</span><span class="sxs-lookup"><span data-stu-id="859d1-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="859d1-170">Cada valor de KPI também pode definir ações de alerta a serem executados pela solução de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="859d1-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="859d1-171">O seguinte trecho mostra as definições de KPI para a estação de assembly na linha de produção 1 em Munique:</span><span class="sxs-lookup"><span data-stu-id="859d1-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="859d1-172">A captura de tela a seguir mostra os dados de KPI no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![Informações de KPI no painel][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="859d1-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="859d1-174">OpcNodes</span></span>

<span data-ttu-id="859d1-175">Os nós **OpcNodes** identificam os itens de dados publicados do servidor OPC UA e especificam como processar esses dados.</span><span class="sxs-lookup"><span data-stu-id="859d1-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="859d1-176">O valor de **NodeId** identifica a NodeID do OPC UA específica do servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="859d1-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="859d1-177">O primeiro nó da estação de assembly na linha de produção 1 em Munique tem um valor igual a **ns=2;i=385**.</span><span class="sxs-lookup"><span data-stu-id="859d1-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="859d1-178">Um valor de **NodeId** especifica o item de dados a ser lido do servidor OPC UA e **SymbolicName** fornece um nome amigável ao usuário ser usado no painel para os dados.</span><span class="sxs-lookup"><span data-stu-id="859d1-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="859d1-179">Outros valores associados a cada nó são resumidos na seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="859d1-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="859d1-180">Valor</span><span class="sxs-lookup"><span data-stu-id="859d1-180">Value</span></span> | <span data-ttu-id="859d1-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="859d1-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="859d1-182">Relevância</span><span class="sxs-lookup"><span data-stu-id="859d1-182">Relevance</span></span>  | <span data-ttu-id="859d1-183">Os valores de KPI e OEE com os quais esses dados contribuem.</span><span class="sxs-lookup"><span data-stu-id="859d1-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="859d1-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="859d1-184">OpCode</span></span>     | <span data-ttu-id="859d1-185">Como os dados são agregados.</span><span class="sxs-lookup"><span data-stu-id="859d1-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="859d1-186">Unidades</span><span class="sxs-lookup"><span data-stu-id="859d1-186">Units</span></span>      | <span data-ttu-id="859d1-187">As unidades a serem usadas no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="859d1-188">Visible</span><span class="sxs-lookup"><span data-stu-id="859d1-188">Visible</span></span>    | <span data-ttu-id="859d1-189">Indica se esse valor será exibido no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="859d1-190">Alguns valores são usados em cálculos, mas não são exibidos.</span><span class="sxs-lookup"><span data-stu-id="859d1-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="859d1-191">Máximo</span><span class="sxs-lookup"><span data-stu-id="859d1-191">Maximum</span></span>    | <span data-ttu-id="859d1-192">O valor máximo que dispara um alerta no painel.</span><span class="sxs-lookup"><span data-stu-id="859d1-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="859d1-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="859d1-193">MaximumAlertActions</span></span> | <span data-ttu-id="859d1-194">Uma ação a ser tomada em resposta a um alerta.</span><span class="sxs-lookup"><span data-stu-id="859d1-194">An action to take in response to an alert.</span></span> <span data-ttu-id="859d1-195">Por exemplo, enviar um comando para uma estação.</span><span class="sxs-lookup"><span data-stu-id="859d1-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="859d1-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="859d1-196">ConstValue</span></span> | <span data-ttu-id="859d1-197">Um valor constante usado em um cálculo.</span><span class="sxs-lookup"><span data-stu-id="859d1-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="859d1-198">Implantar as alterações</span><span class="sxs-lookup"><span data-stu-id="859d1-198">Deploy the changes</span></span>

<span data-ttu-id="859d1-199">Quando você terminar de fazer alterações no arquivo **ContosoTopologyDescription.json**, deverá reimplantar a solução de fábrica conectada à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="859d1-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="859d1-200">O repositório **azure-iot-connected-factory** inclui um script **build.ps1** do PowerShell que pode ser usado para recompilar e implantar a solução.</span><span class="sxs-lookup"><span data-stu-id="859d1-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859d1-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="859d1-201">Next Steps</span></span>

<span data-ttu-id="859d1-202">Saiba mais sobre a solução pré-configurada de fábrica conectada lendo os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="859d1-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="859d1-203">[Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="859d1-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="859d1-204">[Implantar um gateway para a fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="859d1-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="859d1-205">[Permissões no site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="859d1-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="859d1-206">Perguntas frequentes do factory conectado</span><span class="sxs-lookup"><span data-stu-id="859d1-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="859d1-207">[Perguntas frequentes][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="859d1-207">[FAQ][lnk-faq]</span></span>


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