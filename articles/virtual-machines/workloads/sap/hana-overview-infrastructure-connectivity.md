---
title: "aaaInfrastructure e conectividade tooSAP HANA no Azure (instâncias grandes) | Microsoft Docs"
description: "Configure conectividade necessária infraestrutura toouse SAP HANA no Azure (instâncias grandes)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infraestrutura e conectividade para o SAP HANA (instâncias grandes) no Azure 

Algumas definições prévias antes de ler este guia. Em [Visão geral e arquitetura do SAP HANA (instâncias grandes) no Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture), apresentamos duas classes diferentes de unidades de Instância Grande do HANA com:

- S72, S72m, S144, S144m, S192 e S192m, que chamamos tooas Olá ', classe de tipo' de SKUs.
- S384, S384m, S384xm, S576, S768 e S960, que chamamos tooas Olá 'Classe de tipo II' de SKUs.

especificadores de classe Olá são toobe contínuo usado Olá HANA instância grande documentação tooeventually consulte toodifferent recursos e requisitos com base em SKUs do HANA grande instância.

Outras definições que usamos frequentemente são:
- **Grande carimbo da instância:** uma pilha de infraestrutura de hardware que é o SAP HANA TDI certificada e dedicado de instâncias do SAP HANA toorun dentro do Azure.
- **SAP HANA no Azure (instâncias grande):** nome oficial da oferta de saudação em instâncias do HANA toorun do Azure no SAP HANA TDI certified hardware que é implantado em carimbos de instância grande em diferentes regiões do Azure. Olá relacionados ao termo **instância grande HANA** é curta para o SAP HANA no Azure (instâncias grandes) e é amplamente usada neste guia de implantação técnica.
 

Após a compra de saudação do HANA SAP no Azure (instâncias grandes) é finalizada entre você e Olá, equipe de contas da Microsoft enterprise, hello seguintes informações são necessárias pelo Microsoft toodeploy HANA grande instância unidades:

- Nome do cliente
- Informações de contatos comerciais (incluindo endereço de email e número de telefone)
- Informações de contatos técnicos (incluindo endereço de email e número de telefone)
- Informações de contatos da rede técnica (incluindo endereço de email e número de telefone)
- Região de implantação do Azure (Oeste dos EUA, Leste dos EUA, Leste da Austrália, Sudeste da Austrália, Europa Ocidental e Europa Setentrional a partir de julho) 
- 2017)
- Confirmar SAP HANA no Azure (Instâncias Grandes) SKU (configuração)
- Como já detalhadas no documento de arquitetura e visão geral de saudação para instâncias do HANA grande, para cada região do Azure que está sendo implantada:
    - Uma/29 intervalo de endereços IP para conexões ER P2P VNets do Azure tooHANA grandes instâncias
    - Um /24 bloco CIDR usado para o Pool de IP do HANA grandes instâncias de servidor de saudação
- usado no atributo de espaço de endereço de rede virtual de saudação de cada rede virtual do Azure que se conecta toohello HANA grandes instâncias dos valores de intervalo de endereço Olá IP
- Dados para cada sistema de Instâncias Grandes HANA:
  - Nome de host desejado - o ideal é usar o nome de domínio totalmente qualificado.
  - Endereço IP desejado para a unidade de instância grande HANA Olá fora Olá intervalo de endereços do Pool de IP do servidor - tenha em mente que Olá 30 primeiros endereços IP no intervalo de endereços são reservados para uso interno em HANA grandes instâncias de Pool de IP de servidor de saudação
  - Nome do SAP HANA SID para instância do SAP HANA hello (toocreate necessário Olá em disco necessário relacionados à SAP HANA volumes). Olá HANA SID é necessário para criar permissões Olá para <sidadm> nos volumes NFS Olá, que está obtendo a unidade de instância grande HANA toohello anexado. Ele também é usado como um dos componentes de nome Olá Olá dos volumes de disco que ser montados. Se você quiser toorun mais de uma instância do HANA na unidade Olá, é necessário toolist vários SIDs do HANA. Cada uma obtém um conjunto separado de volumes atribuídos.
  - Olá groupid Olá hana sidadm usuário tenha Olá SO Linux é necessária toocreate volumes de disco relacionados ao SAP HANA hello. Olá instalação SAP HANA geralmente cria o grupo de sapsys de saudação com uma id de grupo de 1001. usuário do hana sidadm Olá faz parte do grupo
  - Olá userid Olá hana sidadm usuário tenha Olá SO Linux é necessária toocreate volumes de disco relacionados ao SAP HANA hello. Se você estiver executando várias instâncias do HANA na unidade Olá, é necessário toolist todos Olá <sid>adm usuários 
