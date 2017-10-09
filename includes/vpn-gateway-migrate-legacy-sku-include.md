> [!NOTE]
> * gateway VPN Olá endereço IP público será alterado ao migrar de um antigo tooa SKU SKU de novo.
> * Você não pode migrar clássico toohello de gateways VPN SKUs de novo. Clássico VPN gateways pode apenas usar Olá herdados SKUs (antigos).
> 

Você não pode redimensionar a VPN do Azure entre Olá SKUs antigos e gateways Olá novas famílias SKU. Se você tiver gateways de VPN no modelo de implantação do Gerenciador de recursos de saudação que estão usando a versão mais antiga de saudação do hello SKUs, você pode migrar toohello SKUs de novo. toomigrate, exclua o gateway VPN existente de saudação para sua rede virtual, e criar um novo.

Fluxo de trabalho de migração:

1. Remova qualquer gateway de rede virtual toohello conexões.
2. Exclua gateway de VPN Olá antigo.
3. Crie novo gateway VPN hello.
4. Atualize os dispositivos VPN local com hello novo VPN endereço IP do gateway (para conexões Site a Site).
5. Atualize o valor do endereço IP hello gateway para gateways de rede local VNet para VNet que se conectam toothis gateway.
6. Baixe novos pacotes de configuração do cliente VPN para clientes de P2S conexão de rede virtual toohello por meio deste gateway VPN.
7. Recrie o gateway de rede virtual Olá conexões toohello.
