---
title: "inspeção aaaPacket com observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como toouse observador de rede tooperform profunda inspeção de pacotes coletados de uma VM"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Inspeção de pacotes com o Observador de Rede do Azure

Usando o recurso de captura de pacote de saudação do observador de rede, você pode iniciar e gerenciar sessões de captura em suas VMs do Azure no portal de hello, PowerShell, CLI e programaticamente por meio de saudação SDK e a API REST. Captura de pacote permite que você tooaddress cenários que exigem dados de nível de pacote, fornecendo informações de saudação em um formato utilizável prontamente. Aproveitar os dados de saudação tooinspect ferramentas disponíveis gratuitamente, você pode examinar as comunicações enviadas tooand de suas VMs e obter ideias sobre o tráfego de rede. Alguns usos de exemplo dos dados de captura de pacotes incluem: investigar problemas de rede ou do aplicativo, detectar tentativas de invasão e uso indevido da rede ou manter a conformidade normativa. Neste artigo, mostramos como tooopen um arquivo de captura de pacote fornecidos pelo observador de rede usando uma ferramenta de software livre populares. Também Forneceremos exemplos que mostram como toocalculate uma latência de conexão, identificar o tráfego anormal e examinar estatísticas de rede.

## <a name="before-you-begin"></a>Antes de começar

