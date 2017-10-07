---
title: "aaaDMZ exemplo – crie uma rede de Perímetro tooProtect redes com um Firewall, UDR e NSG | Microsoft Docs"
description: "Criar uma rede de perímetro com um Firewall, o Roteamento Definido pelo Usuário (UDR) e os Grupos de Segurança de Rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Exemplo 3 – crie uma rede de Perímetro tooProtect redes com um Firewall, UDR e NSG
[Retornar toohello página segurança limite de melhores práticas][HOME]

Este exemplo criará uma rede de perímetro com um firewall, quatro servidores Windows, Roteamento Definido pelo Usuário, Reencaminhamento IP e Grupos de Segurança de Rede. Ele também guiará por cada Olá comandos relevantes tooprovide uma compreensão mais profunda de cada etapa. Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ. Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários. 

![DMZ bidirecional com NVA, NSG e UDR][1]

## <a name="environment-setup"></a>Configuração do ambiente
Neste exemplo, há uma assinatura que contém Olá seguinte:

* Três serviços de nuvem: “SecSvc001”, “FrontEnd001” e “BackEnd001”
* Uma rede virtual, “CorpNetwork”, com três sub-redes; “SecNet”, “FrontEnd” e “BackEnd”
* Um dispositivo virtual de rede, neste exemplo, um firewall, conectado toohello SecNet sub-rede
* Um Windows Server que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")
* Um servidor Windows que representa um servidor DNS ("DNS01")

Na seção de referências de saudação abaixo, há um script do PowerShell que criará a maior parte do ambiente Olá descrito acima. Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento.

ambiente de saudação toobuild:

1. Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)
2. Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)
3. Execute o script hello no PowerShell

**Observação**: região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.

Após a execução bem-sucedida do script hello Olá seguindo as etapas de pós-scripts pode ser tomada:

1. Configurar regras de firewall hello, isso é abordado em Olá seção intitulada: Descrição da regra de Firewall.
2. Opcionalmente, na seção de referências de saudação são dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.

Depois que o script hello for executado com êxito as regras de firewall Olá precisará toobe concluída, isso é abordado na seção de saudação: regras de Firewall.

## <a name="user-defined-routing-udr"></a>Roteamento definido pelo usuário (UDR)
Por padrão, a saudação rotas de sistema a seguir é definida como:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Olá VNETLocal é sempre Olá definido prefixos de endereço de saudação VNet para essa rede específico (ou seja ele será alterado de rede virtual tooVNet dependendo de como cada rede virtual específico é definida). Olá restante sistema rotas padrão acima e são estáticos.

Como prioridade, rotas são processadas por meio do método de correspondência de prefixo mais longo (LPM) hello, assim hello rota mais específica na tabela de saudação aplicaria tooa recebe o endereço de destino.

Portanto, o tráfego (por exemplo toohello DNS01 server, 10.0.2.4) destinado a rede local da saudação (10.0.0.0/16) será encaminhado entre o destino de tooits VNet Olá devido toohello 10.0.0.0/16 rota. Em outras palavras, para 10.0.2.4, rota de 10.0.0.0/16 Olá é rota mais específica de hello, embora 0.0.0.0/0 e Olá 10.0.0.0/8 também podem se aplicam, mas uma vez que são menos específicos, elas não afetam esse tráfego. Assim Olá tráfego too10.0.2.4 teria um próximo salto da Olá redes locais e simplesmente toohello destino de rota.

Se o tráfego foi planejado para 10.1.1.1, por exemplo, não se aplicam a rota de 10.0.0.0/16 hello, mas Olá 10.0.0.0/8 seria hello mais específico e esse tráfego Olá seria removido ("preto holed") como Olá próximo salto é Null. 

Se destino Olá não aplicou tooany de prefixos de Null hello ou prefixos de VNETLocal hello, ele seguirá Olá menos específico de rota 0.0.0.0/0 e ser roteada toohello Internet como salto seguinte hello e, portanto, fora da borda de internet do Azure.

Há dois prefixos idênticos na tabela de rotas hello, Olá é ordem de saudação de preferência com base no atributo de "origem" de rotas hello:

1. "VirtualAppliance" = uma tabela de rotas definidas pelo usuário toohello adicionados manualmente
2. "VPNGateway" = uma rota dinâmico (BGP quando usado com redes híbridas) adicionados por um protocolo de rede dinâmica, essas rotas podem ser alterados ao longo do tempo conforme o protocolo dinâmico Olá automaticamente reflete as alterações na rede emparelhada
3. "Default" = Olá sistema rotas, Olá entradas estáticas locais de rede virtual e hello, conforme mostrado na tabela de rotas Olá acima.

> [!NOTE]
> Agora você pode usar o roteamento definida pelo usuário (UDR) com Gateways de VPN e rota expressa tooforce saída e o dispositivo virtual de rede roteado tooa da toobe (NVA) de tráfego de entrada entre locais.
> 
> 

#### <a name="creating-hello-local-routes"></a>Criando Olá rotas locais
Neste exemplo, duas tabelas de roteamento são necessários, um para as sub-redes de front-end e back-end de saudação. Cada tabela é carregada com rotas estáticas apropriadas para Olá recebe sub-rede. Para finalidade Olá neste exemplo, cada tabela tem três rotas:

1. Tráfego de sub-rede local sem próximo salto definido tooallow sub-rede local tráfego toobypass Olá firewall
2. Tráfego de rede virtual com um próximo nó definido como firewall, isso substituições de regra padrão Olá que permite tooroute de tráfego de rede virtual local diretamente
3. Tráfego de todos os demais (0/0) com um próximo nó definido como Olá firewall

Após a criação de tabelas de roteamento de saudação são sub-redes tootheir associado. Olá front-end subrede tabela de roteamento, tendo criado e vinculado toohello sub-rede deve ser assim:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


Neste exemplo, a seguir Olá comandos toobuild usado Olá a tabela de rota, adicione uma rota definida pelo usuário e, em seguida, associar a sub-rede de tooa de tabela de rota hello (Observação; todos os itens abaixo que começa com um sinal de cifrão (por exemplo: $BESubnet) são variáveis definidas pelo usuário do script hello em Olá referência seção deste documento):

