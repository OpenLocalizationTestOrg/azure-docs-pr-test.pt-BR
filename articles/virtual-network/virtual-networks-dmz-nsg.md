---
title: "aaaAzure exemplo DMZ – criar uma rede de Perímetro simples com NSGs | Microsoft Docs"
description: "Criar uma DMZ com grupos de segurança de rede (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Exemplo 1 – Criar uma DMZ simples usando NSGs com um modelo do Azure Resource Manager
[Retornar toohello página segurança limite de melhores práticas][HOME]

> [!div class="op_single_selector"]
> * [Modelo do Resource Manager](virtual-networks-dmz-nsg.md)
> * [Clássico - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Este exemplo criará uma DMZ simples com quatro servidores Windows e Grupos de Segurança de Rede. Este exemplo descreve cada Olá modelo relevante seções tooprovide uma compreensão mais profunda de cada etapa. Há também um tooprovide da seção de cenário de tráfego uma Visão aprofundada passo a passo de como o tráfego passa camadas Olá de defesa Olá DMZ. Por fim, na seção de referências de saudação é Olá toobuild de código e instruções do modelo completo neste ambiente tootest e experiência com vários cenários. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![DMZ de entrada com NSG][1]

## <a name="environment-description"></a>Descrição do ambiente
Neste exemplo, uma assinatura contém Olá recursos a seguir:

* Um único grupo de recursos
* Uma rede virtual com duas sub-redes: “FrontEnd” e “BackEnd”
* Um grupo de segurança de rede que é aplicada tooboth sub-redes
* Um Windows Server que representa um servidor Web de aplicativos ("IIS01")
* Dois servidores Windows que representam servidores de back-end de aplicativos (“AppVM01”, “AppVM02”)
* Um servidor Windows que representa um servidor DNS ("DNS01")
* Um endereço IP público associado Olá aplicativo servidor web

Na seção de referências de hello, há um modelo do Azure Resource Manager tooan de link que cria um ambiente de saudação descrito neste exemplo. Criando Olá VMs e redes virtuais, embora feito pelo modelo de exemplo hello, não são descritas em detalhes neste documento. 

**toobuild esse ambiente** (são instruções detalhadas na seção de referências de saudação deste documento);

1. Implantar Olá modelo do Gerenciador de recursos do Azure em: [modelos de início rápido do Azure][Template]
2. Instalar o aplicativo de exemplo hello em: [Script de exemplo de aplicativo][SampleApp]

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa". Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end. Como alternativa, um IP público pode ser associado a cada servidor de NIC para realizar RDP mais facilmente.
> 
>

Olá seções a seguir fornecem uma descrição detalhada do hello grupo de segurança de rede e como ele funciona para este exemplo, acompanhando a linhas de chave de saudação modelo do Gerenciador de recursos do Azure.

## <a name="network-security-groups-nsg"></a>Grupos de segurança de rede (NSG)
Neste exemplo, um grupo NSG é criado e então carregado com seis regras. 

>[!TIP]
>Em geral, você deve primeiro criar suas regras específicas de "Permitir" e Olá a regras mais genéricas de "Negar" última. Olá prioridade determina quais regras são avaliadas primeiro. Depois que o tráfego for encontrado uma regra específica de tooa tooapply, nenhuma regra adicional será avaliada. Regras NSG podem ser aplicados em Olá direção de entrada ou saída (da perspectiva de saudação da sub-rede Olá).
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

Há uma regra de saída padrão que permite que o tráfego de saída toohello internet. Neste exemplo, permitiremos o tráfego de saída e não modificaremos quaisquer regras de saída. tootraffic de política de segurança de tooapply em ambas as direções, roteamento de definido pelo usuário é necessário e explorado no "Exemplo 3" no hello [página segurança limite de melhores práticas][HOME].

Cada regra é discutida com mais detalhes a seguir:

1. Um recurso de grupo de segurança de rede deve ser instanciadas toohold Olá regras:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. a primeira regra Olá neste exemplo permite que o tráfego DNS entre todos os servidores DNS toohello redes internas na sub-rede de back-end de saudação. regra de saudação tem alguns parâmetros importantes:
  * "destinationAddressPrefix" - regras podem usar um tipo especial de prefixo de endereço chamado uma "marca padrão", essas marcas são identificadores fornecidos pelo sistema que permitem uma maneira fácil de tooaddress uma categoria de maior de prefixos de endereço. Esta regra usa Olá marca padrão "Internet" toosignify os endereços fora Olá VNet. VirtualNetwork e AzureLoadBalancer são outros exemplos de rótulos de prefixo.
  * “Direction” (Direção) indica em qual direção do fluxo de tráfego esta regra entra em vigor. direção de saudação é da perspectiva de saudação de sub-rede hello ou máquina Virtual (dependendo de onde essa NSG está associado). Portanto, se direção "Entrada" e o tráfego é entra sub-rede hello, Olá regra se aplica e tráfego deixando sub-rede Olá não é afetado por essa regra.
  * "Priority" define a ordem de saudação no qual um fluxo de tráfego é avaliado. Olá inferior Olá número Olá Olá prioridade. Quando uma regra se aplica o fluxo de tráfego específico tooa, nenhuma regra adicional é processada. Portanto, se uma regra com prioridade 1 permite o tráfego e uma regra com prioridade 2 nega o tráfego e ambas as regras se aplicam a tootraffic então Olá tráfego será permitido tooflow (desde que a regra 1 tinha uma prioridade mais alta que levou o efeito e nenhuma regra adicional foram aplicada).
  * “Action” (Ação) indica se um tráfego afetado por essa regra é bloqueado (“Deny”, Negar) ou permitido (“Allow”, Permitir).

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Essa regra permite tooflow de tráfego RDP de porta do RDP Olá internet toohello em qualquer servidor Olá associado a sub-rede. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Essa regra permite que o servidor de web do entrada da internet tráfego toohit hello. Essa regra não altera o comportamento de roteamento hello. regra de saudação permite apenas o tráfego destinado a IIS01 toopass. Portanto, se o tráfego de Internet de saudação tivesse servidor de web hello como seu destino essa regra deve permitir que ele e parar o processamento mais regras. (Regra Olá em prioridade 140 todos os outros tráfego da internet é bloqueado). Se você só estiver processando o tráfego de HTTP, essa regra pode ser mais restrito tooonly permitir destino porta 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Essa regra permite toopass de tráfego do servidor de IIS01 Olá toohello AppVM01 server, uma regra posterior bloqueia todos os outros tráfegos de tooBackend de front-end. tooimprove esta regra, se a porta de saudação é conhecida que deve ser adicionada. Por exemplo, se servidor IIS hello está atingindo somente SQL Server no AppVM01, Olá intervalo de portas de destino deverá ser alterado de "*" (qualquer) too1433 (Olá porta do SQL), permitindo uma menor superfície de ataque de entrada em AppVM01 deve aplicativo da web hello comprometido.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Esta regra nega o tráfego de servidores na rede Olá tooany da internet hello. Com as regras de saudação em prioridade 110 e 120, o efeito de saudação é tooallow somente internet tráfego toohello firewall de entrada e as portas do RDP em servidores e bloqueia todo o resto. Essa regra é "à prova de falhas" regra tooblock todos os fluxos inesperados.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. regra final Olá nega o tráfego de sub-rede de back-end do hello front-end subrede toohello. Como essa regra é uma regra de entrada única, inversa de tráfego é permitida (de back-end de saudação toohello front-end).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Cenários de tráfego
#### <a name="allowed-internet-tooweb-server"></a>(*Permitidos*) servidor tooweb da Internet
1. Um usuário de internet solicita uma página HTTP do endereço IP público de saudação do hello que NIC associada Olá IIS01 NIC
2. Olá endereço IP público passa tráfego toohello VNet para IIS01 (servidor de web hello)
3. A sub-rede Frontend inicia o processamento da regra de entrada:
  1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
  2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
  3. Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do servidor de web hello IIS01 (10.0.1.5)
5. IIS01 está escutando o tráfego da web, recebe essa solicitação e inicia o processamento de solicitação de saudação
6. IIS01 solicita saudação do SQL Server em AppVM01 informações
7. Não há regras de saída na sub-rede Frontend; o tráfego é permitido
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
13. Como não há nenhuma regra de saída na sub-rede de front-end hello, Olá resposta seja permitida e Olá Internet usuário recebe Olá web página solicitada.

#### <a name="allowed-rdp-tooiis-server"></a>(*Permitidos*) servidor tooIIS RDP
1. Um administrador do servidor na internet solicita um tooIIS01 de sessão RDP no endereço IP público de saudação do hello que NIC associada Olá IIS01 NIC (esse endereço IP público pode ser encontrado por meio de saudação Portal ou o PowerShell)
2. Olá endereço IP público passa tráfego toohello VNet para IIS01 (servidor de web hello)
3. A sub-rede Frontend inicia o processamento da regra de entrada:
  1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
  2. A regra NSG 2 (RDP) não se aplica; o tráfego é permitido, pare o processamento da regra
4. Sem regras de saída, as regras padrão serão aplicadas e o tráfego de retorno será permitido
5. A sessão RDP está habilitada
6. Prompts de IIS01 Olá nome de usuário e senha

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa". Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.
>
>

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

#### <a name="denied-rdp-toobackend"></a>(*Negado*) toobackend RDP
1. Um usuário de internet tenta tooRDP tooserver AppVM01
2. Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação
3. Contudo, se um endereço IP público tiver sido habilitado por algum motivo, a regra NSG 2 (RDP) permitiria esse tráfego

>[!NOTE]
>servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa". Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Negado*) servidor do Web toobackend
1. Um usuário de internet tenta tooaccess um arquivo em AppVM01
2. Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação
3. Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negado*) Pesquisa de DNS na Web no servidor DNS
1. Um usuário de internet tenta toolook um registro de DNS interno em DNS01
2. Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação
3. Se um endereço IP público foi ativado por algum motivo, a regra NSG 5 (Internet tooVNet) bloqueia esse tráfego (Observação: regra 1 (DNS) não é aplicável porque Olá solicita o endereço de origem é Olá internet e regra 1 só se aplica a toohello rede local virtual como fonte de saudação)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Negado*) acesso ao SQL no servidor de web Olá
1. Um usuário da Internet solicita dados SQL do IIS01
2. Como não há nenhum endereço IP público associado a esta NIC de servidores, esse tráfego nunca insira Olá rede virtual e não alcançar o servidor de saudação
3. Se um endereço IP público foi ativado por algum motivo, sub-rede front-end de saudação começa o processamento de regras de entrada:
  1. Não se aplica a regra 1 (DNS), NSG, mover toonext regra
  2. 2 de regra NSG (RDP) não se aplica, mover toonext regra
  3. Aplicar NSG regra 3 (Internet tooIIS01), o tráfego é o processamento de regras permitido, interrompa
