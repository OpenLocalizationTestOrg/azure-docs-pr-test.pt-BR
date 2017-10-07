---
title: "manutenção aaaPredictive pré-configurado solução | Microsoft Docs"
description: "Uma descrição da manutenção preditiva do hello Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Visão geral da solução pré-configurada de manutenção preditiva

Olá *manutenção preditiva* [pré-configurado solução] [ lnk_preconfigured_solutions] é uma saudação [Microsoft Azure IoT Suite] [ lnk_iot_suite] soluções pré-configuradas. Essa solução integra a coleta de telemetria do dispositivo em tempo real com um modelo preditivo criado com o [Azure Machine Learning][lnk-machine-learning].

Com o Azure IoT Suite, você pode rapidamente e facilmente conectam tooand monitor ativos e analisar a telemetria em tempo real em painéis e visualizações. Solução de manutenção preditiva hello, visualizações e painéis Olá fornecem nova inteligência que pode gerar eficiência e aumentar a fluxos de receita.

## <a name="hello-scenario"></a>Olá cenário

A Fabrikam é uma companhia aérea regional que se dedica a fornecer uma excelente experiência ao cliente a preços competitivos. Uma das causas de atrasos de voos são problemas de manutenção e a manutenção dos motores de aeronave representa um desafio singular. A Fabrikam deve evitar falha do mecanismo durante o voo todo custo, portanto ele inspeciona seus mecanismos regularmente e agenda de manutenção de acordo com o plano de tooa. No entanto, aeronave mecanismos sempre não desempenham Olá mesmo. Algum tipo de manutenção desnecessária é realizada nos motores. O mais importante é que problemas ocorrem, o que pode fazer com que uma aeronave permaneça em solo até que a manutenção seja realizada. Se um avião estiver em um local onde Olá técnicos direita ou peças de reposição não estiverem disponíveis, esses problemas podem ser especialmente dispendiosos.

mecanismos de saudação do aeronave da Fabrikam são instrumentados com sensores que monitoram as condições de mecanismo durante o trânsito. A Fabrikam usa Olá manutenção preditiva solução toocollect Olá sensor dados coletados durante o voo Olá. Após acumulando anos de mecanismo operacional e dados de falha, os cientistas de dados da Fabrikam têm modelada uma saudação toopredict de maneira vida útil restante (regra) de um mecanismo de aeronave. modelo de saudação usa uma correlação entre dados de quatro sensores de mecanismo hello e desgaste mecanismo que leva tooeventual falha. Enquanto a Fabrikam continua a segurança de tooensure tooperform inspeções regular, podem ser usadas Olá modelos toocompute Olá regra para cada mecanismo após cada voo. modelo de saudação usa telemetria Olá coletada de mecanismos de saudação durante o voo hello. A Fabrikam agora pode prever os futuros pontos de falha e planejar a manutenção e reparar antecipadamente.

> [!NOTE]
> modelo de solução de saudação usa dados de desgaste de mecanismo real.

Por prever ponto hello quando a manutenção seja necessária, Fabrikam pode otimizar os custos de tooreduce de operações.

Coordenadores de manutenção trabalham com os agendadores para:

- Plano de manutenção toocoincide com um avião parar em um local específico.
- Certifique-se de tempo suficiente está disponível para Olá aeronave toobe fora de serviço sem causar interrupções de agenda.
- os técnicos de tooschedule tooensure que aeronave é atendida com eficiência sem tempo de espera.

Os gerentes de controle de inventário recebem planos de manutenção, para que possam otimizar seu processo de encomendas e inventário de peças de reposição.

Essas atividades habilitar horário de início do Fabrikam toominimize aeronave e reduzem os custos operacionais, garantindo a segurança Olá de passageiros e equipe.

toounderstand como [Azure IoT Suite] [ lnk_iot_suite] fornece recursos que os clientes Olá precisam potencial de saudação toorealize manutenção preditiva, examine [infográfico] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>Como solução de manutenção preditiva Olá é criada

solução de saudação usa um modelo de aprendizado de máquina do Azure existente como um modelo tooshow esses recursos trabalhando de telemetria do dispositivo coletada por meio de serviços do IoT Suite. A Microsoft criou um [modelo de regressão] [ lnk_regression_model] de um mecanismo de aeronave com base nos dados publicamente disponíveis<sup>\[1\]</sup>e passo a passo orientação sobre como toouse Olá modelo.

Olá solução de manutenção preditiva IoT do Azure usa o modelo de regressão de saudação criado com base neste modelo. modelo de saudação é implantado em sua assinatura do Azure e exposto por meio de uma API gerada automaticamente. solução de saudação inclui um subconjunto de saudação representando 4 (do total de 100) de dados de teste mecanismos e fluxos de dados de sensor Olá 4 (do total de 21). Esses dados são suficiente tooprovide um resultado preciso do modelo treinado hello.

*\[1\] A. Saxena e K. Goebel (2008). “Turbofan Engine Degradation Simulation Data Set” (Conjunto de dados da simulação de degradação do turbofan), Repositório de dados de prognóstico da NASA Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Introdução à manutenção de previsão

