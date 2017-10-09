---
title: "dados pessoais de aaaProtect na Central de segurança do Azure | Microsoft Docs"
description: "proteger dados pessoais usando a central de segurança do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Proteger dados pessoais contra violações e ataques: Central de Segurança do Azure

Este artigo ajuda você a entender como os dados pessoais do toouse Central de segurança do Azure tooprotect de violar e ataques.

## <a name="scenario"></a>Cenário 

Uma empresa cruzeiro grandes, com sede em Olá Estados Unidos, está expandindo suas roteiros de toooffer operações Olá Mediterrâneo e mares báltico, bem como Olá Britânicas. toohelp nesses esforços, ela adquiriu várias linhas de cruzeiro menores com base na Itália, Alemanha, Dinamarca e Olá Reino Unido

empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello. Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito. Também incluem informações de Recursos Humanos, como:

- Endereços
- Números de telefone
- Números de identificação fiscal
- Informações de saúde

linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade. Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes espalhados Olá, mundo têm acesso toosome recursos da empresa.
Dados pessoais viajam pela rede Olá entre esses locais e o data center da Microsoft hello.

## <a name="problem-statement"></a>Problema declarado

empresa de saudação está preocupada a ameaça de saudação de ataques a seus recursos do Azure. Eles querem tooprevent exposição de pessoas de toounauthorized dados pessoais dos funcionários e clientes. Eles desejam obter orientação sobre a prevenção e resposta/correção, bem como uma maneira eficiente toomonitor Olá contínuo de segurança de seus recursos de nuvem.
Ela precisa de uma linha forte de proteção contra os invasores sofisticados e organizados de hoje.

## <a name="company-goal"></a>Meta da empresa

Uma das metas da empresa Olá é privacidade de saudação tooensure dos dados pessoais dos funcionários e clientes protegê-lo contra ameaças. Um dos seus objetivos é toorespond imediatamente toosigns de violação toomitigate Olá impacto. Requer uma maneira tooassess Olá estado atual da segurança, identificar configurações vulneráveis e corrigi-los.

## <a name="solutions"></a>Soluções

O ASC (Central de Segurança do Microsoft Azure) fornece uma solução integrada de gerenciamento de política e monitoramento da segurança. Ele oferece funcionalidades eficazes e fáceis de usar de prevenção, detecção e resposta a ameaças.

### <a name="prevention"></a>Prevenção

ASC ajuda a evitar violações, permitindo que você tooset as políticas de segurança, forneça acesso just-in-time e implementar as recomendações de segurança.

Uma política de segurança define o conjunto de saudação de controles recomendado para recursos em Olá especificado assinatura. No momento o acesso pode ser usado toolock para baixo tráfego de entrada tooyour VMs do Azure, reduzindo a exposição tooattacks. Recomendações de segurança são criadas pelo ASC depois de analisar o estado de segurança Olá seus recursos do Azure.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Como fazer para definir políticas de segurança no ASC?

É possível configurar políticas de segurança para cada assinatura. toomodify uma política de segurança, você deve ser um proprietário ou colaborador da assinatura. No portal do Azure de Olá, Olá a seguir:

1. Selecione **política** no painel de controle do hello ASC.

2. Selecione a assinatura de saudação no qual você deseja tooenable política de saudação.

3. Escolha **política de prevenção de** tooconfigure políticas por assinatura. **Coletar dados de máquinas virtuais** deve ser definido muito**em.**

