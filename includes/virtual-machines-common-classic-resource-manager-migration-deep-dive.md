## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Significado da migração de recursos de IaaS de tooResource de modelo de implantação clássico Olá Manager
Antes que podemos fazer drill down nos detalhes de Olá, vamos examinar diferença Olá entre operações de dados e de plano de gerenciamento nos recursos de IaaS hello.

* *Plano de gerenciamento para o controle* descreve chamadas Olá que entram em plano de gerenciamento para o controle de saudação ou Olá API para modificar recursos. Por exemplo, operações como criar uma VM, reiniciar uma máquina virtual e atualizar uma rede virtual com uma nova sub-rede gerenciam Olá executando recursos. Eles não afetam diretamente a instâncias de toohello conexão.
* *Plano de dados* (aplicativo) descreve o tempo de execução de saudação do próprio aplicativo hello e envolve a interação com as instâncias que não passam pelo Olá API do Azure. Acessar seu site ou efetuar pull de dados de uma instância do SQL Server ou servidor MongoDB em execução seriam considerados um plano de dados ou uma interação com o aplicativo. Copiando um blob de uma conta de armazenamento e acessando um tooRDP de endereço IP público ou o SSH na máquina virtual de saudação também são o plano de dados. Essas operações mantêm o aplicativo de saudação em execução em computação, rede e armazenamento.

Em segundo plano hello, plano de dados Olá é Olá mesmo entre Olá modelo de implantação clássico e a pilha do Gerenciador de recursos. Durante o processo de migração, podemos Converter representação Olá de recursos de saudação de toothat de modelo de implantação Olá clássico na pilha do Gerenciador de recursos de saudação. Como resultado, você precisará toouse novas ferramentas, APIs, SDKs toomanage seus recursos na pilha do Gerenciador de recursos de saudação.

