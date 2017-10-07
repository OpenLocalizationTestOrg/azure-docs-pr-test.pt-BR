---
title: "aaaAzure exemplo DMZ – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
description: "Criar uma DMZ com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Exemplo 1 – Criar uma DMZ simples usando NSGs com o PowerShell clássico
[Retornar toohello página segurança limite de melhores práticas][HOME]

> [!div class="op_single_selector"]
> * [Modelo do Resource Manager](virtual-networks-dmz-nsg.md)
> * [Clássico - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede. Este exemplo descreve cada Olá relevantes PowerShell comandos tooprovide uma compreensão mais profunda de cada etapa. Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ. Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários. 

![DMZ de entrada com NSG][1]

## <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, uma assinatura contém Olá recursos a seguir:

* Dois serviços de nuvem: "FrontEnd001" e "BackEnd001"
* Uma rede virtual, “CorpNetwork”, com duas sub-redes, “FrontEnd” e “BackEnd”
* Um grupo de segurança de rede que é aplicada tooboth sub-redes
* Um Windows Server que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)
* Um servidor Windows que representa um servidor DNS ("DNS01")

Na seção de referências de hello, há um script do PowerShell que cria a maior parte do ambiente de saudação descrito neste exemplo. Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento. 

ambiente de saudação toobuild;

1. Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)
2. Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)
3. Execute o script hello no PowerShell

>[!Note]
>região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.
>
>

Depois que o script hello é executado com êxito adicional etapas opcionais que podem ser tomadas, na seção de referências de saudação dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.

Olá seções a seguir fornecem uma descrição detalhada dos grupos de segurança de rede e como eles funcionam para este exemplo, acompanhando a linhas de chave de script do PowerShell hello.

## <a name="network-security-groups-nsg"></a>Grupos de segurança de rede (NSG)
Neste exemplo, um grupo NSG é criado e então carregado com seis regras. 

> [!TIP]
> Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última. Olá prioridade determina quais regras são avaliadas primeiro. Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada. Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).
> 
> 

Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:

1. O tráfego interno de DNS (porta 53) é permitido
2. O tráfego de RDP (porta 3389) do hello Internet tooany VM é permitido
3. O tráfego HTTP (porta 80) Olá tooweb do servidor de Internet (IIS01) é permitido
4. Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido
5. Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteira (ambas as sub-redes) foi negado
6. Qualquer tráfego (todas as portas) da sub-rede de back-end do hello front-end subrede toohello foi negado

A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicado, mas como a regra 3 tem uma prioridade mais alta somente seria aplicada e regra 5 não seria entram em ação. Assim você seria permitido a solicitação HTTP Olá toohello servidor de web. Se o mesmo que o tráfego foi a tentativa de servidor de DNS01 tooreach hello, regra 5 (Negar) seria Olá primeiro tooapply e hello tráfego não será permitido toopass toohello server. Regra 6 (Negar) bloqueia a sub-rede de front-end de saudação do falando toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4), esse conjunto de regras protege a rede de back-end Olá no caso de um invasor comprometer Olá aplicativo da web em Olá front-end, invasor Olá seria limitado toohello de acesso (somente tooresources exposto no servidor de AppVM01 Olá) de rede back-end "protegido".

Há uma regra de saída padrão que permite que o tráfego de saída toohello internet. Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída. toolock tráfego em ambas as direções, roteamento de definido pelo usuário é necessário e explorado no "Exemplo 3" no hello [página segurança limite de melhores práticas][HOME].

Cada regra é discutida mais detalhadamente como segue (**Observação**: qualquer item na Olá a seguir lista começando com um sinal de cifrão (por exemplo: $NSGName) é uma variável definida pelo usuário do script hello na seção de referência Olá deste documento):