Este artigo percorre alguns cenários pré-configurados em uma captura de pacotes executada anteriormente. Esses cenários ilustram recursos que podem ser acessados examinando uma captura de pacotes. Esse cenário usa [WireShark](https://www.wireshark.org/) tooinspect captura de pacote de saudação.

Ele pressupõe que você já executou uma captura de pacotes em uma máquina virtual. toolearn como toocreate uma captura de pacote visite [captura de pacote de gerenciamento com o portal de saudação](network-watcher-packet-capture-manage-portal.md) ou com REST visitando [capturas de pacotes de gerenciamento com a API REST](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Cenário

Nesse cenário, você irá:

* examinar uma captura de pacotes

## <a name="calculate-network-latency"></a>calcular a latência da rede

Nesse cenário, mostramos como tooview Olá tempo de ida e volta inicial (RTT) de uma conversa de protocolo de controle de transmissão (TCP) que ocorrem entre dois pontos de extremidade.

Quando é estabelecida uma conexão TCP, hello três primeiros pacotes enviados na conexão Olá siga uma padrão conhecido tooas Olá três vias. Examinando pacotes de duas primeiras Olá enviados nesse handshake, uma solicitação inicial do cliente hello e uma resposta do servidor de saudação, podemos calcular latência hello quando essa conexão foi estabelecida. Essa latência seja chamado tooas Olá tempo de ida e volta (RTT). Para obter mais informações sobre o protocolo TCP hello e handshake de três vias Olá consulte toohello recursos a seguir. https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip

### <a name="step-1"></a>Etapa 1

Iniciar o WireShark

### <a name="step-2"></a>Etapa 2

Saudação de carga **. cap** arquivo do pacote de captura. Esse arquivo pode ser encontrado no blob Olá que foi salvo em nosso localmente na máquina virtual Olá dependendo de como você configurou.

### <a name="step-3"></a>Etapa 3

tooview Olá tempo de ida e volta inicial (RTT) em conversas do TCP, nós só verá Olá primeiro dois pacotes envolvidos no handshake TCP hello. Vamos usar Olá primeiro dois pacotes no handshake de três vias hello, que são Olá [SYN], [SYN, ACK] pacotes. Eles são chamados de sinalizadores definidos no cabeçalho TCP hello. último pacote Hello no handshake hello, pacote de saudação [ACK], não será usado neste cenário. Olá [SYN] pacote é enviado pelo cliente hello. Após ele ser recebido o servidor de saudação envia o pacote de saudação [ACK] como uma confirmação de recebimento Olá SYN de cliente de saudação. Aproveitar os fatos Olá resposta do servidor de saudação requer muito pouca sobrecarga, calculamos Olá RTT subtraindo o pacote de saudação [SYN, ACK] foi recebido pelo cliente Olá pelo pacote de tempo [SYN] saudação de tempo de saudação foi enviada pelo cliente de saudação.

Usando o WireShark, esse valor é calculado.

toomore exibir facilmente os primeiros dois pacotes de saudação no handshake de três vias TCP hello, utilizaremos Olá filtragem de recurso fornecido pelo WireShark.

filtro de saudação tooapply em WireShark, expanda hello "Transmission Control Protocol" segmento de um pacote de [SYN] em sua captura e examine sinalizadores Olá definidas no cabeçalho TCP hello.

Já que estamos procurando toofilter em todos os [SYN] e [SYN, ACK] pacotes em sinalizadores cofirm que bit de Syn Olá é definido too1, o botão direito do mouse em bits de Syn Olá -> Aplicar como filtro -> selecionados.

![figura 7][7]

### <a name="step-4"></a>Etapa 4

Agora que você filtrou os pacotes do hello janela tooonly consulte com hello [SYN] o conjunto de bits, você pode facilmente selecionar conversas que lhe interessam tooview Olá RTT inicial. Saudação de tooview uma maneira simples RTT em WireShark simplesmente clique suspensa Olá marcada analysis "SEQ/ACK". Você verá Olá que RTT exibido. Nesse caso, Olá RTT foi 0.0022114 segundos ou 2.211 ms.

![figura 8][8]

## <a name="unwanted-protocols"></a>Protocolos indesejados

Você pode ter vários aplicativos em execução em uma instância de máquina virtual implantada no Azure. Muitos desses aplicativos se comunicam pela rede hello, talvez sem sua permissão explícita. Usando a comunicação de rede de toostore de captura de pacote, poderemos investigar como o aplicativo se comunicando na rede hello e procurar por quaisquer problemas.

Neste exemplo, examinaremos uma captura de pacotes executada antes para os protocolos indesejados que possa indicar a comunicação não autorizada de um aplicativo em execução em seu computador.

### <a name="step-1"></a>Etapa 1

Usando Olá captura mesmo no hello anterior cenário, clique em **estatísticas** > **hierarquia de protocolo**

![menu da hierarquia de protocolos][2]

janela de hierarquia de protocolo Hello é exibida. Essa exibição fornece uma lista de todos os protocolos de saudação que estavam em uso durante a sessão de captura hello e número de saudação de pacotes transmitidas e recebidas usando protocolos de saudação. Essa exibição pode ser útil para localizar o tráfego de rede indesejado em suas máquinas virtuais ou rede.

![hierarquia de protocolos aberta][3]

Como você pode ver no hello captura de tela a seguir, houve tráfego usando o protocolo de BitTorrent hello, que é usado para o compartilhamento de arquivos toopeer ponto a ponto. Como um administrador você não espera toosee BitTorrent tráfego neste determinado as máquinas virtuais. Agora você sabe desse tráfego, remover Olá par toopeer software instalada nesta máquina virtual ou saudação do bloco usando um Firewall ou grupos de segurança de rede de tráfego. Além disso, você pode optar por toorun captura de pacote em um agendamento, portanto você pode examinar o uso do protocolo de saudação em suas máquinas virtuais regularmente. Para obter um exemplo sobre como as tarefas de rede tooautomate no azure visite [monitorar os recursos de rede com a automação do azure](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Localizando os principais destinos e portas

Noções básicas sobre tipos de saudação do tráfego, Olá pontos de extremidade e portas Olá comunicadas sobre é um importante ao monitorar ou solução de problemas de aplicativos e recursos em sua rede. Utilizando um arquivo de captura de pacote acima, pode rapidamente aprendemos Olá principais destinos nosso VM está se comunicando e Olá portas estão sendo utilizadas.

### <a name="step-1"></a>Etapa 1

Usando Olá captura mesmo no hello anterior cenário, clique em **estatísticas** > **estatísticas IPv4** > **destinos e portas**

![janela de captura de pacotes][4]

### <a name="step-2"></a>Etapa 2

Como examinarmos resultados Olá se destaque em uma linha, havia várias conexões na porta 111. porta Hello mais usada foi 3389, que é a área de trabalho remota e Olá restantes são portas dinâmicas de RPC.

Embora esse tráfego pode significar nada, é uma porta que foi usada para muitas conexões e é administrador toohello desconhecido.

![figura 5][5]

### <a name="step-3"></a>Etapa 3

Agora que determinamos fora de porta local que é possível filtrar nossos captura com base na porta hello.

filtro de saudação neste cenário seria:

```
tcp.port == 111
```

Podemos inserir texto de filtro Olá acima na caixa de texto de filtro hello e pressione enter.

![figura 6][6]

Resultados de hello, podemos ver todo o tráfego de saudação é proveniente de uma máquina virtual local em Olá mesma sub-rede. Se ainda não entendemos por que esse tráfego está ocorrendo, é mais pode inspecionar Olá pacotes toodetermine por que ele é fazer essas chamadas na porta 111. Com essas informações, poderá agir Olá apropriado.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre Olá outros recursos de diagnósticos do observador de rede visitando [visão geral do monitoramento de rede do Azure](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













