---
title: "aaaMonitoring recursos no Operations Management Suite solução de segurança e auditoria | Microsoft Docs"
description: "Este documento ajuda a toouse OMS segurança e auditoria recursos toomonitor seus recursos e identificar problemas de segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite
Este documento ajuda você a usar o OMS segurança e auditoria recursos toomonitor seus recursos e identificar problemas de segurança.

## <a name="what-is-oms"></a>O que é o OMS?
O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Para obter mais informações sobre o OMS, leia o artigo de saudação [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Monitorando recursos
Sempre que possível, você desejará que os incidentes de segurança tooprevent aconteça em primeiro lugar de saudação. No entanto, é impossível tooprevent todos os incidentes de segurança. Quando ocorrer um incidente de segurança, você precisará tooensure que seu impacto é minimizado.  Há três recomendações importantes que podem ser usado toominimize Olá número e Olá impacto de incidentes de segurança:

* Avalie regularmente as vulnerabilidades em seu ambiente.
* Verificar com frequência todos os sistemas de computador e tooensure de dispositivos de rede que têm todos os patches mais recentes do hello instalados.
* Verifique regularmente todos os logs e mecanismos de log, incluindo logs de eventos do sistema operacional, logs específicos de aplicativos e logs do sistema de detecção de intrusões.

OMS segurança e auditoria permite solução IT tooactively monitorar todos os recursos, que podem ajudar a minimiza o impacto de saudação de incidentes de segurança. A Segurança e Auditoria do OMS tem domínios de segurança que podem ser usados para monitorar os recursos. domínios de segurança Olá fornece acesso rápido tooa opções, de saudação de monitoramento de segurança domínios a seguir serão abordados com mais detalhes:

* Avaliação de malware
* Avaliação de atualização
* Identidade e Acesso

> [!NOTE]
> para obter uma visão geral de todas essas opções, leia [Introdução à solução de Segurança e Auditoria do Operations Management Suite](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Monitorando a proteção do sistema
Em uma defesa profunda, cada camada de proteção é importante para Olá estado geral de segurança do seu ativo. Computadores com detectadas ameaças e computadores com proteção insuficiente são mostrados no hello bloco de avaliação de Malware em domínios de segurança. Usando informações Olá Olá avaliação de Malware, você pode identificar um plano tooapply proteção toohello os servidores que precisam dela. tooaccess Olá de siga essa opção etapas abaixo:

1. Em Olá **Microsoft Operations Management Suite** clique de painel principal **segurança e auditoria** lado a lado.
   
    ![Segurança e Auditoria](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. Em Olá **segurança e auditoria** painel, clique em **avaliação Antimalware** em **domínios de segurança**. Olá **avaliação Antimalware** painel é exibido conforme mostrado abaixo:

![Avaliação de malware](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Você pode usar o hello **avaliação de Malware** saudação do painel tooidentify problemas de segurança a seguir:

* **Ameaças ativas**: computadores que foram comprometidos e tem ameaças ativas no sistema de saudação.
* **Corrigida a ameaças**: os computadores que foram comprometidos mas ameaças Olá foram corrigidos.
* **Assinatura desatualizada**: computadores que têm proteção contra malware habilitada mas assinatura hello está desatualizado.
* **Sem proteção em tempo real**: computadores que não têm o antimalware instalado.

### <a name="monitoring-updates"></a>Monitorando as atualizações
Aplicar atualizações de segurança mais recentes da saudação é uma prática recomendada de segurança, e ele deve ser incorporado em sua estratégia de gerenciamento de atualização. Serviço Microsoft Monitoring Agent (HealthService.exe) lê as informações de atualização de computadores monitorados e, em seguida, envia esse serviço OMS toohello informações atualizadas na nuvem Olá para processamento. Olá serviço Microsoft Monitoring Agent é configurado como um serviço automático e ele deve ser sempre executado no computador de destino de saudação.

![Monitorando as atualizações](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Lógica é aplicada toohello atualização de dados e o serviço de nuvem Olá registra dados de saudação. Se forem encontradas atualizações ausentes, elas serão mostradas na Olá **atualizações** painel. Você pode usar o hello **atualizações** toowork painel com ausente atualiza e desenvolver um plano tooapply-los toohello servidores que precisam delas. Siga as etapas de saudação abaixo Olá tooaccess **atualizações** painel:

1. Em Olá **Microsoft Operations Management Suite** clique de painel principal **segurança e auditoria** lado a lado.
2. Em Olá **segurança e auditoria** painel, clique em **avaliação de atualização** em **domínios de segurança**. Painel de atualização de saudação é exibido conforme mostrado abaixo:

![Avaliação de atualização](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

Nesse painel, você pode executar um avaliação toounderstand Olá atual estado de atualização de seus computadores e tratar ameaças mais críticas do hello. Usando Olá **críticas ou atualizações de segurança** lado a lado, os administradores de TI será capaz de tooaccess informações detalhadas sobre atualizações de saudação que estão faltando, conforme mostrado abaixo:

![resultado da pesquisa](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Este relatório inclui informações críticas que podem ser usados tooidentify Olá tipo de ameaça neste sistema vulnerável a, que inclui artigos do Microsoft KB Olá associados a atualização de segurança hello e hello Bulletin MS com mais detalhes sobre Olá vulnerabilidade.

### <a name="monitoring-identity-and-access"></a>Monitorando a identidade e o acesso
Com usuários trabalhando em qualquer lugar, usando diferentes dispositivos e acessando uma grande quantidade de aplicativos na nuvem e locais, é fundamental que suas credenciais sejam protegidas. Ataques de roubo de credenciais são aquelas em que um invasor inicialmente obtiver tooaccess de credenciais do usuário regular tooa acesso um sistema de rede de saudação. Muitas vezes, esse ataque inicial é apenas uma rede de toohello do modo tooget acesso, Olá principal objetivo é toodiscover contas de privilégio. 

Os invasores permanecerá na rede hello, usando disponível gratuitamente ferramentas tooextract credenciais de sessões de saudação de outras contas de logon. Dependendo da configuração do sistema hello, essas credenciais podem ser extraídas na forma de saudação de hashes, permissões ou senhas em texto sem formatação mesmo.  

> [!NOTE]
> as máquinas que são diretamente expostos toohello que Internet verá muitas falha tentativas que toologin tente usando todos os tipos de nomes de usuários conhecidos (por exemplo, administrador). Na maioria dos casos é Okey se não forem usados nomes de usuários conhecidos hello e se a senha de saudação é forte o suficiente.
> 
> 

Ele é possível tooidentify esses invasores antes que eles afetem a uma conta com privilégios. Você pode aproveitar **OMS solução de segurança e auditoria** toomonitor identidades e acesso. Siga as etapas de saudação abaixo Olá tooaccess **de identidade e acesso** painel:

1. Em Olá **Microsoft Operations Management Suite** painel principal, clique em segurança e auditoria lado a lado.
2. Em Olá **segurança e auditoria** painel, clique em **de identidade e acesso** em **domínios de segurança**. Olá **de identidade e acesso** painel é exibido conforme mostrado abaixo:

![identidade e acesso](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Como parte de sua estratégia de monitoramento regular, é necessário incluir o monitoramento de identidade. O Administrador de TI deverá examinar se houver um nome de usuário válido específico que apresenta várias tentativas. Isso pode indicar um invasor que adquiriu o nome de usuário real hello e tente forçar toobrute ou por uma ferramenta automática que usa a senha embutida que expirou.

Habilitar este painel IT tooquickly identificar os recursos do potenciais ameaças relacionadas tooidentity e acesso toocompany. É determinado importante tooalso identificar tendências potenciais, por exemplo no lado a lado Olá Logons ao longo do tempo, você pode ver por período de tempo quantas vezes uma tentativa de logon foi realizada. Nesse caso, Olá computador **FileServer** recebido 35 tentativas de logon. É possível explorar mais detalhes sobre esse computador clicando nele. 

![mais detalhes](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

relatório de saudação gerado para este computador traz detalhes importantes sobre esse padrão. Notado que Olá **conta** fornece coluna Olá conta de usuário que foi usado tootry tooaccess Olá sistema, hello **TIMEGENERATED** fornece coluna Olá o intervalo de tempo no qual Olá tentativa foi feita e Olá **LOGONTYPENAME** fornece coluna Olá local em que essa tentativa foi feita. Se essas tentativas foram executadas localmente no sistema Olá por um programa, Olá **processo** coluna poderia ser mostrando o nome do processo de saudação. Em cenários onde a tentativa de logon de saudação vem de um programa, você já tem o nome do processo Olá disponível e agora você pode executar mais investigação no sistema de destino de saudação.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como toomonitor de solução de segurança da OMS e auditoria toouse seus recursos. toolearn mais sobre a segurança do OMS, consulte Olá artigos a seguir:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Introdução à solução de Segurança e Auditoria do Operations Management Suite](oms-security-getting-started.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)

