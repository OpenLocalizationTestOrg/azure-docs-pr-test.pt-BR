Se você estiver tendo problemas para se conectar a máquina virtual de tooa sobre sua conexão VPN, verifique o seguinte hello:

- Verifique se a conexão VPN é estabelecida.
- Verifique se você estiver se conectando a endereço IP privado de toohello para Olá VM.
- Se você puder se conectar toohello VM usando IP privado Olá endereço, mas não Olá nome do computador, verifique se você configurou o DNS corretamente. Para obter mais informações sobre como funciona a resolução de nome para VMs, confira [Resolução de nomes para VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Quando você se conectam via ponto a Site, verifique Olá itens adicionais a seguir:

- Use 'ipconfig' toocheck Olá endereço IPv4 atribuído toohello adaptador de Ethernet no computador de saudação do qual você está se conectando. Se o endereço IP de saudação estiver dentro do intervalo de endereços de saudação do hello VNet que você está se conectando ou dentro do intervalo de endereços de saudação do seu VPNClientAddressPool, isso é chamado tooas um espaço de endereço sobrepostos. Quando seu espaço de endereço se sobrepõe dessa forma, o tráfego de rede Olá não atinge o Azure, ela permanece na rede local Olá.
- Verifique se que esse pacote de configuração de cliente VPN Olá foi gerado depois de endereços IP do servidor DNS Olá foram especificados para Olá VNet. Se você atualizou os endereços IP do servidor DNS hello, gerar e instalar um novo pacote de configuração de cliente VPN.

Para obter mais informações sobre como solucionar problemas de uma conexão de RDP, consulte [tooa de conexões de área de trabalho remota solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
