---
title: "aaaCloud cruiser em e integração de API de cobrança do Microsoft Azure | Microsoft Docs"
description: "Fornece uma perspectiva exclusiva do parceiro de cobrança do Microsoft Azure cruiser em nuvem, em suas experiências integrar Olá APIs de cobrança do Azure em seus produtos.  Isso é especialmente útil para clientes do Azure e do Cloud Cruiser que estejam interessados em usar/experimentar o Cloud Cruiser para o pacote do Microsoft Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Integração da API de Cobrança do Microsoft Azure e Cloud Cruiser
Este artigo descreve como informações de saudação coletadas Olá que novas APIs de cobrança do Microsoft Azure pode ser usado em cruiser em nuvem para o fluxo de trabalho custam simulação e análise.

## <a name="azure-ratecard-api"></a>API RateCard do Azure
Olá API RateCard fornece informações de taxa do Azure. Depois de autenticar com credenciais apropriadas hello, você pode consultar Olá API toocollect metadados sobre os serviços de saudação disponíveis no Azure, junto com as taxas de saudação associadas com sua ID de oferta

Olá, a seguir está um exemplo de resposta da API de saudação mostrando preços Olá para Olá A0 (Windows) instância:

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>TooAzure de Interface do cruiser em RateCard API de nuvem
Cruiser em de nuvem pode aproveitar informações de API RateCard Olá maneiras diferentes. Neste artigo, mostramos como ela pode ser usado toomake IaaS cargas de trabalho custo simulação e análise.

toodemonstrate esse caso de uso, imagine uma carga de trabalho de várias instâncias em execução no Microsoft Azure Pack (WAP). meta de saudação é toosimulate essa mesma carga de trabalho no Azure e os custos de saudação de estimativa de fazer essa migração. Em ordem toocreate esta simulação, há dois toobe principais tarefas executadas:

1. **Importação e processo Olá serviço informações coletadas de saudação RateCard API.** Essa tarefa também é executada em pastas de trabalho hello, onde a extração de saudação da saudação RateCard API é tooa transformados e publicados novo plano de taxa. Este novo plano de taxa será usado nos tooestimate de simulações Olá Olá preços do Azure.
2. **Normalizar serviços WAP e serviços do Azure para IaaS.** Por padrão, os serviços WAP se baseiam em recursos individuais (CPU, tamanho da memória, tamanho do disco, etc.) enquanto os serviços do Azure baseiam-se no tamanho da instância (A0 A1, A2, etc.). A primeira tarefa pode ser realizada pelo mecanismo ETL do cruiser em nuvem, chamado de pastas de trabalho, onde esses recursos podem ser incorporados em tamanhos de instância, análogo tooAzure instância services.

### <a name="import-data-from-hello-ratecard-api"></a>Importar dados de saudação RateCard API
Pastas de trabalho de cruiser em nuvem fornecem uma forma automatizada toocollect e processo de informações de saudação RateCard API.  Pastas de trabalho ETL (extrair, transformar e carregar) permitem a coleção de saudação tooconfigure, transformação e publicação de dados no banco de dados do hello cruiser em nuvem.

Cada pasta de trabalho pode ter uma ou várias coleções, permitindo que você toocorrelate informações toocomplement de origens diferentes ou aumentar dados de uso de saudação. Olá mostrar dois de capturas de tela a seguir como toocreate um novo *coleção* em uma pasta de trabalho e a importação de informações para hello *coleção* de saudação RateCard API:

![Figura 1 — Criando uma nova coleção][1]

![Figura 2: importar dados do novo conjunto de saudação][2]

Depois de importar dados saudação na pasta de trabalho Olá, é possível toocreate várias etapas e os processos de transformação, toomodify e modelo Olá dados. Neste exemplo, já que estamos interessados apenas na infraestrutura-como-um-serviço (IaaS), podemos usar linhas desnecessárias do hello transformação etapas tooremove ou registros, relacionadas tooservices diferente de IaaS.

Hello seguinte captura de tela mostra as etapas de transformação de saudação usados dados de saudação tooprocess coletados da API RateCard:

![Figura 3 - transformação etapas tooprocess coletados dados de API RateCard][3]

### <a name="defining-new-services-and-rate-plans"></a>Definindo novos serviços e a planos de taxa
Existem serviços de toodefine de diferentes maneiras cruiser em nuvem. Uma das opções de saudação é tooimport serviços de Olá Olá de dados de uso. Esse método normalmente é usado quando se trabalha com nuvens públicas, onde os serviços de saudação já são definidos pelo provedor de saudação.