1. Primeira Olá base tabela de roteamento deve ser criada. Este trecho de código mostra a criação de saudação de tabela de saudação para a sub-rede de back-end de saudação. No script hello, uma tabela correspondente também é criada para a sub-rede de front-end de saudação.
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Depois de criar a tabela de rotas hello, rotas definida de usuário específicas podem ser adicionadas. Neste trecho, todo o tráfego (0.0.0.0/0) será encaminhado através do dispositivo virtual de saudação (uma variável, $VMIP [0], é usado toopass Olá endereço de IP atribuído ao dispositivo virtual Olá foi criado anteriormente no script hello). No script hello, também é criada uma regra correspondente na tabela de front-end de saudação.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Olá acima rota de entrada substituirá hello "0.0.0.0/0" rota, mas 10.0.0.0/16 regra saudação padrão que ainda existente que permitiria que tráfego dentro de saudação VNet tooroute diretamente destino toohello e toohello dispositivo de rede Virtual. toocorrect que deve ser adicionada a esta regra de acompanhamento de saudação comportamento.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. Neste ponto, há um toobe da escolha feita. Com hello acima duas rotas todo o tráfego roteará firewall toohello para avaliação, até mesmo tráfego dentro de uma única sub-rede. Isso pode ser desejável, mas tooallow tráfego dentro de um tooroute sub-rede localmente sem o envolvimento do firewall Olá pode ser adicionada a uma regra de terceira, muito específica. Essa rota estados destine de qualquer endereço de sub-rede local Olá pode simplesmente existe rota diretamente (NextHopType = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Por fim, com hello tabela de roteamento criada e preenchida com um rotas definidas pelo usuário, tabela Olá agora deve ser sub-rede tooa associado. No script hello, tabela de rotas Olá front-end também é associada toohello sub-rede front-end. Aqui está o script de associação de saudação para a sub-rede de back-end de saudação.
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>encaminhamento IP
TooUDR um recurso complementar, é o encaminhamento IP. Isso é uma configuração em um dispositivo Virtual que permite o tráfego tooreceive não especificamente endereçado toohello dispositivo e, em seguida, encaminhá-los destino tráfego tooits ultimate.

Por exemplo, se o tráfego de AppVM01 faz uma solicitação toohello DNS01 ao servidor, UDR seria rotear esse firewall toohello. Com o encaminhamento IP habilitado, tráfego Olá para o destino de DNS01 hello (10.0.2.4) será aceita pelo dispositivo hello (10.0.0.4) e, em seguida, encaminhado destino final de tooits (10.0.2.4). Sem o encaminhamento IP ativado Olá Firewall, tráfego seria não aceito pelo dispositivo hello, embora a tabela de rotas Olá firewall hello como o próximo salto de saudação. 

> [!IMPORTANT]
> Ele é crítico tooremember tooenable encaminhamento IP em conjunto com o roteamento definida pelo usuário.
> 
> 

A configuração do Encaminhamento IP é um único comando e pode ser feito no momento da criação da VM. Para Olá fluxo este trecho de código do exemplo hello é final de saudação do script hello e agrupado com comandos UDR hello:

1. Chamar a instância de VM Olá que seu dispositivo virtual, Olá firewall nesse caso e habilitar o encaminhamento de IP (Observação; qualquer item em vermelho, começando com um sinal de cifrão (por exemplo: $VMName[0]) é uma variável definida pelo usuário do script hello na seção de referência Olá deste documento. Olá zero entre colchetes, [0], representa Olá primeira VM na matriz de saudação de VMs, para toowork de script de exemplo hello sem modificação, firewall de Olá Olá deve ser a primeira máquina virtual (VM 0)):
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Grupos de segurança de rede (NSG)
Neste exemplo, um grupo NSG é criado e então carregado com uma única regra. Esse grupo, em seguida, é associado somente toohello front-end e back-end sub-redes (não Olá SecNet). Declarativamente Olá regra a seguir está sendo compilado:

1. Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteiro (todas as sub-redes) foi negado

Embora NSGs sejam usados neste exemplo, seu principal objetivo será ser como uma segunda camada de defesa contra erros de configuração manual. Queremos tooblock todos os tráfego da saudação tooeither da internet Olá front-end ou sub-redes de back-end, o tráfego somente devem fluir através de Olá SecNet firewall de toohello de sub-rede (e, em seguida, se apropriado em toohello front-end ou back-end subredes). Além disso, com as regras UDR Olá em vigor, qualquer tráfego torná-lo em Olá front-end ou back-end subredes seria direcionado out toohello firewall (Obrigado tooUDR). firewall Olá veria isso como um fluxo assimétrico e ficaria o tráfego de saída hello. Assim, há três camadas de saudação de proteção de segurança front-end e back-end sub-redes; 1) sem pontos de extremidade abertos no hello FrontEnd001 e BackEnd001 serviços em nuvem, 2) NSGs negar o tráfego de Internet, firewall de 3) Olá soltar assimétrico tráfego de hello.

Um ponto interessante sobre Olá grupo de segurança de rede neste exemplo é que ele contém apenas uma regra, mostrada abaixo, que é toodeny internet tráfego toohello toda rede virtual que incluiria a sub-rede de segurança hello. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

No entanto, como Olá NSG só é ligado toohello front-end e back-end sub-redes, regra de saudação não é processada no tráfego de entrada toohello sub-rede de segurança. Como resultado, mesmo que a regra NSG Olá não diz nenhum endereço de tooany de tráfego de Internet Olá VNet, porque Olá que NSG nunca foi associado a sub-rede de segurança toohello, o tráfego fluirá toohello sub-rede de segurança.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Regras de firewall
No firewall hello, regras de encaminhamento precisará toobe criado. Desde que o firewall hello está bloqueando ou encaminhamento todas as entrada, saído e dentro do VNet tráfego muitas regras de firewall são necessárias. Além disso, todo o tráfego de entrada atingirá o endereço IP público de serviço de segurança hello (em portas diferentes), toobe processadas pelo firewall hello. Uma prática recomendada é fluxos de lógica de saudação toodiagram antes de configurar o retrabalho de tooavoid de regras de firewall e sub-redes de hello mais tarde. Olá figura a seguir é uma exibição lógica de regras de firewall Olá para este exemplo:

![Modo de exibição lógico de saudação regras de Firewall][2]

> [!NOTE]
> Com base em Olá que solução de virtualização de rede usada, as portas de gerenciamento Olá irão variar. Neste exemplo, um Firewall NextGen Barracuda é mencionado e usa as portas 22, 801 e 807. Consulte Olá appliance fornecedor documentação toofind Olá exata portas usadas para o gerenciamento de dispositivo hello está sendo usado.
> 
> 

