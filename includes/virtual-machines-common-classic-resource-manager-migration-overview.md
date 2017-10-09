# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Suporte de plataforma de migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos
Neste artigo, descreveremos como habilitamos a migração da infraestrutura como um recurso de serviço (IaaS) de modelos de implantação do hello clássico tooResource Manager. Você pode ler mais sobre os [recursos e benefícios do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). Nós de detalhe como recursos de tooconnect de saudação dois modelos de implantação que coexistem em sua assinatura usando o virtual rede gateways site a site.

## <a name="goal-for-migration"></a>Meta de migração
O Gerenciador de Recursos possibilita implantar aplicativos complexos por meio de modelos, configurar máquinas virtuais usando extensões de VM e incorporar o gerenciamento de acesso e a marcação. O Azure Resource Manager inclui implantação paralela e escalonável para máquinas virtuais em conjuntos de disponibilidade. novo modelo de implantação Olá também fornece gerenciamento de ciclo de vida de computação, rede e armazenamento independentemente. Por fim, há um foco sobre como habilitar a segurança por padrão com a imposição de saudação de máquinas virtuais em uma rede virtual.

Quase todos os recursos de saudação do modelo de implantação clássico Olá têm suporte para computação, rede e armazenamento no Gerenciador de recursos do Azure. toobenefit de novos recursos de saudação no Gerenciador de recursos do Azure, você pode migrar existente implantações do modelo de implantação clássico hello.

## <a name="supported-resources-for-migration"></a>Recursos com suporte para migração
Esses recursos de IaaS clássicos têm suporte durante a migração

* Máquinas Virtuais
* Conjuntos de Disponibilidade
* Serviços de Nuvem
* Contas de armazenamento
* Redes Virtuais
* Gateways VPN
* Express Gateways de rota _(no hello mesma assinatura que a rede Virtual somente)_
* Grupos de segurança de rede 
* Tabelas de Rotas 
* IPs Reservados 

## <a name="supported-scopes-of-migration"></a>Escopos de migração com suporte
Há maneiras diferentes de 4 toocomplete de migração de recursos de computação, rede e armazenamento. Estas são 

* Migração de máquinas virtuais (NÃO em uma rede virtual)
* Migração de máquinas virtuais (em uma rede virtual)
* Migração das contas de armazenamento
* Recursos desanexados (Grupos de Segurança de Rede, Tabelas de Rotas e IPs Reservados)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migração de máquinas virtuais (NÃO em uma rede virtual)
No modelo de implantação do Gerenciador de recursos de saudação, a segurança é imposta para seus aplicativos por padrão. Todas as VMs precisam toobe em uma rede virtual no modelo do Gerenciador de recursos de saudação. Olá reinicializações da plataforma Windows Azure (`Stop`, `Deallocate`, e `Start`) Olá VMs como parte da migração de saudação. Você tem duas opções para as redes virtuais Olá Olá máquinas virtuais serão migradas para:

* Você pode solicitar Olá plataforma toocreate uma nova rede virtual e migrar a máquina virtual de saudação na nova rede virtual de saudação.
* Você pode migrar uma máquina virtual de saudação em uma rede virtual existente no Gerenciador de recursos.

> [!NOTE]
> Nesse escopo de migração, ambos Olá operações do plano de gerenciamento e operações do plano de dados Olá podem não estar disponíveis para um período de tempo durante a migração de saudação.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migração de máquinas virtuais (em uma rede virtual)
Para a maioria das configurações de VM, apenas os metadados de saudação está migrando entre modelos de implantação clássico e o Gerenciador de recursos de saudação. Olá subjacentes VMs estão sendo executadas em Olá mesmo hardware Olá mesma rede e com hello mesmo armazenamento. operações do plano de gerenciamento de saudação talvez não consigam por um determinado período de tempo durante a migração de saudação. No entanto, o plano de dados Olá continua toowork. Ou seja, os aplicativos em execução em máquinas virtuais (clássicos) não incorrerá em tempo de inatividade durante a migração de saudação.

