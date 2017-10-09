Há vários motivos quando você não pode iniciar ou conectar tooan aplicativo em execução em uma máquina virtual do Azure (VM). Motivos incluem o aplicativo hello não está em execução ou escutando nas portas Olá esperado, Olá escutando na porta bloqueada ou as regras não corretamente passando o aplicativo de toohello de tráfego de rede. Este artigo descreve uma abordagem metódica toofind e um problema de saudação correto.

Se você estiver tendo problemas para se conectar tooyour VM usando o RDP ou SSH, consulte um dos seguintes Olá artigos primeiro:

* [Solucionar problemas de conexões de área de trabalho remota tooa baseados no Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Solucionar problemas de Secure Shell (SSH) conexões tooa baseados em Linux máquina virtual do Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../articles/resource-manager-deployment-model.md). Este artigo aborda o uso de ambos os modelos, mas a Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.

## <a name="quick-start-troubleshooting-steps"></a>Etapas de solução de problemas de início rápido
Se você tiver problemas para se conectar a aplicativos de tooan, tente Olá etapas de solução de problemas gerais a seguir. Depois de cada etapa, tente conectar aplicativo tooyour novamente:

* Reiniciar a máquina virtual de saudação
* Recrie o ponto de extremidade Olá / regras de firewall / regras de grupo (NSG) de segurança de rede
  * [Modelo do Resource Manager: gerenciar Grupos de Segurança de Rede](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Modelo clássico: gerenciar pontos de extremidade dos Serviços de Nuvem](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Conectar-se de um local diferente, como uma rede virtual do Azure diferente
* Reimplantar a máquina virtual de saudação
  * [Reimplantar VM do Windows](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Reimplantar VM Linux](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Recriar a máquina virtual de saudação

Para obter mais informações, consulte [Solução de problemas de conectividade de ponto de extremidade (RDP/SSH/HTTP, falhas etc.)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Visão geral detalhada da solução de problemas
Há quatro áreas principais de acesso de saudação tootroubleshoot de um aplicativo que está sendo executado em uma máquina virtual do Azure.

![solucionar o problema de incapacidade de iniciar o aplicativo](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. aplicativo Hello em execução no hello máquina virtual do Azure.
   * Aplicativo hello em si está sendo executado corretamente?
2. Olá máquina virtual do Azure.
   * Olá própria máquina virtual está sendo executado corretamente e respondendo toorequests?
3. Pontos de extremidade de rede do Azure.
   * Pontos de extremidade de serviço para máquinas virtuais no modelo de implantação clássico Olá na nuvem.
   * Grupos de segurança de rede e regras NAT de entrada para máquinas virtuais no modelo de implantação do Resource Manager.
   * Fluxo de usuários toohello VM/aplicativo em portas Olá esperado de tráfego pode?
4. Seu dispositivo de borda da Internet.
   * As regras de firewall estão impedindo o tráfego de fluir corretamente?

Para computadores cliente que estão acessando o aplicativo hello através de uma conexão de rota expressa ou VPN site a site, áreas principais de saudação que podem causar problemas são aplicativo hello e Olá a máquina virtual do Azure.

origem de saudação toodetermine de problema de saudação e sua correção, siga estas etapas.

## <a name="step-1-access-application-from-target-vm"></a>Etapa 1: Acessar o aplicativo da VM de destino
Tente tooaccess Olá aplicativo com o programa do cliente apropriado Olá Olá VM na qual ele está em execução. Use o nome de host local hello, endereço IP local de saudação ou endereço de loopback (127.0.0.1) do hello.

![Iniciar o aplicativo diretamente da saudação VM](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Por exemplo, se o aplicativo hello é um servidor web, abra um navegador no hello VM e tente tooaccess uma página da web hospedado em Olá VM.

Se você pode acessar o aplicativo hello, vá muito[etapa 2](#step2).

Se você não pode acessar o aplicativo hello, verifique se Olá configurações a seguir:

* aplicativo Hello está em execução na máquina de virtual de destino hello.
* aplicativo Hello está escutando nas portas TCP e UDP Olá esperado.

No Windows e máquinas virtuais baseadas em Linux, use Olá **netstat - a** comando tooshow Olá portas de escuta ativas. Examine a saída Olá para portas Olá esperado no qual seu aplicativo deve estar escutando. Reiniciar o aplicativo hello ou configurar portas de saudação esperada toouse conforme necessário e tente novamente o aplicativo localmente do tooaccess hello.

## <a id="step2"></a>Etapa 2: Acessar o aplicativo de outra VM em Olá mesma rede virtual
Tente o aplicativo de hello tooaccess de uma VM diferente, mas em Olá mesmo rede virtual, usando o nome do host da VM hello ou seu endereço IP público, privado ou provedor do Azure atribuída. Para máquinas virtuais criadas usando o modelo de implantação clássico hello, não use o endereço IP público de Olá Olá do serviço de nuvem.

![Iniciar o aplicativo de uma VM diferente](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Por exemplo, se o aplicativo hello é um servidor web, tente tooaccess uma página da web em um navegador em uma máquina virtual diferente no hello mesma rede virtual.

Se você pode acessar o aplicativo hello, vá muito[etapa 3](#step3).

Se você não pode acessar o aplicativo hello, verifique se Olá configurações a seguir:

* firewall de host de saudação na VM de destino Olá esteja permitindo o tráfego de saída de resposta e solicitação de entrada hello.
* Detecção de intrusão ou software em execução na VM de destino de saudação de monitoramento de rede esteja permitindo o tráfego de saudação.
* Pontos de extremidade de serviços de nuvem ou grupos de segurança de rede são permitindo o tráfego de saudação:
  * [Modelo clássico: gerenciar pontos de extremidade dos Serviços de Nuvem](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Modelo do Resource Manager: gerenciar Grupos de Segurança de Rede](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Um componente separado em execução em sua VM no caminho de saudação entre teste Olá sua VM, como um firewall, ou um balanceador de carga e a VM esteja permitindo o tráfego de saudação.

Em uma máquina virtual baseados no Windows, use o Firewall do Windows com segurança avançada toodetermine se as regras de firewall Olá excluir o tráfego de entrada e saída do seu aplicativo.

## <a id="step3"></a>Etapa 3: Acessar o aplicativo de rede virtual externa de saudação
Tente o aplicativo hello de tooaccess de um computador fora da rede virtual hello como Olá VM que está executando o aplicativo hello. Use uma rede diferente do computador cliente original.

![Iniciar o aplicativo em um computador fora da rede virtual Olá](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Por exemplo, se o aplicativo hello é um servidor web, tente tooaccess Olá web página em um navegador em execução em um computador que não está na rede virtual hello.

Se você não pode acessar o aplicativo hello, verifique se Olá configurações a seguir:

* Máquinas virtuais criadas usando o modelo de implantação clássico hello:
  
  * Verifique se essa configuração de ponto de extremidade Olá para Olá que VM esteja permitindo o tráfego de entrada de hello, especialmente o protocolo de saudação (TCP ou UDP) e números de porta pública e privada Olá.
  * Verifique se que listas de controle de acesso (ACLs) no ponto de extremidade de saudação não estão impedindo o tráfego de entrada de saudação à Internet.
  * Para obter mais informações, consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Máquinas virtuais criadas usando o modelo de implantação do Gerenciador de recursos de saudação:
  
  * Verifique se que Olá entrada configuração de regra NAT para Olá que VM esteja permitindo o tráfego de entrada de hello, especialmente o protocolo de saudação (TCP ou UDP) e números de porta pública e privada Olá.
  * Verifique se que os grupos de segurança de rede está permitindo que a solicitação de entrada hello e tráfego de resposta de saída.
  * Para obter mais informações, consulte [O que é um NSG (Grupo de Segurança de Rede)?](../articles/virtual-network/virtual-networks-nsg.md)

Se a máquina virtual de saudação ou ponto de extremidade é um membro de um conjunto com balanceamento de carga:

* Verifique se o protocolo de investigação da saudação (TCP ou UDP) e o número da porta estão corretos.
* Se o teste de saudação protocolo e porta é diferente de porta e protocolo do conjunto de balanceamento de carga de saudação:
  * Verificar se o aplicativo hello está escutando no protocolo de investigação da saudação (TCP ou UDP) e o número da porta (use **netstat – a** em Olá VM de destino).
  * Verifique se o firewall Olá host no destino Olá VM está permitindo que a solicitação de entrada de investigação de saudação e tráfego de resposta de investigação de saída.

Se você pode acessar o aplicativo hello, certifique-se de que esteja permitindo o seu dispositivo de borda da Internet:

* tráfego de solicitações de saída do aplicativo de saudação do seu computador de cliente toohello máquina virtual do Azure.
* Olá tráfego de resposta do aplicativo de entrada da saudação máquina virtual do Azure.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Etapa 4, se você não pode acessar o aplicativo hello, usar IP verificar toocheck Olá configurações. 

Para saber mais, veja [Visão geral do monitoramento de rede do Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Recursos adicionais
[Solucionar problemas de conexões de área de trabalho remota tooa baseados no Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Solucionar problemas de Secure Shell (SSH) conexões tooa baseados em Linux máquina virtual do Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