### <a name="logical-rule-description"></a>Descrição da regra lógica
Olá lógico diagrama acima, sub-rede de segurança Olá não é mostrado como firewall Olá é único recurso Olá nessa sub-rede e este diagrama está mostrando as regras de firewall hello e como eles logicamente permitem ou negar fluxos de tráfego e não Olá roteados caminho real. Além disso, dois octetos do endereço IP local do Olá para facilitar a leitura mais fácil da última portas externas de saudação selecionadas para Olá tráfego RDP são portas intervalos superior (8014 – 8026) e foram selecionado toosomewhat alinhada hello (por exemplo, o endereço do servidor local 10.0.1.4 está associado porta externa 8014), no entanto, todas as portas mais alto não conflitante podem ser usadas.

Neste exemplo, precisamos de sete tipos de regras, descritos abaixo:

* Regras externas (para o tráfego de entrada):
  1. Regra de firewall de gerenciamento: Essa regra de redirecionamento do aplicativo permite que portas de gerenciamento do tráfego toopass toohello de solução de virtualização de rede hello.
  2. Regras de RDP (para cada servidor do windows): essas quatro regras (uma para cada servidor) serão permitir o gerenciamento de saudação servidores individuais via RDP. Isso também pode ser empacotado em uma regra dependendo recursos de saudação do hello solução de virtualização de rede que está sendo usado.
  3. Regras de tráfego do aplicativo: Há duas regras de tráfego do aplicativo, Olá primeiro para o tráfego de web de front-end hello e Olá segundo para o tráfego de back-end da saudação (por exemplo, servidor toodata camada da web). configuração de saudação dessas regras dependerá de arquitetura de rede de saudação (em que os servidores são colocados) e fluxos de tráfego (fluxos de tráfego que Olá direção e quais portas são usadas).
     * primeira regra de saudação permitirá que o servidor de aplicativos do hello aplicativo real tráfego tooreach hello. Enquanto hello outras regras permitirem segurança, gerenciamento, etc., regras de aplicativo são o que permite que tooaccess de usuários ou serviços externos Olá aplicativo (s). Neste exemplo, há um único servidor web na porta 80, assim, uma regra de firewall único de aplicativo redirecionará IP externo do tráfego de entrada toohello, toohello web interno endereço IP de servidores. Olá redirecionado sessão tráfego deve ser NAT tinha toohello interno do servidor.
     * Olá segunda regra de tráfego do aplicativo é Olá back-end regra tooallow Olá Web tootalk toohello AppVM01 servidor (mas não AppVM02) por meio de qualquer porta.
* Regras internas (para o tráfego interno da Rede Virtual)
  1. Regra de saída tooInternet: esta regra permitir o tráfego de qualquer rede toopass toohello selecionado redes. Geralmente, essa regra é uma regra padrão já está no firewall hello, mas em um estado desabilitado. Essa regra deve ser habilitada para esse exemplo.
  2. Regra DNS: Essa regra permite que somente o DNS (porta 53) tráfego toopass toohello servidor DNS. Para esse ambiente que maior parte do tráfego de front-end de saudação toohello back-end está bloqueada, esta regra especificamente permite DNS de qualquer sub-rede local.
  3. Subrede tooSubnet regra: essa regra é tooallow qualquer servidor na traseira Olá finalizar o servidor de tooany tooconnect sub-rede na sub-rede de front-end de saudação (mas não Olá inversa).
* Regra à prova de falhas (para o tráfego que não atendam a qualquer Olá acima):
  1. Negar todas as regras de tráfego: Isso deve ser sempre a regra final hello (em termos de prioridade) e como tal, se um tráfego passa falhará toomatch qualquer Olá anteriores serão removida por esta regra de regras. Essa é uma regra padrão e normalmente é ativada; geralmente, não é necessário fazer qualquer modificação.

> [!TIP]
> Na segunda regra de tráfego de aplicativo hello, qualquer porta é permitida para fácil deste exemplo, em uma saudação cenário real mais específicos intervalos de porta e endereço devem ser superfície de ataque de saudação tooreduce usada dessa regra.
> 
> 

<br />

> [!IMPORTANT]
> Depois que todos os Olá acima regras são criados, é importante tooreview prioridade de saudação do tráfego de tooensure cada regra será permitida ou negada conforme desejado. Neste exemplo, as regras de saudação são em ordem de prioridade. É fácil toobe bloqueada fora do firewall Olá ordenados toomis regras de conclusão. No mínimo, certifique-se de gerenciamento Olá firewall Olá em si é sempre absoluto regra de prioridade mais alta hello.
> 
> 

### <a name="rule-prerequisites"></a>Pré-requisitos de regra
Um pré-requisito para o firewall do Olá Olá Máquina Virtual em execução são pontos de extremidade públicos. Para o tráfego de tooprocess firewall Olá Olá pública pontos de extremidade apropriados devem ser abertos. Há três tipos de tráfego neste exemplo; 1) gerenciamento tráfego toocontrol Olá firewall e as regras de firewall, servidores com windows hello 2) RDP tráfego toocontrol e tráfego de aplicativo de 3). Esses são três colunas Olá dos tipos de tráfego em Olá superior metade da exibição lógica de regras de firewall Olá acima.

> [!IMPORTANT]
> Uma chave takeway aqui é tooremember que **todos os** tráfego virá através do firewall do hello. Caso toohello desktop tooremote IIS01 server, mesmo que seja no serviço de nuvem Front End de saudação e na sub-rede Front-End de hello, tooaccess neste servidor precisaremos tooRDP toohello firewall na porta 8014 e permitir a solicitação RDP Olá firewall tooroute Olá internamente toohello IIS01 a porta de RDP. saudação "Conectar" do portal do Azure botão não funcionará porque não há nenhum tooIIS01 de caminho direto RDP (quanto portal Olá pode ver). Isso significa que todas as conexões de saudação internet serão toohello serviço de segurança e uma porta, por exemplo, secscv001.cloudapp.net:xxxx (Olá referência acima diagrama para mapeamento de saudação de porta externa e IP interno e porta).
> 
> 

Um ponto de extremidade pode ser aberto no momento de saudação da criação de VM ou post compilação como é feito no script de exemplo hello e mostrado abaixo neste trecho de código (Observação; todos os itens que começam com um sinal de cifrão (por exemplo: $VMName[$i]) é uma variável definida pelo usuário do script Olá Olá referen seção CE deste documento. Olá "$i" entre colchetes, [$i] representa número de matriz de saudação de uma VM específica em uma matriz de máquinas virtuais):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Embora não claramente mostrado aqui devido toohello uso de variáveis, mas os pontos de extremidade são **somente** aberto em Olá segurança serviço de nuvem. Isso é que todo o tráfego é tratado de tooensure (roteadas, NAT tinha, descartado) por firewall hello.