Um plano de taxas é um conjunto de taxas ou preços que podem ser aplicado toodifferent serviços, com base em datas de efetivação ou grupo de clientes, entre outras opções. Planos de taxa também podem ser usados em simulação de toocreate cruiser em nuvem ou "" cenários, toounderstand como as alterações em serviços podem afetar o custo total de saudação de uma carga de trabalho.

Neste exemplo, usaremos informações do serviço de saudação de novos serviços de saudação RateCard API toodefine em cruiser em nuvem. Em Olá mesmo propósito, podemos usar taxas Olá associadas toohello serviços toocreate um novo plano de taxa no cruiser em nuvem.

No final de saudação do processo de transformação de Olá, é possível toocreate uma nova etapa e publicar dados Olá Olá RateCard API como taxas e novos serviços.

![Figura 4: publicando dados de saudação do hello RateCard API como novos serviços e taxas][4]

### <a name="verify-azure-services-and-rates"></a>Verificação das taxas e os serviços do Azure
Depois de publicar serviços hello e taxas, você pode verificar a lista de saudação de serviços importados do cruiser em nuvem *serviços* guia:

![Figura 5 - verificando Olá novos serviços][5]

Em Olá *taxa planos* guia, você pode verificar Olá novo taxa plano chamado "AzureSimulation" com taxas de saudação importado de saudação RateCard API.

![Figura 6: verificando Olá novo plano de taxa e as taxas associadas][6]

### <a name="normalize-wap-and-azure-services"></a>Normalização WAP e Serviços do Azure
Por padrão, o WAP fornece informações de uso com base no uso de saudação de computação, memória e recursos de rede. No cruiser em nuvem, você pode definir sua alocação de saudação diretamente em serviços com base ou limitado uso desses recursos. Por exemplo, você pode definir uma taxa básica para cada hora de uso da CPU ou custos Olá GB de memória alocada tooan instância.

Neste exemplo, nos custos de toocompare ordem entre WAP e o Azure, é preciso tooaggregate Olá utilização de recursos WAP em pacotes, que pode ser mapeado tooAzure serviços. Essa transformação pode ser implementada facilmente em pastas de trabalho hello:

![Figura 7: transformar os serviços de dados do toonormalize WAP][7]

Olá última etapa na pasta de trabalho de saudação é dados de saudação toopublish no banco de dados do hello cruiser em nuvem. Durante essa etapa, os dados de uso de saudação são fornecidos para os serviços (que mapeiam toohello serviços do Azure) e ligado encargos de saudação do toodefault taxas toocreate.

Depois de terminar de pasta de trabalho de Olá, você pode automatizar processamento Olá de dados Olá, adicionando uma tarefa no Agendador de saudação e especificando a frequência de saudação e a hora de saudação toorun de pasta de trabalho.

