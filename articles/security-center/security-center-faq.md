---
title: "aaaAzure Central de segurança, perguntas frequentes (FAQ) | Microsoft Docs"
description: "Encontre respostas para perguntas frequentes sobre a Central de Segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Perguntas frequentes sobre a Central de Segurança do Azure
Perguntas Frequentes respostas a perguntas sobre o Centro de segurança do Azure, um serviço que ajuda a evitar, detectar e responder toothreats com maior visibilidade e controle sobre a segurança de saudação de seus recursos do Microsoft Azure.

> [!NOTE]
> A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. mais, consulte toolearn [migração da plataforma Azure Security Center](security-center-platform-migration.md). informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Perguntas gerais
### <a name="what-is-azure-security-center"></a>O que é a Central de Segurança do Azure?
Central de segurança do Azure ajuda a evitar, detectar e reagir toothreats com maior visibilidade e controle sobre a segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

### <a name="how-do-i-get-azure-security-center"></a>Como posso obter a Central de Segurança do Azure?
Central de segurança do Azure está habilitado com a sua assinatura do Microsoft Azure e acessada de saudação [portal do Azure](https://azure.microsoft.com/features/azure-portal/). ([Entrar no portal de toohello](https://portal.azure.com), selecione **procurar**e role muito**Central de segurança**).  

## <a name="billing"></a>Cobrança
### <a name="how-does-billing-work-for-azure-security-center"></a>Como funciona o faturamento para a Central de Segurança do Azure?
A Central de Segurança é oferecida em duas camadas:

Olá **grátis** fornece visibilidade sobre o estado de segurança de saudação de recursos do Azure, política de segurança básicas, as recomendações de segurança e integração com produtos de segurança e serviços de parceiros.

Olá **camada padrão** adiciona ameaça avançada recursos de detecção, incluindo inteligência, a análise comportamental, detecção de anomalias, incidentes de segurança de ameaças e relatórios de atribuição da ameaça. camada padrão Hello está livre para Olá primeiros 60 dias. Você deve escolher o serviço de saudação toouse toocontinue além de 60 dias, vamos começar automaticamente toocharge para serviço de saudação.  tooupgrade, selecione preço no hello [política de segurança](security-center-policies.md#set-security-policies). mais, consulte toolearn [preços da Central de segurança](security-center-pricing.md).

## <a name="permissions"></a>Permissões
Central de segurança do Azure usa [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções internas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídos toousers, grupos e serviços no Azure.

Central de segurança avalia a configuração de saudação de vulnerabilidades e problemas de segurança de tooidentify de recursos. Na Central de segurança, você ver apenas as informações relacionadas tooa recurso quando foi atribuída a função de saudação do leitor, colaborador ou proprietário para Olá assinatura ou grupo de recursos que o recurso pertence.

Consulte [permissões na Central de segurança do Azure](security-center-permissions.md) toolearn mais sobre as funções e ações permitidas na Central de segurança.

## <a name="data-collection"></a>Coleta de dados
Central de segurança coleta dados de suas máquinas virtuais tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Quando você acessa pela primeira vez a Central de Segurança, a coleta de dados é habilitada em todas as máquinas virtuais em sua assinatura. Você também pode habilitar a coleta de dados Olá política Central de segurança.

### <a name="how-do-i-disable-data-collection"></a>Como desabilitar a coleta de dados?
Se você estiver usando hello Azure Security Center grátis, você pode desativar a coleta de dados de máquinas virtuais a qualquer momento. Coleta de dados é necessária para as assinaturas na camada padrão hello. Você pode desativar a coleta de dados para uma assinatura no hello política de segurança. ([Entrar no portal do Azure de toohello](https://portal.azure.com), selecione **procurar**, selecione **Central de segurança**e selecione **política**.)  Quando você seleciona uma assinatura, uma nova folha é aberta e oferece a Olá tooturn opção Desativar **coleta de dados**.

### <a name="how-do-i-enable-data-collection"></a>Como habilitar a coleta de dados?
Você pode habilitar a coleta de dados para sua assinatura do Azure Olá política de segurança. coleta de dados tooenable. [Entrar no portal do Azure de toohello](https://portal.azure.com), selecione **procurar**, selecione **Central de segurança**e selecione **política**. Definir **coleta de dados** muito**em**.

### <a name="what-happens-when-data-collection-is-enabled"></a>O que acontece quando a coleta de dados é habilitada?
Quando a coleta de dados é habilitada, Olá Microsoft Monitoring Agent é provisionado automaticamente em todos os existentes e qualquer novo suporte máquinas virtuais que são implantadas na assinatura de saudação.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Dá Olá desempenho de saudação do agente de monitoramento impacto dos meus servidores?
Agente de saudação consome uma quantidade nominal de recursos do sistema e deve ter pouco impacto no desempenho de saudação. Para obter mais informações sobre o impacto no desempenho e o agente de saudação e a extensão, consulte Olá [guia de planejamento e operações](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Onde meus dados são armazenados?
Os dados coletados desse agente são armazenados no análise de Log espaço de trabalho do Log Analytics existente associado à sua assinatura do Azure ou a novos espaços de trabalho. Para obter mais informações, consulte [Segurança de Dados](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Como usar a Central de Segurança do Azure
### <a name="what-is-a-security-policy"></a>O que é uma política de segurança?
Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura. Na Central de segurança do Azure, você pode definir políticas de sua empresa tooyour requisitos de segurança e tipo hello de aplicativos ou confidencialidade dos dados de saudação em cada assinatura de acordo com as assinaturas do Azure.

políticas de segurança Olá habilitadas no monitoramento e as recomendações de segurança de unidade do Centro de segurança do Azure. toolearn mais sobre políticas de segurança, consulte [monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Quem pode modificar uma política de segurança?
toomodify uma política de segurança, você deve ser um administrador de segurança ou um proprietário ou colaborador da assinatura.

toolearn como tooconfigure uma política de segurança, consulte [definindo políticas de segurança na Central de segurança do Azure](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>O que é são recomendações de segurança?
Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure. Quando possíveis vulnerabilidades de segurança são identificadas, são criadas recomendações. Guia de recomendações Olá você pelo processo de saudação da configuração Olá necessário controle. Os exemplos abrangem:

* Provisionamento de antimalware toohelp identificar e remover softwares mal-intencionados
* Configurando [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) e regras toocontrol máquinas de toovirtual de tráfego
* Provisionamento de um toohelp de firewall do aplicativo web proteger contra ataques direcionados a seus aplicativos web
* Como implantar atualizações de sistema ausentes
* Configurações de sistema operacional que não correspondem a saudação de endereçamento recomendado linhas de base

Somente as recomendações que são habilitadas nas Políticas de segurança são mostradas aqui.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>Como ver o estado de segurança atual Olá de meus recursos do Azure?
Olá **visão geral da Central de segurança** folha mostra Olá postura de segurança geral do ambiente dividido por computação, rede, armazenamento e dados e aplicativos. Cada tipo de recurso tem um indicador mostrando se possíveis vulnerabilidades de segurança foram identificadas. Clicar em cada bloco exibe uma lista dos problemas identificados pelo Centro de segurança, junto com um inventário dos recursos de saudação em sua assinatura.

### <a name="what-triggers-a-security-alert"></a>O que dispara um alerta de segurança?
Central de segurança do Azure automaticamente coleta, analisa e funde dados de log de seus recursos do Azure, rede hello e soluções de parceiros, como firewalls e antimalware. Quando forem detectadas ameaças, é criado um alerta de segurança. Os exemplos abrangem a detecção de:

* As máquinas virtuais comprometidas se comunicam com os endereços IP mal-intencionados conhecidos
* Malware avançado detectado com o relatório de erros do Windows
* Ataques por força bruta contra máquinas virtuais
* Alertas de segurança das soluções de segurança de parceiro integradas, como antimalware ou Firewalls de aplicativo Web

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Qual é a diferença de saudação entre ameaças detectadas e alertado pelo Microsoft Security Response Center versus Central de segurança do Azure?
Olá Microsoft Security Response Center (MSRC) executa selecione segurança monitoramento de saudação rede do Azure e a infraestrutura e recebe reclamações abuso e de inteligência de ameaça de terceiros. Quando MSRC fica ciente de que os dados do cliente tem sido acessados por uma parte ilegal ou não autorizada ou uso do cliente saudação do Azure não concordar com os termos de saudação para usar aceitável, um gerente de incidentes de segurança notifica o cliente de saudação. Notificação ocorre normalmente enviando uma toohello de segurança de email especificados na Central de segurança do Azure ou hello proprietário da assinatura do Azure se não for especificado um contato de segurança de contatos.

Central de segurança é um serviço do Azure que monitora o ambiente do Azure do cliente Olá continuamente e aplica-se a análise tooautomatically detectar uma ampla gama de atividades potencialmente mal-intencionadas. Essas detecções são apresentadas como alertas de segurança no painel de Central de segurança hello.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Quais recursos do Azure são monitorados pela Central de Segurança do Azure?
Central de segurança do Azure monitora hello Azure recursos a seguir:

* VMs (máquinas virtuais) (incluindo os [Serviços de Nuvem](../cloud-services/cloud-services-choose-me.md))
* Redes Virtuais do Azure
* Serviço do SQL Azure
* Conta de Armazenamento do Azure
* Aplicativos Web do Azure (em um [Ambiente do Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md))
* Soluções de parceiros integradas com sua assinatura do Azure, como um firewall de aplicativo Web em VMs e no [Ambiente do Serviço de Aplicativo](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Máquinas Virtuais
### <a name="what-types-of-virtual-machines-are-supported"></a>Quais tipos de máquinas virtuais têm suporte?
Monitoramento e as recomendações estão disponíveis para máquinas virtuais (VMs) criadas usando os dois Olá [clássico e modelos de implantação do Gerenciador de recursos](../azure-classic-rm.md).

Consulte [Plataformas com suporte na Central de Segurança do Azure](security-center-os-coverage.md) para obter uma lista de plataformas com suporte.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Por que a Central de segurança do Azure não reconhece a solução de antimalware Olá em execução em minha VM do Azure?
A Central de Segurança do Azure só tem visibilidade de antimalware instalado por meio de extensões do Azure. Por exemplo, a Central de segurança não é capaz de toodetect antimalware que foi instalado em uma imagem que você forneceu ou se você instalou o antimalware em suas máquinas virtuais usando seus próprios processos (como sistemas de gerenciamento de configuração).

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Por que recebo mensagem de saudação "Verificar dados ausentes" para minha VM?
Esta mensagem aparece quando não há nenhum dado de verificação para uma VM. Pode levar algum tempo (menos de uma hora) para toopopulate de dados de verificação após a coleta de dados está habilitada na Central de segurança do Azure. Após a população inicial de saudação de dados de verificação, você receberá esta mensagem porque não há nenhum dado de verificação em todos os ou dados de verificação não recentes. Os exames não são populados para uma VM em um estado parado. Essa mensagem também pode aparecer se dados de verificação não foi preenchida recentemente (de acordo com a política de retenção de saudação de agente do Windows hello, que tem um valor padrão de 30 dias).

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Por que recebo mensagem de saudação "Agente de VM está ausente?"
Olá VM Agent deve ser instalado em VMs tooenable coleta de dados. Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace. Para obter informações sobre como tooinstall Olá VM Agent nas outras VMs, consulte Olá postagem de blog [extensões e agente de VM](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