Um cliente de gerenciamento será necessário toobe instalado em um firewall de saudação do PC toomanage e criar configurações de saudação necessárias. Consulte o fornecedor de documentação do seu firewall (ou outros NVA) Olá sobre como toomanage Olá dispositivo. restante Olá esta seção e a próxima seção hello, criação de regras de Firewall, descrevem configuração Olá do firewall Olá em si, por meio do cliente de gerenciamento de fornecedores hello (ou seja, não Olá portal do Azure ou o PowerShell).

Instruções para download do cliente e conexão toohello Barracuda usado neste exemplo podem ser encontradas aqui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Depois de conectado no firewall hello, mas antes de criar regras de firewall, há duas classes de objeto de pré-requisito que podem facilitar criando regras de saudação; Objetos de serviço e de rede.

Neste exemplo, três objetos de rede nomeada devem ser definido (um para Olá front-end subrede e sub-rede de back-end hello, também um objeto de rede para o endereço IP de saudação do servidor DNS Olá). toocreate uma rede nomeada. a partir do painel de cliente Barracuda NG Admin Olá, navegue toohello guia de configuração, no hello seção de configuração operacional Ruleset, em seguida, clique em "Redes" no menu de objetos de Firewall de saudação, clique novo no menu de editar redes Olá. objeto de rede Olá agora pode ser criado, adicionando o nome de saudação e um prefixo de saudação:

![Criar um objeto de rede de front-end][3]

Isso criará uma rede nomeada para a sub-rede de front-end hello, um objeto semelhante deve ser criado para a sub-rede de back-end Olá também. Agora sub-redes Olá podem ser mais facilmente referenciadas por nome nas regras de firewall de saudação.

Para Olá objeto do servidor DNS:

![Criar um objeto de servidor DNS][4]

Essa referência de endereço IP único será usada em uma regra DNS documento hello.

objetos de pré-requisito segundo Olá são objetos de serviços. Eles representarão portas de conexão de RDP Olá para cada servidor. Como o objeto de serviço RDP existente Olá é porta do RDP padrão toohello associada, 3389, novos serviços podem ser criados tooallow tráfego de portas externas de saudação (8014 8026). novas portas de saudação também podem ser adicionadas toohello serviço RDP existente, mas, para facilitar a demonstração, uma regra individual para cada servidor pode ser criada. toocreate uma nova regra RDP para um servidor. a partir do painel de cliente do hello Barracuda NG administrador, navegue toohello guia de configuração, no hello configuração operacional seção clique Ruleset, em seguida, clique em "Serviços" em Olá menu objetos de Firewall, role para baixo Olá lista de serviços e selecione Olá Serviço de "RDP". Com o botão direito do mouse e selecione copiar, então clique com botão direito do mouse e selecione Colar. Agora há um Objeto de Serviço RDP-Copy1 que pode ser editado. Com o botão direito Copy1 RDP e selecione Editar, Olá Editar objeto de serviço janela será exibida, conforme mostrado aqui:

![Cópia de regra RDP padrão][5]

valores Hello, em seguida, podem ser editado toorepresent Olá serviço RDP para um servidor específico. Para AppVM01 Olá acima padrão regra RDP deve ser modificado tooreflect um novo serviço de nome, descrição, e a porta externa do RDP usado em Olá diagrama Figura 8 (Observação: Olá portas são alterados saudação padrão RDP 3389 porta externa toohello que está sendo usado para isso um servidor específico, no caso de saudação de porta externa do AppVM01 Olá é 8025) hello serviço modificado é mostrado abaixo:

![Regra de AppVM01][6]

Esse processo deve ser repetido toocreate serviços de RDP para Olá restantes servidores; AppVM02, DNS01 e IIS01. criação de saudação desses serviços fará a criação da regra Olá mais simples e mais óbvio na próxima seção, Olá.

> [!NOTE]
> Um serviço RDP para Olá Firewall não é necessário por duas razões. 1) o primeiro firewall de saudação VM é uma imagem de baseadas em Linux para SSH seria usada na porta 22 para gerenciamento de VM em vez de RDP e 2) a porta 22 e duas portas de gerenciamento são permitidas na regra de gerenciamento primeiro Olá descrita abaixo tooallow para conectividade de gerenciamento.
> 
> 

### <a name="firewall-rules-creation"></a>Criação de regras de firewall
Há três tipos de regras de firewall usadas neste exemplo, todas elas têm ícones distintos:

uma regra de redirecionamento do aplicativo Hello: ![ícone de redirecionamento do aplicativo][7]

regra de NAT de destino Olá: ![ícone de NAT de destino][8]

regra de passagem Olá: ![passar ícone][9]

Obter mais informações sobre essas regras podem ser encontradas no site de Barracuda hello.

toocreate Olá regras a seguir (ou verifique se as regras padrão existente), a partir do painel de cliente Barracuda NG Admin hello, navegue toohello guia de configuração, no hello configuração operacional clique Ruleset. Chamado em uma grade, "Principal regras" mostrará Olá existente regras ativadas e desativadas esse firewall. No canto superior direito de saudação desta grade é uma pequena verde "+", clique neste toocreate uma nova regra (Observação: o firewall pode ser "bloqueado" para que as alterações, se você vir um botão marcado "Bloqueio" e são toocreate não é possível ou editar regras, clique neste botão muito "desbloquear" hello se regra t e permitir a edição). Se você quiser tooedit uma regra existente, selecione essa regra, clique com botão direito e selecione Editar regra.

Depois que as regras são criadas e/ou modificadas, eles devem ser enviados por push toohello firewall e, em seguida, ativado, se isso não for feito regra Olá alterações não entrarão em vigor. processo de envio e a ativação de saudação é descrito abaixo as descrições de regras de detalhes de saudação.

especificações de saudação de cada regra necessária toocomplete neste exemplo são descritas da seguinte maneira:

* **Gerenciamento de regra de firewall**: este aplicativo de redirecionamento regra permite o tráfego toopass toohello as portas de gerenciamento do dispositivo virtual do hello rede, neste exemplo, um Firewall de NextGen Barracuda. as portas de gerenciamento Olá são 801, 807 e, opcionalmente, 22. portas de saudação internos e externos são Olá mesmo (ou seja, nenhuma conversão de porta). Essa regra, SETUP-MGMT-ACCESS, é uma regra padrão e é habilitada por padrão (no Firewall NextGen Barracuda versão 6.1).
  
    ![Regra de gerenciamento de firewall][10]

> [!TIP]
> Olá espaço de endereço de origem nesta regra é qualquer, se hello intervalos de endereços IP de gerenciamento são conhecidos, reduzindo a este escopo também reduziria Olá portas de gerenciamento de toohello superfície de ataque.
> 
> 

