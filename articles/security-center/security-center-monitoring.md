---
title: "monitoramento de aaaSecurity na Central de segurança do Azure | Microsoft Docs"
description: "Este artigo ajuda tooget iniciado com o monitoramento de recursos na Central de segurança do Azure."
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
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Monitoramento de integridade de segurança na Central de segurança do Azure
Este artigo ajuda você a usar o hello recursos de monitoramento em conformidade de toomonitor Central de segurança do Azure com as políticas.

## <a name="what-is-security-health-monitoring"></a>O que é o monitoramento de integridade de segurança?
Geralmente, consideramos de monitoramento como detectar e aguardando um evento toooccur para que nós possam reagir toohello situação. Monitoramento de segurança refere-se toohaving uma estratégia proativa que auditorias de seus sistemas de tooidentify de recursos que não atendem aos padrões organizacionais ou práticas recomendadas.

## <a name="monitoring-security-health"></a>Monitoramento de integridade da segurança
Depois de habilitar [políticas de segurança](security-center-policies.md) para recursos de uma assinatura, Central de segurança analisa a segurança do hello de seus recursos tooidentify as vulnerabilidades potenciais. Informações sobre a configuração de rede estão disponíveis imediatamente. Pode levar uma hora ou mais para obter informações sobre a configuração de máquina virtual, como segurança de atualização de status e configuração do sistema operacional, toobecome disponível. Você pode exibir o estado de segurança Olá seus recursos e os problemas no hello **prevenção** seção. Você também pode exibir uma lista desses problemas em Olá **recomendações** lado a lado.

Para obter mais informações sobre como tooapply recomendações, ler [implementar recomendações de segurança na Central de segurança do Azure](security-center-recommendations.md).

Em Olá **prevenção** seção, você pode monitorar o estado de segurança de saudação de seus recursos. Saudação de exemplo a seguir, você pode ver que no bloco de cada recurso (computação, rede, armazenamento e dados e aplicativos) tem o número total de saudação de problemas que foram identificados.

![Bloco de integridade de segurança de recursos](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Monitorar a computação
Quando você clica em **de computação** lado a lado, hello **de computação** folha abre mostra três guias:

- **Visão geral**: recomendações de monitoramento e da máquina virtual.
- **Máquinas Virtuais**: lista todas as máquinas virtuais e seu estado de segurança atual.
- **Serviços de Nuvem**: lista todas as funções da Web e de trabalho monitoradas pela Central de Segurança.

![Atualização de sistema ausente por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Em cada guia, você pode ter várias seções, e em cada seção, você pode selecionar uma opção individual toosee mais detalhes sobre Olá recomendado etapas tooaddress esse problema. 

#### <a name="monitoring-recommendations"></a>Recomendações de monitoramento
Esta seção mostra o número total de saudação de máquinas virtuais que foram inicializadas para coleta de dados e seu status atuais. Depois que todas as máquinas virtuais têm a coleta de dados inicializada, ele ficará pronto tooreceive as políticas de segurança central de segurança. Quando você clica nesta entrada, Olá **agente da VM está ausente ou não respondendo** folha é aberta. 

![Atualização de sistema ausente por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Recomendações de máquina virtual
Esta seção tem um conjunto de [recomendações para cada máquina virtual](security-center-virtual-machine-recommendations.md) que a Central de Segurança do Azure monitora. Olá primeira coluna listas recomendação hello. Olá segunda coluna mostra o número total de saudação de máquinas virtuais que são afetados por essa recomendação. Olá terceira coluna mostra gravidade de saudação do problema Olá conforme ilustrado na Olá captura de tela a seguir.

![Recomendações de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Somente as máquinas virtuais que têm pelo menos um ponto de extremidade público são mostradas no hello **rede integridade** folha em hello **topologia de rede** lista.
>
>

Cada recomendação tem um conjunto de ações que podem ser executadas depois que você clica nela. Por exemplo, se você clicar em **atualizações de sistema ausentes**, Olá **atualizações de sistema ausentes** folha é aberta. Ele lista as máquinas virtuais de saudação ausentes patches e Olá gravidade da atualização ausente Olá, conforme mostrado na seguinte Olá captura de tela.

![Atualizações de sistema ausentes para máquinas virtuais](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Olá **atualizações de sistema ausentes** folha mostra uma tabela com hello informações a seguir:

* **MÁQUINA VIRTUAL**: nome de saudação da máquina virtual Olá que não há atualizações.
* **ATUALIZAÇÕES do sistema**: Olá o número de atualizações do sistema que estão faltando.
* **HORA da última verificação**: tempo de saudação que a Central de segurança verificado pela última vez máquina virtual de saudação para atualizações.
* **ESTADO**: Olá o estado atual da recomendação hello:
  * **Abra**: recomendação Olá ainda não foram resolvida.
  * **Em andamento**: recomendação hello está sendo aplicada toothose recursos, e nenhuma ação é necessária por você.
  * **Resolvido**: recomendação Olá já foi concluída. (Quando Olá problema foi resolvido, entrada hello está esmaecida).
* **SEVERIDADE**: descreve severidade Olá essa recomendação específica:
  * **Alta**: existe uma vulnerabilidade em um recurso significativo (aplicativo, máquina virtual ou grupo de segurança de rede) e ela requer atenção.
  * **Médio**: etapas adicionais ou não críticos são toocomplete necessário um processo ou eliminar a vulnerabilidade.
  * **Baixa**: uma vulnerabilidade que deve ser abordada, mas não exige atenção imediata. (Por padrão, as recomendações baixas não estiverem presentes, mas você pode filtrar em recomendações baixas se você quiser tooview-las.)

detalhes da recomendação tooview Olá, clique o nome de saudação da máquina virtual de saudação. Uma nova folha para a máquina virtual abre com lista de saudação de atualizações, como mostrado na Olá captura de tela a seguir.

![Atualizações de sistema ausentes para uma máquina virtual específica](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Olá recomendações de segurança aqui são Olá mesmo da saudação **recomendações** folha. Consulte Olá [implementar recomendações de segurança na Central de segurança do Azure](security-center-recommendations.md) artigo para obter mais informações sobre como tooresolve recomendações. Isso é aplicável não apenas para máquinas virtuais mas também para todos os recursos que estão disponíveis no hello **integridade de recursos** lado a lado.
>
>

#### <a name="virtual-machines-section"></a>Seção Máquinas virtuais
seção de máquinas virtuais Olá oferece uma visão geral de todas as máquinas virtuais e recomendações. Cada coluna representa um conjunto de recomendações, conforme mostrado no hello captura de tela a seguir:

![Visão geral de todas as máquinas virtuais e recomendações](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

ícone de saudação que aparece em cada recomendação ajuda tooquickly você identificar as máquinas de virtuais Olá que precisam de atenção e Olá tipo de recomendação.

No exemplo anterior de saudação, uma máquina virtual tem uma recomendação crítica relacionados à proteção de ponto de extremidade. tooget obter mais informações sobre a máquina virtual de saudação, clique nele. Uma nova folha que abre representa essa máquina virtual conforme Olá captura de tela a seguir.

![Detalhes de segurança de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Esta folha tem Olá segurança detalhes de saudação máquina virtual. Na parte inferior do hello desta folha, você pode ver Olá recomendado ação e severidade saudação de cada problema.

#### <a name="cloud-services-section"></a>Seção Serviços de nuvem
Para serviços de nuvem, uma recomendação é criada quando a versão do sistema operacional hello está desatualizada conforme Olá captura de tela a seguir:

![Status de integridade de serviços de nuvem](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

Em um cenário onde você tem a recomendação (que não é o caso de Olá para o exemplo anterior Olá), você precisa toofollow etapas de saudação na versão do sistema operacional Olá recomendação tooupdate hello. Quando uma atualização está disponível, você terá um alerta (vermelho ou laranja - depende da gravidade de saudação do problema Olá). Quando você clica nesse alerta nas linhas de saudação WebRole1 (executa o Windows Server com sua tooIIS de aplicativo implantado automaticamente da web) ou WorkerRole1 (executa o Windows Server com sua tooIIS de aplicativo implantado automaticamente da web), uma nova folha é aberta com mais detalhes sobre isso recomendação, conforme mostrado no hello captura de tela a seguir:

![Detalhes do serviço de nuvem](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee uma explicação mais detalhada sobre esta recomendação, clique em **versão do sistema operacional de atualização** em Olá **descrição** coluna. Olá **versão do SO de atualização (visualização)** folha abre com mais detalhes.

![Recomendações dos serviços de nuvem](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Monitorar redes virtuais
Quando você clica em **rede** lado a lado, hello **rede** folha abre com mais detalhes conforme Olá captura de tela a seguir:

![Blog da rede](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Recomendações de rede
Como hello informações de integridade de recursos da máquina virtual, esta folha fornece uma lista resumida dos problemas na parte superior de saudação da folha de saudação e uma lista de redes monitorados na parte inferior da saudação.

lista os problemas potenciais de segurança de saudação seção de divisão de status do sistema de rede e oferece [recomendações](security-center-network-recommendations.md). Os possíveis problemas podem incluir:

* Firewall da Próxima Geração (NGFW) não instalado
* Grupos de segurança da rede em sub-redes não habilitadas
* Grupos de segurança de rede em máquinas virtuais não habilitadas
* Restringir o acesso externo por meio do ponto de extremidade externo público
* Pontos de extremidade voltados para a Internet íntegra

Quando você clica em uma recomendação, abre uma nova folha com mais detalhes sobre a recomendação de saudação conforme mostrado no exemplo a seguir de saudação.

![Detalhes de uma recomendação na folha de rede Olá](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

Neste exemplo, Olá **configurar ausente rede grupos de segurança para sub-redes** folha tem uma lista de sub-redes e proteção do grupo de segurança de rede de máquinas virtuais que estão ausentes. Se você clicar em Olá sub-rede toowhich você deseja que o grupo de segurança de rede tooapply hello, abre outra folha.

Em Olá **o grupo de segurança de rede escolha** folha, você pode selecionar hello mais apropriado grupo de segurança para a sub-rede hello, ou você pode criar um novo grupo de segurança de rede.

#### <a name="internet-facing-endpoints-section"></a>Seção dos pontos de extremidade voltados para a Internet
Em Olá **para pontos de extremidade de Internet** seção, você pode ver máquinas virtuais Olá atualmente configurados com um voltada para o ponto de extremidade e seu status atual da Internet.

![Máquinas virtuais configuradas para o ponto de extremidade e o status da Internet](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Esta tabela tem o nome de ponto de extremidade de saudação que representa Olá máquina virtual, hello Internet voltada para o endereço IP, e Olá atual status de gravidade do grupo de segurança de rede hello e Olá NGFW. Olá tabela é classificada por severidade:

* Vermelho (no topo): alta prioridade e deve ser endereçado imediatamente
* Laranja: prioridade média e deve ser endereçado assim que possível
* Verde (último): estado íntegro

#### <a name="networking-topology-section"></a>Seção de Topologia da rede
Olá **topologia de rede** seção tem uma exibição hierárquica de recursos hello, conforme mostrado na Olá captura de tela a seguir:

![Exibição hierárquica de recursos na seção de topologia de rede](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Essa tabela é classificada (máquinas virtuais e sub-redes) por severidade:

* Vermelho (no topo): alta prioridade e deve ser endereçado imediatamente
* Laranja: prioridade média e deve ser endereçado assim que possível
* Verde (último): estado íntegro

Neste modo de exibição de topologia, o primeiro nível de saudação tem [redes virtuais](../virtual-network/virtual-networks-overview.md), [gateways de rede virtual](/vpn-gateway/vpn-gateway-site-to-site-create.md), e [redes virtuais (clássico)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). segundo nível de saudação tiver sub-redes e terceiro nível de saudação tem máquinas virtuais Olá que pertencem a toothose sub-redes. coluna da direita Olá tem o status atual de saudação do grupo de segurança de rede Olá para esses recursos, conforme mostrado no exemplo a seguir de saudação:

![Status do grupo de segurança de rede Olá na seção de topologia de rede](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

a parte inferior desta folha Hello apresenta recomendações de saudação para esta máquina virtual, que é semelhante toowhat descrito anteriormente. Você pode clicar uma toolearn recomendação mais ou aplicar Olá necessário controle de segurança ou configuração.

### <a name="monitor-storage--data"></a>Monitorar Armazenamento e dados

Quando você clica em **armazenamento & dados** em hello **prevenção** seção, hello **dados recursos** folha abre com recomendações para armazenamento e SQL. Ele também tem [recomendações](security-center-sql-service-recommendations.md) para estado de integridade geral de saudação do banco de dados de saudação. Para saber mais sobre criptografia de armazenamento, leia [Habilitar a criptografia para a conta de armazenamento do Azure na Central de Segurança do Azure](security-center-enable-encryption-for-storage-account.md).

![Recursos de dados](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

Em **SQL recomendações**, você pode clicar em qualquer recomendação e obter mais detalhes sobre tooresolve de ação mais um problema. Olá, exemplo a seguir mostra expansão de saudação do hello **detecção de ameaças e a auditoria de banco de dados em bancos de dados SQL** recomendação.

![Detalhes sobre uma recomendação de SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Olá **detecção de ameaça e habilitar a auditoria em bancos de dados SQL** folha tem Olá informações a seguir:

* Uma lista de bancos de dados SQL
* servidor de saudação em que se encontram
* Obter informações sobre como se essa configuração foi herdada do servidor de saudação ou se é exclusivo no banco de dados
* estado atual da saudação
* severidade de saudação do problema Olá

Quando você clica em Olá tooaddress de banco de dados nesta recomendação, Olá **detecção de auditoria e ameaças** folha abre conforme Olá tela a seguir.

![Folha de Auditoria e Detecção de Ameaça](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

auditoria tooenable, selecione **ON** em Olá **auditoria** opção.

### <a name="monitor-applications"></a>Monitorar aplicativos

Se sua carga de trabalho do Azure tem aplicativos localizados em [máquinas virtuais (criadas por meio do Gerenciador de recursos do Azure)](../azure-resource-manager/resource-manager-deployment-model.md) com web exposto (portas TCP 80 e 443), a Central de segurança pode monitorar os problemas potenciais de segurança tooidentify e recomendável etapas de correção. Quando você clica em Olá **aplicativos** lado a lado, hello **aplicativos** folha é aberta com uma série de recomendações Olá **recomendações de aplicativo** seção. Ele também mostra análise do aplicativo hello por IP virtuais/host conforme Olá captura de tela a seguir.

![Integridade da segurança de aplicativos](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Assim como você com hello outras recomendações, você pode clicar em uma recomendação toosee mais detalhes sobre o problema de saudação e como tooremediate. exemplo Hello mostrado na figura a seguir de saudação é um aplicativo que foi identificado como um aplicativo web não segura. Quando você seleciona o aplicativo hello que foi considerado não seguro, outra folha abre com hello opção disponível a seguir:

![Detalhes sobre um aplicativo que não é seguro](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Esta folha terá uma lista de todas as recomendações para este aplicativo. Quando você clica em Olá **adicionar um firewall do aplicativo web** recomendação, Olá **adicionar um Firewall do aplicativo Web** folha abre com as opções para você tooinstall um firewall do aplicativo web (WAF) de um parceiro como Olá mostrado na captura de tela a seguir.

![Caixa de diálogo Adicionar Firewall de Aplicativo Web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Consulte também
Neste artigo, você aprendeu como toouse monitoramento de recursos na Central de segurança do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md): Saiba como tooconfigure as configurações de segurança na Central de segurança do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md): Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md): Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md): perguntas frequentes sobre como usar o serviço de saudação de localizar.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.
