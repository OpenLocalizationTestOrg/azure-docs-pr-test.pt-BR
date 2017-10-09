Abrir uma porta, ou criar um ponto de extremidade, tooa máquina virtual (VM) no Azure, criando um filtro de rede em uma sub-rede ou interface de rede VM. Você pode colocar esses filtros, que controlam o tráfego de entrada e saído, em um recurso de toohello do grupo de segurança de rede conectados que recebe o tráfego de saudação.

Vamos usar um exemplo comum de tráfego da Web na porta 80. Uma vez que uma VM que está configurado tooserve de solicitações da web saudação padrão a porta 80 TCP (Lembre-se os serviços apropriados toostart hello e abra as regras de firewall do sistema operacional em Olá VM), você:

1. Criará um Grupo de Segurança de Rede.
2. Criará uma regra de entrada permitindo o tráfego com:
   * intervalo de portas de destino Hello "80"
   * Olá intervalo de porta de origem "*" (permitindo que qualquer porta de origem)
   * um valor de prioridade menor 65.500 (toobe maior prioridade do que o padrão pega-tudo hello negar regra de entrada)
3. Olá associar o grupo de segurança de rede com interface de rede VM hello ou sub-rede.

Você pode criar redes complexas configurações toosecure seu ambiente usando regras e grupos de segurança de rede. Nosso exemplo usa apenas uma ou duas regras que permitem o tráfego HTTP ou gerenciamento remoto. Para obter mais informações, consulte o seguinte Olá ['Mais informações'](#more-information-on-network-security-groups) seção ou [o que é um grupo de segurança de rede?](../articles/virtual-network/virtual-networks-nsg.md)

