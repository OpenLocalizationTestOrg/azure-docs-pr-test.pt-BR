---
title: "aaaDocument proteção dos dados pessoais com ferramentas de relatório do Azure | Microsoft Docs"
description: "como toouse toohelp tecnologias e serviços de relatório do Azure proteger a privacidade dos dados pessoais."
services: security
documentationcenter: na
author: barclayn
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
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Documentar a proteção de dados pessoais com ferramentas de relatório do Azure

Este artigo discutirá como toouse Azure reporting services e tecnologias toohelp proteger a privacidade dos dados pessoais.

## <a name="scenario"></a>Cenário

Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas. toohelp esses esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK

Olá empresa usa o Microsoft Azure para processamento e armazenamento de dados corporativos. Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes. Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais. linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.

Os funcionários corporativos acesso Olá rede da empresa Olá escritórios remotos e agentes espalhados Olá, mundo têm acesso toosome recursos da empresa.

## <a name="problem-statement"></a>Problema declarado

empresa Olá deve proteger a privacidade de saudação dos dados pessoais dos funcionários e clientes por meio de uma estratégia de várias camadas de segurança que usa controles estrito de segurança recursos tooimpose no processamento de tooand de acesso de dados pessoais e de gerenciamento do Azure e deve ser toodemonstrate capaz de sua proteção mede toointernal e auditores externos.

## <a name="company-goal"></a>Meta da empresa

Como parte de sua estratégia de segurança de defesa em profundidade, ele é um tootrack de meta da empresa todo o processamento de tooand acesso dos dados pessoais e certifique-se de que a documentação de proteção de privacidade adequado para os dados pessoais estão em vigor e funcionando.

## <a name="solutions"></a>Soluções

Microsoft Azure fornece registro abrangente de monitoramento, e toohelp de ferramentas de diagnóstico rastrear e registrar atividades e eventos associados ao acessar e processar dados pessoais, geográfico fluxo de dados e acesso de terceiros toopersonal dados. Como a segurança dos dados pessoais na nuvem Olá é uma responsabilidade compartilhada, a Microsoft também fornece aos clientes:

- Informações detalhadas sobre seu próprio processamento dos dados dos clientes

- Medidas de segurança administradas pela Microsoft

- O local para o qual envia os dados dos clientes e a forma como eles são enviados

- Detalhes do próprio processo de análises de privacidade da Microsoft

### <a name="azure-active-directory"></a>Azure Active Directory

