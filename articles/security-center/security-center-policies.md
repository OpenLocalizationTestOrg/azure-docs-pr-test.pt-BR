---
title: "políticas de segurança aaaSet na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda tooconfigure políticas de segurança na Central de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Configurar políticas de segurança na Central de Segurança do Azure
Este documento ajuda tooconfigure políticas de segurança na Central de segurança, guiando você pelas Olá etapas necessárias tooperform essa tarefa.

>[!NOTE] 
>A partir do início de junho de 2017, Central de segurança usa dados de toocollect e armazenamento do Microsoft Monitoring Agent saudação. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>Quais são políticas de segurança?
Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura. Na Central de segurança, você pode definir políticas para suas assinaturas do Azure, de acordo com as necessidades de segurança do tooyour da empresa e o tipo de saudação de aplicativos ou confidencialidade dos dados de saudação em cada assinatura.

Por exemplo, os recursos usados para o desenvolvimento ou teste podem ter requisitos de segurança diferentes daqueles usados para os aplicativos de produção. Da mesma forma, os aplicativos com dados regulamentados, como as informações de identificação pessoal, podem requerer um nível mais alto de segurança. Políticas de segurança que estão habilitadas no recomendações de segurança de unidade do Centro de segurança do Azure e monitoramento toohelp identificar vulnerabilidades potenciais e reduzir as ameaças. Leitura [planejamento do Centro de segurança do Azure e guia de operações](security-center-planning-and-operations-guide.md) para obter mais informações sobre como Olá toodetermine opção são apropriadas para você.

## <a name="set-security-policies"></a>Definir políticas de segurança
É possível configurar políticas de segurança para cada assinatura. toomodify uma política de segurança, você deve ser um proprietário ou colaborador da assinatura. Entre em toohello portal do Azure e siga Olá êxito etapas políticas de segurança tooconfigure na Central de segurança:

1. Clique em Olá **política** bloco no painel de controle do hello Central de segurança.
2. Na folha de política de segurança de saudação que é aberta, selecione assinatura Olá no qual você deseja tooenable política de segurança de saudação.

    ![Definir a política](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Olá **política de segurança** folha para a assinatura de saudação selecionada é aberta com um conjunto de opções. saudação de opções disponíveis nessa folha é:

   * **Política de prevenção de**: usar políticas de tooconfigure essa opção por assinatura.  
   * **Notificação por email**: usar tooconfigure essa opção uma notificação de email é enviada em Olá primeiro diário ocorrência de um alerta e de alertas de gravidade. As preferências do email podem ser configuradas apenas para as políticas da assinatura. Leitura [fornecer detalhes de contato de segurança na Central de segurança do Azure](security-center-provide-security-contact-details.md) para obter mais informações sobre como tooconfigure uma notificação por email.
   * **Camada de preços**: Use essa Olá tooupgrade de opção seleção da camada de preços. Consulte [Central de segurança preços](security-center-pricing.md) toolearn mais sobre opções de preços.
4. Verifique se a opção **Coletar dados das máquinas virtuais** está **Ativada**. Essa opção habilita a coleta de log automático para os recursos novos e existentes usando Olá Microsoft Monitoring Agent – essa é Olá mesmo agente usado pelo serviço de Operations Management Suite e análise de Log de saudação. Dados coletados deste agente são armazenados em um espaço de análise de Log existente associado à sua assinatura do Azure ou em um novo espaço, levando em conta Olá de Geografia de saudação VM.

5. Em Olá **política de segurança** folha, clique em **política de prevenção de** toosee Olá opções disponíveis. Clique em **na** tooenable Olá as recomendações de segurança que são relevantes para esta assinatura.

    ![Seleção de políticas de segurança Olá](./media/security-center-policies/security-center-policies-fig7.png)

Use cada opção de hello como toounderstand uma referência a tabela a seguir:

| Política | Quando o estado está ativado |
| --- | --- |
| Atualizações do sistema |Recupera uma lista diária das atualizações de segurança e críticas do Windows Update ou dos Serviços de Atualização do Windows Server. lista recuperada Olá depende de serviço de saudação que está configurado para a máquina virtual e recomenda que as atualizações ausentes Olá aplicado. Para sistemas Linux, a política de saudação usa Olá pacotes fornecido pelo distribuição sistema toodetermine pacotes de gerenciamento que possuem atualizações disponíveis. Também verifica as atualizações de segurança e críticas das máquinas virtuais dos [Serviços de Nuvem do Azure](../cloud-services/cloud-services-how-to-configure.md). |
| Vulnerabilidades do SO |Analisa configurações diário toodetermine problemas do sistema operacional que podem fazer tooattack vulnerável de máquina virtual de saudação. política de saudação também recomenda tooaddress de alterações de configuração essas vulnerabilidades. Consulte Olá [lista de linhas de base recomendadas](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) para obter mais informações sobre configurações específicas de saudação que estão sendo monitorados. (No momento, não há suporte completo para o Windows Server 2016.) |
| Proteção do ponto de extremidade |Recomenda toobe de proteção de ponto de extremidade provisionado para todas as máquinas virtuais do Windows toohelp identificar e remover vírus, spyware e outros softwares mal-intencionados. |
| Criptografia do disco |Recomenda habilitar a criptografia de disco todas as máquinas virtuais tooenhance proteção de dados em repouso. |
| Grupos de segurança de rede |Recomenda que [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) ser configurado toocontrol de entrada e saída de tráfego tooVMs que têm pontos de extremidade públicos. Os grupos de segurança da rede configurados para uma sub-rede são herdados por todas as interfaces de rede da máquina virtual, a menos que o contrário seja especificado. Além disso toochecking que um grupo de segurança de rede foi configurado, esta política avalia regras de tooidentify de regras de segurança de entrada que permitem o tráfego de entrada. |
| Firewall do aplicativo Web |Recomenda-se de que um firewall do aplicativo web sejam fornecidos em máquinas virtuais quando Olá seguinte for verdadeiro: </br></br>[IP público de nível de instância](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) é usado e regras de segurança de entrada para o grupo de segurança de rede associado Olá hello serão configurado tooallow acesso tooport 80/443.</br></br>Balanceamento de carga IP é usado e Olá associado balanceamento de carga e regras de NAT (conversão) do endereço de rede de entrada serão configurado tooallow acesso tooport 80/443. (Para obter mais informações, consulte [Suporte do Azure Resource Manager para o Balanceador de Carga](../load-balancer/load-balancer-arm.md). |
| Firewall da próxima geração |Estende as proteções da rede para além dos grupos de segurança da rede, que são internos no Azure. Central de segurança detectará implantações para o qual um firewall de geração próximo é recomendado e habilitar tooprovision um dispositivo virtual. |
| Auditoria e detecção de ameaças do SQL |Recomenda que a auditoria de acesso tooAzure banco de dados habilitada para fins de conformidade e também avançada detecção de ameaças, para fins de investigação. |
| Criptografia do SQL |Recomenda que a criptografia em repouso seja habilitada para o Banco de Dados SQL, backups associados e arquivos do log de transação. Mesmo se seus dados sejam violados, eles não poderão ser lidos. |
| Avaliação de vulnerabilidade |Recomenda que você instale uma solução de avaliação de vulnerabilidade na VM. |
| Criptografia do Armazenamento |Atualmente, este recurso está disponível para arquivos e blobs do Azure. Depois de habilitar a Criptografia do Serviço de Armazenamento, apenas os novos dados serão criptografados e quaisquer arquivos existentes nesta conta de armazenamento permanecerão não criptografados. |
| Acesso à Rede JIT |Quando está habilitada no momento, a Central de segurança bloqueia o tráfego de entrada tooyour VMs do Azure, criando uma regra NSG. Selecione as portas de saudação em Olá VM toowhich o tráfego de entrada deve ser bloqueado. Para saber mais, confira [Gerenciar o acesso à máquina virtual usando o just in time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time). |

Depois de configurar todas as opções, clique em **Okey** em Olá **política de segurança** folha que apresenta recomendações hello e, em seguida, clique em **salvar** em Olá **segurança Diretiva** folha que tem configurações de saudação inicial.

> [!NOTE]
> saudação de preço é aplicável para o nível de grupo de recursos de saudação. Para obter mais informações, visite Olá [preços](https://azure.microsoft.com/pricing/details/security-center/) página.
>
>

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como tooconfigure políticas de segurança na Central de segurança do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md). Saiba como tooplan e entender a Central de segurança do hello design considerações tooadopt do Azure.
* [Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md). Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md). Saiba como alertas de toosecurity toomanage e responder.
* [Monitoramento das soluções de parceiros na Central de Segurança do Azure](security-center-partner-solutions.md). Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md). Localize as perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre postagens no blog sobre a conformidade e segurança do Azure.
