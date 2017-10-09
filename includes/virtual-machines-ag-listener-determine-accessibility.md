É importante toorealize que há dois tooconfigure de maneiras um ouvinte de grupo de disponibilidade no Azure. Olá maneiras diferem no tipo de saudação do balanceador de carga do Azure que você usar ao criar o ouvinte de saudação. Olá, a tabela a seguir descreve as diferenças de saudação:

| Tipo de balanceador de carga | Implementação | Use quando: |
| --- | --- | --- |
| **Externo** |Olá usa *endereço IP virtual público* saudação do serviço de nuvem que hospeda máquinas virtuais de saudação (VMs). |Você precisa de ouvinte de saudação tooaccess de rede virtual do hello fora, inclusive de saudação à Internet. |
| **Interna** |Usa um *balanceador de carga interno* com um endereço privado para o ouvinte de saudação. |Você pode acessar o ouvinte Olá somente de dentro de saudação mesma rede virtual. Esse acesso inclui VPN site a site em cenários híbridos. |

> [!IMPORTANT]
> Para um ouvinte que Olá de usos VIP público do serviço de nuvem Olá (balanceador externo de carga), contanto que o cliente hello, ouvinte e bancos de dados estão na mesma região do Azure, você não incorrerá em encargos de saída. Caso contrário, nenhum dado retornado por meio de saudação ouvinte é considerado a saída, e são cobrados em taxas de transferência de dados normal. 
> 
> 

Um ILB pode ser configurado somente em redes virtuais com um escopo regional. Redes virtuais existentes configuradas para um grupo de afinidades não podem usar um ILB. Para obter mais informações, consulte [Visão geral do balanceador de carga interno](../articles/load-balancer/load-balancer-internal-overview.md).