* **Regras de RDP**: regras de NAT de destino esses serão permitir o gerenciamento de saudação servidores individuais via RDP.
  Há quatro toocreate de campos crítica necessário esta regra:
  
  1. Origem – tooallow RDP de qualquer lugar, referência hello "Qualquer" é usado no campo de origem hello.
  2. Serviço – usar Olá objeto apropriado de serviço criado anteriormente, neste caso "AppVM01 RDP", portas externas Olá redirecionam toohello endereço IP do local de servidores e tooport 3386 (porta RDP padrão Olá). Essa regra específica é para tooAppVM01 de acesso RDP.
  3. Destino – deve ser Olá *local porta no firewall Olá*, "IP Local do DHCP 1" ou eth0 se usando IPs estáticos. Olá um número ordinal (eth0, eth1, etc.) pode ser diferente se o dispositivo de rede tem várias interfaces de locais. Essa porta Olá é firewall Olá envia de (pode ser Olá mesmo como Olá porta de recebimento), Olá destino de roteados real é no campo de lista de destino hello.
  4. Redirecionamento – esta seção informa o dispositivo virtual Olá onde tooultimately redirecionar esse tráfego. redirecionamento mais simples de saudação é tooplace Olá IP e porta (opcional) no campo da lista de destino de saudação. Se nenhuma porta é a porta de destino de saudação usado na solicitação de entrada hello será usado (ie nenhuma tradução), se uma porta designada porta Olá também será NAT junto com IP hello tratar.
     
     ![Regra RDP do firewall][11]
     
     Um total de quatro regras RDP precisará toobe criado: 
     
     | Nome da Regra | Servidor | O Barramento de | Lista de destino |
     | --- | --- | --- | --- |
     | RDP-para-IIS01 |IIS01 |RDP de IIS01 |10.0.1.4:3389 |
     | RDP-para-DNS01 |DNS01 |RDP de DNS01 |10.0.2.4:3389 |
     | RDP-para-AppVM01 |AppVM01 |RDP de AppVM01 |10.0.2.5:3389 |
     | RDP-para-AppVM02 |AppVM02 |RDP de AppVm02 |10.0.2.6:3389 |

> [!TIP]
> Limitar escopo Olá Olá fonte e campos de serviço pode reduzir a superfície de ataque de saudação. escopo de Hello mais limitada que permitirá que a funcionalidade deve ser usado.
> 
> 

* **Regras de tráfego do aplicativo**: há duas regras de tráfego do aplicativo, Olá primeiro para o tráfego de web de front-end hello e Olá segundo para o tráfego de back-end da saudação (por exemplo, servidor toodata camada da web). Essas regras dependerá da arquitetura de rede de saudação (em que os servidores são colocados) e fluxos de tráfego (fluxos de tráfego que Olá direção e quais portas são usadas).
  
    Primeiro discutido é a regra de front-end de saudação para tráfego da web:
  
    ![Regra Web do firewall][12]
  
    Esta regra NAT de destino permite que o servidor de aplicativos do hello aplicativo real tráfego tooreach hello. Enquanto hello outras regras permitirem segurança, gerenciamento, etc., regras de aplicativo são o que permite que tooaccess de usuários ou serviços externos Olá aplicativo (s). Neste exemplo, há um único servidor web na porta 80, assim, Olá única aplicativo regra de firewall será redirecionado IP externo do tráfego de entrada toohello, toohello web interno endereço IP de servidores.
  
    **Observação**: que não há nenhuma porta atribuída no campo da lista de destino de saudação, assim, hello entrada porta 80 (ou 443 para Olá serviço selecionado) será usado no redirecionamento de saudação do servidor de web hello. Se o servidor de web hello está escutando em uma porta diferente, por exemplo, porta 8080; campo da lista de destino Olá pode ser tooallow too10.0.1.4:8080 atualizado para o redirecionamento de porta Olá também.
  
    Olá próxima regra de tráfego do aplicativo é Olá back-end regra tooallow Olá Web tootalk toohello AppVM01 servidor (mas não AppVM02) por meio de qualquer serviço:
  
    ![Regra da AppVM01 do firewall][13]
  
    Essa regra de passagem permite que qualquer servidor IIS em Olá front-end subrede tooreach Olá AppVM01 (endereço IP 10.0.2.5) em qualquer porta, usando os dados de tooaccess de protocolo exigidos pelo aplicativo da web hello.
  
    Esta captura de tela um "\<explícita dest\>" é usado em toosignify de campo de destino Olá 10.0.2.5 como destino de saudação. Isso pode ser chamada explícita conforme mostrado, ou um objeto de rede (como foi feito nos pré-requisitos Olá para o servidor DNS de saudação). Isso é administrador toohello do firewall hello como método toowhich será usado. tooadd 10.0.2.5 como um Explict Desitnation, clique duas vezes na primeira linha em branco Olá em \<explícita dest\> e insira o endereço de saudação na janela Olá pop-up.
  
    Com essa regra passar, nenhum NAT é necessária porque esse é o tráfego interno, portanto, Olá método de Conexão pode ser definido muito "Não SNAT".
  
    **Observação**: rede de origem Olá nesta regra é qualquer recurso na sub-rede de front-end hello, se haverá apenas um, ou um número específico conhecido dos servidores web, o recurso pode ser um objeto de rede criada toobe mais toothose exatos endereços IP específicos, em vez de Olá todo front-end subrede.

> [!TIP]
> Esta regra usa o serviço hello "Qualquer" toomake Olá toosetup mais fácil de aplicativo de exemplo e usar, também poderá ICMPv4 (ping) em uma única regra. No entanto, essa não é uma prática recomendada. Olá protocolos e portas e ("serviços") devem ser restrita toohello possível mínimo que permite a superfície de ataque do aplicativo operação tooreduce Olá entre esse limite.
> 
> 

<br />

> [!TIP]
> Embora essa regra mostra uma referência explícita dest que está sendo usada, uma abordagem consistente deve ser usada em toda a configuração do firewall hello. É recomendável que Olá objeto de rede denominado ser usadas em toda para facilitar a legibilidade e capacidade de suporte. Olá dest explícito é usado aqui tooshow de apenas um método alternativo de referência e geralmente não é recomendado (especialmente para configurações complexas).
> 
> 

* **Regra de saída tooInternet**: passar essa regra permitirá que o tráfego de redes de destino qualquer origem rede toopass toohello selecionado. Essa regra é uma regra padrão geralmente já firewall Barracuda NextGen de saudação, mas está em um estado desabilitado. Clicando duas vezes em que essa regra podem acessar o comando de ativar a regra de saudação. regra de saudação mostrada aqui foi modificado tooadd Olá duas sub-redes locais que foram criadas como referências na seção de pré-requisitos Olá este documento toohello do atributo de origem dessa regra.
  
    ![Regra de saída do firewall][14]
