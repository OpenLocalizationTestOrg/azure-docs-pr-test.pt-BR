---
title: "Guia de solução de problemas de Central de segurança do aaaAzure | Microsoft Docs"
description: "Este documento ajuda tootroubleshoot problemas na Central de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Guia de solução de problemas da Central de Segurança do Azure
Este guia é para profissionais de TI (tecnologia) de informações, analistas de segurança de informações e os administradores de nuvem cujas organizações estão usando a Central de segurança do Azure e precisam de que problemas relacionados à Central de segurança tootroubleshoot.

>[!NOTE] 
>A partir do início de junho de 2017, Central de segurança usa dados de toocollect e armazenamento do Microsoft Monitoring Agent saudação. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Guia de Solução de Problemas
Este guia explica como a Central de segurança tootroubleshoot de problemas relacionados. A maioria das soluções de problemas de saudação realizadas na Central de segurança ocorre examinando primeiro Olá [Log de auditoria](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) registros para Olá falha no componente. Com os logs de auditoria, você pode determinar:

* Quais operações ocorreram
* Quem iniciou a operação de Olá
* Quando a operação de saudação ocorreu
* status de saudação da operação de saudação
* valores de saudação de outras propriedades que podem ajudá-lo a pesquisar operação Olá

log de auditoria Olá contém todas as operações de gravação (PUT, POST, DELETE) executadas em seus recursos, mas ele não inclui operações de leitura (GET).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Central de segurança usa Olá Microsoft Monitoring Agent – isso é Olá mesmo agente usado pelo serviço de análise de Log – toocollect dados de segurança de suas máquinas virtuais do Azure e Olá Operations Management Suite. Após a coleta de dados está habilitada e agente hello está instalado corretamente no computador de destino Olá, o processo de saudação abaixo deve ser em execução:

* HealthService.exe

Se você abrir o console de gerenciamento de serviços de saudação (services.msc), você também verá Olá Microsoft Monitoring Agent serviço em execução como mostrado abaixo:

![Serviços](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

toosee qual versão do agente Olá tiver, abra **Gerenciador de tarefas**, em Olá **processos** guia Localizar Olá **serviço Microsoft Monitoring Agent**, com o botão direito nela e Clique em **propriedades**. Em Olá **detalhes** guia, procure a versão do arquivo hello conforme mostrado abaixo:

![Arquivo](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Cenários de instalação do Microsoft Monitoring Agent
Há dois cenários de instalação que podem produzir resultados diferentes quando instalar Olá Microsoft Monitoring Agent em seu computador. cenários de saudação com suporte são:

* **Agente instalado automaticamente pela Central de segurança**: neste cenário será capaz de tooview alertas de saudação em locais, a Central de segurança e pesquisa de Log. Você receberá notificações toohello email endereço de email foi configurado na política de segurança Olá para Olá assinatura Olá recurso pertence.
.
* **Agente instalado manualmente em uma máquina virtual localizada no Azure**: nesse cenário, se você estiver usando agentes baixadas e instaladas manualmente anterior tooFebruary 2017, você será tooview capaz de alertas de saudação no portal da Central de segurança de saudação somente se você filtrar Olá espaço de trabalho de saudação assinatura pertence. Caso você filtro no recurso de saudação do hello assinatura pertence, você não será capaz de toosee todos os alertas. Você receberá notificações toohello email endereço de email foi configurado na política de segurança Olá para o espaço de trabalho de saudação do hello assinatura pertence.

>[!NOTE]
> comportamento de saudação tooavoid explicado em hello em segundo lugar, certifique-se de baixar a versão mais recente saudação do agente de saudação.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Solução de problemas de monitoramento de requisitos de rede do agente
Para agentes tooconnect tooand registro com a Central de segurança, eles devem ter acesso de recursos toonetwork, incluindo URLs de domínio e os números de porta de saudação.

- Para servidores proxy, você precisa tooensure que Olá recursos configurados nas configurações do agente de servidor de proxy apropriados. Leia este artigo para obter mais informações sobre [como toochange Olá as configurações de proxy](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Para firewalls que restringem o acesso toohello da Internet, você precisa tooconfigure tooOMS de acesso de toopermit seu firewall. Nenhuma ação é necessária nas configurações do agente.

Olá, a tabela a seguir mostra os recursos necessários para comunicação.

| Recurso de agente | Portas | Ignorar a inspeção de HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sim |
| *.oms.opinsights.azure.com | 443 | Sim |
| *.blob.core.windows.net | 443 | Sim |
| *.azure-automation.net | 443 | Sim |

Se você encontrar problemas de integração com o agente Olá, tornar-se de artigo de saudação tooread [como problemas de integração do Operations Management Suite tootroubleshoot](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Solução de problemas do Endpoint Protection que não está funcionando corretamente

o agente convidado Olá é o processo de pai de saudação de tudo Olá [Antimalware da Microsoft](../security/azure-security-antimalware.md) da extensão. Quando o processo do agente convidado Olá falha, Olá Antimalware da Microsoft que é executado como um processo filho do agente de convidado Olá também poderá falhar.  Em cenários como que é recomendado tooverify Olá as opções a seguir:

- Se o destino de saudação VM é uma imagem personalizada e criador Olá Olá VM nunca instalado agente convidado.
- Se o destino de saudação é uma VM do Linux, em vez de uma VM do Windows, em seguida, instalando a versão do Windows hello da extensão de antimalware Olá em uma VM Linux falhará. Agente de convidado do Linux Olá tem requisitos específicos em termos de versão do sistema operacional e os pacotes necessários e se esses requisitos não forem atendidos Olá VM agent não funcionará lá ou. 
- Se Olá VM foi criada com uma versão antiga do agente convidado. Se ela foi, você deve ser ciente de que alguns agentes antigo poderiam não atualização automática em si versão mais recente do toohello e isso pode causar um problema de toothis. Sempre use a versão mais recente de saudação do agente convidado se criando suas próprias imagens.
- Alguns softwares de terceiros administração podem desabilitar o agente convidado hello, ou bloquear acesso toocertain arquivos locais. Se você tiver instalado na sua VM terceiros, certifique-se de que o agente hello está na lista de exclusão de saudação.
- Determinadas configurações de firewall ou o grupo de segurança de rede (NSG) podem ser bloqueadas tooand de tráfego de rede do agente convidado.
- Algumas ACLs (listas de controle de acesso) podem impedir o acesso ao disco.
- Falta de espaço em disco pode bloquear o agente de convidado Olá funcione corretamente. 

Por saudação padrão Interface de usuário do Microsoft Antimalware está desabilitada, leitura [habilitando Antimalware Interface do usuário Microsoft no Azure Resource Manager VMs pós-implantação](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) para obter mais informações sobre como tooenable se é necessário.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Solução de problemas ao carregar o painel de saudação

Se você tiver problemas ao carregar o painel de Central de segurança hello, certifique-se de usuário Olá que registra Olá assinatura tooSecurity central (ou seja, Olá primeiro usuário que abriu a Central de segurança com assinatura de saudação) e o usuário Olá que gostaria tooturn em coleta de dados deve ser *proprietário* ou *Colaborador* assinatura hello. A partir desse momento também os usuários com *leitor* Olá assinatura possível ver Olá painel/alertas/recomendação/política.

## <a name="contacting-microsoft-support"></a>Entrando em contato com o Suporte da Microsoft
Alguns problemas podem ser identificados usando Olá diretrizes fornecidas neste artigo, outras pessoas, você também pode encontrar documentado em Olá Central de segurança público [fórum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). No entanto, se você precisar de mais solução de problemas, poderá abrir uma nova solicitação de suporte usando o **portal do Azure**, conforme mostrado abaixo: 

![Suporte da Microsoft](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como tooconfigure políticas de segurança na Central de segurança do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Planejamento da Central de segurança do Azure e guia de operações](security-center-planning-and-operations-guide.md) — Saiba como tooplan e entender a Central de segurança do hello design considerações tooadopt do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure

