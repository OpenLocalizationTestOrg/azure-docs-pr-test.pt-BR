---
title: "recomendações de segurança aaaManaging na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como as recomendações na Central de Segurança do Azure ajudam a proteger os recursos do Azure e a cumprir as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Gerenciando recomendações de segurança na Central de Segurança do Azure
Este documento o orienta como recomendações toouse toohelp da Central de segurança do Azure protegem seus recursos do Azure.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Este documento não é um guia passo a passo.
>
>

## <a name="what-are-security-recommendations"></a>O que são recomendações de segurança?
Central de segurança periodicamente analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações. recomendações de saudação orientará você durante processo de saudação do configurando controles de saudação necessário.

## <a name="implementing-security-recommendations"></a>Implementando recomendações de segurança
### <a name="set-recommendations"></a>Definir recomendações
Em [Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md), você aprenderá a:

* Configurar políticas de segurança.
* Habilitar a coleta de dados.
* Escolha quais toosee recomendações como parte de sua política de segurança.

As recomendações de política atuais giram em torno de atualizações do sistema, regras de linha de base, programas antimalware, [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) em sub-redes e em interfaces de rede, auditoria do banco de dados SQL, Transparent Data Encryption do banco de dados SQL e firewalls do aplicativo Web.  [Configurando políticas de segurança](security-center-policies.md) fornece uma descrição de cada opção de recomendação.

### <a name="monitor-recommendations"></a>Monitorar as recomendações
Depois de definir uma política de segurança, Central de segurança analisa o estado de segurança Olá seus recursos tooidentify as vulnerabilidades potenciais. Olá **recomendações** bloco Olá **Central de segurança** folha permite que você saiba o número total de saudação de recomendações identificado pela Central de segurança.

![Bloco Recomendações][1]

detalhes de saudação toosee de cada recomendação:

Selecione Olá **recomendações bloco** em Olá **Central de segurança** folha. Olá **recomendações** folha é aberta.

recomendações de saudação são mostradas em um formato de tabela em que cada linha representa uma recomendação específica. Olá colunas dessa tabela são:

* **Descrição**: explica recomendação hello e o que precisa toobe feito tooaddress-lo.
* **RECURSO**: lista Olá recursos toowhich essa recomendação se aplica.
* **ESTADO**: descreve o estado atual de saudação de recomendação de saudação:
  * **Abra**: recomendação Olá ainda não foram resolvida ainda.
  * **Em andamento**: recomendação hello está sendo aplicada toohello recursos, e nenhuma ação é necessária por você.
  * **Resolvido**: recomendação Olá já foi concluída (nesse caso, linha hello está esmaecida).
* **SEVERIDADE**: descreve severidade Olá essa recomendação específica:
  * **Alta**: existe uma vulnerabilidade em um recurso significativo (como um aplicativo, uma VM ou um grupo de segurança de rede) e ela requer atenção.
  * **Médio**: existe uma vulnerabilidade e não críticos ou mais etapas são necessária tooeliminate ou toocomplete um processo.
  * **Baixa**: existe uma vulnerabilidade que deve ser resolvida, mas não exige atenção imediata. (Por padrão, não são apresentadas recomendações baixas, mas você pode filtrar em recomendações baixas se você quiser toosee-las.)

Uso tabela Olá abaixo como uma referência toohelp entender recomendações disponível hello e o que faz cada uma se você aplicá-lo.

> [!NOTE]
> Você desejará Olá toounderstand [clássico e modelos de implantação do Gerenciador de recursos](../azure-classic-rm.md) para recursos do Azure.
>
>

