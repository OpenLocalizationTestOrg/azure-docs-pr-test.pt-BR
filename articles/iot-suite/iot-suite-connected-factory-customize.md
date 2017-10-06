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
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a>Personalizar como Olá conectadas fábrica solução exibe dados de seus servidores de OPC UA

## <a name="introduction"></a>Introdução

Olá fábrica conectado solução agrega e exibe dados de saudação OPC UA servidores conectados toohello solução. Você pode procurar e enviar comandos toohello OPC UA servidores em sua solução. Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).

Exemplos de dados agregados na solução Olá incluem hello eficiência geral de equipamentos (OEE) e indicadores chave de desempenho (KPIs) que você pode exibir no painel de saudação na fábrica de saudação, linha e níveis de estação. Olá, seguinte captura de tela mostra valores OEE e KPI Olá Olá **Assembly** estação, na **produção linha 1**, em Olá **Munique** fábrica:

![Exemplo de valores OEE e um KPI na solução Olá][img-oee-kpi]

ativa a solução Olá tooview você obter informações de itens de dados específicos do hello servidores OPC UA, chamados *estações*. Olá seguinte captura de tela mostra gráficos do número de saudação de itens fabricados de uma estação específico:

![Gráficos de número de itens fabricados][img-manufactured-items]

Se você clicar em um dos gráficos Olá, você pode explorar dados Olá ainda mais usando Insights de série de tempo (TSI):

![Explorar dados usando o Time Series Insights][img-tsi]

Este artigo descreve:

- Como dados saudação são feita a toohello disponível em vários modos de exibição na solução de saudação.
- Como você pode personalizar a solução de saudação de maneira Olá exibe dados de saudação.

## <a name="data-sources"></a>Fontes de dados

Olá fábrica conectado solução exibe dados de saudação OPC UA servidores conectados toohello solução. instalação de padrão de saudação inclui vários servidores de OPC UA executando uma simulação de fábrica. Você pode adicionar seus próprios servidores OPC UA que [se conectar por meio de um gateway] [ lnk-connect-cf] tooyour solução.

Você pode procurar itens de dados de saudação que um servidor conectado de OPC UA pode enviar tooyour solução no painel de saudação:

1. Navegue toohello **selecionar um servidor de OPC UA** exibição:

    ![Navegue toohello selecione um modo de exibição do servidor de OPC UA][img-select-server]

1. Selecione um servidor e clique em **Conectar**. Clique em **continuar** quando o aviso de segurança de saudação aparece.

    > [!NOTE]
    > Este aviso só aparecerá uma vez para cada servidor e estabelece uma relação de confiança entre o painel de solução hello e servidor de saudação.

1. Você pode agora itens de dados do hello procurar Olá servidor podem enviar toohello solução. Os itens que estão sendo enviados toohello solução tem uma marca de seleção verde:

    ![Itens publicados][img-published]

1. Se você for um *administrador* solução hello, você pode escolher toopublish um toomake de item de dados disponível em Olá conectado a solução de fábrica. Como administrador, também pode alterar o valor de saudação de itens de dados e chamar métodos em Olá servidor OPC UA.

## <a name="map-hello-data"></a>Dados de saudação do mapa

Olá conectado mapas de solução de fábrica e Olá agregações itens de dados publicados de saudação OPC UA server toohello várias exibições em solução de saudação. Olá fábrica conectado solução implanta tooyour conta do Azure quando você provisiona solução hello. Um arquivo JSON em Olá solução do Visual Studio conectado fábrica armazena essas informações de mapeamento. Você pode exibir e modificar esse arquivo de configuração JSON Olá conectado fábrica solução do Visual Studio. Você pode reutilizar a solução Olá depois que você fizer uma alteração.

Você pode usar o arquivo de configuração de saudação para:

- Edite saudação fábricas de simulada existente, as linhas de produção e estações.
- Mapear dados de servidores de OPC UA reais que você se conectar a solução toohello.

tooclone uma cópia da saudação conectado a solução do Visual Studio de fábrica, use Olá git comando a seguir:

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

arquivo Hello **ContosoTopologyDescription.json** define Olá mapeamento da saudação dados do servidor de OPC UA itens toohello exibições no painel de solução de fábrica conectado hello. Você pode encontrar esse arquivo de configuração no hello **Contoso\Topology** pasta Olá **WebApp** projeto no hello solução do Visual Studio.