O [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft. Olá sign-in do serviço e os recursos de relatório de auditoria entrar detalhada e informações do aplicativo uso atividade toohelp monitorar e garantir que dados pessoais toocustomers' acesso apropriado e funcionários.

Há dois tipos de relatórios de atividade:

- Olá [relatórios de atividade/logs de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) fornecem um registro detalhado das atividades/tarefas do sistema

- Olá [log/relatório de atividade de entradas](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) mostra que executou cada atividade listada no relatório de auditoria Olá

Usando Olá dois juntos, você pode acompanhar o histórico de saudação de todas as tarefas executadas e quem executou cada. Ambos os tipos de relatórios são personalizáveis e podem ser filtrados.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Como acessar segurança e auditoria Olá logs?

Olá logs de auditoria e de segurança podem ser acessados no portal do Active Directory de saudação de três maneiras diferentes: por meio de saudação **atividade** seção (selecione **logs de auditoria** ou **entradas**), ou de **usuários e grupos** ou **aplicativos empresariais** em **gerenciar** no Active Directory. Relatórios também podem ser acessados por meio de saudação do Active Directory do Azure API de relatório. 

1. No portal do Azure de Olá, selecione **Active Directory do Azure.**

2. Em Olá **atividade** seção, selecione **logs de auditoria.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.

4.  Selecione um item no hello toosee de exibição de lista todos os detalhes disponíveis sobre ele.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

Os relatórios do Azure Active Directory também incluem dois tipos de relatórios de segurança, **usuários sinalizados para risco** e **entradas de risco**, que podem ajudá-lo a monitorar riscos potenciais no ambiente do Azure.

Para obter mais informações sobre Olá reporting service, consulte [reporting do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Visite [relatórios de atividades do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) para informações mais específicas sobre Olá relatórios disponíveis no Active Directory do Azure. Este site inclui mais detalhes sobre como tooaccess e usar [relatórios de atividade de logs de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) e [relatórios de atividade de entrada](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) no portal de saudação. Também inclui informações sobre os relatórios de segurança [usuários sinalizados para risco](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) e [entradas de risco](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).

Visite Olá [auditoria do Active Directory do Azure referência da API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site para obter mais informações sobre como tooconnect tooAzure Directory reporting programaticamente.

### <a name="log-analytics"></a>Log Analytics

[Análise de log](https://azure.microsoft.com/services/log-analytics/) pode [coletar dados do Monitor do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate-lo com outros dados e fornecer análise adicional. O Azure Monitor coleta e analisa os dados de monitoramento para o ambiente do Azure. 

Ferramentas de análise no Log Analytics, como pesquisas de logs, exibições e soluções, funcionam com todos os dados coletados, fornecendo uma análise centralizada de todo o ambiente. Análise de log pode agregar e analisar os logs de eventos do Windows, logs do IIS e Syslogs, que pode ajudar a detectar possíveis violações de dados pessoais que podem expor os usuários de toounauthorized dados pessoais.

#### <a name="how-do-i-use-log-analytics"></a>Como fazer para usar o Log Analytics?

Você pode acessar a análise de Log por meio do portal do OMS hello ou hello portal do Azure, de qualquer navegador da web. Análise de log inclui um recuperar de tooquickly de linguagem de consulta e consolidar dados no repositório de saudação. Você pode criar e salvar pesquisas de Log toodirectly analisar dados no portal de saudação.

toocreate um espaço de trabalho de análise de Log em Olá portal do Azure, Olá a seguir:

1. Selecione **análise de Log** na lista de saudação de serviços Olá Marketplace.

2. Selecione **criar,** , em seguida, especificar nome de saudação do seu espaço de trabalho do OMS, selecione sua assinatura, o grupo de recursos, o local e preço.

3. Clique em **Okey** toodisplay uma lista dos espaços de trabalho.

4. Selecione um espaço de trabalho toosee seus detalhes.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Visite Olá [documentação de análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn mais sobre o serviço de saudação.

Visite Olá [começar com um espaço de trabalho de análise de Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) toocreate tutorial um espaço de trabalho de avaliação e conheça os fundamentos de saudação do como toouse Olá serviço.

Visite Olá seguindo a páginas da web para obter informações mais específicas na como tooconnect toouse análise de Log com hello registra descrito acima:

[Fontes de dados de logs de eventos do Windows no Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Logs do IIS no Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Fontes de dados do Syslog no Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure Monitor/Log de Atividades do Azure 

O [Azure Monitor](https://azure.microsoft.com/services/monitor/) fornece logs e métricas de infraestrutura de nível básico para a maioria dos serviços do Microsoft Azure.
Monitoramento pode ajudar toogain aprofundamento sobre seus aplicativos do Azure. Monitor do Azure depende de saudação do Azure extensão de diagnóstico (Windows ou Linux) para coletar logs e as métricas de nível de aplicativo mais. [Olá Log de atividades do Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) é um dos recursos de saudação, você pode exibir o Monitor do Azure. Ele acompanha todas as chamadas à API e fornece uma grande quantidade de informações sobre as atividades que ocorrem no [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Você pode pesquisar hello (anteriormente chamado operacional ou os Logs de auditoria) do Log de atividades para obter informações sobre seu recurso como visto pelo Olá infraestrutura do Azure. 

Embora muitas das informações de saudação registrada no hello atividade de log pertence tooperformance e serviço de integridade, há também informações relacionada tooprotection de dados. Usando hello atividade de Log, você pode determinar hello ", que e quando" para qualquer gravação as operações executadas em recursos de saudação na sua assinatura do Azure (PUT, POST, DELETE).

Por exemplo, ele fornece um registro, quando um administrador exclui um grupo de segurança de rede, que pode afetar a proteção de saudação dos dados pessoais. As entradas do Log de atividades são armazenadas no Azure Monitor por 90 dias.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Como usar dados de saudação coletados pelo Monitor do Azure?

Há um número de maneiras toouse Olá dados no log de atividades de saudação e outros recursos do Monitor do Azure.

- Você pode transmitir locais de tooother Olá dados na linha real.

- Você pode armazenar dados de saudação por períodos mais longos que padrões Olá, usando um [conta de armazenamento do Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) e definindo uma política de retenção.

- Poderá Olá visual dados em gráficos e gráficos, usando Olá [portal do Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), ou ferramentas de visualização de terceiros.

- Você pode consultar dados hello usando Olá API REST do Monitor do Azure, comandos CLI, [PowerShell](https://docs.microsoft.com/powershell/) cmdlets, ou Olá .NET SDK.

tooget iniciado com o Monitor do Azure, selecione **mais serviços** em Olá portal do Azure.

1. Role para baixo demais**Monitor** em Olá **monitoramento e gerenciamento** seção.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Monitor é aberto no hello **Log de atividades** exibição.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Você pode criar e salvar consultas para filtros comuns e pin hello mais importantes consultas tooa painel do portal para que você sempre saiba se ocorreram eventos que atendem aos seus critérios.

1. Você pode filtrar a exibição de saudação por grupo de recursos, timespan e categoria de evento.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Em seguida, você pode fixar o painel do portal de tooa consultas clicando Olá **Pin** botão. Isso ajuda a criar uma única fonte de informações para os dados operacionais em seus serviços. nome da consulta Hello e número de resultados serão exibidos no painel de saudação.

Você também pode usar métricas de tooview Monitor Olá para todos os recursos do Azure, configurar alertas e as configurações de diagnóstico e pesquisar o log de saudação. Para obter mais informações sobre como toouse Olá Monitor do Azure e o Log de atividades, consulte [Introdução ao Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Diagnóstico do Azure 

capacidade de diagnóstico Olá no Azure habilita a coleta de dados de várias fontes. logs de eventos do Windows Hello, que incluem o log de segurança hello, podem ser especialmente úteis no rastreamento e documentar a proteção de dados pessoais. log de segurança Olá rastreia eventos de êxito e falha de logon, bem como alterações de permissões, a detecção de padrões, indicando que certos tipos de ataques, as alterações nas políticas relacionadas à segurança, as alterações de associação de grupo de segurança e muito mais.

Por exemplo, evento ID 4695 alertas você toohello tentada unprotection dos dados protegidos auditáveis. Isso se refere a toohello dados proteção DPAPI (API), que ajuda a tooprotect dados, como chaves privadas, as credenciais armazenadas e outras informações confidenciais.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Como habilitar a extensão de diagnóstico Olá para VMs do Windows?

Você pode usar extensão de diagnóstico de saudação do PowerShell tooenable para uma VM do Windows, assim como os dados de log toocollect. Olá etapas para fazer isso dependem no qual modelo de implantação que você usar (Gerenciador de recursos ou clássico). extensão de diagnóstico tooenable Olá em uma VM existente que foi criada por meio do modelo de implantação do Gerenciador de recursos de saudação, você pode usar o hello [cmdlet do PowerShell Set-AzureRMVMDiagnosticsExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* é Olá caminho toohello arquivo que contém a configuração de diagnóstico de saudação em XML. Para obter mais instruções sobre como habilitar o diagnóstico do Azure em uma máquina virtual, consulte [tooenable de usar o PowerShell diagnóstico do Azure em uma máquina virtual que executa o Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Olá extensão de diagnóstico do Azure pode transferir a conta de armazenamento do Azure Olá coletado dados tooan ou enviá-lo tooservices como Application Insights. Você pode usar dados de saudação para auditoria.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Como fazer para armazenar e exibir os dados de diagnóstico?

É importante tooremember que dados de diagnóstico não são armazenados permanentemente, a menos que você transferir toohello Microsoft Azure tooAzure ou emulador de armazenamento. toostore e exibir dados de diagnóstico no armazenamento do Azure, siga estas etapas:

1. Especifique uma conta de armazenamento no arquivo ServiceConfiguration cscfg hello. Diagnóstico do Azure pode usar o serviço de Blob hello ou serviço de tabela hello, dependendo do tipo de saudação de dados. Os logs de Eventos do Windows são armazenados em formato de Tabela.

2. Transferência de dados de saudação. Você pode solicitar dados de diagnóstico de saudação tootransfer por meio do arquivo de configuração de saudação. Para o SDK 2.4 e anterior, você também pode fazer solicitação Olá programaticamente.

3. Exibir dados hello, usando [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Server Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) no Visual Studio, ou [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) no estúdio de gerenciamento do Azure.

Para obter mais informações sobre como tooperform essas etapas, consulte [armazenar e exibir dados de diagnóstico no armazenamento do Azure.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Análise do Armazenamento do Azure 

Análise de armazenamento registra informações detalhadas sobre o serviço de armazenamento de tooa de solicitações bem-sucedidas e com falha. Essas informações podem ser solicitações individuais toomonitor usados, que podem ajudar a acessar toopersonal dados armazenados no serviço de saudação de documentação. No entanto, o log da Análise de Armazenamento não está habilitado por padrão na conta de armazenamento. Você pode habilitá-lo no portal do Azure de saudação.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Como fazer para configurar o monitoramento de uma conta de armazenamento?

monitoramento de tooconfigure para uma conta de armazenamento, Olá a seguir:

1. Selecione **contas de armazenamento** em Olá portal do Azure, selecione Olá nome da conta de saudação que você deseja toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. Em Olá **monitoramento** seção, selecione **diagnóstico.**

3.  Selecione Olá **tipo** de dados de métricas, você deseja toomonitor para cada serviço (arquivo de Blob, tabela). logs de diagnóstico de toosave tooinstruct armazenamento do Azure para leitura, gravação e exclusão de solicitações para Olá blob, tabela e serviços de fila, selecione **logs de Blob, tabela de logs** e **fila de logs.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Usando o controle deslizante de saudação na parte inferior do hello, defina Olá **retenção** política em dias (valor de 1 a 365). Sete dias é o padrão de saudação.

5. Selecione **salvar** tooapply definições de configuração de saudação.

Entradas de log do log de armazenamento contêm Olá informações sobre solicitações individuais a seguir:

- Informações de tempo, como a hora de início, latência de ponta a ponta e latência de servidor.

- Detalhes da operação de armazenamento hello como o tipo de operação hello, chave de saudação do cliente de saudação do objeto de armazenamento de saudação está acessando, sucesso ou falha e código de status HTTP Olá retornado toohello cliente.

- Detalhes de autenticação, como o tipo de saudação do cliente de saudação de autenticação usado.

- Informações de simultaneidade, como Olá valor de ETag e carimbo de hora da última modificação.

- tamanhos de saudação de mensagens de solicitação e resposta de saudação.

Para obter mais instruções sobre como tooenable análise de armazenamento de log, consulte [monitorar uma conta de armazenamento Olá portal do Azure.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Central de Segurança do Azure 

[Central de segurança do Azure](https://azure.microsoft.com/services/security-center/) monitores Olá estado de segurança de seus recursos do Azure em ordem tooprevent detectar ameaças e fornece recomendações para responder. Ele fornece várias maneiras de documento de toohelp suas medidas de segurança que proteger a saudação privacidade dos dados pessoais.

O monitoramento da integridade da segurança ajuda a garantir a conformidade com as políticas de segurança. Monitoramento de segurança é uma estratégia proativa que auditorias de seus sistemas de tooidentify de recursos que não atendem aos padrões organizacionais ou práticas recomendadas. Você pode monitorar o estado de segurança Olá Olá recursos a seguir:

- Computação (máquinas virtuais e serviços de nuvem)

- Rede (redes virtuais)

- Armazenamento e dados (auditoria de servidor e banco de dados e detecção de ameaças, TDE, criptografia de armazenamento)

- Aplicativos (problemas potenciais de segurança)

Problemas de segurança em qualquer uma dessas categorias podem representar uma privacidade toohello de ameaça dos dados pessoais.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Como exibir o estado de segurança Olá meus recursos do Azure?

Central de segurança periodicamente analisa o estado de segurança Olá seus recursos do Azure. Você pode exibir as possíveis vulnerabilidades de segurança identifica em Olá **prevenção** seção do painel de saudação.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. Em Olá **prevenção** seção, selecione Olá **de computação** lado a lado. Você verá aqui um **visão geral,** juntamente com hello **máquinas virtuais** listagem de todas as máquinas virtuais e seus estados de segurança e Olá **serviços de nuvem** lista de funções da web e de trabalho monitorados pela Central de segurança.

2. Em Olá **visão geral** guia, a segunda uma recomendação tooview obter mais informações.

3. Em Olá **máquinas virtuais** , selecione uma VM tooview mais detalhes.

Quando a coleta de dados é habilitada na Central de segurança do Azure, Olá Microsoft Monitoring Agent é provisionado automaticamente em todos os existentes e qualquer novo suporte para máquinas virtuais que são implantadas. Os dados coletados por meio desse agente são armazenados em um espaço de trabalho existente do [Log Analytics](https://azure.microsoft.com/services/log-analytics/) associado à sua assinatura ou a um novo espaço de trabalho.

Os [Relatórios de Inteligência contra Ameaças](https://docs.microsoft.com/azure/security-center/security-center-threat-report) são fornecidos pela Central de Segurança. Eles fornecem informações úteis toohelp discernir invasor Olá identidade, objetivos, atuais e históricos campanhas e táticas e ferramentas de ataque procedimentos usados. Informações de mitigação e correção também são incluídas.

Olá principal finalidade desses relatórios de ameaça é toohelp toorespond você efetivamente toohello take imediata de ameaça e ajuda mede o problema de saudação toomitigate posteriormente. informações Olá Olá relatórios também podem ser útil quando você documentar a resposta a incidentes para emissão de relatórios e para fins de auditoria.

Relatórios de inteligência de ameaça Olá são apresentados. Formato PDF, acessado por meio de um link em Olá **relatórios** campo de saudação **suspeito processo executado** folha para cada alerta de segurança na Central de segurança do Azure.

Para obter mais informações sobre como tooview e use Olá relatório de inteligência de ameaça, consulte [o relatório de inteligência de ameaça do Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Próximas etapas:

[Guia de Introdução ao Olá do Active Directory do Azure API de relatório](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[O que é o Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Visão geral do monitoramento no Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Introdução toohello Log de atividades do Azure (vídeo)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