Este tutorial mostra como tooprovision Olá solução manutenção preditiva. Ele também orienta você por meio de recursos básicos de saudação de solução de manutenção preditiva hello. Você pode acessar muitos desses recursos por meio do painel de solução de saudação implanta junto com a solução Olá pré-configurado.

toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.

> [!NOTE]
> Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].

1. Faça logon no muito[azureiotsuite.com] [ lnk-azureiotsuite] usando o Azure, as credenciais de conta e clique em  **+**  toocreate uma solução.
1. Clique em **selecione** Olá **manutenção preditiva** lado a lado.
1. Insira um **nome da solução** sua manutenção previsão pré-configurados de solução.
1. Selecione Olá **região** e **assinatura** deseja toouse tooprovision Olá solução.
1. Clique em **criar solução** Olá toobegin processo de provisionamento. Normalmente, esse processo leva vários toorun de minutos.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Aguarde a saudação toocomplete do processo de provisionamento

1. Clique em bloco de saudação para sua solução com **provisionamento** status.
1. Saudação de aviso **provisionamento estados** como serviços do Azure são implantados na sua assinatura do Azure.
1. Após a conclusão do provisionamento, Olá alterações de status muito**pronto**.
1. Clique em Olá bloco toosee Olá detalhes de sua solução no painel direito da saudação. Nesse painel, você pode iniciar Olá solução painel de controle e acesso Olá aprendizado de máquina espaço de trabalho.

> [!NOTE]
> Se você encontrar problemas de implantação de solução Olá pré-configurado, examine [permissões no site do hello azureiotsuite.com] [ lnk-permissions] e hello [perguntas frequentes sobre] [ lnk-faq]. Se os problemas de saudação persistirem, criar um tíquete de serviço em Olá [portal][lnk-portal].

Há detalhes esperado toosee que não estejam listados para sua solução? Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="view-hello-solution"></a>Solução de saudação do modo de exibição

Esta seção orienta você por meio da solução de saudação da interface do usuário.

### <a name="predictive-maintenance-dashboard"></a>Painel Manutenção Preditiva

Esta página no aplicativo da web hello usa PowerBI JavaScript controles (consulte Olá [repositório PowerBI-visuals][lnk-powerbi]) toovisualize:

* dados de saída de saudação de trabalhos do Stream Analytics Olá no armazenamento de blob.
* Olá regra e ciclo de contagem por mecanismo aeronave.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>Observar o comportamento de saudação da solução de nuvem Olá

Em Olá portal do Azure, navegue até o grupo de recursos toohello com o nome da solução Olá você escolheu tooview seus recursos provisionados.

![][img-resource-group]

Quando você provisiona solução Olá pré-configurados, você recebe um email com um espaço de trabalho do aprendizado de máquina de toohello do link. Você também pode navegar toohello o espaço de trabalho de aprendizado de máquina da saudação [azureiotsuite.com] [ lnk-azureiotsuite] página para sua solução provisionada. Um bloco está disponível nesta página quando Olá solução no hello **pronto** estado.

![][img-machine-learning]

No portal de solução hello, você pode ver que esse exemplo hello está provisionado com dois aeronave de toorepresent de quatro dispositivos simulada com dois mecanismos por aeronave, cada um com quatro sensores. Quando você navega pela primeira vez o portal de solução toohello, simulação Olá será interrompida.

![][img-simulation-stopped]

Clique em **iniciar simulação** toobegin simulação de saudação. Olá histórico de sensor, regra, ciclos e regra de histórico de preencher o painel de saudação.

![][img-simulation-running]

Quando a regra for menor que 160 (um limite arbitrário escolhido para fins de demonstração), o portal de solução de saudação exibe um toohello próximo de símbolo de aviso regra exibir. portal de solução Olá também destaca o mecanismo de aeronave Olá em amarelo. Observe como os valores de regra Olá têm uma tendência descendente geral geral, mas tendem a toobounce para cima e para baixo. Esse comportamento resulta de comprimentos de ciclo de variáveis hello e precisão do modelo hello.

![][img-simulation-warning]

simulação completa Olá leva cerca de 35 toocomplete de minutos 148 ciclos. Olá 160 regra cumprimento do limite para Olá primeira vez em cerca de 5 minutos e ambos os mecanismos de atingido o limite de saudação aproximadamente 8 minutos.

simulação de saudação é executada por meio do conjunto de dados completo Olá para 148 ciclos e estabelece nos valores de regra e ciclo de final.

Você pode parar a simulação de saudação em qualquer ponto, mas clicar em **iniciar simulação** reproduções Olá simulação a partir do início de saudação do conjunto de dados de saudação.

## <a name="next-steps"></a>Próximas etapas

mais sobre como o Azure IoT permite cenários de manutenção preditiva, leitura de toolearn [capturar o valor da saudação Internet das coisas][lnk_capture_value].

Tirar uma [passo a passo] [ lnk-predictive-walkthrough] de solução de manutenção preditiva hello.

Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:

* [Perguntas frequentes sobre o IoT Suite][lnk-faq]
* [Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/