Olá configurações a seguir não têm suporte no momento. Se o suporte é adicionado Olá futuras, algumas VMs nessa configuração podem incorrer em tempo de inatividade (vá por meio de parada, desalocar e reiniciar as operações de VM).

* Você tem mais de um conjunto de disponibilidade em um único serviço de nuvem.
* Você tem um ou mais conjuntos de disponibilidade e as VMs que não estão em um conjunto de disponibilidade em um único serviço de nuvem.

> [!NOTE]
> Nesse escopo de migração, o plano de gerenciamento Olá talvez não consigam por um período de tempo durante a migração de saudação. Para algumas configurações, conforme descrito acima, ocorre tempo de inatividade do plano de dados.
>
>

### <a name="storage-accounts-migration"></a>Migração das contas de armazenamento
migração direta do tooallow, você pode implantar máquinas virtuais do Gerenciador de recursos em uma conta de armazenamento clássicos. Com essa funcionalidade, recursos de computação e rede podem e devem ser migrados independentemente de contas de armazenamento. Depois de migrar seu máquinas virtuais e a rede Virtual, você precisa toomigrate sobre o processo de migração do armazenamento contas toocomplete hello.

> [!NOTE]
> modelo de implantação do Gerenciador de recursos de saudação não tem o conceito de saudação do clássico imagens e discos. Quando a conta de armazenamento Olá é migradas, clássicas imagens e discos não são visíveis na pilha do Gerenciador de recursos de saudação mas Olá fazendo VHDs permanecem na conta de armazenamento hello.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Recursos desanexados (Grupos de Segurança de Rede, Tabelas de Rotas e IPs Reservados)
Grupos de segurança de rede, tabelas de rotas e IPs reservados que não estão anexados tooany máquinas virtuais e redes virtuais podem ser migradas de forma independente.

<br>

## <a name="unsupported-features-and-configurations"></a>Recursos e configurações sem suporte
No momento, não oferecemos suporte para alguns recursos e configurações. Olá seções a seguir descreve nossas recomendações ao redor deles.

### <a name="unsupported-features"></a>Recursos sem suporte
Olá recursos a seguir não têm suporte no momento. Se desejar remover essas configurações, migrar VMs hello e, em seguida, reabilitar as configurações de saudação no modelo de implantação do Gerenciador de recursos de saudação.

