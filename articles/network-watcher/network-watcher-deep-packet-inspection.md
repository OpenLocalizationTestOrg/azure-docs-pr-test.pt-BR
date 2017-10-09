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
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="304d9-103">Inspeção de pacotes com o Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="304d9-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="304d9-104">Usando o recurso de captura de pacote de saudação do observador de rede, você pode iniciar e gerenciar sessões de captura em suas VMs do Azure no portal de hello, PowerShell, CLI e programaticamente por meio de saudação SDK e a API REST.</span><span class="sxs-lookup"><span data-stu-id="304d9-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="304d9-105">Captura de pacote permite que você tooaddress cenários que exigem dados de nível de pacote, fornecendo informações de saudação em um formato utilizável prontamente.</span><span class="sxs-lookup"><span data-stu-id="304d9-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="304d9-106">Aproveitar os dados de saudação tooinspect ferramentas disponíveis gratuitamente, você pode examinar as comunicações enviadas tooand de suas VMs e obter ideias sobre o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="304d9-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="304d9-107">Alguns usos de exemplo dos dados de captura de pacotes incluem: investigar problemas de rede ou do aplicativo, detectar tentativas de invasão e uso indevido da rede ou manter a conformidade normativa.</span><span class="sxs-lookup"><span data-stu-id="304d9-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="304d9-108">Neste artigo, mostramos como tooopen um arquivo de captura de pacote fornecidos pelo observador de rede usando uma ferramenta de software livre populares.</span><span class="sxs-lookup"><span data-stu-id="304d9-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="304d9-109">Também Forneceremos exemplos que mostram como toocalculate uma latência de conexão, identificar o tráfego anormal e examinar estatísticas de rede.</span><span class="sxs-lookup"><span data-stu-id="304d9-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="304d9-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="304d9-110">Before you begin</span></span>