* **Regra de DNS**: passar essa regra permite que somente o DNS (porta 53) tráfego toopass toohello servidor DNS. Para esse ambiente que maior parte do tráfego de front-end de saudação toohello back-end está bloqueada, esta regra permite especificamente DNS.
  
    ![Regra DNS do firewall][15]
  
    **Observação**: nesta tela hello captura o método de Conexão está incluído. Como essa regra é para o tráfego de endereços IP do interno IP toointernal, nenhum NATing é necessária, este Olá método de Conexão está definido muito "Não SNAT" para esta regra de passagem.
* **Subrede tooSubnet regra**: passar essa regra é uma regra padrão que foi ativada e modificado tooallow qualquer servidor em volta Olá terminar server de tooany tooconnect sub-rede em Olá sub-rede front-end. Essa regra é o tráfego interno de todos os para que Olá método de Conexão pode ser definido como tooNo SNAT.
  
    ![Regra IntraVNet do firewall][16]
  
    **Observação**: Olá bidirecional de caixa de seleção não estiver marcada (nem é marcado na maioria das regras), isso é significativo para essa regra em que ele faz isso regra "única direção", que pode ser iniciada uma conexão de rede de front-end do toohello de sub-rede de back-end Olá, mas não Olá inversa. Se essa caixa de seleção tiver sido marcada, essa regra permitirá o tráfego bidirecional, o que não é desejável em nosso diagrama lógico.
* **Negar todas as regras de tráfego**: deve ser a regra final hello (em termos de prioridade) e como tal, se um tráfego que flui toomatch falhar qualquer Olá anterior regras será removido por essa regra. Essa é uma regra padrão e normalmente é ativada; geralmente, não é necessário fazer qualquer modificação. 
  
    ![Regra Negar do firewall][17]

> [!IMPORTANT]
> Depois que todos os Olá acima regras são criados, é importante tooreview prioridade de saudação do tráfego de tooensure cada regra será permitida ou negada conforme desejado. Neste exemplo, regras de saudação estão na ordem de saudação que devem ser exibidos no hello grade principal de regras em Olá Barracuda cliente de gerenciamento de encaminhamento.
> 
> 

## <a name="rule-activation"></a>Ativação da regra
Com a especificação de toohello Olá ruleset modificado de diagrama lógico de hello, Olá ruleset deve ser carregado toohello firewall e, em seguida, ativado.

![Ativação de regra de firewall][18]

No canto superior direito de saudação do cliente de gerenciamento de saudação são um cluster de botões. Olá "enviar alterações" botão toosend Olá modificado regras toohello firewall, clique botão de "Ativar" hello.

Com a ativação de saudação do conjunto de regras de firewall Olá esta compilação do ambiente de exemplo foi concluída.

## <a name="traffic-scenarios"></a>Cenários de tráfego
> [!IMPORTANT]
> Uma chave takeway é tooremember que **todos os** tráfego virá através do firewall do hello. Caso toohello desktop tooremote IIS01 server, mesmo que seja no serviço de nuvem Front End de saudação e na sub-rede Front-End de hello, tooaccess neste servidor precisaremos tooRDP toohello firewall na porta 8014 e permitir a solicitação RDP Olá firewall tooroute Olá internamente toohello IIS01 a porta de RDP. saudação "Conectar" do portal do Azure botão não funcionará porque não há nenhum tooIIS01 de caminho direto RDP (quanto portal Olá pode ver). Isso significa que todas as conexões de saudação internet serão toohello serviço de segurança e uma porta, por exemplo, secscv001.cloudapp.net:xxxx.
> 
> 

Para esses cenários, Olá seguindo as regras de firewall deve estar em vigor:

1. Gerenciamento do firewall
2. TooIIS01 RDP
3. TooDNS01 RDP
4. TooAppVM01 RDP
5. TooAppVM02 RDP
6. Toohello de tráfego de aplicativo Web
7. TooAppVM01 de tráfego do aplicativo
8. Saída toohello da Internet
9. TooDNS01 de front-end
10. Tráfego de dentro da sub-rede (end toofront back-end apenas)
11. Negar Tudo

conjunto de regras de firewall real Hello, provavelmente terão muitas outras regras toothese adição, regras de saudação em qualquer determinado firewall também terá números de prioridade diferentes Olá aqueles listados aqui. Esta lista e números associados são de relevância de tooprovide entre apenas essas onze regras e a prioridade relativa de saudação entre eles. Em outras palavras; no firewall do hello real, Olá "RDP tooIIS01" pode ser regra número 5, mas como está abaixo da regra de "Gerenciamento de Firewall" hello e acima de regra de "RDP tooDNS01" hello que ele seria alinhar com intenção de saudação desta lista. lista de saudação também ajudará a saudação abaixo cenários permitindo brevidade; Por exemplo "Regra de FW 9 (DNS)". Também por questão de brevidade, Olá quatro regras RDP será coletivamente chamado, "hello regras RDP" quando o cenário de tráfego de saudação é tooRDP não relacionado.

Lembre-se também de que os grupos de segurança de rede estão no local para o tráfego da internet em Olá front-end e back-end subredes.

#### <a name="allowed-internet-tooweb-server"></a>(Permitido) Internet tooWeb Server
1. O usuário da Internet solicita uma página HTTP de SecSvc001.CloudApp.Net (Internet Voltada para o Serviço de Nuvem)
2. Tráfego passa do serviço de nuvem por meio de um ponto de extremidade aberto na interface toofirewall porta 80 10.0.0.4:80
3. Nenhum NSG atribuído tooSecurity sub-rede, para que as regras do sistema NSG permitem tráfego toofirewall
4. Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)
5. O firewall inicia o processamento de regras:
   1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
   2. Regras 2 a 5 (regras de RDP) não se aplicam, mova a regra toonext
   3. FW regra 6 (aplicativo: Web) se aplicam, o tráfego é permitido, o firewall NAT-too10.0.1.4 (IIS01)
6. subrede front-end Olá começa o processamento de regras de entrada:
   1. NSG regra 1 (bloco de Internet) não se aplica (esse tráfego foi NAT seria pelo firewall hello, portanto, o endereço de origem de saudação agora é firewall Olá na sub-rede de segurança hello e vistos por sub-rede front-end de saudação o tráfego do NSG toobe "local" e, portanto, é permitido), mover toonext regra
   2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
7. IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação
8. Tentativas de IIS01 tooinitiates um tooAppVM01 de sessão FTP na sub-rede back-end
9. rota UDR Olá na sub-rede front-end torna o próximo salto do hello firewall Olá
10. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
11. O firewall inicia o processamento de regras:
    1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
    2. Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra
    3. 6 de regra FW (aplicativo: Web) não se aplicam, mova a regra toonext
    4. 7 de regra FW (aplicativo: back-end) se aplicam, o tráfego é permitido, firewall encaminha o tráfego too10.0.2.5 (AppVM01)
12. subrede back-end Olá começa o processamento de regras de entrada:
    1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
    2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
13. AppVM01 recebe a solicitação de saudação e inicia a sessão de saudação e responde
14. rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá
15. Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede de back-end é permitido
16. Porque isso está retornando o tráfego em uma sessão estabelecida Olá de firewall passa o servidor de web hello resposta toohello back (IIS01)
17. A sub-rede Frontend inicia o processamento da regra de entrada:
    1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
    2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
18. servidor do IIS Olá recebe a resposta hello, conclui a transação Olá com AppVM01 e conclui construção Olá resposta HTTP, essa resposta HTTP é enviada toohello solicitante
19. Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede front-end é permitido
20. Olá firewall de saudação de acertos de resposta HTTP e como isso é Olá resposta tooan estabelecida sessão NAT é aceito pelo firewall Olá
21. Olá firewall, em seguida, redireciona Olá resposta back toohello usuário pela Internet
22. Desde que não existem regras NSG saída ou saltos UDR na sub-rede de front-end Olá resposta Olá é permitida e Olá Internet usuário recebe Olá web página solicitada.

#### <a name="allowed-internet-rdp-toobackend"></a>(Permitido) TooBackend RDP de Internet
1. Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP via SecSvc001.CloudApp.Net:8025, onde o 8025 é o número da porta do hello atribuídos pelo usuário para a regra de firewall "RDP tooAppVM01" hello
2. serviço de nuvem Olá passa o tráfego por meio do ponto de extremidade aberto Olá na interface de toofirewall porta 8025 em 10.0.0.4:8025
3. Nenhum NSG atribuído tooSecurity sub-rede, para que as regras do sistema NSG permitem tráfego toofirewall
4. O firewall inicia o processamento de regras:
   1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
   2. FW regra 2 (RDP IIS) não se aplica, mover toonext regra
   3. FW regra 3 (DNS01 RDP) não se aplica, mover toonext regra
   4. Aplicar FW regra 4 (RDP AppVM01), o tráfego é permitido, o firewall NAT-too10.0.2.5:3386 (porta RDP em AppVM01)
5. subrede back-end Olá começa o processamento de regras de entrada:
   1. NSG regra 1 (bloco de Internet) não se aplica (esse tráfego foi NAT seria pelo firewall hello, portanto, o endereço de origem de saudação agora é firewall Olá na sub-rede de segurança hello e vistos por sub-rede de back-end Olá o tráfego do NSG toobe "local" e, portanto, é permitido), mover toonext regra
   2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
6. O AppVM01 está ouvindo o tráfego RDP e responde
7. Sem regras de saída, as regras NSG padrão serão aplicadas e o tráfego de retorno será permitido
8. UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação
9. Porque isso está retornando o tráfego em uma sessão estabelecida Olá de firewall passa o usuário da internet Olá resposta toohello back
10. A sessão RDP está habilitada
11. O AppVM01 solicita a senha do nome de usuário

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Permitido) Pesquisa de DNS do Servidor Web no servidor DNS
1. Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.
2. Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS
3. UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação
4. Nenhuma regra NSG saída é associados toohello front-end subrede, o tráfego é permitido
5. O firewall inicia o processamento de regras:
   1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
   2. Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra
   3. FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra
   4. Regra de FW 8 (tooInternet) não se aplica, mover toonext regra
   5. Aplicar a regra de FW 9 (DNS), o tráfego é permitido, firewall encaminha o tráfego too10.0.2.4 (DNS01)
6. subrede back-end Olá começa o processamento de regras de entrada:
   1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
   2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
7. Servidor DNS recebe a solicitação de saudação
8. Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet
9. UDR roteia o tráfego de saída toohello firewall como próximo salto de saudação
10. Nenhuma regra NSG de saída na sub-rede Backend; o tráfego é permitido
11. O firewall inicia o processamento de regras:
    1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
    2. Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra
    3. FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra
    4. Aplicar FW regra 8 (tooInternet), o tráfego é permitido, sessão é SNAT tooroot Server de DNS na Internet de saudação
12. Servidor DNS da Internet responde, desde que esta sessão foi iniciada no firewall hello, resposta Olá é aceito pelo firewall Olá
13. Como esta é uma sessão estabelecida, o firewall Olá encaminha Olá resposta toohello Iniciar servidor, DNS01
14. subrede back-end Olá começa o processamento de regras de entrada:
    1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
    2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
15. servidor DNS Olá recebe e armazena em cache a resposta de saudação e, em seguida, responde toohello solicitação inicial back tooIIS01
16. rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá
17. Nenhuma regra NSG saída existe na sub-rede de back-end hello, o tráfego é permitido
18. Esta é uma sessão estabelecida no firewall hello, resposta Olá é encaminhada pelo servidor de IIS Olá firewall back toohello
19. A sub-rede Frontend inicia o processamento da regra de entrada:
    1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
    2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido
20. IIS01 recebe a resposta de saudação do DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Permitido) Servidor de tooFrontend do servidor de back-end
1. Um administrador conectado tooAppVM02 via RDP solicita um arquivo diretamente do servidor de IIS01 Olá por meio do Explorador de arquivos do windows
2. rota UDR Olá na sub-rede back-end torna o próximo salto do hello firewall Olá
3. Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede de back-end é permitido
4. O firewall inicia o processamento de regras:
   1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
   2. Regra de firmware 2 a 5 (regras de RDP) não se aplicam, mover toonext regra
   3. FW regras 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra
   4. Regra de FW 8 (tooInternet) não se aplica, mover toonext regra
   5. Não se aplica a regra de FW 9 (DNS), mova a regra toonext
   6. Aplicar FW regra 10 (dentro da sub-rede), o tráfego é permitido, firewall passa tráfego too10.0.1.4 (IIS01)
5. A sub-rede Frontend inicia o processamento da regra de entrada:
   1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
   2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
