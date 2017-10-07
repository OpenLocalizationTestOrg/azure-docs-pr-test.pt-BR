---
title: aaaCreate sua primeira Virtual do Azure de rede | Microsoft Docs
description: "Saiba como toocreate uma rede Virtual do Azure (VNet), conecte-se duas máquinas virtuais (VM) toohello VNet e conectar toohello VMs."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Criar sua primeira rede virtual

Saiba como toocreate uma rede virtual (VNet) com duas sub-redes, criar duas máquinas virtuais (VM) e conecte-se tooone cada VM de sub-redes Olá, conforme mostrado na figura abaixo de saudação:

![Diagrama de rede virtual](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Uma rede virtual do Azure (VNet) é uma representação de sua própria rede na nuvem hello. Você pode controlar as configurações de rede do Azure e definir blocos de endereço DHCP,  configurações de DNS, políticas de segurança e roteamento. toolearn mais sobre conceitos de rede virtual, leia Olá [visão geral da rede Virtual](virtual-networks-overview.md) artigo. Recursos de saudação toocreate mostrados na Figura Olá as etapas a seguir de saudação concluída:

1. [Criar uma rede virtual com duas sub-redes](#create-vnet)
2. [Criar duas VMs, cada um com uma interface de rede (NIC)](#create-vms)e associe uma tooeach de grupo (NSG) de segurança de rede NIC
3. [Conecte-se tooand de saudação VMs](#connect-to-from-vms)
4. [Excluir todos os recursos](#delete-resources). Incorre em encargos para alguns dos recursos de saudação criados neste exercício, enquanto eles são provisionados. encargos de saudação toominimize, depois de concluir o exercício hello, certifique-se toocomplete Olá etapas esta seção toodelete Olá os recursos criar.

Você terá um entendimento básico de como você pode usar uma rede virtual depois Olá concluindo as etapas neste artigo. Próximas etapas são fornecidas para que você pode aprender mais sobre como toouse VNets em um nível mais profundo.

## <a name="create-vnet"></a>Criar uma rede virtual com duas sub-redes

toocreate uma rede virtual com duas sub-redes, etapas Olá completa que seguem. Subredes diferentes são normalmente usados toocontrol fluxo de saudação do tráfego entre sub-redes.

1. Faça logon no toohello [portal do Azure](<https://portal.azure.com>). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free). 
2. Em Olá **Favoritos** painel do portal de saudação, clique em **novo**.
3. Em Olá **novo** folha, clique em **rede**. Em Olá **rede** folha, clique em **rede Virtual**, conforme mostrado na figura abaixo de saudação:

    ![Diagrama de rede virtual](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  Em Olá **rede Virtual** folha, deixe *Gerenciador de recursos de* marcada como modelo de implantação de saudação e clique em **criar**.
5.  Em Olá **criar folha de rede virtual** que aparece, digite Olá valores a seguir, clique em **criar**:

    |**Configuração**|**Valor**|**Detalhes**|
    |---|---|---|
    |**Nome**|*MyVNet*|Olá nome deve ser exclusivo dentro do grupo de recursos de saudação.|
    |**Espaço de endereço**|*10.0.0.0/16*|Você pode especificar qualquer espaço de endereço desejado em notação CIDR.|
    |**Nome da sub-rede**|*Front-end*|nome da sub-rede Olá deve ser exclusivo dentro da rede virtual hello.|
    |**Intervalo de endereços da sub-rede**|*10.0.0.0/24*| intervalo de saudação especificado deve existir no espaço de endereço Olá definido para a rede virtual hello.|
    |**Assinatura**|*[Sua assinatura]*|Selecione uma saudação de toocreate assinatura VNet no. Uma VNet existe em uma única assinatura.|
    |**Grupo de recursos**|**Criar novo:** *MyRG*|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) artigo de visão geral.|
    |**Localidade**|*Oeste dos EUA*| Normalmente Olá local que é o local físico de tooyour mais próximo é selecionado.|

    Olá usa redes toocreate de alguns segundos. Depois que ela for criada, você ver hello Azure painel do portal.

6. Com a rede virtual de saudação criado, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **MyVNet** rede virtual no hello **todos os recursos** folha. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir *MyVNet* em Olá **filtrar por nome...** Olá acesso caixa tooeasily VNet.
7. Olá **MyVNet** folha é aberta e exibe informações sobre Olá VNet, conforme mostrado na figura abaixo de saudação:

    ![Diagrama de rede virtual](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Conforme mostrado na imagem anterior hello, clique em **sub-redes** toodisplay uma lista de sub-redes de saudação de saudação VNet. Olá somente sub-rede existente é **front-end**, Olá sub-rede que você criou na etapa 5.
9. No hello MyVNet - folha de sub-redes, clique em **+ sub-rede** toocreate uma sub-rede com hello seguintes informações e clique em **Okey** toocreate subrede hello:

    |**Configuração**|**Valor**|**Detalhes**|
    |---|---|---|
    |**Nome**|*Back-end*|Olá nome deve ser exclusivo dentro da rede virtual hello.|
    |**Intervalo de endereços**|*10.0.1.0/24*|intervalo de saudação especificado deve existir no espaço de endereço Olá definido para a rede virtual hello.|
    |**Grupo de segurança de rede** e **Tabela de rotas**|*None* (padrão)|Os NSGs (Grupos de segurança de rede) serão abordados mais adiante neste artigo. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.|

10. Após a nova subrede Olá é adicionado toohello VNet, você pode fechar Olá **MyVNet – sub-redes** folha, em seguida, feche Olá **todos os recursos** folha.

## <a name="create-vms"></a>Criar máquinas virtuais

Com hello redes e sub-redes criados, você pode criar VMs hello. Para este exercício, ambas as VMs que execute o sistema de operacional de servidor do Windows hello, embora eles podem executar qualquer sistema operacional com suporte pelo Azure, incluindo várias distribuições do Linux diferentes.

### <a name="create-web-server-vm"></a>Criar VM do servidor web Olá

toocreate Olá web server VM, Olá concluir as etapas a seguir:

1. No painel de favoritos portal do Azure hello, clique em **novo**, **de computação**, em seguida, **Datacenter do Windows Server 2016**.
2. Em Olá **Datacenter do Windows Server 2016** folha, clique em **criar**.
3. Em Olá **Noções básicas de** folha que aparece, digite ou selecione Olá valores a seguir e clique em **Okey**:

    |**Configuração**| **Valor**|**Detalhes**|
    |---|---|---|
    |**Nome**|*MyWebServer*|Essa VM serve como um servidor Web ao qual os recursos da Internet se conectam.|
    |**Tipo de disco da VM**|*SSD*|
    |**Nome de usuário**|*Sua escolha*|
    |**Senha e Confirmar senha**|*Sua escolha*|
    | **Assinatura**|*<Your subscription>*|Olá assinatura deve ser Olá a mesma assinatura que você selecionou na etapa 5 da saudação [criar uma rede virtual com duas sub-redes](#create-vnet) deste artigo. Olá VNet que você se conectar a uma VM toomust existe no hello mesmo assinatura Olá VM.|
    |**Grupo de recursos**|**Usar existente:** selecione *MyRG*|Que estamos usando Olá mesmo grupo de recursos, como foi feito Olá VNet, Olá recursos não têm tooexist em Olá mesmo grupo de recursos.|
    |**Localidade**|*Oeste dos EUA*|Olá local deve ser Olá mesmo local que você especificou na etapa 5 da saudação [criar uma rede virtual com duas sub-redes](#create-vnet) deste artigo. Máquinas virtuais e hello VNets que se conectam toomust existem no hello mesmo local.|

4. Em Olá **escolher um tamanho de** folha, clique em *DS1_V2 padrão*, em seguida, clique em **selecione**. Saudação de leitura [tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter uma lista de todos os tamanhos de VM do Windows Azure com suporte.
5. Em Olá **configurações** folha, insira ou selecione Olá valores a seguir e clique em **Okey**:

    |**Configuração**|**Valor**|**Detalhes**|
    |---|---|---|
    |**Armazenamento: usar discos gerenciados**|*Sim*||
    |**Rede virtual**| Selecione *MyVNet*|Você pode selecionar qualquer rede virtual existente no hello mesmo local como Olá VM que você está criando. toolearn mais sobre VNets e sub-redes, ler Olá [rede Virtual](virtual-networks-overview.md) artigo.|
    |**Sub-rede**|Selecione *Front-end*|Você pode selecionar qualquer sub-rede que existe dentro do hello VNet.|
    |**Endereço IP público**|Aceite o padrão de saudação|Um endereço IP público permite que você tooconnect toohello VM de saudação à Internet. toolearn mais informações sobre endereços IP públicos, ler Olá [endereços IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artigo.|
    |**Grupo de Segurança de Rede (firewall)**|Aceite o padrão de saudação|Clique em Olá **MyWebServer (novo)-nsg** portal de saudação padrão NSG criado tooview suas configurações. Em Olá **criar grupo de segurança de rede** folha que é aberta, observe que ele tenha uma regra de entrada que permite o tráfego TCP/3389 (RDP) de qualquer endereço IP de origem.|
    |**Todos os outros valores**|Aceite os padrões de saudação|toolearn mais sobre Olá restantes configurações, ler Olá [sobre VMs](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.|

    Grupos de segurança de rede (NSG) permitem que você toocreate regras de entrada/saída para o tipo de saudação do tráfego de rede que possa fluir tooand de saudação VM. Por padrão, todos os toohello de tráfego de entrada VM é negada. Você pode adicionar regras de entrada adicionais de TCP/80 (HTTP) e TCP/443 (HTTPS) para um servidor Web de produção. Não há nenhuma regra para o tráfego de saída porque, por padrão, todo tráfego de saída é permitido. Você pode adicionar ou remover o tráfego de toocontrol de regras por suas políticas. Saudação de leitura [grupos de segurança de rede](virtual-networks-nsg.md) artigo toolearn mais sobre os NSGs.

6.  Em Olá **resumo** folha, examine as configurações de saudação e clique em **Okey** toocreate Olá VM. Um bloco de status é exibido no painel do portal hello como Olá que VM cria. Pode levar alguns toocreate de minutos. Você não precisa toowait para ele toocomplete. Você pode continuar a próxima etapa toohello durante a saudação que VM é criada.

### <a name="create-database-server-vm"></a>Criar VM do servidor de banco de dados Olá

toocreate Olá banco de dados server VM, Olá concluir as etapas a seguir:

1.  No painel do hello Favoritos, clique em **novo**, **de computação**, em seguida, **Datacenter do Windows Server 2016**.
2.  Em Olá **Datacenter do Windows Server 2016** folha, clique em **criar**.
3.  Em Olá **folha Noções básicas sobre**, insira ou selecione Olá valores a seguir e clique em **Okey**:

    |**Configuração**|**Valor**|**Detalhes**|
    |---|---|---|
    |**Nome**|*MyDBServer*|Essa VM atua como um servidor de banco de dados que Olá web server se conecta ao, mas que Olá Internet não pode se conectar ao.|
    |**Tipo de disco da VM**|*SSD*||
    |**Nome de usuário**|Sua escolha||
    |**Senha e Confirmar senha**|Sua escolha||
    |**Assinatura**|<Your subscription>|Olá assinatura deve ser Olá a mesma assinatura que você selecionou na etapa 5 do hello [criar uma rede virtual com duas sub-redes](#create-vnet) deste artigo.|
    |**Grupo de recursos**|**Usar existente:** selecione *MyRG*|Que estamos usando Olá mesmo grupo de recursos, como foi feito Olá VNet, Olá recursos não têm tooexist em Olá mesmo grupo de recursos.|
    |**Localidade**|*Oeste dos EUA*|Olá local deve ser Olá mesmo local que você especificou na etapa 5 da saudação [criar uma rede virtual com duas sub-redes](#create-vnet) deste artigo.|

4.  Em Olá **escolher um tamanho de** folha, clique em *DS1_V2 padrão*, em seguida, clique em **selecione**.
5.  Em Olá **configurações** folha, insira ou selecione Olá valores a seguir e clique em **Okey**:

    |**Configuração**|**Valor**|**Detalhes**|
    |----|----|---|
    |**Armazenamento: usar discos gerenciados**|*Sim*||
    |**Rede virtual**|Selecione *MyVNet*|Você pode selecionar qualquer rede virtual existente no hello mesmo local como Olá VM que você está criando.|
    |**Sub-rede**|Selecione *Back-end* clicando Olá **sub-rede** caixa, selecionando **Back-end** de saudação **escolha uma sub-rede** folha|Você pode selecionar qualquer sub-rede que existe dentro do hello VNet.|
    |**Endereço IP público**|Nenhum – o endereço padrão Olá clique **nenhum** de saudação **escolher endereço IP público** folha|Sem um endereço IP público, você pode conectar somente toohello VM de outro toohello VM conectada mesma rede virtual. Você não pode se conectar tooit diretamente da saudação da Internet.|
    |**Grupo de Segurança de Rede (firewall)**|Aceite o padrão de saudação| Como o padrão de saudação que NSG criado para Olá MyWebServer VM, esse NSG também tem Olá mesmo padrão de regra de entrada. Você pode adicionar uma regra de entrada adicional a TCP/1433 (MS SQL) para um servidor de banco de dados. Não há nenhuma regra para o tráfego de saída porque, por padrão, todo tráfego de saída é permitido. Você pode adicionar ou remover o tráfego de toocontrol de regras por suas políticas.|
    |**Todos os outros valores**|Aceite os padrões de saudação||

6.  Em Olá **resumo** folha, examine as configurações de saudação e clique em **Okey** toocreate Olá VM. Um bloco de status é exibido no painel do portal hello como Olá que VM cria. Pode levar alguns toocreate de minutos. Você não precisa toowait para ele toocomplete. Você pode continuar a próxima etapa toohello durante a saudação que VM é criada.

## <a name="review"></a>Examinar os recursos

Se você criou uma VNet e duas VMs, Olá portal do Azure criado vários recursos adicionais para você no grupo de recursos de MyRG hello. Examine o conteúdo de Olá Olá MyRG do grupo de recursos executando Olá etapas a seguir:

1. Em Olá **Favoritos** painel, clique em **mais serviços**.
2. Em Olá **mais serviços** painel, digite *grupos de recursos* na caixa de saudação que tenha a palavra hello *filtro* nele. Clique em **grupos de recursos** quando você vê-lo no hello lista filtrada.
3. Em Olá **grupos de recursos** painel, clique em Olá *MyRG* grupo de recursos. Se você tiver muitos grupos de recursos existentes em sua assinatura, você pode digitar *MyRG* na caixa de saudação que contém o texto de saudação *filtrar por nome...* grupo de recursos do MyRG tooquickly acesso hello.
4.  Em Olá **MyRG** folha, você verá esse grupo de recursos Olá contém 12 recursos, como mostrado na figura abaixo de saudação:

    ![Conteúdo do grupo de recursos](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

mais sobre contas de armazenamento, leitura hello, discos e VMs de toolearn [Máquina Virtual](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [disco](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), e [conta de armazenamento](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de visão geral. Você pode ver Olá dois NSGs Olá portal padrão criado para você. Você também pode ver esse portal Olá criado dois recursos de interface (NIC) de rede. Uma NIC permite recursos de tooother de tooconnect uma VM em Olá VNet. Saudação de leitura [NIC](virtual-network-network-interface.md) artigo toolearn mais sobre NICs. portal de saudação também criada um recurso de endereço IP público. Endereços IP públicos são uma configuração para um recurso de endereço IP público. toolearn mais informações sobre endereços IP públicos, ler Olá [endereços IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artigo.

## <a name="connect-to-from-vms"></a>Conecte-se toohello VMs

Com sua rede virtual e duas máquinas virtuais criadas, agora você pode conectar VMs toohello completando as etapas de saudação do hello seções a seguir:

### <a name="connect-from-internet"></a>Conecte-se a VM do servidor web toohello de saudação da Internet

tooconnect toohello web VM do servidor de saudação à Internet, Olá concluir as etapas a seguir:

1. No portal de Olá, grupo de recursos de MyRG abrir Olá Concluindo Olá etapas Olá [analise recursos](#review) deste artigo.
2. Em Olá **MyRG** folha, clique em Olá **MyWebServer** VM.
3. Em Olá **MyWebServer** folha, clique em **conectar**, conforme mostrado na figura abaixo de saudação:

    ![Conecte-se a VM do servidor tooweb](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Permitir Olá de toodownload seu navegador *MyWebServer.rdp* de arquivo e, em seguida, abri-lo.
5. Se você receber uma caixa de diálogo informando você Editor de conexão remota Olá Olá não pode ser verificadas, clique em **conectar**.
6. Ao inserir suas credenciais, certifique-se de logon com o nome de usuário de saudação e senha que você especificou na etapa 3 do hello [servidor web da saudação criar VM](#create-web-server-vm) deste artigo. Se hello **a segurança do Windows** caixa que aparece não lista as credenciais corretas de saudação, talvez seja necessário tooclick **mais opções**, em seguida, **usar uma conta diferente**, portanto, você pode Especifica senha e o nome de usuário correto Olá). Clique em **Okey** tooconnect toohello VM.
7. Se você receber um **Conexão de área de trabalho remota** caixa informando que Olá a identidade do computador remoto Olá não pode ser verificado, clique em **Sim**.
8. Agora você está conectado toohello MyWebServer VM de saudação à Internet. Deixe conexão de área de trabalho remota Olá etapas de saudação toocomplete aberto na próxima seção, Olá.

conexão remota Olá é toohello endereço do IP público atribuído toohello IP endereço recurso Olá portal público criado na etapa 5 do hello [criar uma rede virtual com duas sub-redes](#create-vnet) deste artigo. conexão Olá é permitida porque a regra padrão de saudação criado no hello **MyWebServer nsg** toohello VM de qualquer endereço IP de origem de entrada do NSG permitido TCP/3389 (RDP). Se você tentar tooconnect toohello VM em qualquer outra porta, conexão Olá falha, a menos que você adicione regras de entrada adicionais toohello NSG permitindo Olá portas adicionais.

>[!NOTE]
>Se você adicionar as regras de entrada adicionais toohello NSG, certifique-se de que Olá mesmas portas estão abertas no firewall do Windows hello ou Olá falha de conexão.
>

### <a name="connect-to-internet"></a>Conecte-se toohello da Internet do servidor de web hello VM

tooconnect toohello saída da Internet do servidor de web hello VM, Olá concluir as etapas a seguir:

1. Se você ainda não tiver um toohello de conexão remota MyWebServerVM abrir, fazer uma conexão remota de toohello VM completando as etapas de saudação do hello [conectar toohello web VM do servidor de saudação Internet](#connect-from-internet) deste artigo.
2. Na área de trabalho do Windows hello, abra o Internet Explorer. Em Olá **instalação do Internet Explorer 11** caixa de diálogo, clique em **não usar configurações recomendadas**, em seguida, clique em **Okey**. É recomendado tooaccept Olá configurações recomendada para um servidor de produção.
3. Na barra de endereços do Internet Explorer hello, digite [bing.com](http:www.bing.com). Se você receber uma caixa de diálogo do Internet Explorer, clique em **adicionar**, em seguida, **adicionar** em Olá **sites confiáveis** caixa de diálogo e clique em **fechar**. Repita esse processo para outras caixas de diálogo do Internet Explorer.
4. Página de pesquisa no hello Bing, digite *whatsmyipaddress*, Olá Lupa botão. Bing retorna Olá pública IP endereço atribuído toohello público recurso de endereço IP criado pelo portal hello quando você criou Olá VM. Se você examinar configurações Olá Olá **MyWebServer ip** recursos, consulte Olá mesmo endereço IP atribuído o recurso de endereço IP público toohello, conforme mostrado na imagem de saudação que segue. Olá IP endereço atribuído tooyour VM é diferente no entanto.

    ![Conecte-se a VM do servidor tooweb](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Deixe conexão de área de trabalho remota Olá etapas de saudação toocomplete aberto na próxima seção, Olá.

Você está toohello tooconnect capaz de Internet da saudação VM porque todos os conectividade de saída de hello VM é permitida por padrão. Você pode limitar a conectividade de saída com a adição de adição regras toohello NSG aplicada toohello NIC, Olá de sub-rede toohello NIC está conectada, ou ambos.

Se Olá VM for colocada em Olá parado (desalocado) estado usando portal hello, endereço IP público de saudação pode alterar. Se você precisar que Olá público endereço IP nunca alteração, você pode usar o método de alocação estática Olá para o endereço IP hello, em vez de método de alocação dinâmica de hello (que é o padrão de saudação). toolearn mais sobre as diferenças entre os métodos de alocação de Olá ler Olá [tipos e métodos de alocação de endereços IP](virtual-network-ip-addresses-overview-arm.md) artigo.

### <a name="webserver-to-dbserver"></a>Conecte-se a VM do servidor de banco de dados toohello da VM do servidor web Olá

tooconnect toohello banco de dados server VM do servidor de web hello VM, Olá concluir as etapas a seguir:

1. Se você ainda não tiver um toohello de conexão remota MyWebServer VM abrir, fazer uma conexão remota de toohello VM completando as etapas de saudação do hello [conectar toohello web VM do servidor de saudação Internet](#connect-from-internet) deste artigo.
2. Clique botão de início Olá no canto inferior esquerdo de saudação da área de trabalho do Windows hello e comece a digitar *área de trabalho remota*. Quando exibe a lista do menu Iniciar Olá **Conexão de área de trabalho remota**, clique nele.
3. Em Olá **Conexão de área de trabalho remota** caixa de diálogo, digite *MyDBServer* Olá nome do computador e clique em **conectar**.
4. Insira o nome de usuário de saudação e senhas que você digitou na etapa 3 do hello [criar o VM do servidor de banco de dados de saudação](#create-database-server-vm) seção deste artigo, em seguida, clique em **Okey**.
5. Se você receber uma caixa de diálogo informando que a identidade do computador remoto Olá Olá não pode ser verificada, clique em **Sim**.
6. Deixe a conexão de área de trabalho remota Olá servidores tooboth toocomplete abrir Olá as etapas na próxima seção, Olá.

Você está servidor de banco de dados de toohello conexão do toomake capaz de saudação VM Olá web do servidor de VM para Olá motivos a seguir:

- Conexões de entrada de TCP/3389 estão habilitadas para qualquer IP de origem no padrão de saudação NSG criado na etapa 5 do hello [criar o VM do servidor de banco de dados de saudação](#create-database-server-vm) deste artigo.
- Você iniciou a conexão de saudação do servidor de web hello VM, que é conectado toohello mesma rede virtual como o servidor de banco de dados de saudação VM. tooconnect tooa VM que não tem um tooit de endereço atribuído de IP público, você deve se conectar de outro toohello VM conectada mesmo VNet, mesmo se Olá VM estiver conectado tooa outra sub-rede.
- Mesmo que VMs Olá sub-redes toodifferent conectado, o Azure cria as rotas padrão que habilitam a conectividade entre as sub-redes. Você pode substituir as rotas padrão Olá criando seu próprio porém. Saudação de leitura [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo toolearn mais sobre o roteamento no Azure.

Se você tentar tooinitiate um servidor de banco de dados de toohello VM conexão remota de saudação da Internet, como você fez no hello [conectar toohello web VM do servidor de saudação Internet](#connect-from-internet) seção deste artigo, você vê que Olá **conectar** opção fica esmaecida. Conecte-se esmaecidas porque não há nenhum toohello de endereço atribuído de IP público VM, portanto tooit conexões de entrada de saudação da Internet não são possíveis.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Conecte-se toohello da Internet do servidor de banco de dados de saudação VM

Conecte-se toohello saída à Internet do servidor de banco de dados de saudação VM Concluindo Olá etapas a seguir:

1. Se você ainda não tiver um toohello de conexão remota MyDBServer VM abrir de saudação MyWebServer VM, Olá concluir etapas no hello [servidor de banco de dados de toohello conectar VM do servidor de web hello VM](#webserver-to-dbserver) deste artigo.
2. Na área de trabalho do Windows hello em Olá MyDBServer VM, abra o Internet Explorer e responder a caixas de diálogo toohello como você fez nas etapas 2 e 3 do hello [conectar toohello da Internet do servidor de web hello VM](#connect-to-internet) deste artigo.
3. Na barra de endereço hello, digite [bing.com](http:www.bing.com).
4. Clique em **adicionar** na caixa de diálogo do Internet Explorer Olá for exibida, em seguida, **adicionar**, em seguida, **fechar** em Olá **confiáveis** caixa de diálogo de sites. Conclua essas etapas em todas as caixas de diálogo adicionais que aparecerem.
5. Página de pesquisa no hello Bing, digite *whatsmyipaddress*, Olá Lupa botão. Bing retorna Olá pública IP endereço atribuído atualmente toohello VM Olá infraestrutura do Azure. 6. Feche Olá remote desktop toohello MyDBServer VM de saudação MyWebServer VM e fechar Olá conexão remota toohello MyWebServer VM.

Olá toohello de conexão de saída da Internet é permitido porque todo o tráfego de saída é permitido por padrão, mesmo que um recurso de endereço IP público não está atribuído a toohello MyDBServer VM. Todas as VMs, por padrão, são capazes de tooconnect saída toohello da Internet, com ou sem um recurso atribuído endereço IP público toohello VM. Você não é capaz de tooconnect toohello público de endereços IP de saudação da Internet no entanto, como era capaz de toofor Olá MyWebServer VM que tem um IP público endereço recurso atribuído.

## <a name="delete-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:

1. grupo de recursos tooview Olá MyRG criado neste artigo, concluir etapas Olá em 1 a 3 [analise recursos](#review) deste artigo. Uma vez, analise os recursos de saudação no grupo de recursos de saudação. Se você criou o grupo de recursos de MyRG hello, por etapas anteriores, você verá 12 recursos de saudação mostrados na imagem de saudação na etapa 4.
2. Na folha de MyRG hello, clique em Olá **excluir** botão.
3. Hello portal exige que você tootype nome de saudação do hello tooconfirm de grupo de recursos que você deseja toodelete-lo. Se você vir recursos diferentes de recursos Olá mostrados na etapa 4 do hello [Analise os recursos de](#review) seção deste artigo, clique em **Cancelar**. Se você ver somente os recursos de saudação 12 criados como parte deste artigo, digite *MyRG* para o nome do grupo de recursos hello, em seguida, clique em **excluir**. Excluir um grupo de recursos exclui todos os recursos no grupo de recursos de saudação, portanto, sempre tooconfirm-se de conteúdo de saudação de um grupo de recursos antes de excluí-lo. portal de saudação exclui todos os recursos contidos no grupo de recursos hello, em seguida, exclui o grupo de recursos de saudação em si. Esse processo leva vários minutos.

## <a name="next-steps"></a>Próximas etapas

Neste exercício, você criou uma VNet e duas VMs. Você especificou configurações personalizadas durante a criação da VM e aceitou várias configurações padrão. É recomendável que você leia Olá artigos a seguir antes de implantar VMs, tooensure entender todas as configurações disponíveis e produção VNets:

- [Redes virtuais](virtual-networks-overview.md)
- [Endereços IP públicos](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Interfaces de rede](virtual-network-network-interface.md)
- [Grupos de segurança de rede](virtual-networks-nsg.md)
- [Máquinas virtuais](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
