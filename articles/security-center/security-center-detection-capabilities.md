---
title: "recursos de aaaDetection na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda toounderstand como funcionam os recursos de detecção do Centro de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Recursos de detecção da Central de Segurança do Azure
Este documento aborda recursos de detecção Avançado da Central de segurança do Azure, que ajuda a identificar ameaças ativas direcionando os recursos do Microsoft Azure e fornece a que você com informações de saudação necessário toorespond rapidamente.

> [!NOTE]
> Detecções avançadas estão disponíveis em saudação padrão da camada do Azure Central de segurança. Há uma avaliação gratuita de 60 dias disponível. Você pode atualizar do hello seleção de preço em Olá [política de segurança](security-center-policies.md). Visite [página do Centro de segurança](https://azure.microsoft.com/pricing/details/security-center/) toolearn mais sobre preços. 
> 
> 

## <a name="responding-tootodays-threats"></a>Respondendo a ameaças de tootoday
Houve alterações significativas no cenário de ameaças Olá sobre Olá últimos 20 anos. Em Olá anterior, as empresas geralmente somente tinham tooworry sobre Desfiguração do site por invasores individuais que principalmente estava interessado em ver "o que eles fariam". Os hackers de hoje em dia são muito mais sofisticados e organizados. Eles geralmente têm objetivos estratégicos e financeiros específicos. Eles também possuem mais recursos toothem disponíveis, como eles podem ser suportados por estados de país ou crime organizado.

Essa abordagem gerou um nível de profissionalismo em classificações de invasor Olá sem precedentes tooan. Eles não estão mais interessados em desfiguração da Web. Eles são agora interessado roubar informações contas financeiras e dados privados – todos os quais eles podem usar toogenerate descontar Olá a open market ou tooleverage um negócio específico, a posição de política ou militar. Mais sobre que os invasores com o objetivo de financeiros invasores Olá que violam a pessoas e redes toodo danos tooinfrastructure.

Em resposta, as organizações geralmente implantar várias soluções de ponto, com foco em defesa do perímetro da empresa hello ou pontos de extremidade procurando assinaturas de ataques conhecidos. Essas soluções tendem toogenerate um alto volume de alertas de baixa fidelidade, que requerem um tootriage de analistas de segurança e investigar. A maioria das organizações não têm tempo de saudação e experiência necessária toorespond toothese alertas – tantos vão periféricos.  Enquanto isso, os invasores evoluíram toosubvert seus métodos muitas proteções baseadas em assinatura e [adaptar ambientes toocloud](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Novas abordagens são necessário toomore rapidamente identificar ameaças emergentes e acelerar a detecção e a resposta. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Como a Central de segurança do Azure detecta e responde toothreats
Pesquisadores de segurança da Microsoft estão constantemente em bloqueio de saudação para ameaças. Eles têm acesso tooan extenso conjunto de telemetria obtida com a presença global da Microsoft na nuvem hello e local. Esta coleção profundos e diversas de conjuntos de dados permite que a Microsoft toodiscover novo ataque padrões e tendências em seus produtos de consumidor e empresariais no local, bem como os serviços online. Como resultado, a Central de Segurança pode atualizar rapidamente seus algoritmos de detecção conforme os invasores lançam explorações novas e cada vez mais sofisticadas. Isso ajuda a acompanhar o ritmo de um ambiente de ameaças que muda rapidamente. 

Detecção de ameaças de segurança central funciona automaticamente Coletando informações de segurança de seus recursos do Azure, rede hello e soluções de parceiros conectado. Ele analisa essas informações, geralmente correlacionando informações de várias fontes, tooidentify ameaças. Alertas de segurança são priorizados na Central de segurança, juntamente com recomendações sobre como tooremediate Olá ameaça.

![Apresentação e coleta de dados da Central de Segurança](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

A Central de Segurança emprega análise de segurança avançada, que vai além das abordagens baseadas em assinatura. Soluções de dados grandes e [aprendizado de máquina](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologias são eventos tooevaluate utilizado pela estrutura de nuvem inteira hello – detecção de ameaças que seriam impossível tooidentify usando abordagens manuais e prevendo Olá evolução de ataques. Essas análises de segurança incluem: 

* **Integrado a inteligência de ameaça**: parece para conhecidos atores ruins, aproveitando a inteligência de ameaça global de produtos e serviços, Microsoft hello Microsoft Digital Crimes unidade (DCU), Olá Microsoft Security Response Center (MSRC) e externas feeds.
* **Análise de comportamento**: aplica os comportamentos mal-intencionados de toodiscover padrões conhecidos. 
* **Detecção de anomalias**: usa estatísticas de criação de perfil toobuild uma linha de base histórica. Ele o alertará sobre desvios das linhas de base estabelecidas em conformidade com o vetor de ataque potencial tooa.

### <a name="threat-intelligence"></a>Inteligência contra ameaças
A Microsoft tem uma grande quantidade de inteligência contra ameaças globais. Telemetria fluxos de várias fontes, como o Azure, Office 365, Microsoft CRM online, o Microsoft Dynamics AX, outlook.com, MSN.com, Olá Microsoft Digital Crimes unidade (DCU) e Microsoft Security Response Center (MSRC). Os pesquisadores também recebem informações de inteligência de ameaça que são compartilhadas entre os provedores de serviços de nuvem principal e assina toothreat intelligence feeds de terceiros. Central de segurança do Azure pode usar este tooalert informações você toothreats de atores de ruins conhecidos. Alguns exemplos incluem:

* **Endereço IP mal-intencionado comunicação de saída tooa**: tooa de tráfego de saída conhecidos botnet ou darknet provavelmente indica que o recurso tenha sido comprometido e um invasor tentar tooexecute de comandos no sistema ou exfiltrate dados. Central de segurança do Azure compara o banco de dados do tooMicrosoft do tráfego de rede global de ameaças e o alerta quando ele detecta que o endereço IP mal-intencionado tooa comunicação.

## <a name="behavioral-analytics"></a>Análise comportamental
Análise de comportamento é uma técnica que analisa e compara tooa coleção de padrões conhecidos. No entanto, esses padrões não são assinaturas simples. Eles são determinados por meio de algoritmos de aprendizagem de máquina complexos que são aplicadas toomassive conjuntos de dados. Eles também são determinados pela análise cuidadosa de comportamentos mal-intencionados por analistas especialistas. Central de segurança do Azure podem usar recursos de tooidentify comprometido de análise de comportamento com base na análise de logs de máquina virtual, logs de dispositivo de rede virtual, logs de infraestrutura, despejos de memória e outras fontes. 

Além disso, há correlação com outros toocheck de sinais para dar suporte a evidência de uma campanha generalizada. Essa correlação ajuda tooidentify eventos que são consistentes com estabelecida indicadores de comprometimento. Alguns exemplos incluem:

* **Execução do processo suspeitas**: invasores empregam várias técnicas tooexecute mal-intencionados sem detecção. Por exemplo, um invasor pode dar malware Olá mesmos nomes de arquivos do sistema legítimo, mas coloque esses arquivos em um local alternativo, use um nome que é muito semelhante tooa benignas ou arquivo de máscara Olá true extensão de. Monitores e comportamentos de processos de modelos de Central de segurança processam exceções de toodetect execuções como estes.  
* **Oculta as tentativas de malware e explorações**: sofisticadas de malware é capaz de tooevade antimalware tradicionais produtos nunca gravar toodisk ou criptografar os componentes de software armazenados no disco.  No entanto, esse tipo de malware pode ser detectado usando a análise de memória, como malware Olá deve deixar rastreamentos na memória em ordem toofunction. Quando o software falha, um despejo de captura uma parte da memória em tempo de saudação de travamento hello.  Analisando memória Olá no despejo Olá, Central de segurança do Azure pode detectar técnicas usadas tooexploit vulnerabilidades no software, acessar dados confidenciais e clandestinamente persistem com um computador comprometido sem afetar o desempenho de saudação do seu computador.
* **Lateral movimentação e reconhecimento interno**: toopersist em um comprometido rede e localizar/coleta dados valioso, os invasores muitas vezes tentam toomove lateralmente da saudação comprometida tooothers máquina dentro Olá a mesma rede. Central de segurança monitora o processo e as atividades de logon em ordem toodiscover tentativas tooexpand destaque de um invasor em rede hello, como probing de rede de execução de comando remoto e enumeração de conta.
* **Scripts do PowerShell mal-intencionados**: PowerShell está sendo usado por invasores tooexecute mal-intencionados em máquinas virtuais de destino para uma variedade de propósitos. A Central de Segurança inspeciona a atividade do PowerShell para obter evidência de atividades suspeitas. 
* **Ataques de saída**: os invasores geralmente recursos de nuvem com objetivo hello usando esses ataques adicionais de toomount de recursos de destino. Comprometido máquinas de virtuais, por exemplo, pode ser usado toolaunch ataques de força bruta em relação a outras máquinas virtuais, enviar SPAM ou examinar portas abertas e Olá de outros dispositivos na internet. Aplicando máquina toonetwork tráfego de aprendizado, Central de segurança pode detectar quando as comunicações de rede de saída excederem norma hello. No caso de saudação de SPAM, Central de segurança também correlaciona tráfego incomuns de email com inteligência do Office 365 toodetermine se mensagens de saudação provavelmente mal-intencionado ou Olá resultado de uma campanha de email legítimo.  

### <a name="anomaly-detection"></a>Detecção de anomalias
Central de segurança do Azure também usa as ameaças tooidentify de detecção de anomalias. Análise de toobehavioral contraste (o que depende de padrões conhecidos derivados de grandes conjuntos de dados), detecção de anomalias mais "personalizada" e concentra-se nas linhas de base são implantações tooyour específico. Aprendizado de máquina toodetermine aplicada a atividade normal para implantações e, em seguida, regras de condições de exceções de toodefine gerado que podem representar um evento de segurança. Aqui está um exemplo:

* **Ataques de força bruta vindos de RDP/SSH**: suas implantações podem ter máquinas virtuais ocupadas com uma grande quantidade diária de logons e outras máquinas virtuais que têm muito poucos ou nenhum logon. Central de segurança do Azure pode determinar a atividade de logon de linha de base para as máquinas virtuais e usar toodefine de aprendizado de máquina que está fora da atividade de logon normal. Se o número de logons hello ou tempo de saudação do dia de logons de saudação ou local de saudação do qual Olá logons são solicitados ou outras características de logon significativamente diferente da linha de base de saudação, um alerta pode ser gerado. Novamente, o aprendizado de máquina determina o que é relevante.

## <a name="continuous-threat-intelligence-monitoring"></a>Monitoramento contínuo de inteligência contra ameaças
Central de segurança do Azure funciona segurança dados ciência equipes de pesquisa e que monitoram continuamente as alterações no cenário de ameaças hello. Isso inclui Olá iniciativas a seguir:

* **Monitoramento de inteligência contra ameaças**: a inteligência contra ameaças inclui mecanismos, indicadores, implicações e conselhos acionáveis sobre ameaças iminentes ou existentes. Essas informações são compartilhadas na comunidade de segurança hello e Microsoft monitora continuamente os feeds de inteligência de ameaça de fontes internas e externas.
* **Compartilhamento de sinal**: ideias de equipes de segurança de todo o amplo portfólio da Microsoft de serviços locais e de nuvem, servidores e dispositivos de ponto de extremidade cliente são compartilhadas e analisadas. 
* **Especialistas de segurança da Microsoft**: comprometimento contínuo com as equipes da Microsoft que trabalham em campos de segurança especializada, como computação forense e detecção de ataque à Web.
* **Detecção de ajuste**: algoritmos são executados em conjuntos de dados de clientes reais e pesquisadores de segurança de trabalhar com os resultados de saudação do toovalidate de clientes. Verdadeiros e falsos positivos são algoritmos de aprendizado de máquina toorefine usado.

Esses esforços combinados culminar detecções novos e aprimorados, que você pode se beneficiar de instantaneamente – não há nenhuma ação para você tootake.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como funcionam os recursos de detecção do tooAzure Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [Gerenciando e responder a alertas toosecurity na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)
* [Alertas de Segurança por Tipo na Central de Segurança do Azure](security-center-alerts-type.md)
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.