| Provedor de recursos | Recurso | Recomendações |
| --- | --- | --- |
| Computação |Discos de máquina virtual não associados. | blobs VHD Olá por trás desses discos serão serão migrados quando é migrada Olá conta de armazenamento |
| Computação |Imagens de máquinas virtuais. | blobs VHD Olá por trás desses discos serão serão migrados quando é migrada Olá conta de armazenamento |
| Rede |ACLs de ponto de extremidade. | Remova as ACLs de Ponto de Extremidade e repita a migração. |
| Rede |Rede virtual com o Gateway de ExpressRoute e Gateway de VPN  | Remover Olá Gateway VPN antes de iniciar a migração e recrie Olá Gateway VPN após a conclusão da migração. Saiba mais sobre a [migração do ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Rede |ExpressRoute com links de autorização  | Remover conexão de rede de toovirtaul Olá rota expressa circuito antes do início da migração e, em seguida, recrie a conexão Olá após a conclusão da migração. Saiba mais sobre a [migração do ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Rede |Gateway de Aplicativo | Remover Olá Application Gateway antes de iniciar a migração e recrie Olá Application Gateway após a conclusão da migração. |
| Rede |Redes virtuais usando Emparelhamento VNet. | Migrar a rede Virtual tooResource Manager e, em seguida, ponto a ponto. Saiba mais sobre [Emparelhamento de VNet](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Configurações sem suporte
Olá configurações a seguir não têm suporte no momento.

| O Barramento de | Configuração | Recomendações |
| --- | --- | --- |
| Gerenciador de Recursos |RBAC (Controle de Acesso Baseado em Função) para recursos clássicos |Porque Olá URI dos recursos de saudação é modificado após a migração, é recomendável que você planejar atualizações de política RBAC Olá que precisam toohappen após a migração. |
| Computação |Várias sub-redes associadas a uma VM |Atualize Olá sub-rede configuração tooreference somente sub-redes. |
| Computação |Máquinas virtuais que pertencem a rede virtual tooa mas não tem uma sub-rede explícita atribuída |Opcionalmente, você pode excluir Olá VM. |
| Computação |Máquinas virtuais que têm alertas e políticas de Escala Automática |migração de saudação atravessa e essas configurações serão descartadas. É altamente recomendável que você avaliar seu ambiente antes de você Olá migração. Como alternativa, você pode reconfigurar as configurações de alerta Olá após a conclusão da migração. |
| Computação |Extensões de VM do XML (BGInfo 1.*, Depurador, Implantação da Web e Depuração Remota do Visual Studio) |Não há suporte para isso. É recomendável que você remova essas extensões de toocontinue migração da máquina virtual de saudação ou eles serão removidos automaticamente durante o processo de migração hello. |
| Computação |Diagnóstico de inicialização com o armazenamento Premium |Desabilite o recurso de diagnóstico de inicialização para Olá VMs antes de continuar com a migração. Você pode habilitar o diagnóstico de inicialização na pilha do Gerenciador de recursos de saudação novamente após a conclusão da migração de saudação. Além disso, os blobs que estão sendo usados para captura de tela e logs seriais devem ser excluídos para que você não seja cobrado por eles. |
| Computação |Serviços de nuvem que contêm funções de trabalho/web |Não há suporte para esse recurso no momento. |
| Rede |Redes virtuais que contêm máquinas virtuais e funções de trabalho/web |Não há suporte para esse recurso no momento. |
| Serviço de aplicativo do Azure |Redes virtuais que contêm ambientes do Serviço de Aplicativo |Não há suporte para esse recurso no momento. |
| Azure HDInsight |Redes virtuais que contêm serviços do HDInsight |Não há suporte para esse recurso no momento. |
| Serviços de Ciclo de Vida do Microsoft Dynamics |Redes virtuais que contêm máquinas virtuais gerenciadas pelos Serviços de Ciclo de Vida do Microsoft Dynamics |Não há suporte para esse recurso no momento. |
| Azure AD Domain Services |Redes virtuais que contêm serviços do Azure AD Domain Services |Não há suporte para esse recurso no momento. |
| RemoteApp do Azure |Redes virtuais que contêm implantações do Azure RemoteApp |Não há suporte para esse recurso no momento. |
| Gerenciamento de API do Azure |Redes virtuais que contêm implantações do Gerenciamento de API do Azure |Não há suporte para esse recurso no momento. Olá toomigrate IaaS VNET, altere Olá VNET de saudação implantação de gerenciamento de API que é uma operação de tempo de inatividade não. |
| Computação |Extensões da Central de Segurança do Azure com uma VNET que tenha um gateway de VPN em conectividade de trânsito ou um gateway de ExpressRoute com o servidor DNS local |Central de segurança do Azure instala extensões em seu toomonitor de máquinas virtuais de segurança e gerar alertas automaticamente. Essas extensões geralmente são instaladas automaticamente se Olá política Central de segurança do Azure está habilitado na assinatura de saudação. Migração do gateway de ExpressRoute não é tem suporte atualmente e os gateways de VPN com conectividade de trânsito perdem o acesso local. Excluir rota expressa gateway ou migrando gateway VPN com conectividade de trânsito faz com que toobe internet acesso tooVM armazenamento conta perdido quando continuando com a confirmação de migração de saudação. migração de saudação não continuará quando isso acontece como blob de status do agente de convidado de saudação não pode ser preenchida. É recomendável toodisable política Central de segurança do Azure na assinatura Olá 3 horas antes de continuar com a migração. |