4. Tráfego atinge o endereço IP interno do hello IIS01 (10.0.1.5)
5. IIS01 não está escutando na porta 1433, assim nenhuma solicitação de toohello de resposta

## <a name="conclusion"></a>Conclusão
Este exemplo é uma maneira relativamente simple e direta de isolamento de sub-rede de back-end de saudação do tráfego de entrada.

Mais exemplos e uma visão geral dos limites de segurança de rede podem ser encontrados [aqui][HOME].

## <a name="references"></a>Referências
### <a name="azure-resource-manager-template"></a>Modelo do Azure Resource Manager
Este exemplo usa um modelo do Azure Resource Manager predefinido em um repositório GitHub mantido pela Microsoft e abra toohello comunidade. Esse modelo pode ser implantado diretamente fora do GitHub, ou baixado e modificadas toofit suas necessidades. 

modelo principal Hello está no arquivo hello denominado "azuredeploy.json". Esse modelo pode ser enviado por meio do PowerShell ou CLI (com o arquivo de associado "azuredeploy.parameters.json" hello) toodeploy este modelo. Localizar hello mais fácil é forma toouse Olá botão "Implantar tooAzure" na página de README.md Olá no GitHub.

modelo de saudação toodeploy que se baseia neste exemplo do GitHub e hello portal do Azure, siga estas etapas:

1. Em um navegador, navegue toohello [modelo][Template]
2. Clique em botão de "Implantar tooAzure" hello (ou hello "Visualizar" botão toosee uma representação gráfica do modelo)
3. Digite hello conta de armazenamento, o nome de usuário e senha na folha de parâmetros de saudação, clique em **Okey**
5. Criar um Grupo de Recursos para essa implantação (você pode usar uma existente, mas é recomendável usar uma nova para obter melhores resultados)
6. Se necessário, altere as configurações de assinatura e localização de saudação para sua rede virtual.
7. Clique em **revisar os termos legais**, leia os termos de saudação e clique em **compra** tooagree.
8. Clique em **criar** toobegin implantação Olá desse modelo.
9. Depois que a implantação Olá concluída com êxito, navegar toohello que grupo de recursos criado para esta implantação toosee Olá os recursos configurados dentro.

>[!NOTE]
>Esse modelo permite que o RDP toohello IIS01 somente servidor (Olá localizar IP público para IIS01 em Olá Portal). servidores de back-end tooany tooRDP nesta instância, o servidor do IIS Olá é usado como uma "salto caixa". Primeiro servidor IIS toohello RDP e, em seguida, do servidor de saudação RDP do servidor IIS toohello back-end.
>
>

tooremove essa implantação, Olá excluir grupo de recursos e todos os recursos filho também serão excluídos.

#### <a name="sample-application-scripts"></a>Scripts de aplicativo de exemplo
Depois que o modelo de saudação é executado com êxito, você pode definir o servidor de web hello e servidor de aplicativos com um tooallow de aplicativo da web simples teste com essa configuração de rede de Perímetro. tooinstall um aplicativo de exemplo para este e outros exemplos de rede de Perímetro, foi fornecido no hello link a seguir: [Script de exemplo de aplicativo][SampleApp]

## <a name="next-steps"></a>Próximas etapas

* Implantar este exemplo
* Criar aplicativo de exemplo hello
* Testar diferentes fluxos de tráfego por meio dessa DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "DMZ de entrada com NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md