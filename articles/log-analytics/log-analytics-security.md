---
title: "segurança de dados de análise de aaaLog | Microsoft Docs"
description: Saiba mais sobre como o Log Analytics protege a sua privacidade e seus dados.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Segurança de dados do Log Analytics
Microsoft é confirmada tooprotecting sua privacidade e segurança de dados, oferecendo softwares e serviços que ajudam a gerenciar Olá infraestrutura de TI da sua organização. Reconhecemos que quando você entrega seus dados tooothers, essa confiança requer segurança rigorosa. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço.

Segurança e proteção de dados é uma prioridade principal da Microsoft. Entre em contato conosco com perguntas, sugestões ou problemas sobre qualquer Olá seguintes informações, incluindo nossas políticas de segurança em [opções de suporte do Azure](http://azure.microsoft.com/support/options/).

Este artigo explica como os dados são coletados, processados e protegidos pela análise de Log Olá Operations Management Suite (OMS). Você pode usar agentes tooconnect toohello web service, use dados operacionais do System Center Operations Manager toocollect ou recuperar dados de diagnóstico do Azure para uso pela análise de Log. Hello os dados coletados são enviados pela Internet de saudação usando a autenticação baseada em certificado & SSL 3 toohello serviço de análise de Log, que é hospedado no Microsoft Azure. Dados são compactados pelo agente de saudação antes de serem enviado.

saudação de serviço de análise de Log gerencia seus dados baseados em nuvem com segurança usando Olá métodos a seguir:

* segregação de dados
* retenção de dados
* segurança física
* gerenciamento de incidentes
* conformidade
* certificações de padrões de segurança

## <a name="data-segregation"></a>Segregação de dados
Os dados do cliente são mantidos separados logicamente em cada componente Olá serviço OMS. Todos os dados são marcados por organização. Essa marcação persiste em todo o ciclo de vida de dados de saudação e é imposta em cada camada de serviço hello. Cada cliente tem um blob do Azure dedicado que hospeda os dados de longo prazo Olá

## <a name="data-retention"></a>Retenção de dados
Dados indexados de pesquisa de log são armazenados e retidos de acordo tooyour preços do plano. Para obter mais informações, consulte [Preços do Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft exclui os dados do cliente 30 dias depois que o espaço de trabalho do hello OMS é fechado. Microsoft também exclui Olá onde residem os dados de saudação de conta de armazenamento do Azure. Quando os dados do cliente são removidos, não ocorre a destruição de nenhuma unidade física.

Olá, a tabela a seguir lista algumas das soluções disponíveis de saudação do OMS e exemplos Olá tipos de dados coletados.

| **Solução** | **Tipos de dados** |
| --- | --- |
| Avaliação de Configuração |Dados de configuração, metadados e dados de estado |
| Planejamento da capacidade |Dados de desempenho e metadados |
| Antimalware |Dados de configuração e metadados |
| Avaliação de atualização do sistema |Metadados e dados de estado |
| Gerenciamento de Log |Logs de eventos de definidos pelo usuário, logs de eventos do Windows e/ou os logs do IIS |
| Controle de Alterações |Inventário de software e metadados do serviço Windows |
| Avaliação do SQL e Active Directory |Dados WMI, dados do registro, dados de desempenho e resultados de exibição do gerenciamento dinâmico do SQL Server |

Olá, a tabela a seguir mostra exemplos de tipos de dados:

| **Tipo de dados** | **Campos** |
| --- | --- |
| Alerta |Nome do Alerta, Descrição do Alerta, BaseManagedEntityId, ID do Problema, IsMonitorAlert, RuleId, ResolutionState, Prioridade, Gravidade, Categoria, Proprietário, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configuração |CustomerID, AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Evento |EventId, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, Number, Categoria, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Observação:** ao gravar eventos com campos personalizados no log de eventos do Windows toohello, o OMS os coleta. |
| Metadados |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Address, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Desempenho |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Estado |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Segurança física
saudação de análise de Log no serviço OMS é operada pelos funcionários da Microsoft e todas as atividades são registradas e podem ser auditadas. serviço de saudação é executado totalmente no Azure e está em conformidade com hello critérios de engenharia comuns do Azure. Você pode exibir detalhes sobre Olá a segurança física dos ativos do Azure na página 18 da saudação [visão geral de segurança do Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Áreas de toosecure de direitos de acesso físico são alteradas em um dia útil para qualquer pessoa que não tem a responsabilidade de serviço do OMS hello, incluindo transferência e término. Você pode ler sobre a infraestrutura física global Olá usamos em [Datacenters da Microsoft](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Gerenciamento de incidentes
O OMS tem um processo de gerenciamento de incidentes que todos os serviços Microsoft seguem. toosummarize, nós:

* Use um modelo de responsabilidade compartilhada em que uma parte de responsabilidade de segurança pertence tooMicrosoft e uma parte pertence toohello cliente
* Gerenciamos incidentes de segurança do Azure
  * Início de uma investigação sobre a detecção de um incidente
  * Avalie o impacto de saudação e a gravidade de um incidente por um membro da equipe de resposta a incidentes na chamada. Com base na evidência, avaliação de saudação pode ou não pode resultar em mais escalonamento toohello resposta equipe de segurança.
  * Diagnosticar um incidente por resposta especialistas tooconduct Olá forense ou técnica investigação de segurança, identificar estratégias de contenção e redução de solução alternativa. Se a equipe de segurança Olá suspeitar de que os dados do cliente podem ter ficado exposto tooan ilegal ou não autorizado execução paralela individual dos Olá processo de notificação de incidentes do cliente começa em paralelo.  
  * Estável e recuperar de incidente hello. equipe de resposta a incidentes Olá cria um problema de saudação de toomitigate de plano de recuperação. As etapas de contenção de crise, como colocar os sistemas afetados em quarentena, podem ocorrer imediatamente e em paralelo com o diagnóstico. Reduções de prazo mais longo podem ser planejadas que ocorrem após o risco de imediato saudação passou.  
  * Fechar o incidente hello e realizar um post-mortem. equipe de resposta a incidentes Olá cria um post-mortem que descreve os detalhes de saudação do hello incidente, com políticas de toorevise intenção hello, procedimentos e processos tooprevent uma recorrência de evento de saudação.
* Notificamos os clientes dos incidentes de segurança
  * Determine o escopo de saudação de clientes afetados e tooprovide qualquer pessoa que é afetado detalhadas de um aviso de possível
  * Crie um aviso tooprovide clientes com informações detalhadas suficiente para que eles possam realizar uma investigação do seu lado e atender aos compromissos feitas aos usuários finais de tootheir enquanto não indevidamente atrasando o processo de notificação de saudação.
  * Confirme e declare o incidente hello, conforme necessário.
  * Notificamos os clientes com uma notificação de incidentes sem demora excessiva e acordo com qualquer compromisso contratual ou legal. As notificações de incidentes de segurança são entregues tooone ou mais dos administradores do cliente por qualquer meio seleciona da Microsoft, inclusive por meio de email.
* Conduzimos o treinamento e a prontidão de equipe
  * Funcionários da Microsoft são necessárias toocomplete segurança e treinamento de reconhecimento, que ajuda a tooidentify e relatório suspeitar de problemas de segurança.  
  * Operadores que trabalham em Olá serviço Microsoft Azure tem obrigações de treinamento de adição ao redor de seus sistemas de toosensitive de acesso que hospeda os dados do cliente.
  * A equipe de resposta de segurança da Microsoft recebe treinamento especializado para suas funções

Caso haja uma perda de dados de qualquer cliente, notificamos cada cliente dentro de um dia. No entanto, a perda de dados do cliente nunca ocorreu com o OMS. Além disso, mantemos cópias dos dados que foram criados e eles são distribuídos geograficamente.

Para obter mais informações sobre como a Microsoft responde toosecurity incidentes, consulte [resposta de segurança do Microsoft Azure na nuvem de saudação](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Conformidade
Olá segurança das informações do OMS software serviço e desenvolvimento da equipe e o programa de controle dá suporte a seus requisitos de negócios e cumpre as normas e toolaws conforme descrito em [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) e [Conformidade Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Como o OMS estabelece os requisitos de segurança, identifica os controles de segurança, gerencia e monitora os riscos também são descritos lá. Anualmente, revisamos as políticas, padrões, procedimentos e diretrizes.

Cada membro de equipe de desenvolvimento do OMS recebe treinamento formal sobre a segurança de aplicativo. Internamente, usamos um sistema de controle de versão para o desenvolvimento de software. Cada projeto de software é protegido pelo sistema de controle de versão de saudação.

A Microsoft tem uma equipe de segurança e conformidade que monitora e analisa todos os serviços na Microsoft. Gerentes de segurança de informações Olá equipe e não estão associados com hello engenharia departamentos que desenvolve OMS. os responsáveis pela segurança de saudação têm seu próprios cadeia de gerenciamento e conduzir independentes avaliações de conformidade e segurança tooensure dos serviços e produtos.

O conselho de diretores da Microsoft é notificado por um relatório anual sobre todos os programas de segurança da informação na Microsoft.

equipe de serviço e desenvolvimento de software OMS do Hello está trabalhando ativamente com as equipes de conformidade e Legal da Microsoft hello e outros tooacquire de parceiros do setor várias certificações.

## <a name="certifications-and-attestations"></a>Certificações e atestados
Análise de logs do OMS atende Olá requisitos a seguir:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Pagamento cartão Industry (PCI compatíveis) Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) por Olá PCI Security Standards Council.
* Compatível com [SOC (Service Organization Controls) 1 Tipo 1 e SOC 2 Tipo 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2)
* [HIPAA e HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) para empresas que tenham um contrato de sócio corporativo HIPAA
* Critérios de engenharia comum do Windows
* Microsoft Trustworthy Computing (a página pode estar em inglês)
* Como um serviço do Azure, componentes de saudação usados pelo OMS aderem tooAzure requisitos de conformidade. Você pode ler mais em [Conformidade do Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> Em algumas certificações/atestados, o Log Analytics está listado com o nome antigo de *Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Fluxo de dados de segurança de computação em nuvem
Olá diagrama a seguir mostra uma arquitetura de segurança de nuvem como Olá fluxo de informações de sua empresa e como ela é protegida ao se move o serviço de análise de Log toohello, visto por você no portal do OMS hello. Para obter mais informações sobre cada etapa após o diagrama de saudação.

![Imagem de coleta de dados e segurança da OMS](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Inscrever-se no Log Analytics e coletar dados
Para sua organização toosend dados tooLog análise, você deve configurar agentes do Windows, os agentes em execução em máquinas virtuais do Azure ou agentes do OMS para Linux. Se você usar agentes do Operations Manager, você usar um Assistente de configuração em Olá Operations console tooconfigure-los. Usuários (que podem ser você, outros usuários individuais ou um grupo de pessoas) criar uma ou mais contas da OMS (espaços de trabalho do OMS) e registrar os agentes usando uma saudação contas a seguir:

* [ID Organizacional](../active-directory/sign-up-organization.md)
* [Conta da Microsoft - Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Um espaço de trabalho do OMS é onde os dados são coletados, agregados, analisados e apresentados. Um espaço de trabalho é usado principalmente como um meio de dados toopartition, e cada espaço de trabalho é exclusivo. Por exemplo, convém toohave seus dados de produção gerenciados com um espaço de trabalho do OMS e seus dados de teste gerenciados com outro espaço de trabalho. Espaços de trabalho também ajudam um dados de toohello de acesso do usuário de controle do administrador. Cada espaço de trabalho pode ter várias contas de usuário associadas a ele, e cada conta de usuário pode acessar vários espaços de trabalho do OMS. Você cria os espaços de trabalho com base na região do datacenter. Cada espaço de trabalho é replicado tooother datacenters em região hello, principalmente para disponibilidade do serviço OMS.

Para o Operations Manager, quando o Assistente de configuração de saudação for concluído, cada grupo de gerenciamento do Operations Manager estabelece uma conexão com o serviço de análise de Log de hello. Você usa toochoose do Assistente para adicionar computadores Olá quais computadores no grupo de gerenciamento de saudação são permitidos toosend serviço de toohello de dados. Para outros tipos de agente, cada uma se conecta com segurança toohello serviço do OMS.

Toda a comunicação entre sistemas conectados e hello serviço de análise de Log é criptografada.  Olá TLS protocolo (HTTPS) é usado para criptografia.  Olá processo SDL da Microsoft é seguido tooensure análise de Log está atualizado com os avanços mais recentes Olá em protocolos de criptografia.

Cada tipo de agente coleta dados para o Log Analytics. tipo de saudação de dados que são coletados é depende de tipos de saudação de soluções usadas. Você pode ver um resumo de coleta de dados em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md). Além disso, há informações mais detalhadas de coleção disponíveis para a maioria das soluções. Uma solução é um conjunto de exibições predefinidas, de consultas de pesquisa de log, de regras de coleta de dados e de lógica de processamento. Somente os administradores podem usar uma solução de tooimport de análise de Log. Após a importação da solução Olá, é movido toohello servidores de gerenciamento do Operations Manager (se usado) e, em seguida, os agentes de tooany que você escolheu. Depois disso, agentes Olá coletam dados de saudação.

## <a name="2-send-data-from-agents"></a>2. Enviar dados de agentes
Registre todos os tipos de agente com uma chave de registro e uma conexão segura é estabelecida entre o agente de saudação e serviço de análise de Log de saudação usando autenticação baseada em certificado e SSL com a porta 443. Usa um toogenerate armazenamento secreto do OMS e manter as chaves. As chaves privadas são giradas a cada 90 dias e são armazenadas no Azure e são gerenciadas pelo hello Azure operações que seguem estritas práticas normativas e de conformidade.

Com o Operations Manager, registre um espaço de trabalho com o serviço de análise de Log hello e uma conexão HTTPS segura é estabelecida entre o servidor de gerenciamento do Operations Manager Olá.

Para agentes do Windows em execução em máquinas virtuais do Azure, uma chave de armazenamento somente leitura é eventos de diagnóstico tooread usados nas tabelas do Azure.

Se qualquer agente toocommunicate não é possível toohello serviço por algum motivo, hello dados coletados são armazenados localmente em um cache temporário e o servidor de gerenciamento Olá tenta tooresend dados de saudação a cada oito minutos por duas horas. dados armazenados em cache do agente Olá são protegidos pelo armazenamento de credenciais do sistema de operacional hello. Se o serviço de saudação não pode processar dados saudação após duas horas, os agentes de saudação colocará em fila dados saudação. Se a fila de saudação fica cheio, OMS inicia descartando tipos de dados, começando com os dados de desempenho. limite de fila do agente de saudação é uma chave do registro para que possa modificá-lo, se necessário. Os dados coletados são compactados e enviados serviço toohello, ignorando os bancos de dados local, para que ele não adicione qualquer carga toothem. Após a coleta de saudação dado é enviado, ele é removido do cache de saudação.

Conforme descrito acima, os dados de seus agentes são enviados pela SSL tooMicrosoft datacenters do Azure. Opcionalmente, você pode usar o ExpressRoute tooprovide adicionais de segurança para dados de saudação. Rota expressa é uma maneira toodirectly conectar tooAzure da sua rede WAN existente, como um multi-protocolo de label switching (MPLS) VPN, fornecido por um provedor de serviço de rede. Para obter mais informações, consulte [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. Olá o serviço de análise de Log recebe e processa os dados
saudação de serviço de análise de Log assegura que os dados de entrada são de uma fonte confiável ao validar certificados e a integridade dos dados de saudação com a autenticação do Azure. Olá dados brutos não processados são armazenados como um blob em [armazenamento do Microsoft Azure](../storage/common/storage-introduction.md) e não está criptografado. No entanto, cada blob de armazenamento do Azure tem um conjunto de conjunto exclusivo de chaves, que é acessível toothat único usuário. tipo Hello dos dados armazenados depende de tipos de saudação de soluções que foram importados e usados toocollect dados. Em seguida, Olá serviço de análise de Log processa dados brutos de saudação de blob de armazenamento do Azure hello.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Usar dados de saudação do tooaccess de análise de Log
Você pode entrar tooLog análise no portal do OMS hello usando a conta organizacional hello ou conta da Microsoft que você configurou anteriormente. Todo o tráfego entre o portal do OMS hello e análise de logs do OMS é enviado por um canal HTTPS seguro. Ao usar o portal do OMS hello, uma ID de sessão é gerada no cliente de usuário da saudação (navegador da web) e dados são armazenados em um cache local até Olá sessão seja encerrada. Quando finalizadas, a saudação será excluído. Os cookies do lado do cliente, que não contêm informações de identificação pessoal, não são removidos automaticamente. Os cookies de sessão são marcados como HTTPOnly e são protegidos. Após um período ocioso predeterminado, sessão portal do OMS Olá é encerrada.

Usando o portal do OMS hello, você pode exportar o arquivo de dados de CSV tooa e você pode acessar dados usando APIs de pesquisa. Exportação CSV é limitado too50, 000 linhas por exportação e os dados de API é restrito too5, 000 linhas por pesquisa.

## <a name="next-steps"></a>Próximas etapas
* [Introdução à análise de Log](log-analytics-get-started.md) toolearn mais sobre análise de logs e get em funcionamento em minutos.