| Recomendações | Descrição |
| --- | --- |
| [Habilitar coleta de dados para assinaturas](security-center-enable-data-collection.md) |Recomenda-se de que você ativar a coleta de dados na política de segurança Olá para cada uma das suas assinaturas e todas as máquinas virtuais (VMs) em suas assinaturas. |
| [Corrigir as vulnerabilidades do sistema operacional](security-center-remediate-os-vulnerabilities.md) |Recomenda que você alinhe suas configurações de sistema operacional com hello recomendado regras de configuração, por exemplo, não permita toobe senhas salva. |
| [Aplicar atualizações do sistema](security-center-apply-system-updates.md) |Recomenda que você implante tooVMs atualizações críticas e segurança de sistema ausente. |
| [Aplicar um controle de acesso à rede Just-In-Time](security-center-just-in-time.md) | Recomenda que você aplique acesso à VM just in time. Olá apenas no recurso de tempo está no modo de visualização e disponível no hello camada padrão da Central de segurança. Consulte [preços](security-center-pricing.md) camadas de preços do toolearn mais sobre o Centro de segurança. |
| [Reinicializar após as atualizações do sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomenda que você reinicialize um processo de saudação do VM toocomplete de aplicação de atualizações do sistema. |
| [Adicione um firewall do aplicativo Web](security-center-add-web-application-firewall.md) |Recomenda que você implante um WAF (firewall do aplicativo Web) para pontos de extremidade da Web. Uma recomendação WAF é mostrada para qualquer IP voltado para uso público (IP de nível de instância ou IP de balanceamento de carga) que tem um grupo de segurança de rede associado com portas de entrada da Web abertas (80,443). </br>Central de segurança recomenda que você provisionar um toohelp WAF se proteger contra ataques direcionados a seus aplicativos web em máquinas virtuais e no ambiente de serviço de aplicativo. Um ASE (Ambiente do Serviço de Aplicativo) é uma opção do plano de serviço [Premium](https://azure.microsoft.com/pricing/details/app-service/) do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo do Azure. toolearn mais sobre ASE, consulte Olá [documentação do ambiente de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).</br>Você pode proteger vários aplicativos web na Central de segurança adicionando esses aplicativos tooyour WAF as implantações existentes. |
| [Finalizar a proteção do aplicativo](security-center-add-web-application-firewall.md#finalize-application-protection) |configuração de saudação toocomplete de um WAF, o tráfego deve ser redirecionado toohello WAF dispositivo. Seguir essa recomendação conclui as alterações de configuração necessárias hello. |
| [Adicionar um Firewall de Última Geração](security-center-add-next-generation-firewall.md) |Recomenda que você adicione um Firewall de próxima geração (NGFW) de um tooincrease de parceiro Microsoft suas proteções de segurança. |
| [Rotear o tráfego apenas através do NGFW](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Recomenda que você configure regras de grupo (NSG) de segurança de rede que forçar o tráfego de entrada tooyour VM por meio de seu NGFW. |
| [Instalar proteção do ponto de extremidade](security-center-install-endpoint-protection.md) |Recomenda-se de que você forneça antimalware programas tooVMs (VMs do Windows somente). |
| [Resolver alertas de integridade do Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomenda que você resolva falhas do Endpoint Protection. |
| [Habilitar Grupos de Segurança de Rede em sub-redes ou máquinas virtuais](security-center-enable-network-security-groups.md) |Recomenda que você habilite NSGs em sub-redes ou VMs. |
| [Restringir o acesso por meio de ponto de extremidade para a Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recomenda que você configure regras de tráfego de entrada para NSGs. |
| [Habilitar a detecção de ameaças e auditoria em servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomenda que você ative a detecção de ameaças e a auditoria para servidores SQL do Azure. (Apenas o serviço do SQL Azure. Não inclui o SQL em execução nas suas máquinas virtuais.) |
| [Habilitar a detecção de ameaças e auditoria em bancos de dados SQL](security-center-enable-auditing-on-sql-databases.md) |Recomenda que você ative a detecção de ameaças e a auditoria para Bancos de Dados SQL do Azure. (Apenas o serviço do SQL Azure. Não inclui o SQL em execução nas suas máquinas virtuais.) |
| [Habilitar Transparent Data Encryption em bancos de dados SQL](security-center-enable-transparent-data-encryption.md) |Recomenda que você habilite a criptografia para bancos de dados SQL. (Apenas o serviço do Azure SQL.) |
| [Habilitar o Agente de VM](security-center-enable-vm-agent.md) |Permite que você toosee que exigem VMs Olá agente de VM. Olá VM Agent deve ser instalado em VMs tooprovision patch de varredura, verificação de linha de base e os programas antimalware. Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace. artigo Olá [agente de VM e extensões – parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente de VM. |
| [Aplicar a criptografia de disco](security-center-apply-disk-encryption.md) |Recomenda de que você criptografe os discos de VM usando o Azure Disk Encryption (VMs do Windows e do Linux). Criptografia é recomendada para Olá SO e os volumes de dados na sua VM. |
| [Fornecer detalhes de contato de segurança](security-center-provide-security-contact-details.md) |Recomenda que você forneça informações de contato de segurança para cada uma das suas assinaturas. Informações de contato são um número de telefone e um endereço de email. Olá, informações são usado toocontact se encontra de nossa equipe de segurança que os recursos sejam comprometidos. |
| [Atualizar a versão do sistema operacional](security-center-update-os-version.md) |Recomenda que você atualize a versão de sistema operacional (SO) Olá para seu serviço de nuvem toohello versão mais recente disponível para a família de sistemas operacionais.  toolearn mais sobre serviços de nuvem, consulte Olá [visão geral dos serviços de nuvem](../cloud-services/cloud-services-choose-me.md). |
| [Avaliação de vulnerabilidade não instalada](security-center-vulnerability-assessment-recommendations.md) |Recomenda que você instale uma solução de avaliação de vulnerabilidade na VM. |
| [Corrigir vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Permite que você toosee sistema e do aplicativo vulnerabilidades detectadas pela solução de avaliação de vulnerabilidade Olá instalada na sua VM. |
| [Habilitar a criptografia para a Conta de Armazenamento do Azure](security-center-enable-encryption-for-storage-account.md) | Recomenda a habilitação da Criptografia do Serviço de Armazenamento do Azure para dados em repouso. Criptografia de serviço de armazenamento (SSE) funciona criptografando dados hello quando ele é gravado tooAzure armazenamento e descriptografa antes da recuperação. SSE está disponível somente para Olá serviço Blob do Azure e pode ser usado para blobs de bloco, blobs de página e blobs de acréscimo. mais, consulte toolearn [criptografia do serviço de armazenamento de dados em repouso](../storage/common/storage-service-encryption.md).</br>A SSE tem suporte apenas nas contas de armazenamento do Resource Manager. |

Você pode filtrar e ignorar as recomendações.

1. Selecione **filtro** em Olá **recomendações** folha. Olá **filtro** folha é aberto e você selecionar valores de severidade e estado de saudação desejar toosee.

    ![Recomendações de filtro][2]
2. Se você determinar que uma recomendação não é aplicável, você poderá ignorar Olá recomendação e, em seguida, filtrá-los fora da sua exibição. Há dois toodismiss de maneiras uma recomendação. Uma maneira é tooright clique em um item e, em seguida, selecione **ignorar**. Olá outros é toohover sobre um item, clique em pontos Olá três exibidas toohello direita e, em seguida, selecione **ignorar**. Você pode exibir as recomendações ignoradas ao clicar em **Filtro** e selecionar **Ignoradas**.

    ![Ignorar recomendação][3]

### <a name="apply-recommendations"></a>Aplicar recomendações
Depois de examinar todas as recomendações, decida qual delas aplicar primeiro. É recomendável que você use a classificação de severidade hello como Olá tooevaluate parâmetro principal que recomendações devem ser aplicadas primeiro.

Na tabela de saudação das recomendações acima, selecione uma recomendação e examiná-lo como um exemplo de como tooapply uma recomendação.

## <a name="next-steps"></a>Próximas etapas
Neste documento, você foram introduzidas toosecurity recomendações na Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
