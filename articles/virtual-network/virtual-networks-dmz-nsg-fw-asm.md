---
title: "aaaDMZ exemplo – criar uma rede de Perímetro tooprotect aplicativos com um Firewall e NSGs | Microsoft Docs"
description: "Criar uma DMZ com um Firewall e Grupos de Segurança de Rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Exemplo 2 – criar uma rede de Perímetro tooprotect aplicativos com um Firewall e NSGs
[Retornar toohello página segurança limite de melhores práticas][HOME]

Este exemplo criará uma DMZ com um firewall, quatro servidores Windows e Grupos de Segurança de Rede. Ele também guiará por cada Olá comandos relevantes tooprovide uma compreensão mais profunda de cada etapa. Também há um cenário de tráfego seção tooprovide um detalhadas passo a passo sobre como o tráfego passa as camadas de saudação de defesa Olá DMZ. Por fim, na seção de referências de saudação é código completo hello e instrução toobuild este ambiente tootest e experiência com vários cenários. 

![Entrada de rede de Perímetro com NVA e NSG][1]

## <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, há uma assinatura que contém Olá seguinte:

* Dois serviços de nuvem: "FrontEnd001" e "BackEnd001"
* Uma rede virtual, “CorpNetwork”, com duas sub-redes: “FrontEnd” e “BackEnd”
* Um único grupo de segurança de rede que é aplicada tooboth sub-redes
* Um dispositivo virtual de rede, neste exemplo, um Firewall Barracuda NextGen conectado toohello front-end subrede
* Um Windows Server que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos ("AppVM01", "AppVM02")
* Um servidor Windows que representa um servidor DNS ("DNS01")

> [!NOTE]
> Embora este exemplo usa um Firewall de NextGen Barracuda, muitas das Olá que diferentes dispositivos de rede Virtual pode ser usados para este exemplo.
> 
> 

Na seção de referências de saudação abaixo, há um script do PowerShell que criará a maior parte do ambiente Olá descrito acima. Criando Olá VMs e redes virtuais, embora são feitos pelo script de exemplo hello, não são descritas em detalhes neste documento.

ambiente de saudação toobuild:

1. Salvar arquivo hello rede config xml incluído na seção de referências de saudação (atualizada com nomes, o local e o cenário de saudação fornecido de toomatch de endereços IP)
2. Atualização Olá variáveis no script de Olá Olá script toomatch Olá ambiente é toobe executar (assinaturas, nomes de serviço, etc.)
3. Execute o script hello no PowerShell

**Observação**: região Olá representado em Olá script do PowerShell deve corresponder região Olá representada no arquivo de xml de configuração de rede hello.

Após a execução bem-sucedida do script hello Olá seguindo as etapas de pós-scripts pode ser tomada:

1. Configurar regras de firewall hello, isso é abordado em Olá seção intitulada: regras de Firewall.
2. Opcionalmente, na seção de referências de saudação são dois tooset de scripts, o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro.

Olá próxima seção explica a maioria das Olá scripts instruções relativo tooNetwork grupos de segurança.

## <a name="network-security-groups-nsg"></a>Grupos de segurança de rede (NSG)
Neste exemplo, um grupo NSG é criado e então carregado com seis regras. 

> [!TIP]
> Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última. Olá prioridade determina quais regras são avaliadas primeiro. Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada. Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).
> 
> 

Declarativamente, Olá regras a seguir está sendo compilado para o tráfego de entrada:

1. O tráfego interno de DNS (porta 53) é permitido
2. O tráfego de RDP (porta 3389) do hello Internet tooany VM é permitido
3. O tráfego HTTP (porta 80) de saudação Internet toohello NVA (firewall) é permitido
4. Qualquer tráfego (todas as portas) do IIS01 tooAppVM1 é permitido
5. Qualquer tráfego (todas as portas) do hello Internet toohello VNet inteira (ambas as sub-redes) foi negado
6. Qualquer tráfego (todas as portas) da sub-rede de back-end do hello front-end subrede toohello foi negado

A sub-rede de tooeach associada essas regras, se uma solicitação HTTP foi entrada do servidor web do hello Internet toohello, ambos regras 3 (Permitir) e 5 (Negar) seria aplicado, mas como a regra 3 tem uma prioridade mais alta somente seria aplicada e regra 5 não seria entram em ação. Assim, você seria permitido a solicitação de Olá HTTP toohello firewall. Se o mesmo que o tráfego foi a tentativa de servidor de DNS01 tooreach hello, regra 5 (Negar) seria Olá primeiro tooapply e hello tráfego não será permitido toopass toohello server. Regra de 6 (Negar) blocos Olá front-end subrede contra toohello sub-rede de back-end (com exceção de tráfego permitido nas regras 1 e 4), isso protege a rede de back-end de saudação no caso de um invasor comprometer Olá aplicativo da web em Olá front-end, o invasor Olá teria acesso limitado toohello back-end "protegido" rede (somente tooresources exposto no servidor de AppVM01 Olá).

Há uma regra de saída padrão que permite que o tráfego de saída toohello internet. Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída. toolock tráfego em ambas as direções, roteamento de definido pelo usuário é necessário, isso é explorado em um exemplo de diferente que pode ser encontrados no hello [documento de limite de segurança principal][HOME].

Olá acima discutido NSG regras são muito semelhantes toohello NSG na [exemplo 1: criar uma rede de Perímetro simples com NSGs][Example1]. Analise Olá NSG descrição nesse documento para uma visão detalhada de cada regra NSG e os atributos de TI.

## <a name="firewall-rules"></a>Regras de firewall
Um cliente de gerenciamento será necessário toobe instalado em um firewall de saudação do PC toomanage e criar configurações de saudação necessárias. Consulte o fornecedor de documentação do seu firewall (ou outros NVA) Olá sobre como toomanage Olá dispositivo. restante Olá desta seção descrevem configuração Olá do firewall Olá em si, por meio do cliente de gerenciamento de fornecedores hello (ou seja, não Olá portal do Azure ou o PowerShell).

Instruções para download do cliente e conexão toohello Barracuda usado neste exemplo podem ser encontradas aqui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

No firewall hello, regras de encaminhamento precisará toobe criado. Como este exemplo só roteia o tráfego de entrada toohello firewall da internet e, em seguida, o servidor de web toohello, encaminhamento somente uma regra NAT é necessário. No hello Barracuda NextGen Firewall usado em Olá Este exemplo regra pode ser um destino NAT regra toopass "Horário de verão NAT (") esse tráfego.

a seguir Olá toocreate regra (ou verifique se as regras padrão existente), a partir do painel de cliente Barracuda NG Admin hello, navegue toohello guia de configuração, no hello configuração operacional clique Ruleset. Chamado em uma grade, "Principal regras" mostrará Olá existente regras ativadas e desativadas no firewall hello. No canto superior direito de saudação desta grade é uma pequena verde "+", clique neste toocreate uma nova regra (Observação: seu firewall pode ser "bloqueado" para que as alterações, se você vir um botão marcado "Bloqueio" e são toocreate não é possível ou editar regras, clique neste botão muito "desbloquear" hello conjunto de regras e permitir a edição). Se você quiser tooedit uma regra existente, selecione essa regra, clique com botão direito e selecione Editar regra.

Crie uma nova regra e forneça um nome, como "WebTraffic". 

ícone de regra de NAT de destino Olá tem esta aparência: ![ícone de NAT de destino][2]

regra de saudação em si deve ter esta aparência:

![Regra de firewall][3]

Aqui qualquer endereço de entrada acertos Olá Firewall tentar tooreach HTTP (porta 80 ou 443 para HTTPS) será enviado Olá interface "DHCP1 IP Local" e o toohello redirecionado servidor Web com hello endereço IP do 10.0.1.5 do Firewall. Desde que o tráfego de saudação é recebidas na porta 80 e o servidor de web toohello contínuo na porta 80, nenhuma alteração de porta foi necessária. No entanto, Olá lista de destino podem ter sido 10.0.1.5:8080 se o servidor Web escutar na porta 8080, portanto, traduzindo Olá 80 em Olá firewall tooinbound porta 8080 Olá web servidor de porta de entrada.

Um método de Conexão deve também ser sinalizado, para Olá regra de destino da saudação da Internet, "SNAT dinâmico" é mais apropriado. 

Embora somente uma regra tenha sido criada, é importante que sua prioridade seja definida corretamente. Se na grade de saudação de todas as regras de firewall de saudação a nova regra é na parte inferior da saudação (abaixo da regra de "BLOCKALL" hello), ele nunca será entra em jogo. Certifique-se de regra Olá recém-criado para o tráfego da web é acima de regra BLOCKALL hello.

Depois que Olá regra é criada, ela deve ser enviada por push toohello firewall e, em seguida, ativado, se isso não for feito regra Olá alteração não terá efeito. processo de envio e a ativação de saudação é descrito na próxima seção, Olá.