![Figura 8 — Planejamento de pasta de trabalho][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Criação de relatórios para análise de custo de simulação de carga de trabalho
Depois de uso de saudação é coletado e encargos são carregados no banco de dados do hello cruiser em nuvem, podemos aproveitar Olá Insights de cruiser em nuvem módulo toocreate Olá cargas de trabalho custo simulação é desejado.

Em ordem toodemonstrate neste cenário, criamos Olá relatórios a seguir:

![Comparação de custos][9]

gráfico de saudação superior mostra uma comparação de custo por serviços, comparando o preço de saudação de carga de trabalho de saudação em execução para cada serviço específico entre WAP (azul escuro) e o Azure (azul claro).

gráfico do Hello inferior mostra Olá mesmo dados mas divididos por departamento. Isso mostra Olá custos para cada departamento toorun sua carga de trabalho WAP e no Azure, junto com a diferença de saudação entre eles na barra de economia de saudação (verde).

## <a name="azure-usage-api"></a>API de Uso do Azure
### <a name="introduction"></a>Introdução
Recentemente, a Microsoft introduziu Olá API de uso do Azure, permitindo que os assinantes pull tooprogrammatically no ideias de toogain de dados de uso sobre seu consumo. Isso é uma ótima notícia para clientes cruiser em nuvem que pode se beneficiar da saudação mais rico conjunto de dados disponível por essa API.

Cruiser em de nuvem pode Aproveite a integração de saudação com hello API de uso de várias maneiras. granularidade da saudação (informações de uso por hora) e informações de metadados de recursos disponíveis por meio de saudação que API fornece Olá necessário do conjunto de dados toosupport flexível Showback ou estorno modelos. 

Neste tutorial, apresentaremos um exemplo de como cruiser em nuvem pode se beneficiar de saudação informações de uso de API. Mais especificamente, podemos será criar um grupo de recursos no Azure, associar marcas para estrutura de conta Olá e descrevem Olá o processo de extração e processamento das informações de marca de saudação em cruiser em nuvem.

objetivo final de saudação é toobe toocreate capaz de relatórios como Olá seguindo um e ser capaz de tooanalyze de custo e consumo com base na estrutura de conta Olá preenchida por marcas de saudação.

![Figura 10 — Relatório com divisões usando marcações][10]

### <a name="microsoft-azure-tags"></a>Marcas do Microsoft Azure
dados de saudação disponíveis por meio de saudação API de uso do Azure incluem não apenas informações de consumo, mas também metadados de recursos, incluindo marcas associadas a ele. Marcas fornecem uma maneira fácil tooorganize seus recursos, mas em toobe ordem eficaz, você precisa tooensure que:

* Marcas são aplicadas corretamente toohello recursos em tempo de provisão
* Marcas corretamente são usadas na estrutura de conta Olá Showback/estorno processo tootie Olá uso toohello da organização.

Estes dois requisitos podem ser desafiadoras, especialmente quando há um processo manual sobre como provisionar hello ou carregar lado. Marcas de digitação, incorretas ou ausentes ainda são reclamações comuns dos clientes quando usando marcas e esses erros pode tornar a vida em Olá Carregando lado muito difícil.

Com hello nova API de uso do Azure, cruiser em nuvem pode extrair informações de identificação de recurso e através de uma ferramenta ETL sofisticada, chamada de pastas de trabalho, corrigir esses erros comuns de marcação. Por meio de transformações usando expressões regulares e correlação de dados, cruiser em nuvem pode identificar recursos marcados incorretamente e aplicar marcas correto do hello, garantindo a associação correta Olá dos recursos de saudação com consumidor hello.

Em Olá Carregando lado, cruiser nuvem em automatiza Olá Showback/estorno processo e podem utilizar Olá marca informações tootie Olá uso toohello apropriado consumidor (departamento, divisão, projeto, etc.). Essa automação é um enorme aprimoramento e pode assegurar um processo de cobrança consistente e auditável.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Criando um grupo de recursos com marcas no Microsoft Azure
Olá primeira etapa deste tutorial é toocreate um grupo de recursos no hello portal do Azure, então, criar novas marcas tooassociate toohello recursos. Neste exemplo, estamos criando Olá marcas a seguir: departamento, ambiente, proprietário, o projeto.

saudação de captura de tela abaixo mostra um exemplo de que marcas associada ao grupo de recursos com hello.

![Figura 11 — Grupo de Recursos com as marcações associadas no Portal do Azure][11]

Olá próxima etapa é toopull Olá informações das Olá API uso cruiser em nuvem. Olá API de uso no momento fornece respostas em formato JSON. Aqui está um exemplo de hello dados recuperados:

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Importar dados de saudação API de uso para cruiser em nuvem
Pastas de trabalho de cruiser em nuvem fornecem uma forma automatizada toocollect e processo de informações de Olá API de uso. Uma pasta de trabalho ETL (extrair, transformar e carregar) permite a coleta de saudação tooconfigure, transformação e publicação de dados no banco de dados do hello cruiser em nuvem.

Cada pasta de trabalho pode ter uma ou várias coleções. Isso permite que informações toocorrelate fontes diferentes toocomplement ou ampliar Olá de dados de uso. Neste exemplo, vamos criar uma nova planilha na pasta de trabalho de modelo do Azure hello (*UsageAPI)* e definir uma nova *coleção* informações tooimport Olá API de uso.

![Figura 3: dados de uso API importados para a folha de UsageAPI Olá][12]

Observe que esta pasta de trabalho já possui outra folhas tooimport serviços do Azure (*ImportServices*) e processar informações de consumo de saudação do hello API de cobrança (*PublishData*).

Em seguida, usaremos Olá Olá de toopopulate de API de uso *UsageAPI* folha e informações de Olá correlacionar com os dados de consumo de saudação do hello API de cobrança em Olá *PublishData* folha.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Processar informações de marca de saudação do hello API de uso
Depois de importar dados saudação na pasta de trabalho Olá, vamos criar etapas de transformação em Olá *UsageAPI* planilha nas informações de saudação tooprocess ordem de saudação API. Primeira etapa é toouse uma saudação "JSON dividir" tooextract do processador marcas de um único campo, em seguida, criar campos para cada um deles (departamento, projeto, proprietário e ambiente).

![Figura 4 - criar novos campos de informações de marca de saudação][13]

Saudação de aviso "Rede" serviço não tem informações de marca hello (caixa amarela), mas podemos verificar que faz parte de saudação mesmo grupo de recursos, observando Olá *ResourceGroupName* campo. Como temos marcas Olá para Olá outros recursos do grupo de recursos, podemos usar esta saudação de tooapply informações marcas toothis recurso posteriormente no processo de saudação ausente.

Olá, próxima etapa é toocreate uma pesquisa associando Olá informações da tabela de saudação marcas toohello *ResourceGroupName*. Essa tabela de pesquisa será usada na próxima etapa tooenrich Olá consumo dados saudação com informações de marca.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Adicionando dados de consumo Olá marca informações toohello
Agora podemos pode saltar toohello *PublishData* folha, quais processos Olá informações de consumo de saudação API de cobrança e adicionar campos Olá extraídos de marcas de saudação. Esse processo é executado examinando a tabela de pesquisa de saudação criada na etapa anterior de saudação, usando Olá *ResourceGroupName* como chave Olá para pesquisas de saudação.

![Figura 5 - populando a estrutura de conta Olá com informações de saudação do pesquisas Olá][14]

Observe que foram aplicados a campos de estrutura Olá conta apropriada para o serviço de "Rede" Olá, corrigir o problema de saudação com hello ausente marcas. É populado também campos de estrutura de conta Olá para recursos que não seja nosso grupo de recursos de destino com "Outros", em ordem toodifferentiate em Olá relatórios.

Agora precisamos apenas tooadd dados de uso uma etapa toopublish hello. Durante esta etapa, taxas de saudação apropriadas para cada serviço definidos no nosso plano de taxa será aplicada toohello as informações de uso com custos resultante de saudação carregados no banco de dados de saudação.

Olá mais importante é que você só tem toogo esse processo por meio de uma vez. Quando a pasta de trabalho de saudação for concluída, você precisa apenas tooadd-Agendador toohello e ele serão executado por hora ou diariamente Olá agendado. Em seguida, ele é apenas uma questão de criar novos relatórios, ou personalizar os existentes, em ordem tooanalyze Olá tooget significativo análises de dados com o uso de nuvem.

### <a name="next-steps"></a>Próximas etapas
* Para obter instruções detalhadas sobre a criação de pastas de trabalho cruiser em nuvem e relatórios, consulte tooCloud cruiser em do on-line [documentação](http://docs.cloudcruiser.com/) (logon válido necessário).  Para obter mais informações sobre o Cloud Cruiser, entre em contato com [info@cloudcruiser.com](mailto:info@cloudcruiser.com).
* Consulte [obter ideias sobre o consumo de recursos do Microsoft Azure](billing-usage-rate-card-overview.md) para uma visão geral das APIs de RateCard e Olá uso de recursos do Azure.
* Check-out Olá [referência da API REST do Azure cobrança](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) para obter mais informações sobre as duas APIs, que fazem parte do conjunto de saudação de APIs fornecidas pelo hello Azure Resource Manager.
* Se você quiser toodive diretamente no código de exemplo hello, check-out de nosso Microsoft Azure cobrança API exemplos de código em [exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>Saiba mais
* Consulte Olá [visão geral do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) artigo toolearn mais sobre hello Azure Resource Manager.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figura 1 — Criando uma nova coleção"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figura 2: importar dados do novo conjunto de saudação"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figura 3 - transformação etapas tooprocess coletados dados de API RateCard"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figura 4: publicando dados de saudação do hello RateCard API como novos serviços e taxas"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figura 5 - verificando Olá novos serviços"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figura 6: verificando Olá novo plano de taxa e as taxas associadas"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figura 7: transformar os serviços de dados do toonormalize WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figura 8 — Planejamento de pasta de trabalho"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figura 9 - relatório de exemplo de cenário de comparação de custo de carga de trabalho Olá"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figura 10 — Relatório com divisões usando marcações"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figura 11 — Grupo de Recursos com as marcações associadas no Portal do Azure"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figura 12 - dados de uso API importados para a folha de UsageAPI Olá"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figura 13 - criar novos campos de informações de marca de saudação"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figura 14 - populando a estrutura de conta Olá com informações de saudação do pesquisas Olá"