1. Primeiro um grupo de segurança de rede devem ser compilado regras de saudação toohold:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. a primeira regra Olá neste exemplo permite que o tráfego DNS entre todos os servidores DNS toohello redes internas na sub-rede de back-end de saudação. regra de saudação tem alguns parâmetros importantes:
   
   * “Type” (Tipo) indica em qual direção do fluxo de tráfego esta regra entra em vigor. direção de saudação é da perspectiva de saudação de sub-rede hello ou máquina Virtual (dependendo de onde essa NSG está associado). Portanto, se o tipo é "Entrada" e tráfego está inserindo a sub-rede de saudação, Olá regra se aplica e tráfego deixando sub-rede Olá não é afetado por essa regra.
   * "Priority" define a ordem de saudação no qual um fluxo de tráfego é avaliado. Olá inferior Olá número Olá Olá prioridade. Quando uma regra se aplica o fluxo de tráfego específico tooa, nenhuma regra adicional é processada. Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 nega o tráfego e ambas as regras se aplicam a tootraffic então Olá tráfego será permitido tooflow (desde que a regra 1 tinha uma prioridade mais alta que levou o efeito e nenhuma regra adicional foram aplicada).
   * "Action" significa se um tráfego afetado por essa regra é bloqueado ou permitido.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Essa regra permite tooflow de tráfego RDP de porta do RDP Olá internet toohello em qualquer servidor Olá associado a sub-rede. Essa regra usa dois tipos especiais de prefixos de endereço; “VIRTUAL_NETWORK” e “INTERNET”. Essas marcas são uma maneira fácil de tooaddress uma categoria de maior de prefixos de endereço.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Essa regra permite que o servidor de web do entrada da internet tráfego toohit hello. Essa regra não altera o comportamento de roteamento hello. regra de saudação permite apenas o tráfego destinado a IIS01 toopass. Portanto, se o tráfego de Internet de saudação tivesse servidor de web hello como seu destino essa regra deve permitir que ele e parar o processamento mais regras. (Regra Olá em prioridade 140 todos os outros tráfego da internet é bloqueado). Se você só estiver processando o tráfego de HTTP, essa regra pode ser mais restrito tooonly permitir destino porta 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Essa regra permite toopass de tráfego do servidor de IIS01 Olá toohello AppVM01 server, uma regra posterior bloqueia todos os outros tráfegos de tooBackend de front-end. tooimprove esta regra, se a porta de saudação é conhecida que deve ser adicionada. Por exemplo, se servidor IIS hello está atingindo somente SQL Server no AppVM01, Olá intervalo de portas de destino deverá ser alterado de "*" (qualquer) too1433 (Olá porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 deve aplicativo da web hello comprometido.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Esta regra nega o tráfego de servidores na rede Olá tooany da internet hello. Com as regras de saudação em prioridade 110 e 120, o efeito de saudação é tooallow somente internet tráfego toohello firewall de entrada e as portas do RDP em servidores e bloqueia todo o resto. Essa regra é "à prova de falhas" regra tooblock todos os fluxos inesperados.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. regra final Olá nega o tráfego de sub-rede de back-end do hello front-end subrede toohello. Como essa regra é uma regra de entrada única, inversa de tráfego é permitida (de back-end de saudação toohello front-end).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Cenários de tráfego
#### <a name="allowed-internet-tooweb-server"></a>(*Permitidos*) servidor tooweb da Internet
1. Um usuário da Internet solicita uma página HTTP de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para Internet)
2. Nuvem tráfego passa do serviço por meio de um ponto de extremidade aberto na porta 80 para IIS01 (servidor de web hello)
3. A sub-rede Frontend inicia o processamento da regra de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do servidor de web hello IIS01 (10.0.1.5)
5. IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação
6. IIS01 solicita saudação do SQL Server em AppVM01 informações
7. Como não há regras de saída na sub-rede Frontend, o tráfego é permitido
8. subrede back-end Olá começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra
   4. 4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa
9. AppVM01 recebe Olá consulta SQL e responde
10. Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida
11. A sub-rede Frontend inicia o processamento da regra de entrada:
    1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
    2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.
12. servidor do IIS Olá recebe a resposta SQL hello e conclui a resposta HTTP hello e envia toohello solicitante
13. Como não há nenhuma regra de saída na sub-rede de front-end Olá Olá resposta seja permitida, e hello internet usuário recebe Olá web página solicitada.

#### <a name="allowed-rdp-toobackend"></a>(*Permitidos*) toobackend RDP
1. Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP no BackEnd001.CloudApp.Net:xxxxx onde xxxxx é o número da porta Olá atribuído aleatoriamente para RDP tooAppVM01 (porta Olá atribuído pode ser encontrada em Olá portal do Azure ou por meio do PowerShell)
2. A sub-rede Backend inicia o processamento da regra de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra
3. Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido
4. A sessão RDP está habilitada
5. Prompts de AppVM01 Olá nome de usuário e senha

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Permitido*) Pesquisa de DNS do servidor Web no servidor DNS
1. Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.
2. Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS
3. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
4. A sub-rede Backend inicia o processamento da regra de entrada:
   * A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra
5. Servidor DNS recebe a solicitação de saudação
6. Servidor DNS não tem endereço Olá armazenado em cache e solicita que um servidor DNS raiz em Olá internet
7. Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido
8. Resposta de saudação responde do servidor DNS da Internet, desde que esta sessão foi iniciada internamente, é permitida
9. Servidor DNS armazena em cache a resposta hello e responde toohello solicitação inicial back tooIIS01
10. Nenhuma regra de saída na sub-rede Backend; o tráfego é permitido
11. A sub-rede Frontend inicia o processamento da regra de entrada:
    1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
    2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que Olá tráfego é permitido
12. IIS01 recebe a resposta de saudação do DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Permitido*) Arquivo de acesso do servidor Web em AppVM01
1. IIS01 solicita um arquivo em AppVM01
2. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
3. subrede back-end Olá começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. NSG regra 3 (tooIIS01 da Internet) não se aplica, mover toonext regra
   4. 4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa
4. AppVM01 recebe a solicitação de saudação e responde com o arquivo (supondo que o acesso é autorizado)
5. Como não há nenhuma regra de saída na sub-rede de back-end hello, resposta Olá é permitida
6. A sub-rede Frontend inicia o processamento da regra de entrada:
   1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
   2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.
7. servidor do IIS Olá recebe arquivo hello

#### <a name="denied-web-toobackend-server"></a>(*Negado*) servidor do Web toobackend
1. Um usuário de internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, esse tráfego não passaria Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negado*) Pesquisa de DNS na Web no servidor DNS
1. Um usuário de internet tenta toolook um registro de DNS interno em DNS01 por meio de saudação BackEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para DNS, esse tráfego não passaria Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: essa regra 1 (DNS) não se aplicariam por dois motivos, primeiro endereço de origem de saudação é Olá da internet, esta regra só se aplica a toohello redes locais como saudação de origem, também Essa regra é uma regra de permissão, portanto ele nunca seria negar o tráfego)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Negado*) Web tooSQL acesso através do firewall
1. Um usuário da Internet solicita dados SQL de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)
2. Como não há nenhum ponto de extremidade aberto para SQL, esse tráfego não passaria Olá serviço de nuvem e não alcançar o firewall Olá
3. Se o ponto de extremidade estava aberto por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do hello IIS01 (10.0.1.5)
5. IIS01 não está escutando na porta 1433, assim nenhuma solicitação de toohello de resposta

## <a name="conclusion"></a>Conclusão
Este exemplo é uma maneira relativamente simple e direta de isolamento de sub-rede de back-end de saudação do tráfego de entrada.

Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].

## <a name="references"></a>Referências
### <a name="main-script-and-network-config"></a>Script principal e configuração de rede
Salve Olá Script completo em um arquivo de script do PowerShell. Salvar Olá configuração de rede em um arquivo denominado "NetworkConf1.xml".
Modificar Olá variáveis definidas pelo usuário como script hello necessários e execução.

#### <a name="full-script"></a>Script completo
Esse script será, com base em variáveis definidas pelo usuário Olá;

1. Conecte-se tooan assinatura do Azure
2. Criar uma conta de armazenamento
3. Criar uma rede virtual e duas sub-redes, conforme definido no arquivo de configuração de rede de saudação
4. Crie quatro VMs do Windows Server
5. Configure o NSG, incluindo:
   * Criando um NSG
   * Preenchendo-o com regras
   * Associação de sub-redes apropriados da saudação NSG toohello

Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.

> [!IMPORTANT]
> Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell. Somente as mensagens de erro em vermelho são motivo de preocupação.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Arquivo de configuração de rede
Salve esse arquivo xml com o local atualizado e adicionar variável de toohello $NetworkConfigFile Olá link toothis arquivo hello precede o script.

```XML
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
```

#### <a name="sample-application-scripts"></a>Scripts de aplicativo de exemplo
Se você quiser tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]

## <a name="next-steps"></a>Próximas etapas
* Atualizar e salvar o arquivo XML
* Executar o ambiente de saudação do hello PowerShell script toobuild
* Instalar o aplicativo de exemplo hello
* Testar diferentes fluxos de tráfego por meio dessa DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "DMZ de entrada com NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

