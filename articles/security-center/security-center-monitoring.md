---
title: "Monitoramento de segurança na Central de Segurança do Azure | Microsoft Docs"
description: "Este artigo o ajuda a se familiarizar com o monitoramento de recursos na Central de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 93fff129afb04e3a1896d275551f585f45658d6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Monitoramento de integridade de segurança na Central de segurança do Azure
Este artigo o ajuda a usar os recursos de monitoramento na Central de segurança do Azure para monitorar a conformidade com as políticas.

## <a name="what-is-security-health-monitoring"></a>O que é o monitoramento de integridade de segurança?
Costumamos pensar em monitoramento como assistir e esperar até que um evento ocorra para poder reagir à situação. Monitoramento de segurança refere-se a ter uma estratégia proativa que audita seus recursos para identificar sistemas que não atendem aos padrões organizacionais ou práticas recomendadas.

## <a name="monitoring-security-health"></a>Monitoramento de integridade da segurança
Depois de habilitar as [políticas de segurança](security-center-policies.md) para os recursos de uma assinatura, a Central de Segurança analisa a segurança de seus recursos para identificar as possíveis vulnerabilidades. Informações sobre a configuração de rede estão disponíveis imediatamente. Pode levar uma hora ou mais para que informações sobre a configuração de máquina virtual, como segurança de atualização de status e configuração do sistema operacional, se tornem disponíveis. Você pode exibir o estado de segurança de seus recursos e quaisquer problemas na seção **Prevenção**. Você também pode exibir uma lista desses problemas no bloco **Recomendações** .

Para obter mais informações sobre como aplicar recomendações, leia [Implementar as recomendações de segurança na Central de segurança do Azure](security-center-recommendations.md).

Na seção **Prevenção**, você pode monitorar o estado de segurança dos seus recursos. No exemplo a seguir, você pode ver que no bloco de cada recurso (Computação, Rede, Armazenamento e dados, e Aplicativo) há o número total de problemas que foram identificados.

![Bloco de integridade de segurança de recursos](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Monitorar a computação
Quando você clica no bloco **Computação**, a folha **Computação** que abre mostra três guias:

- **Visão geral**: recomendações de monitoramento e da máquina virtual.
- **Máquinas Virtuais**: lista todas as máquinas virtuais e seu estado de segurança atual.
- **Serviços de Nuvem**: lista todas as funções da Web e de trabalho monitoradas pela Central de Segurança.

![Atualização de sistema ausente por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Há várias seções em cada guia e, em cada seção, você pode selecionar uma opção individual para ver mais detalhes sobre as etapas recomendadas e resolver esse problema específico. 

#### <a name="monitoring-recommendations"></a>Recomendações de monitoramento
Esta seção mostra o número total de máquinas virtuais que foram inicializadas para coleta de dados e seu status atual. Depois que todas as máquinas virtuais tiverem inicializado a coleta de dados, estarão prontas para receber as políticas de segurança da Central de Segurança. Quando você clica nessa entrada, a folha **O agente de VM está faltando ou não está respondendo** é aberta. 

![Atualização de sistema ausente por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Recomendações de máquina virtual
Esta seção tem um conjunto de [recomendações para cada máquina virtual](security-center-virtual-machine-recommendations.md) que a Central de Segurança do Azure monitora. A primeira coluna lista a recomendação. A segunda coluna mostra o número total de máquinas virtuais que são afetadas por essa recomendação. A terceira coluna mostra a severidade do problema, conforme ilustrado na captura de tela a seguir.

![Recomendações de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Somente as máquinas virtuais que têm pelo menos um ponto de extremidade público são mostradas na folha **Integridade de Rede** na lista **Topologia de rede**.
>
>

Cada recomendação tem um conjunto de ações que podem ser executadas depois que você clica nela. Por exemplo, se você clicar em **Atualizações de sistema ausentes**, a folha **Atualizações de sistema ausentes** será aberta. Ele lista as máquinas virtuais que estão sem patches e a gravidade da atualização ausente, conforme mostrado na captura de tela a seguir.

![Atualizações de sistema ausentes para máquinas virtuais](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

A folha **Atualizações de sistema ausentes** mostra uma tabela com as seguintes informações:

* **MÁQUINA VIRTUAL**: o nome da máquina virtual com atualizações ausentes.
* **ATUALIZAÇÕES DO SISTEMA**: o número de atualizações do sistema que estão ausentes.
* **HORA DA ÚLTIMA VERIFICAÇÃO**: a hora em que a Central de Segurança verificou pela última vez a máquina virtual para detectar atualizações.
* **ESTADO**: o estado atual da recomendação:
  * **Aberta**: a recomendação ainda não foi resolvida.
  * **Em Andamento**: a recomendação está sendo aplicada atualmente aos recursos, e não é necessário que você realize nenhuma ação.
  * **Resolvido**: a recomendação já foi concluída. (Quando o problema foi resolvido, a entrada será esmaecida).
* **GRAVIDADE**: descreve a gravidade dessa recomendação específica:
  * **Alta**: existe uma vulnerabilidade em um recurso significativo (aplicativo, máquina virtual ou grupo de segurança de rede) e ela requer atenção.
  * **Média**: são necessárias etapas adicionais ou não críticas para concluir um processo ou eliminar a vulnerabilidade.
  * **Baixa**: uma vulnerabilidade que deve ser abordada, mas não exige atenção imediata. (Por padrão, não são apresentadas recomendações baixas, mas você pode filtrar as recomendações baixas caso deseje exibi-las.)

Para exibir os detalhes de recomendação, clique no nome da máquina virtual. Uma nova folha para a máquina virtual é aberta com a lista de atualizações, conforme mostrado na captura de tela a seguir.

![Atualizações de sistema ausentes para uma máquina virtual específica](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> As recomendações de segurança são as mesmas na folha de **Recomendações**. Confira o artigo [Implementar recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) para obter mais informações sobre como resolver as recomendações. Isso é aplicável não apenas a máquinas virtuais, mas também a todos os recursos que estão disponíveis no bloco **Integridade de Recursos**.
>
>

#### <a name="virtual-machines-section"></a>Seção Máquinas virtuais
A seção de máquinas virtuais fornece uma visão geral de todas as máquinas virtuais e recomendações. Cada coluna representa um conjunto de recomendações, conforme mostrado na seguinte captura de tela:

![Visão geral de todas as máquinas virtuais e recomendações](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

O ícone que aparece em cada recomendação o ajuda a identificar rapidamente as máquinas virtuais que precisam de atenção e o tipo de recomendação.

No exemplo anterior, uma máquina virtual tem uma recomendação crítica relacionada à proteção de ponto de extremidade. Para obter mais informações sobre a máquina virtual, clique nela. Será aberta uma nova folha que representa essa máquina virtual, conforme mostrado na captura de tela a seguir.

![Detalhes de segurança de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Esta folha tem os detalhes de segurança para a máquina virtual. Na parte inferior dessa folha, você pode ver a ação recomendada e a gravidade de cada problema.

#### <a name="cloud-services-section"></a>Seção Serviços de nuvem
Para os serviços de nuvem, uma recomendação é criada quando a versão do sistema operacional está desatualizada, conforme mostra a captura de tela a seguir:

![Status de integridade de serviços de nuvem](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

Em um cenário no qual você há uma recomendação (que não é o caso do exemplo anterior), você precisa seguir as etapas na recomendação para atualizar a versão do sistema operacional. Quando uma atualização estiver disponível, você terá um alerta (vermelho ou laranja - depende da gravidade do problema). Ao clicar nesse alerta vermelho nas linhas WebRole1 (executa o Windows Server com seu aplicativo Web automaticamente implantado no IIS) ou WorkerRole1 (executa o Windows Server com seu aplicativo Web automaticamente implantado no IIS), uma nova folha será aberta com mais detalhes sobre essa recomendação, conforme mostrado na seguinte captura de tela:

![Detalhes do serviço de nuvem](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

Para ver uma explicação mais detalhada sobre essa recomendação, clique em **Atualizar versão do sistema operacional** na coluna **DESCRIÇÃO**. A folha **Atualizar versão do sistema operacional (visualização)** é aberta com mais detalhes.

![Recomendações dos serviços de nuvem](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Monitorar redes virtuais
Quando você clica no bloco **Rede** a folha **Rede** é aberta com mais detalhes, conforme mostrado na seguinte captura de tela:

![Blog da rede](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Recomendações de rede
Assim como as informações de integridade de recursos de máquinas virtuais, essa folha fornece uma lista resumida dos problemas na parte superior da folha e uma lista de redes monitoradas na parte inferior.

A seção de divisão de status de rede lista os problemas de segurança potenciais e oferece [recomendações](security-center-network-recommendations.md). Os possíveis problemas podem incluir:

* Firewall da Próxima Geração (NGFW) não instalado
* Grupos de segurança da rede em sub-redes não habilitadas
* Grupos de segurança de rede em máquinas virtuais não habilitadas
* Restringir o acesso externo por meio do ponto de extremidade externo público
* Pontos de extremidade voltados para a Internet íntegra

Quando você clica em uma recomendação, uma nova folha é aberta com mais detalhes sobre a recomendação, conforme mostrado no exemplo a seguir.

![Detalhes de uma recomendação na folha Rede](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

Neste exemplo, a folha **Configurar grupos de segurança de rede ausentes para sub-redes** tem uma lista de sub-redes e máquinas virtuais que estão sem proteção do grupo de segurança de rede. Se você clicar na sub-rede à qual deseja aplicar o grupo de segurança de rede, outra folha será aberta.

Na folha **Escolher grupo de segurança da rede**, você pode selecionar o grupo de segurança da rede mais apropriado para a sub-rede ou pode criar um novo grupo de segurança da rede.

#### <a name="internet-facing-endpoints-section"></a>Seção dos pontos de extremidade voltados para a Internet
Na seção **Pontos de extremidade voltados para a Internet**, você pode ver as máquinas virtuais configuradas no momento com um ponto de extremidade voltado para a Internet e seu status atual.

![Máquinas virtuais configuradas para o ponto de extremidade e o status da Internet](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Esta tabela tem o nome de ponto de extremidade que representa a máquina virtual, o endereço IP público da Internet e o status de severidade atual do grupo de segurança de rede e o NGFW. A tabela é classificada por severidade:

* Vermelho (no topo): alta prioridade e deve ser endereçado imediatamente
* Laranja: prioridade média e deve ser endereçado assim que possível
* Verde (último): estado íntegro

#### <a name="networking-topology-section"></a>Seção de Topologia da rede
A seção **Topologia de rede** tem uma exibição hierárquica dos recursos, como mostrado na seguinte captura de tela:

![Exibição hierárquica de recursos na seção de topologia de rede](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Essa tabela é classificada (máquinas virtuais e sub-redes) por severidade:

* Vermelho (no topo): alta prioridade e deve ser endereçado imediatamente
* Laranja: prioridade média e deve ser endereçado assim que possível
* Verde (último): estado íntegro

Nessa exibição da topologia, o primeiro nível tem as [redes virtuai](../virtual-network/virtual-networks-overview.md), [gateways da rede virtual](/vpn-gateway/vpn-gateway-site-to-site-create.md) e [rede virtual (clássica)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). O segundo nível tem sub-redes, e o terceiro nível tem as máquinas virtuais que pertencem a essas sub-redes. A coluna da direita tem o status atual do grupo de segurança da rede para esses recursos, como mostrado neste exemplo:

![O status do grupo de segurança de rede na seção de Topologia de rede](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

A parte inferior da folha tem as recomendações para essa máquina virtual, que é semelhante ao que foi descrito anteriormente. Você pode clicar em uma recomendação para obter mais informações ou aplicar a configuração ou controle de segurança necessário.

### <a name="monitor-storage--data"></a>Monitorar Armazenamento e dados

Quando você clica em **Armazenamento e dados** na seção **Prevenção** a folha **Recursos de Dados** é aberta com recomendações para SQL e Armazenamento. Ela também contém [recomendações](security-center-sql-service-recommendations.md) para o estado de integridade geral do banco de dados. Para saber mais sobre criptografia de armazenamento, leia [Habilitar a criptografia para a conta de armazenamento do Azure na Central de Segurança do Azure](security-center-enable-encryption-for-storage-account.md).

![Recursos de dados](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

Em **Recomendações de SQL**, você pode clicar em qualquer recomendação e obter mais detalhes sobre uma ação adicional para resolver um problema. O exemplo a seguir mostra a expansão da recomendação **Auditoria e Detecção de ameaças do banco de dados em bancos de dados SQL**.

![Detalhes sobre uma recomendação de SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

A folha **Habilitar Auditoria e Detecção de ameaças nos bancos de dados SQL** contém as seguintes informações:

* Uma lista de bancos de dados SQL
* O servidor no qual eles estão localizados
* Informações indicando se essa configuração foi herdada do servidor ou se é exclusiva do banco de dados
* O estado atual
* A gravidade do problema

Quando você clicar no banco de dados para lidar com essa recomendação, a folha **Auditoria e Detecção de Ameaças** será aberta, conforme mostrado na tela a seguir.

![Folha de Auditoria e Detecção de Ameaça](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

Para habilitar a auditoria, selecione **ATIVADO** na opção **Auditoria**.

### <a name="monitor-applications"></a>Monitorar aplicativos

Se sua carga de trabalho do Azure tiver aplicativos localizados em [máquinas virtuais (criadas por meio do Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) com portas Web expostas (portas TCP 80 e 443), a Central de Segurança poderá monitorá-los para identificar os problemas de segurança em potencial e as etapas recomendáveis de correção. Quando você clicar no bloco **Aplicativos**, a folha **Aplicativos** será aberta com uma série de recomendações na seção **Recomendações do Aplicativo**. Ele também mostra a divisão de aplicativo por IP virtual/host, conforme mostrado na captura de tela a seguir.

![Integridade da segurança de aplicativos](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Como fez com as outras recomendações, você pode clicar em uma delas para ver mais detalhes sobre o problema e como corrigi-lo. O exemplo mostrado na figura a seguir é um aplicativo que foi identificado como aplicativo Web não seguro. Quando você selecionar o aplicativo que foi considerado não seguro, outra folha será aberta com a seguinte opção disponível:

![Detalhes sobre um aplicativo que não é seguro](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Esta folha terá uma lista de todas as recomendações para este aplicativo. Quando você clica na recomendação **Adicionar um firewall de aplicativo Web**, a folha **Adicionar um Firewall de Aplicativo Web** é aberta com opções para instalar um WAF (firewall de aplicativo Web) de um parceiro, conforme mostrado na captura de tela a seguir.

![Caixa de diálogo Adicionar Firewall de Aplicativo Web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Consulte também
Neste artigo, você aprendeu como usar os recursos de monitoramento na Central de segurança do Azure. Para saber mais sobre a Central de Segurança do Azure, veja o seguinte:

* [Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança na Central de Segurança do Azure.
* [Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.
* [Monitorando as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md): saiba como monitorar o status de integridade de suas soluções de parceiros.
* [Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md): encontre as perguntas frequentes sobre como usar o serviço.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.