4. Em Olá **política de prevenção de** opções, selecionadas **na** tooenable Olá as recomendações de segurança que são relevantes para a assinatura de saudação.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Para obter mais instruções e uma explicação de cada uma das recomendações de política de saudação que podem ser habilitadas, consulte [definir políticas de segurança na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Como fazer para configurar o acesso JIT (Just-In-Time)?

Quando JIT está habilitada, a Central de segurança bloqueia o tráfego de entrada tooyour VMs do Azure, criando uma regra NSG. Selecione as portas de saudação em Olá VM toowhich o tráfego de entrada será bloqueado para baixo. toouse JIT acessar, Olá a seguir:

1. Selecione Olá **logo no bloco de acesso VM tempo** na folha ASC hello.

2. Selecione Olá **recomendado** guia.

3. Em **VMs**, selecione Olá VMs que você deseja tooenable. Isso coloca uma tooa de marca de seleção próxima VM. 
4. Selecione **Habilitar JIT** nas VMs.
5. Selecione **Salvar**.

Em seguida, você pode ver as portas padrão Olá ASC recomenda habilitar de JIT. Você também pode adicionar e configurar uma nova porta na qual você deseja tooenable Olá apenas na solução de tempo. Olá **apenas no acesso de tempo de VM** lado a lado na Central de segurança de saudação mostra o número de saudação de máquinas virtuais configuradas para acesso JIT. Ele também mostra o número de Olá aprovados de solicitações de acesso feitas no hello última semana.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Para obter instruções sobre como toodo, e informações adicionais sobre apenas no acesso de tempo, consulte [gerenciar o acesso de máquina virtual usando no momento.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>Como fazer para implementar as recomendações de segurança do ASC?

Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações. recomendações de saudação orientará você durante processo de saudação do configurando controles de saudação necessário. 
1. Selecione Olá **recomendações** bloco no painel ASC hello.

2. Exibir recomendações de saudação, que são mostradas em um formato de tabela em que cada linha representa uma recomendação.

3. recomendações de toofilter, selecione **filtro** e selecione os valores de severidade e estado de saudação desejar toosee.

4. toodismiss uma recomendação não é aplicável, você pode clique com botão direito e selecione **ignorar.**

5. Avalie qual recomendação deve ser aplicada primeiro.

6. Aplica recomendações de saudação em ordem de prioridade.

Para obter uma lista de recomendações possíveis e instruções passo a passo sobre como tooapply cada, consulte [Gerenciando recomendações de segurança na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Detecção e resposta

Detecção e resposta vá juntas, conforme desejar toorespond assim que possível após uma ameaça é detectada.
A detecção de ameaças ASC funciona automaticamente Coletando informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado. O ASC pode atualizar rapidamente seus algoritmos de detecção conforme os invasores lançam explorações novas e cada vez mais sofisticadas. Para obter informações mais detalhadas sobre como funciona a detecção de ameaças do ASC, consulte [Funcionalidades de detecção da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Como gerenciar e responder a alertas toosecurity?

É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema de saudação. Central de segurança também inclui recomendações sobre como tooremediate um ataque. toomanage a segurança de alertas, fazer Olá a seguir:

1. Selecione Olá **alertas de segurança** bloco no painel de controle do hello ASC. Isso mostra detalhes de cada alerta.

2. Selecione toofilter alertas com base na data, estado e gravidade, **filtro** e selecione os valores hello deseja toosee.

3. toorespond tooan alerta, selecioná-la e examinar as informações de saudação, selecione Olá recurso que foi atacado.

4. Em Olá **descrição** campo, você verá os detalhes, incluindo correção recomendada.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Para obter mais instruções sobre alertas de toosecurity está respondendo, consulte [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Para obter ajuda na investigação de alertas de segurança, a empresa Olá pode integrar alertas ASC com sua própria solução SIEM, usando [integração do Azure Log](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Como fazer para gerenciar incidentes de segurança?

No ASC, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da cadeia de encerramento. Um incidente revelará a lista de saudação de alertas relacionados, que permite que você tooobtain obter mais informações sobre cada ocorrência. Incidentes aparecem na hello bloco alertas de segurança e de folha.

tooreview e gerenciar incidentes de segurança, Olá a seguir:

1. Selecione Olá **alertas de segurança** lado a lado. Se for detectado um incidente de segurança, ele será exibido no gráfico de alertas de segurança hello. Ele terá um ícone diferente dos outros alertas.

2. Selecione toosee incidente hello mais detalhes sobre este incidente de segurança. Detalhes adicionais incluem sua descrição completa, sua severidade, seu estado atual, Olá atacado recursos, etapas de correção de saudação incidente hello e Olá alertas que foram incluídos neste incidente.

Você pode filtrar toosee **incidentes apenas**, **alertas somente**, ou **ambos**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Como acessar o relatório de inteligência de ameaça de Olá?

ASC analisa informações contra ameaças de tooidentify várias fontes. as equipes de resposta a incidentes tooassist investigam e corrigir ameaças, Central de segurança inclui um relatório de inteligência de ameaça que contém informações sobre a ameaça de saudação que foi detectada.

A Central de Segurança tem três tipos de relatórios de ameaça, que podem variar de acordo com o ataque.
Olá relatórios disponíveis são:

- Relatório de Grupo de Atividade: fornece análises avançadas sobre os invasores, seus objetivos e táticas.

- Relatório de Campanha: concentra-se nos detalhes de campanhas de ataque específicas.

- Relatório de resumo de ameaça: abrange todos os itens em dois relatórios de saudação anterior.

Esse tipo de informação é muito útil durante o processo de resposta a incidentes hello, onde houver uma fonte de saudação toounderstand investigação em andamento de ataque hello, Olá motivações do invasor e quais toomitigate toodo esse problema futuramente.

1. tooaccess Olá inteligência de ameaça de relatório, Olá a seguir:

2. Selecione Olá **alertas de segurança** bloco no painel ASC hello.

3. Selecione o alerta de segurança de saudação do qual você deseja tooobtain obter mais informações.

4. Em Olá **relatórios** , clique em relatório de inteligência de ameaça Olá link toohello.

5. Isso abrirá o arquivo PDF hello, o que pode ser baixado.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Para obter informações adicionais sobre Olá relatório de inteligência de ameaça ASC, consulte [o relatório de inteligência de ameaça do Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Avaliação

toohelp com avaliação, teste e avaliação de sua postura de segurança, ASC fornece para avaliação de vulnerabilidade integrado com Qualys agentes de nuvem, como parte de seu componente de recomendações de máquina virtual.

Olá Qualys agente relatórios vulnerabilidade dados toohello Qualys plataforma de gerenciamento, que envia dados de monitoramento de integridade e vulnerabilidade fazer tooASC. Olá recomendação tooadd uma solução de avaliação de vulnerabilidade é exibida no hello **recomendações** folha no painel de controle do hello ASC.

Após a solução de avaliação de vulnerabilidade hello está instalada na VM de destino Olá, verificações de segurança central Olá toodetect VM e identificam vulnerabilidades do sistema e do aplicativo. Detectados problemas são mostrados em Olá **recomendações de máquinas virtuais** opção.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Como fazer para implementar uma solução de avaliação de vulnerabilidade? 

Se uma Máquina Virtual não tem uma solução de avaliação de vulnerabilidade integrada já implantada, a Central de Segurança recomenda que ela seja instalada.

1. No painel ASC hello, em Olá **recomendações** folha, selecione **adicionar uma solução de avaliação de vulnerabilidade.**

2. Selecione VMs Olá onde deseja que a solução de avaliação de vulnerabilidade tooinstall hello.

3. Clique em **Instalar em [número de] VMs.**

4. Selecione uma solução de parceiro no hello Azure Marketplace ou em **usar solução existente,** selecione **Qualys.**

5. Você pode ativar as configurações de atualização do hello automática ou desativar Olá **soluções de parceiros** folha.

Para obter mais instruções sobre como tooimplement uma solução de avaliação de vulnerabilidade, consulte [avaliação de vulnerabilidade na Central de segurança do Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Próximas etapas

- [Guia de início rápido da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Introdução tooAzure Central de segurança](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Integrando alertas da Central de Segurança do Azure com a integração de logs do Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Melhorar a Central de Segurança do Azure com a avaliação de vulnerabilidade integrada](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