## <a name="rule-activation"></a>Ativação da regra
Com hello ruleset modificado tooadd essa regra, Olá ruleset deve ser carregado toohello firewall e ativado.

![Ativação de regra de firewall][4]

No canto superior direito de saudação do cliente de gerenciamento de saudação são um cluster de botões. Olá "enviar alterações" botão toosend Olá modificado regras toohello firewall, clique botão de "Ativar" hello.

Com a ativação de saudação do conjunto de regras de firewall Olá esta compilação do ambiente de exemplo foi concluída. Opcionalmente, Olá post compilação scripts no hello referências seção pode ser executados tooadd uma saudação de tootest aplicativo toothis ambiente abaixo cenários de tráfego.

> [!IMPORTANT]
> É toorealize crítica que você não atingirá servidor da web de saudação diretamente. Quando um navegador solicita uma página HTTP do FrontEnd001.CloudApp.Net, servidor web passa de ponto de extremidade (porta 80) HTTP Olá esse tráfego toohello firewall não hello. Olá firewall em seguida, de acordo com regra toohello criado acima NATs que solicitam toohello servidor Web.
> 
> 

## <a name="traffic-scenarios"></a>Cenários de tráfego
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Permitido) TooWeb Web Server através do Firewall
1. Usuário da Internet solicita uma página HTTP de FrontEnd001.CloudApp.Net (Internet Voltada para o Serviço de Nuvem)
2. Tráfego passa do serviço de nuvem por meio de um ponto de extremidade aberto na porta 80 toofirewall local interface 10.0.1.4:80
3. A sub-rede Frontend inicia o processamento da regra de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. Aplicar NSG regra 3 (Internet tooFirewall), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)
5. Regra de firewall encaminhamento ver isso é o tráfego na porta 80, redireciona o servidor de web toohello IIS01
6. IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação
7. IIS01 solicita saudação do SQL Server em AppVM01 informações
8. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
9. subrede back-end Olá começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra
   4. 4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa
10. AppVM01 recebe Olá consulta SQL e responde
11. Como não há nenhuma saídas regras em Olá resposta de saudação de sub-rede de back-end é permitido
12. A sub-rede Frontend inicia o processamento da regra de entrada:
    1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
    2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.
13. servidor do IIS Olá recebe a resposta SQL hello e conclui a resposta HTTP hello e envia toohello solicitante
14. Como esta é uma sessão NAT de firewall Olá, destino de resposta da saudação (inicialmente) é para Olá Firewall
15. firewall Olá recebe resposta de saudação do Olá Web Server e encaminha back toohello usuário pela Internet
16. Como não há nenhum regras de saída em Olá resposta de saudação do front-end subrede é permitido e Olá usuário pela Internet recebe Olá web página solicitada.

#### <a name="allowed-rdp-toobackend"></a>(Permitido) TooBackend RDP
1. Administrador do servidor na internet solicitações tooAppVM01 de sessão RDP no BackEnd001.CloudApp.Net:xxxxx onde xxxxx é o número da porta Olá atribuído aleatoriamente para RDP tooAppVM01 (porta Olá atribuído pode ser encontrada em Olá Portal do Azure ou por meio do PowerShell)
2. Desde Olá que firewall está escutando apenas em Olá FrontEnd001.CloudApp.Net endereço, ele não está envolvido com esse fluxo de tráfego
3. A sub-rede Backend inicia o processamento da regra de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra
4. Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido
5. A sessão RDP está habilitada
6. O AppVM01 solicita a senha do nome de usuário

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Permitido) Pesquisa de DNS do Servidor Web no servidor DNS
1. Web necessidades de servidor, IIS01, um feed de dados em www.data.gov, mas precisa tooresolve Olá endereço.
2. Olá configuração de rede para listas de rede virtual Olá DNS01 (10.0.2.4 na sub-rede de back-end Olá) como o servidor DNS primário de hello, IIS01 envia Olá tooDNS01 de solicitação DNS
3. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
4. A sub-rede Backend inicia o processamento da regra de entrada:
   1. A regra NSG 1 (DNS) não se aplica; o tráfego é permitido, pare o processamento da regra
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Permitido) O arquivo de acesso do Servidor Web em AppVM01
1. IIS01 solicita um arquivo em AppVM01
2. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
3. subrede back-end Olá começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. NSG regra 3 (tooFirewall da Internet) não se aplica, mover toonext regra
   4. 4 de regra NSG (IIS01 tooAppVM01) se aplicam, o tráfego é o processamento de regras permitido, interrompa
