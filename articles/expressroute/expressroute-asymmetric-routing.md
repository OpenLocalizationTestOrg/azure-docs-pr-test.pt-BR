---
title: roteamento de aaaAsymmetric | Microsoft Docs
description: "Este artigo orienta problemas Olá que um cliente poderá enfrentar com o roteamento assimétrico em uma rede que tem o destino de tooa vários links."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Roteamento assimétrico com vários caminhos de rede
Este artigo explica como o encaminhamento e o retorno do tráfego de rede podem adotar rotas diferentes quando há vários caminhos disponíveis entre a origem e o destino da rede.

É importante toounderstand dois conceitos toounderstand assimétrica de roteamento. Um é o efeito de saudação de vários caminhos de rede. Olá outros é como dispositivos, como um firewall, mantêm o estado. Esses tipos de dispositivos são chamados de dispositivos com estado. Uma combinação desses dois fatores cria cenários na rede à qual o tráfego é descartado por um dispositivo com monitoração de estado porque o dispositivo com monitoração de estado Olá não detecta que o tráfego originado com o próprio dispositivo hello.

## <a name="multiple-network-paths"></a>Vários caminhos de rede
Quando uma rede corporativa tem somente um toohello link Internet por meio de seu provedor de serviços de Internet, todos os tooand de tráfego de Internet de saudação viaja Olá mesmo caminho. Geralmente, as empresas compram vários circuitos, como caminhos redundantes, tempo de atividade tooimprove. Quando isso acontece, é possível que o tráfego que passa fora da rede hello, toohello Internet, passa por um link e hello retornar tráfego passa por um link diferente. Isso é conhecido como roteamento assimétrico. Roteamento assimétrico, inversa tráfego de rede tem um caminho diferente de fluxo de saudação original.

![Rede com vários caminhos](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Embora ele ocorre principalmente em Olá Internet, roteamento assimétrico também se aplica a tooother combinações de vários caminhos. Ele se aplica, por exemplo, caminho de Internet tooan e um caminho particular que vão toohello mesmo destino e caminhos toomultiple particulares vá toohello mesmo destino.

Cada roteador ao longo de forma hello, de origem toodestination, calcula tooreach de caminho melhor Olá um destino. Olá determinação do roteador do melhor caminho possíveis se baseia em dois fatores principais:

* O roteamento entre as redes externas é baseado em um protocolo de roteamento, BGP (Border Gateway Protocol). BGP usa anúncios de vizinhos e executa uma série de etapas toodetermine Olá melhor caminho toohello devem destino. Ele armazena o melhor caminho de saudação na sua tabela de roteamento.
* comprimento de saudação de uma máscara de sub-rede associada a uma rota influencia caminhos de roteamento. Se receber um roteador vários anúncios para Olá mesmo endereço IP, mas com as máscaras de sub-rede diferente, o roteador de saudação prefere anúncio Olá com uma máscara de sub-rede mais porque ele é considerado uma rota mais específica.

## <a name="stateful-devices"></a>Dispositivos com estado
Roteadores verificar Olá cabeçalho IP de um pacote para fins de roteamento. Alguns dispositivos pesquisar ainda mais dentro do pacote de saudação. Normalmente, esses dispositivos examinam os cabeçalhos da Camada4 (Protocolo de Controle de Transmissão - TCP; User Datagram Protocol - UDP) ou até mesmo da Camada7. Esses tipos de dispositivos são dispositivos de otimização da largura de banda ou dispositivos de segurança. 

O firewall é um exemplo comum de dispositivo com estado. Um firewall permite ou nega toopass um pacote por meio de suas interfaces com base em vários campos, como o protocolo, porta TCP/UDP e cabeçalhos de URL. Esse nível de inspeção de pacotes coloca uma pesada carga de processamento no dispositivo de saudação. desempenho tooimprove, firewall Olá inspeciona primeiro o pacote de um fluxo de saudação. Se ele permite Olá pacote tooproceed, ele mantém as informações de fluxo de saudação em sua tabela de estado. Todo o fluxo de pacotes subsequentes toothis relacionados são permitidas com base na determinação de saudação inicial. Um pacote que é parte de um fluxo existente pode chegar ao firewall hello. Se firewall Olá nenhuma informação de estado anterior sobre ele firewall Olá descarta o pacote de saudação.

## <a name="asymmetric-routing-with-expressroute"></a>Roteamento assimétrico com o ExpressRoute
Quando você conectar tooMicrosoft por meio de rota expressa do Azure, as alterações de rede assim:

* Você tem várias tooMicrosoft de links. Um link é sua conexão de Internet existente e outra Olá é por meio de rota expressa. Alguns tooMicrosoft de tráfego pode percorrer Olá Internet mas voltar por meio de rota expressa, ou vice-versa.
* Você recebe endereços IP mais específicos por meio do ExpressRoute. Portanto, para o tráfego do seu tooMicrosoft de rede para serviços oferecidos por meio de rota expressa, roteadores sempre preferem rota expressa.

efeito de saudação toounderstand tem destas duas alterações em uma rede, vamos considerar alguns cenários. Por exemplo, você tem apenas um circuito toohello Internet e consumir todos os serviços da Microsoft por meio de saudação à Internet. tráfego de saudação do seu percorrerá tooMicrosoft e de volta de rede Olá mesmo link da Internet e passa pelo firewall hello. registros de firewall Olá Olá fluxo, ele vê o primeiro pacote de saudação e retornará pacotes são permitidas porque fluxo Olá existe na tabela de estado de saudação.

![Roteamento assimétrico com o ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

Então, você ativa o ExpressRoute e consome os serviços oferecidos pela Microsoft por meio do ExpressRoute. Todos os outros serviços da Microsoft são consumidos pela Olá da Internet. Você pode implantar um firewall separadas na sua borda que está conectada tooExpressRoute. Microsoft anuncia a rede de tooyour de prefixos mais específica sobre a rota expressa para serviços específicos. Sua infraestrutura de roteamento escolhe a rota expressa como caminho de saudação preferencial para os prefixos. Se você não é publicidade seu tooMicrosoft de endereços IP público por meio do ExpressRoute, a Microsoft se comunica com seus endereços IP públicos por meio de saudação da Internet. Encaminhar o tráfego de sua rede tooMicrosoft usa a rota expressa e tráfego inverso da Microsoft usa Olá da Internet. Quando o firewall Olá na borda Olá vê um pacote de resposta para um fluxo que não for encontrada na tabela de estado hello, descarta o tráfego de retorno hello.

Se você escolher Olá toouse mesmo conversão de endereços de rede (NAT) do pool do ExpressRoute e de saudação da Internet, você verá problemas semelhantes com clientes de saudação em sua rede em endereços IP privados. Solicitações de serviços como o Windows Update vão via Olá Internet porque os endereços IP para esses serviços não são anunciados por meio de rota expressa. No entanto, o tráfego de retorno Olá volta por meio de rota expressa. Se um endereço IP com a Microsoft recebe Olá a mesma máscara de sub-rede de saudação à Internet e rota expressa, ela prefere rota expressa a saudação da Internet. Se um firewall ou outro dispositivo com monitoração de estado que está em sua borda da rede e voltados para a rota expressa não possui anteriores informações sobre o fluxo de hello, descarta os pacotes de saudação que pertencem a toothat fluxo.

## <a name="asymmetric-routing-solutions"></a>Soluções do roteamento assimétrico
Você tem duas opções principais toosolve Olá problema de roteamento assimétrico. Uma é por meio de roteamento e outros Olá é usando NAT na origem (SNAT).

### <a name="routing"></a>Roteamento
Certifique-se de que os endereços IP públicos são links de rede de (longa distância WAN) de longa distância tooappropriate anunciado. Por exemplo, se você quiser toouse Olá da Internet para o tráfego de autenticação e rota expressa para o tráfego de email, não deve anunciar seus endereços IP públicos de serviços de Federação do Active Directory (AD FS) por meio do ExpressRoute. Da mesma forma, certifique-se não tooexpose um local endereços de tooIP do servidor do AD FS Olá roteador recebe pela rota expressa. Rotas recebidas pela rota expressa são mais específicas para que eles demarcador de rota expressa Olá preferencial para tooMicrosoft de tráfego de autenticação. Isso causa o roteamento assimétrico.

Se você quiser toouse rota expressa para autenticação, certifique-se de que está anunciando os endereços IP públicos do AD FS através do ExpressRoute sem NAT. Dessa forma, o tráfego originado da Microsoft e vai tooan local do servidor AD FS enviados pela rota expressa. Tráfego de retorno do cliente tooMicrosoft usa rota expressa porque é rota preferencial Olá em Olá da Internet.

### <a name="source-based-nat"></a>NAT com base em origem
Outra maneira de solucionar os problemas do roteamento assimétrico é usando a SNAT. Por exemplo, você não tenha anunciado endereço IP público de saudação de um servidor de SMTP Simple Mail Transfer Protocol () no local por meio do ExpressRoute porque você pretende toouse Olá esse tipo de comunicação na Internet. Uma solicitação que se origina com a Microsoft e, em seguida, vai tooyour local do servidor SMTP atravessa Olá da Internet. Você SNAT Olá entrada solicitação tooan endereço IP interno. Tráfego reverso do servidor de SMTP Olá vai toohello firewall de borda (que você usa para NAT) em vez de por meio de rota expressa. o tráfego de retorno Olá volta por meio de saudação à Internet.

![Configuração de rede da NAT com base na origem](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Detecção de roteamento assimétrico
Rastreamento de rotas é Olá melhor maneira toomake-se de que o tráfego de rede está atravessando o caminho de saudação esperado. Se você espera que o tráfego do seu caminho de Internet local SMTP server tooMicrosoft tootake hello, Olá esperado é de rastreamento de rotas de saudação SMTP server tooOffice 365. resultado de saudação valida que o tráfego é realmente saiam da sua rede para saudação da Internet e não para a rota expressa.

