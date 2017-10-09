

Existem dois níveis de balanceamento de carga para serviços de infraestrutura do Azure:

* **Nível de DNS**: balanceamento de carga para serviços de nuvem do tráfego toodifferent localizados em diferentes dados centers, toodifferent sites do Azure localizados em data centers diferentes ou tooexternal pontos de extremidade. Isso é feito com o Azure Traffic Manager e o método de balanceamento de carga de saudação Round Robin.
* **Nível de rede**: de entrada da Internet tráfego toodifferent máquinas virtuais de um serviço de nuvem de balanceamento de carga ou o balanceamento do tráfego entre máquinas virtuais em um serviço de nuvem ou rede virtual de carga. Isso é feito com o balanceador de carga do Azure hello.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Balanceamento de carga do Gerenciador de Tráfego para serviços de nuvem e sites
Traffic Manager permite distribuição Olá toocontrol tooendpoints de tráfego do usuário, que pode incluir serviços de nuvem, sites, sites externos e outros perfis do Gerenciador de tráfego. O Traffic Manager funciona aplicando um consultas do sistema de nomes (DNS) de tooDomain do mecanismo de política inteligente Olá nomes de domínio dos recursos de Internet. Os serviços de nuvem ou sites podem ser executados em diferentes datacenters no Olá, mundo.

Você deve usar REST ou o Windows PowerShell tooconfigure pontos de extremidade externos ou perfis do Gerenciador de tráfego como pontos de extremidade.

O Traffic Manager usa três balanceamento de carga de tráfego de toodistribute métodos:

* **Failover**: Use este método quando você deseja toouse um ponto de extremidade primário para todo o tráfego, mas fornece backups caso Olá primário fica indisponível.
* **Desempenho**: Use este método quando tiver pontos de extremidade em diferentes locais geográficos e desejar solicitar clientes toouse hello "mais próximo" ponto de extremidade em termos de latência mais baixa hello.
* **Round Robin:** usar esse método quando desejar que os serviços de carga toodistribute em um conjunto de nuvem no hello mesmo datacenter ou em serviços de nuvem ou sites em data centers diferentes.

Para obter mais informações, consulte [Sobre métodos de balanceamento de carga do Gerenciador de Tráfego](../articles/traffic-manager/traffic-manager-routing-methods.md).

Olá diagrama a seguir mostra um exemplo de hello método de balanceamento de carga Round Robin para distribuir tráfego entre os diferentes serviços de nuvem.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

processo básico de saudação é seguir hello:

1. Um cliente da Internet consulta um serviço de web domínio nome correspondente tooa.
2. DNS encaminha Olá nome consulta solicitação tooTraffic Manager.
3. Gerenciador de tráfego escolhe Olá próximo serviço de nuvem no hello lista Round Robin e envia de volta Olá nome DNS. servidor DNS do cliente de Internet Olá resolve o endereço IP do hello nome tooan e envia toohello cliente da Internet.
4. Olá Internet se conecta ao serviço de nuvem Olá escolhido pelo Gerenciador de tráfego.

Para obter mais informações, consulte [Gerenciador de Tráfego](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Balanceamento de carga do Azure para máquinas virtuais
Olá de máquinas virtuais no mesmo serviço de nuvem ou rede virtual pode se comunicar entre si diretamente usando seus endereços IP privados. Computadores e serviços fora Olá serviço de nuvem ou rede virtual só pode se comunicar com máquinas virtuais em um serviço de nuvem ou rede virtual com um ponto de extremidade configurado. Um ponto de extremidade é um mapeamento de um endereço IP público e a porta toothat endereço IP e porta de uma máquina virtual ou a função da web em um serviço de nuvem do Azure.

Olá balanceador de carga do Azure distribui aleatoriamente um tipo específico de tráfego de entrada em várias máquinas virtuais ou serviços em uma configuração conhecida como um conjunto com balanceamento de carga. Por exemplo, você pode distribuir a carga de saudação do tráfego de solicitação da web em vários servidores web ou funções da web.

Olá diagrama a seguir mostra um ponto de extremidade com balanceamento de carga para tráfego web (sem criptografia) padrão que é compartilhado entre três máquinas virtuais para Olá pública e privada a porta TCP 80. Essas três máquinas virtuais estão em um conjunto de balanceamento de carga.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Para obter mais informações, consulte [Balanceador de carga do Azure](../articles/load-balancer/load-balancer-overview.md). Para as etapas de saudação toocreate um conjunto com balanceamento de carga, consulte [configurar um conjunto com balanceamento de carga](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

O Azure também pode balancear a carga dentro de um serviço de nuvem ou rede virtual. Isso é conhecido como balanceamento de carga interno e pode ser usado em Olá maneiras a seguir:

* Saldo de tooload entre servidores em diferentes camadas de um aplicativo de várias camada (por exemplo, entre as camadas web e o banco de dados).
* tooload saldo linha de negócios (LOB) aplicativos hospedados no Azure sem a necessidade de software ou hardware de Balanceador de carga adicional.
* tooinclude servidores locais no conjunto de saudação de computadores cujo tráfego tem a carga balanceada.

Semelhante tooAzure balanceamento de carga e balanceamento de carga interno é facilitada pela configuração de um conjunto de balanceamento de carga interno.

Olá diagrama a seguir mostra um exemplo de um ponto de extremidade com balanceamento de carga interno para um aplicativo de linha de negócios (LOB) que é compartilhado entre três máquinas virtuais em uma rede virtual entre locais.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Considerações do Balanceador de carga
Um balanceador de carga é configurado por padrão tootimeout uma sessão ociosa em 4 minutos. Se seu aplicativo por trás de um balanceador de carga deixa uma conexão ociosa por mais de 4 minutos, e ele não tem uma configuração de Keep-Alive, conexão hello será removida. Você pode alterar tooallow de comportamento de Balanceador de carga Olá um [mais configuração de tempo limite para o balanceador de carga do Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Outra consideração é o tipo de saudação do modo de distribuição com suporte pelo Balanceador de carga do Azure. Você pode configurar a afinidade de IP de origem (IP de origem, IP de destino) ou o protocolo de IP de origem (IP de origem, IP de destino e protocolo). Confira [Azure Load Balancer distribution mode (source IP affinity)](../articles/load-balancer/load-balancer-distribution-mode.md) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas
Para as etapas de saudação toocreate um conjunto com balanceamento de carga, consulte [configurar um conjunto de balanceamento de carga interno](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Para obter mais informações sobre o balanceador de carga, confira [Balanceamento de carga interno](../articles/load-balancer/load-balancer-internal-overview.md).

