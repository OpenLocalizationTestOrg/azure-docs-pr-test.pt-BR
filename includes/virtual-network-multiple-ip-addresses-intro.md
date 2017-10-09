> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Modelo](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Uma máquina Virtual (VM) do Azure tem um ou mais interfaces de rede (NIC) anexado tooit. Uma NIC pode ter um ou mais estático ou dinâmico IP pública e privada endereços tooit atribuído. A atribuição de IP vários endereços tooa VM habilita Olá recursos a seguir:

* Hospede vários sites ou serviços com diferentes endereços IP e os certificados SSL em um único servidor.
* Funcione como um dispositivo virtual de rede, como um firewall ou balanceador de carga.
* Olá capacidade tooadd qualquer IP privado Olá endereços para qualquer Olá NICs tooan pool de back-end do balanceador de carga do Azure. Olá após Olá apenas um endereço IP primário Olá que NIC primário pode ser adicionados tooa pool de back-end. toolearn mais sobre como tooload equilibrar várias configurações de IP, ler Olá [várias configurações de IP de balanceamento de carga](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.

Cada tooa NIC conectada VM tem um ou mais configurações de IP associado tooit. Cada configuração recebe um endereço IP privado estático ou dinâmico. Cada configuração também pode ter um tooit de recurso associado de endereço IP público. Um recurso de endereço IP público tem qualquer um dinâmico ou estático público IP endereço atribuído tooit. toolearn mais sobre IP endereços no Azure, leia Olá [endereços IP no Azure](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) artigo. 

Há um limite toohow IP privado muitos endereços podem ser atribuídos a NIC tooa. Também há um limite toohow vários endereços IP públicos que podem ser usados em uma assinatura do Azure. Consulte Olá [Azure limita](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo para obter detalhes.
