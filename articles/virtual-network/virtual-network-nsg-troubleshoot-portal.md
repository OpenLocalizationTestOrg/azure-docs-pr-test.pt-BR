---
title: "aaaTroubleshoot grupos de segurança de rede - Portal | Microsoft Docs"
description: "Saiba como grupos de segurança de rede tootroubleshoot na implantação do Azure Resource Manager Olá modelo usando Olá Portal do Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Solucionar problemas de grupos de segurança de rede usando Olá Portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Se configurado os grupos de segurança de rede (NSGs) em sua máquina virtual (VM) e estão com problemas de conectividade VM, este artigo fornece uma visão geral dos recursos de diagnóstico para os NSGs toohelp solucionar outros problemas.

Os NSGs permitem que você toocontrol tipos de saudação do tráfego de fluxo para dentro e fora de suas máquinas virtuais (VMs). Os NSGs podem ser aplicadas toosubnets em uma rede Virtual do Azure (VNet), interfaces de rede (NIC) ou ambos. Olá efetivo regras aplicadas tooa NIC são uma agregação das regras de saudação que existem no hello NSGs aplicados tooa NIC e hello sub-rede está conectado ao. As regras nesses NSGs podem, às vezes, entrar em conflito umas com as outras e afetar a conectividade de rede de uma VM.  

Você pode exibir todas as regras de segurança efetiva de saudação do seus NSGs aplicados ao NICs da VM. Este artigo mostra como problemas de conectividade VM tootroubleshoot usando essas regras em Olá modelo de implantação do Gerenciador de recursos do Azure. Se você não estiver familiarizado com conceitos de rede virtual e NSG, leia Olá [rede Virtual](virtual-networks-overview.md) e [grupos de segurança de rede](virtual-networks-nsg.md) artigos de visão geral.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Usando o fluxo de tráfego VM de tootroubleshoot de regras de segurança efetiva
cenário de saudação que segue é um exemplo de um problema de conexão comum:

Uma VM denominada *VM1* faz parte de uma sub-rede denominada *Subnet1* em uma VNet denominada *WestUS-VNet1*. Toohello de tooconnect uma tentativa de VM usando o RDP usando a porta TCP 3389 falhará. Os NSGs são aplicados em ambos os Olá NIC *VM1 NIC1* e Olá sub-rede *Subnet1*. TooTCP porta 3389 do tráfego é permitida em Olá associado à interface de rede de saudação do NSG *VM1 NIC1*, no entanto, porta 3389 ocorre uma falha da tooVM1 ping do TCP.

Embora este exemplo usa a porta TCP 3389, Olá seguintes etapas pode ser usada toodetermine falhas de conexão de entrada e saída em qualquer porta.

### <a name="vm"></a>Exibir regras de segurança em vigor para uma máquina virtual
Concluir Olá seguindo as etapas tootroubleshoot NSGs para uma VM:

Você pode exibir a lista completa de regras de segurança efetiva de saudação em uma NIC, de saudação própria máquina virtual. Você também pode adicionar, modificar e excluir as regras NSG NIC e de sub-rede da folha de regras efetivo hello, se você tiver permissões tooperform essas operações.

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **máquinas virtuais** na lista de saudação que aparece.
3. Selecione tootroubleshoot uma VM na lista de saudação que é exibido e uma folha VM com opções é exibida.
4. Clique em **Diagnosticar e resolver problemas** e selecione um problema comum. Neste exemplo, **toomy VM do Windows não consigo conectar** está selecionado. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Etapas aparecem em problema hello, conforme mostrado na figura abaixo de saudação: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Clique em *regras de grupo de segurança efetiva* na lista de saudação de etapas recomendadas.
6. Olá **obter regras de segurança efetiva** folha é exibida, conforme mostrado na figura abaixo de saudação:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Observe Olá seções de imagem Olá a seguir:
   
   * **Escopo:** definido muito*VM1*, Olá VM selecionado na etapa 3.
   * **Adaptador de rede:** *VM1-NIC1* foi selecionado. Uma VM pode ter vários adaptadores de rede (NIC). Cada NIC pode ter regras de segurança em vigor únicas. Ao solucionar problemas, regras de segurança efetiva Olá tooview talvez seja necessário para cada NIC.
   * **Os NSGs associados:** NSGs podem ser aplicado tooboth Olá NIC e hello sub-rede Olá NIC está conectada ao. Figura hello, um NSG foi aplicada tooboth Olá NIC e hello subrede a que ele está conectado. Você pode clicar nos nomes NSG Olá toodirectly modificar as regras em Olá NSGs.
   * **Guia VM1 nsg:** lista Olá das regras exibidas na imagem de saudação é para Olá NSG aplicado NIC toohello. Várias regras padrão são criadas pelo Azure sempre que um NSG é criado. Não é possível remover as regras padrão hello, mas você pode substituí-los com as regras de prioridade mais alta. toolearn mais sobre as regras padrão, ler Olá [visão geral do NSG](virtual-networks-nsg.md#default-rules) artigo.
   * **Coluna de destino:** algumas regras Olá com texto na coluna hello, enquanto outros têm prefixos de endereço. texto de saudação é o nome de saudação de regra de segurança padrão marcas aplicadas toohello quando ele foi criado. marcas de saudação são identificadores fornecidos pelo sistema que representam vários prefixos. Selecionar uma regra com uma marca, como *AllowInternetOutBound*, lista de prefixos de Olá Olá **prefixos de endereço** folha.
   * **Download:** lista Olá de regras pode ser longa. Você pode baixar um arquivo. csv de regras de saudação para análise offline clicando **baixar** e salvar arquivo hello.
   * **AllowRDP** regra de entrada: essa regra permite que o RDP conexões toohello VM.
7. Clique em Olá **Subnet1 NSG** guia tooview Olá efetivo regras Olá NSG aplicado sub-rede toohello, conforme mostrado na figura abaixo de saudação: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Saudação de aviso *denyRDP* **entrada** regra. Aplicado na sub-rede Olá as regras de entrada são avaliadas antes das regras aplicadas na interface de rede de saudação. Como Olá negar regra será aplicada na sub-rede Olá, Olá solicitação tooconnect tooTCP 3389 falha, porque Olá permitem que a regra no hello NIC nunca é calculada. 
   
    Olá *denyRDP* regra é motivo Olá por Olá conexão de RDP está falhando. Removendo deve resolver o problema de saudação.
   
   > [!NOTE]
   > Se Olá VM associados com hello NIC não está em um estado de execução, ou os NSGs ainda não foram aplicado toohello NIC ou sub-rede, nenhuma regra será mostrada.
   > 
   > 
8. regras do NSG tooedit, clique em *Subnet1 NSG* em Olá **NSGs associado** seção.
   Isso abre o hello **Subnet1 NSG** folha. Você pode editar diretamente regras Olá clicando em **regras de segurança de entrada**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Depois de remover Olá *denyRDP* Olá da regra de entrada **Subnet1 NSG** e adicionando um *allowRDP* regra, a lista de regras efetivo Olá aparência Olá figura abaixo:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Confirme que a porta TCP 3389 esteja aberta abrindo uma conexão de RDP toohello VM ou usando a ferramenta de PsPing hello. Você pode aprender mais sobre PsPing ao ler Olá [página de download do PsPing](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Exibir regras de segurança em vigor para um adaptador de rede
Se o fluxo de tráfego VM é afetado para uma NIC específica, você pode exibir uma lista completa de regras efetivo Olá Olá NIC do contexto de interfaces de rede Olá Concluindo Olá etapas a seguir:

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **interfaces de rede** na lista de saudação que aparece.
3. Selecione um adaptador de rede. Olá a imagem a seguir, uma NIC denominado *NIC1 VM1* é selecionado.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Observe que Olá **escopo** é definido toohello interface de rede selecionada. Saiba mais sobre toolearn Olá informações adicionais mostradas, ler etapa 6 do hello **NSGs solucionar problemas de uma VM** deste artigo.
   
   > [!NOTE]
   > Se um NSG é removido de uma interface de rede, Olá sub-rede NSG é ainda em vigor em Olá fornecido NIC. Nesse caso, saída de hello só mostra regras de sub-rede Olá NSG. Regras somente aparecerão se Olá NIC é anexado tooa VM.
   > 
   > 
4. Você pode editar diretamente as regras para NSGs associados a uma NIC e a uma sub-rede. toolearn como, leia a etapa 8 de saudação **exibir regras de segurança efetiva para uma máquina virtual** deste artigo.

## <a name="nsg"></a>Exibir regras de segurança em vigor para um NSG (grupo de segurança de rede)
Ao modificar as regras NSG, talvez você queira tooreview impacto de saudação de regras de saudação que está sendo adicionado em uma VM específica. Você pode exibir uma lista completa das regras de segurança efetiva Olá para todos os Olá NICs que um determinado NSG é aplicado, sem ter que tooswitch o contexto da saudação dada folha NSG. tootroubleshoot regras efetivo dentro de um NSG, Olá concluir as etapas a seguir:

1. Logon toohello portal do Azure em https://portal.azure.com.
2. Clique em **mais serviços**, em seguida, clique em **grupos de segurança de rede** na lista de saudação que aparece.
3. Selecione um NSG. Na figura abaixo de Olá, um NSG denominado VM1 nsg foi selecionado.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Observe Olá seções da imagem anterior Olá a seguir:
   
   * **Escopo:** definir toohello NSG selecionado.
   * **Máquina virtual:** quando um NSG sub-rede tooa aplicadas, é aplicada tooall interfaces tooall anexado VMs toohello conectado sub-rede. Esta lista mostra todas as VMs às quais este NSG foi aplicado. Você pode selecionar qualquer VM na lista de saudação.
     
     > [!NOTE]
     > Se um NSG está tooonly aplicada uma sub-rede vazia, máquinas virtuais não serão listados. Se um NSG é aplicado tooa NIC que não está associado uma VM, as NICs também não serão listadas. 
     > 
     > 
   * **Adaptador de rede:** uma VM pode ter vários adaptadores de rede. Você pode selecionar uma interface de rede conectado toohello selecionado de VM.
   * **AssociatedNSGs:** a qualquer momento, um NIC pode ter até tootwo efetivos NSGs, um aplicado toohello NIC e Olá toohello as outras sub-redes. Embora o escopo de saudação for selecionado como VM1-nsg se Olá NIC tem uma sub-rede efetivada NSG, saída de hello mostrará dois NSGs.
4. Você pode editar diretamente as regras para NSGs associados a uma NIC ou a uma sub-rede. toolearn como, leia a etapa 8 de saudação **exibir regras de segurança efetiva para uma máquina virtual** deste artigo.

Saiba mais sobre toolearn Olá informações adicionais mostradas, ler etapa 6 do hello **exibir regras de segurança efetiva para uma máquina virtual** deste artigo.

> [!NOTE]
> Embora uma sub-rede e a NIC podem ter toothem de apenas um NSG aplicada, um NSG pode ser associado toomultiple NICs e várias sub-redes.
> 
> 

## <a name="considerations"></a>Considerações
Considere Olá pontos a seguir ao solucionar problemas de conectividade:

* As regras NSG padrão bloqueará o acesso de entrada de saudação à internet e permitir VNet o tráfego de entrada. As regras devem ser adicionadas explicitamente tooallow acesso de entrada da Internet, conforme necessário.
* Se não houver nenhuma regra de segurança NSG causando toofail de conectividade de rede da VM, problema de saudação pode ser devido a:
  * Software de firewall em execução no sistema operacional da VM Olá
  * Rotas configuradas para soluções de virtualização ou tráfego local. Tráfego de Internet pode ser redirecionado tooon local por meio de túnel forçado. Uma conexão de RDP/SSH de saudação Internet tooyour VM pode não funcionar com essa configuração, dependendo de como o hardware de rede local Olá lida com esse tráfego. Saudação de leitura [rotas de solução de problemas](virtual-network-routes-troubleshoot-powershell.md) artigo toolearn como toodiagnose encaminhar os problemas que podem estar impedindo Olá fluxo do tráfego do hello VM. 
* Se você tiver emparelhadas VNets, por padrão, Olá marca VIRTUAL_NETWORK expandirá automaticamente tooinclude prefixos para emparelhadas VNets. Você pode exibir esses prefixos no hello **ExpandedAddressPrefix** listar, tootroubleshoot qualquer tooVNet relacionados problemas emparelhamento de conectividade. 
* Regras de segurança efetiva são mostradas apenas se houver que um NSG associado da VM Olá NIC e ou uma sub-rede. 
* Se não há nenhum NSGs associados Olá NIC ou sub-rede e tiver um endereço IP público atribuído tooyour VM, todas as portas será abertas para acesso de entrada e saído. Se Olá VM tem um endereço IP público, aplicar os NSGs toohello NIC ou sub-rede é recomendável.