- ID de assinatura do Azure para toowhich de assinatura do Azure Olá HANA SAP no Azure HANA grandes instâncias serão toobe diretamente conectado. Essa ID de assinatura faz referência a saudação assinatura do Azure, que vai toobe cobrado por hello instância grande HANA unidades.

Depois de fornecer Olá informações, provisiona Microsoft HANA SAP no Azure (instâncias grandes) e retornará Olá informações necessárias toolink seus VNets do Azure tooHANA grandes instâncias e tooaccess Olá instância grande HANA unidades.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Conectar máquinas virtuais do Azure tooHANA grandes instâncias

Como já mencionado no [visão geral do SAP HANA (grandes instâncias) e arquitetura no Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) implantação mínima de saudação do HANA grandes instâncias com a camada do aplicativo SAP Olá na pesquisa do Azure, como:

![Rede virtual do Azure conectado tooSAP HANA no Azure (instâncias grandes) e no local](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Levando em Olá lado da rede virtual do Azure, percebemos Olá necessidade de:

- definição de saudação de uma rede virtual do Azure que está indo toobe usado toodeploy Olá VMs de camada do aplicativo SAP Olá em.
- Isso automaticamente significa que Olá Vnet do Azure é definida que é realmente Olá um usado toodeploy Olá VMs em uma sub-rede padrão.
- Olá VNet do Azure que é criado deve toohave pelo menos uma sub-rede VM e uma sub-rede de Gateway de rota expressa. Intervalos de endereços IP hello como discutido na Olá seções a seguir e especificados devem ser atribuídas a essas sub-redes.

Portanto, vamos examinar mais detalhadamente Olá criação de rede virtual do Azure para grandes instâncias do HANA

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Olá criar rede virtual do Azure para grandes instâncias do HANA

>[!Note]
>Olá VNet do Azure para instância grande HANA deve ser criado usando o modelo de implantação do Azure Resource Manager hello. Não há suporte para Hello mais antigas do Azure modelo de implantação, conhecido como o modelo de implantação clássico com hello solução instância grande HANA.

Olá rede virtual pode ser criada usando Olá portal do Azure, o PowerShell, o modelo do Azure ou o CLI do Azure (consulte [criar uma rede virtual usando o portal do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Saudação de exemplo a seguir, analisamos uma rede virtual criada por meio de saudação portal do Azure.

Se considerarmos às definições de saudação de uma rede virtual do Azure por meio de saudação portal do Azure, vamos dar uma olhada em algumas das definições de saudação e como aquelas relacionam toowhat é a lista de intervalos de endereços IP diferentes. Como estamos falando Olá **espaço de endereço**, queremos dizer o espaço de endereço Olá Olá VNet do Azure é permitido toouse. Este espaço de endereço também é um intervalo de endereços Olá Olá usa VNet para a propagação de rotas BGP. Esse **Espaço de Endereço** pode ser visto aqui:

![Espaço de endereço do VNet do Azure exibidos no hello portal do Azure](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

No caso de Olá anterior, com 10.16.0.0/16, Olá VNet do Azure foi fornecido um toouse de intervalo de endereço IP em vez disso, grande e de longa. Significa que todos os intervalos de endereços IP de saudação de subredes subsequentes nesta rede podem ter seus intervalos dentro desse espaço de endereço' '. Geralmente, não recomendamos tal um intervalo de endereços grande para a rede virtual único no Azure. Mas obter um passo adiante, vamos dar uma olhada em sub-redes Olá definidos no hello VNet do Azure:

![Sub-redes de Rede Virtual do Azure e seus intervalos de endereços IP](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Como você pode ver, examinamos uma VNet com uma primeira sub-rede VM (aqui chamado “padrão”) e uma sub-rede chamada “GatewaySubnet”.
No hello seção a seguir, nós nos referimos toohello intervalo de endereços IP de sub-rede hello, que foi chamado 'default' em gráficos de saudação como **intervalo de endereços IP de sub-rede de VM do Azure**. No hello seções a seguir, nós nos referimos toohello intervalo de endereços IP de sub-rede de Gateway do hello como **o intervalo de endereços IP de sub-rede de Gateway de rede virtual**. 

No caso de Olá demonstrado pelo gráfico de saudação dois acima, verá que Olá **espaço de endereço de rede virtual** abrange ambos, hello **intervalo de endereços IP de sub-rede de VM do Azure** e hello **endereço IP de sub-rede do Gateway de rede virtual intervalo**. 

Em outros casos em que precisar tooconserve ou ser específicos com seus intervalos de endereços IP, você pode restringir Olá **espaço de endereço de rede virtual** de um intervalos específicos de rede virtual toohello que está sendo usado por cada sub-rede. Nesse caso, você pode definir Olá **espaço de endereço de rede virtual** de uma rede virtual específico como vários intervalos conforme mostrado aqui:

![Espaço de Endereço de Rede Virtual do Azure com dois espaços](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

Nesse caso, Olá **espaço de endereço de rede virtual** tem dois espaços definidos. Esses dois espaços, intervalos de endereços IP idênticos toohello definidos para **intervalo de endereços IP de sub-rede de VM do Azure** e hello **o intervalo de endereços IP de sub-rede de Gateway de rede virtual.**

Você pode usar qualquer padrão de nomenclatura que desejar para essas sub-redes de locatário (sub-redes de VM). No entanto, **sempre deve haver uma e apenas uma sub-rede de gateway para cada VNet** que se conecta toohello SAP HANA no circuito de rota expressa do Azure (instâncias grandes). E **esta sub-rede de gateway deve sempre ser denominado "GatewaySubnet"** tooensure a localização correta de gateway de rota expressa hello.

> [!WARNING] 
> É fundamental que dessa sub-rede de gateway Olá sempre é denominada "GatewaySubnet".

Várias sub-redes VM podem ser usadas, até mesmo utilizando intervalos de endereços não contíguas. Mas como mencionado anteriormente, esses intervalos de endereços devem ser abordados por Olá **espaço de endereço de rede virtual** de saudação redes de forma agregada ou em uma lista de saudação exato intervalos de sub-redes VM hello e Olá sub-rede de gateway.

Resumindo fatos importantes de saudação sobre uma rede virtual do Azure que se conecta tooHANA grandes instâncias:

- Você precisa toosubmit tooMicrosoft Olá **espaço de endereço de rede virtual** ao executar uma implantação inicial do HANA grandes instâncias. 
- Olá **espaço de endereço de rede virtual** pode ser um intervalo maior do que abrange o intervalo de saudação para o intervalo de endereços IP de sub-rede de VM do Azure e o intervalo de endereços IP de sub-rede de Gateway de rede virtual hello.
- Ou você pode enviar como **espaço de endereço de rede virtual** vários intervalos que abrangem Olá IP de diferentes intervalos de intervalo de endereços IP de sub-rede VM e o intervalo de endereços IP de sub-rede de Gateway de rede virtual Olá de endereço.
- Olá definido **espaço de endereço de rede virtual** é usada propagação de roteamento de BGP.
- Olá nome da sub-rede de Gateway Olá deve ser: **"GatewaySubnet".**
- Olá **espaço de endereço de rede virtual** é usado como um filtro Olá instância grande HANA lado tooallow ou impedir unidades de instância grande HANA toohello tráfego do Azure. Se hello informações de roteamento de BGP de saudação VNet do Azure e intervalos de endereços IP de saudação configurados para filtragem Olá lado instância grande HANA não coincidirem, podem surgir problemas de conectividade.
- Há alguns detalhes sobre a sub-rede de Gateway de saudação que são discutidas mais para baixo na seção 'Conectar-se um tooHANA redes grandes ExpressRoute de instância'



### <a name="different-ip-address-ranges-toobe-defined"></a>Intervalos de endereço IP diferente toobe definido 

Já, apresentamos alguns toodeploy de necessário intervalos HANA grandes instâncias nas seções anteriores de endereço IP hello. Mas há mais alguns intervalos de endereços IP que são importantes. Vamos analisar alguns detalhes adicionais. Olá seguintes endereços IP dos quais nem todos os necessário toobe enviado tooMicrosoft necessário toobe definido antes de enviar uma solicitação para a implantação inicial:

- **Espaço de endereço de rede virtual:** apresentado anteriormente, é como já ou são o endereço IP hello intervalo você atribuiu (ou planejar tooassign) tooyour endereço Space no hello redes virtuais do Azure (VNet) conectando toohello instância grande do SAP HANA ambiente. É recomendável que esse parâmetro do espaço de endereço é um valor de várias linha composto Olá intervalos de sub-rede de VM do Azure e hello intervalo de sub-rede de Gateway do Azure conforme mostrado no gráfico de saudação anteriormente. Esse intervalo não deve sobrepor seu local ou intervalos de endereços do Pool de IP do servidor ou ER P2P. Como tooget isso ou esses intervalos de endereço IP? A equipe de rede corporativa ou o provedor de serviço deve fornecer um ou vários Intervalos de Endereços IP que não são usados dentro da rede. Exemplo: Se sua sub-rede da VM do Azure (consulte anteriormente) é 10.0.1.0/24 e sua sub-rede do Gateway do Azure (veja a seguir) é 10.0.2.0/28, em seguida, seu espaço de endereço de rede virtual do Azure é recomendável toobe duas linhas; 10.0.1.0/24 e 10.0.2.0/28. Embora os valores de espaço de endereço de saudação podem ser agregados, é recomendável combiná-la em intervalos de sub-rede toohello tooavoid de reutilização acidental de IP não usado intervalos de endereços em espaços de endereço maior no hello futuras em outro lugar na sua rede. **Olá espaço de endereço de rede virtual é um intervalo de endereços IP, na qual toobe necessidades enviada tooMicrosoft na solicitação de uma implantação inicial**

- **Intervalo de endereços IP do Azure VM sub-rede:** este intervalo de endereços IP como discutido anteriormente já, é hello um você atribuiu (ou planeja tooassign) toohello parâmetro de sub-rede de rede virtual do Azure na VNET do Azure, conectar-se o ambiente de instância do SAP HANA grande toohello . Este intervalo de endereços IP é usado tooassign IP endereços tooyour VMs do Azure. endereços IP de saudação fora desse intervalo são permitidos tooconnect tooyour instância grande do SAP HANA servidor (es). Se necessário, podem ser usadas várias sub-redes de VM do Azure. Um bloco CIDR /24 é recomendado pela Microsoft para cada sub-rede de VM do Azure. Este intervalo de endereço deve ser uma parte dos valores hello usado em Olá espaço de endereço de rede virtual do Azure. Como tooget esse intervalo de endereços IP? A equipe de rede corporativa ou o provedor de serviço deve fornecer um Intervalo de Endereços IP que não estejam sendo usados atualmente na rede.

- **Intervalo de endereços IP de sub-rede de Gateway de rede virtual:** dependendo Olá recursos planejar toouse, hello recomendado tamanho seria:
   - Gateway do ExpressRoute de ultra desempenho: bloco de endereço /26 – necessário para a classe do Tipo II de SKUs
   - Coexistência com VPN e ExpressRoute usando um Gateway de ExpressRoute de alto desempenho (ou menor): bloco de endereço /27
   - Todas as outras situações: bloco de endereço /28. Este intervalo de endereço deve ser uma parte dos valores de saudação usada em valores de "Espaço de endereço de rede virtual" hello. Este intervalo de endereço deve ser uma parte dos valores de saudação usada em valores de espaço de endereço de rede virtual do Azure Olá que você precisa toosubmit tooMicrosoft. Como tooget esse intervalo de endereços IP? A equipe de rede corporativa ou o provedor de serviço deve fornecer um Intervalo de Endereços IP que não estejam sendo usados atualmente na rede. 

- **Intervalo para P2P ER conectividade de endereços:** este intervalo é o intervalo IP Olá para sua conexão de rota expressa de instância grande (ER) do SAP HANA P2P. Este intervalo de endereços IP deve ser um intervalo de endereços IP CIDR /29. Esse intervalo não deve sobrepor seu local ou outros intervalos de endereços IP do Azure. Este intervalo de endereços IP é usado tooset a conectividade de saudação ER dos servidores Gateway de rota expressa do Azure VNet toohello instância grande do SAP HANA. Como tooget esse intervalo de endereços IP? A equipe de rede corporativa ou o provedor de serviço deve fornecer um Intervalo de Endereços IP que não estejam sendo usados atualmente na rede. **Este intervalo é de um intervalo de endereços IP, na qual toobe necessidades enviada tooMicrosoft na solicitação de uma implantação inicial**
  
- **O intervalo de endereços do Pool do IP do servidor:** desse intervalo de endereços IP é usado tooassign Olá individuais tooHANA instância grande servidores de endereços IP. Olá recomendado tamanho da sub-rede é um /24 CIDR bloquear - mas se necessária pode ser menor mínimo tooa do fornecimento de 64 endereços IP. Desse intervalo, hello 30 primeiros endereços IP são reservados para uso pela Microsoft. Certifique-se de que esse fato seja considerado ao escolher o tamanho de saudação do intervalo de saudação. Esse intervalo não deve sobrepor seu local ou outro IP Azure endereços. Como tooget esse intervalo de endereços IP? Seu provedor de serviço ou de equipe de rede corporativa deve fornecer um intervalo de endereços IP que não estejam em uso em sua rede. Um /24 (recomendado) exclusivo CIDR bloquear toobe usado para atribuir endereços IP específicos Olá necessários para o SAP HANA no Azure (instâncias grandes). **Este intervalo é de um intervalo de endereços IP, na qual toobe necessidades enviada tooMicrosoft na solicitação de uma implantação inicial**
 
Se você precisar toodefine e planejar os intervalos de endereços IP hello acima, todos os não-los necessário tooMicrosoft toobe transmitido. toosummarize Olá acima, intervalos de endereços IP de saudação são tooMicrosoft tooname necessários são:

- Espaços de Endereço de Rede Virtual do Azure
- Intervalo de endereços para conectividade de ER-P2P
- Intervalo de Endereços do Pool de IPs do Servidor

Adicionando VNets adicionais que precisam tooconnect tooHANA grandes instâncias, exige que você toosubmit Olá novo espaço de endereço de rede virtual do Azure está adicionando tooMicrosoft. 

A seguir é um exemplo de diferentes intervalos de saudação e alguns intervalos de exemplo que for necessário tooconfigure e eventualmente fornece tooMicrosoft. Como você pode ver, o valor Olá Olá espaço de endereço de rede virtual do Azure não é agregado no primeiro exemplo de hello, mas é definido de intervalos de saudação de saudação primeira VM do Azure sub-rede intervalo de endereços IP e o intervalo de endereços IP de sub-rede de Gateway de rede virtual Olá. Intervalos de endereços usando várias sub-redes VM no hello VNet do Azure seria trabalho adequadamente Configurando e enviando Olá IP adicionais Olá adicionais sub-redes de VM como parte da saudação espaço de endereço de rede virtual do Azure.

![Intervalos de endereços IP necessários na implantação mínima do SAP HANA no Azure (Instâncias Grandes)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

Você também tem a possibilidade de saudação de agregar dados Olá enviar tooMicrosoft. Nesse caso, Olá espaço de endereço de rede virtual do Azure do hello só inclui um espaço. Usando intervalos de endereços IP de saudação usados no exemplo hello anteriores. Esse Espaço de endereço da VNet agregado poderá ser semelhante ao seguinte:

![Segunda possibilidade de intervalos de endereços IP necessários na implantação mínima do SAP HANA no Azure (Instâncias Grandes)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Como você pode ver acima, em vez de dois intervalos menores que definiu o espaço de endereço de saudação do hello VNet do Azure, temos um intervalo maior do que abrange 4096 endereços IP. Uma definição grande do espaço de endereço de saudação deixa alguns grandes intervalos não utilizados. Como Olá valor (es) de espaço de endereço de rede virtual é usados para a propagação de rotas BGP, o uso de Olá intervalos não utilizados no local ou em outro lugar na sua rede pode causar problemas de roteamento. Portanto, é recomendado tookeep Olá que espaço de endereço estreitamente alinhado com o espaço de endereço de sub-rede real Olá usado. Se necessário, sem incorrer em tempo de inatividade Olá VNet, você pode sempre adicionar novos valores de espaço de endereço mais tarde.
 
> [!IMPORTANT] 
> Cada endereço IP do espaço de endereço de rede virtual do intervalo de ER-P2P, Pool de IP do servidor, do Azure deve **não** se sobrepõem uns com os outros ou qualquer outro intervalo usado em outro lugar na sua rede; cada um deve ser discreta e como gráficos de saudação dois Mostrar anterior, talvez não seja um subrede de qualquer outro intervalo. Se ocorrerem sobreposições entre intervalos, Olá VNet do Azure não pode se conectar toohello circuito de rota expressa.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Próximas etapas após a definição de intervalos de endereços
Após a definição de intervalos de endereços IP hello, hello seguintes atividades necessário toohappen:

1. Envie intervalos de endereços IP Olá para o espaço de endereço de rede virtual do Azure, conectividade de ER P2P hello e o intervalo de endereços do Pool do IP do servidor, junto com outros dados que foi listados no início de saudação do documento de saudação. Neste momento, você também pode iniciar toocreate Olá redes e sub-redes de VM hello. 
2. Um circuito de rota expressa é criado pela Microsoft entre sua assinatura do Azure e o carimbo de instância grande HANA hello.
3. Uma rede de locatário é criada no carimbo de instância grande Olá pela Microsoft.
4. Microsoft configura endereços IP de seu espaço de endereço de rede virtual do Azure se comunica com HANA grandes instâncias de rede no hello SAP HANA em tooaccept de infraestrutura do Azure (instâncias grandes).
5. Dependendo Olá adquirido específico do SAP HANA no SKU do Azure (instâncias grandes), a Microsoft atribui uma unidade de computação em uma rede de locatário, alocar e montar o armazenamento e instalar o sistema operacional de saudação (SUSE ou Red Hat Linux). Endereços IP para essas unidades são tirados Olá enviada tooMicrosoft de intervalo de endereço de Pool de IP do servidor.

No final de Olá Olá do processo de implantação, a Microsoft oferece Olá tooyou de dados a seguir:
- Informações necessárias tooconnect seu circuito de rota expressa do Azure VNet(s) toohello que se conecta a VNets do Azure tooHANA grandes instâncias:
     - Chaves de autorização
     - PeerID de ExpressRoute
- Dados tooaccess HANA grandes instâncias depois de estabelecida circuito de rota expressa e rede virtual do Azure.

Você também pode encontrar sequência Olá de se conectar a instâncias grandes HANA documento hello [terminar tooEnd programa de instalação do SAP HANA grandes instâncias](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Muitas das Olá etapas a seguir são mostradas em um exemplo de implantação nesse documento. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>Conectando um tooHANA VNet ExpressRoute de instância grande

Conforme definido todos os intervalos de endereços IP hello e agora tem dados saudação volta da Microsoft, você pode iniciar a conexão Olá VNet que você criou antes tooHANA grandes instâncias. Uma vez Olá que vnet do Azure é criado, um gateway de rota expressa deve ser criado em Olá VNet toolink Olá VNet toohello circuito de rota expressa que conecta o locatário do cliente toohello no carimbo de instância grande hello.

> [!NOTE] 
> Esta etapa pode levar too30 minutos toocomplete, como o novo gateway de saudação é criado no hello designado a assinatura do Azure e, em seguida, conectado toohello especificado VNet do Azure.

Se já existir um gateway, verifique se ele é um gateway de ExpressRoute ou não. Caso contrário, o gateway de saudação deve ser excluído e recriado como um gateway de rota expressa. Se um gateway de rota expressa já está estabelecido, como Olá que vnet do Azure já está conectado toohello circuito de rota expressa para conectividade local, passe toohello VNets vinculação seção abaixo.

- Usar o hello (novo) [portal do Azure](https://portal.azure.com/), ou toocreate PowerShell um gateway VPN ExpressRoute conectado tooyour VNet.
  - Se você usar Olá portal do Azure, adicione um novo **Gateway de rede Virtual** e, em seguida, selecione **ExpressRoute** como tipo de saudação do gateway.
  - Se você escolher o PowerShell em vez disso, primeiro Baixe e use hello mais recente [SDK do Azure PowerShell](https://azure.microsoft.com/downloads/) tooensure uma experiência ideal. Olá comandos a seguir cria um gateway de rota expressa. textos Olá precedido por um  _$_  são variáveis definidas pelo usuário que toobe necessidade atualizado com as informações específicas.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

Neste exemplo, Olá SKU do gateway de alto desempenho foi usado. As opções são HighPerformance ou UltraPerformance como Olá somente SKUs de gateway que têm suporte para o SAP HANA no Azure (instâncias grandes).

> [!IMPORTANT]
> Para tipos de HANA grandes instâncias de saudação SKU S384, S384m, S384xm, S576, S768 e S960 (tipo de classe II SKUs), hello uso da saudação UltraPerformance SKU de Gateway é obrigatório.

### <a name="linking-vnets"></a>Como vincular redes virtuais

Agora que hello VNet do Azure tem um gateway de rota expressa, você pode usar informações de autorização Olá fornecidas pelo Microsoft tooconnect Olá rota expressa gateway toohello SAP HANA no circuito de rota expressa do Azure (instâncias grandes) criado para essa conectividade. Esta etapa pode ser realizada usando Olá portal do Azure ou o PowerShell. portal de saudação é recomendado, porém instruções do PowerShell são da seguinte maneira. 

- Executar Olá comandos para cada gateway de rede virtual usando um AuthGUID diferente para cada conexão a seguir. duas primeiras entradas de saudação mostradas na seguinte de script hello são provenientes das informações de saudação fornecidas pela Microsoft. Além disso, Olá AuthGUID é específico para cada rede virtual e seu gateway. Significa que, se você quiser tooadd outra rede virtual do Azure, você precisa tooget AuthID outro para o circuito de rota expressa que se conecta HANA grandes instâncias no Azure. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Se você quiser tooconnect Olá gateway toomultiple circuitos ExpressRoute que estão associados a sua assinatura, talvez seja necessário tooexecute essa etapa mais de uma vez. Por exemplo, você provavelmente vai tooconnect Olá mesmo circuito de ExpressRoute de toohello de Gateway de rede virtual que se conecta a rede Olá tooyour de rede virtual no local.

## <a name="adding-more-ip-addresses-or-subnets"></a>Como adicionar mais endereços IP ou sub-redes

Use qualquer Olá portal do Azure, PowerShell ou CLI ao adicionar mais endereços IP ou sub-redes.

Nesse caso, recomendação de saudação é tooadd Olá novo endereço intervalo IP como novo intervalo toohello espaço de endereço de rede virtual em vez de gerar um novo intervalo agregado. Em ambos os casos, é necessário ter toosubmit esta alteração tooMicrosoft tooallow conectividade fora desse novas unidades IP endereço intervalo toohello instância grande HANA no seu cliente. Você pode abrir um suporte do Azure solicitação tooget Olá novo endereço de rede virtual espaço adicionado. Após receber a confirmação, realize Olá próximas etapas.

toocreate uma sub-rede adicional de saudação portal do Azure, consulte o artigo de saudação [criar uma rede virtual usando o portal do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), e toocreate do PowerShell, consulte [criar uma rede virtual usando o PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Como adicionar redes virtuais

Depois de conectar inicialmente um ou mais VNets do Azure, talvez você queira tooadd adicionais aqueles que acessar o SAP HANA no Azure (instâncias grandes). Primeiro, enviar uma solicitação de suporte do Azure, em que a solicitação incluir Olá informações específicas identificação Olá determinada implantação do Azure e Olá intervalo de espaço de endereços IP de saudação espaço de endereço de rede virtual do Azure. SAP HANA no gerenciamento de serviços do Azure fornece informações necessárias do hello necessário tooconnect Olá adicionais VNets e rota expressa. Para cada rede virtual, é necessário um toohello de tooconnect da chave de autorização exclusiva circuito de rota expressa tooHANA grandes instâncias.

Etapas tooadd uma nova rede virtual do Azure:

1. Concluir a primeira etapa Olá no processo de integração hello, consulte Olá _criar rede virtual do Azure_ seção.
2. Conclua a segunda etapa Olá no processo de integração de saudação, consulte Olá _criação de sub-rede de gateway_ seção.
3. tooconnect seu toohello adicional do VNets circuito de rota expressa de instância grande HANA, abra uma solicitação de suporte do Azure com informações em Olá nova rede virtual e solicite uma nova chave de autorização.
4. Depois de receber a notificação de que a autorização de saudação é concluída, use informações de autorização fornecida pela Microsoft Olá Olá toocomplete terceira etapa no processo de integração de saudação, consulte Olá _VNets vinculação_ seção.

## <a name="increasing-expressroute-circuit-bandwidth"></a>Como aumentar a largura de banda do circuito de ExpressRoute

Consulte com o SAP HANA no Gerenciamento de Serviços do Azure. Se você estiver tooincrease aconselhados Olá largura de banda Olá SAP HANA no circuito de rota expressa do Azure (instâncias grandes), crie uma solicitação de suporte do Azure. (Você pode solicitar um aumento para uma largura de banda do circuito único backup tooa máximo de 10 Gbps). Em seguida, receber notificação depois Olá operação for concluída; Nenhuma ação adicional necessária tooenable essa velocidade superior no Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Como adicionar um circuito de ExpressRoute adicional

Consulte SAP HANA no gerenciamento de serviços do Azure, se você está ciente de que um circuito de rota expressa adicional é necessária, fazer uma toocreate de solicitação de suporte do Azure, um novo circuito de rota expressa (e tooget autorização informações tooconnect tooit). espaço de endereço de saudação que vai ser usado em Olá que vnets deve ser definida antes de fazer a solicitação de hello, na ordem para o SAP HANA na autorização de tooprovide de gerenciamento de serviços do Azure.

Depois de circuito de saudação novo é criado e Olá SAP HANA na configuração de gerenciamento de serviços do Azure for concluída, você vai notificação tooreceive informações Olá necessárias tooproceed. Execute as etapas de saudação fornecidas acima para criar e conectar Olá novo VNet toothis adicional circuito. Você não é capaz de tooconnect VNets do Azure toothis adicional circuito se eles já conectado tooanother SAP HANA no circuito de rota expressa do Azure (instância grande) no hello mesma região do Azure.

## <a name="deleting-a-subnet"></a>Como excluir uma sub-rede

tooremove uma sub-rede de rede virtual, a saudação portal do Azure, PowerShell ou CLI pode ser usado. Caso o IP de Rede Virtual do Azure endereço intervalo/Azure Espaço de Endereço de rede virtual foi um intervalo agregado, não há nenhum acompanhamento para você com a Microsoft. Exceto que Olá VNet ainda estiver propagando espaço de endereço de rota do BGP que inclui a sub-rede Olá excluído. Se você definiu o endereço de IP de rede virtual do Azure Olá intervalo/Azure espaço de endereço de rede virtual como vários intervalos de endereços IP do qual foi atribuído tooyour excluído sub-rede, exclua que fora do seu espaço de endereço de rede virtual e subsequentemente informar SAP HANA no gerenciamento de serviços do Azure tooremove de saudação intervalos que HANA SAP no Azure (instâncias grandes) é permitido toocommunicate com.

Enquanto não há ainda é de processo de saudação para remover as sub-redes específica, dedicada Azure.com orientação sobre a remoção de sub-redes, Olá reverter do processo de saudação para adicioná-los. Consulte o artigo Olá [criar uma rede virtual usando o portal do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre a criação de sub-redes.

## <a name="deleting-a-vnet"></a>Como excluir uma rede virtual

Use o portal do Azure, de saudação do PowerShell ou CLI ao excluir uma rede virtual. SAP HANA no gerenciamento de serviços do Azure remove as autorizações existentes de Olá em Olá SAP HANA no circuito de ExpressRoute do Azure (instâncias grandes) e remova o endereço de IP de rede virtual do Azure Olá intervalo/Azure espaço de endereço de rede virtual para comunicação de saudação com HANA grandes instâncias.

Depois de saudação VNet foi removida, abra um espaço de endereço suporte do Azure solicitação tooprovide Olá IP toobe intervalo removido.

Enquanto não há ainda específica, dedicada Azure.com orientação sobre como remover VNets, processo de saudação para remover as VNets é Olá reverter do processo de saudação para adicioná-las, que é descrito acima. Consulte os artigos Olá [criar uma rede virtual usando o portal do Azure de saudação](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [criar uma rede virtual usando o PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como criar VNets.

tooensure tudo o que for removido, excluir Olá itens a seguir:

- Olá conexão de rota expressa, Gateway de rede virtual, IP público do Gateway de rede virtual e rede virtual

## <a name="deleting-an-expressroute-circuit"></a>Como excluir um circuito de ExpressRoute

tooremove um SAP HANA adicionais no circuito de rota expressa do Azure (instâncias grandes), abra uma solicitação de suporte do Azure com o SAP HANA no gerenciamento de serviços do Azure e solicitar que o circuito Olá deve ser excluído. Dentro de Olá assinatura do Azure, você pode excluir ou manter Olá VNet conforme necessário. No entanto, você deve excluir a conexão de saudação entre hello circuito de rota expressa grande de instâncias HANA e Olá vinculado gateway de rede virtual.

Se você deseja tooremove uma rede virtual, siga as orientações de saudação sobre como excluir uma rede virtual na seção de saudação acima.