![A captura de tela que ilustra a diferença entre o plano de gerenciamento/controle e o plano de dados](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> Em alguns cenários de migração, Olá plataforma Windows Azure interrompe desaloca e reinicia as máquinas virtuais. Isso acarreta um curto tempo de inatividade do plano de dados.
>

## <a name="hello-migration-experience"></a>experiência de migração de saudação
Antes de começar a experiência de migração Olá, é recomendável seguir hello:

* Certifique-se de que recursos Olá que você deseja toomigrate não usam quaisquer recursos sem suporte ou configurações. Geralmente plataforma Olá detecta esses problemas e gera um erro.
* Se você tiver VMs que não estão em uma rede virtual, ele serão interrompidos e desalocados como parte da saudação de operação de preparação. Se você não quiser o endereço IP público de saudação toolose, olhando para reservar o endereço IP de saudação antes de disparar Olá operação de preparação. No entanto, se Olá VMs estiverem em uma rede virtual, eles não são interrompidos e desalocados.
* Planeje a migração durante o horário comercial tooaccommodate falhas inesperadas que podem ocorrer durante a migração.
* Baixe a configuração atual Olá das suas máquinas virtuais usando o PowerShell, comandos de interface de linha de comando (CLI) ou APIs REST toomake mais fácil para validação após a etapa de preparação de saudação for concluída.
* Atualize seu modelo de implantação de automação/operacionalização scripts toohandle Olá Gerenciador de recursos antes de iniciar a migração de saudação. Opcionalmente, você pode fazer as operações GET quando recursos de saudação estiverem em Olá preparado estado.
* Avalie políticas RBAC Olá configuradas nos recursos de IaaS clássicos hello e planejar após a conclusão da migração de saudação.

fluxo de trabalho de migração de saudação é da seguinte maneira

![Captura de tela que mostra o fluxo de trabalho de migração de saudação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Todas as operações de saudação descritas nas seções a seguir de saudação são idempotentes. Se você tiver um problema que não seja um recurso sem suporte ou um erro de configuração, é recomendável que você repita Olá preparar, anular ou confirmar a operação. Olá plataforma Windows Azure tenta novamente a ação de saudação.
>
>

### <a name="validate"></a>Validar
Olá validar a operação é Olá primeira etapa no processo de migração de saudação. objetivo Olá desta etapa é o estado de saudação de tooanalyze de recursos de saudação que desejar toomigrate no modelo de implantação clássico hello e retorna êxito/falha se houver recursos Olá capazes de migração.

Você selecionar um serviço de nuvem ou de rede virtual hello (se não estiver em uma rede virtual) que você deseja toovalidate para migração.

* Se o recurso de saudação não é capaz de migração, Olá plataforma Windows Azure lista todos os motivos de saudação de por que não há suporte para migração.

#### <a name="checks-not-done-in-validate"></a>Verificações não realizadas em Validar

Validar operação apenas analisa o estado de saudação de recursos de Olá no modelo de implantação clássico hello. Ele pode verificar todas as falhas e cenários sem suporte devido a configurações de toovarious no modelo de implantação clássico hello. Não é possível toocheck para todos os problemas que Olá pilha pode impor recursos Olá durante a migração do Azure Resource Manager. Esses problemas só são verificados quando recursos Olá passar por uma transformação na próxima etapa de saudação da migração, ou seja, de preparação. Olá tabela a seguir lista todos os problemas de saudação não marcados em validar.


|Verificações de rede que não estão em Validar|
|-|
|Uma Rede Virtual com gateways ER e VPN|
|Uma conexão de gateway de Rede Virtual em estado desconectado|
|Todos os circuitos ER são pré-migrados tooAzure pilha de Gerenciador de recursos|
|Verificações de cota do Azure Resource Manager para recursos de Rede, ou seja, IP Público Estático, IPs Públicos Dinâmicos, Balanceador de Carga, Grupos de Segurança de Rede, Tabelas de Rotas, Interfaces de Rede |
| Verifique se todas as regras de balanceador de carga são válidas para a implantação/rede virtual |
| Verificar IPs privados conflitantes entre as máquinas virtuais interrompidas desalocadas em Olá mesmo VNET |

### <a name="prepare"></a>Preparar
operação de preparação de saudação é Olá segunda etapa no processo de migração de saudação. objetivo Olá desta etapa é toosimulate transformação Olá Olá recursos de IaaS de recursos do Gerenciador de tooResource de modelo de implantação clássico e apresentar isso lado a lado para que você toovisualize.

> [!NOTE] 
> Os recursos para Clássico não são modificados durante esta etapa. Portanto, é uma etapa seguro toorun se você estiver tentando migração. 

Você selecionar Olá virtual rede ou hello serviço de nuvem (se não for uma rede virtual) que você deseja tooprepare para migração.

* Se o recurso de saudação não é capaz de migração, Olá plataforma Windows Azure interrompe o processo de migração de saudação e motivo Olá por Olá preparar Falha na operação de lista.
* Se o recurso de saudação é capaz de migração, Olá plataforma Windows Azure pela primeira vez bloqueia operações de plano de gerenciamento de saudação para recursos de saudação na migração. Por exemplo, você não é capaz tooadd tooa um disco de dados VM em migração.

Olá plataforma Windows Azure, em seguida, inicia Olá migração de metadados do modelo de implantação clássico tooResource Manager para Olá migrar recursos.

Depois de preparar Olá operação for concluída, você tem a opção de saudação de recursos de saudação no modelo de implantação clássico e o Gerenciador de recursos de visualização. Para cada serviço de nuvem no modelo de implantação clássico hello, hello plataforma Windows Azure cria um nome de grupo de recursos que tem saudação padrão `cloud-service-name>-Migrated`.

> [!NOTE]
> Ele não é possível tooselect Olá nome do grupo de recursos criado para recursos migrados (ou seja, "-migrados"), mas após a conclusão da migração, você pode usar o Gerenciador de recursos do Azure move recursos toomove recursos tooany grupo de recursos que você deseja. tooread mais sobre isso, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../articles/resource-group-move-resources.md)

Aqui estão duas telas que mostram o resultado de saudação após uma operação de preparação bem-sucedida. Primeira tela mostra um grupo de recursos que contém o serviço de nuvem Olá original. Segunda tela mostra Olá novo "-migrados" grupo de recursos que contém recursos do Azure Resource Manager equivalentes de saudação.

![Captura de tela que mostra o serviço de nuvem clássico do Portal](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Captura de tela que mostra os recursos do Azure Resource Manager no Portal em Preparação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Aqui está uma olhada bastidores seus recursos após a conclusão de saudação da fase de preparação. Observe que o recurso de saudação é plano de dados Olá é Olá mesmo. Ele é representado no plano de gerenciamento de saudação (modelo de implantação clássico) e o plano de controle de saudação (Gerenciador de recursos).

![Em segundo plano da saudação na fase de preparação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> As Máquinas Virtuais que não estão em uma Rede Virtual clássica são interrompidas e desalocadas nesta fase da migração.
>

### <a name="check-manual-or-scripted"></a>Verificação (manual ou com scripts)
Na etapa de verificação Olá, você pode usar, opcionalmente, configuração de Olá que baixou toovalidate anterior que migração Olá parece correta. Como alternativa, você pode entrar em toohello portal e o ponto de verificação Olá propriedades e recursos toovalidate que a migração de metadados parece bom.

Se estiver migrando uma rede virtual, a maior parte da configuração das máquinas virtuais não é reiniciada. Para aplicativos nessas VMs, você pode validar que o aplicativo hello é ainda em execução.

Você pode testar seu monitoramento/automação e scripts operacionais toosee se Olá VMs estiverem funcionando conforme o esperado e se seus scripts atualizados funcionam corretamente. Somente operações GET têm suporte quando há recursos de Olá Olá preparado estado.

Não há nenhuma janela de tempo de conjunto antes que você precisará de migração de saudação toocommit. Você pode levar tanto tempo quanto desejar nesse estado. No entanto, o plano de gerenciamento hello está bloqueado para esses recursos até que você anulada ou confirmada.

Se você encontrar problemas, sempre pode anular migração hello e voltar toohello modelo de implantação clássico. Depois de você voltar, Olá plataforma Windows Azure abrirá operações do plano de gerenciamento de saudação nos recursos de saudação para que você possa retomar operações normais nessas VMs no modelo de implantação clássico hello.

### <a name="abort"></a>Anular
Anular é uma etapa opcional que você pode usar toorevert seu modelo de implantação clássico toohello alterações e interromper a migração de saudação. Essa operação exclui Olá metadados de Gerenciador de recursos para os recursos que foi criado na etapa de preparação anterior hello. 

![Em segundo plano da saudação na fase de anulação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Esta operação não pode ser executada depois de você ter disparado operação de confirmação de saudação.     
>

### <a name="commit"></a>Confirmar
Depois de concluir a validação de saudação, você poderá confirmar migração hello. Recursos não aparecerá mais no modelo de implantação clássico e estão disponíveis apenas no modelo de implantação do Gerenciador de recursos de saudação. Olá recursos migrados podem ser gerenciados apenas no novo portal de saudação.

> [!NOTE]
> Esta é uma operação idempotente. Se ele falhar, é recomendável que você repita a operação de saudação. Se ele persistir toofail, crie um tíquete de suporte ou criar um fórum post com uma marca de ClassicIaaSMigration em nossa [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Em segundo plano da saudação na fase de confirmação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Onde toobegin migração?

Aqui está um fluxograma que mostra como tooproceed com a migração

![Captura de tela que mostra as etapas de migração de saudação](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Conversão de recursos de Gerenciador de recursos de tooAzure de modelo de implantação clássico
Você pode encontrar o modelo de implantação clássico hello e representações de Gerenciador de recursos de recursos de saudação em Olá a tabela a seguir. Atualmente, não há suporte para outros recursos e funcionalidades.

| Representação do clássico | Representação do Gerenciador de Recursos | Anotações detalhadas |
| --- | --- | --- |
| Nome do serviço de nuvem |Nome DNS |Durante a migração, um novo grupo de recursos é criado para cada serviço de nuvem com o padrão de nomenclatura Olá `<cloudservicename>-migrated`. Esse grupo de recursos contém todos os seus recursos. nome do serviço de nuvem Olá torna-se um nome DNS que está associado ao endereço IP público de saudação. |
| Máquina virtual |Máquina virtual |As propriedades específicas da VM são migradas sem alterações. Certas informações osProfile, como o nome do computador, não são armazenadas no modelo de implantação clássico hello e permanecerá vazias após a migração. |
| Recursos de disco anexado tooVM |TooVM implícita discos anexados |Discos não são modelados como recursos de nível superior no modelo de implantação do Gerenciador de recursos de saudação. Eles são migrados como discos implícita em Olá VM. Somente os discos que estão anexados tooa atualmente há suporte para a VM. Máquinas virtuais do Gerenciador de recursos agora pode usar contas de armazenamento clássico, que permite facilmente migrados Olá discos toobe sem nenhuma atualização. |
| Extensões de VM |Extensões de VM |Todas as extensões de recurso hello, exceto extensões XML, são migradas do modelo de implantação clássico hello. |
| Certificados de máquina virtual |Certificados no Cofre da Chave do Azure |Se um serviço de nuvem contém certificados de serviço, um novo cofre de chaves do Azure por serviço de nuvem e move os certificados de saudação no cofre de chaves hello. Olá VMs são tooreference atualizado Olá certificados de Cofre de chaves hello. <br><br> **Observação:** não excluir Olá keyvault como ele pode causar Olá VM toogo em um estado de falha. Estamos trabalhando para melhorar as coisas em Olá back-end para que possa ser excluídos com segurança ou movidos juntamente com hello nova assinatura do VM tooa cofres de chaves. |
| Configuração do WinRM |Configuração do WinRM em osProfile |Configuração do gerenciamento remoto é movida do Windows inalterados, como parte da migração de saudação. |
| Propriedade do conjunto de disponibilidade |Recurso do conjunto de disponibilidade | Especificação de conjunto de disponibilidade foi uma propriedade em Olá VM no modelo de implantação clássico hello. Conjuntos de disponibilidade se tornar um recurso de nível superior como parte da migração de saudação. Olá seguintes configurações não são suportadas: vários conjuntos de disponibilidade por serviço de nuvem, ou um ou mais disponibilidade juntamente com máquinas virtuais que não estão em qualquer conjunto de disponibilidade em um serviço de nuvem. |
| Configuração de rede em uma VM |Interface de rede primária |Configuração de rede em uma máquina virtual é representada como recursos de interface de rede primária Olá após a migração. Para VMs que não estão em uma rede virtual, o endereço IP interno de saudação alterações durante a migração. |
| Várias interfaces de rede em uma VM |Interfaces de rede |Se uma VM tem várias interfaces de rede associados a ele, cada interface de rede se torna um recurso de nível superior como parte da migração de saudação do modelo de implantação do Gerenciador de recursos de hello, juntamente com todas as propriedades de saudação. |
| Conjunto de pontos de extremidade com balanceamento de carga |Balanceador de carga |No modelo de implantação clássico Olá, plataforma Olá atribuído um balanceador de carga implícita para cada serviço de nuvem. Durante a migração, é criado um novo recurso de Balanceador de carga e conjunto de ponto de extremidade de balanceamento de carga Olá torna-se em regras de Balanceador de carga. |
| Regras NAT de entrada |Regras NAT de entrada |Pontos de extremidade de entrada definidos no hello VM são regras de conversão de endereços de rede convertido tooinbound sob o balanceador de carga Olá durante a migração de saudação. |
| Endereço VIP |Endereço IP público com o nome DNS |endereço IP virtual Olá torna-se um endereço IP público e está associado ao balanceador de carga de saudação. Um IP virtual só pode ser migrado se houver um ponto de extremidade de entrada atribuído tooit. |
| Rede virtual |Rede virtual |rede virtual Olá é migrado, com todas as suas propriedades, modelo de implantação do Gerenciador de recursos de toohello. Um novo grupo de recursos é criado com o nome da saudação `-migrated`. |
| IPs Reservados |Endereço IP público com método de alocação estático |IPs reservados associado com o balanceador de carga Olá são migradas, junto com a migração de saudação do serviço de nuvem hello ou máquina virtual de saudação. No momento, não há suporte para a migração de IP reservado não associado. |
| Endereço IP público por VM |Endereço IP público com método de alocação dinâmico |Olá endereço IP público associado Olá que VM é convertida como um recurso de endereço IP público, com hello toostatic de conjunto de método de alocação. |
| NSGs |NSGs |Grupos de segurança de rede associados a uma sub-rede são clonados como parte do modelo de implantação do Gerenciador de recursos do hello migração toohello. Olá NSG no modelo de implantação clássico Olá não é removido durante a migração de saudação. No entanto, as operações do plano de gerenciamento de Olá para Olá NSG são bloqueadas quando Olá migração está em andamento. |
| Servidores DNS |Servidores DNS |Servidores DNS associados a uma rede virtual ou Olá VM são migradas como parte da migração do recurso correspondente hello, juntamente com todas as propriedades de saudação. |
| UDRs |UDRs |Rotas definidas pelo usuário associadas a uma sub-rede são clonadas como parte do modelo de implantação do Gerenciador de recursos do hello migração toohello. Olá UDR no modelo de implantação clássico Olá não é removido durante a migração de saudação. operações do plano de gerenciamento de saudação para Olá UDR são bloqueadas quando Olá migração está em andamento. |
| Propriedade de encaminhamento IP em uma configuração de rede da VM |Propriedade Olá NIC de encaminhamento de IP |propriedade de encaminhamento de IP de saudação em uma máquina virtual é propriedade de tooa convertido na interface de rede Olá durante a migração de saudação. |
| Balanceador de carga com vários IPs |Balanceador de carga com vários recursos IP públicos |Cada IP público associado com o balanceador de carga Olá é convertido tooa recurso IP público e associado ao balanceador de carga Olá após a migração. |
| Nomes de DNS internos na Olá VM |Nomes de DNS internos na Olá NIC |Durante a migração, sufixos DNS internos Olá para VMs Olá são migrados tooa propriedade somente leitura denominada "InternalDomainNameSuffix" em Olá NIC. sufixo de saudação permanece inalterado após a migração e a resolução VM deve continuar toowork como anteriormente. |
| Gateway de Rede Virtual |Gateway de Rede Virtual |As propriedades do Gateway de Rede Virtual são migradas sem alterações. Olá VIP associada Olá gateway não altera qualquer um. |
| Site de rede local |Gateway de Rede Local |Propriedades do site de rede local são migrados tooa inalterado novo recurso chamado Gateway de rede Local. Ele representa prefixos de endereço local e o IP do gateway remoto. |
| Referências de conexões |Conexão |Referências de conectividade entre o gateway e o site de rede local na configuração de rede é representado por um recurso recém-criado chamado Conexão, no Resource Manager, após a migração. Todas as propriedades de referência de conectividade em arquivos de configuração de rede são recursos de Conexão copiada toohello inalterado recém-criado. Rede virtual tooVNet conectividade em clássico é obtida criando dois túneis IPsec toolocal sites de rede que representa a saudação VNets. Isso é transformado tooVnet2Vnet conexão tipo no modelo do Gerenciador de recursos sem a necessidade de gateways de rede local. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Automação de tooyour alterações e ferramentas após a migração
Como parte da migração de seus recursos do modelo de implantação do hello clássico implantação modelo toohello Gerenciador de recursos, você deve ter um tooupdate sua automação existentes ou ferramentas tooensure que ele continue toowork após a migração de saudação.