conteúdo de saudação do arquivo JSON de saudação é organizado como uma hierarquia de fábrica, linha de produção e os nós de estação. Essa hierarquia define a hierarquia de navegação de saudação no painel de fábrica conectado hello. Os valores em cada nó de hierarquia Olá determinam informações de Olá exibidas no painel de saudação. Por exemplo, o arquivo JSON de saudação contém Olá Olá fábrica Munique valores a seguir:

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

local, a descrição e o nome da saudação aparecem nesta exibição no painel de saudação:

![Dados de Munique no painel de saudação][img-munich]

Cada fábrica, linha de produção e estação tem uma propriedade de imagem. Você pode encontrar esses arquivos JPEG em Olá **Content\img** pasta Olá **WebApp** projeto. Esses arquivos de imagem exibem no painel de fábrica conectado de saudação.

Cada estação inclui várias propriedades detalhadas que definem Olá mapeamento da saudação OPC UA itens de dados. Essas propriedades são descritas Olá seções a seguir:

### <a name="opcuri"></a>OpcUri

Olá **OpcUri** valor é hello OPC UA aplicativo URI que identifica exclusivamente a saudação servidor OPC UA. Por exemplo, Olá **OpcUri** valor de estação de assembly hello na linha de produção 1 em Munique semelhante ao seguinte Olá: **urn: scada2194:ua:munich:productionline0:assemblystation**.

Você pode exibir hello URIs de saudação conectada OPC UA servidores no painel de solução de saudação:

![Exibir URIs do servidor OPC UA][img-server-uris]

### <a name="simulation"></a>Simulação

Olá informações Olá **simulação** nó é específico toohello simulação OPC UA que é executado no hello servidores OPC UA provisionados por padrão. Ele não é usado para um servidor OPC UA real.

### <a name="kpi1-and-kpi2"></a>Kpi1 e Kpi2

Esses nós descrevem como dados de estação Olá contribuem toohello dois valores KPI no painel de saudação. Em uma implantação padrão, esses valores de KPI são unidades por hora e kWh por hora. solução de saudação calcula os valores KPI no nível de saudação de uma estação e agrega-los na linha de produção de hello e níveis de fábrica.

Cada KPI tem um valor mínimo, máximo e de destino. Cada valor KPI também pode definir ações de alerta para tooperform de solução de fábrica Olá conectado. Olá trecho a seguir mostra definições de KPI Olá para a estação de assembly hello na linha de produção 1 em Munique:

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

Olá seguinte captura de tela mostra dados KPI de saudação no painel de saudação.

![Informações de KPI no painel de saudação][lnk-kpi]

### <a name="opcnodes"></a>OpcNodes

Olá **OpcNodes** identificam nós Olá itens de dados publicados de saudação servidor OPC UA e especificar como tooprocess esses dados.

Olá **NodeId** valor identifica Olá NodeID de UA OPC específico de saudação servidor OPC UA. primeiro nó Olá na estação de assembly Olá para a linha de produção 1 em Munique tem um valor **ns = 2; i = 385**. Um **NodeId** valor especifica Olá tooread de item de dados de saudação servidor OPC UA e hello **SymbolicName** fornece toouse um nome amigável de usuário no painel de saudação para os dados.

Outros valores associados a cada nó são resumidos na Olá a tabela a seguir:

| Valor | Descrição |
| ----- | ----------- |
| Relevância  | os valores KPI e OEE Olá esses dados contribuem para. |
| OpCode     | Como os dados de saudação são agregados. |
| Unidades      | Olá unidades toouse, no painel de saudação.  |
| Visible    | Se toodisplay este valor no painel de saudação. Alguns valores são usados em cálculos, mas não são exibidos.  |
| Máximo    | valor máximo Olá que dispara um alerta no painel de saudação. |
| MaximumAlertActions | Tootake uma ação no alerta de tooan de resposta. Por exemplo, envie uma estação de tooa do comando. |
| ConstValue | Um valor constante usado em um cálculo. |

## <a name="deploy-hello-changes"></a>Implantar alterações Olá

Quando terminar de fazer alterações toohello **ContosoTopologyDescription.json** arquivo, você deve reimplantar Olá conectado fábrica solução tooyour conta do Azure.

Olá **azure iot-conectado-fábrica** repositório inclui um **build.ps1** script do PowerShell, você pode usar toorebuild e implantar a solução de saudação.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre solução de fábrica pré-configurado de saudação conectada por Olá ler artigos a seguir:

* [Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]
* [Implantar um gateway para a fábrica conectada][lnk-connect-cf]
* [Permissões no site de azureiotsuite.com Olá][lnk-permissions]
* [Perguntas frequentes do factory conectado](iot-suite-faq-cf.md)
* [Perguntas frequentes][lnk-faq]


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