6. Supondo que a autorização e autenticação adequada, IIS01 aceita a solicitação de saudação e responde
7. rota UDR Olá na sub-rede front-end torna o próximo salto do hello firewall Olá
8. Como não há nenhuma regra NSG saída em Olá resposta de saudação de sub-rede front-end é permitido
9. Pois esta é uma sessão existente no firewall Olá esta resposta é permitida e firewall Olá retorna Olá resposta tooAppVM02
10. A sub-rede Backend inicia o processamento da regra de entrada:
    1. NSG regra 1 (bloco de Internet) não se aplica, mover toonext regra
    2. As regras NSG padrão permitir o tráfego de toosubnet de sub-rede, o tráfego é permitido, pare o processamento de regras NSG
11. AppVM02 recebe a resposta de saudação

#### <a name="denied-internet-direct-tooweb-server"></a>(Negado) Internet direto tooWeb Server
1. Usuário de Internet tenta tooaccess Olá servidor web, IIS01, por meio de saudação FrontEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para o tráfego de HTTP, isso não seria passar Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG (bloco de Internet) na sub-rede de front-end Olá bloqueia esse tráfego
4. Finalmente, rota do hello front-end subrede UDR poderia enviar qualquer tráfego de saída de IIS01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída dessa forma, há pelo menos três camadas independentes de saudação de defesa entre hello IIS01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.

#### <a name="denied-internet-toobackend-server"></a>(Negado) Internet tooBackend Server
1. Usuário de Internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG (bloco de Internet) bloqueia esse tráfego
4. Finalmente, rota UDR Olá poderia enviar qualquer tráfego de saída de AppVM01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída Olá dessa forma, há pelo menos três camadas independentes de defesa entre Olá AppVM01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.

#### <a name="denied-frontend-server-toobackend-server"></a>(Negado) Servidor de front-end tooBackend Server
1. Suponha que IIS01 foi comprometido e está executando código mal-intencionado tentar servidores de sub-rede tooscan Olá back-end.
2. rota UDR Olá front-end subrede poderia enviar qualquer tráfego de saída de IIS01 toohello firewall como próximo salto de saudação. Isso não é algo que pode ser alterada por Olá comprometido VM.
3. firewall Olá processaria tráfego hello, se a solicitação Olá foi tooAppVM01 ou servidor DNS toohello para pesquisas DNS tráfego potencialmente pode ser permitido pelo firewall da saudação (vencimento tooFW regras 7 e 9). Todo o outro tráfego seria bloqueado pela Regra FW 11 (Negar Tudo).
4. Se avançada detecção de ameaças foi habilitada no firewall da saudação (que não é abordado neste documento, consulte a documentação do fornecedor Olá para seu dispositivo de rede específico ameaça recursos avançados), até mesmo o tráfego será permitido pelo Olá básico de regras de encaminhamento abordadas neste documento pode ser impedido se tráfego Olá contido assinaturas conhecidas ou padrões de sinalizar uma regra avançada.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Negado) Pesquisa DNS da Internet no servidor DNS
1. Usuário de Internet tenta toolookup um registro DNS interno em DNS01 por meio do serviço BackEnd001.CloudApp.Net 
2. Como não há nenhum ponto de extremidade aberto para o tráfego de DNS, isso não seria passar Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, Olá NSG regra (bloco de Internet) na sub-rede de front-end Olá a bloquear esse tráfego
4. Finalmente, rota UDR de sub-rede de back-end Olá poderia enviar qualquer tráfego de saída de DNS01 toohello firewall como salto seguinte hello e firewall Olá teria visto como tráfego assimétrico e descartar a resposta de saída dessa forma, há pelo menos três camadas independentes de saudação de defesa entre hello DNS01 e internet por meio de seu serviço de nuvem impedindo o acesso não autorizado/inadequados.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Negado) Acesso à Internet tooSQL através do Firewall
1. O usuário da Internet solicita dados SQL de SecSvc001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)
2. Como não há nenhum ponto de extremidade aberto para SQL, isso não passaria Olá serviço de nuvem e não alcançar o firewall Olá
3. Se o ponto de extremidade do SQL estava aberto por algum motivo, o firewall Olá começaria processamento da regra:
   1. FW regra 1 (FW Mgmt) não se aplica, mover toonext regra
   2. Regras 2 a 5 (regras de RDP) não se aplicam, mova a regra toonext
   3. FW regra 6 e 7 (regras de aplicativo) não se aplicam, mover toonext regra
   4. Regra de FW 8 (tooInternet) não se aplica, mover toonext regra
   5. Não se aplica a regra de FW 9 (DNS), mova a regra toonext
   6. Regra de FW 10 (dentro da sub-rede) não se aplica, mover toonext regra
   7. A Regra FW 11 (Negar Tudo) se aplica; o tráfego é permitido, pare o processamento da regra

## <a name="references"></a>Referências
### <a name="main-script-and-network-config"></a>Script principal e configuração de rede
Salve Olá Script completo em um arquivo de script do PowerShell. Salve Olá configuração de rede em um arquivo denominado "NetworkConf2.xml".
Modificar as variáveis definidas pelo usuário de saudação conforme necessário. Executar script hello, siga as instruções regra de configuração do Firewall Olá acima.

#### <a name="full-script"></a>Script Completo
Esse script vai, com base em variáveis do hello definida pelo usuário:

1. Conecte-se tooan assinatura do Azure
2. Criar uma nova conta de armazenamento
3. Criar uma nova rede virtual e três sub-redes conforme definido no arquivo de configuração de rede de saudação
4. Criar cinco máquinas virtuais; um firewall e quatro VMs do Windows Server
5. Configurar o UDR, incluindo:
   1. Criar duas novas tabelas de rotas
   2. Adicionar rotas toohello tabelas
   3. Associar sub-redes de tooappropriate de tabelas
6. Ativar o encaminhamento IP hello NVA
7. Configure o NSG, incluindo:
   1. Criando um NSG
   2. Adicionando uma regra
   3. Associação de sub-redes apropriados da saudação NSG toohello

Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.

> [!IMPORTANT]
> Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell. Somente as mensagens de erro em vermelho são motivo de preocupação.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Arquivo de configuração de rede
Salve esse arquivo xml com o local atualizado e adicione Olá link toothis arquivo toohello $NetworkConfigFile variável no script de saudação acima.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Scripts de aplicativo de exemplo
Se você quiser tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "DMZ bidirecional com NVA, NSG e UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Modo de exibição lógico de saudação regras de Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Criar um objeto de rede de front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Criar um objeto de servidor DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Cópia da regra RDP padrão"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regra de AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Ícone de redirecionamento do aplicativo"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Ícone de NAT de destino"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Ícone de passagem"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regra de Gerenciamento de Firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regra RDP do firewall"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regra Web do firewall"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regra de AppVM01 do firewall"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regra de saída do firewall"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regra de DNS do firewall"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regra entre VNets do firewall"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regra Negar do firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Ativação de regra de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
