---
title: "aaaAzure segurança de dados do Centro de segurança | Microsoft Docs"
description: "Este documento explica como os dados são gerenciados e protegidos na Central de Segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Segurança dos Dados da Central de Segurança do Azure
impedir que clientes toohelp, detectam e respondem toothreats, Central de segurança do Azure coleta e processa os dados relacionados à segurança, incluindo informações de configuração, metadados, logs de eventos, os arquivos de despejo de falha e muito mais. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço.

Este artigo explica como os dados são gerenciados e protegidos na Central de Segurança do Azure.

>[!NOTE] 
>A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Fontes de dados
Central de segurança do Azure analisa dados de saudação visibilidade de tooprovide fontes a seguir em seu estado de segurança, identificar vulnerabilidades recomendável atenuações e detectar ameaças ativas:

- Os serviços do Azure: Usa informações sobre a configuração de saudação de serviços do Azure que você implantou comunicando-se com o provedor de recursos do serviço.
- Tráfego da Rede: usa os metadados do tráfego da rede de exemplo a partir da infraestrutura da Microsoft, como a origem/IP de destino/porta, tamanho do pacote e protocolo da rede.
- Soluções de Parceiros: usa alertas de segurança das soluções de parceiros integradas, como firewalls e soluções antimalware. 
- Suas Máquinas Virtuais e Servidores: usa as informações da configuração e informações sobre os eventos de segurança, como eventos do Windows e logs de auditoria, logs do IIS, mensagens do syslog e arquivos de despejo corrompidos de suas máquinas virtuais. Além disso, quando um alerta é criado, Central de segurança do Azure pode gerar um instantâneo do disco VM Olá afetado e extrair o alerta de toohello relacionados de artefatos de máquina do disco VM hello, como um arquivo de registro, para fins de análise forense.


## <a name="data-protection"></a>Proteção de dados
**Diferenciação de dados**: dados são mantidos separados logicamente em cada componente serviço hello. Todos os dados são marcados por organização. Essa marcação persiste em todo o ciclo de vida de dados de saudação e é imposta em cada camada de serviço hello.

**Acesso a dados**: no pedido tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, o pessoal da Microsoft pode acessar as informações coletadas ou analisados pelos serviços do Azure, incluindo arquivos de despejo de falha, processar eventos de criação de VM instantâneos de disco e artefatos, que podem incluir acidentalmente os dados do cliente ou dados pessoais de suas máquinas virtuais. Cumprimento toohello [política de privacidade e termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), qual estado que Microsoft não será usar dados de cliente ou derivar informações dele para fins comerciais propaganda ou semelhantes. Somente usamos os dados do cliente como necessário tooprovide você com o Azure de serviços, incluindo fins compatível com o fornecimento desses serviços. Você mantém todos os direitos tooCustomer dados.

**Use dados**: a Microsoft usa os padrões e inteligência de ameaça Vista em vários locatários tooenhance nossos recursos de detecção e prevenção; fazemos acordo com os compromissos de privacidade de saudação descritos em nosso [privacidade Instrução](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Local dos dados

**Seu espaço**: um espaço de trabalho é especificado para Olá áreas a seguir, e os dados coletados de suas máquinas virtuais do Azure, incluindo os despejos de memória e alguns tipos de dados de alerta, são armazenados no hello mais próximo do espaço de trabalho. 

| Replicação geográfica de VM                        | Replicação Geográfica do Espaço de Trabalho |
|-------------------------------|---------------|
| Estados Unidos, Brasil, Canadá | Estados Unidos |
| Europa, Reino Unido        | Europa        |
| Pacífico Asiático, Japão, Índia    | Pacífico Asiático  |
| Austrália                     | Austrália     |

 
Instantâneos de disco VM são armazenados em Olá mesma conta de armazenamento como discos VM hello.
 
Para máquinas virtuais e servidores que executam em outros ambientes, por exemplo, no local, você pode especificar espaço de trabalho hello e região onde os dados coletados são armazenados. 

**Armazenamento central de segurança do Azure**: informações sobre alertas de segurança, incluindo alertas de parceiro são armazenados regional de acordo com o local de toohello de saudação relacionadas a recursos do Azure, enquanto que informações sobre o status de integridade de segurança e recomendação está armazenada centralmente em Olá Brasil ou Europa, de acordo com o local do toocustomer.
A Central de Segurança do Azure coleta as cópias transitórias dos seus arquivos de despejo corrompidos e analisa-as para obter evidências das tentativas de exploração e comprometimentos bem-sucedidos. Central de segurança do Azure executa essa análise no hello mesma área geográfica como Olá espaço de trabalho e exclusões Olá cópias efêmeras quando a análise for concluída.

Artefatos de máquina são armazenados centralmente no hello mesma região como Olá VM. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gerenciar a coleta de dados das máquinas virtuais

Quando você escolhe habilitar a Central de Segurança no Azure, a coleta de dados é ativada para cada uma de suas assinaturas do Azure. Você também pode ativar a coleta de dados para suas assinaturas em Olá seção de política de segurança da Central de segurança do Azure. Quando a coleta de dados é ativada, Central de segurança do Azure provisiona Olá Microsoft Monitoring Agent em todas as existentes suporte para máquinas virtuais do Azure e os novos que são criados. agente do Microsoft Monitoring Olá procura segurança várias configurações e eventos relacionados em [de rastreamento de eventos do Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) rastreamentos (ETW). Além disso, sistema operacional de saudação gerará eventos de log de eventos durante Olá Olá máquina em execução. Exemplos desses dados são: tipo e versão do sistema operacional, logs do sistema operacional (logs de eventos do Windows), processos em execução, nome do computador, endereços IP, usuário registrado e ID do locatário. Olá Microsoft Monitoring Agent lê as entradas do log de eventos e rastreamentos ETW e os copia tooyour espaço para análise. Olá Microsoft Monitoring Agent também copia o espaço de tooyour de arquivos de despejo de falha.

Se você estiver usando livre de Central de segurança do Azure, você também pode desativar a coleta de dados de máquinas virtuais em Olá política de segurança. Coleta de dados é necessária para as assinaturas na camada padrão hello. Os instantâneos de disco da VM e a coleção de artefatos ainda serão habilitados mesmo que a coleta de dados tenha sido desabilitada.


## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como os dados são gerenciados e protegidos na Central de Segurança do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte:

* [Planejamento da Central de segurança do Azure e guia de operações](security-center-planning-and-operations-guide.md) — Saiba como tooplan e entender a Central de segurança do hello design considerações tooadopt do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure
