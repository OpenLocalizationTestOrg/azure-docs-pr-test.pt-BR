---
title: "Serviços de balanceamento de carga aaaUsing no Azure | Microsoft Docs"
description: "Este tutorial mostra como toocreate um cenário usando Olá portfólio de balanceamento de carga do Azure: Gerenciador de tráfego, o Application Gateway e o balanceador de carga."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Usando os serviços de balanceamento de carga no Azure

## <a name="introduction"></a>Introdução

O Microsoft Azure fornece vários serviços para gerenciar a forma como o tráfego de rede é distribuído e como sua carga é balanceada. Você pode usar esses serviços individualmente ou combinar seus métodos, dependendo de suas necessidades, a solução ideal de saudação toobuild.

Neste tutorial, podemos primeiro definir um caso de uso do cliente e ver como ele pode se tornar mais robusto e alto desempenho usando o hello portfólio de balanceamento de carga do Azure a seguir: Gerenciador de tráfego, o Application Gateway e o balanceador de carga. Em seguida, fornecemos instruções passo a passo para a criação de uma implantação geograficamente redundantes, distribui o tráfego tooVMs e ajuda a gerenciar diferentes tipos de solicitações.

Em um nível conceitual, cada um desses serviços desempenha um papel distinto na hierarquia de balanceamento de carga de saudação.

* **O Gerenciador de Tráfego** fornece balanceamento de carga DNS global. Ele analisa as solicitações de entrada DNS e responde com um ponto de extremidade íntegro, conforme Olá roteamento cliente de saudação de política foi selecionado. Opções de métodos de roteamento são:
  * Desempenho roteamento toosend Olá solicitante toohello mais próximo ponto de extremidade em termos de latência.
  * Prioridade de roteamento toodirect todos os tráfego tooan ponto de extremidade com outros pontos de extremidade como backup.
  * Weighted round robin roteamento, que distribui o tráfego com base na importância Olá atribuído tooeach de ponto de extremidade.

  Olá se conecta diretamente toothat de ponto de extremidade. O Azure Traffic Manager detecta quando um ponto de extremidade não está íntegro e, em seguida, redireciona Olá instância Íntegro de tooanother de clientes. Consulte também[documentação do Azure Traffic Manager](traffic-manager-overview.md) toolearn mais sobre o serviço de saudação.
* O **Gateway de Aplicativo** fornece o ADC (Controlador de Entrega de Aplicativos) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para o aplicativo. Ele permite que os clientes produtividade de farm da web toooptimize descarregando gateway de aplicativo de toohello de terminação SSL de uso intensivo de CPU. Outros recursos de roteamento de camada 7 incluem round-robin distribuição de tráfego de entrada, a afinidade de sessão baseada em cookie, roteamento baseado no caminho de URL e Olá capacidade toohost vários sites por trás de um gateway de aplicativo único. O Gateway de Aplicativo pode ser configurado como um gateway voltado para a Internet, um gateway apenas interno ou uma combinação de ambos. O Gateway de Aplicativo é totalmente gerenciado pelo Azure, escalonável e altamente disponível. Ele fornece um conjunto avançado de recursos de log e diagnósticos para melhor capacidade de gerenciamento.
* **Balanceador de carga** é parte integrante da pilha de SDN Azure hello, fornecimento de alto desempenho e baixa latência camada 4 balanceamento de carga de serviços para os protocolos TCP e UDP todos os. Ele gerencia conexões de entrada e saída. Você pode configurar públicos e internos com balanceamento de carga pontos de extremidade e definem regras toomap destinos de pool de tooback a fim de conexões de entrada usando TCP e HTTP de investigação de integridade opções toomanage disponibilidade do serviço.

## <a name="scenario"></a>Cenário