4. AppVM01 recebe a solicitação de saudação e responde com o arquivo (supondo que o acesso é autorizado)
5. Como não há nenhuma saídas regras em Olá resposta de saudação de sub-rede de back-end é permitido
6. A sub-rede Frontend inicia o processamento da regra de entrada:
   1. Não há nenhuma regra NSG que aplica tooInbound tráfego da sub-rede de front-end do toohello de sub-rede de back-end Olá, para que nenhuma das regras do NSG Olá aplicar
   2. regra do sistema padrão Olá permitindo o tráfego entre as sub-redes permitiria que esse tráfego para que o tráfego de saudação é permitido.
7. servidor do IIS Olá recebe arquivo hello

#### <a name="denied-web-direct-tooweb-server"></a>(Negado) TooWeb direta do Web Server
Desde Olá servidor Web, IIS01 e Olá Firewall são em Olá mesmo serviço de nuvem, eles compartilham Olá mesmo endereço IP público. Assim, qualquer tráfego HTTP seria direcionado toohello firewall. Enquanto a solicitação de saudação utilizarão com êxito, não pode ir diretamente toohello servidor Web, ele passado como criados, por meio de saudação do Firewall pela primeira vez. Consulte Olá primeiro cenário nesta seção para fluxo de tráfego de saudação.

#### <a name="denied-web-toobackend-server"></a>(Negado) TooBackend Web Server
1. Usuário de Internet tenta tooaccess um arquivo em AppVM01 por meio de saudação BackEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para compartilhamento de arquivos, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Negado) Pesquisa de DNS na Web no servidor DNS
1. Usuário de Internet tenta toolookup um registro DNS interno em DNS01 por meio de saudação BackEnd001.CloudApp.Net serviço
2. Como não há nenhum ponto de extremidade aberto para DNS, isso não passaria Olá serviço de nuvem e não alcançar o servidor de saudação
3. Se o ponto de extremidade de saudação estava aberto por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: essa regra 1 (DNS) não se aplicariam por dois motivos, primeiro endereço de origem de saudação é Olá da internet, esta regra só se aplica a toohello redes locais como saudação de origem, também Esta é uma regra de permissão, para que ele nunca seria negar o tráfego)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Negado) Acesso via Web tooSQL através do Firewall
1. O usuário da Internet solicita dados SQL de FrontEnd001.CloudApp.Net (Serviço de Nuvem Voltado para a Internet)
2. Como não há nenhum ponto de extremidade aberto para SQL, isso não passaria Olá serviço de nuvem e não alcançar o firewall Olá
3. Se o ponto de extremidade estava aberto por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:
   1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
   2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
   3. Aplicar NSG regra 2 (Internet tooFirewall), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do firewall hello (10.0.1.4)
5. Firewall não tem nenhuma regra de encaminhamento para SQL e descarta Olá tráfego

## <a name="conclusion"></a>Conclusão
Essa é uma maneira relativamente simples de proteger seu aplicativo com um firewall e o isolamento de sub-rede de back-end de saudação do tráfego de entrada.

Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].

## <a name="references"></a>Referências
### <a name="main-script-and-network-config"></a>Script principal e configuração de rede
Salve Olá Script completo em um arquivo de script do PowerShell. Salve Olá configuração de rede em um arquivo denominado "NetworkConf2.xml".
Modificar as variáveis definidas pelo usuário de saudação conforme necessário. Executar script hello, siga as instruções regra de configuração do Firewall Olá acima.

#### <a name="full-script"></a>Script Completo
Esse script vai, com base em variáveis do hello definida pelo usuário:

1. Conecte-se tooan assinatura do Azure
2. Criar uma nova conta de armazenamento
3. Criar uma nova rede virtual e duas sub-redes, conforme definido no arquivo de configuração de rede de saudação
4. Criar 4 VMs do windows server
5. Configure o NSG, incluindo:
   * Criando um NSG
   * Preenchendo-o com regras
   * Associação de sub-redes apropriados da saudação NSG toohello

Este script do PowerShell deve ser executado localmente em um computador ou servidor conectado à Internet.

> [!IMPORTANT]
> Quando esse script for executado, poderá haver avisos ou outras mensagens informativas que aparecerão no PowerShell. Somente as mensagens de erro em vermelho são motivo de preocupação.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "DMZ de entrada com NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Ícone de NAT de destino"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regra de Firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Ativação de regra de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