<span data-ttu-id="304d9-111">Este artigo percorre alguns cenários pré-configurados em uma captura de pacotes executada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="304d9-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="304d9-112">Esses cenários ilustram recursos que podem ser acessados examinando uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="304d9-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="304d9-113">Esse cenário usa [WireShark](https://www.wireshark.org/) tooinspect captura de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="304d9-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="304d9-114">Ele pressupõe que você já executou uma captura de pacotes em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="304d9-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="304d9-115">toolearn como toocreate uma captura de pacote visite [captura de pacote de gerenciamento com o portal de saudação](network-watcher-packet-capture-manage-portal.md) ou com REST visitando [capturas de pacotes de gerenciamento com a API REST](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="304d9-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="304d9-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="304d9-116">Scenario</span></span>

<span data-ttu-id="304d9-117">Nesse cenário, você irá:</span><span class="sxs-lookup"><span data-stu-id="304d9-117">In this scenario, you:</span></span>

* <span data-ttu-id="304d9-118">examinar uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="304d9-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="304d9-119">calcular a latência da rede</span><span class="sxs-lookup"><span data-stu-id="304d9-119">Calculate network latency</span></span>

<span data-ttu-id="304d9-120">Nesse cenário, mostramos como tooview Olá tempo de ida e volta inicial (RTT) de uma conversa de protocolo de controle de transmissão (TCP) que ocorrem entre dois pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="304d9-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="304d9-121">Quando é estabelecida uma conexão TCP, hello três primeiros pacotes enviados na conexão Olá siga uma padrão conhecido tooas Olá três vias.</span><span class="sxs-lookup"><span data-stu-id="304d9-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="304d9-122">Examinando pacotes de duas primeiras Olá enviados nesse handshake, uma solicitação inicial do cliente hello e uma resposta do servidor de saudação, podemos calcular latência hello quando essa conexão foi estabelecida.</span><span class="sxs-lookup"><span data-stu-id="304d9-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="304d9-123">Essa latência seja chamado tooas Olá tempo de ida e volta (RTT).</span><span class="sxs-lookup"><span data-stu-id="304d9-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="304d9-124">Para obter mais informações sobre o protocolo TCP hello e handshake de três vias Olá consulte toohello recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="304d9-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="304d9-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="304d9-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-126">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="304d9-126">Step 1</span></span>

<span data-ttu-id="304d9-127">Iniciar o WireShark</span><span class="sxs-lookup"><span data-stu-id="304d9-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="304d9-128">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="304d9-128">Step 2</span></span>

<span data-ttu-id="304d9-129">Saudação de carga **. cap** arquivo do pacote de captura.</span><span class="sxs-lookup"><span data-stu-id="304d9-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="304d9-130">Esse arquivo pode ser encontrado no blob Olá que foi salvo em nosso localmente na máquina virtual Olá dependendo de como você configurou.</span><span class="sxs-lookup"><span data-stu-id="304d9-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="304d9-131">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="304d9-131">Step 3</span></span>

<span data-ttu-id="304d9-132">tooview Olá tempo de ida e volta inicial (RTT) em conversas do TCP, nós só verá Olá primeiro dois pacotes envolvidos no handshake TCP hello.</span><span class="sxs-lookup"><span data-stu-id="304d9-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="304d9-133">Vamos usar Olá primeiro dois pacotes no handshake de três vias hello, que são Olá [SYN], [SYN, ACK] pacotes.</span><span class="sxs-lookup"><span data-stu-id="304d9-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="304d9-134">Eles são chamados de sinalizadores definidos no cabeçalho TCP hello.</span><span class="sxs-lookup"><span data-stu-id="304d9-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="304d9-135">último pacote Hello no handshake hello, pacote de saudação [ACK], não será usado neste cenário.</span><span class="sxs-lookup"><span data-stu-id="304d9-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="304d9-136">Olá [SYN] pacote é enviado pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="304d9-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="304d9-137">Após ele ser recebido o servidor de saudação envia o pacote de saudação [ACK] como uma confirmação de recebimento Olá SYN de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="304d9-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="304d9-138">Aproveitar os fatos Olá resposta do servidor de saudação requer muito pouca sobrecarga, calculamos Olá RTT subtraindo o pacote de saudação [SYN, ACK] foi recebido pelo cliente Olá pelo pacote de tempo [SYN] saudação de tempo de saudação foi enviada pelo cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="304d9-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="304d9-139">Usando o WireShark, esse valor é calculado.</span><span class="sxs-lookup"><span data-stu-id="304d9-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="304d9-140">toomore exibir facilmente os primeiros dois pacotes de saudação no handshake de três vias TCP hello, utilizaremos Olá filtragem de recurso fornecido pelo WireShark.</span><span class="sxs-lookup"><span data-stu-id="304d9-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="304d9-141">filtro de saudação tooapply em WireShark, expanda hello "Transmission Control Protocol" segmento de um pacote de [SYN] em sua captura e examine sinalizadores Olá definidas no cabeçalho TCP hello.</span><span class="sxs-lookup"><span data-stu-id="304d9-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="304d9-142">Já que estamos procurando toofilter em todos os [SYN] e [SYN, ACK] pacotes em sinalizadores cofirm que bit de Syn Olá é definido too1, o botão direito do mouse em bits de Syn Olá -> Aplicar como filtro -> selecionados.</span><span class="sxs-lookup"><span data-stu-id="304d9-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![figura 7][7]

### <a name="step-4"></a><span data-ttu-id="304d9-144">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="304d9-144">Step 4</span></span>

<span data-ttu-id="304d9-145">Agora que você filtrou os pacotes do hello janela tooonly consulte com hello [SYN] o conjunto de bits, você pode facilmente selecionar conversas que lhe interessam tooview Olá RTT inicial.</span><span class="sxs-lookup"><span data-stu-id="304d9-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="304d9-146">Saudação de tooview uma maneira simples RTT em WireShark simplesmente clique suspensa Olá marcada analysis "SEQ/ACK".</span><span class="sxs-lookup"><span data-stu-id="304d9-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="304d9-147">Você verá Olá que RTT exibido.</span><span class="sxs-lookup"><span data-stu-id="304d9-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="304d9-148">Nesse caso, Olá RTT foi 0.0022114 segundos ou 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="304d9-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![figura 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="304d9-150">Protocolos indesejados</span><span class="sxs-lookup"><span data-stu-id="304d9-150">Unwanted protocols</span></span>

<span data-ttu-id="304d9-151">Você pode ter vários aplicativos em execução em uma instância de máquina virtual implantada no Azure.</span><span class="sxs-lookup"><span data-stu-id="304d9-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="304d9-152">Muitos desses aplicativos se comunicam pela rede hello, talvez sem sua permissão explícita.</span><span class="sxs-lookup"><span data-stu-id="304d9-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="304d9-153">Usando a comunicação de rede de toostore de captura de pacote, poderemos investigar como o aplicativo se comunicando na rede hello e procurar por quaisquer problemas.</span><span class="sxs-lookup"><span data-stu-id="304d9-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="304d9-154">Neste exemplo, examinaremos uma captura de pacotes executada antes para os protocolos indesejados que possa indicar a comunicação não autorizada de um aplicativo em execução em seu computador.</span><span class="sxs-lookup"><span data-stu-id="304d9-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-155">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="304d9-155">Step 1</span></span>

<span data-ttu-id="304d9-156">Usando Olá captura mesmo no hello anterior cenário, clique em **estatísticas** > **hierarquia de protocolo**</span><span class="sxs-lookup"><span data-stu-id="304d9-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![menu da hierarquia de protocolos][2]

<span data-ttu-id="304d9-158">janela de hierarquia de protocolo Hello é exibida.</span><span class="sxs-lookup"><span data-stu-id="304d9-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="304d9-159">Essa exibição fornece uma lista de todos os protocolos de saudação que estavam em uso durante a sessão de captura hello e número de saudação de pacotes transmitidas e recebidas usando protocolos de saudação.</span><span class="sxs-lookup"><span data-stu-id="304d9-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="304d9-160">Essa exibição pode ser útil para localizar o tráfego de rede indesejado em suas máquinas virtuais ou rede.</span><span class="sxs-lookup"><span data-stu-id="304d9-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![hierarquia de protocolos aberta][3]

<span data-ttu-id="304d9-162">Como você pode ver no hello captura de tela a seguir, houve tráfego usando o protocolo de BitTorrent hello, que é usado para o compartilhamento de arquivos toopeer ponto a ponto.</span><span class="sxs-lookup"><span data-stu-id="304d9-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="304d9-163">Como um administrador você não espera toosee BitTorrent tráfego neste determinado as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="304d9-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="304d9-164">Agora você sabe desse tráfego, remover Olá par toopeer software instalada nesta máquina virtual ou saudação do bloco usando um Firewall ou grupos de segurança de rede de tráfego.</span><span class="sxs-lookup"><span data-stu-id="304d9-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="304d9-165">Além disso, você pode optar por toorun captura de pacote em um agendamento, portanto você pode examinar o uso do protocolo de saudação em suas máquinas virtuais regularmente.</span><span class="sxs-lookup"><span data-stu-id="304d9-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="304d9-166">Para obter um exemplo sobre como as tarefas de rede tooautomate no azure visite [monitorar os recursos de rede com a automação do azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="304d9-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="304d9-167">Localizando os principais destinos e portas</span><span class="sxs-lookup"><span data-stu-id="304d9-167">Finding top destinations and ports</span></span>

<span data-ttu-id="304d9-168">Noções básicas sobre tipos de saudação do tráfego, Olá pontos de extremidade e portas Olá comunicadas sobre é um importante ao monitorar ou solução de problemas de aplicativos e recursos em sua rede.</span><span class="sxs-lookup"><span data-stu-id="304d9-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="304d9-169">Utilizando um arquivo de captura de pacote acima, pode rapidamente aprendemos Olá principais destinos nosso VM está se comunicando e Olá portas estão sendo utilizadas.</span><span class="sxs-lookup"><span data-stu-id="304d9-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-170">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="304d9-170">Step 1</span></span>

<span data-ttu-id="304d9-171">Usando Olá captura mesmo no hello anterior cenário, clique em **estatísticas** > **estatísticas IPv4** > **destinos e portas**</span><span class="sxs-lookup"><span data-stu-id="304d9-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![janela de captura de pacotes][4]

### <a name="step-2"></a><span data-ttu-id="304d9-173">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="304d9-173">Step 2</span></span>

<span data-ttu-id="304d9-174">Como examinarmos resultados Olá se destaque em uma linha, havia várias conexões na porta 111.</span><span class="sxs-lookup"><span data-stu-id="304d9-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="304d9-175">porta Hello mais usada foi 3389, que é a área de trabalho remota e Olá restantes são portas dinâmicas de RPC.</span><span class="sxs-lookup"><span data-stu-id="304d9-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="304d9-176">Embora esse tráfego pode significar nada, é uma porta que foi usada para muitas conexões e é administrador toohello desconhecido.</span><span class="sxs-lookup"><span data-stu-id="304d9-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![figura 5][5]

### <a name="step-3"></a><span data-ttu-id="304d9-178">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="304d9-178">Step 3</span></span>

<span data-ttu-id="304d9-179">Agora que determinamos fora de porta local que é possível filtrar nossos captura com base na porta hello.</span><span class="sxs-lookup"><span data-stu-id="304d9-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="304d9-180">filtro de saudação neste cenário seria:</span><span class="sxs-lookup"><span data-stu-id="304d9-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="304d9-181">Podemos inserir texto de filtro Olá acima na caixa de texto de filtro hello e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="304d9-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![figura 6][6]

<span data-ttu-id="304d9-183">Resultados de hello, podemos ver todo o tráfego de saudação é proveniente de uma máquina virtual local em Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="304d9-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="304d9-184">Se ainda não entendemos por que esse tráfego está ocorrendo, é mais pode inspecionar Olá pacotes toodetermine por que ele é fazer essas chamadas na porta 111.</span><span class="sxs-lookup"><span data-stu-id="304d9-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="304d9-185">Com essas informações, poderá agir Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="304d9-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="304d9-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="304d9-186">Next steps</span></span>

<span data-ttu-id="304d9-187">Saiba mais sobre Olá outros recursos de diagnósticos do observador de rede visitando [visão geral do monitoramento de rede do Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="304d9-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