Nesse cenário de exemplo, usamos um site simples com dois tipos de conteúdo: imagens e páginas da Web processadas dinamicamente. site Olá deve ser geograficamente redundante e deve atender seus usuários de hello mais próximo (latência mais baixa) toothem local. Olá desenvolvedor do aplicativo decidir que todas as URLs que corresponderam Olá padrão imagens / * servido a partir de um pool dedicado de VMs diferentes do restante de saudação do farm da web de saudação.

Além disso, o pool VM padrão Olá servir conteúdo dinâmico Olá precisa banco de dados do tootalk tooa back-end que é hospedado em um cluster de alta disponibilidade. toda a implantação Olá é configurada por meio do Gerenciador de recursos do Azure.

Usar o Gerenciador de tráfego, o Application Gateway e o balanceador de carga permite que esse site tooachieve essas metas de design:

* **Redundância geográfica de várias**: se uma região for desativada, rotas de Gerenciador de tráfego tráfego perfeitamente a região mais próxima toohello sem qualquer intervenção do proprietário do aplicativo hello.
* **Latência reduzida**: porque o Traffic Manager direciona automaticamente região mais próxima da saudação cliente toohello, experiências de clientes de saudação menor latência ao solicitar o conteúdo da página da Web de saudação.
* **Escalabilidade independente**: porque a carga de trabalho do aplicativo Olá web é separada por tipo de conteúdo, o proprietário do aplicativo hello pode dimensionar cargas de trabalho de solicitação do hello independentes um do outro. Application Gateway garante que o tráfego de saudação seja pools de direito toohello roteada com base em Olá especificado regras e a integridade de saudação do aplicativo hello.
* **Balanceamento de carga interno**: porque o balanceador de carga é na frente de cluster de alta disponibilidade hello, somente Olá ativas e íntegro ponto de extremidade para um banco de dados é exposto toohello aplicativo. Além disso, um administrador de banco de dados pode otimizar a carga de trabalho de saudação distribuindo réplicas ativas e passivas no cluster de saudação independente do aplicativo front-end hello. Balanceador de carga de cluster de alta disponibilidade toohello conexões de entrega e garante que somente bancos de dados de integridade recebem solicitações de conexão.

Olá diagrama a seguir mostra a arquitetura Olá deste cenário:

![Diagrama de arquitetura de balanceamento de carga](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> Este exemplo é apenas uma das muitas configurações possíveis de serviços Olá balanceamento de carga que o Azure oferece. Gerenciador de tráfego, o Application Gateway e o balanceador de carga podem ser misturados e toobest correspondente atender às suas necessidades de balanceamento de carga. Por exemplo, se o descarregamento de SSL ou o processamento de camada 7 não forem necessários, o balanceador de carga pode ser usado no lugar de Gateway de Aplicativo.

## <a name="setting-up-hello-load-balancing-stack"></a>Configurando a pilha de balanceamento de carga de saudação

### <a name="step-1-create-a-traffic-manager-profile"></a>Etapa 1: Criar um perfil do Gerenciador de Tráfego

1. No portal do Azure de Olá, clique em **novo**e, em seguida, pesquisa de mercado hello "Perfil do Gerenciador de tráfego".
2. Em Olá **perfil do Traffic Manager criar** folha, digite Olá informações básicas a seguir:

  * **Nome**: forneça ao seu perfil de Gerenciador de Tráfego um nome de prefixo DNS.
  * **Método de roteamento**: selecione Olá política do método de roteamento de tráfego. Para obter mais informações sobre métodos de hello, consulte [sobre o Gerenciador de tráfego de métodos de roteamento de tráfego](traffic-manager-routing-methods.md).
  * **Assinatura**: selecione Olá assinatura que contém o perfil de saudação.
  * **Grupo de recursos**: grupo de recursos de saudação Select que contém o perfil de saudação. Pode ser um grupo de recursos novo ou existente.
  * **Local do grupo de recursos**: serviço de Gerenciador de tráfego é global e não vinculado tooa local. No entanto, você deve especificar uma região para grupo de saudação onde metadados Olá associados ao perfil do Traffic Manager Olá residem. Este local não terá impacto na disponibilidade de tempo de execução de saudação do perfil de saudação.

3. Clique em **criar** toogenerate Olá perfil do Traffic Manager.

  ![Criar folha do Gerenciador de Tráfego](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Etapa 2: Criar hello gateways de aplicativo

1. No hello portal do Azure, no painel esquerdo do hello, clique em **novo** > **rede** > **Application Gateway**.
2. Digite hello informações básicas sobre o gateway do aplicativo hello a seguir:

  * **Nome**: nome de saudação do gateway de aplicativo hello.
  * **Tamanho da SKU**: Olá tamanho do gateway de aplicativo hello, disponível como pequeno, médio ou grande.
  * **Contagem de instâncias**: número de saudação de instâncias, um valor de 2 a 10.
  * **Grupo de recursos**: grupo de recursos de saudação que mantém o gateway de aplicativo hello. Pode ser um grupo de recursos existente ou um novo.
  * **Local**: região Olá Olá application gateway, que é Olá mesmo local que o grupo de recursos de saudação. local de saudação é importante, porque o IP público e rede virtual Olá devem estar no hello mesmo local que o gateway de saudação.
3. Clique em **OK**.
4. Defina a rede virtual hello, sub-rede, IP de front-end e configurações do ouvinte para o gateway de aplicativo hello. Nesse cenário, o endereço IP de front-end de saudação é **pública**, que permite toobe adicionado como um ponto de extremidade toohello perfil do Traffic Manager posteriormente.
5. Configure o ouvinte de saudação com uma saudação as opções a seguir:
    * Se você usar HTTP, não há nada tooconfigure. Clique em **OK**.
    * Se você usar HTTPS, será necessária configuração adicional. Consulte também[criar um application gateway](../application-gateway/application-gateway-create-gateway-portal.md), começando na etapa 9. Quando você concluiu a configuração de saudação, clique em **Okey**.

#### <a name="configure-url-routing-for-application-gateways"></a>Configurar o roteamento de URL para os gateways de aplicativo

Quando você escolhe um pool de back-end, um gateway de aplicativos está configurado com uma regra de caminho usa um padrão de caminho da URL de solicitação de saudação na distribuição de tooround robin adição. Neste cenário, estamos adicionando uma regra de caminho com toodirect qualquer URL com "/images/\*" toohello pool de servidores de imagem. Para obter mais informações sobre como configurar a URL de roteamento baseado em caminho para um gateway de aplicativo, consulte muito[criar uma regra de caminho para um application gateway](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagrama de camada da web de Gateway de Aplicativo](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. De seu grupo de recursos, vá toohello instância do gateway de aplicativo hello que você criou na saudação anterior da seção.
2. Em **configurações**, selecione **pools de back-end**e, em seguida, selecione **adicionar** tooadd Olá VMs que você deseja tooassociate com pools de back-end do hello da camada da web.
3. Em Olá **Adicionar pool de back-end** folha, insira nome de saudação do pool de back-end hello e todos os endereços IP de saudação de máquinas de saudação que residem no pool de saudação. Nesse cenário, estamos conectando dois pools de servidores de back-end de máquinas virtuais.

  ![Folha de "Adicionar pool de back-end" do Gateway de Aplicativo](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. Em **configurações** do gateway de aplicativo hello, selecione **regras**e, em seguida, clique em Olá **caminho com base em** botão tooadd uma regra.

  ![Botão de "Caminho com base em" de regras de Gateway de Aplicativo](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Em Olá **Adicionar regra de caminho com base em** folha, configurar a regra de saudação fornecendo Olá informações a seguir.

   Configurações básicas:

   + **Nome**: nome amigável de saudação da regra de saudação que é acessível no portal de saudação.
   + **Ouvinte**: ouvinte Olá que é usado para a regra de saudação.
   + **Padrão de pool de back-end**: Olá toobe de pool de back-end usado com a regra padrão de saudação.
   + **Configurações de HTTP padrão**: Olá HTTP configurações toobe usado com a regra padrão de saudação.

   Regras com base no caminho:

   + **Nome**: nome amigável de saudação da regra de caminho com base em hello.
   + **Caminhos**: regra de caminho de saudação que é usada para encaminhar o tráfego.
   + **Pool de back-end**: Olá toobe de pool de back-end usado com esta regra.
   + **Configuração de HTTP**: Olá HTTP configurações toobe usado com esta regra.

   > [!IMPORTANT]
   > Caminhos: caminhos válidos devem começar com "/". Olá curinga "\*" é permitido somente no final de saudação. Exemplos válidos são /xyz, /xyz\*; ou /xyz/\*.

   ![Folha "Adicionar regra com base no caminho" do Gateway de Aplicativo](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Etapa 3: Adicionar pontos de extremidade do Traffic Manager toohello de gateways de aplicativo

Nesse cenário, o Traffic Manager é gateways tooapplication conectado (conforme configurado no hello etapas anteriores) que residem em diferentes regiões. Agora que os gateways de aplicativos Olá estão configurados, Olá próxima etapa é tooconnect-los tooyour perfil do Traffic Manager.

1. Abra o seu perfil do Gerenciador de Tráfego. Assim, procure toodo em seu grupo de recursos ou a pesquisa do nome de saudação do perfil do Gerenciador de tráfego de saudação do **todos os recursos**.
2. No painel esquerdo do hello, selecione **pontos de extremidade**e, em seguida, clique em **adicionar** tooadd um ponto de extremidade.

  ![Botão “Adicionar” de Pontos de extremidade do Gerenciador de Tráfego](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Em Olá **Adicionar ponto de extremidade** folha, crie um ponto de extremidade inserindo Olá informações a seguir:

  * **Tipo**: Selecionar tipo de saudação de saldo de tooload de ponto de extremidade. Nesse cenário, selecione **Azure ponto de extremidade** porque estamos são conectá-lo toohello instâncias de gateway de aplicativos que foram configuradas anteriormente.
  * **Nome**: insira o nome de saudação do ponto de extremidade de saudação.
  * **Tipo de recurso de destino**: selecione **endereço IP público** e, em seguida, em **recurso de destino**, selecione o IP público de saudação do application gateway Olá configurado anteriormente.

   ![Folha "Adicionar ponto de extremidade" do Gerenciador de Tráfego](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Agora você pode testar sua configuração acessando-os com hello DNS do seu perfil do Traffic Manager (neste exemplo: TrafficManagerScenario.trafficmanager.net). Reenviar solicitações, ativar ou desativar as máquinas virtuais e servidores web que foram criados em regiões diferentes e alterar a configuração de saudação tootest de configurações de perfil de Gerenciador de tráfego.

### <a name="step-4-create-a-load-balancer"></a>Etapa 4: criar um balanceador de carga

Nesse cenário, o balanceador de carga distribui conexões de bancos de dados do Olá web camada toohello dentro de um cluster de alta disponibilidade.

Se o cluster de alta disponibilidade de banco de dados está usando o SQL Server AlwaysOn, consulte muito[configurar um ou mais sempre em ouvintes de disponibilidade](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) para obter instruções passo a passo.

Para obter mais informações sobre como configurar um balanceador de carga interno, consulte [criar um balanceador de carga interno no portal do Azure de saudação](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. No hello portal do Azure, no painel esquerdo do hello, clique em **novo** > **rede** > **balanceador de carga**.
2. Em Olá **criar balanceador de carga** folha, escolha um nome para o balanceador de carga.
3. Saudação de conjunto **tipo** muito**interno**e escolha a rede virtual apropriado de saudação e a sub-rede para Olá tooreside de Balanceador de carga no.
4. Em **Atribuição de endereço IP**, selecione **Dinâmico** ou **Estático**.
5. Em **grupo de recursos**, escolha o grupo de recursos Olá Olá balanceador de carga.
6. Em **local**, escolha a região apropriada Olá Olá balanceador de carga.
7. Clique em **criar** toogenerate balanceador de carga de saudação.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Conecte-se um balanceador de carga de toohello de nível de banco de dados de back-end

1. De seu grupo de recursos, localize o balanceador de carga Olá criado nas etapas anteriores hello.
2. Em **configurações**, clique em **pools de back-end**e, em seguida, clique em **adicionar** tooadd um pool de back-end.

  ![Folha de "Adicionar pool de back-end" do balanceador de carga](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Em Olá **Adicionar pool de back-end** folha, insira o nome de saudação do pool de back-end de saudação.
4. Adicione máquinas individuais ou um pool de back-end de toohello de conjunto de disponibilidade.

#### <a name="configure-a-probe"></a>Configurar uma investigação

1. No balanceador de carga, em **configurações**, selecione **testes**e, em seguida, clique em **adicionar** tooadd uma investigação.

 ![Folha de "Adicionar teste" do balanceador de carga](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Em Olá **adicionar teste** folha, insira nome Olá Olá da investigação.
3. Selecione Olá **protocolo** para investigação hello. Para um banco de dados, é ideal utilizar uma investigação TCP em vez de uma investigação HTTP. toolearn mais sobre testes de Balanceador de carga, consulte muito[investigações do balanceador de carga de compreender](../load-balancer/load-balancer-custom-probe-overview.md).
4. Digite hello **porta** de seu toobe de banco de dados usado para acessar a investigação de saudação.
5. Em **intervalo**, especifique a frequência tooprobe Olá aplicativo.
6. Em **limite não íntegro**, especifique Olá número de falhas de investigação contínua que deve ocorrer para Olá back-end VM toobe considerado não íntegro.
7. Clique em **Okey** toocreate investigação de saudação.

#### <a name="configure-hello-load-balancing-rules"></a>Configurar regras de balanceamento de carga de saudação

1. Em **configurações** do balanceador de carga, selecione **regras de balanceamento de carga**e, em seguida, clique em **adicionar** toocreate uma regra.
2. Em Olá **regra de balanceamento de carga de adicionar** folha, digite Olá **nome** para a regra de balanceamento de carga de saudação.
3. Escolha Olá **endereço de IP de front-end** de saudação balanceador de carga, **protocolo**, e **porta**.
4. Em **porta de back-end**, especifique Olá porta toobe usado no pool de back-end de saudação.
5. Selecione Olá **pool de back-end** e hello **investigação** que foram criados no hello etapas tooapply Olá regra anterior para.
6. Em **persistência de sessão**, escolha como você deseja Olá sessões toopersist.
7. Em **tempos limite de ociosidade**, especifique Olá número de minutos antes de um tempo limite de ociosidade.
8. Em **IP flutuante**, selecione **Desabilitado** ou **Habilitado**.
9. Clique em **Okey** toocreate regra de saudação.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Etapa 5: Conectar-se o balanceador de carga da camada da web VMs toohello

Agora podemos configurar Olá IP balanceador de carga e o endereço de porta front-end em aplicativos de saudação que estão em execução em suas VMs de camada da web para qualquer conexão de banco de dados. Essa configuração é específica toohello aplicativos executados nessas máquinas virtuais. endereço IP de destino tooconfigure hello e a porta, consulte a documentação do aplicativo toohello. endereço IP de saudação toofind de saudação front-end, no hello portal do Azure, vá pool de IP de front-end de toohello Olá **configurações do balanceador de carga** folha.

![Painel de navegação de "Pool Frontend IP" do balanceador de carga](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Próximas etapas

* [Visão geral do Gerenciador de Tráfego](traffic-manager-overview.md)
* [Visão geral do Gateway de Aplicativo](../application-gateway/application-gateway-introduction.md)
* [Visão geral do Azure Load Balancer](../load-balancer/load-balancer-overview.md)
