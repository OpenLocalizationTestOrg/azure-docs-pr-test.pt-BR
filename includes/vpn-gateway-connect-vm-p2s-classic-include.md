Você pode conectar tooa VM é implantada tooyour VNet, criando um VM do tooyour de Conexão de área de trabalho remota. Hello tooinitially de maneira recomendada verificar se você pode se conectar tooyour VM é tooconnect por usando seu IP privado de endereços, em vez do nome do computador. Dessa forma, você está testando toosee se você puder se conectar, não se a resolução de nomes está configurada corretamente. 

1. Localize o endereço IP privado de saudação para sua VM. Você encontrará o endereço IP privado de saudação de uma VM examinando o hello propriedades para a VM no portal do Azure de saudação do hello, ou usando o PowerShell.
2. Verifique se você está conectado tooyour VNet usando Olá ponto a Site VPN conexão. 
3. Abrir Conexão de área de trabalho remota, digitando "RDP" ou "Conexão de área de trabalho remota" na caixa de pesquisa de saudação na barra de tarefas de saudação, selecione a Conexão de área de trabalho remota. Você também pode abrir a Conexão de área de trabalho remota usando o comando de 'mstsc' hello no PowerShell. 
3. Na Conexão de área de trabalho remota, insira o endereço IP privado de saudação do hello VM. Você pode em configurações adicionais de tooadjust "Mostrar opções", e se conectar.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot uma conexão de RDP tooa VM

Se você estiver tendo problemas para se conectar a máquina virtual de tooa sobre sua conexão VPN, há algumas coisas que você pode verificar. Para obter mais informações sobre solução de problemas, consulte [tooa de conexões de área de trabalho remota solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Verifique se a conexão VPN é estabelecida.
- Verifique se você estiver se conectando a endereço IP privado de toohello para Olá VM.
- Use 'ipconfig' toocheck Olá endereço IPv4 atribuído toohello adaptador de Ethernet no computador de saudação do qual você está se conectando. Se o endereço IP de saudação estiver dentro do intervalo de endereços de saudação do hello VNet que você está se conectando ou dentro do intervalo de endereços de saudação do seu VPNClientAddressPool, isso é chamado tooas um espaço de endereço sobrepostos. Quando seu espaço de endereço se sobrepõe dessa forma, o tráfego de rede Olá não atinge o Azure, ela permanece na rede local Olá.
- Se você puder se conectar toohello VM usando IP privado Olá endereço, mas não Olá nome do computador, verifique se você configurou o DNS corretamente. Para obter mais informações sobre como funciona a resolução de nome para VMs, confira [Resolução de nomes para VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Verifique se que esse pacote de configuração de cliente VPN Olá foi gerado depois de endereços IP do servidor DNS Olá foram especificados para Olá VNet. Se você atualizou os endereços IP do servidor DNS hello, gerar e instalar um novo pacote de configuração de cliente VPN.
